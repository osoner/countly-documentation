#Countly Drill

Countly now offers something called Countly Drill to Countly Cloud and Enterprise customers. This is a bit of a game changer and we hope to clarify how to use Countly Drill in this quick reference. Before we start to get more into the magic, we need to make sure you understand all about Countly custom events (which has been around for more than a year) since Countly Drill is all about custom events.

In the custom event system Countly lets you keep track of your own metrics in a pretty simple way by sending data like this;

	{
		"key": "Ride",
		"count": 1,
		"sum": 15.99,
		"segmentation": {
			"Car Type": "Luxury",
			"Time of Day": "15:00",
			"Coupon Used": "CLYROCKS",
			"Duration": "13"
		}		
	}

Here we are tracking **Ride** event for our made up app that has segmentation properties called **Car Type**, **Time of Day**, **Coupon Used** and **Duration** which lets us keep track of various occurrences of the same event. We use the `sum` property to store the amount paid for the ride.

We normally get a report that looks like below for our **Ride** event. Which is a great way to see a high level overview of how things are going and performing single level segmentations on our data.

<img src="http://count.ly/images/resources/drill/drill_events.png" />

Using Countly Drill we will be able to;

* Perform advanced segmentations on our data using **AND**, **OR** and **BY** filters to our segmentation properties as well as user properties such as **Device**, **App Version**, **Platform**, **Platform Version**, **Session Count**, **Session Duration**, **First Session**, **Last Session**, **Country**, **City** and **Carrier**
* View data on a **line**, **pie** or **bar** chart, whicever makes more sense to us
* Change the time bucket displayed on the chart and table to **hourly**, **daily**, **weekly** or **monthly**
* View how many times the event occured as well as how many users performed this event and an average (times/users)

Without further due we want to show you some of these highlights using real reports for our custom event **Ride**;

1. Show **Ride** events with `"Car Type": "Luxury"`
	
	<img src="http://count.ly/images/resources/drill/drill_basic.png" />

2. Show **Ride** events with `"Car Type": "Luxury"` that has a `Duration` higher than 20 and show the report segmented by `Coupon`. And please show this on a pie chart

	<img src="http://count.ly/images/resources/drill/drill_pie.png" />

3. Show **Ride** events with `"Car Type": "Luxury"` or `"Car Type": "Basic"` that has a `"Coupon Used": "CLYROCKS"`  and show the report segmented by `Country`

	<img src="http://count.ly/images/resources/drill/drill_country.png" />

4. This is all great but will I define these filters every time I need to see a report? Nope, we have bookmarks

	<img src="http://count.ly/images/resources/drill/drill_bookmark.png" />

We could have added thousand more items to this list but we believe you are ready to see it for yourself at this point :) Go on and sign up for a free account on Countly Cloud and experience the magic!



