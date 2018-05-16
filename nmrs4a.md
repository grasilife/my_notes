# React.Component三种手动绑定this的方法

## <a name="ie2ffe"></a>在构造函数中绑定
```javascript
 constructor(props) {
       super(props);
       this.Enter = this.Enter.bind(this);
  }
```
## <a name="pw5xwe"></a>使用bind绑定
```javascript

```
## <a name="bhetqn"></a>使用arrow function绑定
```javascript
<div onKeyUp={(event)=>this.Enter(event)}></div> 
```

