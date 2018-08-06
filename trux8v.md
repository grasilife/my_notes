# margin为负

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">双飞翼和圣杯布局主要是利用margin为负值的原理；</span></span>
# <a name="bk4nng"></a>一、margin为负值产生的影响
## <a name="qad7og"></a>对于自身的影响
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">当元素不存在width属性或者（width：auto）的时候，负margin会增加元素的宽度；</span></span>
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<style>
.container{
        margin:0 auto;
        width: 500px;
        border: 1px #ccc solid;
        margin-bottom: 20px;
}
.box1{
    margin-left: -20px;
}
</style>
<div class="container">
    <div class="box1">
           I dont have the width
      </div>
  </div>

</html>
```
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">可以看到box1增加了20px宽度，margin-left和margin-right都是可以增加宽度，</span></span><span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(247, 247, 247)">margin-top为负值不会增加高度，只会产生向上位移，margin-bottom为负值不会产生位移，会减少自身的供css读取的高度</span></span>
## <a name="wat5re"></a>对文档流的影响
元素如果用了margin-left:-20px;毋庸置疑的自身会向左偏移20px和定位（position：relative）有点不一样的是，在其后面的元素会补位，也就是后面的行内元素会紧贴在此元素的之后。总结，不脱离文档流不使用float的话，负margin元素是不会破坏页面的文档流。


![image.png | left | 533x308](https://cdn.nlark.com/yuque/0/2018/png/111166/1532948649910-d51bd163-1c66-423d-b157-29a104dad3cb.png "")

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(247, 247, 247)">所以如果你使用负margin上移一个元素，所有跟随的元素都会被上移。</span></span>
## <a name="gmhmrn"></a>对浮动元素的影响
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<style>
    .flb {
        float: left;
        width: 100px;
        height: 100px;
    }

    .flbox1 {
        background-color: rgba(33, 114, 214, 0.8);
    }

    .flbox2 {
        background-color: rgba(255, 82, 0, 0.8);
    }

    .flbox3 {
        background-color: rgba(90, 243, 151, 0.8);
    }
</style>
<div class="container">
    <div class="flb flbox1">box1</div>
    <div class="flb flbox2">box2</div>
    <div class="flb flbox3">box3</div>
</div>


</html>
```


