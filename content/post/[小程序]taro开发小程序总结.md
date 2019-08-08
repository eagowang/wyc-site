---
title: "[小程序]Taro开发小程序总结"
author: "eago"
tags: ["taro", "小程序"]
categories: ["小程序"]
date: 2019-05-23T11:29:41+08:00
draft: false
---

## 小程序

1. 小程序可以使用字体图标，下载字体文件到本地，将 iconfont.css 中的 font-face 替换成在线地址即可
2. 动态删减小程序 tabbar item，会出现抖动。原因是每个 page 都有一个 tabbar 实例，每进入一个 tabbar 都要重新生成。所以会先看到旧的。暂无解决办法
3. 自定义 shareAction 会被 tabbar 遮挡住。解决办法：自定义 tabbar 支持显示隐藏，打开 shareAction 时，隐藏 tabbar
4. 小程序 webview（业务域名）支持一级域名
5. 普通二维码进入小程序，只有 q 参数，并且需要 decodeURIComponent
6. 小程序真机不能显示//test.rabbitpre.com/a.png 这样的图片，要加上 https(开发工具是可以展示的，有误导)
7. 小程序 getUserInfo 发生在 wx.login 之前，会出现 illegal buffer 错误。解决办法：wx.login 成功回调之后再 getUserInfo
8. 小程序 switchTab 不能带参数，解决办法，使用全局变量传递，用完清除掉
9. 小程序 swiper 动态减少后，current 大于 swiperItem 数量，swiper 就会空白，解决办法：加入 current 属性，并手动设置
10. 第三方平台小程序模板开发，可以使用 ext.json，配置默认的 appId 和额外信息

```json
{
  "extEnable": true,
  "extAppid": "",
  "ext": {
    "appId": ""
  }
}
```

还需在 taro 配置中添加如下配置，否则不会主动 copy

```json
copy: {
    patterns: [
      {
        from: 'src/ext.json',
        to: '../var/static/ext.json',
      },
    ],
    options: {},
  },
```

11. 取消授权后，可以先 getSetting，判断有无授权，无授权 openSetting，提示去授权

```javascript
Taro.getSetting({
      success: async res => {
        if (res.authSetting['scope.writePhotosAlbum'] === false) {
          Taro.showModal({
            title: '',
            content: '请打开“保存到相册”权限',
            success(res) {
              if (res.confirm) {
                Taro.openSetting({
                  success(res) {

                  },
                });
              }
            },
          });
        } else {
        }
      }
```

## taro

1. 使用 static options= {adGlobalClassClass: true}，不在组件 less 文件中引入 common.less 能减少生成代码体积
2. 当前开发使用的 taro 版本不支持在 render 以外的地方定义 jsx
3. 无法使用高阶组件
4. 路由参数\$router.params 的属性不能和组件 state 重名，因为 taro 会把他们合并为一个对象
5. taro-mobx 在 JSX 中使用变量时，不能用到对象属性，比如：abc.xyz，需要先 const xyz = abc.xyz，然后在 JSX 中直接使用 xyz
6. taro 官方构建不支持单独编译某个文件，即 webpack 中的 include 属性无效。
7. 组件之间无法通过外部样式传递 className 属性。解决方案，通过其他 props 判断添加不同的 class
8. 不支持动态组件，循环不同组件的数组时会报错，只能一个个罗列

## 其他

1. iphoneX 兼容底部操作栏兼容，自定义导航栏兼容

2. image-cropper 插件在 iphone 中，初始化图片不会居中。解决办法：手动调用一次 imageReset

3. 在小程序 onShow 时使用 Taro.eventCenter.on 监听事件埋点，需要在 onHide 时 Taro.eventCenter.off,并且要注意 on,off 的引用不变。否者会出现隐藏/显示/隐藏/显示后上报累加的问题
