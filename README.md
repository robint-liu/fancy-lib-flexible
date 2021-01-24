# @i61/fancy-lib-flexible
### 基于lib-flexible修改，根据html标签的宽度、window.devicePixelRatio等自动设定html标签的font-size及data-dpr属性。


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
window.lib.flexible.setMaxWidth(666) // 默认值为768(ipad宽度)，可自定义设备最大宽度，无特殊需要时可不写。
```

## 用法
### 1、全局变量
```js
window.lib ==> {
  flexible:{
    dpr: 3, // 当前设备像素比
    rem: 37.5, // 当前rem值
    /** 
    * 更新html fontSize，更新当前rem值
    */
    refreshRem: function refreshRem() {
      var width = docEl.getBoundingClientRect().width;
      if (width > maxWidth) {
        width = maxWidth;
      }
      var rem = width / 10;
      docEl.style.fontSize = rem + 'px';
      flexible.rem = win.rem = rem;
    },
    /** 
    * 将指定px值转为对应rem
    * @param {number} d px值
    * @return {string} 对应rem，带单位rem
    */
    px2rem: function (d) {
      var val = parseFloat(d) / this.rem;
      if (typeof d === 'string' && d.match(/px$/)) {
        val += 'rem';
      }
      return val;
    },
    /** 
    * 将指定rem值转为对应px
    * @param {number} d rem值
    * @return {string} 对应px，带单位px
    */
    rem2px: function (d) {
      var val = parseFloat(d) * this.rem;
      if (typeof d === 'string' && d.match(/rem$/)) {
        val += 'px';
      }
      return val;
    },
    /** 
    * 设置最大逻辑像素宽度限定值，默认值为768。
    * @param {number} width 宽度值
    * @return {undefined}
    */
    setMaxWidth: function (width) {
      if (isNaN(width)) {
        throw new Error("function setMaxWidth`s param is invalid！")
      }
      maxWidth = width
      refreshRem();
    }
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