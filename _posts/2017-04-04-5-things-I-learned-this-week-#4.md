---
layout: post
title: "5 things I learned this week #4"
date: 2017-04-04
---
<h1>{{ page.title }}</h1>
<p class="meta">{{ page.date | date_to_string }}</p>

<p>Back from 8 days spent in India for work purposes and it's that time of the week again:

<ul>
	<li>Some new vocabulary for me this week, with the term <strong>SRP: Single responsibility principle</strong>. This is the concept as per which every module or class should have a single responsibility. Throughout the different tutorials, programs and classes I took about iOS development, this concept was usually taken into consideration but none of the teacher or writer explicitly referred to it - and I think that's unfortunate. This should be one of the very first topic of any programming language class or program.</li>
  <br />
	<li>Digging into the SRP concept explained above, I found this <a href="https://github.com/ochococo/OOD-Principles-In-Swift" target="_blank">GitHub repository</a> listing <strong>Object Oriented Design principles</strong>. In addition to SRP, it explains the following principles:
	
  <ul>
    <li> the Open Closed principle (extending a class behavior)</li>
    <li> the Liskov Substitution principle (subclasses must interchangeable with their base class)</li>
    <li> the Interface Segregation principle (avoid interfaces that clients do not need to use)</li>
    <li> the Dependency Inversion principle (decoupling modules)</li>
   </ul>
  All of these concepts form the <strong>SOLID</strong> acronym which represents the five basic principles of object-oriented programming an design.</li>
  <br />
  <li><strong>Method swizzling</strong> or the ability to modify methods at runtime in order to inject stubs or mocks objects. Part of my learnings on test-driven development, I came across this blog post from Jon Reid on QualityCoding.org. If the name was somewhat scary at first, the concept is fairly simple and even better news: many frameworks are available to help do the job!</li>
  <br />
	<li><strong>Swift 3.1</strong> is here and Cosmin Pupaza took the time to write an amazing <a href="https://www.raywenderlich.com/156352/whats-new-in-swift-3-1" target="_blank">article</a> about its feature on Raywenderlinch.com. Here is just a quick summary of the language updates as highlighted in the blog post linked previously:
  <ul>	
    <li>Failable numeric conversion initializer</li>
    <li>New <code>Sequence</code> (protocol) functions: <code>prefix(while:)</code> and <code>drop(while:)</code></li>
    <li>Concrete type constraints (previously only protocols could be constraints)</li>
    <li>Nested generics (and how nested class can inherit T from its outter class)</li>
    <li>Availability by Swift version (although I'm not quite sure about how useful this feature would be)</li>
    <li>Convert non escaping closures to escaping ones</li>
  </ul>
  This release also includes updates on the <a href="https://swift.org/package-manager/" target="_blank">Swift Package Manager</a>, but I have not dug into this topic yet.</li>
  <br />
	<li><strong>App size</strong> can be a pretty important factor in terms of downloads success, as Apple does not allow the download over cellular networks for apps above 100MB (nothing new but I'm catching up). Such download can only be initiated over WiFi, which could therefore results in a loss of potential users. See the <a href="https://segment.com/blog/mobile-app-size-effect-on-downloads/" target="_blank">example of Peter Reinhardt</a> who saw a 66% drop of installs after the app gain some weight and went over the 100MB limit.</li>
</ul></p>
