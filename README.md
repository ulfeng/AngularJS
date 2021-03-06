## AngularJS 简介
##### AngularJS 扩展了HTML
```html
<div ng-app=""> // ng-app 指令定义了一个AngularJS应用程序
    <p>姓名：<input type="text" ng-model="name"></p> // ng-model 把元素值(如输入域的值)绑定到应用程序
    <p ng-bind="name"></p> // ng-bind 把应用程序数据绑定到HTML视图
</div>

<script src="http://apps.bdimg.com/libs/angular.js/1.3.9/angular.min.js"></script>
```
##### AngularJS表达式
```html
<p>我的第一个表达式：{{ 5 + 5 }}</p>
// AngularJS表达式写在双大括号内，可以包含文字、运算符和变量
// 数字、对象、数组、字符串
```

##### AngularJS应用
```html
<div ng-app="myApp" ng-controller="myCtrl">
名：<input type="text" ng-model="firstName"><br>
姓：<input type="text" ng-model="lastName"><br>
姓名：{{firstName + " " + lastName}}
</div>
<script>
var app = angular..moudle('myApp', []);
app.controller('myCtrl',function($scope){
    $scope.firstName = "John";
    $scopr.lastName = "Doe";
})
</script>

// ng-app 定义了应用，ng-controller 定义了控制器

```

##### AngularJs指令
```html
// ng-app 初始化一个AngularJS应用程序
// ng-init 初始化应用程序数据
// ng-model 把元素值(如输入域的值)绑定到应用程序
// ng-bind 绑定数据
// {{}}数据绑定
// ng-reapeat 重复HTML元素
<div ng-app="" ng-init="names=['Jani','Hege','Kai']">
    <p>使用 ng -repeat 来循环数组</p>
    <ul>
        <li ng-repeat="x in names">
        {{ x }}
    </ul>
</div>
```

##### AngularJS控制器
```javascript
var app = angular.moudle('myApp',[]);
app.controller('personCtrl',function($scope){
    $scope.firstName = "John";
    $scope.lastName = "Doe";
    $scope.fullName = function(){
        return $scope.firstName + " " +$scope.lastName; 
    }
})
// 可在外部引用
```

##### AngularJS 过滤器
```javascript
    // curreny 格式化数字为货币格式
    // filter 从数组项中选择一个子集
    // lowercase 格式化字符串为小写
    // orderBy 根据某个表达式排列数组
    // uppercase 格式化字符串为大写
```
currency 过滤器
```html
    <div ng-app="myApp" ng-controller="costCtrl">
        <input type="number" ng-model="quantity" />
        <input type="number" ng-model="price" />
        <p>总价 = {{ (quantity*price) | currency }}</p>
    </div>

    <script>
        var app = angular.module('myApp', []);
        app.controller('costCtrl', function ($scope) {
            $scope.quantity = 1;
            $scope.price = 9.99;
        });
    </script>
```
向指令添加过滤器
```html
    <div ng-app="myApp" ng-controller="namesCtrl">
        <p>循环对象</p>
        <ul>
            <li ng-repeat="x in names | orderBy:'city'">
                {{ x.name +", " + x.city }}
            </li>
        </ul>
    </div>
    <script>
        var app = angular.module('myApp', []);
        app.controller('namesCtrl', function ($scope) {
            $scope.names = [
            {
                name: "zhangsan",
                city: "ShangHai"
            },
            {
                name: "LiSi",
                city: "BeiJing"
            }
            ]
        });
    </script>
```
过滤输入
```html
<div ng-app="myApp" ng-controller="fliterCtrl">
        <input type="text" ng-model="test" />
        <ul>
            <li ng-repeat="x in names | filter:test | orderBy:'city'">
                {{ (x.name | uppercase) +", "+x.city }}
            </li>
        </ul>
    </div>
    <script>
        var app = angular.module('myApp', []);
        app.controller('fliterCtrl', function ($scope) {
            $scope.names = [{
                name: "Wang",
                city: "Chongqing"
            },
            {
                name: "Hong",
                city: "BeiJing"
            },
            {
                name: "Sun",
                city:"Guangzhou"
            }
            ]
        })
    </script>
```

##### AngularJS http(xmlHttpRequest Ajax)
```javascript
    <div ng-app="myApp" ng-controller="customersCtrl">
        <ul>
            <li ng-repeat="x in names">
                {{ x.Name+", "+x.City+", "+x.Country }}
            </li>
        </ul>
    </div>
    <script>
        var app = angular.module('myApp', []);
        app.controller('customersCtrl', function ($scope, $http) {
            $http.get("test.json").success(function (response) {
                $scope.names = response.records;
            });
        });
    </script>
```

