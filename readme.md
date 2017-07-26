
#Shadowrocket自定义规则
**规则地址：**<https://raw.githubusercontent.com/xiabob/Shadowrocket-ADBlock-Rules/master/sr_adb.conf>

#net-speeder
netspeeder.sh是[net-speeder](https://github.com/snooda/net-speeder)一键安装脚本，使用方法：

centos系统
<pre>
wget https://raw.githubusercontent.com/xiabob/Shadowrocket-ADBlock-Rules/master/netspeeder.sh
sh netspeeder.sh
</pre>

"卸载"net-speeder的方法：删除/usr/local/netspeeder目录下的文件即可。


# 以下是原始内容

## Best Proxy Rules

这里是一系列好用的翻墙规则，针对 [Shadowrocket](https://liguangming.com/Shadowrocket) 开发，支持广告过滤，使用 Python 按照一定的规则和模板定期自动生成，并且使用开源的力量，集众人之力逐渐完善。

**本规则有以下特点：**

- 仅对 `被墙` 且 `世界前 500` 的网站视为需要代理。所有被墙的网站太多，很大部分为垃圾网站，并没有必要一一匹配。
- 自动转换最新版本的 `EasyList, Eaylist China, 乘风规则` 为 SR 规则，全面去除广告且去除重复。
- 也包括自定义的广告过滤规则，针对 iOS 端的网页广告、App 广告和视频广告。
- 提供多个规则文件让大家自由选择或者自由切换使用。
- 专门针对 ShadowRocket 开发，可以保证与 SR 的兼容性。


### 目录

- [黑名单过滤 + 广告](#黑名单过滤--广告)
- [白名单过滤 + 广告](#白名单过滤--广告)
- [白名单过滤](#白名单过滤)
- 神-奇-分-隔-符
- [常见问题](#常见问题)
- [相关推荐](#相关推荐)
- [问题反馈](#问题反馈)
- [捐助](#捐助)


## 黑名单过滤 + 广告

黑名单中包含了境外网站中无法访问的那些，对不确定的网站则默认直连。

- 代理：top500 网站中不可直连的境外网站
- 直连：默认直连境外其余网站、中国网站
- 包含广告过滤

规则地址：<https://raw.githubusercontent.com/h2y/Shadowrocket-ADBlock-Rules/master/sr_top500_banlist_ad.conf>

![](https://user-images.githubusercontent.com/12909077/27505548-db67b776-58d4-11e7-8775-ff038c8c11bf.png)

## 白名单过滤 + 广告

白名单中包含了境外网站中可以访问的那些，对不确定的网站则默认代理。

- 直连：top500 网站中可直连的境外网站、中国网站
- 代理：默认代理其余的所有境外网站
- 包含广告过滤

规则地址：<https://raw.githubusercontent.com/h2y/Shadowrocket-ADBlock-Rules/master/sr_top500_whitelist_ad.conf>

![](https://user-images.githubusercontent.com/12909077/27505553-ef1b86c6-58d4-11e7-9fb1-eafbd0c5dc81.png)


## 白名单过滤

现在很多浏览器都自带了广告过滤功能，而广告过滤的规则其实较为臃肿，如果你不需要全局地过滤 App 内置广告和视频广告，可以选择这个不带广告过滤的版本。

- 直连：top500 网站中可直连的境外网站、中国网站
- 代理：默认代理其余的所有境外网站
- 不包含广告过滤

规则地址：<https://raw.githubusercontent.com/h2y/Shadowrocket-ADBlock-Rules/master/sr_top500_whitelist.conf>

![](https://user-images.githubusercontent.com/12909077/27505552-ef108226-58d4-11e7-82eb-8558289d3953.png)


## 常见问题

- **上千行的代理规则，会对上网速度产生影响吗？**

> 不会的。
>
> 我之前也认为这是一个每次网络数据包经过都会执行一次的规则文件，逐行匹配规则，所以需要尽可能精简。但后来和 SR 作者交流后发现这是一个误区，SR 在每次加载规则时都会生成一棵搜索树，可以理解为对主机名从后往前的有限状态机 DFA，并不是逐行匹配，并且对每次的匹配结果还有个哈希缓存。
>
> 换句话说，2000 行的规则和 50 行的规则在 SR 中均为同一量级的时间复杂度 O(1)。


- **你提供了这么多规则，如何选择适合我的？**

> 黑白名单区别在于对待 `境外冷门网站` 的不同，黑名单默认直连，而白名单则默认使用代理。前者可能会有被墙的情况出现。后者不会出现无法翻墙的情况，但也许会使用代理去连接原本可以直连的网站，速度变慢，当然，如果你的翻墙服务器速度不低于直连，就果断使用白名单吧。
>
> 如果你选择恐惧症爆发，那就两个都下载好了，黑白名单在手，天下无忧。


- **你提供了这么多规则，却没有我想要的 o(>.<)o**

> 有任何建议或疑问，[请联系我](#问题反馈)。

- **广告过滤不完全？**

> 该规则并不保证 100% 过滤所有的广告，尤其是视频广告，与网页广告不同的是，优酷等 App 每次升级都有可能更换一次广告策略，因此难以保证其广告屏蔽的实时有效性。


## 相关推荐

[**AppleDNS**](https://github.com/gongjianhui/AppleDNS)

Hosts 生成工具，生成 `在当前所在网络环境下` Apple 服务器的 DNS 最优解析结果，加快访问速度。

电脑需安装 Python，按照 Readme 运行后，将生成的 hosts 粘贴到 `Shadowrocket->Settings->DNS->Hosts` 即可。

**<http://ip111.cn/>**

这是一个很棒的 IP 查询网站，支持同时查询你的境内境外 IP，以及谷歌 IP。

[**CloudGateRules_SR**](https://github.com/CloudGateRules/Shadowrocket)

这同样是由开源社区维护的另一款 SR 规则，大家也可以试试。


## 问题反馈

任何问题欢迎在 [Issues](https://github.com/h2y/Shadowrocket-ADBlock-Rules/issues) 中反馈，如果没有账号可以去 [我的网站](https://hzy.pw/p/2096#comments) 中留言。

你的反馈会让此规则变得更加完美。

**如何贡献代码？**

通常的情况下，对 [factory 目录](https://github.com/h2y/Shadowrocket-ADBlock-Rules/tree/master/factory) 下的 3 个 `manual_*.txt` 文件做对应修改即可。


## 捐助

本项目不接受任何形式的捐助，因为自由地上网本来就是大家的权利，没有必要为此付出更多的代价。

但是，作为一个翻墙规则，不可避免的会对网站有所遗漏，需要大家来共同完善，当发现不好用的地方时，请打开 SR 的日志功能，检查一下是哪一个被墙的域名走了直连，或者是哪一个可以直连的域名走了代理。

将需要修改的信息反馈给我，大家的努力会让这个规则越来越完善！
>>>>>>> 87f4a450d56e33dea1101bd5167b70d938f2c5da
