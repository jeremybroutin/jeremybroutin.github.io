---
layout: post
title: "5 things I learned this week #8"
date: 2017-05-24
---
<h1>{{ page.title }}</h1>
<p class="meta">{{ page.date | date_to_string }}</p>

1 week ago I started to work on my first Objective-C project at work, making me pretty busy as I burry myself into [Apple's documentation][1] on the language and another [Objective-C crash course for Swift developers][2]. Therefore this week's update (and potentially a few more) will include some learning about Objective-C as well.

- **Nil pointer in Objective-C** can receive messages. In comparison with Swift, it is possible to call methods on nil pointer without facing any run time issue. The call will simply do nothing and will not crash if made on a nil pointer. For instance, if I have a dog property which is of class Dog, and call [self.dog speak] without initializing dog in the first place, the speak method will not be executed and the program will continue to run normally. See this [StackOverflow thread][3] about this behavior. This is why Swift is considered as a safer language than Objective-C as such scenario would result in crash, therefore forcing the developers to be more careful when designing their code (by leveraging optionals and checking for value using conditional binding or guard statements).

- **_Nullable and _Nonnull**, the equivalent of Optionals in Swift. When I started with Objective-C (litterally 8 days ago), one of the first few things I wondered was about to declare a property as Optional. This is clearly a Swift habit (which is my first and main programming language thus far) and I thought that Objective-C simply didn't offer similar functionality. Obviously I thought wrong. From Xcode 6.3 onwards, Objective-C offers two new types annotations to let one know that a pointer might have a NULL (or nil) value or not. These can be either:
	- be applied to a pointer type: `- (AAPLListItem * _Nullable)itemWithName:(NSString * _Nonnull)name;`
	- or, better, be written using their non-underscore forms
		- in methods: `- (nullable AAPLListItem *)itemWithName:(nonnull NSString *)name;`
		- and in properties: `@property (copy, readonly, nonnull) NSArray *allItems;`
See the full explanation and code examples (from which the lines above are taken) on the [Swift blog][7].

- **Main queue vs main thread**: are the two strictly bounded together? Although it appears that yes if we read Apple's documentation on operations queues, this topic has often been discussed on the web. An [issue filed to Apple DTS team][4] in January 2016 led to a response stating that: "the main queue and the main thread are not the same thing". Several blog posts addressed this very discussion and Marcin Krzyzanomski explained on his blog that:
	- the main queue is bound to the main thread
	- but the main thread is not bound to the main queue
Basically it is not enough to check for the main thread (`NSThread.isMainThread()`) to assume that the execution is on in the main queue., as the main thread might be reused by another concurrent queue for instance.

- **enum and associated value** are extremely powerfull especially in regards to handling networking responses. By leveraging a Result enum, one case can associate the expected data (from the server response) with the Success case, while also attaching the returned error with the Failure case. This greatly improve code readibility as demonstrated by Sommer Panage in her [talk in Try! Swift 2017 at Tokyo][5], or as exposed by the [Big Nerd Ranch Photorama tutorial][6].

- **UndoManager** in Swift: Benjamin Encz shows us on his [blog post][8] how easy it is to create a Undo/Redo Manager in Swift by leveraging value types, and which is better suited to the language that the famous NSUndoManager API (widely spread in Objective-C codebases). The overall implementation is pretty simple yet very powerful, using a redo and an undo stacks to keep track of the latests annotations while updating a remote database in parallel.



[1]: https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/Introduction/Introduction.html
[2]: https://www.udemy.com/objectivec/
[3]: https://stackoverflow.com/questions/156395/sending-a-message-to-nil
[4]: https://github.com/ReactiveCocoa/ReactiveCocoa/issues/2635#issuecomment-170215083
[5]: https://news.realm.io/news/sommer-panage-writing-your-ui-swiftly/
[6]: https://www.bignerdranch.com/books/ios-programming/
[7]: https://developer.apple.com/swift/blog/?id=25
[8]: http://blog.benjamin-encz.de/post/simple-undo-redo-swift
