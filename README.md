# impacket-rbcd
The original version of impact-ntlmrelayx only supported requests from machine accounts when playing through RBCD. Now I have made some small changes to enable it to support requests from user accounts.  

原始版本的impacket-ntlmrelayx 通过RBCD方式进行Relay的时候只能支持来自机器账户的请求，现在我做了一些小小的改变，使其能够支持来自用户账户的请求。
ntlmrelayx的相关依赖已经补充完成，可以直接使用 Pyinstaller进行打包为exe，在windows主机上进行执行 

## 如何使用这个工具？
在某些特殊场景的AD渗透测试当中，我们可以使用考虑使用NtlmRelayToLdap的方式进行攻击。
攻击手法：利用 基于资源的约束性委派获取目标主机的权限。

原版本的 Impacket 只允许机器账户 发起 Relay修改自身的 属性为 攻击者所创建的机器账户。此工具补全了此类的攻击场景，加上了**允许受害者账户发起Relay进行修改自身所添加的机器账户的msDS-AllowedToActOnBehalfOfOtherIdentity属性**的场景。  

在修改此属性之后，我们可以利用基于资源的约束性委派（RBCD）从而获取到受害者账户的计算机账户的高权限票据进行横向移动。  
因为在内网中大量未进行设置 IPV6 场景等多个NTLM的触发点，给 NTLM relay over Http 提供了极大的攻击面，所以这款工具在某些场合会有奇迹发生。


### NTLM 触发点 
- 受害者访问攻击者的网站链接
- 受害者输错网络地址
- 所在的网络未进行配置IPv6，攻击者冒充DHCPV6和DNSV6服务器
- 受害者访问存在 XSS漏洞的网站
- 受害者打开邮件【基于特定的邮箱客户端foxmail是可以的，outlook需要注意版本】
- 打印机漏洞
- petitpotam
- ...




## referer
[修改工具的方式来源](https://www.cnblogs.com/unicodeSec/p/14260648.html)



## 免责声明
本工具禁止进行未授权测试，禁止二次开发后进行未授权测试。
在使用本工具进行检测时，您应确保该行为符合当地的法律法规，并且已经取得了足够的授权。
如您在使用本工具的过程中存在任何非法行为，您需自行承担相应后果，我不承担任何法律及连带责任。
在使用本工具前，请您务必审慎阅读、充分理解各条款内容，限制、免责声明。 除非您已充分阅读、完全理解并接受本协议所有条款，否则，请您不要使用本工具。您的使用行为或者您以其他任何明示或者默示方式表示接受本协议的，即视为您已阅读并同意本协议的约束。
