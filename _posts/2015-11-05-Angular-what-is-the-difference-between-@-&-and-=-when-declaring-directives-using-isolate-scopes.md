---
layout: post
title: Angular - What is the difference between @, & and = when declaring directives using isolate scopes
description: ""
headline: "Value, method and reference"
categories: technical
tags:
  - geeky
  - web-development
comments: false
mathjax: null
featured: true
published: false
---

Honestly the difference between these three symbols is pretty straight forward, but it took me ages to fully wrap my head around it and appreciate the power they gave me. If I can stop you from smacking your face into your desk even one time less than I did, I feel I have accomplished something!

# Isolate Scope
 You will only come across these three symbols in AngularJS when you are dealing with directives declared using an isolate scope. Generally in Angular scope trickles downwards, like water running down the River Seine. This means that a child scope will always have access to anything declared on its parent scopes (who is upstream on the river, see what I did there?!), but a parent scope does not have access to declarations made in its children's scopes. This is really powerful, but in large views can be incredibly difficult to keep track of. This is where isolate scopes come in. When a child declares an isolate scope its relation to its parent scope changes, it no longer has access to data on its parent scope. You now have to pass in all the data you want the child scope to be aware of explicitly. The great thing is, you don't have to pass everything in, only the data the directive should really know about. Since the original scope structure was the River Seine, that makes an isolate scope the Bastille, a prison - nothing goes in or out unless permitted. This is where these three symbols come in, they are the only keys to the prison. Before going into more detail, a quick preview of each key's power:

- @ - pass by value (attribute binding)
- & - pass by method (expression binding)
- = - pass by reference (two-way data binding)

Explaining stuff in isolation is hard, so lets use a real life example. You have come up with a brilliant product, a t-shirt subscription, one new shirt every few days (no laundry?). When getting users to sign up, the subscription is down river from the product. The product knows about subscriptions, but subscriptions know nothing about the product. As a result, the parent scope will be the product. That makes the subscription the child scope, and since we are good explicit developers, we are going to use a directive with an isolate scope. Into the Bastille!

# Key 1: -- @ --
In Angular terms `@` binds an attribute to the isolate scope. This means you are passing in a literal value. Think of it as re-establishing the standard scope structure for the given variable, a specific set of people can now enter the Bastille, but there is no way out. Data can be passed from the parent to the child, but not back up. It is one way, downward communication. In the example below, the parent scope, `my-product`, can update `details` and `my-product-subscription` will see that change, but it cannot tell `my-product` about any change.

{% highlight html %}
<my-product>
  <my-product-subscription plan-details='{ { details } }'></my-product-subscription>
</my-product>
{% endhighlight %}

See a live example [here](http://plnkr.co/edit/7Tyfh74Z2rqBqYNMORdh?p=preview).

Useful application:
To pass visual data into a directive. For example, someone has a subscription to your awesome t-shirt thing and you want to show what subscription they are on in your directive. The parent gives the child directive the details, which promptly displays them - no more communication necessary.

# Key 2: -- & --
`&` allows you to bind an expression to the child scope. You are literally passing a method into the directive. The cool thing about this is that when the directive's isolate scope calls the method, the method will be executed in the scope of the parent, where it was originally declared. The Bastille has just found a way to actually let people out, but this key can't let anyone in. As a result, it is effectively also one way communication, but in the upward direction. In this example, the child scope, `my-product-subscription` can call the method `subscribe-to-plan`and it will be executed by `my-product` as `subscribe` in its scope.

{% highlight html %}

<my-product>
  <my-product-subscription subscribe-to-plan='subscribe(details)'></my-product-subscription>
</my-product>
{% endhighlight %}

See a live example [here](http://plnkr.co/edit/7cBkCVK3PoY4qqYUKGM3?p=preview).

Useful application:
To allow a visual element to pass data upwards to a higher level controller. For example, your first customer is ready to buy and they want to select a subscription, so they click on the subscription they want, in his case our isolate child scope. This directive receives this click and calls a method in its parent scope. The parent controller can then perform the correct action, like collecting card details, to then create and persist the subscription.

# Key 3: -- = --
`=` allows you to establish two-way data binding between the child and parent scopes. You are essentially giving the directive a reference to the value. I like to think of it as a pointer, so that both scopes can update the same memory location. This gives us full two way communication between the scopes - in a way it's a combination of `@` and `&`. Well I think we just found the master key, well ish. Now both `my-product` and `my-product-subscription` can update the `product`. This is identical to the standard two-way data binding used in Angular when you use `ng-model` to bind a controller's model to a view so it can be updated by both.

{% highlight html %}
<my-product>
  <my-product-subscription color='color'></my-product-subscription>
</my-product>
{% endhighlight %}

See a live example [here](http://plnkr.co/edit/KHCrnPnzoIYWiZUoD7Wy?p=preview).

Useful application:
To pass data back and forth. The new customer wanted blue t-shirts. Now you ask them to select their subscription, from a selection of nice blue boxes - we want a consistent experience. But in the process you want to let them change to a different color. Here you would need the binding in both ways since the subscription needs to know what color was initially selected for our UI prettification, but it needs to let the parent know if it changed along the way, wouldn't want to ship the wrong color.

# Some Quirks
Just a few things I have picked up along the way that I thought might stop you from making the same mistakes I did. They're kind of like those tricks you used to open that door in your student house that should probably have had it's lock greased or replaced three years ago.

- The symbols are totally counter-intuitive. When I think pass by value, an `=` would make more sense. Pass by reference makes so much sense as an `@`, but it isn't. Thanks to [Ed Saunders](github.com/seddy) for this observation. Angular seems to like doing counter-intuitive things like this. (Factories are singletons and services aren't, what?!)
- When using `@` make sure to use `{ {} }` otherwise you will just be passing in a string directly. (This can also be used for string interpolation with is cool, for example `plan-details='subscription_number_{{plan.id}}'`.)
- When using `&` make sure to call the method with an object inside the directive. For example, if you pass it in like this `subscribe-to-plan='subscribe(details)'` the directive would have to call it like this `subscribeToPlan({details: yourDetails})`.


### Extra Resources
Egghead.io has some great resources on this stuff:

- @: [https://egghead.io/lessons/angularjs-isolate-scope-attribute-binding](https://egghead.io/lessons/angularjs-isolate-scope-attribute-binding)
- &: [https://egghead.io/lessons/angularjs-isolate-scope-expression-binding](https://stackoverflow.com/questions/14908133/what-is-the-difference-between-vs-and-in-angularjs)
- =: [https://egghead.io/lessons/angularjs-isolate-scope-two-way-binding](https://egghead.io/lessons/angularjs-isolate-scope-two-way-binding)
- And a nice little review: [https://egghead.io/lessons/angularjs-isolate-scope-review](https://egghead.io/lessons/angularjs-isolate-scope-review)


Stack overflow also has a great summary (which also references these egghead videos!):

[https://stackoverflow.com/questions/14908133/what-is-the-difference-between-vs-and-in-angularjs](https://stackoverflow.com/questions/14908133/what-is-the-difference-between-vs-and-in-angularjs)

You can also download all my examples directly [here](https://github.com/ram535ii/angular-isolate-scope-examples).

