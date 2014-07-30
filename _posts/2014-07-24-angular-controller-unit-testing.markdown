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

And then, in order to utilize the controller in your page, do the following in your html:

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

2. "Controller-as" Convention
---------------------------
This convention, used in the [Code School free course][angular_codeschool], allows you to avoid many of the problems associated with scope in Angular. To utilize this declaration, simply follow the following convention in your module:

{% highlight javascript linenos%}
// app.js
var app = angular.module('controllerAsExample',[]);
app.controller('asCtrl', function(){
	this.data = [
	...
	];
});
{% endhighlight %}

... and the following convention in your html file:

{% highlight html linenos%}
<body ng-controller="asCtrl as controllerNick">
		<p ng-repeat="item in controllerNick.data">{% raw %}
			{{item.name}}
		{% endraw %}</p>
</body>
{% endhighlight %}

Notice that in the html file, we needed to access data by calling "controllerNick.data", instead of just using "data" as in the previous convention.
In order to test this convention in Karma, use the following convention:

{% highlight javascript linenos%}
describe('asCtrl', function(){

	beforeEach(module('controllerAsExample'));

	it('should create data model with 3 items', inject(function($controller) {
		ctrl = $controller('asCtrl', {});
		expect(scope.data.length).toBe(3);
	}));
});
{% endhighlight %}

And that's all there is to it! You simply don't inject the $scope into the $controller in the second use case, and your unit tests will work exactly as you expect!

[angularjs]:    https://angularjs.org/
[angular_tutorial]:    https://docs.angularjs.org/tutorial
[angular_codeschool]:    http://campus.codeschool.com/courses/shaping-up-with-angular-js/intro
[understanding_scopes]:     https://github.com/angular/angular.js/wiki/Understanding-Scopes
[ngController_docs]:     https://docs.angularjs.org/api/ng/directive/ngController
[scope_docs]:     https://docs.angularjs.org/guide/scope