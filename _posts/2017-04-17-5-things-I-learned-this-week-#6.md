---
layout: post
title: "5 things I learned this week #6"
date: 2017-04-17
---
<h1>{{ page.title }}</h1>
<p class="meta">{{ page.date | date_to_string }}</p>

It's been a busy week at work as I started to ramp up on our internal version control system (built on Perforce).  
This weekend? The NBA playoffs started (Go Warriors!), and boum: no time for the weekly checkup.  

- Lately, there have been heated discussions in the Swift-o-sphere about **access controls**, as part of the [Apple swift-evolution GitHub repository][1].
Jesse Squires gave an [extensive point of view][2] regarding the current situation of access control in Swift 3 and how it might evolve (or not) in future versions.  
With the proposal [SE-0159][3] rejected, Erica Sadun recently proposed a new solution on the swift-evolution alias, introducing "[flexible access control scoping][4]". She proposes the addition a new declaration named `accessgroup` which would enable the customization of existing declaration, and the creation of custom access control groups.

- **Protocol Oriented Programming** makes OOP (Object Oriented Programming) obsolete. Well not exactly, but I find it very beautiful whenever I read code examples about it.  
It brings many benefits over OOP such as avoiding deep pyramidal structures between classes, preventing unnecessary inheritance for subclasses and encouraging value type coding (bye bye reference type bugs!). A couple of very useful resources are listed below for reference:
	- [WWDC 2015 session about POP][5]
	- [RayWenderlich POP Tutorial][6]
	- [Introduction to POP, by Bob Lee][7]
- Talking about protocol... In a [blog post last week][8], Josh Smith demonstarted how to leverage the [Swift's Mirror API][9] to facilitate access to the properties of struct objects (`AdressBookContact` and `FaceBookContact`) as part of an Enum (`Contact`). The result is a simple **ReflectableEnum protocol**, that ease up the implementation but which has to be used with caution:
	- it relies on a strict naming convention, as the property in the `Contact` enum have to be the exact same as the ones in the Structs
	- the protocol forces unwrap optional values, which means that the program would crash if the point above is not respected for instance
- **Debug print** and why we should be careful with logging in production code: I recently heard about debugPrint and found it handy to enhance my debugging skills a little bit. debugPrint is more powerful than the regular print as it _"writes the textual representations of the given items [...]"_ - (Apple's own definition).  
While I learned about debugPrint, I also understood the reason why we should not leave any logging statement in production code: optimization and therefore speed. 
Kostiantyn Koval highlighted in this [blog post][10] how a simple print statement left inside a for loop can prevent optimizations from the Swift compiler.

- **[Secrets of Swift's Speed][11]**, written by Mike Ash exposes different speculations regarding what makes Swift so... swift. The article is a bit old (2014) and Swift has evolved a lot since then, but the basics exposed here are still valid. So the secrets of Swift's speed are:
	- a strongly typed language, providing tighter guarantees to the compiler 
	- a faster method dispatch, leveraging vtable (an array of function pointers)
	- a more intelligent compiler:
		- able to better optimize method calls (inlining or even eliminating the call entirely)
		- able to allocate less memory (either using the stack instead of the heap, or just not allocating anything at all)
	- a better use of arguments registers for methods with multiple parameters (as Swift doesn't use _cmd compared to Objective-C)
	- aliasing is not so big of an issue (compared to C for instance) as pointers are rare in Swift


[1]: https://github.com/apple/swift-evolution
[2]: http://www.jessesquires.com/thoughts-on-swift-access-control/
[3]: https://github.com/apple/swift-evolution/blob/master/proposals/0159-fix-private-access-levels.md
[4]: https://github.com/apple/swift-evolution/pull/681/files#diff-0
[5]: https://developer.apple.com/videos/play/wwdc2015/408/
[6]: https://www.raywenderlich.com/148448/introducing-protocol-oriented-programming
[7]: https://blog.bobthedeveloper.io/introduction-to-protocol-oriented-programming-in-swift-b358fe4974f
[8]: https://ijoshsmith.com/2017/04/08/reflectable-enums-in-swift-3/
[9]: https://developer.apple.com/reference/swift/mirror
[10]: https://medium.com/ios-os-x-development/swift-log-devil-or-why-println-is-dangerous-46390453353d
[11]: https://mikeash.com/pyblog/friday-qa-2014-07-04-secrets-of-swifts-speed.html