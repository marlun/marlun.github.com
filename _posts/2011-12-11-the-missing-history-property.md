---
layout: post
title: The missing history property
categories:
- coffeescript
- backbone
---

When using Backbone.js with CoffeeScript you can get the following message when trying to run `Backbone.history.start()`:

	TypeError: Cannot call method 'start' of undefined

If you do it could be because the constructor of your router has not be executed. Backbone only creates the history property when at least one router has initialized its routes. My code looked something like the following:

	class App extends Backbone.Router

		constructor: ->
			console.log "Inside App constructor"

	app = new App()
	Backbone.history.start()

The reason it didn't work in my case was because I created a constructor
without calling `super()`. In CoffeeScript, parent constructors is called by
default as long as you don't define a constructor, if you do, you need to call
`super()`.
