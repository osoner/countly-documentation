#Countly Funnels

Funnels are now available to [Countly Cloud](https://count.ly/products/editions/cloud) and [Enterprise](https://count.ly/products/editions/enterprise) users. It is pretty easy to use Countly Funnels but in case you want to read before digging deeper, here is our quick reference. 

Some fun facts before we start;

* Countly Funnels are retroactive. You don't need to create your funnel to be able to see the data for a past period.
* Countly Funnels depend entirely on [custom events](https://count.ly/resources/reference/custom-events), and a little bit on [Countly Drill](https://count.ly/resources/reference/drill).
* Funnels view on you dashboard has more code on the frontend than it has at the backend :) 

First time you open the funnels view you will be greeted by a funnel creation form. You can define the steps of your funnel by either inputting the custom event key you plan to send in the future or selecting one from your existing events. A funnel needs to have at least 2 steps.

<img src="https://count.ly/images/resources/funnels/create.png" />

After saving your funnel you will immediately be taken to your beautiful reporting view. At the top you can see how many users of your application entered this funnel by performing the first step event. Right next to it there is the success rate and number of users who have completed this funnel by performing every single event.

<img src="https://count.ly/images/resources/funnels/funnel.png" />

Let's get to the best part. You can filter the first step event by your event's segmentation properties as well as user properties (metrics) like platform, device, country etc. thanks to [Countly Drill](https://count.ly/resources/reference/drill).

<img src="https://count.ly/images/resources/funnels/funnel_filter.png" />

Most common use cases of funnel analytics are;

- Tracking in app purchase conversions, understanding the paths that lead to IAPs and optimizing them 
- Understanding which level or part of your application/game users tend to leave
- Performing A/B test analysis to see which versions perform better

We are sure that our creative community will come up with a lot more than this list. If you want to try Countly Funnels right away [sign up for a free account](https://count.ly/) on Countly Cloud now!





