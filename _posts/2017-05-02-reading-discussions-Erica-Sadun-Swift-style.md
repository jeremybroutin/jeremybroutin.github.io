---
layout: post
title: "Reading discussions on Erica Sadun's Swift Style book"
date: 2017-05-02
---
<h1>{{ page.title }}</h1>
<p class="meta">{{ page.date | date_to_string }}</p>

<p><strong>If there was some particular point, or overall aspect of the book, that really irritated you or inspired you, grab that and expound upon it!</strong></p>
<p>One section of the book I spent quite a lot time was "Adding lazy evaluation", probably because this was a topic I did not fully master before that. I've seen&nbsp;it here and there and even used sometimes in my own code&nbsp;(as I understood the basics of it at least), but I was clearly missing a deeper understanding of this functionality. I believe the book approaches it pretty simply while diving into more advanced details (which is exactly what I was looking for).</p>
<p>It opened a door on the bigger performance optimization topic, as I started to research more on <span style="font-size: 10pt;"><code>lazy</code></span> first and quickly found out about dynamic dispatch and access controls, better optimization for value types over reference types, unchecked operations, generics, and other tips.</p>
<p><strong>Identify one of the author&rsquo;s style recommendations that forced you to learn something new about Swift before you could understand what she was talking about.</strong></p>
<p>There were several topics that I either discovered entirely or add to reinforce to fully understand them:</p>
<ul>
<li>Currying (see below)</li>
<li>Lazy initialization (see above)</li>
<li>Functional Programming</li>
<li>Typealias</li>
</ul>
<p><strong>Explain currying. What is it? When is it useful?</strong></p>
<p>Currying is the concept of converting a function that takes multiple arguments into a sequence of functions that each have one single argument. The first function accepts only one argument, and returns a function that also accept one argument only. This second function will behave the exact same way, until we exhaust all arguments and return a single value.&nbsp;</p>
<p>A curried function can have a type: <span style="font-size: 10pt;"><code>Int -&gt; Int -&gt; Int</code></span> for instance, which is a function that takes an Int as argument, and returns a function also taking one Int argument and returning an Int. I personally find it useful to add parenthesis (although they are not necessary) to better under stand it: <span style="font-size: 10pt;"><code>Int -&gt; (Int -&gt; Int)</code></span>.</p>
<p>Function currying is particularly useful&nbsp;because it allows us to assign a parameter value at run time, based on the previous function result.&nbsp;There is no need for the program to know what value is expected for its argument until the previous call reaches the curried function.</p>
<p>I must agree that the concept is particularly hard to grasp at first, especially if like me, you do not have too much experience with functional programming, but I think that seeing actual implementation and reproducing it helps a lot.</p>
<p><strong>Do you follow the Rule of Kevin? Why or why not?</strong></p>
<p>Until now, I was mostly (if not all the time) adding parenthesis around all my trailing closures. The reason is that hitting ENTER on the placeholder in Xcode was returning this format...</p>
<p>But the rule of Kevin opened my eyes on this, and I now try to follow it every time: use parenthesis when it returns a value (when the "argument is functional") and just braces for procedural closures. It really seems like something obvious once I read and started applying this rule!</p>
<p><strong>Where do you stand on:</strong></p>
<ul>
<li><span></span><strong>same name shadowing?</strong></li>
</ul>
<p>I'm always following the name shadowing practice exposed in the book, as I find it confusing and often messy to use different symbols to unwrap optionals.&nbsp;More than often did I find myself wondering "what different name on Earth could I give to this variable for conditional unwrapping" whenever I tried not to use name shadowing. Overall I find that not using name shadowing is bad for both the developer and any code reader later on.</p>
<ul>
<li><span></span><strong>guaranteed resources?</strong></li>
</ul>
<p>I must admit though that it is extremely tempting to forced unwrap optionals when you know that a value exists: it's usually safe (for instance for image file you know exist since you added them yourself) and much faster(since you don't handle the nil case). However, I strongly believe in the concept of failing gracefully, and making sure that we handle unexpected case is definitely a good habit to get. The advices from the book in regard to the use of guard statement and precondition failure is not something I was always applying so far, but I will definitely force myself to use them going forward.</p>
<ul>
<li><span></span><strong>guard, if, and preconditions?</strong></li>
</ul>
<p>One thing that I really loved about Swift 2.0 was the introduction of the guard statement, especially against the pyramid of doom caused by nested if let conditional binding. I strongly believe in the power of guard to return as early as possible whenever something is not behaving as you would expect (nil optional or bool condition for instance). However I do agree with the book which explains that we should not always replace if statements by guard ones, especially when you need to apply some changes&nbsp;as part of the else clause.</p>
<ul>
<li><span></span><strong>unneeded use of &ldquo;self&rdquo;?</strong></li>
</ul>
<p>I really like the implicit inference&nbsp;to self that the Swift compiler is giving us. I believe it speeds up the way I write code without causing any issue whenever I need to explicitly declare it since the compiler is able to flag it for me. It is important to understand when/why self is needed however (ambiguous context, @escaping closure).</p>
<p><strong>What&rsquo;s the difference between &ldquo;weak&rdquo; and &ldquo;unowned&rdquo;?</strong></p>
<p><span>Weak and unowned are pretty similar in the sense that they both prevent retain cycle by not increasing the retain count of the object being referred. However they are different regarding their possible values.<br />UNKNOWN is like an implicitly unwrapped optionals, which means that it will never be nil&nbsp;once initialized.<br />WEAK on the other hand does zero out the pointer to the object, which means that the reference&nbsp;can be nil during its life time.</span></p>
