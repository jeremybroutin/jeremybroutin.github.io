---
layout: post
title: "5 things I learned this week #3"
date: 2017-03-27
---
<h1>{{ page.title }}</h1>
<p class="meta">{{ page.date | date_to_string }}</p>

<p>3rd episode in this series that keeps me reading and learning (almost) every day!
<ul>
	<li><strong>XCTest teardDown</strong>: "Every object you create in <code>setUp</code> should be destroyed in <code>tearDown</code>". <a href="http://qualitycoding.org/teardown/" target="_blank">This article</a> from qualitycoding.org explains that if an XCTestCase instance is created for every individual test invocation, it is not automatically destroyed/deallocated upon completion (which one could naturally expect thanks to <a href="https://en.wikipedia.org/wiki/Automatic_Reference_Counting" target="_blank">ARC</a>). Hence why the need of leveraging the <code>tearDown</code> method to deinitialize anything that could impact following tests. Doing so guarantees that each state are evaluated independently (which is part of the testing best practice named <a href="https://github.com/ghsukumar/SFDC_Best_Practices/wiki/F.I.R.S.T-Principles-of-Unit-Testing" target="_blank">FIRST</a>) and start with a clean state.</li>
  <br />
	<li><strong>Debugging and crash symbolication</strong>: understanding and fixing bugs can be very frustrating, but it is even more if we don't understand how useful crash symbolication can be. As Dmitry Fink mentions it in his article <a href="https://www.bugsee.com/blog/ios-crash-symbolication-dummies-part-2/" target="_blank">iOS Crash Symbolication for dummies</a>, 
  <blockquote>symbolication is the process of translating the return addresses [in a stack tracet] back into human readable method, filename and line numbers.</blockquote>
  The tutorial explains how to get the dSYM file, which is where Xcode puts all the debug information during the build process, and how to "manually" match it with a crash report. Understanding the logic is extremely useful, but hopefully several tools like <a href="https://rollout.io/blog/ios-crash-reporting-tools-2017-update/" target="_blank">these ones</a>are here to automate this process and make our life easier.</li>
	<br />
  <li><strong>Swift optimization</strong>: writing code that works is fine, but writing performant code that can easily scale up as more and more users use your app is WAY better. This is kind of "old" but this week, I came across this official swift GitHub repository: <a href="https://github.com/apple/swift/blob/master/docs/OptimizationTips.rst" target="_blank">Writing High Performance Swift Code</a>. Many advices are extremely simple to think about and implement:

  <ul>
    <li> reducing dynamic dispatch by using <code>final</code>, <code>private</code> or <code>fileprivate</code> appropriately</li>
    <li> using container type efficiently by adding the value type in an array or doing in place mutation</li>
    <li> marking protocols as class protocols if they are limited to class only</li>
     <li> and more that I'm yet to explore and fully understand.</li>
  </ul>
  </li>
	<li> <strong>Code habits</strong>: writing your tests even before you write your production code. This is something completely new to me but I do see the idea here. This concept was introduced to me by Essential Developers in their TDD (<strong>Test Driven Development</strong>) <a href="https://www.youtube.com/playlist?list=PLyjgjmI1UzlSUlaQD0RvLwwW-LSlJn-F6" target="_blank">YouTube series</a>. The two developers, Caoi and Mike, share weekly videos on how they go about building an app from the idea until the full code completion, demonstrating:
  <blockquote> the discipline of test driven development, the power of modular systems, and how to welcome future requirements.</blockquote>
  Each week covers a new topic from storyboard prototyping to testing, swift closures and recursion, retain cycles, or writing a framework.</li>
  <br />
	<li> <strong>guard vs if let</strong>: in <a href="https://www.natashatherobot.com/swift-when-to-use-guard-vs-if" target="_blank">her article</a> Natasha the Robot discusses the difference between the two options to safely unwrap values, and when one should chose one vs the other. The conclusion is pretty straight forward, use <code>guard</code> if the value you are looking for MUST be present (and if not you can gracefully exit) and use <code>if let</code> if this value can also be nil (which allows you to continue even without this value).</li>
</ul>
</p>
