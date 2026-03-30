# 高级功能参考

## nvue 原生渲染

nvue 页面使用原生渲染引擎（Weex），在 App 端性能优于 webview 渲染。

### 何时使用 nvue

1. 需要高性能长列表（`<list>` / `<waterfall>` 组件，自动回收离屏内存）
2. 复杂下拉刷新（`<refresh>` 组件）
3. 左右拖动列表
4. 区域滚动 + 横向拖动 + 吸顶效果
5. 需要自定义键盘按钮文字（如"发送"替代"完成"）
6. map/video 等原生组件层级问题
7. 直播推流（`<live-pusher>` 组件）
8. 极致 App 启动速度优化（搭配 fast 启动模式）

### nvue 核心限制

```
布局：只支持 flex（默认 flex-direction: column）
文本：只能在 <text> 组件中
v-show：不支持，只能用 v-if
class 绑定：只支持数组语法 :class="[cls1, cls2]"
背景图：不支持 CSS 背景图，用 <image> 组件 + 层叠实现
选择器：只支持 class 选择器（无 id、元素、后代选择器）
单位：默认 px（非 rpx），需用 uni.upx2px() 转换
页面滚动：自动包裹 scroller，可用 disableScroll: true 禁用
动画：不支持 CSS 动画，使用 BindingX 或 weex.animation
```

### nvue 高性能列表

```vue
<!-- nvue 专属 list 组件（自动回收内存） -->
<list>
  <cell v-for="item in list" :key="item.id">
    <text>{{ item.name }}</text>
  </cell>
  <loading @loading="loadMore">
    <text>加载中...</text>
  </loading>
</list>

<!-- 瀑布流 -->
<waterfall column-count="2" column-width="auto">
  <cell v-for="item in list" :key="item.id">
    <image :src="item.image" mode="widthFix" />
  </cell>
</waterfall>
```

---

## RenderJS（视图层 JS）

在视图层运行 JS，消除逻辑层与视图层的通信延迟，适用于高性能交互场景。

**平台支持**：App-vue + H5

```vue
<template>
  <view @click="bindingTest.bindClick">点击触发 renderjs</view>
  <canvas canvas-id="bindingTest" style="width:100%;height:400px" />
</template>

<script>
export default {
  methods: {
    bindClickCallback(data) {
      // 逻辑层收到 renderjs 的回调
      console.log('来自 renderjs:', data)
    }
  }
}
</script>

<script module="bindingTest" lang="renderjs">
export default {
  mounted() {
    // 可访问 document、window、第三方 DOM 库
    // 例：引入 echarts、threejs 等
  },
  methods: {
    bindClick(e, ownerInstance) {
      // 在视图层执行，60fps 无延迟
      ownerInstance.callMethod('bindClickCallback', { msg: 'hello' })
    }
  }
}
</script>
```

**用途**：Canvas 动画（echarts/three.js）、高频手势响应、直接操作 DOM

---

## 国际化（i18n）

### Vue 页面多语言

```js
// main.js
import { createSSRApp } from 'vue'
import { createI18n } from 'vue-i18n'
import en from './locale/en.json'
import zhHans from './locale/zh-Hans.json'

export function createApp() {
  const app = createSSRApp(App)
  const i18n = createI18n({
    locale: uni.getLocale(),     // 自动跟随系统语言
    messages: { en, 'zh-Hans': zhHans }
  })
  app.use(i18n)
  return { app }
}
```

```vue
<template>
  <text>{{ $t('hello') }}</text>
  <button @click="changeLocale">切换语言</button>
</template>

<script setup>
const changeLocale = () => {
  uni.setLocale('en')          // 切换语言
}
// 监听语言变化
uni.onLocaleChange((res) => {
  console.log('语言切换为:', res.locale)
})
</script>
```

### pages.json 国际化

