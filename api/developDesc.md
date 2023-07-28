# API统一格式
> 这里讲的是大部分服务的接口格式，不包括一些特殊的接口，比如登录接口和GPT接口，这些接口的格式会在各自的文档中说明。

## 基准路由
```https://ai.moeworld.tech/api/service/```

您在`概述`页面中看到的路由都是用于此基准路由之上的，例如`通用人脸检测`的子路由为`/image/general/human/face/det`

那么您的请求地址就应该是这样的：`https://ai.moeworld.tech/api/service/image/general/human/face/det`

## 请求方式
所有的接口都是使用`POST`请求，请求的`Content-Type`为`application/form`

## 请求参数
对于这些视觉图像分析的接口而言，请求的参数都是一样的

总共有两个参数，分别是`apikey`和`image`，其中`apikey`是您的API密钥，`image`是您要分析的图片

### ApiKey
您可以在控制台的仪表盘中找到它，注意不要将它泄露给任何人，包括站点管理员，因为管理员不会向您索要您的个人API密钥

### Image
图像需要使用base64编码，如果您在程序中调用，您可以使用任何语言的base64编码函数，例如在Python中您可以使用`base64.b64encode()`函数，如果您使用的是Java，那么您可以使用`Base64.getEncoder().encodeToString()`函数

原始图片可以是jpg格式或者png格式，对于这两种格式的图片，您都可以使用base64编码直接转换

但是请注意，请不要在提交的数据中包含`data:image/png;base64,`这样的标识头，这可能会导致程序意外的出错或无法正确分析识别

提交的数据看起来应该像这样
```base64
iVBORw0KGgoAAAANSUhEUgAABAAAAAKqCAYAAACkSiwxAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAAEnQAABJ0Ad5mH3gAAP+lSURBVHhe7P31m1tZlq2N9l908TvnuweaqruLK9EYHKEQh0KsEIeCOczMzMzMzGxn2k4no5MZatw55taSt+VwQlVlVXcd/zCezby3tN6x5prrH0aNfgbPj3oazz73Bzzz7O9VHH/u+ad0vllOcR6XP/3M71RPPf3bR9YdM/Y5jB33PMaNH4XxFaN1mvO5Htf/w1O/UXGc+7BvO3rMsw+p/
```
而不是这样
```base64
data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABAAAAAKqCAYAAACkSiwxAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAAEnQAABJ0Ad5mH3gAAP+lSURBVHhe7P31m1tZlq2N9l908TvnuweaqruLK9EYHKEQh0KsEIeCOczMzMzMzGxn2k4no5MZatw55taSt+VwQlVlVXcd/zCezby3tN6x5prrH0aNfgbPj3oazz73Bzzz7O9VHH/u+ad0vllOcR6XP/3M71RPPf3bR9YdM/Y5jB33PMaNH4XxFaN1mvO5Htf/w1O/UXGc+7BvO3rMsw+p/
```

> 这里的base64只是随便截取的一段，不是合法的base64编码图像

我们的程序会检查您提交的数据是否包含`data:image/png;base64,`这样的标识头，如果包含，那么程序会自动将其删除，但是这样做可能会导致程序无法正确分析识别，因为我们无法预料到你提交的标识头会是什么样的，也无法保证完全能够去除，所以请您在提交数据时注意这一点

## 返回数据

返回的数据将会是一段json字符串，您可以使用任何语言的json解析函数来解析它，或者如果你愿意的话，也可以选择直接使用字符串操作的方式进行分析（因为格式并不复杂）

---

成功处理的话返回的数据格式如下

```json
{
    "code": 1000, 
    "msg": "[INFO] success. __main__", 
    "result": [
        [
            {
                "bbox": [
                    87.8051986694336, 
                    203.67938232421875, 
                    139.88705444335938, 
                    262.81439208984375
                ], 
                "category": "face|wider", 
                "score": 0.8517948389053345
            }, 
        ]
    ]
}
```

其中`code`是状态码，`msg`是状态信息，`result`是返回的结果

---

如果处理失败的话返回的数据格式如下

```json
{
    "code": 1000, 
    "msg": "[INFO] success. __main__", 
    "result": null
}
```

其中`code`是状态码，`msg`是状态信息，`result`是返回的结果，这里的`result`是`null`，表示没有返回结果

## 备注
为了便于阅读，此处的返回数据格式是经过格式化的，实际返回的数据是没有格式化的，也就是说，返回的数据中不会有换行符和空格

如果您使用的是Python，那么您可以使用`json.dumps()`函数来格式化它，如果您使用的是Java，那么您可以使用`JSONObject.toString()`函数来格式化它