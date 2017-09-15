# 记录一些我自己认为是BUG的坑眼

* writing-mode:vertical-rl;在 Safari 上异常（无解，等于苹果浏览器不能玩耍了）
* transform 下的 fixed 失效，与 absolute 等效（能不用 fixed 绝不用）
* touchend 或 tap 会出现事件穿透，其实浏览器已经做了优化，click 是可以满足我们的要求的
* 元素未显示时的 swiper 的初始化是有误的，mySwiper.update() 有效
* 苹果机 new Date(d) 时 d 不能采用 "xxxx-xx-xx" 格式，必须分开成多个参数
* display:flex 被 display: none 覆盖后再使用 jquery 的 fadeIn() 将显示 display: block
* 苹果机有滚动反弹，与 position: fixed 一起玩耍时很可怕
* clip:rect() 必须要和 absolute 合用，且 (1,2,3,4) 2&3 必须有(作为宽高)
* scaleX 等的默认值是 0 不是 1，所以动画时会有一闪的状态
* text-transform 有时会在跳页时回归最初，比如全部大写的跳页再回来会出现明显的小写变大写的过程（什么特定情况还未总结出）
* 极少部分苹果机图片加载会阻塞后续程序
* 最好不要 for 里面套 ajax，不然你的服务器会超级崩溃的，当然浏览器也会报出请求过量的错误
* overflow:hidden 在子级 transform 时无效，需要再套一层父级，有时子级的父级也无效，需要祖父级添加 overflow:hidden
* setTimeout("x()",500) 的 x 必须为全局函数，否则报错，所以还是用 setTimeout(x,500) 吧，同理 <div onclick="aaa()"> 的 aaa 也必须是全局函数
* audio 有些手机不支持 m4a 格式的音频
* 禁用了 touchstart 后 input 也不能点了
* 苹果机的 blur 有问题，有待实验
* iframe 套的网页会缓存，修改后刷新可能无效，且会保存 history，最好用一次就新建删除一次
* 项目较大时，全局事件里面加 alert，容易产生混淆，如快速两次 click，第一次弹窗，第二次点击算什么呢
* <datalist> 并不好用，有时会不出现内容，且样式不可控，不推荐使用
* 苹果手机自动播放音频得放在 wx.ready 里面
* 摇一摇事件有时清除不了，可能是触发太多烧机器，推荐再加个变量控制开关
* onstorage 事件监听必须两个页面都打开着才能互传信息
* submit 和 button 不能套在 a 里面，否则 submit 事件将消失
* 自己写的 Object.prototype.has 与 jquery 的 Tween 冲突，换个名字吧
* 苹果机的渐变 transparent 可能会呈现为黑色，用 rgba(255,255,255,0) 解决
* 苹果机 rotateY 问题超烦，旋转的一半后沉于 body 的背后不显示，需要 translateZ 来处理
* 大部分苹果机微信支付后无法再横屏
* 部分苹果机 window.orientation 不准，进去就是 90，多转几次又好了，所以最好还是使用宽高判断
* setInterval 设置 document.title 效果非常不稳定，用 requestAnimationFrame 就好了
* absolute 下的 offsetLeft 会以父级定位的相对位置来计算（可能有误，以后研究）
* Object.assign 的 this 指向有待研究
* 移动端同个 input[type="file"] 的 change 事件只触发一次
* if lt IE 只能判断到 9，10及10以上及edge都无效
* sourceTree 上传，大小写不区分，比如 Index 和 index
* touchend 时 touches 是已经不存在了的
* canvas 的 globalAlpha 小于 0 时会按 1 来计算
* 函数传参时最后多打个逗号，PC正常显示，但在移动端把后续程序全部卡住
* 在 Vue 实例元素内，自己 append 出来的元素是无法修改的
* Vue.component 必须放在 new Vue 前面
* svg 的 image 必须带宽高，否则 firefox 等浏览器不显示
* input 弹出的虚拟键盘仅 number 有下一步这样的功能键
* flex 下的 <img> 高度 auto 会失效，需 align-item: flex-start
* background 只支持 .svg 文件式的引用，无法使用 #xxx 代码式的引用