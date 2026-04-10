# uniapp-skill 说明文件

## 概述

`uniapp-skill` 是为 Claude Code 构建的 uni-app 开发知识技能库，涵盖 uni-app 框架全链路开发知识（含 uni-app x / UTS 插件）。当用户提及 uni-app、uniapp、uni-app x、uvue、UTS、HBuilderX、DCloud、小程序、跨端开发等关键词时自动触发。

## 知识来源

| 来源 | 说明 |
|------|------|
| uni-app 官方文档 | `E:\claude\unidocs-zh\docs\` 下 500+ 篇 markdown 文件，系统性学习 |
| uni-app x 官方文档 | `https://doc.dcloud.net.cn/uni-app-x/` UTS 语言、uvue 渲染、鸿蒙支持 |
| DCloud 社区精华帖 | `ask.dcloud.net.cn` 推荐/精华帖，覆盖 8 页内容 |
| 实战经验 | 社区高频问题、最佳实践、避坑指南 |

## 文件结构

```
uniapp-skill/
├── SKILL.md                              主入口（663 行）
│   ├── 第一部分：学习路径规划
│   ├── 第二部分：项目搭建
│   ├── 第三部分：核心功能实现
│   ├── 第四部分：调试与发布
│   ├── 第五部分：避坑指南（含 uni-app x）
│   ├── 第六部分：进阶功能速查
│   ├── 第七部分：社区最佳实践
│   ├── 第八部分：uni-app x 与 UTS 插件
│   ├── 第九部分：测试方案
│   ├── 第十部分：安全实践
│   ├── 第十一部分：CI/CD 与 Vite 配置
│   └── 参考文件完整索引
│
├── references/                           26 个参考文件（~10,670 行）
│   ├── project-setup.md         (173)    环境搭建、项目创建、目录结构、UI 库
│   ├── pages-config.md          (176)    pages.json 全部字段详解
│   ├── manifest.md              (455)    [新增] manifest.json 完整参考：核心字段、各平台配置、OAuth/Push/Maps、模板
│   ├── lifecycle.md             (521)    应用/页面/组件生命周期、时序图、Vue3 用法、Pinia 交互、平台差异、陷阱
│   ├── api.md                   (282)    网络请求、路由、UI、存储、位置、设备
│   ├── components.md            (356)    内置组件 + uni-ui 常用组件
│   ├── more-components.md       (405)    扩展组件、媒体组件、nvue 高性能组件
│   ├── conditional-compilation.md (201)  条件编译语法与平台标识
│   ├── vue3-patterns.md         (209)    Composition API、组合函数、Vue2→3 迁移
│   ├── advanced-features.md     (541)    nvue/RenderJS/i18n/暗黑/TS/SSR/WebSocket/Vite 配置
│   ├── app-native.md            (265)    登录/支付/推送/分享/安全加固/隐私合规
│   ├── cloud-services.md        (295)    UniPush/一键登录/uni统计/uniCloud/uni-AD
│   ├── media-file-api.md        (275)    图片/视频/音频/录音/相机/文件操作
│   ├── system-device-api.md     (374)    设备信息/蓝牙/传感器/UI控制/DOM查询
│   ├── native-resources.md      (367)    Android/iOS/鸿蒙原生配置、地图、CORS
│   ├── debug-publish.md         (203)    各平台运行调试与打包发布
│   ├── pitfalls.md              (282)    13 大常见问题（含 uni-app x 坑点）
│   ├── community-practices.md  (1,048)   社区精华实战（热更新/性能/登录等）
│   ├── uniapp-x-uts.md          (442)    uni-app x 架构/uvue/UTS/插件开发/混编/鸿蒙/迁移
│   ├── harmony-basics.md        (283)    [新增] 鸿蒙基础：环境搭建/项目配置/签名/条件编译/错误排查
│   ├── harmony-development.md   (431)    鸿蒙核心开发：UTS 插件/原生组件/华为登录/URL Scheme
│   ├── harmony-advanced.md      (254)    [新增] 鸿蒙进阶：元服务/调试/发布/地图
│   ├── harmony-migration.md   (1,637)    [新增] 鸿蒙适配迁移：日常适配/老项目迁移/架构师笔记
│   ├── testing.md               (422)    Vitest 单元测试 + uni-automator E2E 测试
│   ├── security.md              (383)    Token 安全/接口签名/XSS 防护/UGC 检测
│   └── cicd.md                  (391)    GitHub Actions/环境变量/Vite 配置/包体积管控
│
└── README.md                             本说明文件
```

