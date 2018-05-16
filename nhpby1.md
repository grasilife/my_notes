# CSS3 超实用属性：pointer-events

最近发现了一个叫pointer-events的css属性，是一个与javascript有关的属性，pointer-events直译为__指针事件__，当把值设置为none后，他有如下相关特性。
1. 阻止用户的点击动作产生任何效果
2. 阻止缺省鼠标指针的显示
3. 阻止CSS里的hover和active状态的变化触发事件
4. 阻止JavaScript点击动作触发的事件
一条CSS可以做许多事情是不是很神奇，我们在看一下兼容性情况如何。
IE 　11+
Firefox 　3.6＋
Chrome　4.0+
Safari　　6.0
Opera　 15.0
iOS Safari   6.0
Android Browser　2.1+
Android Chrome　18.0+
看下实例，具体是怎么回事。html代码：
```html
<!DOCTYPE html>
<html>
<head>
<style>
  a[href="http://example.com"] {
      pointer-events: none;
  }
</style>
</head>
<body>
<ul>
    <li><a href="https://www.baidu.com/">百度</a></li>
    <li><a href="http://example.com">一个不能点击的链接</a></li>
</ul>
</body>
</html>


```
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">第二个a标签不仅无法被点击，而且没有鼠标手形样式。再看一个例子</span></span>
```html
<!DOCTYPE html>
<html>
<head>
<style>
.bottom {
    background: yellow;
    width: 100px;
    height: 100px;
}
.top {
    width: 100px;
    height: 100px;
    position: absolute;
    top: 0;
    left: 0;
}
</style>
</head>
<body>
    <!-- 下方div -->
    <div class="bottom">
        <a href="www.baidu.com">bottom-百度</a>
    </div>
    <!-- 上方div -->
    <div class="top"></div>
</body>
</html>
```
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">此时由于top的div位于a标签之上，无法点击到a标签。</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">如果我们给上方的top层加上一个pointer-events属性后：</span></span>
```css
.top {
  pointer-events: none;
}
```
我们就可以穿过top层去点击下面的a标签了，此时这个top层如果有颜色的话相当于可看不可摸了.

为什么说这个属性非常的实用呢，在许多网站上过节的时候页面最上层会用canvas绘制的雨、雪花，避免这些悬浮物遮挡住页面从而影响鼠标点击，可以使用pointer-events=none属性，让这些上方的canvas不会遮挡鼠标事件，让鼠标事件可以穿透上方的canvas来点击页面.

参考资料:[https://www.jianshu.com/p/3eba945fc19e](https://www.jianshu.com/p/3eba945fc19e)

