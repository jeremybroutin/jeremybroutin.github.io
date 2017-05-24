---
layout: post
title: "Lyft app deconstruction"
date: 2017-05-11
---
<h1>{{ page.title }}</h1>
<p class="meta">{{ page.date | date_to_string }}</p>

_This post is a work in progress, thanks for your patience._

As part of an ongoing university professional certificate on iOS development, we have been tasked to analyze an app of our choice and to deconstruct it. A list of sample questions were provided to guide our review, and I chose to group them under the categories exposed below.

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

![lyft_app_main_view](https://cloud.githubusercontent.com/assets/8300361/25978189/a56c3196-3675-11e7-942b-00fec35d5e2b.png)

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

## App deconstruction

### What would the data model look like?

There are several models that probably exist in the Lyft app:
- One representing the user, which will include its identification and personal information (stored credit card for instance)
- One more model exists for the selected driver, that will pick the user. This model would carry all of the driver's information such as name, car model, and review score.
- Finally, Lyft probably includes a model for a ride, that includes references to both driver and rider, the route's source, origin, date and length as well as the cost associated and any reviews.

### Where does the user-created data live? Who owns it? What are the privacy implications?

There are only two types of user-created data in the Lyft app:
- the user profile information
- the reviews given to the drivers
All of this data is stored in the Cloud (or potentially on Lyft servers), and not on the user's device directly.  
This allows a user to easily change phone without losing its information or historic rides.

In terms of ownership and privacy, the user is the owner of her personal data, and should have read, edit and delete access to it at any time.  
Lyft must provide a clear privacy policy (to which the user agrees when using the app) and which states how the personal information might or might not be shared with 3rd party companies for advertising purposes.

### What backend services are involved? What do those services need to provide?

In terms of backend infrastructure, Lyft must call some sort of real time database in order to:
- retrieve the user's information
- retrieve the currently online drivers and their live locations (as well as keeping those constantly updated)
The first set of data returned is "static" meaning that a one-off call is sufficient for the entire time the user will be in the app.  
The second however could be pretty expensive in terms of bandwith and battery on the user end, and I would safely assume that both user and drivers locations are only updated when the app is awake and in the foreground.

## UI analysis

### What custom UI is used ? How you would implement it?

- The main interface relies on GMSMapView, which is provided by the Google Maps SDK.  
- Lyft then adds the ride ordering process in a custom UIView that overlays the mapView.
![lyft_app_main_view](https://cloud.githubusercontent.com/assets/8300361/25978189/a56c3196-3675-11e7-942b-00fec35d5e2b.png)

- Interacting with this overlay triggers a modal View Controller, which includes a [tableview][4] with multiple sections:
	- The first three sections are static
	- The fourth is dynamic based on the automated results provided by Google (in relation with the current user location)
- In addition to this main interaction channel (mapView and overlay views), Lyft also provide a slide bar menu on the left  [insert screenshot]
	- This menu is also a simple static tableview with a cell for each navigation item, as well as a header (the user profile) and a footer (promotion to become a driver)
	- This tableview is displayed upon the interaction with a button in the main viewcontroller, and can be dismissed use a [swipe right gesture][3]

### What are some helpful or interesting uses of animations?

One the additional feature provided by Lyft is the ability to order different types of rides: Line (shared route), Lyft, Plus (large vehicle), Premier (deluxe option).  
The Lyft app leverages a very useful animation to show and hide the view carrying this animation which expands and retracts to its original button, basically guiding the user as to where to find these options. I believe such animation to managed via a [UIPopoverController][5]. 
The view is displayed automatically when the app is opened, and retracts automatically as the user starts interacting with the map, therefore not disturbing the user experience when the content of the displayed view is not needed.  
![lyft_app_main_view](https://cloud.githubusercontent.com/assets/8300361/25978189/a56c3196-3675-11e7-942b-00fec35d5e2b.png)

### What's an effect/animation that you cannot figure out how to do?

When the user choses to display the menu (left hand side navigation items), the main view (that contains the mapView) size is reduced, giving an impression of a "stack" and therefore reinforcing the priority of the menu view on top of the main view. This effect, combined with the display of the menu view, would be something requiring much investigation on my end to achieve.


[1]: https://www.lyft.com/
[2]: https://en.wikipedia.org/wiki/Lyft
[3]: https://developer.apple.com/reference/uikit/uiswipegesturerecognizerappl
[4]: https://developer.apple.com/reference/uikit/uitableview
[5]: https://developer.apple.com/reference/uikit/uipopovercontroller