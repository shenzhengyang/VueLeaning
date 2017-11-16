## Angular 表达式
* ng-app="" 应用程序所有者
* ng-init="常量、数组、字符串"
* ng-bind="绑定元素，可以为字符串，常量，json，数组"
## Angular 指令
* ng-model 指令把元素值（比如输入域的值）绑定到应用程序
* ng-repeat="x in names" 循环遍历数据"
* app.directive 创建自定义指令
* ng-show="myForm.myAddress.$error.email" 返回值为true的情况下显示
* myForm.myAddress.$valid 输入值合法为true
* myForm.myAddress.$dirty 只改变为true
* myForm.myAddress.$touched 通过触屏点击为true
## Angular Scope(作用域)
* $scope 对象当作一个参数传递:
app.controller('myCtrl', function($scope) {
    $scope.carname = "Volvo";
});
* scope 是一个 JavaScript 对象，带有属性和方法
app.controller('myCtrl', function($scope) {
    $scope.name = "Runoob";
    $scope.sayHello = function() {
        $scope.greeting = 'Hello ' + $scope.name + '!';
    };
});
* 根作用域 所有的应用都有一个 $rootScope，$rootScope 可作用于整个应用中
## Angular 控制器
angular.module('myApp',[]).controller('personCtrl',function($scope){
	$scope.names="";
});
可以引入外部文件
## Angular 过滤器
* {{lastName|uppercase}}通过管道字符（|）去过滤
* ng-repeat="x in names | orderBy: 'country'"
* 输入过滤
ng-repeat="x in names | filter:test | orderBy:'country'"
* 自定义过滤器
angular.module('myApp',[]).filter('reverse',function(){
	return function(text){
		return text.split(",").reverse().join("");	
	}
});
## Angular Service 服务
* $location.absUrl(); 服务 返回当前页面的URL
* $http 服务
angular.module('myApp',[]).controller('myCtrl',function($scope,$http){
	$http.get("welconme.htm").then(function(response){
		$scope.myWelcome=response.data;
	});
});
* $timeout 服务(定时器)
angular.modular('myApp',[]).controller('myCtrl',function($scope.$timeout){
	$scope.myHeader="Hello World";
	$timeout(function(){
		$scope.mHeader="How are you today?";
	},2000);	
});
* $interval 服务 （计时器）
angular.module('myApp',[]).controller('myCtrl'.function($scope,$interval){
	$scope.theTime=new Date().toLocaleTimeString();
	$interval(function(){
		$scope.theTime=new Date().toLocaleTimeString();
	},1000)
})
* 创建自定义服务
angular.module('myApp',[]).service('hexafy',function(){
	this.myFunc=function(x){
		return x.toString(16);
	}
});
## Angular XMLHttpRequest
* $http
$http({
	method:'GET',
	url:'/someUrl'
}).then(function successCallback(response){
	//请求成功的逻辑
},function errorCallback(response){
	//请求失败逻辑
});
## Angular 选择框
* ng-options 
<code>
<select ng-init="selectedName=name[0]" ng-model="selectedName" ng-options="x for x in names"">
</select>
</code>
* ng-repeate(倾向于在这种方法，简单易懂)
<select>
<option ng-repeat='x in names'>{{x}}</option>
</select>
## Angular 表格
* ng-repeat
<tr ng-repeat="x in names">
    <td>{{ x.Name }}</td>
    <td>{{ x.Country }}</td>
</tr>
* $index 显示序号
* $even $odd 奇偶行数
和ng-if 使用
## Angular HTML DOM
* ng-disable 指令
ng-disable="true" 值为true 时不可使用
* ng-show 指令
ng-show="true" 值为true时可见
* ng-hide 指令
ng-hide="true" 值为true 时隐藏
## Angular 事件
* ng-click
<button ng-click="toggle()">隐藏/显示</button>
<script>
angular.module('myApp',[]).controller('myCtrl',function($scope){
	$scope.toggle=function(){
		//函数逻辑
	}
})
</script>
## Angular 输入验证
$dirty $invalid $error
$dirty		表单有填写记录
$valid		字段内容合法的
$invalid	字段内容是非法的
$pristine	表单没有填写记录
## Angular 全局API
angular.lowercase()	转换字符串为小写
angular.uppercase()	转换字符串为大写
angular.isString()	判断给定的对象是否为字符串，如果是返回 true。
angular.isNumber()	判断给定的对象是否为数字，如果是返回 true。
## Angular 包含
* ng-include="'xxx.html'"
## Angular 动画
引入angular-animate.min.js库文件
angular.module('myApp',['ngAnimate']);
## Angular 依赖注入
* value
// 定义一个模块
var mainApp = angular.module("mainApp", []);
// 创建 value 对象 "defaultInput" 并传递数据
mainApp.value("defaultInput", 5);
// 将 "defaultInput" 注入到控制器
mainApp.controller('CalcController', function($scope, CalcService, defaultInput) {
   $scope.number = defaultInput;
   $scope.result = CalcService.square($scope.number);
   $scope.square = function() {
      $scope.result = CalcService.square($scope.number);
   }
});
* factory
// 定义一个模块
var mainApp = angular.module("mainApp", []);
// 创建 factory "MathService" 用于两数的乘积 provides a method multiply to return multiplication of two numbers
mainApp.factory('MathService', function() {
   var factory = {};
   factory.multiply = function(a, b) {
      return a * b
   }
   return factory;
}); 
// 在 service 中注入 factory "MathService"
mainApp.service('CalcService', function(MathService){
   this.square = function(a) {
      return MathService.multiply(a,a);
   }
});
* provider
// 定义一个模块
var mainApp = angular.module("mainApp", []);
// 使用 provider 创建 service 定义一个方法用于计算两数乘积
mainApp.config(function($provide) {
   $provide.provider('MathService', function() {
      this.$get = function() {
         var factory = {};  
         
         factory.multiply = function(a, b) {
            return a * b; 
         }
         return factory;
      };
   });
});



