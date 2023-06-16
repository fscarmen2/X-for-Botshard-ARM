# Argo Xray for Botshard (ARM)

* * *

# 目录

- [项目特点](README.md#项目特点)
- [部署](README.md#部署)

* * *

## 项目特点:
* 本项目用于在 [Botshard.com](https://dashboard.botshard.com/) 免费服务上部署 Xray
* 根据本平台自行修改的哪吒探针，以能使用其 VNC 达到 ssh 的效果，可以自由选择是否安装
* 使用 CloudFlare 的 Argo 隧道，直接优选 + 隧道，CDN 不用再做 workers
* 针对本项目另辟蹊径处理 root 权限，可玩性大大增加
* 部署完成如发现不能上网，请检查域名是否被墙，可使用 Cloudflare CDN 或者 worker 解决。参照文章：https://www.hicairo.com/post/57.html
* 前端 js 定时保活，会玩的用户可以根据具体情况修改间隔时间
* 节点信息以 V2rayN / Clash / 小火箭 链接方式输出
* 可以使用浏览器使用 webssh 和 webftp，更方便管理系统

## 部署:
* 注册 [Botshard.com](https://panel.botshard.com/)
* entrypoint.sh 的 6-8 行修改 UUID、WS 路径和哪吒变量
* PaaS 平台用到的变量

  | 变量名        | 是否必须 | 默认值 | 备注 |
  | ------------ | ------ | ------ | ------ |
  | UUID         | 否 | de04add9-5c68-8bab-950c-08cd5320df18 | 可在线生成 https://www.zxgj.cn/g/uuid |
  | WSPATH       | 否 | argo | 勿以 / 开头，各协议路径为 `/WSPATH-协议`，如 `/argo-vless`,`/argo-vmess`,`/argo-trojan`,`/argo-shadowsocks` |
  | NEZHA_SERVER | 否 |        | 哪吒探针与面板服务端数据通信的IP或域名 |
  | NEZHA_PORT   | 否 |        | 哪吒探针服务端的端口 |
  | NEZHA_KEY    | 否 |        | 哪吒探针客户端专用 Key |
  | NEZHA_TLS    | 否 |        | 哪吒探针是否启用 SSL/TLS 加密 ，如不启用不要该变量，如要启用填"1" |
  | ARGO_AUTH    | 否 |        | Argo 的 Token 或者 json 值 |
  | ARGO_DOMAIN  | 否 |        | Argo 的域名，须与 ARGO_DOMAIN 必需一起填了才能生效 |
  | WEB_USERNAME | 否 | admin  | 网页和 webssh 的用户名 |
  | WEB_PASSWORD | 否 | password | 网页和 webssh 的密码 |
  | SSH_DOMAIN   | 否 |        | webssh 的域名，用户名和密码就是 <WEB_USERNAME> 和 <WEB_PASSWORD> |
  | FTP_DOMAIN   | 否 |        | webftp 的域名，用户名和密码就是 <WEB_USERNAME> 和 <WEB_PASSWORD> |

* 需要应用的 js
  | 命令 | 说明 |
  | ---- |------ |
  | <URL>/list | 查看节点数据 |
  | <URL>/listen | 查看后台监听端口 |
  | <URL>/test |	测试是否为只读系统 |