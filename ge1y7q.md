# 属性扩散

有时候你需要给组件设置多个属性，你不想一个个写下这些属性，或者有时候你甚至不知道这些属性的名称，这时候 *spread attributes* 的功能就很有用了。

比如：
```javascript
var props = {};
props.foo = x;
props.bar = y;
var component = <Component {...props} />;
```
`props` 对象的属性会被设置成 `Component` 的属性。

属性也可以被覆盖：
```javascript
var props = { foo: 'default' };
var component = <Component {...props} foo={'override'} />;
console.log(component.props.foo); // 'override'
```
<span data-type="color" style="color:rgb(51, 51, 51)"><span data-type="background" style="background-color:rgb(255, 255, 255)">写在后面的属性值会覆盖前面的属性。</span></span>
