# 技术介绍
> [!important]
> MCP，全称是Model Context Protocol，模型上下文协议，由Claude母公司Anthropic于去年11月正式提出。
> 
> ![](MCP.assets/a5eca16e9f67ab98d77f08b6d2fefedc_MD5.jpeg)
> 
> 总的来说，MCP解决的最大痛点，就是Agent开发中调用外部工具的技术门槛过高的问题。
> 
> ![](MCP.assets/29dbbdf711ab53feffe70b1d27193c42_MD5.jpeg)![](MCP.assets/71d9a55bd74c2f3dfd35316cfbc8726f_MD5.jpeg)

> [!example]
> ![](MCP.assets/eb1e313f13f992e698edfe9895cd6778_MD5.jpeg)![](MCP.assets/dde888651192904fd0df9477595c31f4_MD5.jpeg)



# MCP客户端Client开发流程
## uv 工具介绍与使用
> [!info]
> `MCP`开发要求借助uv进行虚拟环境创建和依赖管理。`uv` 是一个`Python` 依赖管理工具，类似于 `pip` 和 `conda`，但它更快、更高效，并且可以更好地管理 `Python` 虚拟环境和依赖项。它的核心目标是替代 `pip`、`venv` 和 `pip-tools`，提供更好的性能和更低的管理开销。

> [!important]
> uv 的特点：
> 1. 速度更快：相比 `pip`，`uv` 采用 Rust 编写，性能更优。
> 2. 支持 PEP 582：无需 virtualenv，可以直接使用 __pypackages__ 进行管理。
> 3. 兼容`pip`：支持 requirements.txt 和 pyproject.toml 依赖管理。
> 4. 替代`venv`：提供 uv venv 进行虚拟环境管理，比 venv 更轻量。
> 5. 跨平台：支持 Windows、macOS 和 Linux。


## uv安装流程
> [!def]
> ![](MCP.assets/1845ce0b318a24c6b152c1acfa1a7f20_MD5.jpeg)
```
pip install uv    # 方法一
curl -LsSf https://astral.sh/uv/install.sh | sh   # 方法二
```


## uv的基本用法介绍
> [!def]
> ![](MCP.assets/295e86d793ce3fb864c0f40e8303ad5f_MD5.jpeg)


# MCP极简客户端搭建流程
## 创建MCP客户端项目
> [!code]
> ![](MCP.assets/20204ad70a6d853ea20b1d70017cbf36_MD5.jpeg)
```bash
# 创建项目目录
uv init mcp-client
cd mcp-client
```


## 创建MCP客户端虚拟环境
> [!code] 创建虚拟环境
> ![](MCP.assets/ab6b5c2bb3fff16aaf675f42eaa6ccb4_MD5.jpeg)
```bash
# 创建虚拟环境
uv venv

# 激活虚拟环境
source .venv/bin.activate
```
> [!code]
> ![](MCP.assets/1d551f178b612df72a2541f074ced32a_MD5.jpeg)
```
# 安装 MCP SDK  
uv add mcp
```


## 编写基础MCP客户端
> [!code]
> ![](MCP.assets/4b17d111eb72108de9b9159e3d9fd907_MD5.jpeg)
```python
import asyncio
from mcp import ClientSession
from contextlib import AsyncExitStack

class MCPClient:
    def__init__(self):
        """初始化 MCP 客户端"""
        self.session = None
        self.exit_stack = AsyncExitStack()

    async def connect_to_mock_server(self):
        """模拟 MCP 服务器的连接（暂不连接真实服务器）"""
        print("✅ MCP 客户端已初始化，但未连接到服务器")

    async def chat_loop(self):
        """运行交互式聊天循环"""
        print("\nMCP 客户端已启动！输入 'quit' 退出")

        whileTrue:
            try:
                query = input("\nQuery: ").strip()
                if query.lower() == 'quit':
                    break
                print(f"\n🤖 [Mock Response] 你说的是：{query}")
            except Exception as e:
                print(f"\n⚠️ 发生错误: {str(e)}")

    asyncdefcleanup(self):
        """清理资源"""
        await self.exit_stack.aclose()

async def main():
    client = MCPClient()
    try:
        await client.connect_to_mock_server()
        await client.chat_loop()
    finally:
        await client.cleanup()

if __name__ == "__main__":
    asyncio.run(main())

```





