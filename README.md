# 苍穹外卖 (sky-take-out)

基于黑马程序员《苍穹外卖》企业级项目实战课程完成的学习项目，前后端分离架构：后端自行实现，前端（管理端 + 微信小程序端）为课程生态内可运行的实现。

## 项目简介

苍穹外卖是一套面向中小餐饮商家的外卖点单系统，包含：

- **商家管理端**（Web，店长/员工使用）：员工、分类、菜品、套餐、订单管理，营业状态与数据统计
- **用户端**（微信小程序，消费者使用）：浏览菜单、购物车、下单、支付、催单、地址管理

两端共用同一套 Spring Boot 后端服务。

## 技术栈

| 模块 | 技术 |
| --- | --- |
| 后端 | Spring Boot + MyBatis + MySQL + Redis + JWT + WebSocket |
| 管理端 | Vue 2.6 + TypeScript + Element UI + ECharts |
| 用户端 | uni-app（编译到微信小程序） |
| 部署 | Nginx（静态资源托管 + 反向代理） |

## 目录结构

```
backend/    Spring Boot 后端（sky-common / sky-pojo / sky-server）
frontend/
  web-admin/  管理端源码（可 npm run serve 本地开发，npm run build 打包部署）
  mp-weixin/  小程序端编译产物（用微信开发者工具直接打开运行）
deploy/
  sql/        数据库建表与初始化脚本
  nginx/      Linux 下的 nginx 部署配置
```

## 分支说明

本仓库使用三分支模型：

- **`main`**：日常开发分支，持续提交，后端"挖空"方法的实现、功能调整都在这里进行，提交历史不追求整洁。
- **`baseline`**：冻结快照分支，定格在项目完成前后端迁移、整理完目录结构那一刻，**此后不再提交、不合并、不变动**，作为一个固定参照点，方便随时用 `git diff baseline main` 查看自己相对初始脚手架到底改了什么。
- **`showcase`**：**教学展示分支**，专门整理给别人阅读、学习这个项目用的。它不是从 `main` 自动合并过来的，而是单独维护一套按知识点/功能模块组织、经过整理的干净提交历史（例如"实现员工登录"、"实现菜品分页查询"这样一个提交对应一块完整内容），目的是让别人不用翻一堆调试 commit 就能看懂实现思路。更新 `showcase` 是手动挑选、重新整理 `main` 上的改动，不是简单合并。

## 本地运行

**后端**：先在 `backend/sky-take-out/sky-server/src/main/resources/application-dev.yml`（未提交，需自行创建，参考 `application.yml` 中引用的 `sky.datasource.*` 配置项）配置好本地 MySQL/Redis，再用 IDEA 跑 `SkyApplication`，默认端口 `8080`。

**管理端**：
```bash
cd frontend/web-admin
npm install --legacy-peer-deps
npm run serve
```
浏览器打开 `http://localhost:8081`。

**小程序端**：用微信开发者工具直接导入 `frontend/mp-weixin` 目录运行。

**生产部署参考**：`deploy/nginx/sky-take-out.conf`，托管 `frontend/web-admin` 的构建产物并反向代理后端接口。

## 参考资料

本项目管理端前端基于开源模板 [vue-typescript-admin-template](https://github.com/armour/vue-typescript-admin-template) 的"瑞吉外卖/苍穹外卖"定制分支整理而来。迁移与核对过程中查阅、参考过以下资料：

- [GitHub - ydh9851/sky-take-out](https://github.com/ydh9851/sky-take-out) — 苍穹外卖技术栈与功能模块说明
- [GitHub - lvanning/sky-takeout](https://github.com/lvanning/sky-takeout)

课程来源：黑马程序员《苍穹外卖》企业级项目实战课程。
