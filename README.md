# @i61/fancy-lib-flexible
## 基于lib-flexible修改，根据html标签的宽度、window.devicePixelRatio等自动设定html标签的font-size及data-dpr属性，支持自定义最大宽度(兼容了ipad类似的尺寸屏幕)。


## 安装
```
npm config set registry http://verdaccio.61info.com/
npm install @i61/fancy-lib-flexible
```

## 全局引入

```
import '@i61/fancy-lib-flexible'

或者写成下面这样：

import fancyLibFlexible from '@i61/fancy-lib-flexible'
fancyLibFlexible.setMaxWidth(width) // 已默认为768(ipad宽度)，可自定义设备最大宽度，无特殊需要时可不写。
```

## 使用场景
### 1、全局变量
```
window.lib ==> {
  dpr: 3,
  rem: 54,
  px2rem: ƒ (e),
  refreshRem: ƒ g(),
  rem2px: ƒ (e),
}
```

### 2、结合html标签data-dpr属性启用不同图片
```
.btn-android {
  background-image: url("../img/@2x/android.png?v=@@version");
  [data-dpr="3"] & {
    background-image: url("../img/@3x/android.png?v=@@version");
  }
}
```