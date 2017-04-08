---
layout: post
title: "Review of debugging options"
date: 2017-03-10
---
<h1>{{ page.title }}</h1>
<p class="meta">{{ page.date | date_to_string }}</p>
<h2>Introduction</h2>
<p>Swift debugging is a powerful skill that allows developer to quickly identify issues and fix them. Even better, it helps us to better understand our mistakes and therefore to prevent them in the future. Which makes us better programmer in the long run</p>

<p>Before even jumping into the debugging methods described below, one must always start by reproducing the bug. This is key in order to lead our investigation and chose where we should start looking into the code. This should greatly speed up the issue identification and resolution overall.</p>
<h2>Debugging methods</h2>
<h3>Rubber duck debugging</h3>
<p>One trick that served me well numerous times is to explain what I expect my code to do to a rubber duck that I have on my desk. As my duck sucks in programming, I need to go step by step into the intended behavior of my code for it to follow along, and I usually find out what I did wrong when doing so. But in case a bug is not THAT obvious, here are the debugging methods I learned about.</p>
<h3>Caveman debugging</h3>
<p>The most simple approach to debugging is to use <code>print</code> statements, carefully placed in the code in order to gather additional information on the app's behavior as well as the values being carried by variables and/or constants.
<pre>func myFunction( param: inout String) {
	print("param is: \(param)")
	param = "Superb " + param
	print("param is now: \(param)")
}
</pre>
This will print out the value of param in the Xcode console before and after we modify it inside the function.</p>

<img class="alignnone size-full wp-image-14" src="https://swifting.files.wordpress.com/2016/04/screen-shot-2017-03-10-at-3-07-44-pm.png" alt="Screen Shot 2017-03-10 at 3.07.44 PM" width="1414" height="582" />

<p>This works well for simple/basic debugging but it becomes really cumbersome for more complex issues. Nobody wants to write hundreds of print statement just to understand the state of the app at different steps.</p>
<h3>Breakpoint debugging</h3>
<p>Here comes the breakpoints to the rescue. A breakpoint is some sort of pause button allowing you to interrupt the execution of your app at a specific... point. This is extremely useful to understand if a particular method is properly called for instance, and what is the state of our variables at any given time and to spot exactly where the code is not doing what we expected it to do.</p>

<img class="alignnone size-full wp-image-16" src="https://swifting.files.wordpress.com/2017/03/screen-shot-2017-03-10-at-3-17-24-pm.png" alt="Screen Shot 2017-03-10 at 3.17.24 PM" width="993" height="228" />

<p>When our code hits a breakpoint (while the app is running), XCode provides us detailed information about the stack frame we are in and any additional information available. All of this is done by LLDB, <strong>L</strong>ow <strong>L</strong>evel <strong>D</strong>e<strong>b</strong>ugger, which provides both a graphical and a command line interfaces:
<ul>
 	<li>the graphical interface is what allows us to place and remove breakpoints in the gutter, and is also responsible for displaying the debug area in a readable fashion (left hand side of the screenshot)</li>
 	<li>the command line interface is available in the Console (right hand side of the screenshot) and allows for advanced debugging via <a href="http://lldb.llvm.org/tutorial.html" target="_blank">LLDB commands</a>. This tool is extremely powerful (you can add breakpoints anywhere in your code for instance, without having to do it manually for each file) and even allows for the execution of methods.</li>
</ul>
</p>
<p>Breakpoints give countless information for debugging but also enable our ability to <a href="https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/debugging_with_xcode/chapters/quickstart.html#//apple_ref/doc/uid/TP40015022-CH7-SW9" target="_blank">step over, step into and step out</a> of a function we are currently investigating. No need to place a breakpoint on each line, you can control what you do next after hitting your breakpoint (including resuming code execution obviously).</p>
<h3>Visual Debugging</h3>
<p>(coming soon)</p>

 
