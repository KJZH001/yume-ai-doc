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

`gpt`参数代表的是你请求的模型的类别，**注意是类别**

目前这个位置可以填写的值有`gpt`和`chat`，分别代表的是GPT和ChatGLM

其中，只有`https://ai.moeworld.tech/api/gpt/`这部分是必须的，`MoeKey-xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`和`chat/completions`是可选的，`chat/completions`是默认的请求路径，具体取决于你想要对接的程序

实际上，后面这部分是什么都无所谓，接口不会管你在后面究竟传入了什么东西，但是为了方便，我们还是建议你使用默认的请求路径

### 鉴权方式
正如你所看到的完整请求路径，我们使用的是API Key作为请求路由的一部分的方式进行鉴权，你可以在[这里](https://ai.moeworld.tech/page/dashboard)查看你的API Key

这是考虑到有些程序可能不支持在请求头中传入鉴权信息，或者是强制要求使用Authorization: Bearer sk-xxx的格式

为了防止出现格式上出现预期之外的情况，所以我们使用了这种方式进行鉴权

毕竟，大多数程序当中，请求的路径是可以被随便修改的，而请求头却不是，甚至你可能还需要和格式斗智斗勇一番

比如，要不要加Bearer？或者，程序只为了对接Openai官方的API，而不是对接其他的API

所以强制帮你在key上塞了个sk-，但是你的key里又没有sk这么个标识头，这就很尴尬了

#### 使用路由传参鉴权
```
https://ai.moeworld.tech/api/gpt/MoeKey-xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/chat/completions
```
这是我们的完整请求路径，其中`MoeKey-xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`是你的API Key

你可以在[这里](https://ai.moeworld.tech/page/dashboard)查看你的API Key

请不要感到疑惑，你在控制台上看到的key是没有`MoeKey-`这串标识头的，但是你在请求路径中需要加上这串标识头

