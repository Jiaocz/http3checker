# HTTP/3 QUIC Tester
测试你的浏览器是否使用HTTP/3 QUIC

## Screenshot
![ScreenShot](https://github.com/Jiaocz/http3checker/blob/main/screenshot.png)

## 前端构建
[![Build Test](https://github.com/Jiaocz/http3checker/actions/workflows/build-test.yml/badge.svg)](https://github.com/Jiaocz/http3checker/actions/workflows/build-test.yml) [![CodeQL](https://github.com/Jiaocz/http3checker/actions/workflows/codeql-analysis.yml/badge.svg)](https://github.com/Jiaocz/http3checker/actions/workflows/codeql-analysis.yml)

使用[Vite.js](https://vitejs.dev)建立项目，使用以下命令安装依赖
```shell
pnpm i # 安装依赖
pnpm dev # 调试服务
pnpm build # 构建项目
```

## 后端支持
请使用[nginx-quic](https://quic.nginx.org)分支构建的Nginx服务器，并在server中添加
```
listen 443 http3 reuseport;
```
添加HTTP/3支持，并添加以下header
```
add_header Alt-Svc 'h3=":443"; ma=86400'; # 通知浏览器使用HTTP/3
add_header x-quic $http3; # 为本应用提供检测HTTP/3的方案
```
