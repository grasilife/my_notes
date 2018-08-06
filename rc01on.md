# JS中for循环里面的闭包问(for循环中的函数)

<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(245, 245, 245)">我们先看一个正常的for循环，普通函数里面有一个for循环，for循环结束后最终返回结果数组</span></span>
```javascript
function box(){
    var arr = [];
    for(var i=0;i<5;i++){
        arr[i] = i;        
    }
    return arr;
}
alert(box())                                    //正常情况不需要闭包，就可以达到预期效果，输出结果为一个数组0,1,2,3,4
```
<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(245, 245, 245)">有时我们需要在for循环里面添加一个匿名函数来实现更多功能，看下面代码</span></span>
```javascript
//循环里面包含闭包函数
function box(){
    var arr = [];
    for(var i=0;i<5;i++){
        arr[i] = function(){
            return i;                            //由于这个闭包的关系，他是循环完毕之后才返回，最终结果是4++是5
        }                                        //这个匿名函数里面根本没有i这个变量，所以匿名函数会从父级函数中去找i，
    }                                            //当找到这个i的时候，for循环已经循环完毕了，所以最终会返回5
    return arr;
}
//alert(box());                                    //执行5次匿名函数本身
//alert(box()[1]);　　　　　　　　　　　　　　　　　　　//执行第2个匿名函数本身
//alert(box().length);                            //最终返回的是一个数组，数组的长度为5
alert(box()[0]());                                //数组中的第一个数返回的是5，这是为什么？
```
上面这段代码就形成了一个闭包：
__<span data-type="color" style="color:rgb(128, 0, 128)">闭包是指有权访问另一个函数作用域中的变量的函数，创建闭包的常见的方式，就是在一个函数内部创建另一个函数，通过另一个函数访问这个函数的局部变量。</span>__
<span data-type="color" style="color:rgb(0, 0, 0)">在for循环里面的匿名函数执行 return i 语句的时候，由于匿名函数里面没有i这个变量，所以这个i他要从父级函数中寻找i，而父级函数中的i在for循环中，当找到这个i的时候，是for循环完毕的i，也就是5，所以这个box得到的是一个数组[5,5,5,5,5]。</span>
## <a name="spuggz"></a>解决方案1
<span data-type="color" style="color:rgb(0, 0, 0)">在看解决方案一之前，我们先看一下匿名函数的自我执行：</span>

<span data-type="color" style="color:rgb(128, 0, 128)"><strong>匿名函数自我执行的写法是，在函数体外面加一对圆括号，形成一个表达式，在圆括号后面再加一个圆括号，里面可传入参数。</strong></span>

<span data-type="color" style="color:rgb(0, 0, 0)">例如下代码：</span>
```javascript
(function(){
    alert('lee');                        //匿名函数自我执行(匿名函数)()
})();
```
<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(245, 245, 245)">我们再来看解决方案1：</span></span>
```javascript
function box(){
    var arr = [];
    for(var i=0;i<5;i++){
        arr[i] = (function(num){                    //自我执行，并传参(将匿名函数形成一个表达式)(传递一个参数)
            return num;                            //这里的num写什么都可以                    
        })(i);                                    //这时候这个括号里面的i和上面arr[i]的值是一样的都是取自for循环里面的i                            
    }                                            
    return arr;
}
//alert(box());                                
//alert(box()[1]);
//alert(box().length);                            
alert(box()[0]);
```
<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(245, 245, 245)">通过给匿名函数传参，而传递的这个参数i是每次执行for循环里面的i，每次传递的参数i的值都不一样，匿名函数里面的num接收传递的参数i，所以box()最终输出结果为[0,1,2,3,4]</span></span>
### <a name="yfa3co"></a>解决方案2
<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(245, 245, 245)">这种方案的原理就是在匿名函数1里面再写入一个匿名函数2，这个匿名函数2需要的num值会在他的父级函数匿名函数1里面去寻找，而匿名函数1里面的num值就是传入的这个参数i，和上面例子中的i是一样的，</span></span>
```javascript
function box(){
    var arr = [];
    for(var i=0;i<5;i++){
        arr[i] = (function(num){
        //num在这里                                    //原理和上面一种方法一样的，所以可以实现闭包                    
            return function(){                        //在这个闭包里面再写一个匿名函数
                return num;                            
            };                                                                
        })(i)                                                
    }
    return arr;
}
//alert(box());                                
//alert(box()[1]);
//alert(box().length);
var b = box();                            
alert(b[0]());
alert(box()[0]());
```
<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(245, 245, 245)">box()最终返回结果[0,1,2,3,4],</span></span>
## <a name="sdwuul"></a>解决方案3
<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(245, 245, 245)">如果将一个匿名函数自我执行的时候赋值给一个变量，那么这个匿名函数中的圆括号的可以去掉的，看下面代码，</span></span>
```javascript
var tip = function(){                                //这样把匿名函数自我执行的时候赋值给一个变量，那么圆括号是可以去掉的
    alert('lee');
}();
```
<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgb(245, 245, 245)">利用匿名函数的这一特点，我们可以将解决方案1中的代码改进一下：</span></span>
```javascript
function box(){
    var arr = [];
    for(var i=0;i<5;i++){
        arr[i] = function(num){                
            return num;                            
        }(i);                                
    }                                            
    return arr;
}
//alert(box());                                
//alert(box()[1]);
//alert(box().length);                            
alert(box()[4]);
```


参考资料：[https://www.cnblogs.com/ZinCode/p/5551907.html](https://www.cnblogs.com/ZinCode/p/5551907.html)
