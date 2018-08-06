# 表单


```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script src="https://cdn.bootcss.com/angular.js/1.4.6/angular.min.js"></script>
</head>
<body>

<div ng-app="myApp" ng-controller="myCtrl">

<p>选择网站:</p>
<input type="checkbox" ng-model="myVar1" name="name" ng-change=checkBoxfn()>苹果
<input type="checkbox" ng-model="myVar2" name="name" ng-change=checkBoxfn()>梨
<input type="radio" ng-model="myVar" value="dogs1">Dogs
<input type="radio" ng-model="myVar" value="dogs">Dogs
<select ng-model="selectedSite" ng-options="x.url for x in sites" ng-change=fn()>
	<option disabled value="">请选择数据源类型</option>
</select>

<h1>你选择的是: {{selectedSite.site}}</h1>
<p>网址为: {{selectedSite.url}}</p>

</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
   $scope.sites = [
	    {site : "Google", url : "http://www.google.com"},
	    {site : "Runoob", url : "http://www.runoob.com"},
	    {site : "Taobao", url : "http://www.taobao.com"}
	];
	$scope.fn=function(){
		console.log(this)
	}
});
</script>

<p>该实例演示了使用 ng-options  指令来创建下拉列表，选中的值是一个对象。</p>
</body>
</html>

```

