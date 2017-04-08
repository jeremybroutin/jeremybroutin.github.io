---
layout: post
title: "5 things I learned this week #1"
date: 2017-03-11
---

<p>I'm starting this series of weekly posts to highlight 5 things I recently learned.  
The concept is to explain each new learning in a one liner and to link to the original source or any related resource.</p>
<ol>
 	<li><strong>Xcode shortcuts</strong>: or how to add or customize keyboards shortcut to never use leave your hands off the keyboard. Credit to the <a href="http://ericasadun.com/2017/02/23/xcode-tricks-adding-keyboard-shortcuts/">Erica Sadun blog post</a>.</li>
<br />
 	<li>Adding your own <strong>custom framework</strong> in Swift is not that complicated. See the 9 min <a href="https://www.youtube.com/watch?v=vChxJ_Nk6kI">YouTube video tutorial</a> of Vea Software.
A challenge I faced though is that building the framework with "Generic iOS device" seems to prevent the compiler to identify my framework class once imported into a project (even after properly add the embedded binary). Building the framework with a different active scheme solved my problem.</li>
<br />
 	<li><strong>LLDB</strong> (<a href="https://lldb.llvm.org/tutorial.html">Low level debugger</a>) allows one to execute method after hitting a breakpoint. The command is <code>expr</code> (short for <code>expression</code>) followed by the method code.</li>
<br />
 	<li>Swift <strong>Generics</strong> can have <strong>Type Constraints</strong>. This is particularly useful when using protocol to make sure that the dynamic type conforms to specific behaviors that you previously defined. Checkout the <a href="https://www.raywenderlich.com/154371/swift-generics-tutorial-getting-started">Raywenderlich tutorial on Generics</a>.</li>
<br />
 	<li>The <strong><a href="https://github.com/airbnb/lottie-ios">Lottie library</a></strong> developed by AirBnB is pretty amazing. It enables the integration of beautiful Adobe After Effects animations in iOS app using JSON files or a URL payload. I will try to integrate it in my next project app.</li>
</ol>
<p>That's it for this week!</p>
