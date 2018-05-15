# this的指向

<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(255, 255, 255)">首先必须要说的是,</span></span><strong><span data-type="color" style="color:#FA541C">this的指向在函数定义的时候是确定不了的，只有函数执行的时候才能确定this到底指向谁,实际上this的最终指向的是那个调用它的对象</span></strong><strong>（</strong><span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(255, 255, 255)">虽然在很多情况下那样去理解不会出什么问题，但是实际上这样理解是不准确的),那么接下来我会深入的探讨这个问题.</span></span>
#### <a name="t66xqk"></a>一般场景
1.
```javascript
function a(){
    var user = "grasilife";
    console.log(this.user); //undefined
    console.log(this); //Window
}
a();
```
```javascript
function a(){
    var user = "grasilife";
    console.log(this.user); //undefined
    console.log(this);　　//Window
}
window.a();
```
<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(255, 255, 255)">this最终指向的是调用它的对象，这里的函数a实际是被Window对象所点出来.</span></span>
2.
```javascript
var o = {
    user:"grasilife",
    fn:function(){
        console.log(this.user);  //grasilife
    }
}
o.fn();
```
<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(255, 255, 255)">this指向的是对象o，因为你调用这个fn是通过o.fn()执行的</span></span>
#### <a name="u9m9lf"></a>非一般场景
1.
```javascript
var o = {
    user:"grasilife",
    fn:function(){
        console.log(this.user); //grasilife
    }
}
window.o.fn();
```
<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(255, 255, 255)">这段代码和上面的那段代码几乎是一样的,但是这里的this为什么不是指向window,如果按照上面的理论,最终this指向的是调用它的对象.</span></span>
2.
```javascript
var o = {
    a:10,
    b:{
        a:12,
        fn:function(){
            console.log(this.a); //12
        }
    }
}
o.b.fn();
```
<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(255, 255, 255)">这里同样也是对象o点出来的,但是同样this并没有执行它,那你肯定会说我一开始说的那些不就都是错误的吗?其实也不是,只是一开始说的不准确,接下来我将补充一句话,我相信你就可以彻底的理解this的指向的问题.</span></span>

结论:
* 如果一个函数中有this,但是它没有被上一级的对象所调用,那么this指向的就是window,这里需要说明的是在js的严格版中this指向的不是window,但是我们这里不探讨严格版的问题,你想了解可以自行上网查找
* 如果一个函数中有this,这个函数有被上一级的对象所调用,那么this指向的就是上一级的对象。
* 如果一个函数中有this,__这个函数中包含多个对象，尽管这个函数是被最外层的对象所调用,this指向的也只是它上一级的对象,__例子3可以证明，如果不相信，那么接下来我们继续看几个例子.


---

3.
```javascript
var o = {
    a:10,
    b:{
        // a:12,
        fn:function(){
            console.log(this.a); //undefined
        }
    }
}
o.b.fn();
```
<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(255, 255, 255)">尽管对象b中没有属性a，这个this指向的也是对象b，因为this只会指向它的上一级对象，不管这个对象中有没有this要的东西。</span></span>
4.比较特殊的情况
```javascript
var o = {
    a:10,
    b:{
        a:12,
        fn:function(){
            console.log(this.a); //undefined
            console.log(this); //window
        }
    }
}
var j = o.b.fn;
j();
```
这里this指向的是window，是不是有些蒙了？其实是因为你没有理解一句话，这句话同样至关重要。
this永远指向的是最后调用它的对象，也就是看它执行的时候是谁调用的，例子4中虽然函数fn是被对象b所引用，但是在将fn赋值给变量j的时候并没有执行所以最终指向的是window，这和例子3是不一样的，例子3是直接执行了fn。
this讲来讲去其实就是那么一回事，只不过在不同的情况下指向的会有些不同，上面的总结每个地方都有些小错误，也不能说是错误，而是在不同环境下情况就会有不同，所以我也没有办法一次解释清楚，只能你慢慢地的去体会。
5.构造函数版this
```javascript
function Fn(){
    this.user = "grasilife";
}
var a = new Fn();
console.log(a.user); //grasilife
```
这里之所以对象a可以点出函数Fn里面的user是因为new关键字可以改变this的指向，将这个this指向对象a，为什么我说a是对象，因为用了new关键字就是创建一个对象实例，理解这句话可以想想我们的例子3，我们这里用变量a创建了一个Fn的实例（相当于复制了一份Fn到对象a里面），此时仅仅只是创建，并没有执行，而调用这个函数Fn的是对象a，那么this指向的自然是对象a，那么为什么对象a中会有user，因为你已经复制了一份Fn函数到对象a中，用了new关键字就等同于复制了一份。
除了上面的这些以外，我们还可以自行改变this的指向，关于自行改变this的指向请看[JavaScript中call,apply,bind方法的总结](http://www.cnblogs.com/pssp/p/5215621.html)这篇文章，详细的说明了我们如何手动更改this的指向。
6.this碰到return时
```javascript
function fn()  
{  
    this.user = 'grasilife';  
    return {};  
}
var a = new fn;  
console.log(a.user); //undefined
```
```javascript
function fn()  
{  
    this.user = 'grasilife';  
    return function(){};
}
var a = new fn;  
console.log(a.user); //undefined
```
```javascript
function fn()  
{  
    this.user = 'grasilife';  
    return 1;
}
var a = new fn;  
console.log(a.user); //grasilife
```
```javascript
function fn()  
{  
    this.user = 'grasilife';  
    return undefined;
}
var a = new fn;  
console.log(a.user); //grasilife
```
结论:
* __如果返回值是一个对象，那么this指向的就是那个返回的对象，如果返回值不是一个对象那么this还是指向函数的实例。__


---

```javascript
function fn()  
{  
    this.user = 'grasilife';  
    return undefined;
}
var a = new fn;  
console.log(a); //fn {user: "grasilife"}
```
7.this遇上null
```javascript
function fn()  
{  
    this.user = 'grasilife';  
    return null;
}
var a = new fn;  
console.log(a.user); //grasilife
```
#### <a name="a9sisd"></a>__知识点补充：__
1. <span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(255, 255, 255)">在严格版中的默认的this不再是window，而是undefined。</span></span>
2. <span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(255, 255, 255)">new操作符会改变函数this的指向问题，虽然我们上面讲解过了，但是并没有深入的讨论这个问题，网上也很少说，所以在这里有必要说一下。</span></span>
3. <span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(255, 255, 255)">为什么this会指向a？首先new关键字会创建一个空的对象，然后会自动调用一个函数apply方法，将this指向这个空对象，这样的话函数内部的this就会被这个空的对象替代。</span></span>
4. 当你new一个空对象的时候,js内部的实现并不一定是用的apply方法来改变this指向的,这里我只是打个比方而已.
    if (this === 动态的\可改变的) return true;
```javascript
function fn(){
    this.num = 1;
}
var a = new fn();
console.log(a.num); //1
```

参考资料: [https://www.cnblogs.com/pssp/p/5216085.html](https://www.cnblogs.com/pssp/p/5216085.html)
