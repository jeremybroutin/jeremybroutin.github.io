This week I spent a lot of time on one particular topic which is not directly related to Swift but yet still relevant from a mobile app development perspective.  
- MachineZonejust released a new live data feeds API called *[Satori] (https://www.satori.com)*. This API provides live data of existing channels such as GitHub, Twitter or Weather feeds and also enable people to create their own. Simply subscribe to an existing channel and you will start receiving live data! I've started to test it with a few channels to get and store data, that my apps can use to display useful information.
- *Firebase Functions*: Firebase offers Cloud functions capabilities to react to key information within the app and trigger any remote work on Google Cloud (Firebase is built on top of Google Cloud). This is both extremely simple and powerful to execute heavy functions outside of your app and pass whatever outputs back to it, while leveragign the computing power of Google. A couple of use cases include:
	- entry modification when written into the Firebase Realtime database
	- converting images when stored in Firebase Storage
	- sending email confirmation via Firebase Cloud Messaging
	- and much more which are publicly available on the [Firebase GitHub repository](https://github.com/firebase/functions-samples/)
- Understanding *nil, Nil, NULL and NSNull*. If one of the main benefit of Swift over Objective-C is that it is a safer language, I found it really interesting to understand more about nil (null) pointers and their origins from C and Objective-C languages. [Matt Thompson's article](http://nshipster.com/nil/) on NSHipster explains the following:
	- In Objective-C, a newly allocated object starts as nil but yet this object can receive message to it, message that would simply be dropped, becoming a no-operation (if the object is still nill). Swift protects from such behavior via [optional type](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/TheBasics.html). 
	- Nil is slightly different as it is a class pointer and the author does mention that we don't see this one very often.
	- NULL simply represents "nothing" for pointers
	- NSNull is a class pointer (like Nil) and therefore an actual object (singleton object actually) used to represent null. It can be particularly useful in building dictionaries with null values, since value for a specific key cannot actually be null (but can be NSNull!)
	<code>
	let myNullObject = NSNull()
	var dict = [
	"key": myNullObject
	]
	print(dict["key"]!)
	// dictionary can be built and print statement gives <null>
	</code>
- Topic 4
- Topic 5