---
layout: post
title:  "Unit Testing \"controller as\" Controllers in Angular.js"
tags: coding angular.js unit-testing
---
I've decided to pick up a front-end framework, because what else am I going to do in my free time. My framework of choice is (of course) [Angular.js][angularjs], which I've been learning with the use of both the [official tutorial][angular_tutorial] and the [Code School free course][angular_codeschool]. 

I've noticed a discrepancy between the way the two different learning tools handle controllers, specifically with regards to implicitly/explicitly passing the [scope][scope_docs] to the controller. As mentioned in the [official docs][ngController_docs], there are two way of creating controllers:

1. Controller-as convention
============================
This  
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
	<ul>
		<li ng-repeat="phone in phoneList.phones">
			{{phone.name}}
		</li>
	</ul>
</body>
</html>
{% endhighlight %}




[angularjs]:    https://angularjs.org/
[angular_tutorial]:    https://docs.angularjs.org/tutorial
[angular_codeschool]:    http://campus.codeschool.com/courses/shaping-up-with-angular-js/intro
[understanding_scopes]:     https://github.com/angular/angular.js/wiki/Understanding-Scopes
[ngController_docs]:     https://docs.angularjs.org/api/ng/directive/ngController
[scope_docs]:     https://docs.angularjs.org/guide/scope