**总计：28 个文件，约 11,330 行**

## 知识覆盖范围

### 基础开发

| 模块 | 覆盖内容 |
|------|----------|
| 项目搭建 | HBuilderX / CLI 创建、目录结构、main.js、uni.scss |
| 页面配置 | pages.json 全字段、globalStyle、tabBar、分包、easycom |
| 应用配置 | manifest.json 核心字段、各平台配置（app-plus/app-harmony/h5/小程序）、SDK 集成 |
| 生命周期 | App/页面/组件三级钩子、执行顺序、时序图、Vue3 Composition API、Pinia 交互、平台差异、常见陷阱 |
| 路由导航 | navigateTo/redirectTo/switchTab/reLaunch、EventChannel、全局事件 |
| 条件编译 | #ifdef/#ifndef、平台标识符、JS/CSS/Template/pages.json/静态资源 |
| 样式体系 | rpx 单位、page 根节点、CSS 预处理器、nvue flex 限制 |

### 核心 API

| 模块 | 覆盖内容 |
|------|----------|
| 网络请求 | uni.request + 拦截器、路由守卫、请求封装 |
| UI 交互 | showToast/showModal/showLoading/showActionSheet |
| 本地存储 | getStorage/setStorage（同步/异步） |
| 媒体文件 | 图片选择压缩预览、视频处理、音频播放录音、文件上传下载 |
| 系统设备 | 设备信息、网络、蓝牙、传感器、电池、剪贴板、振动 |
| UI 控制 | 导航栏、TabBar、动画、滚动、字体、键盘、DOM 查询 |

### 组件体系

| 类别 | 组件 |
|------|------|
| 基础 | view、text、image、scroll-view、swiper |
| 表单 | input、textarea、button、picker、form、switch、slider |
| 导航 | navigator、tabBar、custom-tab-bar |
| 媒体 | video、camera、live-pusher、live-player、animation-view |
| 覆盖 | cover-view、movable-view |
| uni-ui | 30+ 组件（badges/cards/lists/forms/popups/tables 等） |
| nvue | list、waterfall、recycle-list（自动内存回收） |

### uni-app x 与 UTS（新增）

| 模块 | 覆盖内容 |
|------|----------|
| 架构对比 | 传统 uni-app vs uni-app x（渲染引擎/编译目标/性能） |
| uvue 页面 | 文件后缀、CSS 子集限制（仅 flex）、各平台支持状态 |
| UTS 语言 | 语法要点、类型系统（强类型 vs TS）、类型推导演进 |
| UTS 插件开发 | 目录结构、Android/iOS/鸿蒙插件示例、config.json 配置 |
| 混编能力 | kt/java/swift/ets 直接混编、导入方式 |
| 鸿蒙支持 | 环境要求（DevEco Studio 5.0.7+/API 14+）、特有功能 |
| 版本兼容 | HBuilderX 版本功能矩阵、Node/Vite/Vue 版本要求 |
| 迁移指南 | 传统→x 迁移步骤、常见问题与解决方案 |
| 选型建议 | 何时选传统 uni-app / 何时选 uni-app x |

### 测试方案（新增）

| 模块 | 覆盖内容 |
|------|----------|
| Vitest 单元测试 | 安装配置、uni API Mock、setup 文件、覆盖率 |
| 测试工具函数 | 纯函数测试示例 |
| 测试 Composable | useCounter 组合函数测试 |
| 测试 Pinia Store | Store actions/getters 测试、mock storage |
| 测试 uni API 调用 | uni.request mock、异步测试 |
| uni-automator E2E | 安装、页面测试编写、API 速查表 |
| 最佳实践 | 测什么/不测什么、目录结构、package.json 脚本 |

### 安全实践（新增）

