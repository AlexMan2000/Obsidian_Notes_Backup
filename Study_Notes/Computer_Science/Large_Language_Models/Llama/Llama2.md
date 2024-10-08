# Transformer and LLaMA
> [!important]
> ![](Llama2.assets/a3d3147e3f61dff2b41cf22861b20103_MD5.jpeg)








# 环境配置
> [!def]
> - `conda env create --file <filename.yml>`
> 
```yml
name: llama2-gpu  
channels:  
  - defaults  
  - nvidia  
dependencies:  
  - python==3.10  
  - nvidia::cuda-toolkit==12.1.1  
  - pip  
  - pip:  
    - -r requirements.txt
```
> [!code] Minimum Requirements
```txt
numpy  
scipy  
tqdm  
docopt  
nltk  
torchvision  
torch  
sentencepiece  
lxml==5.0.0  
sacrebleu  
tensorboard
```





