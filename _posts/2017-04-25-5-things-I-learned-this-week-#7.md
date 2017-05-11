---
layout: post
title: "5 things I learned this week #7"
date: 2017-04-25
---
<h1>{{ page.title }}</h1>
<p class="meta">{{ page.date | date_to_string }}</p>

Time is scarse these last couple of weeks so let's dive right in!

- **Stride**

- **Functional programing** is a paradigm, a way of thinking about code, that can be simplified around two key concepts:
	- avoid state aka not creating temporary variable or constant (immutable state).
	- rely on pure functions, each function has one and only one purpose and has no side effects.
In Swift, a couple of tools can greatly help us think and build functional code:
  	- `map`, that allows to iterate over each element of an array of dictionary and apply a specific function on each element.
  	- `filter`, that allows to return a filtered list of elements based on a function passed in the closure and against which each element of the array is evaluated.
  	- `reduce`, which is a simple way to return a single value of out of an array, by concatenating strings or summing up ints for instance.
These are called high order functions and are first class citizens in functional programming languages. High order functions accept other functions as parameter and/or return functions as well.

- To pass elements from one class to another, several options exists (notifications, KVO...) but one of the most common is to use the **delegate pattern**. Let's say for instance that you want to pass data from a `store` class that is charged with retrieving data from iCloud into your `viewController` class. 
	- You could implement a protocol that the viewController conforms to and implements to receive and display the data. 
	- Meanwhile the `store` class owns a delegate variable (usually an unwrapped optional) that the `viewController` declared after initializing the `store` class.
	```
	// in store class
	var delegate: MyDelegate?
	// in viewController class
	let store = Store()
	store.delegate = self
	```
	- Now that both classes are hooked up, the `store` can simply call the delegate function whenever it is finished receiving data and ready to pass it to the `viewController`
	```
	self.delegate?.myDelegateFunction()
	```
This [StackOverflow response about Swift delegates in Swift 3][1] is extremely good and detailed.

- **iCloud Key Value Store** is an extremely simple way to store small bites of information in the cloud, allowing for instance a user to sync its app preferences or latest changes across all of her devices (iPhone and iPad for instance). Using the NSUbiquitousKeyValueStore, it is extremely simple to store string, double or object:
```
var iCloudKeyStore = NSUbiquitousKeyValueStore()
iCloudKeyStore.setString("valueToBeStored", forKey: "myKeyString")
```
and to retrieve data:
```
iCloudKeyStore.stringForKey("myKeyString")
```
I like to think about it as a cloud UserDefaults :)

- The iOS MapKit framework includes the **[`MKPolyline`][2]** class to represents the "line" connecting multiple CLLocations. Using the [`MKPolylineRender`][3] companion class to visually represent it, one can now display the route a runner or a biker is taking, assuming the app has the authorization to track the user's location. If you are looking for a complete tutorial on how to leverage this MKPolyline class, I just completed the excellent RayWenderlich tutorial app called [MoonRunner][4] and I definitely recommend it.


[1]: http://stackoverflow.com/questions/40501780/examples-of-delegates-in-swift-3
[2]: https://developer.apple.com/reference/mapkit/mkpolyline
[3]: https://developer.apple.com/reference/mapkit/mkpolylinerenderer
[4]: https://www.raywenderlich.com/97944/make-app-like-runkeeper-swift-part-1

