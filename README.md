简体中文 | [English](./docs/en.md)  

在 Cloudflare workers 中部署 vless.xhttp 协议的代理服务器。  

#### 使用方法
 1. 前置要求，拥有一个由 CF 托管的一级域名
 1. 在 CF 控制面板的 `网络` 配置中启用 `gRPC` 功能
 1. 在 DNS 配置中添加一个二级域名的 A 记录，随便填个 IPv4 地址，开启小黄云
 1. 新建一个 workers 把 [src/index.js](./src/index.js) 里面的代码复制进去
 1. 在 workers 的配置页面添加路由，指向上面新加的二级域名，例如: `sub.your-website.com/*`

代码顶部有几个配置项：  
UUID 这个不用解释了吧  
PROXY 反代 CF 网页的服务器，格式： `example.com`  
LOG_LEVEL 日志级别，可选：debug, info, error, none  
TIME_ZONE 日志时间戳的时区，中国填 `8`  

这些配置项也可以在 workers 的环境变量界面中配置。环境变量的优先级更高。  

一切顺利的话，访问 `https://sub.your-website.com` 会看到 `Hello world!`  
访问 `https://sub.your-website.com/xhttp/?uuid=YOUR-UUID` 得到客户端的 `config.json`  

#### 注意事项
 * 网站测速结果是错的，这个脚本很慢，不要有太高的期望
 * 只能部署到 workers，不能部署到 pages [issue #2](https://github.com/vrnobody/cfxhttp/issues/2)
 * 使劲薅，免费的资源就会消失，且用且珍惜

#### 感谢
很多代码抄袭自某个项目的，但找不到原项目了，欢迎认领。  
