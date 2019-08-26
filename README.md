
大段文字看起来眼睛好累，所以我随便按每10个进行一次分割。  
如果你有更好的展现形式，欢迎投稿，非常感谢！

# 记录一些坑眼

* `\1` 在正则中，有匹配还好，没有的话请注意 `'\1'.split('')` 与 `/\1/.test('\1')` 的不同
* `eval([1,2] + '==' + 2);  // true`，感觉使用 `eval` 时还会有其他骚处理

-----

* `<select>` 的 `readonly` 还是能点开，推荐使用 `select[readonly] { pointer-events: none; }`
* `let` 和 `const` 不会像 `var` 一样会在 window 下声明，比如 `let a` 是取不到 `window.a` 的
* `wx.onMenuShareAppMessage` 的 `type` 不能是空字符串，要么不传，要么 `type: "link"`
* `wx.config` 需要传入的链接，苹果机下如果使用过 history api 将签名失败。
* Safari 和 IE9- 浏览器中，`option` 设 `display:none` 无效，可包一层隐藏的 `span` 或重新拼 dom
* CSS 的 `centent` 的文本和图片，是不可选择的
* 苹果机键盘弹起后元素上移，键盘收回后元素不归位，用 `$(document).scrollTop(0, 0);` 解决（部分机型依旧不行）
* 3.0 版本前的 `$.param` 会把空格转为 `+` 号，可能后来发现链接中的 + 与空格的 + 冲突所以砍掉了
* IOS 下的 webgl 不清晰，可显示 2d 的 canvas 绘制隐藏的 webgl 的 getImageDate 能清晰
* 小程序不会正确处理图片链接中 `\`，造成图片请求但不显示，只能是 `/` 式的路径，比如 [图片](http://images.duocaixing.net\undefined/2019-06-04/201906041118494757_wKgED1ws7UCAKPhVAAVr2lUbIUI02.jpeg)

-----

* 部分安卓机 `background-image` 与 `border-radius` 合用会不显示图片，需加上 `background-color` 才行
* `input[type="number"]` 不支持使用 selection 相关的光标操作
* 用 `data:image/svg+xml,` 拼出来的 SVG 背景图，`background-size` 不支持拉伸了。
* ES6 用变量作对象属性名时有点小问题，如 `var a = 'x'; var obj = { [a]: 1 }; obj[a]; // 1` 但 `obj.a` 不会
* 苹果机 Safari 下设 `user-scalable=no` 的 `<meta>` 无效
* `btoa` 转 base64 不支持传入中文等 Unicode 字符，可搭配 `encodeURIComponent` 使用
* 极少情况下 `textarea` 书写时双标签间有回车会不显示 `placeholder`，可能与编辑器有关
* IOS 的 `iframe` 不支持传高度，最好有个父级包着并设 `-webkit-overflow-scrolling` 滚动
* `[0, , 2, 3].indexOf()` 得 `-1`，`[0, undefined, 2, 3].indexOf()` 得 `1`
* `RegExp` 第二个参数，若传入 `'s'` 部分苹果机报错，看 [文档](http://www.w3school.com.cn/jsref/jsref_obj_regexp.asp) 确实说只能传 `'igm'`

-----

* 给 `option` 设 `label` 而不写在 `innerText`，部分苹果机会不显示文本但能滑动选择
* 在 vue 的根节点进行 `innerHTML += 'x'` 会造成 vue-router 失效，`appendChild` 是 OK 的
* `input[type="checkbox"]` 加字符串 `checked="false"` 或 `setAttribute('checked', '')` 也会勾选
* html 中 `data-userId` 会显示为全小写 `data-userid`，但 `attr('data-USERID')` 不区分大小写都能获取到
* UTF-16 字符在处理字符串时需注意，比如 `'𠮷'.slice(-1)` 会得到未知字符，恐怕只能用 `for-of` 来做了
* 空数组进行 `every` 判断始终为 `true`，需根据场景做好排除
* 在 SCSS 中 `@extend .x` 不仅会继承 `.x`，与其相关无论写在何处的 `h1.x` 也会被继承
* `:last-child` 是按 dom 位置来的，并不受 `order` 排序的影响
* 给伪元素的 `content` 直接加 `text-indent:-999em` 无效，需改为其他 `display` 才行，即 `inline` 不可以
* `JSON.stringify(Infinity) === "null"`（NaN 也是），`JSON.stringify({a: undefined}) === "{}"`（但 null 不会）

-----

* 父级 `overflow:auto; position:relative;`，子级绝对定位并超出，结果会显示滚动条，并非完全脱离文档流
* 父级无高度时，子级 `position: relative` 的百分比定位 `top: 50%` 会无效
* ueditor 插件初始化时会触发 `hashchange` 事件，希望你在这里面没有写什么操作
* `display: flex` 和子级 `margin: auto;` 合用时，效果很奇妙，比如居中/两个子级的自动空隙等
* `<script src="xx.js" />` 不能使用单标签格式，不然会把后面的都当做文本
* 属性选择器 `[id=value]` 中当 value 中有小数点时会报错，保险起见还是带双引号更好 `[id="value"]`
* 小程序
