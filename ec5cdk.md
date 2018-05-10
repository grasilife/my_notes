# 比较

### Object.is()
<span data-type="color" style="color: rgb(51, 51, 51);"><span data-type="background" style="background-color: rgb(255, 255, 255);">首先先看 ==，由于JS是弱类型的，如果使用 == 进行比较，== 操作符会自动将 0，‘ ’（空字符串），null，undefined 转成布尔型false，这样就会出现</span></span>
```javascript
0 == ' '  // true
null == undefined // true
[1] == true // true
```
<span data-type="color" style="color: rgb(51, 51, 51);"><span data-type="background" style="background-color: rgb(255, 255, 255);">这显然是不符合预期的。所以JS为我们提供了全等操作符 ===，它不会进行类型转换，也就是说如果两个值一样，必须符合类型也一样。但是，它还是有两种疏漏的情况</span></span>
```javascript
+0 === -0 // true，但我们期待它返回false
NaN === NaN // false，我们期待它返回true
```
<span data-type="color" style="color: rgb(51, 51, 51);"><span data-type="background" style="background-color: rgb(255, 255, 255);">所以，Object.is修复了=== 这两种判断不符合预期的情况</span></span>
```javascript
function(x, y) {
    // SameValue algorithm
    if (x === y) {
     // 处理为+0 != -0的情况
      return x !== 0 || 1 / x === 1 / y;
    } else {
    // 处理 NaN === NaN的情况
      return x !== x && y !== y;
    }
};
```
这样就使得Object.is()总是返回我们需要的结果。 它在下面6种情况下，会返回true
* 两个值都是 undefined
* 两个值都是 null
* 两个值都是 true 或者都是 false
* 两个值是由相同个数的字符按照相同的顺序组成的字符串
* 两个值指向同一个对象
* 两个值都是数字并且
    * 都是正零 +0
    * 都是负零 -0
    * 都是 NaN
    * 都是除零和 NaN 外的其它同一个数字
    * 可以看出Object.is可以对基本数据类型:null,undefined,number,string,boolean做出非常精确的比较，但是对于引用数据类型是没办法直接比较的。
__* *__
参考资料:
[http://www.imweb.io/topic/598973c2c72aa8db35d2e291](http://www.imweb.io/topic/598973c2c72aa8db35d2e291)
[http://www.jstips.co/zh\_cn/javascript/why-you-should-use-Object.is()-in-equality-comparison/](http://www.jstips.co/zh_cn/javascript/why-you-should-use-Object.is()-in-equality-comparison/)
