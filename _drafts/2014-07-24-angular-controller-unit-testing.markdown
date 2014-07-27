---
layout: post
title:  "Unit Testing \"controller as\" Controllers in Angular.js"
tags: coding angular.js unit-testing
---
I've decided to pick up a front-end framework, because what else am I going to do in my free time. My framework of choice is (of course) [Angular.js][angularjs], which I've been learning with the use of both the [official tutorial][angular_tutorial] and the [Code School free course][angular_codeschool]. 

I've noticed a discrepancy between the way the two different learning tools handle controllers, specifically with regards to implicitly/explicitly passing the [scope][scope_docs] to the controller. As mentioned in the [official docs][ngController_docs], there are two way of creating controllers:

1. Injecting $scope into the Controller
---------------------------------------
This method, described in the [Angular tutorial][angular_tutorial] and [docs][ngController_docs], is the more common declaration style. 

Simply inject the scope as a dependency in the controller:
{% highlight javascript linenos%}
// app.js
var app = angular.module('controllerExample',[]);
app.controller('injectCtrl', [$scope, function($scope){
	$scope.data = [
	...
	];
});
{% endhighlight %}
And then, in order to utilize the controller in your page, do the following:
{% highlight html linenos%}
<body ng-controller="injectCtrl">
		<p ng-repeat="item in data">{% raw %}
			{{item.name}}
		{% endraw %}</p>
</body>
{% endhighlight %}
Notice that the ng-controller is defined to simply be the controller name, and that we do need need to reference the controller in order to access data. In order to test this controller using Karma, we would have to run the following test:

{% highlight javascript linenos%}
describe('injectCtrl', function(){

  beforeEach(module('controllerExample'));

  it('should create data model with 3 items', inject(function($controller) {
    var scope = {},
        ctrl = $controller('injectCtrl', {$scope:scope});

    expect(scope.data.length).toBe(3);
  }));

});

{% endhighlight %}

This method, despite being the more popular option, can lead to a number of problems due to scope issues (you can read [here][understanding_scopes] for more information about these scope issues), and thus I prefer to not use it if I can.

2. Controller-as convention
---------------------------
This method, used in te 
{% highlight javascript linenos%}
// app.js - controller-as example
var app = angular.module('controllerAsExample',[]);
app.controller('asCtrl', function(){
	this.data = [
	...
	];
});
{% endhighlight %}

{% highlight html linenos%}
<!doctype html>
<html lang="en" ng-app="phonecatApp">
<head>
	...
	<script src="js/controllers.js"></script>
</head>
<body ng-controller="PhoneListCtrl as phoneList">
		<p ng-repeat="phone in phoneList.phones">
			{{phone.name}}
		</p>
</body>
</html>
{% endhighlight %}




[angularjs]:    https://angularjs.org/
[angular_tutorial]:    https://docs.angularjs.org/tutorial
[angular_codeschool]:    http://campus.codeschool.com/courses/shaping-up-with-angular-js/intro
[understanding_scopes]:     https://github.com/angular/angular.js/wiki/Understanding-Scopes
[ngController_docs]:     https://docs.angularjs.org/api/ng/directive/ngController
[scope_docs]:     https://docs.angularjs.org/guide/scope