# ES5和ES6函数的写法

1. return的不同
```javascript
//es5的写法
function test(color) {
    return {
        type: "click",
        background: color
    }
}
// es6的写法
const test = (color) => {
    return ({
        type: "click",
        background: color
    })
}
```

<span data-type="color" style="color: rgb(114, 46, 209);">注意:ES6中return后面是()圆括号,ES6中规定return一个对象时加圆括号;</span>
