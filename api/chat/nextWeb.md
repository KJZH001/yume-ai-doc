# 在线可视化的大语言面板
为了便于一些用户能够更加方便的在线使用，以及在手机等移动设备上使用它

我们搭建了一个魔改的ChatGPT-Next-Web的在线版本，你可以在这里使用它：

[https://moechat.moeworld.top/](https://moechat.moeworld.top/)

## 开始使用
在您开始使用之前，你需要对面板进行一些配置，这些配置将会被保存在你的浏览器中，不会被上传到服务器

这也意味着，如果你更换了浏览器，或者清除了浏览器缓存，你的配置将会丢失

### 配置面板
在左下角有一个设置按钮，点击展开设置界面

你需要关注的有以下几个选项：

1.接口地址
2.API Key
3.自定义模型名称
4.模型(model)
5.注入系统级提示信息

#### 接口地址
这里你需要填写为
```
https://api.moeworld.top/api/openai/index.php?web=true&
```
不需要对地址做出任何的修改

#### API Key
这里你需要填写你的API Key，你可以在[这里](https://ai.moeworld.tech/page/dashboard)查看你的API Key

这里直接填写你在控制台拿到的key即可，没有MoeKey-或者sk-这些前缀标识头