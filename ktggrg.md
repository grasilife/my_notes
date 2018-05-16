# 区分event对象中的[clientX,offsetX,screenX,pageX]

### <a name="r2xkbt"></a>clientX clientY
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">client直译就是客户端，客户端的窗口就是指游览器的显示页面内容的窗口大小（不包含工具栏、导航栏等等).</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">event.clientX、event.clientY就是用来获取鼠标距游览器显示窗口的长度.</span></span>


![image.png | left | 700x373](https://cdn.yuque.com/yuque/0/2018/png/111166/1526451307416-a9b5540e-bd37-4fb3-ad7a-3215f3629802.png "")

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">兼容性：IE和主流游览器都支持。</span></span>
### <a name="lpudar"></a>offsetX offsetY
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">offset意为偏移量，是被点击的元素距左上角为参考原点的长度，而IE、FF和Chrome的参考点有所差异。</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">Chrome下，offsetX offsetY是包含边框的，如图所示。</span></span>


![image.png | left | 626x471](https://cdn.yuque.com/yuque/0/2018/png/111166/1526451352056-ed079652-c652-40eb-8c77-79c57d81dc51.png "")

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">而IE、FF是不包含边框的，如果鼠标进入到border区域，为返回负值，如图所示。</span></span>


![image.png | left | 468x417](https://cdn.yuque.com/yuque/0/2018/png/111166/1526451366816-ac33cd1d-6932-4229-88e1-6ddf4e90a847.png "")

<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">兼容性：IE9+,chrome,FF都支持此属性。</span></span>
### <a name="nfctze"></a>screenX screenY
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">screen顾名思义是屏幕，是用来获取鼠标点击位置到屏幕显示器的距离，距离的最大值需根据屏幕分辨率的尺寸来计算。</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">event.screenX</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">event.sreenY</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">兼容性：所有游览器都支持此属性。</span></span>
### <a name="vgn0tx"></a>pageX pageY
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">page为页面的意思，页面的高度一般情况</span></span>__client游览器__<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">显示区域装不下，所以会出现垂直滚动条。</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">鼠标距离页面初始page原点的长度。</span></span>


![image.png | left | 652x737](https://cdn.yuque.com/yuque/0/2018/png/111166/1526451454083-ec3cf042-1e78-4f7d-a7e1-d8bbf7349042.png "")


<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">在IE中没有pageX、pageY取而代之的是event.x、evnet.y。x和y在webkit内核下也实现了，所以火狐不支持x，y。</span></span>
<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">兼容性：IE不支持，其他高级游览器支持。</span></span>

参考资料:[https://www.jianshu.com/p/a52077e8369d](https://www.jianshu.com/p/a52077e8369d)
