---
layout: post
title:  Cadu! <i>Now with fewer redirects!</i>
date:   2017-05-24 20:47:11 +0000
---


Recently, I added some AJAX functionality to Cadu (my personal assistant interface app... check out the readme [here](https://github.com/kjleitz/cadu)!) so that the whole page doesn't have to reload every time you want to perform any action. That's _nice._ That's _modern._ That's... _expected nowadays._

## So, what, you want a cookie? How is that special?

Yes, actually, a cookie sounds great right about now!

## Here you go!

Thanks!

## No prob!

It's not special, no. AJAX has been around for a while now. But for me, it _is_ special, because it marks the first time I've _really_ employed a lot of JavaScript (and jQuery, let alone AJAX) to create a front-end for one of my projects. I figured I'd detail some of the things that caught my attention.

## Distracted debugging

Diving back into JavaScript after spending so much time with Ruby is fun, but has its frustrations. I don't think either language is any better or worse than the other (they each have their strengths and weaknesses, and both are _very_ fun to write), but I will say that I think Ruby makes bugs easier to find. I think it even makes them easier to avoid in the first place.

In my opinion, it's not the difference in built-in methods, and it's not the difference in domains to which each language is suited. It's not the difference in types, nor the class vs. prototypal inheritance, and it's not even the descriptiveness of the error messages (although I have some... _opinions..._ there).

It's the visual noise. I make _so many fewer_ errors writing Ruby code than JavaScript. I seriously believe it's just easier to see. Maybe there's magic happening behind the scenes, and the "implicit" nature of a lot of Ruby code can cause confusion, but the issues are far outweighed by your ability to grok what's happening in the code _instantly._ Seems silly, right? Lose a few parentheses and suddenly your code is bug-free? Well, laugh all you want, but it's true. If you can understand the intention of your code, line by line, without having to parse byproducts of structure in your head, that's fewer bugs written and more bugs found. Give me whitespace and underscores over grouping symbols and camelCase any day.

## Markers and Mustaches

I don't love the concept of putting Handlebars templates in script tags right there in the HTML. It rubs me the wrong way. Maybe I'm just new to it and that feeling will change, or maybe there's a better way I'm not aware of... but for Cadu, at least, I decided to be a little hacky and combine ERB templates with Handlebars templates, for a little better organization.

I have Handlebars script tags at the bottom of the relevant pages (in my `tasks/index.html.erb`, for example), into which I render ERB partials from a `handlebars` subfolder in each relevant view directory.

Those files contain a mix of ERB and Handlebars templating languages. I use embedded Ruby only to plant dynamic values which _will not change_ based on their placement or use in the page (and only are dynamic insofar as they will be rendered server-side to generate the "correct" Handlebars template/partial to use and re-use once the page is loaded). I use Handlebars expressions to plant dynamic values which _do change_ based on their use on the page.

As long as you keep this in mind, that ERB comes first and Handlebars second, it turns out to be a pretty powerful combination for generating templates. I can use `current_user` logic and Pundit policies to generate appropriate templates that are then manipulated by JavaScript. No need for using some clever AJAX in a Handlebars helper to call back to the server for back-end functionality, or whatever else you might think of. Just a two-step render.

To be fair, it's a little messy. But that's half the fun!

## Keeping functions small

When you write functions that deal with AJAX calls, it's a little hard to keep them _short._

The practice of writing short functions, with a single responsibility, is excellent. Learning that was a revelation. It seems obvious in retrospect, but until you put a conscious effort into writing short functions, you make these gnarly, branching, nesting beasts that are hard to reason about and harder to debug. You end up repeating a lot of code unknowingly, naming things poorly, and being inconsistent in how you access similar functionality across your code. That makes things less readable, more bug-prone, and harder to come back to after a weekend away from your project.

With short, atomic, descriptively-named functions, life is easier... and because of that, I got a little tripped up when writing functions that dealt with AJAX. When you're executing code asynchronously like that, you need to pass callback functions to execute when a certain piece of data has arrived or some action has finished. Often, those functions are passed anonymously, and even more often, you can never touch that data or that action "outside" of the actual async code block.

What does that mean? It means (if you're not careful) long, sprawling functions that are hard to follow and hard to re-use, as well as all the other difficulties that come with rambling code.

One solution is to avoid anonymous functions when you can. If you name functions and make them general enough to be able to execute a specific singular action, you can pass them as the callback to your jQuery `$.post(...)`, for example. You can also allow the function that employs the AJAX call to accept a callback parameter, itself, and place it appropriately. That way, you can use that function more generically elsewhere in synchronous code, passing it whatever callback is necessary in that given circumstance.

It might seem obvious, but it was hard to wrap my head around, initially. Higher-order functions (and being aware of closures) take some getting used to, before being able to use them properly.

I imagine there's also the possibility of returning a jQuery `Deferred` object (or a Promise? _note to self: learn more about promises!_) from an asynchronous function, allowing it to "wrap" the underlying functionality of the asynchronous code and expose the retrieved data (or other result) by chaining it with handler methods like `.done()` or `.fail()`. But that's something you'll have to try yourself.

## "Repeat after me: I am a bad-ass queen. Kyuh! Kyuh! Kyuh!"

So, there you have it. I learned a lot from this project. I hope some of this info can come in handy for you, too.
