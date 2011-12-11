The missing history property

When using Backbone.js with CoffeeScript you can get the following message when trying to run `Backbone.history.start()`:

	TypeError: Cannot call method 'start' of undefined

If you do it could be because the constructor of your router has not be executed. Backbone only creates the history property when at least one router has initialized its routes. My code looked something like the following:

	class App extends Backbone.Router

		constructor: ->
			console.log "Inside App constructor"

	app = new App()
	Backbone.history.start()

Can you spot the reason why it didn't work in my case? It was because I created a constructor without calling `super()`. In your classes in CoffeeScript you need to call `super()` for it to call its parent constructor.