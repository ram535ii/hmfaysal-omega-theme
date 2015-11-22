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

Honestly the difference between these three symbols is pretty straight forward, but it took me ages to fully wrap my head around it and appreciate the power they gave me. If I can stop you from smacking your face into your desk even one time less than I did, I feel I have accomplished something! (Also, I'm totally assuming you know what AngularJS directives and scopes are.)

# Isolate Scope
 You will only come across these three symbols in AngularJS when you are dealing with directives declared using an isolate scope. If you are reading this you probably know what isolate scopes are, but I'll give it a quick revision anyway. Generally in Angular scope trickles downwards, like water running down the River Seine. This means that a child scope will always have access to anything declared on its parent scopes (who is upstream on the river, see what I did there?!), but a parent scope does not have access to declarations made in its children's scopes. On the surface this sounds great, but ultimately it results in an unwieldy application where everything and nothing is responsible for all the data.

This is where isolate scopes come in. When an element declares an isolate scope its relation to its parent scope changes. The child isolate scope no longer has access to data on its parent scope. You now have to pass the isolate scope the data it cares about explicitly. This is really awesome, since now we are explicit. You can know at an element and know exactly what data it needs and can change. Sticking with our wonderful analogy, that makes an isolate scope the Bastille, a prison - nothing goes in or out unless permitted. This analogy is great since just as in a prison you want to control exactly what comes in (no cakes with files please) and out (ideally not the prisoners), this is the mentality to take with elements as well.This is where these three symbols come in, they are the only keys to the prison. Before going into more detail, a quick preview of each key's power:

- @ - pass by value (attribute binding)
- & - pass by method (expression binding)
- = - pass by reference (two-way data binding)

Explaining stuff in isolation is hard, so lets use a real life example. Take a login pop-up. It has a title, the standard login fields and a close button. Pretty good example below - please imagine is has a title! In this case lets say its the login form for a bank.

TODO: namecheap pic
<figure>
  <a href="{{ site.url }}/images/tijn-angular-isolate-scope.png"><img src="{{ site.url }}/images/tijn-angular-isolate-scope.png" style="max-height: 250px;"></a>
  <figcaption><a href="http://ram535ii.github.io/" data-toggle="tooltip" title="Example Scope Setup">A t-shirt subscription service</a>.</figcaption>
</figure>

# Key 1: -- @ --

`@` is used to pass in a literal value, such as a string or number. Data can be passed from the parent to the child, but not back up. It is one way, downward communication - with one catch: you can only pass in primitives. In Angular terms this is called attribute binding (value <-> attribute). In terms of our real life example, this is ideal for passing in the title I told you to imagine. Why not just hard code it I hear you thinking. I want to be able to use the login directive in multiple contexts, such as logging in the first time, but also when a user session has timed out - the title shoudl be different for these two contexts. In the example below, the parent scope, `banking-app`, can update `expiredSessionTitle` and `login-form` will see that change, but it cannot tell `banking-app` about any change. As a result, this key is ideal for passing data that only needs to be displayed, such as a static title - but remember, primitives only.

{% highlight html %}
<banking-app>
  <login-form title ='{ { expiredSessionTitle } }'></login-form>
</banking-app>
{% endhighlight %}

See a live example proving out the concept [here](http://plnkr.co/edit/WXbifMi5MUD1sfqv7Y3d?p=preview).


# Key 2: -- & --

`&` gives you the ability to pass a method into a directive. The cool thing about this is that when the directive's isolate scope calls the method, the method will be executed in the scope of the parent, where it was originally declared.  As a result, it is effectively also one way communication, but in the upward direction. In Angular land this is called expression binding (method <-> expression). This is ideal for our login form's close button. The parent scope opened the form pop-up, so it should also be responsible to close it - so path a method in to do that. More concretely - the child scope, `login-form` can call the method `submit-login-close`and it will be executed by `banking-app` as `handleLoginClose` in its scope. Now `login-form` does not need to worry about what closing means. You could even pass an argument back with the method call, but that isn't illustrated here.

{% highlight html %}
<banking-app>
<login-form submit-login-close='handleLoginClose()'></login-form>
</banking-app>
{% endhighlight %}

I'm not lying you can see an example of this concept working [here](http://plnkr.co/edit/WtStUx8X8XSQAddldZJ0?p=preview).


# Key 3: -- = --

`=` is the secret to passing in a value by reference. I like to think of it as a pointer, so that both scopes can update the same memory location. This gives us full two way communication between the scopes - in a way it's a combination of `@` and `&` - this means we can also pass in more than primitives, most importantly objects. Angular refers to this as the now much loved two-way data binding (reference <-> two-way data binding). Now if a user is trying to extend an expired login session we can pass in all the information we want as a single object. This could include their username, time since their session expired, their favorite color - whatever! Our `banking-app` now passes in `userDetails` and `login-form` can happily display all this to the user. It could even let the user update the details on the `banking-app` parent scope, although that isn't useful here. Passing objects into directives is fantastic.

{% highlight html %}
<banking-app>
  <login-form login-details='userDetails'></login-form>
</banking-app>
{% endhighlight %}

It works! Check it [here](http://plnkr.co/edit/XKfXmqAKamRXAwYWaMn2?p=preview).

Now you know what these three mysterious symbols mean, and you didn't even have to prowl through the _wonderful_ documentation on this specific topic. I've also put together a little example of all three working at the same time [here](http://plnkr.co/edit/ZNWY4dQnBoFHc72RkE2O?p=preview). I just want to extend a thank you to [Maria Stylianou](http://github.com/marsty5) for reading my first draft and an event bigger thank you to [Peter Nixey](http://github.com/peternixey) for going through countless drafts with me.

# Some Quirks
Only read on if you are comfortable with these concepts. I just want to share a few things I have picked up along the way that I thought might stop you from making the same mistakes I did. They're kind of like those tricks you used to open that door in your student house that should probably have had its lock greased or replaced three years ago.

- The symbols are totally counter-intuitive. When I think pass by value, an `=` would make more sense. Pass by reference makes so much sense as an `@`, but it isn't - it's the exact opposite. Thanks to [Ed Saunders](http://github.com/seddy) for this observation. Angular seems to like doing counter-intuitive things like this. (Factories are singletons and services aren't, what?!)
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
