# 大语言模型
这篇文档主要会介绍关于大语言模型的通用接口的一些基本用法


## 模型介绍
目前主要包含两大类型模型，分别为来自Openai的GPT和清华大学国产的ChatGLM

GPT当前主要支持ChatGPT(GPT-3.5)，使用自部署的聚合后端接口对接Azure Openai认知服务

ChatGLM使用的是ChatGLM6B的int4量化模式运行，效果目前不如ChatGPT，但是完全自行部署，具有更好的安全性和隐私性

## 接口定义
以ChatGPT为例，你可以在[这里](https://ai.moeworld.tech/chat/gpt)查看接口的大致定义和在线调试


### 请求路径
```
https://ai.moeworld.tech/api/gpt/MoeKey-xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/chat/completions
```
你在控制台上会看到类似这样的请求路径，其中`MoeKey-xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`是你的API Key，你可以在[这里](https://ai.moeworld.tech/page/dashboard)查看你的API Key

其中，只有`https://ai.moeworld.tech/api/gpt/`这部分是必须的，`MoeKey-xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`和`chat/completions`是可选的，`chat/completions`是默认的请求路径，具体取决于你想要对接的程序

实际上，后面这部分是什么都无所谓，接口不会管你在后面究竟传入了什么东西，但是为了方便，我们还是建议你使用默认的请求路径