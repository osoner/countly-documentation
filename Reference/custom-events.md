#Custom Events

As you all know Countly 12.08 release includes long-awaited custom events feature. This means a whole new world of tracking so we wanted to explain a litle what events can do for you.

####Basics

The structure of the simplest event object is just like below;

	{
		"key": "button_click",
		"count": 1
	}

Below properties are the only mandatory properties for an event;

- `key` identifies the event
- `count` is the number of times this event occured

If the event is tied to an overall numerical data, such as a purchase, we can use `sum` to keep track of that;

	{
		"key": "in_app_purchase",
		"count": 1,
		"sum": 0.99
	}


####Segmentation

In the **Basics** section we have seen an example `in_app_purchase` event that had only `count` and `sum` properties. It is nice to be able to track total number of purchases and total amount of purchases but sometimes we may need more detailed information;

- What item is purchased more?
- Which countries were top performers in terms of in app purchase?
- Which application version lead to more sales?

Segmentation makes it possible to categorize/label an event in order to answer all those questions and much more. By simply adding segmentation key-value pairs to our event we can track detailed metrics;

	{
		"key": "in_app_purchase",
		"count": 1,
		"sum": 0.99,
		"segmentation": {
			"app_version": "1.0",
			"country": "Turkey",
			"item": "sword"
		}
	}

An event key can have unlimited number of segmentation key-values and all these segmentation keys will be available from your dashboard the moment you first use them inside your application.