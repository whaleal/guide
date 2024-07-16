# Whaleal Account

## 简介
Whaleal Account 是一个前后端分离的 OAuth2.0 授权中心与用户中心，适用于 微服务鉴权、单点登录、企业开放平台 等场景。
（[访问地址](https://account.whaleal.com)）

## 功能模块
* 用户管理
* 应用管理
* 角色与权限管理
* OAuth2 授权模式与授权作用域管理 （GrantType & Scope）
* 应用授权与鉴权

## 支持的授权模式
* 授权码模式 authorization_code
* 客户端凭据模式 client_credentials
* 隐式授权模式 implicit
* 令牌刷新 refresh_token
* 密码模式 password （出于安全考虑默认不启用，如需启用可以自行创建。）