```
// 目录结构
locale/
├── en.json         { "index.title": "Home", "tab.home": "Home" }
└── zh-Hans.json    { "index.title": "首页", "tab.home": "首页" }
```

```json
// pages.json 中使用 %key% 语法
{
  "pages": [{ "path": "pages/index/index", "style": { "navigationBarTitleText": "%index.title%" } }],
  "tabBar": { "list": [{ "text": "%tab.home%" }] }
}
```

### 语言 API

```js
uni.getLocale()                  // 获取当前语言
uni.setLocale('zh-Hans')         // 设置语言
uni.onLocaleChange((e) => {})    // 监听语言切换
```

---

## 暗黑模式

### 配置启用

```json
// manifest.json
{
  "app-plus": { "darkmode": true, "themeLocation": "theme.json" },
  "h5": { "darkmode": true, "themeLocation": "theme.json" },
  "mp-weixin": { "darkmode": true, "themeLocation": "theme.json" }
}
```

### 主题变量

```json
// theme.json（项目根目录）
{
  "light": {
    "navBgColor": "#f8f8f8",
    "navTxtStyle": "black",
    "bgColor": "#ffffff",
    "txtColor": "#333333"
  },
  "dark": {
    "navBgColor": "#292929",
    "navTxtStyle": "white",
    "bgColor": "#1b1b1b",
    "txtColor": "#e0e0e0"
  }
}
```

```json
// pages.json 中引用
{ "navigationBarBackgroundColor": "@navBgColor", "navigationBarTextStyle": "@navTxtStyle" }
```

### CSS 适配

```css
@media (prefers-color-scheme: dark) {
  page { background-color: #1b1b1b; color: #e0e0e0; }
  .card { background-color: #2c2c2c; }
}
```

### 运行时检测

```js
const theme = uni.getSystemInfoSync().theme  // 'light' | 'dark'

// App.vue 中监听主题切换
import { onThemeChange } from '@dcloudio/uni-app'
onThemeChange((res) => { console.log('主题切换:', res.theme) })
```

---

## TypeScript 支持

### 配置

```json
// tsconfig.json
{
  "compilerOptions": {
    "types": ["@dcloudio/types"]
  }
}
```

```vue
<script setup lang="ts">
import { ref } from 'vue'
import { onLoad } from '@dcloudio/uni-app'

interface Item {
  id: number
  name: string
  price: number
}

const list = ref<Item[]>([])
const loading = ref<boolean>(false)

onLoad((options: { id?: string }) => {
  if (options?.id) fetchDetail(Number(options.id))
})
</script>
```

### 注意事项

- Vue3 + CLI 支持最新 TypeScript
- HBuilderX 内置 TS 3.7.5（Vue2）
- nvue + Vue2 不支持 TypeScript

---

## 环境变量

### Vue3 + Vite（推荐）

```
# .env.development
VITE_API_BASE=https://dev-api.example.com
VITE_APP_TITLE=开发环境

# .env.production
VITE_API_BASE=https://api.example.com
VITE_APP_TITLE=生产环境
```

```js
// 使用（前缀必须是 VITE_）
const apiBase = import.meta.env.VITE_API_BASE
```

### Vue2 + Webpack

```
# .env.development
VUE_APP_API_BASE=https://dev-api.example.com
```

```js
const apiBase = process.env.VUE_APP_API_BASE
```

---

## 性能优化

### 架构理解

- 非 H5 平台：逻辑层（JS）与视图层（渲染）分离，通信有延迟
- H5 平台：单层，无分离开销

### 关键优化策略

1. **数据管理**：只在 `data()` / `ref()` 中定义视图需要的数据，非视图数据放普通变量
2. **长列表**：
   - App-nvue：使用 `<list>` 组件（自动回收内存）
   - App-vue：页面级滚动优于 `<scroll-view>` 区域滚动
   - 通用：使用 uni-ui 的 `<uni-list>` 组件
   - 实现分页加载，限制数据量
