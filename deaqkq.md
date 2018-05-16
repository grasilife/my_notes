# 创建一个组件

## <a name="8fl1fl"></a>无状态函数式组件
```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```
__特点：__
* 组件不会被实例化，整体渲染性能得到提升
* 组件不能访问`this`对象
* 组件无法访问生命周期的方法
* 无状态组件只能访问输入的`props`，同样的`props`会得到同样的渲染结果，不会有副作用

无状态组件使得代码结构更加清晰，减少代码冗余，在开发过程中，尽量使用无状态组件
## <a name="o440bq"></a>React.createClass
__特点：__
* React.createClass会自绑定函数方法导致不必要的性能开销
* React.createClass的[mixins](https://link.jianshu.com/?t=https://hulufei.gitbooks.io/react-tutorial/mixin.html)不够自然、直观

基本已被弃用
## <a name="cincgp"></a>React.Component
`React.Component`<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">是以ES6的形式来创建</span></span>`react`<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">的组件的，是React目前极为推荐的创建有状态组件的方式，相对于 </span></span>`React.createClass`<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">可以更好实现代码复用。将上面</span></span>`React.createClass`<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">的形式改为</span></span>`React.Component`<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">形式如下：</span></span>
```javascript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

导出模块的方式
1.第一种
```javascript
class ImgGra extends React.Component {
}
export default ImgGra
```
2.第二种
```javascript
export default class ImgGra extends React.Component {
}
```
*我们在实际应用中应该选择哪种方法来创建组件呢？*
* 只要有可能，尽量使用无状态组件创建形式
* 否则（如需要state、生命周期方法等），使用`React.Component`这种es6形式创建组件

