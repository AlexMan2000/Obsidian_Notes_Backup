# RAG with Agents - QA
## Environment Setup - Colab
> [!code]
```python
from google.colab import drive
drive.mount('/content/drive')

# Change the working directory to somewhere in your Google Drive.
# You could check the path by right clicking on the folder.
%cd "/content/drive/MyDrive/AI_Agents/mlhw1/"

!python3 -m pip install --no-cache-dir llama-cpp-python==0.3.4 --extra-index-url https://abetlen.github.io/llama-cpp-python/whl/cu122
!python3 -m pip install googlesearch-python bs4 charset-normalizer requests-html lxml_html_clean

  

from pathlib import Path
if not Path('./Meta-Llama-3.1-8B-Instruct-Q8_0.gguf').exists():
    !wget https://huggingface.co/bartowski/Meta-Llama-3.1-8B-Instruct-GGUF/resolve/main/Meta-Llama-3.1-8B-Instruct-Q8_0.gguf


if not Path('./public.txt').exists():
    !wget https://www.csie.ntu.edu.tw/~ulin/public.txt


if not Path('./private.txt').exists():
    !wget https://www.csie.ntu.edu.tw/~ulin/private.txt
```


## Prepare the LLM and LLM utility function
> [!code]
```python
from llama_cpp import Llama

# Load the model onto GPU
llama3 = Llama(
    "./Meta-Llama-3.1-8B-Instruct-Q8_0.gguf",
    verbose=False,
    n_gpu_layers=-1,
    n_ctx=16384,    # This argument is how many tokens the model can take. The longer the better, but it will consume more memory. 16384 is a proper value for a GPU with 16GB VRAM.
)

def generate_response(_model: Llama, _messages: str) -> str:
    '''
    This function will inference the model with given messages.
    '''
    _output = _model.create_chat_completion(
        _messages,
        stop=["<|eot_id|>", "<|end_of_text|>"],
        max_tokens=512,    # This argument is how many tokens the model can generate, you can change it and observe the differences.
        temperature=0,      # This argument is the randomness of the model. 0 means no randomness. You will get the same result with the same input every time. You can try to set it to different values.
        repeat_penalty=2.0,
    )["choices"][0]["message"]["content"]
    return _output
```


## Search Tool
> [!code]
```python
from typing import List
from googlesearch import search as _search
from bs4 import BeautifulSoup
from charset_normalizer import detect
import asyncio
from requests_html import AsyncHTMLSession
import urllib3
urllib3.disable_warnings()

async def worker(s:AsyncHTMLSession, url:str):
    try:
        header_response = await asyncio.wait_for(s.head(url, verify=False), timeout=10)
        if 'text/html' not in header_response.headers.get('Content-Type', ''):
            return None
        r = await asyncio.wait_for(s.get(url, verify=False), timeout=10)
        return r.text
    except:
        return None

async def get_htmls(urls):
    session = AsyncHTMLSession()
    tasks = (worker(session, url) for url in urls)
    return await asyncio.gather(*tasks)

async def search(keyword: str, n_results: int=3) -> List[str]:
    '''
    This function will search the keyword and return the text content in the first n_results web pages.

    Warning: You may suffer from HTTP 429 errors if you search too many times in a period of time. This is unavoidable and you should take your own risk if you want to try search more results at once.
    The rate limit is not explicitly announced by Google, hence there's not much we can do except for changing the IP or wait until Google unban you (we don't know how long the penalty will last either).
    '''
    keyword = keyword[:100]
    # First, search the keyword and get the results. Also, get 2 times more results in case some of them are invalid.
    results = list(_search(keyword, n_results * 2, lang="zh", unique=True))
    # Then, get the HTML from the results. Also, the helper function will filter out the non-HTML urls.
    results = await get_htmls(results)
    # Filter out the None values.
    results = [x for x in results if x is not None]
    # Parse the HTML.
    results = [BeautifulSoup(x, 'html.parser') for x in results]
    # Get the text from the HTML and remove the spaces. Also, filter out the non-utf-8 encoding.
    results = [''.join(x.get_text().split()) for x in results if detect(x.encode()).get('encoding') == 'utf-8']
    # Return the first n results.
    return results[:n_results]


# TESTING
# You can try out different questions here.
test_question='請問誰是 Taylor Swift？'

messages = [
    {"role": "system", "content": "你是 LLaMA-3.1-8B，是用來回答問題的 AI。使用中文時只會使用繁體中文來回問題。"},    # System prompt
    {"role": "user", "content": test_question}, # User prompt
]

print(generate_response(llama3, messages))
```



## Agents
> [!code]
> Agent class has the following attributes and methods:
> - **Attributes**:
> 	- **role_description**: The role of the agent. For example, if you want this agent to be a history expert, you can set the role_description to "You are a history expert. You will only answer questions based on what really happened in the past. Do not generate any answer if you don't have reliable sources.".
> 	- **task_description**: The task of the agent. For example, if you want this agent to answer questions only in yes/no, you can set the task_description to "Please answer the following question in yes/no. Explanations are not needed."
> 	- **llm**: Just an indicator of the LLM model used by the agent.
> - **Method**:
> 	- **inference**: This method takes a message as input and returns the generated response from the LLM model. The message will first be formatted into proper input for the LLM model. (This is where you can set some global instructions like "Please speak in a polite manner" or "Please provide a detailed explanation".) The generated response will be returned as the output.
```python
class LLMAgent():
    def __init__(self, role_description: str, task_description: str, llm:str="bartowski/Meta-Llama-3.1-8B-Instruct-GGUF"):
        self.role_description = role_description   # Role means who this agent should act like. e.g. the history expert, the manager......
        self.task_description = task_description    # Task description instructs what task should this agent solve.
        self.llm = llm  # LLM indicates which LLM backend this agent is using.
    def inference(self, message:str) -> str:
        if self.llm == 'bartowski/Meta-Llama-3.1-8B-Instruct-GGUF': # If using the default one.
            # TODO: Design the system prompt and user prompt here.
            # Format the messsages first.
            messages = [
                {"role": "system", "content": f"{self.role_description}"},  # Hint: you may want the agents to speak Traditional Chinese only.
                {"role": "user", "content": f"{self.task_description}\n{message}"}, # Hint: you may want the agents to clearly distinguish the task descriptions and the user messages. A proper seperation text rather than a simple line break is recommended.
            ]
            return generate_response(llama3, messages)
        else:
            # TODO: If you want to use LLMs other than the given one, please implement the inference part on your own.
            return ""
```


## RAG Pipeline
> [!code]
```python
async def pipeline(question: str) -> str:
    # TODO: Implement your pipeline.
    # Currently, it only feeds the question directly to the LLM.
    # You may want to get the final results through multiple inferences.
    extracted_question = question_extraction_agent.inference(question)
    extracted_keywords = keyword_extraction_agent.inference(extracted_question)
    results = await search(extracted_keywords, 1)
    results = '\n'.join(results)
    # summarized_results = search_result_summarize_agent.inference(results)
    print(len(summarized_results))
    user_prompt = "Background:\n" + results + "\nQuestion:" + extracted_question + "\nA:"
    # Just a quick reminder, make sure your input length is within the limit of the model context window (16384 tokens), you may want to truncate some excessive texts.
    return qa_agent.inference(user_prompt)
```
