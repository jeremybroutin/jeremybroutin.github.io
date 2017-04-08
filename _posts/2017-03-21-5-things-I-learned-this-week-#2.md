---
layout: post
title: "Review of debugging options"
date: 2017-03-10
---
<h1>{{ page.title }}</h1>
<p class="meta">{{ page.date | date_to_string }}</p>
<p>Coming in a bit late due to some travels to New York and then to India over the last couple of days but here we are:
<ol>
	<li>Basic <strong>Unit Testing</strong> and the use of the XCTest library to assert critical methods from simple projects we had previously built within the University of Washington <a href="https://www.pce.uw.edu/certificates/ios-application-development" target="_blank">iOS Certificate</a>. To deepen my understanding of Unit Testing, I have also started the <a href="https://www.raywenderlich.com/150073/ios-unit-testing-and-ui-testing-tutorial" target="_blank">Ray Wenderlich dedicated tutorial</a> which goes further with the use of stubs, mock objects, UI testing and performance testing. A new programming skill from which I just started to scratch the surface!</li>
<br />
	<li>Better/easier <a href="https://github.com/itaiferber/swift-evolution/blob/swift-archival-serialization/proposals/XXXX-swift-archival-serialization.md?utm_campaign=iOS%2BDev%2BWeekly&utm_medium=email&utm_source=iOS_Dev_Weekly_Issue_292" target="_blank"><strong>Serialization</strong> is coming for Swift</a>, and will provide a way to encode struct and enums and a type safe solution to serialize to external formats like JSON and plist. No more <code>if let dict = json["myDict"], let val = dict["myVal"]</code> or -worst- nested conditional unwrapping. It will also removed the need for dedicated framework such as <a href="https://github.com/SwiftyJSON/SwiftyJSON" target="_blank">SwiftyJSON</a>.</li>
<br />
	<li>Using <strong>inout</strong> parameters to manipulate external variables (external from the scope of the function). The variables are passed by reference, and therefore sustained any modification applied by the function. See <a href="https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/doc/uid/TP40014097-CH34-ID545" target="_blank">Apple's documentation</a> for full details.</li>
<br />
	<li>Using <strong>protocols to handle networking calls</strong> and subsequent results (with dependency injection) not only make the code more readable but also allows for better testing. Great <a href="https://www.natashatherobot.com/protocol-oriented-networking-in-swift/" target="_blank">article</a> from Natacha The Robot!</li>
<br />
	<li><strong>Method dispatch</strong>, 3 primary methods (direct, table, and message) and all of them are supported by Swift. If you ever wondered what's really behind the <code>static</code>, <code>dynamic</code>, <code>@objc</code>, <code>final</code>, or <code>@inline</code> keywords and about overall code performance, I found this <a href="https://www.raizlabs.com/dev/2016/12/swift-method-dispatch/" target="_blank">article from Raizlabs</a> extremely well written. It details how Swift handles dispatching for value types, classes, protocols and NSObjects while also highlighting what matters in how we write code (use of extensions or of reference value for instance).</li>
</ol></p>

 
