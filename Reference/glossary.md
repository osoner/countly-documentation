#Glossary

In this glossary you'll find explanations to abbreviations and other terms you see in articles and Countly dashboard.

####General

* **Total users:** Number of unique devices your application is used from.
* **New users:** Number of first time users.
* **Returning users:** Number of users that have used your application at least one time before.
* **Total sessions:** Number of times your application is opened.
* **New sessions:** Number of times your application is opened by a first time user.
* **Unique sessions:** Number of times your application is opened from a unique device.
* **Average time spent:** Total duration spent using your application divided by total user count.
* **Events served:** Number of write API requests Countly Server received for your application.
* **Average events served:** Number of write API requests Countly Server received for your application divided by total user count.
* **Session frequency:** Indicator of how frequently users open your application. User is put into one of the ranges below:
	- 1-24 hours
	- 1 day
	- 2 days
	- 3 days
	- 4 days
	- 5 days
	- 6 days
	- 7 days
	- 8-14 days
	- 15-30 days
	- 30+ days
* **User loyalty:** Indicator of how many previous sessions users had. User is put into one of the ranges below:
	- 1
	- 2
	- 3-5
	- 6-9
	- 10-19
	- 20-49
	- 50-99
	- 100-499
	- Greater than 500

####Events
* **Event:** A custom metric that is not available through default functionality provided. Can be anything such as number of button clicks, in app purchase times and amounts, number of times the player finished a game level etc.
* **Event Count:** Total `count` received for an event key.
* **Event Sum:** Total `sum` received for an event key.
* **Segmentation:** Secondary key to slice the data for an event. Can be anything just like an event key and it is used to categorize the event data. An example can be using `app_version` and `country` segmentations for an `in_app_purchase` event. This way, one can compare `in_app_purchase` count for different `app_versions` and `countries` of the user.