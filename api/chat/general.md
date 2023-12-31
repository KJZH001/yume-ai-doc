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

目前这个位置可以填写的值有`gpt`和`glm`，分别代表的是GPT和ChatGLM

其中，只有`https://ai.moeworld.tech/api/gpt/`这部分是必须的，`MoeKey-xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`和`chat/completions`是可选的，`chat/completions`是默认的请求路径，具体取决于你想要对接的程序

实际上，后面这部分是什么都无所谓，接口不会管你在后面究竟传入了什么东西，但是为了方便，我们还是建议你使用默认的请求路径

### 可选参数
这里有一个可用于获取计费情况的参数，你可以在请求路径的最后加上`?detail=true`来获取计费情况

例如，url应该是这样的
```url
https://ai.moeworld.tech/api/glm/MoeKey-xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/chat/completions?detail=true
```
这是预期返回的结果
```json
{
    "id": "chatcmpl-77PZm95TtxE0oYLRx3cxa6HtIDI7s",
    "object": "chat.completion",
    "created": 1682000966,
    "model": "gpt-3.5-turbo-0301",
    "usage": {
        "prompt_tokens": 0,
        "completion_tokens": 0,
        "total_tokens": 0
    },
    "choices": [
        {
            "message": {
                "role": "assistant",
                "content": "你好!请问有什么需要帮助的吗?"
            },
            "finish_reason": "stop",
            "index": 0
        }
    ]
}{
    "uuid": "xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "balance": 8.77,
    "fee": 0.05,
    "total_tokens": 0
}
```

比起默认的情况，多出了这么一段json

```json
{
    "uuid": "xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "balance": 8.77,
    "fee": 0.05,
    "total_tokens": 0
}
```
其中，`total_tokens`代表的是本次请求消耗的token数量，`fee`代表的是本次请求消耗的token数量乘以单价，`balance`代表的是你的账户余额

不同的模型计费情况会有所不同，具体请参考我们后续公布的计费文档

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

请注意，如果你在路由中包含了你的API Key，那么不管你在请求头中的Authorization传入了什么，都会被忽略

甚至Authorization都没有传入也是可以的

#### 使用Openai兼容的接口定义进行传参鉴权
请注意，接口的鉴权中，使用路由传参的优先级高于使用Openai兼容的接口定义进行传参，如果你想要使用这种方式进行鉴权，路径中不能够包含你的key

如果可以的话也请优先考虑使用路由传参的方式进行鉴权而不是这种兼容的接口定义进行传参的方式进行鉴权

如果你确实需要使用和Openai协议接口一致的鉴权方式，那么你可以优先考虑使用`聚合接口`，你可以目录中找到它

---

你的请求路径看上去应该是这样，比起另外一种方式少了一串key

```
https://ai.moeworld.tech/api/gpt/chat/completions
```

同样的，你需要为你的header里加入这么一串东西

```
Authorization: Bearer xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```
这里和Openai的协议接口定义保持一致，请注意，这里的key是没有`sk-`这个标识头的，也同样没有`MoeKey-`这个标识头

**后续我们可能会对key的表示头做出通用匹配以更好的解决兼容性问题，但目前还没有正式将此计划实现的打算**

## 请求体
这是一个和官方接口完全相同的实列
```
{
  "model": "gpt-3.5-turbo",
  "messages": [
    {
      "role": "user",
      "content": "你好！"
    }
  ]
}
```
请求的模型由`model`的值决定，如果是GLM模型，这个值不会起作用，但是你仍然需要传入这个值（可以随便填）

`messages`是一个数组，数组中的每一个元素都是一个对象，对象中包含两个属性，`role`和`content`

`role`可以是`user，assistant，system`，分别代表`用户，AI生成的内容和系统级别的提示（也就是你给AI的设定）`

如果你想要做出更细致的微调或者传递历史对话，可以修改`messages`的内容

具体的请查阅Openai官方的文档，这里不再赘述

## 响应内容
以下仅供参考，具体的响应内容取决于你的请求内容
```
{
    "id": "chatcmpl-7oqoflxUbLGTN6rWApmbCMjPX9Hzj",
    "object": "chat.completion",
    "created": 1692353781,
    "model": "gpt-35-turbo",
    "choices": [
        {
            "index": 0,
            "finish_reason": "stop",
            "message": {
                "role": "assistant",
                "content": "你好啊！有需要我帮忙的吗？"
            }
        }
    ],
    "usage": {
        "completion_tokens": 16,
        "prompt_tokens": 11,
        "total_tokens": 27
    }
}
```

## 注意
目前我们所有的接口均不支持流式传输

如果你强行启用它你只会得到一个一次性输出完毕的流式响应，这没有一点用处

这里讲的只是通用的大语言接口定义，每个模型不同的地方请查阅对应的文档