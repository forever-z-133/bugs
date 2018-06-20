
大段文字看起来眼睛好累，所以我随便按每10个进行一次分割。  
如果你有更好的展现形式，欢迎投稿，非常感谢！

# 记录一些我自己认为是BUG的坑眼

* 小程序的 `cover-view` 不能使用 `:before` 和 `gradient` 样式
* `disabled` 会禁掉 `mouse` 事件，却没有禁 `touch` 事件
* `$.fn.serializeArray` 方法会把回车 `\n` 改为 `\r\n`，增加了字符串长度
* `Math.round` 四舍五入方法可能有误，见 [推文](https://mp.weixin.qq.com/s/MlnVE0_bWHVGb7MAPBBG1Q)
* 看 [源码](https://blog.csdn.net/lixuepeng_001/article/details/53742589) 发现，`Array.sort` 是要返回正负，而非布尔值
* 浏览器开始禁止音频视频的自动播放，暂时无解
* `<a><a>x</a></a>` 会被解析为 `<a></a><a>x</a>`，但动态添加（append 或 innerHTML）的话可以嵌套
* `location.origin` 在 IE11 以下不兼容

-----

* 自写推文代码遇坑，svg 仅支持闭合标签（即 `<rect></rect>`），不支持 `position`
* 粘贴功能 `execCommand('paste')` 被各家浏览器禁用掉了
* 小程序的 `cover-view` 手机上不触发 touch 事件
* 小程序的 `cover-image` 不能单独定位，如果父级 `cover-view` 定位了那倒可以了
* 写 HTML 时两个节点间有换行或空格，需要两次 nextSibling 才能找到上一个节点，因为中间多了一个空白的 text 节点
* 小程序的 toast 和 loading 等其实解决不了点击太快的问题，还得靠变量来阻止才行
* `inline` 行级元素设置 `transform` 无效
* 苹果机没有原生双击事件 `dblclick`
* `:not(.x):last-of-type` 并不代表去掉 `.x` 后的最后一个，它们是或者关系而非并且关系
* `table-layout: fixed` 表示不再自动分配宽度，傻逼的我还以为是固定 `thead` 达到类似 `position:fixed` 的效果

-----

* `writing-mode:vertical-rl`;在 Safari 上异常（无解，等于苹果浏览器不能玩耍了）
* `translate3d` 下的 `fixed` 失效，与 `absolute` 等效，反正能不用 fixed 绝不用
* `touchend` 或 `tap` 会出现事件穿透，其实浏览器已经做了优化，`click` 是可以满足我们的要求的。但拖拽里套点击，差异很大有待研究
* 元素未显示时的 swiper 的初始化是有误的，`mySwiper.update()` 有效
* 苹果机 `new Date(d)` 时 `d` 不能采用 "xxxx-xx-xx" 格式，必须分开成多个参数
* `display:flex` 被 `display: none` 覆盖后再使用 jquery 的 `fadeIn()` 将显示 `display: block`
* 苹果机有滚动反弹，与 `position: fixed` 一起玩耍时很可怕
* `clip:rect(1,2,3,4)` 必须要和 `absolute` 合用，且 2&3 必须有(作为宽高)，更推荐使用 `clip-path`
* `scaleX` 等的默认值是 0 不是 1，所以小心 css 动画时会有一闪的状态，虽然通常我们会用 `scale(x, y)` 更多

-----

* `text-transform` 有时会在跳页时回归最初（什么特定情况还未总结出）
* 极少部分苹果机图片加载会阻塞后续程序
* 最好不要 `for` 里面套 ajax，不然你的服务器会超级崩溃的，当然浏览器也会报出请求过量的错误
* overflow:hidden 在子级 transform 时无效，需要再套一层父级，有时子级的父级也无效，需要祖父级添加 overflow:hidden
* setTimeout("x()",500) 的 x 必须为全局函数，否则报错，所以还是用 setTimeout(x,500) 吧，同理 `<div onclick="aaa()">` 的 aaa 也必须是全局函数
* 有些手机 `<audio>` 不支持 m4a 格式的音频
* 禁用了 `window` 的 `touchstart` 后 `input` 也不能点了
* 苹果机的 `blur` 自主触发有问题，有待实验
* `iframe` 套的网页会缓存，修改后刷新可能无效，且会保存 history，最好用一次就新建删除一次
* `<datalist>` 并不好用，有时会不出现内容，且样式不可控，不推荐使用

-----

* 苹果手机自动播放音频得放在 `wx.ready` 里面
* 摇一摇事件有时清除不掉，可能是触发太多烧机器，推荐再加个变量控制开关
* `onstorage` 事件监听必须两个页面都打开着才能互传信息
* `submit` 和 `button` 不能套在 `a` 里面，否则 `onsubmit` 事件将消失
* 自己写的 Object.prototype.has 与 jquery 的 Tween 冲突，换个名字吧
* 苹果机的渐变 `transparent` 可能会呈现为黑色，可用 `rgba(255,255,255,0)`；但渐变中也会出现半透明黑，得依情况改 rgb 三值
* 苹果机 `rotateY` 问题超烦，旋转的一半后沉于 `body` 的背后不显示，需要 `translateZ` 来处理
* 大部分苹果机微信支付后无法再横屏
* 部分老牌机 `window.orientation` 不准，进去就是 90，多转几次又好了，十分偶现
* `setInterval` 设置 `document.title` 移动端效果非常不稳定，用 `requestAnimationFrame` 就好了

-----

* `absolute` 下的 `offsetLeft` 会以父级定位的相对位置来计算（可能有误，以后研究）
* `Object.assign` 的 `this` 指向有待研究
* 移动端同个 `input[type="file"]` 的 change 事件只触发一次
* if lt IE 只能判断到 9，10及10以上及edge都无效
* sourceTree 上传，大小写不区分，比如 Index 和 index
* `touchend` 时 `touches` 是已经不存在了的
* canvas 的 `globalAlpha` 小于 0 时会按 1 来计算
* 函数传参时最后多打个逗号，PC正常显示，但在移动端把后续程序全部卡住
* 在 Vue 实例元素内，自己 append 出来的元素是无法修改的
* `Vue.component` 必须放在 `new Vue` 前面

-----

* svg 的 `image` 必须带宽高，否则 firefox 等浏览器不显示
* `input` 弹出的虚拟键盘仅 number 有下一步这样的功能键
* `flex` 下的 `<img width="50%">` 高度 `auto` 会失效，需 `align-item: flex-start`
* background 只支持 .svg 文件式的引用，无法使用 #xxx 代码式的引用
* 多个 `transition-property` 会触发多次 `transitionEnd`，注意 border / padding 会触发四次
* 多个 jquery 对象会触发多次动画回调，如 `$('.x1, .x2').show(cb)` 会触发两次 cb
* 小程序的音频最好不要超过 8 个，不然总是有警告
* 苹果机小程序背景音乐调不了音量
* delete 只能删数组和对象里的键值，不能删除变量、函数和函数的参数。比如 `var a = 1; delete a; alert(a); // 2`
* firefox 在 mask-size 小于 100% 时各种卡，大于时还行，不知怎么办
* 微信放视频没有自动播放，需要点击触发。可见此 [教程](http://www.cnblogs.com/foreverZ/p/6038950.html)
