# 利用动态viewport+rem制作一张自适应的svg雪碧图icon

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(247, 247, 247)">先看下主流浏览器 、手机的尺寸和分辨率</span></span>


![image.png | left | 700x3839](https://cdn.nlark.com/yuque/0/2018/png/111166/1532949609483-efd667e8-0c6d-48ba-b15a-7d2d6e11fc8a.png "")

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(247, 247, 247)">移动端雪碧图的痛点-不能自适应</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">移动端的icon大小不是不定的，如果用px固定住，在高分辨率手机中就会变得很小在低分辨率手机中就会变得很大。</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">所以手机都拿icon图标需要用百分比来或者用rem布局来调整icon的大小。</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(247, 247, 247)">background-position百分比计算公式</span></span>
```
x：（容器的宽度-图片的宽度）x (50%)
y：（容器的高度-图片的高度）x (30%)
```
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">比如：容器是width：600px；height：600px；而图片是width：200px；height：200px；</span></span>
```
.icon{
    width: 600px;
    height: 200px;
    background:#FFF url(image) no-repeat fixed 50% 30%;
}
```


![image.png | left | 506x400](https://cdn.nlark.com/yuque/0/2018/png/111166/1532949709808-f8416a5e-ffbe-4e75-a0a1-7b8029a12145.png "")

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">background-position:0% 0%;表示左上角对齐</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">background-position:100% 0%;表示右上角对齐</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">动态viewport最初是由手淘使用来解决适应各种手机分辨率的一个解决方案：</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">会根据手机的分辨率和比率rate生成一个最佳的viewpoint和相对应基准的font-size大小;</span></span>
# <a name="z31sps"></a>viewport.js
```javascript
!function(win) {
    function resize() {
        var domWidth = domEle.getBoundingClientRect().width;
        if(domWidth / v > 540){
            domWidth = 540 * v;
        }
        win.rem = domWidth / 10;
        domEle.style.fontSize = win.rem + "px";
        var rem= win.rem;
    }
    var v, initial_scale, timeCode, dom = win.document, domEle = dom.documentElement, viewport = dom.querySelector('meta[name="viewport"]'), flexible = dom.querySelector('meta[name="flexible"]');
    if (viewport) {
        var o = viewport.getAttribute("content").match(/initial\-scale=(["']?)([\d\.]+)\1?/);
        if(o){
            initial_scale = parseFloat(o[2]);
            v = parseInt(1 / initial_scale);
        }
    } else if(flexible) {
        var o = flexible.getAttribute("content").match(/initial\-dpr=(["']?)([\d\.]+)\1?/);
        if (o) {
            v = parseFloat(o[2]);
            initial_scale = parseFloat((1 / v).toFixed(2))
        }
    }
    if (!v && !initial_scale) {
        var n = (win.navigator.appVersion.match(/android/gi), win.navigator.appVersion.match(/iphone/gi));
        v = win.devicePixelRatio;
        v = n ? v >= 3 ? 3 : v >= 2 ? 2 : 1 : 1, initial_scale = 1 / v
    }
    //没有viewport标签的情况下
    if (domEle.setAttribute("data-dpr", v), !viewport) {
        if (viewport = dom.createElement("meta"), viewport.setAttribute("name", "viewport"), viewport.setAttribute("content", "initial-scale=" + initial_scale + ", maximum-scale=" + initial_scale + ", minimum-scale=" + initial_scale + ", user-scalable=no"), domEle.firstElementChild) {
            domEle.firstElementChild.appendChild(viewport)
        } else {
            var m = dom.createElement("div");
            m.appendChild(viewport), dom.write(m.innerHTML)
        }
    }
    win.dpr = v;
    win.addEventListener("resize", function() {
        clearTimeout(timeCode), timeCode = setTimeout(resize, 300)
    }, false);
    win.addEventListener("pageshow", function(b) {
        b.persisted && (clearTimeout(timeCode), timeCode = setTimeout(resize, 300))
    }, false);
    resize();
}(window);

```

CSS3的出现，他同时引进了一些新的单位，包括我们今天所说的rem。在W3C官网上是这样描述rem的——“font size of the root element” 。
关于rem两个传送门
[http://www.w3cplus.com/css3/define-font-size-with-css3-rem](https://link.jianshu.com?t=http://www.w3cplus.com/css3/define-font-size-with-css3-rem)
[http://xiaoho.com/webapp-font-size/](https://link.jianshu.com?t=http://xiaoho.com/webapp-font-size/)

## <a name="k3swed"></a>html
```html
<span class="i i_menu_0"></span>
```
## <a name="80tkvr"></a>css
```css
.i {
    width: 0.8rem; height: 0.8rem;
    background: url(../images/ico_global.svg) no-repeat;
    display: inline-block;
    background-size: 1100%;
}
.i_menu_0 { background-position: 0% 0%; }
.i_menu_1 { background-position: 10% 0%; }
.i_menu_2 { background-position: 20% 0%; }
.i_menu_3 { background-position: 30% 0%; }
.i_menu_4 { background-position: 40% 0%; }
.i_menu_5 { background-position: 50% 0%; }

```


上面有两个关键属性background-size:1100%;background-position:x% x%;

为什么是1100%
看我的svg图就知道了


![image.png | left | 700x676](https://cdn.nlark.com/yuque/0/2018/png/111166/1532949868506-87f88643-3c7b-4d91-bf3b-8b94e63459fd.png "")

我把一张图片平均分成11×11的正方形格子，之所以用11×11的正方形格子，
是因为background-position: 0% 0%;是第一个格子,是从零开始计数,所以0%-100%可以平均分成最多11个整数。
当然你可以分成，3×3的格子
0%代表第一个格子
50%代表中间的格子
100%代表最后一个格子


![image.png | left | 222x220](https://cdn.nlark.com/yuque/0/2018/png/111166/1532949883525-e7051e5e-626d-4e9a-a22d-bae7811e84df.png "")


<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(247, 247, 247)">优点</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">矢量化，文件大小更小，图标更清晰,加载速度更快</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">支持渐变背景和支持多色彩icon</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">调用方便</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(247, 247, 247)">缺点</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">由于没有svg雪碧图的自动化构建工具，所有的图片都只能人工维护，维护成本有些高。</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">兼容性不是很好,但是如果你是做移动端，可以不用考虑这个问题。因为大多移动端都支持svg图片。</span></span>


![image.png | left | 700x552](https://cdn.nlark.com/yuque/0/2018/png/111166/1532949925544-5598df93-8f7b-4491-a0c9-dcaa1b806f4f.png "")

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">关于svg优雅的降级可以查看张鑫旭的这篇博客</span></span>
[http://www.zhangxinxu.com/wordpress/2013/09/svg-fallbacks/](https://link.jianshu.com/?t=http://www.zhangxinxu.com/wordpress/2013/09/svg-fallbacks/)

参考资料：[https://www.jianshu.com/p/91dc6d5ab88c](https://www.jianshu.com/p/91dc6d5ab88c)
