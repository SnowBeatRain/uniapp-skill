# uniapp-skill 说明文件

## 概述

`uniapp-skill` 是为 Claude Code 构建的 uni-app 开发知识技能库，涵盖 uni-app 框架全链路开发知识。当用户提及 uni-app、uniapp、HBuilderX、DCloud、小程序、跨端开发等关键词时自动触发。

## 知识来源

| 来源 | 说明 |
|------|------|
| uni-app 官方文档 | `E:\claude\unidocs-zh\docs\` 下 500+ 篇 markdown 文件，系统性学习 |
| DCloud 社区精华帖 | `ask.dcloud.net.cn` 推荐/精华帖，覆盖 8 页内容 |
| 实战经验 | 社区高频问题、最佳实践、避坑指南 |

## 文件结构

```
uniapp-skill/
├── SKILL.md                              主入口（456 行）
│   ├── 第一部分：学习路径规划
│   ├── 第二部分：项目搭建
│   ├── 第三部分：核心功能实现
│   ├── 第四部分：调试与发布
│   ├── 第五部分：避坑指南
│   ├── 第六部分：进阶功能速查
│   ├── 第七部分：社区最佳实践
│   └── 参考文件完整索引
│
├── references/                           17 个参考文件（5,299 行）
│   ├── project-setup.md         (173)    环境搭建、项目创建、目录结构、UI 库
│   ├── pages-config.md          (176)    pages.json 全部字段详解
│   ├── lifecycle.md             (110)    应用/页面/组件生命周期
│   ├── api.md                   (282)    网络请求、路由、UI、存储、位置、设备
│   ├── components.md            (356)    内置组件 + uni-ui 常用组件
│   ├── more-components.md       (405)    扩展组件、媒体组件、nvue 高性能组件
│   ├── conditional-compilation.md (166)  条件编译语法与平台标识
│   ├── vue3-patterns.md         (209)    Composition API、组合函数、Vue2→3 迁移
│   ├── advanced-features.md     (463)    nvue/RenderJS/i18n/暗黑/TS/SSR/WebSocket
│   ├── app-native.md            (265)    登录/支付/推送/分享/安全加固/隐私合规
│   ├── cloud-services.md        (295)    UniPush/一键登录/uni统计/uniCloud/uni-AD
│   ├── media-file-api.md        (275)    图片/视频/音频/录音/相机/文件操作
│   ├── system-device-api.md     (374)    设备信息/蓝牙/传感器/UI控制/DOM查询
│   ├── native-resources.md      (367)    Android/iOS/鸿蒙原生配置、地图、CORS
│   ├── debug-publish.md         (138)    各平台运行调试与打包发布
│   ├── pitfalls.md              (197)    10 大常见问题详解
│   └── community-practices.md  (1,048)   社区精华实战（热更新/性能/登录等）
│
└── README.md                             本说明文件
```

**总计：18 个文件，5,755 行**

## 知识覆盖范围

### 基础开发

| 模块 | 覆盖内容 |
|------|----------|
| 项目搭建 | HBuilderX / CLI 创建、目录结构、main.js、uni.scss |
| 页面配置 | pages.json 全字段、globalStyle、tabBar、分包、easycom |
| 生命周期 | App/页面/组件三级钩子、执行顺序、参数说明 |
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

### 工程化

| 模块 | 覆盖内容 |
|------|----------|
| 调试 | H5(Chrome)/小程序(开发者工具)/App(HBuilderX) 各平台调试方法 |
| 打包 | 云打包/安心打包/离线打包、各平台发布流程 |
| 避坑 | 10 大高频问题：静态资源/样式兼容/tabBar/请求/条件编译/生命周期/包体积/nvue/第三方库 |
| 环境变量 | .env + VITE_* / VUE_APP_*、Vite 配置 |
| 地图服务 | 高德/百度/腾讯/Google 配置与费用 |
| CORS | H5 跨域解决方案（同域/CORS 头/云函数代理） |

## 触发条件

当用户消息中包含以下任一关键词时自动加载：

`uni-app` `uniapp` `HBuilderX` `DCloud` `跨端开发` `小程序` `多端` `pages.json` `manifest.json` `uni.request` `uni.navigateTo` `easycom` `nvue` `uts` `uniCloud` `uni-ui` `条件编译` `#ifdef`

以及涉及目标平台：微信小程序、H5、App、支付宝、抖音、QQ、百度、鸿蒙。
