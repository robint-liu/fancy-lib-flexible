# @i61/fancy-lib-flexible
### 基于lib-flexible修改，根据html标签的宽度、window.devicePixelRatio等自动设定html标签的font-size及data-dpr属性，支持自定义最大宽度(兼容了ipad类似的尺寸屏幕)。


## 安装
```bash
npm install @i61/fancy-lib-flexible -S
```

```bash
yarn add @i61/fancy-lib-flexible -S
```
## 引入

```js
import '@i61/fancy-lib-flexible'

// 或者写成下面这样：

import fancyLibFlexible from '@i61/fancy-lib-flexible'
fancyLibFlexible.setMaxWidth(666) // 默认值为768(ipad宽度)，可自定义设备最大宽度，无特殊需要时可不写。
```

## 用法
### 1、全局变量
```js
window.lib ==> {
  flexible:{
    dpr: 3,
    rem: 37.5,
    px2rem: function (d) {
      var val = parseFloat(d) / this.rem;
      if (typeof d === 'string' && d.match(/px$/)) {
        val += 'rem';
      }
      return val;
  },
    refreshRem: function refreshRem() {
      var width = docEl.getBoundingClientRect().width;
      if (width > maxWidth) {
        width = maxWidth;
      }
      var rem = width / 10;
      docEl.style.fontSize = rem + 'px';
      flexible.rem = win.rem = rem;
    },
    rem2px: function (d) {
      var val = parseFloat(d) * this.rem;
      if (typeof d === 'string' && d.match(/rem$/)) {
        val += 'px';
      }
      return val;
    },
  }
}
```

### 2、结合html标签data-dpr属性加载不同的图片
```css
.btn-android {
  background-image: url("../img/@2x/android.png?v=@@version");
  [data-dpr="3"] {
    background-image: url("../img/@3x/android.png?v=@@version");
  }
}
```