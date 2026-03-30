# uni-app 生命周期完整参考

官方文档：https://uniapp.dcloud.net.cn/collocation/frame/lifecycle.html

## 应用生命周期（App.vue）

| 钩子 | 说明 | Vue3 import |
|------|------|-------------|
| `onLaunch` | 应用初始化完成，全局只触发一次 | `@dcloudio/uni-app` |
| `onShow` | 应用启动或从后台进入前台 | `@dcloudio/uni-app` |
| `onHide` | 应用进入后台 | `@dcloudio/uni-app` |
| `onError` | 脚本错误或 API 调用失败 | `@dcloudio/uni-app` |
| `onUniNViewMessage` | nvue 页面发送消息 | `@dcloudio/uni-app` |
| `onUnhandledRejection` | 未处理的 Promise 拒绝 | `@dcloudio/uni-app` |
| `onThemeChange` | 主题变化 | `@dcloudio/uni-app` |

```vue
<!-- App.vue -->
<script setup>
import { onLaunch, onShow, onHide } from '@dcloudio/uni-app'

onLaunch((options) => {
  // options.path: 打开的页面路径
  // options.query: 打开时的 query 参数
  // options.scene: 打开场景值（小程序）
  console.log('App 初始化', options)
})
</script>
```

## 页面生命周期

| 钩子 | 说明 | 参数 |
|------|------|------|
| `onLoad` | 页面加载，只触发一次 | options（页面参数对象） |
| `onShow` | 页面显示（每次进入页面均触发） | — |
| `onReady` | 页面首次渲染完成，只触发一次 | — |
| `onHide` | 页面隐藏（navigateTo 跳走时触发） | — |
| `onUnload` | 页面卸载（redirectTo/navigateBack 时触发） | — |
| `onPullDownRefresh` | 下拉刷新（需配置 enablePullDownRefresh） | — |
| `onReachBottom` | 滚动到页面底部 | — |
| `onPageScroll` | 页面滚动 | { scrollTop } |
| `onResize` | 屏幕旋转/尺寸变化 | { size } |
| `onTabItemTap` | 当前 tab 页被再次点击 | { index, text, pagePath } |
| `onShareAppMessage` | 用户点击右上角分享 | { from, target } |
| `onShareTimeline` | 用户点击右上角"分享到朋友圈"（仅微信） | — |
| `onAddToFavorites` | 用户点击收藏（仅微信） | — |
| `onNavigationBarButtonTap` | 原生导航栏按钮点击 | { index } |
| `onNavigationBarSearchInputChanged` | 导航栏搜索内容变化 | — |
| `onBackPress` | 页面返回（返回 true 阻止默认返回） | { from } |

```vue
<script setup>
import {
  onLoad, onShow, onReady, onHide, onUnload,
  onPullDownRefresh, onReachBottom, onPageScroll
} from '@dcloudio/uni-app'

onLoad((options) => {
  const { id, type } = options   // 接收 navigateTo url 中的 query 参数
})

onPullDownRefresh(async () => {
  await fetchData()
  uni.stopPullDownRefresh()      // 必须调用，否则加载动画不停
})

onReachBottom(() => {
  if (hasMore.value) loadMore()
})

onPageScroll(({ scrollTop }) => {
  showBackTop.value = scrollTop > 300
})
</script>
```

## 组件生命周期

uni-app 组件支持 Vue 标准生命周期（非页面生命周期）：

| Vue3 钩子 | 说明 |
|-----------|------|
| `onBeforeMount` | 挂载前 |
| `onMounted` | 挂载后（DOM 可用） |
| `onBeforeUpdate` | 更新前 |
| `onUpdated` | 更新后 |
| `onBeforeUnmount` | 卸载前 |
| `onUnmounted` | 卸载后 |

> 组件内不能使用 `onLoad`、`onShow` 等页面生命周期，只有页面才有这些钩子。

## 执行顺序

页面进入：`onLoad` → `onShow` → `onReady`

navigateTo 跳转：A `onHide` → B `onLoad` → B `onShow` → B `onReady`

navigateBack 返回：B `onUnload` → A `onShow`

redirectTo：当前页 `onUnload` → 新页 `onLoad` → `onShow` → `onReady`

## App 端特有

```js
// 监听应用进入后台
plus.globalEvent.addEventListener('pause', () => {})
// 监听应用回到前台
plus.globalEvent.addEventListener('resume', () => {})
```
