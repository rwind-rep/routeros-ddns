- - -
* dnspod 腾讯DNS(国内与国际) 与 cloudflare CF 同时更新
* 脚本支持IPV4与IPV6同时更新
- - -
|参数|说明|
|---|---|
|scriptname|定义脚本名|
|pppoe|拨号接口名称|
|dnslist|DNS认证列表|
|domains|需要更新域名列表|
|subdomains|子域名|
|ipv6address|拨号提供前缀后ROS根据UUID分配后缀(详细提取方式参照脚本文件)|
|ipv6scheduler|拨号IPV6会变动，他不是根据宽带重新拨号变动，所以开启定时器提取前缀有效时间验证是否变动。默认关闭(开启会自动添加一个定时器任务。请正确填写脚本名)|
```php
#注意事项：ROS 脚本数组所用;符合分割最后一个参数后面不要添加分割符号

#定义脚本名(如果开启IPV6定时执行必须修改此值与你设置值相同)
scriptname "DDNS_Update"
#(需要修改)获取拨号接口名称
pppoe "PPPoE"

#需要更新DNS网站和对应token
#书写格式：单个DNS商 {{token="";dnsapi="DNS商"}} 多个域名商 {{token="";dnsapi="DNS商"}}
#腾讯DNS更新支持国内和国际，书写格式：{{token="腾讯token：199237,a9d9d0812f72d";dnsapi="DNS商：dnspod.cn 或 dnspod.com"}}
#CF DNS更新，书写格式：{{token={email="";key=""};dnsapi="cloudflare.com"}}
#(需要修改)DNS列表
dnslist {
{token="";dnsapi="dnspod.cn"};
{token="";dnsapi="dnspod.com"};
{token={email="";key=""};dnsapi="cloudflare.com"}
}

#(需要修改)更新域名列表
domains {"example.com";"example.me";"example.io"}

#(需要修改)子域名(支持多个子域名)
subdomains {"ip";"api";"www";"*";"@"}

#需要更新ipv6 地址后缀，前缀自动获取接口,后缀提取方法：如fe80::5eb9:1ff:fe95:1e70/64 提取后：5eb9:1ff:fe95:1e70
#(需要修改) ipv6后缀
ipv6address "9c06:7eff:fe9b:c208"

#ipv6 定时器开关(因为电信IPV6间隔1个小时就会更改)
#(需要修改) ipv6定时器
ipv6scheduler false
```