| 模块 | 覆盖内容 |
|------|----------|
| Token 安全 | 加密存储（AES 封装）、refresh token 机制、自动刷新 |
| 接口签名 | HMAC-SHA256 签名、拦截器集成、后端校验要点 |
| XSS 防护 | DOMPurify 富文本净化、HTML 实体转义、URL 参数校验、CSP |
| UGC 检测 | uni-sec-check 文本/图片安全检测 |
| HTTPS | manifest.json 配置、拦截器强制 HTTPS、小程序合法域名 |
| 敏感数据 | 日志脱敏、App 端防截屏 |
| 平台要点 | H5 CSP/CORS、小程序 appSecret 仅服务端、App 加固 |

### CI/CD 与工程化（新增）

| 模块 | 覆盖内容 |
|------|----------|
| GitHub Actions | H5 构建部署、微信小程序上传（miniprogram-ci）、多平台并行 |
| 环境变量 | .env 文件管理、VITE_* 注入、CI Secrets 配置 |
| Vite 配置 | 路径别名、开发代理、构建优化（terser）、全局常量 |
| App 构建 | 云打包 CLI、安心打包 |
| 小程序管控 | 主包 2MB 限制检查、分包策略、preloadRule |

### 进阶能力

| 模块 | 覆盖内容 |
|------|----------|
| Vue3 深入 | Composition API、composables、Props/Emits/v-model/provide-inject/Slots |
| 原生渲染 | nvue 限制与优势、RenderJS 60fps 交互 |
| 国际化 | vue-i18n + pages.json %key% 语法 |
| 暗黑模式 | theme.json + CSS @media + onThemeChange |
| TypeScript | @dcloudio/types + lang="ts" |
| SSR | 服务端渲染、SEO 优化 |
| WebSocket | uni.connectSocket 实时通信 |
| WebView | web-view + evalJS 双向通信 |

### App 原生

| 模块 | 覆盖内容 |
|------|----------|
| 登录 | 微信/QQ/Apple/一键登录(univerify) |
| 支付 | 微信/支付宝/Apple IAP/Stripe/PayPal |
| 推送 | UniPush 2.0 + 厂商离线通道 |
| 分享 | 系统分享 + 平台分享 + 小程序分享 |
| 安全 | APK 加固、防篡改、防重打包 |
| 隐私 | androidPrivacy.json 合规弹窗 |
| 原生配置 | AndroidManifest.xml、Info.plist、Entitlements、鸿蒙 |

### 云服务

| 模块 | 覆盖内容 |
|------|----------|
| uniCloud | 云函数/云对象 + 云数据库(JQL) + 云存储 + 前端网页托管 |
| UniPush 2.0 | 全平台推送，客户端+服务端完整代码 |
| 一键登录 | 运营商网关认证，换取手机号完整流程 |
| uni 统计 | 开源全平台统计，自定义事件上报 |
| uni-AD | Banner/信息流/激励视频/开屏等广告 |

### 社区实战

| 主题 | 覆盖内容 |
|------|----------|
| wgt 热更新 | 服务端 API + 客户端下载安装 + uni-upgrade-center |
| 性能优化 | 分包策略、主包瘦身、白屏骨架屏、数据/渲染优化 |
| 自定义导航栏 | 状态栏适配、微信胶囊计算、底部安全区 |
| Android 合规 | 隐私弹窗模板、权限申请、自查清单、常见拒审原因 |
| 全局变量 | globalData/Pinia/provide-inject/globalProperties 选型 |
| 微信登录 | code→token 完整流程、手机号快速验证、静默登录 |
| 图片上传 | useImageUpload composable（选择+压缩+批量上传） |
| 分页加载 | usePagination composable + z-paging 组件 |
| 请求封装 | Promise 封装 + 错误处理 + API 模块化 |
| 调试技巧 | condition 启动页、vConsole、平台差异调试 |

## 触发条件

当用户消息中包含以下任一关键词时自动加载：

`uni-app` `uniapp` `uni-app x` `uvue` `UTS` `HBuilderX` `DCloud` `跨端开发` `小程序` `多端` `pages.json` `manifest.json` `uni.request` `uni.navigateTo` `easycom` `nvue` `uts` `uniCloud` `uni-ui` `条件编译` `#ifdef` `uni-automator` `vitest`

以及涉及目标平台：微信小程序、H5、App、支付宝、抖音、QQ、百度、鸿蒙。