##### AngularJS 表格
```html
<style>
table, th , td  {
  border: 1px solid grey;
  border-collapse: collapse;
  padding: 5px;
}
table tr:nth-child(odd)	{
  background-color: #f1f1f1;
}
table tr:nth-child(even) {
  background-color: #ffffff;
}
</style>

    <div ng-app="myApp" ng-controller="customersCtrl">
        <table>
            <tr ng-repeat="x in names | orderBy:'Country'">
                <td>{{ $index+1 }}</td> // 加序号
                <td>{{ x.Name }}</td>
                <td>{{ x.Country }}</td>
            </tr>
        </table>
    </div>

    <script>
        var app = angular.module('myApp', []);
        app.controller('customersCtrl', function ($scope, $http) {
            $http.get("test.json").success(function (response) {
                $scope.names = response.records;
            })
        });
    </script>
```

##### AngularJS SQL
```html
<div ng-app="myApp" ng-controller="sqlCtrl">
        <table>
            <tr ng-repeat="x in names">
                <td>{{ x.Name }}</td>
                <td>{{ x.City }}</td>
            </tr>
        </table>
    </div>
    <script>
        var app = angular.module('myApp', []);
        app.controller('sqlCtrl', function ($scope, $http) {
            $http.get("test.php").success(function (response) {
                $scope.names = response.records;
            });
        })
    </script>
```

#### AngularJS HTML DOM

ng-disabled 指令
```html
<div ng-app="" ng-init = "mySwitch=true">
    <p>
        <button ng-disabled = "mySwitch">点击！</button>
    </p>
    <p>
        <input type = "checkbox" ng-model="mySwitch" />按钮
    </p>
</div>
```

ng-show 指令
```html
<div ng-app = "">
    <p ng-show = "true">我是可见的</p>
    <p ng-show = "false">我是不可见的</p>
</div>
```

ng-show 根据value值来隐藏或显示一个HTML元素
```html
<div ng-app = "13">
    <p ng-show = "hour > 12">我是可见的。<p>
</div>
```

ng-hide 指令
```html
<div ng-app = "">
    <p ng-hide = "true">我是不可见的。</p>
    <p ng-hide = "false">我是可见的。</p>
</div>
```

#### AngularJS 事件

ng-click 指令
```html
<div ng-app="myApp" ng-controller="myCtrl">
    <button ng-click="count = count +１"＞点我！</button>
    <p{{ count }}</p>
</div>
<script>
var app = angular.module('myApp',[]);
app.controller('myCtrl',function($scope){
    $scope.count = 0;
});
</script>
```

隐藏指令
```html
<div ng-app = "myApp" ng-controller = "personCtrl">
    <button ng-click = "toggle()">显示/隐藏</button>
    <p ng-hide = "myWar">
        名： <input type = "text" ng-model = "firstName"><br>
        姓： <input type = "text" ng-model = "lastName"><br>
        姓名： {{ firstName + " " + lastName }}
    </p>
</div>
<script>
var app = angular.module("myApp",[]);
app.controller("personCtrl", function($scope){
    $scope.firstName = "John";
    $scope.lastName = "Doe";
    $scope.myVar = false;
    $scope.toggle = function(){
        $scope.myVar = !$scope.myVar;
    }
})
</script>
```

显示指令
```html
<div ng-app = "myApp" ng-controller = "personCtrl">
    <button ng-click = "toggle()">显示/隐藏</button>
    <p ng-show = "myWar">
        名： <input type = "text" ng-model = "firstName"><br>
        姓： <input type = "text" ng-model = "lastName"><br>
        姓名： {{ firstName + " " + lastName }}
    </p>
</div>
<script>
var app = angular.module("myApp",[]);
app.controller("personCtrl", function($scope){
    $scope.firstName = "John";
    $scope.lastName = "Doe";
    $scope.myVar = true;
    $scope.toggle = function(){
        $scope.myVar = !$scope.myVar;
    }
});
</script>
```

#### AngularJS模块
模块定义了一个应用程序<br>
模块是应用程序中不同部分的容器<br>

带有控制器的模块
```html
<div ng-app = "myApp" ng-controller = "myCtrl">
{{ firstName + "" +lastName }}
</div>
<script>
var app = angular.module("myApp", []);
app.controller("myCtrl", function($scope){
    $scope.firstName = "John";
    $scope.lastName = "Doe";
});
</script>
```
模块和控制器也可以包含在JS文件中<br>
AngularJs库是在文档的<head>区域被加载
































































