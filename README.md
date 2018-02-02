# MP-PUSH

开发此项目的目的是实现一个自己的“[Server酱](http://sc.ftqq.com/)”，方便自定义。

零痛苦部署，极度简单的API，代码开源，自由扩展。

## 准备好服务号或者测试号

如果注册不了服务号也一点关系没有，测试号完全可以满足个人使用的需求。打开[这里](https://mp.weixin.qq.com/debug/cgi-bin/sandbox?t=sandbox/login)进行注册。

先配置一个消息模板，需要带一个 `text` 字段。

## 没钱买服务器也没关系

LeanCloud 提供免费的后台托管，去[这里](https://leancloud.cn/dashboard/login.html#/signin)注册一个。

然后新建一个应用，在云引擎的设置里面添加自定义环境变量：

- `WX_APP_ID` 测试号 appID
- `WX_APP_SC` 测试号 appsecret
- `WX_TOKEN` 需和接口配置信息的 Token 一致
- `WX_TEMPLATE_ID` 新建的模板 ID
- `WX_TEMPLATE_DEST` 模板的详情要打开的 URL，目前可以瞎填

绑定一个二级域名

## 准备部署

首先确认本机已经安装 [Node.js](http://nodejs.org/) 运行环境和 [LeanCloud 命令行工具](https://leancloud.cn/docs/leanengine_cli.html)，然后执行下列指令：

```
$ git clone https://github.com/brucx/mp-push-leancloud.git
$ cd mp-push-leancloud
```

安装依赖：

```
npm install
```

登录并关联应用：

```
lean login
lean switch
```

部署到 LeanEngine：

```
lean deploy
```

## 确认接口配置信息

在[测试号管理](https://mp.weixin.qq.com/debug/cgi-bin/sandboxinfo?action=showinfo&t=sandbox/index)页面确认接口配置信息。

URL 为 `https://二级域名.leanapp.cn/wx`
Token 需和 `WX_TOKEN` 一致

## 关注测试号

公众号内发送 `link ${频道名称}` 绑定频道。
发送 POST 请求触发推送
```
POST /push HTTP/1.1
content-type: application/json

{
  "channelName": "频道名称",
  "text": "OK"
}
```

结束
