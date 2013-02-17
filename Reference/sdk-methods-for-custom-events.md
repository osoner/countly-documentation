#SDK Methods for Custom Events

With the release of v12.08, we have introduced a custom event system in Countly. In this article we will go over the functionality by showing the usage of the methods in the Countly SDKs.

In all the examples below we will be recording a **purchase** event. Here is a quick summary what information each usage will provide us;

* Usage 1: how many times **purchase** event occured.
* Usage 2: how many times **purchase** event occured + the total amount of those purchases.
* Usage 3: how many times **purchase** event occured + which countries and application versions those purchases were made from.
* Usage 4: how many times **purchase** event occured + the total amount both of which are also available segmented into countries and application versions.

##1. Event key and count

**iOS:**

	[[Countly sharedInstance] recordEvent:@"purchase" count:1];

**Android:**

	Countly.sharedInstance().recordEvent("purchase", 1);

**Windows Phone:**

	Countly.CountlyEvent ev = new Countly.CountlyEvent();
	ev.Key = "User Login";
	ev.Count = 1;
	Countly.SharedInstance().PostEvent(ev);

##2. Event key, count and sum

**iOS:**

	[[Countly sharedInstance] recordEvent:@"purchase" count:1 sum:0.99];

**Android:**

	Countly.sharedInstance().recordEvent("purchase", 1, 0.99);

**Windows Phone:**

	Countly.CountlyEvent ev = new Countly.CountlyEvent();
	ev.Key = "Purchase";
	ev.Count = 1;
	ev.Sum = 125;

	Countly.SharedInstance().PostEvent(ev);

##3. Event key and count with segmentation(s)

**iOS:**

	NSDictionary * dict = [NSDictionary dictionaryWithObjectsAndKeys: @"Turkey", @"country", @"1.0", @"app_version"];

	[[Countly sharedInstance] recordEvent:@"purchase" segmentation:dict count:1];

**Android:**

	HashMap<String, String> segmentation = new HashMap<String, String>();
	segmentation.put("country", "Turkey");
	segmentation.put("app_version", "1.0");

	Countly.sharedInstance().recordEvent("purchase", segmentation, 1);

**Windows Phone:**

	Countly.CountlyEvent ev = new Countly.CountlyEvent();
	ev.Key = "Purchase";
	ev.Count = 1;
	ev.Segmentation = new Dictionary<string,string>();
	ev.Segmentation.Add("Country", "Turkey");
	ev.Segmentation.Add("Age", "28");

	Countly.SharedInstance().PostEvent(ev);

##4. Event key, count and sum with segmentation(s)

**iOS:**

	NSDictionary * dict = [NSDictionary dictionaryWithObjectsAndKeys: @"Turkey", @"country", @"1.0", @"app_version"];

	[[Countly sharedInstance] recordEvent:@"purchase" segmentation:dict count:1 sum:0.99];

**Android:**

	HashMap<String, String> segmentation = new HashMap<String, String>();
	segmentation.put("country", "Turkey");
	segmentation.put("app_version", "1.0");

	Countly.sharedInstance().recordEvent("purchase", segmentation, 1, 0.99);

**Windows Phone:**

	Countly.CountlyEvent ev = new Countly.CountlyEvent();
	ev.Key = "Purchase";
	ev.Count = 1;
	ev.Sum = 125;
	ev.Segmentation = new Dictionary<string,string>();
	ev.Segmentation.Add("Country", "Turkey");
	ev.Segmentation.Add("Age", "28");

	Countly.SharedInstance().PostEvent(ev);



Keep in mind that there is **no limit** on number of segmenation key/value pairs to use, so you can extend the above examples and use country, app\_version, game\_level, time\_of\_day and any other segmentation that will provide you valuable insights.