3. **高频交互**：使用 renderjs（App-vue/H5）或 wxs（微信小程序）避免通信延迟
4. **组件拆分**：将列表项封装为独立组件，实现细粒度更新
5. **图片优化**：避免大图引起白屏，使用压缩图片，大图用网络地址

---

## SSR（服务端渲染）

**优势**：更好的 SEO、更快的首屏加载、慢网络/设备友好

### 核心约束

- 只有 `beforeCreate` 和 `created` 在服务端执行
- 浏览器 API（window/document）只能在 `onMounted` 后使用
- 避免副作用（定时器、全局变量）
- 使用 `ssrRef` 保持服务端/客户端状态一致（Vue3）

### 推荐方案

使用 uniCloud 部署 SSR 应用，简化服务器配置。

---

## WebSocket

```js
// 创建连接
const socketTask = uni.connectSocket({
  url: 'wss://api.example.com/ws',
  header: { 'Authorization': 'Bearer token' }
})

// 监听连接打开
socketTask.onOpen(() => {
  console.log('WebSocket 已连接')
  socketTask.send({ data: JSON.stringify({ type: 'ping' }) })
})

// 监听消息
socketTask.onMessage((res) => {
  const data = JSON.parse(res.data)
  console.log('收到消息:', data)
})

// 监听关闭
socketTask.onClose(() => { console.log('连接关闭') })

// 监听错误
socketTask.onError((err) => { console.error('连接错误:', err) })

// 关闭连接
socketTask.close({ code: 1000, reason: '正常关闭' })
```

> 注意：微信小程序最多 5 个 WebSocket 连接。

---

## 请求拦截器

```js
// 全局请求拦截
uni.addInterceptor('request', {
  invoke(args) {
    // 请求前：添加 baseURL 和 token
    if (!args.url.startsWith('http')) {
      args.url = 'https://api.example.com' + args.url
    }
    args.header = {
      ...args.header,
      'Authorization': `Bearer ${uni.getStorageSync('token')}`
    }
  },
  success(res) {
    // 响应后：统一处理 401
    if (res.data?.code === 401) {
      uni.removeStorageSync('token')
      uni.reLaunch({ url: '/pages/login/login' })
    }
  },
  fail(err) {
    uni.showToast({ title: '网络异常', icon: 'none' })
  }
})

// 路由拦截（登录守卫）
uni.addInterceptor('navigateTo', {
  invoke(args) {
    const token = uni.getStorageSync('token')
    const protectedPages = ['/pages/mine/mine', '/pages/order/order']
    if (!token && protectedPages.some(p => args.url.startsWith(p))) {
      uni.navigateTo({ url: '/pages/login/login' })
      return false  // 阻止原始跳转
    }
  }
})

// 移除拦截器
uni.removeInterceptor('request')
```

---

## Vite 构建配置

```js
// vite.config.js（仅 Vue3）
import { defineConfig } from 'vite'
import uni from '@dcloudio/vite-plugin-uni'

export default defineConfig({
  plugins: [uni()],
  define: {
    __APP_VERSION__: JSON.stringify('1.0.0')
  },
  build: {
    minify: 'terser',
    terserOptions: {
      compress: { drop_console: true }  // 生产环境移除 console
    }
  }
})
```

---

## WebView 组件

```vue
<template>
  <web-view
    :src="webUrl"
    :webview-styles="{ progress: { color: '#007AFF' } }"
    @message="onMessage"
  />
</template>

<script setup>
import { ref } from 'vue'

const webUrl = ref('https://example.com')

const onMessage = (e) => {
  // 接收 H5 页面通过 uni.postMessage 发来的消息
  console.log('来自 web-view:', e.detail.data)
}
</script>
```

**注意**：
- 小程序端需在后台配置业务域名白名单
- 本地 HTML 文件放在 `/hybrid/html/` 或 `/static/` 目录
- App 端可用 `evalJS()` 与 web-view 双向通信
