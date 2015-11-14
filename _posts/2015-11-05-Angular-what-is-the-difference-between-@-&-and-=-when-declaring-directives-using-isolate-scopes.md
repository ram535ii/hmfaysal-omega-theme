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

Honestly the difference between these three symbols is pretty straight forward, but it took me ages to fully wrap my head around it and appreciate the power they gave me. If I can stop you from smacking your face into your desk even one time less than I did, I feel I have accomplished something! (Also, I'm totally assuming you know AngularJS directives and scopes are.)

# Isolate Scope
 You will only come across these three symbols in AngularJS when you are dealing with directives declared using an isolate scope. Generally in Angular scope trickles downwards, like water running down the River Seine. This means that a child scope will always have access to anything declared on its parent scopes (who is upstream on the river, see what I did there?!), but a parent scope does not have access to declarations made in its children's scopes. This is really powerful, but in large views can be incredibly difficult to keep track of. This is where isolate scopes come in. When a child declares an isolate scope its relation to its parent scope changes, it no longer has access to data on its parent scope. You now have to pass in all the data you want the child scope to be aware of explicitly. The great thing is, you don't have to pass everything in, only the data the directive should really know about. Since the original scope structure was the River Seine, that makes an isolate scope the Bastille, a prison - nothing goes in or out unless permitted. This is where these three symbols come in, they are the only keys to the prison. Before going into more detail, a quick preview of each key's power:

- @ - pass by value (attribute binding)
- & - pass by method (expression binding)
- = - pass by reference (two-way data binding)

Explaining stuff in isolation is hard, so lets use a real life example. And because we can, let's use a classic one - the glorious ToDo App. The ToDo app itself will always be the parent scope. With this scope we have two different child scopes, the individual ToDo items and a form to add new ToDos. Since we are good explicit developers, we are going to use directives with isolate scopes for both out different types of child scope - see pretty illustration below. Into the Bastille!

<figure>
  <a href="{{ site.url }}/images/tijn-angular-isolate-scope.png"><img src="{{ site.url }}/images/tijn-angular-isolate-scope.png" style="max-height: 250px;"></a>
  <figcaption><a href="http://ram535ii.github.io/" data-toggle="tooltip" title="Example Scope Setup">A t-shirt subscription service</a>.</figcaption>
</figure>

# Key 1: -- @ --

### The 'let data in' key
In Angular terms `@` binds an attribute to the isolate scope. This means you are passing in a literal value. Think of it as re-establishing the standard scope structure for the given variable, a specific set of people can now enter the Bastille, but there is no way out. Data can be passed from the parent to the child, but not back up. It is one way, downward communication - with one catch: you can only pass in primitives. In the example below, the parent scope, `todo-app`, can update `item` and `todo-item` will see that change, but it cannot tell `todo-ap` about any change. As a result, this key is ideal for passing data that only needs to be displayed, such as a ToDo item (in an ideal world where nobody needs to update there ToDos) - but remember, primitives only.

{% highlight html %}
<todo-app>
  <todo-item text ='{ { item } }'></todo-item>
</todo-app>
{% endhighlight %}

See a live example proving out the concept [here](http://plnkr.co/edit/7Tyfh74Z2rqBqYNMORdh?p=preview).


# Key 2: -- & --

### The 'let data out' key
`&` allows you to bind an expression to the child scope. You are literally passing a method into the directive. The cool thing about this is that when the directive's isolate scope calls the method, the method will be executed in the scope of the parent, where it was originally declared.  As a result, it is effectively also one way communication, but in the upward direction. The Bastille has just found a way to actually let people out, but this key can't let anyone(data) in. In this example, the child scope, `add-todo-form` can call the method `submit-todo-item`and it will be executed by `todo-app` as `add-todo-item` in its scope. As a result, `todo-app` can create a new instance of `todo-item` and display the added item as you might expect.

{% highlight html %}
<todo-app>
  <add-todo-form submit-todo-item='add-todo-item(details)'></add-todo-form>
</todo-app>
{% endhighlight %}

I'm not lying you can see an example of this concept working [here](http://plnkr.co/edit/7cBkCVK3PoY4qqYUKGM3?p=preview).


# Key 3: -- = --

### The 'let data in and out' key
`=` allows you to establish two-way data binding between the child and parent scopes. You are essentially giving the directive a reference to the value. I like to think of it as a pointer, so that both scopes can update the same memory location. This gives us full two way communication between the scopes - in a way it's a combination of `@` and `&`. Well I think we just found the master key, well ish. We can now leave our ideal world and let a `todo-item` edit itself, since now both `todo-app` and `todo-item` can update the `item` or `text` depending on which scope you are looking in. This is identical to the standard two-way data binding used in Angular when you use `ng-model` to bind a controller's model to a view so it can be updated by both. Mind you, this means we can now also pass in more than primitives. Instead of just passing in the `todo-item`s text, we could pass in the entire object and display additional information such as due-date or date created. (This could alternatively have been done by passing in each attribute separately, but I'm not a fan of that.)

{% highlight html %}
<todo-app>
  <todo-item text='item'></todo-item>
</todo-app>
{% endhighlight %}

It works! Check it [here](http://plnkr.co/edit/KHCrnPnzoIYWiZUoD7Wy?p=preview).


# Some Quirks
Only read on if you are comfortable with these concepts. I just want to share a few things I have picked up along the way that I thought might stop you from making the same mistakes I did. They're kind of like those tricks you used to open that door in your student house that should probably have had its lock greased or replaced three years ago.

- The symbols are totally counter-intuitive. When I think pass by value, an `=` would make more sense. Pass by reference makes so much sense as an `@`, but it isn't - it's the exact opposite. Thanks to [Ed Saunders](github.com/seddy) for this observation. Angular seems to like doing counter-intuitive things like this. (Factories are singletons and services aren't, what?!)
- When using `@` make sure to use `{ {} }` in the directive declaration,  otherwise you will just be passing in a string directly. (This can also be used for string interpolation with is cool, for example `plan-details='subscription_number_{{plan.id}}'`.)
- When using `&` make sure to call the method with an object inside the directive. For example, if you pass it in like this `subscribe-to-plan='subscribe(details)'` the directive would have to call it like this `subscribeToPlan({details: yourDetails})`.


### Extra Resources
Egghead.io has some great resources on this stuff:

- @: [https://egghead.io/lessons/angularjs-isolate-scope-attribute-binding](https://egghead.io/lessons/angularjs-isolate-scope-attribute-binding)
- &: [https://egghead.io/lessons/angularjs-isolate-scope-expression-binding](https://stackoverflow.com/questions/14908133/what-is-the-difference-between-vs-and-in-angularjs)
- =: [https://egghead.io/lessons/angularjs-isolate-scope-two-way-binding](https://egghead.io/lessons/angularjs-isolate-scope-two-way-binding)
- And a nice little review: [https://egghead.io/lessons/angularjs-isolate-scope-review](https://egghead.io/lessons/angularjs-isolate-scope-review)


Stack overflow also has a great summary (which also references these egghead videos!):

[https://stackoverflow.com/questions/14908133/what-is-the-difference-between-vs-and-in-angularjs](https://stackoverflow.com/questions/14908133/what-is-the-difference-between-vs-and-in-angularjs)

You can also download all my plunker examples directly [here](https://github.com/ram535ii/angular-isolate-scope-examples).

Thanks for reading and may the light shine upon you.
