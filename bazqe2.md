# 倒三角错误提示框


```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <title></title>
    <style type="text/css">
.tooltips {
  position: relative;
  height: 28px;
  line-height: 28px;
  background: #fff;
  border: 1px solid red;;
  border-radius: 4px;
  padding: 0px 15px;
  display: inline-block;
  margin: 0px 0px 10px 0px;
}

.arrow {
  position: absolute;
  width: 0px;
  height: 0px;
  line-height: 0px;
  border-width: 0px 10px 15px 10px;
  border-style: dashed dashed solid dashed;
  border-left-color: transparent;
  border-right-color: transparent;
}

.arrow-border {
  color: red;
  bottom: 27px;
  left: 8%;
}

.arrow-bg {
  color: #fff;
  bottom: 25px;
  left: 8%;
}
//用于tips悬浮
.error-index{
  position: absolute;
  z-index: 1000;
}
    </style>
</head>

<body>
    <!--先定义一个相对定位的盒子div：-->
    <div class="tooltips">
        <!--给div盒子添加一个三角型图标-->
        <!--给“小三角穿上松紧带”需要使用两个三角形叠加的方式-->
        <!--首先我们定义两个三角形的div，一个背景色和盒子的边框颜色相同，一个背景色和盒子的背景色一致：-->
        <div class="arrow arrow-border"></div>
        <div class="arrow arrow-bg"></div>
        <!--注意：.arrow-bg和.arrow-border的bottom位置相差为1px（可根据边框宽度调整）两个div的顺序不可颠倒。-->
    </div>
</body>

</html>
```


![image.png | left | 461x288](https://cdn.yuque.com/yuque/0/2018/png/111166/1530864462633-0ac56a93-7cee-4527-aacc-3ca7fec56366.png "")
上图示
