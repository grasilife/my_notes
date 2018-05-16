# CSS 解决img底部空白间隙

## <a name="tppinb"></a>概述
img一直以来有一个很大的问题就是底部空白间隙，一直以为是img默认样式造成的，后来查了相关的资料，才弄清楚为什么会产生这样的结果。

首先仔细看下图中的边框与img的间隙。


![image.png | left | 641x514](https://cdn.yuque.com/yuque/0/2018/png/111166/1526449770347-c66f380c-f363-4cbd-82b7-18e30dd9d8c4.png "")


<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">用过ps文字工具的同学头知道，在使用文本工具中会出现如下的现象，字母或者汉字会超出那条基线。</span></span>


![image.png | left | 700x170](https://cdn.yuque.com/yuque/0/2018/png/111166/1526448135387-3ca1af9d-9d2d-48e9-9100-028a13a3d638.png "")

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">而在CSS中也有那条线，而且inline默认的垂直对齐方式vertical-align默认值是baseline(基线对齐)，也是以</span></span>__x字母__<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">的下方为基准。（在平面设计中，字体设计也同样基于这样的一个原则，x的下方为基线）</span></span>
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <style>
        div {
            width: 600px;
            border: 1px solid black;
        }

        img {}
    </style>
    <title>Document</title>
</head>

<body>
    <div>
        <img src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1526459777004&di=0bf33155b0ad4f7d6aaf90cce3fb1b61&imgtype=0&src=http%3A%2F%2Fimg3.duitang.com%2Fuploads%2Fblog%2F201403%2F25%2F20140325182429_jATZt.jpeg">
        <span>xyp</span>
    </div>
</body>

</html>
```
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">观察上方的代码，字体的大小直接影响着超出基线间隙，所以字体大小可以影响基线间隙。</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">同时行内本身的</span></span>`line-height`<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">是会移动基线的（文字垂直居中可以通过line-height实现）。所以行高也是可以影响基线的位置。</span></span>
## <a name="4c0ehu"></a>解决方案
知道底部间隙的原因是因为行内元素默认的垂直对齐方式为baseline造成的字体下方会有间隙，所以解决起来就挺好办了。一切的原因都是inline行内属性在作怪，只要对症下药即可。

目前有4种非常简单的解决方案。
__第一种方法：__<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">修改img行内元素的垂直居中方式，让它不在以基线对齐。</span></span>
```css
img {
    vertical-align: bottom;
}
```


![image.png | left | 635x508](https://cdn.yuque.com/yuque/0/2018/png/111166/1526449830905-1c4cc6eb-812e-4756-a438-b3e006943e40.png "")

__第二种方法：__<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">修改行高，使行高变小，这样基线下方的位置基本可以忽略。</span></span>
```css
div {
    line-height: 0px;
}
```


![image.png | left | 628x500](https://cdn.yuque.com/yuque/0/2018/png/111166/1526449859776-b980fff5-f412-4a59-abaa-fcb3bee3fc52.png "")

__第三种方法：__<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">修改img行内元素的字体大小，基线的下方间隙是部分字体超过基线下方而产生的，如果把父元素的</span></span>`font-size`<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">变的超小，基线的下方距离将忽略不计。</span></span>
```css
div {
    font-size: 0px;
}
```


![image.png | left | 615x497](https://cdn.yuque.com/yuque/0/2018/png/111166/1526449920051-515ef37c-d687-4230-802e-83220a694296.png "")

xyp消失,<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">如果把字体改的非常大，那么间隙又会出现。</span></span>
```css
div {
    font-size: 80px;
}
```


![image.png | left | 641x519](https://cdn.yuque.com/yuque/0/2018/png/111166/1526449965631-05015198-c24c-47bd-932f-0f8ba5eac6e8.png "")

__第四种方法：__<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">直接让img变成块级元素，不在受行内基线的影响。</span></span>
```css
img {
    display: block;
}

```


![image.png | left | 661x536](https://cdn.yuque.com/yuque/0/2018/png/111166/1526450002178-4fbfd3a9-b359-4abc-adcb-a7c311dee173.png "")

__第五种方法：浮动__<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">。</span></span>
```css
img {
    float：left;
}
```


![image.png | left | 765x521](https://cdn.yuque.com/yuque/0/2018/png/111166/1526450110476-76c41e04-49f0-45c5-acb8-48838d5e072e.png "")

### <a name="mx5mpi"></a>结语
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">在深入研究img间隙原因之前，我一直使用的是</span></span>`display: block`<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">来控制间隙，在深入学习之后，才发现有这么多方式可以解决，懂得原理很重要。所以学习一定要知其所以然。</span></span>

参考资料:[https://www.jianshu.com/p/e7373c2bbef1](https://www.jianshu.com/p/e7373c2bbef1)


