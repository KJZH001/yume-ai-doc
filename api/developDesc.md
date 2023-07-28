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

但是请注意，请不要在提交的数据中包含`data:image/png;base64,`这样的标识头

提交的数据看起来应该像这样
```
iVBORw0KGgoAAAANSUhEUgAABAAAAAKqCAYAAACkSiwxAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAAEnQAABJ0Ad5mH3gAAP+lSURBVHhe7P31m1tZlq2N9l908TvnuweaqruLK9EYHKEQh0KsEIeCOczMzMzMzGxn2k4no5MZatw55taSt+VwQlVlVXcd/zCezby3tN6x5prrH0aNfgbPj3oazz73Bzzz7O9VHH/u+ad0vllOcR6XP/3M71RPPf3bR9YdM/Y5jB33PMaNH4XxFaN1mvO5Htf/w1O/UXGc+7BvO3rMsw+p/
```
而不是这样
```
data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABAAAAAKqCAYAAACkSiwxAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAAEnQAABJ0Ad5mH3gAAP+lSURBVHhe7P31m1tZlq2N9l908TvnuweaqruLK9EYHKEQh0KsEIeCOczMzMzMzGxn2k4no5MZatw55taSt+VwQlVlVXcd/zCezby3tN6x5prrH0aNfgbPj3oazz73Bzzz7O9VHH/u+ad0vllOcR6XP/3M71RPPf3bR9YdM/Y5jB33PMaNH4XxFaN1mvO5Htf/w1O/UXGc+7BvO3rMsw+p/
```
