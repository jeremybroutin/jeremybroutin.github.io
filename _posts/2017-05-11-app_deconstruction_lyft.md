---
layout: post
title: "Lyft app deconstruction"
date: 2017-05-11
---
<h1>{{ page.title }}</h1>
<p class="meta">{{ page.date | date_to_string }}</p>

_This post is a work in progress, thanks for your patience._

## Introduction
### What does the app do?
[Lyft][1] is a transportation network company (source [Wikipedia][2]) or in other words, an on-demand ride sharing servide provider.
It provides users the ability to request a ride from their phone, using a network of drivers who are non professional individuals.
Anyone can sign up to become a driver but one must go under a strict screening process before being approved by the company.
For the riders, the unique requirement is to download the app, sign up and create a profile in a few minutes to be able to get their first ride.

### Who's it for?
Lyft can be used by anyone that has a phone (with the mobile app installed and a user profile, which includes a credit card for payments).
As per its current expansion, Lyft is mostly targeting people living in relatively large urban agglomerations that need to cover short trips (from home to a restaurant, or from work to the gym for instance).

### What problem/need/purpose does it address?
Lyft (like its biggest competitor Uber) addresses a need for on-demand (aka getting a ride within a few minutes max), cheap and safe way of moving around short distances.
It beats the traditional taxi business by including technology in the user experience through an intuitive mobile app, allowing users to request a pick up wherever they are.
Lyft also broke the transportation standard by its intent to build a "relationship" and a feeling of trust between riders and drivers, providing information on both protagonists prior to the pick up - including reviews from previous riders/drivers.


## Personal review
### What do you like? What parts did the developers absolutely nail?
Lyft is very simple and its usage is extremely intuitive, proving an excellent design.
It is easy to quickly understand how it works and to complete the expected action (order a ride), without the need for a help section or other tips given by the app.
One particular UI feature that I really like with Lyft is the fact that the pick up location Pin (MKAnnotation) is "fixed" on the map, allowing the users to simplify adjust the map to their desired location instead of dragging the pin (which would be cumbersome if you need to zoom or unzoom for instance).

[[https://github.com/jeremybroutin/jeremybroutin.github.io/blob/master/_images/lyft_app_main_view.png|alt=Lyft]]


### What would you steal?
There are a couple of small features that I would definitely try to reproduce:
- the navigation between view controllers which is managed by a small and simple arrow on top of the main summary view, on the lower half of the screen
- the modal presentation of the trip cost summary (some sort of translucid background with a subview acting like a pop up rising from the bottom of the screen)
- the gradient color applied to some button is something I'd also try to implement
- and finally the sliding left hand side menu panel, useful to provide access to all the app details without interfering with the main user experience

### What's confusing about the UI? What do you hate? What would you change?
There is nothing that I "hate" - otherwise I would probably have stopped using the app!
But I would say the biggest "annoyance" is how the car views (representing drivers locations) pile up on each other while zooming out.

Some minor improvements I could think of would be to:
- change the back button for the different menu option, which is currently using a vertical dots, to ease UI/navigation understanding
- customize a bit the table view controller displaying the ride history
- propose a "delete history" option, which would use SMS confirmation (code provided) to make avoid unwanted deletion
- customize the default user profile picture to something a bit more fun (and add additional encouragements when the user creates an account, detailling the benefits of adding a picture)
- change the location of the edit profile button to the bottom of its view controller


## App behaviors deconstruction
What happens when there's no network?
What happens when you deny permission requests (camera, location, microphone, etc)?
What would the data model look like?
What backend services are involved? What do those services need to provide?
What are the underlying frameworks?
What's a better noun for the user than "user"? (pilot, skipper, driver, parent, fan, traveler, reader, shopper, listener, artist)
Where are some nonobvious uses of table views, collection views, other simple UIKit elements?
Where are webviews used?
What custom UI (not available in IB, or not available at all with standard UIKit) is used? How would you implement it?
What's an effect/animation that you can't figure out how to do?
What are some helpful or interesting uses of animations? What are some inappropriate animations?
What HIG violations do you see?
What security implications do you see?
Where does the user-created data live? Who owns it? What are the privacy implications?
What are the ethical implications for a developer or a designer working on this app?
What's the business model? How does the publisher make money?


[1]: https://www.lyft.com/
[2]: https://en.wikipedia.org/wiki/Lyft