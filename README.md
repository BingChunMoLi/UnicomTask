

### 2.准备需要的参数

手机号、服务密码、`appId`。

其中`appId`的获取:

+ 安卓用户可在文件管理 --> `Unicom/appid` 文件中获取。

+ 苹果用户可抓取客户端登录接口获取。
> `https://m.client.10010.com/mobileService/login.htm`
 
### 3.将参数填到Secrets

在`Secrets`中的`Name`和`Value`格式如下：

Name | Value
-|-|-
USERS_COVER | config.json中内容

将`config.json`中内容复制下来，按照要求填写添加到`Secrets`中，如若选填内容不想配置，需将该项留空。如只想基本功能，无需通知和用积分抽奖，应填写如下内容：

```json
[
    {
        "username": "18566669999",
        "password": "123456",
        "appId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    }
]
```

注意`json`格式，最后一个要删掉逗号。建议在填写之前，使用[json校验工具](https://www.bejson.com/)进行校验。

注意：不要将个人信息填写到仓库`config.json`文件中（不要动这个文件就没事），以免泄露。

多账号，参考[关于多账号的使用方式](https://github.com/srcrs/UnicomTask/discussions/16)

![](https://draw-static.vercel.app/UnicomTask/将参数填到Secrets中.gif)

### 4.开启Actions

默认`Actions`处于禁止状态，在`Actions`选项中开启`Actions`功能，把那个绿色的长按钮点一下。如果看到左侧工作流上有黄色`!`号，还需继续开启。

![](https://draw-static.vercel.app/UnicomTask/开启Actions.gif)

### 5.进行一次push操作

`push`操作会触发工作流运行。

删除掉`README.md`中的😄即可。完成后，每天早上`7:30`将自动完成每日任务。

![](https://draw-static.vercel.app/UnicomTask/进行一次push操作.gif)


### 2.准备需要的参数

* 开通云函数 `SCF` 的腾讯云账号，在[访问秘钥页面](https://console.cloud.tencent.com/cam/capi)获取账号的 `TENCENT_SECRET_ID`，`TENCENT_SECRET_KEY`

> 注意！为了确保权限足够，获取这两个参数时不要使用子账户！此外，腾讯云账户需要[实名认证](https://console.cloud.tencent.com/developer/auth)。

* 依次登录 [SCF 云函数控制台](https://console.cloud.tencent.com/scf) 和 [SLS 控制台](https://console.cloud.tencent.com/sls) 开通相关服务，确保您已开通服务并创建相应[服务角色](https://console.cloud.tencent.com/cam/role) **SCF_QcsRole、SLS_QcsRole**

* 手机号，服务密码，appId等等（参考[2.准备需要的参数](#2准备需要的参数)）

### 3.将参数填到Secrets

`Name`和`Value`格式如下：
  
Name | Value
-|-
TENCENT_SECRET_ID | 腾讯云用户SecretID(需要主账户，子账户可能没权限)
TENCENT_SECRET_KEY | 腾讯云账户SecretKey
USERS_COVER | config.json中内容

如对于`Secrets`不知如何添加，参考[3.将参数填到Secrets](#3将参数填到secrets)

![](https://draw-static.vercel.app/UnicomTask/云函数添加Secrets.png)

### 4.部署

* 添加完上面`3`个`Secrets`后，进入`Actions`(上面那个不是`Secrets`下面那个) --> `deploy for serverless`，点击右边的`Run workflow`即可部署至腾讯云函数(如果出错请在红叉右边点击`deploy for serverless`查看部署任务的输出信息找出错误原因)。

* 首次`fork`可能要去`Actions`里面同意使用`Actions`条款，如果`Actions`里面没有`deploy for serverless`，点一下右上角的`star`，`deploy for serverless`就会出现在`Actions`里面。（参考[4.开启Actions](#4开启actions)）

# 同步上游代码

在最新的代码中，已经加上自动同步上游代码的`Action`，将会定时在每周五`16`点执行，文件地址在`.github/workflows/auto_merge.yml`。

同时您也可以安装[pull](https://github.com/apps/pull)应用，也可实现自动同步上游代码。
