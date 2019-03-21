# 微信本地调试

**一、 使用的测试公众号**

> 开发前，需要扫码关注



**二、安装 hosts 文件修改工具**

> HostsSwitcher-v.1.0.0.0.zip（Windows）

目的：添加 `127.0.0.1 xf.dev.xxxx.com`到hosts文件中

本地开发，使用`xf.dev.xxxx.com:`29879`/admin`地址

在`微信Web开发者工具`中使用此链接就可以调试`jssdk`了



**三、开发**

> 后台服务器提供微信token校验功能，使用的是Nate的测试公众号
>
> 故而所有开发人员的`微信Web开发者工具`都需要扫码登陆

打开`微信Web开发者工具`

地址栏中输入`edu-saas.dev.xiaojing0.com:29879/admin`开始表演

## 原理说明 <a id="&#x539F;&#x7406;&#x8BF4;&#x660E;"></a>

![](https://xiaojing0.gitbooks.io/web-manual/content/assets/%E5%85%AC%E4%BC%97%E5%8F%B7%E8%B0%83%E8%AF%95%E9%80%BB%E8%BE%91.png)

