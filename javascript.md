# Javascript styleguide

## Indentation
- Use two spaces for indentation.

## General
- Use `camelCase` for variable, function and property names
- Use `PascalCase` for constructor names
- Avoid private properties - but when necessary, pepend their names with an underscore
- Use `""` for strings
- Use declarative names for variables and functions (no single-letter function parameters!)
- Use semicolon; 

Be expressive and use nifty Javascript shortcuts to set default values for variables and functions:

	// Don't:
	function aFunction(options) {
		if(options === undefined) {
			settings = {}
		}
	}

	// Do:
	function aFunction(options) {
		settings = options || {}
	}

Don't pollute the global scope! Use self invoked functions do define a private scope:

	// Don't:
	var variableThatWillLeak = "Foo"
	var aGlobalFunction = function() {
		return "Hi " + variableThatWillLeak
	}

	function Person(name) {
		this.name = name
	}

	window.Person = Person

	// Do:
	(function(rootScope) {
		var variableThatWontLeak = "Foo"
		var aPrivateFunction = function() {
			return "Hi " + variableThatWontLeak
		}

		function Person(name) {
			this.name = name
		}

		rootScope.Person = Person
		rootScope.globalVar = variableThatWontLeak
	})(window)

	// Outside:
	var johan = new Person("Johan")
	console.log(globalVar)
	// => "Foo"

Use the `function name() {}` construct for constructors, and the `var name = function() {}` construct for regular functions:

	// Don't:
	var Person = function() {
		this.name = "Johan"
	}

	function square(x) {
		return x*x
	}

	// Do:
	function Person() {
		this.name = "Johan"
	}

	var square = function(x) {
		return x*x
	}

*Avoid* getting into callback pyramides by using your superhuman refactoring skills to create clean, readable asynchronous code:

	// Don't
    service.uploadAvatar("image.jpg", function(res) {
        db.getPerson(2, function(person) {
			person.avatar = res.url
			db.save(person, function(newPerson) {
				service.post(newPerson, function(response) {
					console.log(response)
				})
			})
		})
	})

	// Do:
	service.uploadAvatar("image.jpg", setAvatar)

	var setAvatar = function(response) {
		db.getPerson(2, function(person) {
			person.avatar = response.url
			db.save(person, postToService)
		})
	}

	var postToService = function(person) {
		service.post(person, console.log)
	}

Even better, use *Promises* instead of callbacks:

	// Do:
	var setAvatar = function(response) {
		return db.getPerson(2, function(person) {
			person.avatar = response.url
			return db.save(person)
		})
	}

	service.uploadAvatar("image.jpg")
		.then(setAvatar)
		.then(service.post)
		.done(console.log)

This assumes that all `db` and `service` methods return promises.

## Variables

- Always use `var` for local variables.
- When declaring more than one variable at once, separate them by commas.

Example:

	// Don't:
	var firstVar = 1
	var secondVar = 2
	var thirdVar

	// Do:
	var firstVar = 1,
		secondVar = 2,
		thirdVar

Instead of rebinding `this`, use the new `bind` method for functions to bind the scope of `this`.

Example:

	// Don't:
	var App = {
		init: function() {
			var that = this
			return function() {
				console.log("Init: ", that)
			}
		}
	}


    //Do:
	var App = {
		init: function() {
			return function() {
				console.log("Init: ", this)
			}.bind(this)
		}
	}

In promise chains:

	var App = {
		name: "Awesome App",
		doStuff: function() {
			console.log(this.name)
		}
	}

	aPromiseCall.then(App.doStuff)
	// => 'Error'
	aPromiseCall.then(App.doStuff.bind(App))
	// => "Awesome App"

## Conditionals

Always use the `===` and `!==` operators when testing equality

	// Example

	console.log(1 == true)
	// => 'true'
	console.log(1 === true)
	// => 'false'

[Truth Equality and JavaScript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108).

Use shortcuts:

	// bad
	if (name !== '') {
	  // ...stuff...
	}

	// good
	if (name) {
	  // ...stuff...
	}

	// bad
	if (collection.length > 0) {
	  // ...stuff...
	}

	// good
	if (collection.length) {
	  // ...stuff...
	}

Use ternary expressions when possible:

	// Don't
	var variable
	if(something()) {
		variable = "Foo"
	}
	else {
		variable = "Bar"
	}

	// Do:
	var variable = (something()) ? "Foo" : "Bar"

## Object and Array literals

Use literals when creating objects and arrays

	// Don't:
	var arr = new Array(),
		obj = new Object()

	// Do:
	var arr = [],
		obj = {}

Remember that Javascript objects are just like associative arrays! These can be accessed with the standard `obj[prop]` construct.

Example:

	// Ye olde, boring way of accessing properties and functions:
	if(value) {
		$("#thing").slideDown()
	}
	else {
		$("#thing").slideUp()
	}

	// The Sexy Dynamic JS Way
	var method = (value) ? "Down" : "Up"
	$("#thing")["slide"+method]()	// evaluates to '$(#thing).slide<Method>()'

As always, don't abuse this and write unreadable code.

## Modules

Use the CommonJS module pattern when creating self-contained modules and managing dependencies:

	// Do:

	// A Person module
	(function() {
		var dep = require("dep")

		function Person(name) {
			this.name = name
		}

		Person.prototype.greet = function() {
			return "Hi " + this.name
		}
		 
		// Using 'exports' to define the outside interface of the module
		exports.Person = Person
	})()
	
	// A utils module
	(function() {
		var utils = {
			square: function(x) {
				return x*x
			}
		}

		module.exports = utils
	})()

	// Outside
	(function() {
		var Person = require("./person").Person,
			utils = require("./utils")

		(new Person("Johan")).greet()

		utils.square(2)
	})()

When using [Browserify](http://browserify.org/), this will work in the browser as well.

## Further reading

- [GitHub JS Styleguide](https://github.com/styleguide/javascript)
- [AirBnB JS Styleguide](https://github.com/airbnb/javascript)
- [Google JS Styleguide](https://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
