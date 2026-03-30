# pages.json 配置详解

官方文档：https://uniapp.dcloud.net.cn/collocation/pages.html

## globalStyle（全局窗口样式）

```json
{
  "globalStyle": {
    "navigationBarTitleText": "页面标题",
    "navigationBarBackgroundColor": "#007AFF",
    "navigationBarTextStyle": "white",           // white | black
    "navigationStyle": "default",                // default | custom（自定义导航栏）
    "backgroundColor": "#F8F8F8",
    "backgroundTextStyle": "dark",               // light | dark（下拉 loading 样式）
    "enablePullDownRefresh": false,
    "onReachBottomDistance": 50,                 // 触底距离（px）
    "usingComponents": {},
    "rpxCalcMaxDeviceWidth": 960,
    "rpxCalcBaseDeviceWidth": 375,
    "pageOrientation": "portrait"                // portrait | landscape
  }
}
```

## pages（页面配置）

```json
{
  "pages": [
    {
      "path": "pages/index/index",              // 必填，相对于项目根目录
      "style": {
        "navigationBarTitleText": "首页",
        "enablePullDownRefresh": true,
        "navigationStyle": "custom",            // 自定义导航栏
        "disableScroll": false,                 // 禁止页面整体滚动
        "app-plus": {                           // App 平台专属
          "titleNView": {
            "buttons": [{ "text": "按钮", "fontSize": "16px" }]
          }
        },
        "mp-weixin": {                          // 微信小程序专属
          "usingComponents": {}
        },
        "h5": {                                 // H5 专属
          "pullToRefresh": { "color": "#007AFF" }
        }
      }
    }
  ]
}
```

## tabBar（底部/顶部导航栏）

```json
{
  "tabBar": {
    "color": "#7A7E83",                         // 未选中文字颜色
    "selectedColor": "#007AFF",                 // 选中文字颜色
    "borderStyle": "black",                     // black | white（边框颜色）
    "backgroundColor": "#ffffff",
    "position": "bottom",                       // bottom | top（top 仅微信小程序支持）
    "fontSize": "10px",
    "iconWidth": "24px",
    "spacing": "3px",
    "height": "50px",
    "midButton": {                              // 中间突出按钮（App/H5）
      "width": "80px",
      "height": "50px",
      "text": "发布",
      "iconPath": "static/plus.png",
      "iconWidth": "24px",
      "backgroundImage": "static/mid-bg.png"
    },
    "list": [
      {
        "pagePath": "pages/index/index",        // 必须是 pages 中已注册的页面
        "text": "首页",
        "iconPath": "static/tab/home.png",      // 图标路径（81×81px 推荐）
        "selectedIconPath": "static/tab/home-active.png",
        "iconfont": {                           // 字体图标（与 iconPath 二选一）
          "text": "\ue102",
          "selectedText": "\ue103",
          "fontSize": "24px",
          "color": "#7A7E83",
          "selectedColor": "#007AFF"
        },
        "visible": true                         // 是否显示（App 3.2.10+）
      }
    ]
  }
}
```

> tabBar 页面跳转只能用 `uni.switchTab()`，`navigateTo` / `redirectTo` 无效。

## subPackages（分包加载）

```json
{
  "subPackages": [
    {
      "root": "subpkg-user",                    // 分包根目录
      "pages": [
        { "path": "profile/profile" },
        { "path": "settings/settings" }
      ]
    },
    {
      "root": "subpkg-order",
      "pages": [
        { "path": "list/list" },
        { "path": "detail/detail" }
      ]
    }
  ],
  "preloadRule": {                              // 分包预加载
    "pages/index/index": {
      "network": "all",                         // all | wifi
      "packages": ["subpkg-user"]
    }
  }
}
```

> 主包放 tabBar 页面和公共资源；分包用于按需加载，减小首屏包体积。
> App 端分包需在 manifest.json 中额外开启。

## easycom（自动引入组件）

```json
{
  "easycom": {
    "autoscan": true,                           // 默认 true，自动扫描 components 目录
    "custom": {
      "^uni-(.*)": "@dcloudio/uni-ui/lib/uni-$1/uni-$1.vue",
      "^my-(.*)": "@/components/my-$1/my-$1.vue",
      "^van-(.*)": "vant-weapp/dist/$1/index"
    }
  }
}
```

easycom 规则：组件符合 `components/comp-name/comp-name.vue` 目录结构即可自动引入，无需 import / components 声明。

## condition（启动模式配置，仅开发期间）

```json
{
  "condition": {
    "current": 0,
    "list": [
      {
        "name": "调试详情页",
        "path": "pages/detail/detail",
        "query": "id=123"
      }
    ]
  }
}
```

## networkTimeout（网络超时）

```json
{
  "networkTimeout": {
    "request": 60000,
    "connectSocket": 60000,
    "uploadFile": 60000,
    "downloadFile": 60000
  }
}
```
