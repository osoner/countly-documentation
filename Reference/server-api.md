#Countly Server API Reference

This document describes the API functionality provided with Countly Server. Both read (`/o`) and write (`/i`) requests are available through the Countly Server API.

##1. Write API

First API call when user opens up your application;

	http://your_domain/i?
		app_key=AAA &
		device_id=BBB &
		sdk_version=CCC &
		begin_session=1 &
		metrics= {
			"_os": "DDD",
			"_os_version": "EEE",
			"_device": "FFF",
			"_resolution": "GGG",
			"_carrier": "HHH",
			"_app_version": "III"
		}

Second and consequent API calls are just like below. The same call is repeated every 30 seconds extending user's current session duration;

	http://your_domain/i?
		app_key=AAA &
		device_id=BBB &
		session_duration=30

Final API call ending user's session;

	http://your_domain/i?
		app_key=AAA &
		device_id=BBB &
		end_session=1


Of course each request is url encoded and does not have any of the spaces/new lines shown in the above examples;

	http://your_domain/i?app_key=AAA&device_id=BBB&sdk_version=CCC&begin_session=1&metrics=%7B%22_os%22%3A%22DDD%22%2C%22_os_version%22%3A%22EEE%22%2C%22_device%22%3A%22FFF%22%2C%22_resolution%22%3A%22GGG%22%2C%22_carrier%22%3A%22HHH%22%7D

###Parameters

####Mandatory Parameters

Parameters listed below are mandatory for **every** write API request.

* `app_key`

	Application key for the current application. Can be obtained from your dashboard after creating your application.

* `device_id`

	Unique id for the user device.

####Optional Parameters

* `begin_session`

	Indicates the start of the user session. begin\_session should be used with the API call you make at the beginning of user's session. begin\_session should be given the value 1. `sdk_version` parameter needs to be present in the request if begin_session is used.

* `end_session`

	Indicates the end of the user session. end\_session should be used with the API call you make at the end of user's session. end\_session should be given the value 1.

* `metrics`

	JSON object containing key, value pairs. metrics can only be sent together with begin_session.

	Currently below predefined metrics are valid;

		metrics={
			"_os": "DDD",
			"_os_version": "EEE",
			"_device": "FFF",
			"_resolution": "GGG",
			"_carrier": "HHH",
			"_app_version": "III"
		}

* `session_duration`

	Heartbeat like parameter for extending session duration of the user for session\_duration seconds.

* `timestamp`

	10 digit UTC timestamp for recording past data.

* `events`

	JSON array containing event objects. Each event object can have below properties;

		- key (Mandatory, String)
		- count (Mandatory, Integer)
		- sum (Optional, Double)
		- segmentation (Optional, Dictionary Object)

	A sample API call to the server will look like this;

		http://your_domain/i?
			app_key=AAA &
			device_id=BBB &
			events= [
				{
					"key": "level_success",
					"count": 4
				},
				{
					"key": "level_fail",
					"count": 2
				},
				{
					"key": "in_app_purchase",
					"count": 3,
					"sum": 2.97,
					"segmentation": {
						"app_version": "1.0",
						"country": "Turkey"
					}
				}
			]

	After this request we will be able to;

	1. See how many times user completed a level successfully or failed.
	2. See how many times in app purchase occured and the total amount of these IAPs.
	3. Segment IAP data into two levels, one is app_version and the other is country. So we will be able to identify which application version performed best in terms of IAP and which countries tend to do IAP more.


##2. Read API

Countly Dashboard uses this read API in order to fetch data for your dashboard.

	http://your_domain/o?
		app_key=AAA &
		method=BBB &

###Parameters

####Mandatory Parameters

Parameters listed below are mandatory for **every** read API request.

* `app_key`

	Application key for the current application. Can be obtained from your dashboard after creating your application.

* `method`

	Defines the data to fetch. Can take one of *sessions, users, locations, carriers, devices, device_details, app_versions, events, get_events* values.

	For example below read request fetches all location related data for the application;

		http://your_domain/o?
			app_key=AAA &
			method=locations &

####Optional Parameters

* `callback`

	Callback function name. If specified, result will be sent as a parameter to this function (JSONP).

* `event`

	This parameter is used only if `method=events` is available inside the request. Such as;

		http://your_domain/o?
			app_key=AAA &
			method=events &
			event=in_app_purchase

	It is used in order the specify which event data will be fetched and returned. If this parameter is missing from the request;

		http://your_domain/o?
			app_key=AAA &
			method=events

	First event from the event list will automatically be selected by the API and the data for this event will be returned.

* `action`

	Can only take *refresh* value for now. If the read request contains `action=refresh` parameter only the data for the current day will be returned.

		http://your_domain/o?
			app_key=AAA &
			method=locations &
			action=refresh