![image.png | left | 540x119](https://cdn.nlark.com/yuque/0/2018/png/111166/1532948722881-b3881ee6-54de-472e-91f7-9283ed3ddc93.png "")

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(247, 247, 247)">给他们都加上margin-left:-25px;</span></span>
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<style>
    .flb {
        float: left;
        width: 100px;
        height: 100px;
        margin-left: -25px;
    }

    .flbox1 {
        background-color: rgba(33, 114, 214, 0.8);
    }

    .flbox2 {
        background-color: rgba(255, 82, 0, 0.8);
    }

    .flbox3 {
        background-color: rgba(90, 243, 151, 0.8);
    }
</style>
<div class="container">
    <div class="flb flbox1">box1</div>
    <div class="flb flbox2">box2</div>
    <div class="flb flbox3">box3</div>
</div>


</html>
```


![image.png | left | 558x129](https://cdn.nlark.com/yuque/0/2018/png/111166/1532948772039-642a04af-64b9-4be6-936a-d300782725af.png "")

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">可以看出3个盒子都向左移动25px；</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">box1自身向左移动了25px，box2又覆盖了其25px，所以我们就看到了“宽度”为50px的box1</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">box2，box3以此类推！</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(247, 247, 247)">让我再看看margin-left: -50px;的情况</span></span>


![image.png | left | 535x108](https://cdn.nlark.com/yuque/0/2018/png/111166/1532948811656-8688308f-e0ef-4864-ae41-c4a0e0a1e741.png "")

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(247, 247, 247)">如果只给box3设置margin-left:-200px;</span></span>
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<style>
    .flb {
        float: left;
        width: 100px;
        height: 100px;

    }

    .flbox1 {
        background-color: rgba(33, 114, 214, 0.8);
    }

    .flbox2 {
        background-color: rgba(255, 82, 0, 0.8);
    }

    .flbox3 {
        background-color: rgba(90, 243, 151, 0.8);
        margin-left: -200px;
    }
</style>
<div class="container">
    <div class="flb flbox1">box1</div>
    <div class="flb flbox2">box2</div>
    <div class="flb flbox3">box3</div>
</div>


</html>
```


![image.png | left | 515x111](https://cdn.nlark.com/yuque/0/2018/png/111166/1532948855852-f446964a-0ccf-452a-bee6-5fde4977c106.png "")

### <a name="ps36gs"></a>总结：
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">负margin会改变浮动元素的显示位置，即使我的元素写在DOM的后面，我也能让它显示在最前面。圣杯布局、双飞翼布局啊什么的，都是利用这个原理实现的。（下文有详细）</span></span>
## <a name="nfd4pg"></a>对绝对定位影响
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<style>
    .absolute {
        position: absolute;
        top: 50%;
        left: 50%;
        height: 200px;
        width: 200px;
        background-color: #ccc;
        margin-top: -100px;
        margin-left: -100px;
    }
</style>
<div class="absolute"></div>


</html>
```
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">对于绝对定位元素，负margin会基于其绝对定位坐标再偏移，</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">唯有的缺点就是你必须知道这个觉得定位元素宽度的和高度才能并设置负margin值使其居中浏览器窗口，</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">若对于不确定宽度和高度可以用</span></span>
```css
transform: translate3d(-50%,-50%,0); 
```
# <a name="vu31cx"></a>二、margin为负值的常见布局应用
## <a name="4xi4pq"></a>左右固定，中间自适应（双飞翼）
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">双飞翼的好处：</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">1.可以让主要内容出现在dom结构的前面，现将主要内容渲染</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">2.中间只适应，两边固定宽度的效果</span></span>


![image.png | left | 617x575](https://cdn.nlark.com/yuque/0/2018/png/111166/1532949005898-5e8a742a-e19e-4a12-9eba-e860d65a92c0.png "")


```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0
    }

    .main {
        float: left;
        width: 100%;

    }

    .main .main-content {
        margin: 0 210px;
        background-color: rgba(33, 114, 214, 0.8);
        height: 500px
    }

    .left {
        width: 200px;
        float: left;
        background-color: rgba(255, 82, 0, 0.8);
        margin-left: -100%;
        height: 200px
    }

    .right {
        width: 200px;
        height: 200px;
        margin-left: -200px;
        float: left;
        background-color: rgba(90, 243, 151, 0.8);
    }
</style>
<div class="main">
    <div class="main-content">main content</div>
</div>
<div class="left">left</div>
<div class="right">right</div>



</html>
```
## <a name="vlfnwz"></a>去除列表右边框
利用负margin增加宽度的特点，举个在实际中应用例子
对于图片列表，我会常常设计成两边对齐，中间元素平均分布，类似下面的布局


![image.png | left | 700x503](https://cdn.nlark.com/yuque/0/2018/png/111166/1532949087540-4f6c4659-a08d-4e9d-94dd-c61de0c47c45.png "")

想让每一排最后一个对齐父元素的右边框，一般都两种处理，第一种会在给个循环体内的最后一个添加一个float:right属性或者做特殊处理，但这样还需要后端配合，我们自己能解决的就尽量自己解决。还有就是用css3的flexbox布局能解决这个两边对齐，但是这种布局兼容性不好，你的用户用IE的话，不推荐！
so，负margin就能发挥其增加元素宽度的特点，完美的解决这个问题！


```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<style>
    .container {
        margin: 0 auto;
        width: 500px;
        border: 1px #ccc solid;
        margin-bottom: 20px;
    }

    .list {
        overflow: hidden;
        margin-right: -10px;

    }

    .list li {
        width: 92px;
        height: 92px;
        background-color: #ccc;
        margin-bottom: 20px;
        float: left;
        margin-right: 10px;
    }
</style>
<div class="container">
    <ul class="list">
        <li>我是一个列表</li>
        <li>我是一个列表</li>
        <li>我是一个列表</li>
        <li>我是一个列表</li>
        <li>我是一个列表</li>
        <li>我是一个列表</li>
        <li>我是一个列表</li>
        <li>我是一个列表</li>
        <li>我是一个列表</li>
        <li>我是一个列表</li>
    </ul>
</div>

</html>
```


![image.png | left | 515x219](https://cdn.nlark.com/yuque/0/2018/png/111166/1532949169411-d17ecb6b-17a5-4321-b5d1-abb461f3aed6.png "")

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(247, 247, 247)">计算公式：</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(247, 247, 247)">假设一横列展示的数量为x，元素见的间距为y，父距宽度z</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(247, 247, 247)">则元素的宽度＝（z－y（x－1））/x</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(247, 247, 247)">本例中li的宽度为（500－10（5-1））/5=92</span></span>
## <a name="ef03be"></a>负边距+定位：水平垂直居中
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">上面已经举例，用了负margin会向对应方向偏移的特点！</span></span>
## <a name="g4nrai"></a>去除列表最后一个li元素的border-bottom
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">很多情况下，我们会用li标签来模拟表格，再给li标签添加下边距的时候，最后一个li标签表格会和父元素的边框靠在一起，会显得整个“table”的底部边框会比其他的边粗一些！</span></span>
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<style>
    ul.table {
        border: 1px #ccc solid;
        margin-top: 100px;
    }

    ul.table li {
        border-bottom: 1px #ccc solid;
        list-style: none;
    }
</style>

<body>
    <ul class="table">
        <li>I am li</li>
        <li>I am li</li>
        <li>I am li</li>
        <li>I am li</li>
        <li>I am li</li>
    </ul>
</body>

</html>
```


![image.png | left | 515x170](https://cdn.nlark.com/yuque/0/2018/png/111166/1532949302435-6f7e505d-d543-415c-8b79-0c229101f77f.png "")

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">下面添加一个margin-bottom:-1px;的属性,就可以使其看起来更完美</span></span>
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<style>
    ul.table {
        border: 1px #ccc solid;
        margin-top: 100px;
    }

    ul.table li {
        border-bottom: 1px #ccc solid;
        list-style: none;
        margin-bottom: -1px;
    }
</style>

<body>
    <ul class="table">
        <li>I am li</li>
        <li>I am li</li>
        <li>I am li</li>
        <li>I am li</li>
        <li>I am li</li>
    </ul>

</body>

</html>
```


![image.png | left | 514x143](https://cdn.nlark.com/yuque/0/2018/png/111166/1532949353741-bdd7bff7-39fa-46d6-804c-e2db06d47c1d.png "")

## <a name="1xsbum"></a>多列等高
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">利用margin-bottom为负值会减少css读取元素高度的特性，加上padding-bottom和overflow:hidden,就能做一个未知高度的多列等高布局（当然也可以用table）</span></span>
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<style>
    .container {
        margin: 0 auto;
        width: 100%;
        overflow: hidden;
    }

    .left {
        height: 50px;
        width: 33.33%;
        margin-bottom: -5000px;
        padding-bottom: 5000px;
        float: left;
        background-color: rgba(33, 114, 214, 0.8);
    }

    .main {
        height: 100px;
        margin-bottom: -5000px;
        width: 33.33%;
        float: left;
        padding-bottom: 5000px;
        background-color: rgba(255, 82, 0, 0.8);
    }

    .right {
        width: 33.33%;
        float: left;
        margin-bottom: -5000px;
        padding-bottom: 5000px;
        background-color: rgba(90, 243, 151, 0.8)
</style>

<body>
    <div class="container">
        <div class="left"> height:50px</div>
        <div class="main">height:100px</div>
        <div class="right">height:30px</div>
    </div>
</body>

</html>
```


![image.png | left | 598x139](https://cdn.nlark.com/yuque/0/2018/png/111166/1532949419579-23fc27c3-f4e8-4cc5-bbf9-a55e7f871801.png "")

虽然设置了5000的内边距，但是我用－5000的外边距去抵消掉，所以对于父元素来说（上文所说的css能读取的高度），他还是原来的高度（但其自身实际高度为5000p x+本来高度），然后父元素在加上overflow:hidden;以最高的高度进行裁切，所以就有了看起来“等高”的3个div。

今天整理和实验了下负margin的原理和应用，希望你看了文章有所收获，欢迎交流！

参考资料：[https://www.jianshu.com/p/549aaa5fabaa](https://www.jianshu.com/p/549aaa5fabaa)
