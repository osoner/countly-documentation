#Technical FAQ

##How does Countly platform work?
After your install Countly SDK in your application, users of this application start sending event data to Countly server. From these events, Countly gathers information about what they do, how they behave, which operator they are on, etc.

##Which language is Countly written with?
We are using [Node.js](http://nodejs.org/) and [MongoDB](http://www.mongodb.org/). Both backend and frontend are completely written in javascript. You can take a look at the [API code](https://github.com/Countly/countly-server/blob/master/api/api.js) which collects data from client SDKs and writes this data to database.

##How are event and session data sent to Countly?
As the user opens the application, Countly SDK starts collecting data the way you define. Events and sessions are collected and then sent to Countly (or your) servers using HTTP srequest every 60 seconds.

##Does Countly show my data in real-time?
All reports and charts are shown in real-time. There are no batch processes running in the background to visualize or collect data, so you don't have to wait for the next process to run.

##Will Countly slow down my mobile application?
Our lightweight SDK works asynchronously and doesn't block any function calls inside your code.

##What happens if SDK cannot send requests?
If your mobile application cannot send an event information (mainly due to the fact that device is not connected to internet, user is on a plane or underground), then this information is stored in memory. As soon as the connection is established, it's sent to the server.

##How many users can a Countly server handle?
In our tests, a high configuration server can handle 700 events per second, which is roughly 20.000 concurrent mobile users. See [implementation and configuration scenarios](/resources/reference/implementation-scenarios) for potential installation alternatives. However, do not take this number as a reference as it depends a lot on number of events, network load, configuration, disk speed, RAM size and many other criteria.

##Are there any video tutorials for installing and configuring Countly? 
Andrew Krowczyk of [Magrocket](http://magrocket.com) prepared wonderful videos for Countly: 

* [Installing and setting up Countly](http://www.youtube.com/watch?v=WaNme8YS0S0)
* [Configuring Countly](http://www.youtube.com/watch?v=EwBf99Btntw)
* [Custom events](http://www.youtube.com/watch?v=BpwSuXtvjsI)

##Where should I put my Countly start code for Android? 
In as much activity as you can, preferably in each activity.

##When I compare iTunes data with Countly dashboard, I see slight difference regarding new users. What can be causing this?
Countly counts new user as unique device IDs, that is, if a user downloads the same app to iPhone and iPad, it's counted twice. Apple counts it once.

##What's the hostname I should write inside SDK when I use Countly Cloud?
You must use https://cloud.count.ly when you use our service, instead of your own server.

## I reinstalled Countly and need to create an app using the previous key. How can I do that? 

If you reinstalled Countly and need the app key in order to create another application with he same key used by
your previous applications,follow the steps below: 

1. Login to your server shell
2. Connect to mongodb like this: `mongo countly`
3. Execute `db.apps.find()`
4. Find the id of the application that you want to modify 
5. Execute the update like this: `db.apps.update({id: "ID_YOU_GOT_FROM_PREVIOUS_STEP"},{"$set": {"app_key": "NEW_APP_KEY"}});`

## How do I make Countly use all cores in my server? 

Starting from v13.06, we added cluster mechanism to api.js to fork 
itself according to number of cores in the server in order to increase utilisation. 
This can also be configured from api/config.js by changing "worker" count.

## Are there any limits on data collected? 

Both yes and no. In some cases we limit the data sent to make Countly perform better and handle absurd conditions: 

1. There's a limit of 100 characters for event keys.
2. There's a limit of 100 segmentations per event and each of those segmentation can have 1000 unique values at most.
3. There are no limits on CPU or RAM of the server
4. There are no limits on number of accounts, applications or users

## Help! MongoDB eats 100% CPU.

If you collect events having a lot of unique segmentation values (e.g almost unique to every user, for example), 
this will cause collection sizes to be "extreme", causing locks all over the place.

some events that take parameters which value is almost unique per user

## How do I remove all users and define a new user? 

1. Login to your server terminal with root credentials
2. Type "mongo countly"
3. Type "db.members.drop()"

This way existing members will be deleted so that you will be redirected to the setup screen again.

##How do I debug api.js when requesting servername/i URL?

You can use a module like [node-inspector](https://github.com/node-inspector/node-inspector) if you want to go into detail.

##How do you calculate online users? 

Online users are unique users that we received a begin_session for and has an ongoing session 
extended by session_duration and/or event requests. We consider the user as offline as soon 
as we receive an end_session request for him or 60 seconds passed since last request received.

This feature is available only for Cloud/Enterprise Editions. 

##How do calculate live users barchart?

When you login to the dashboard, the live users chart on top right of the page shows you how many users have opened your app for the last 10 seconds. So if you read "80" there, that means your app has been opened by 80 users for last 10 second
time frame.

This feature is available only for Cloud/Enterprise Editions. 

## What happens if my users send my application to the background? 

As soon as your application is sent to background, the session is over. Session calculation doesn't involve apps that are
sitting on the background, so for a session to be live, app should be running and sending data to server.

##How can I test my new translations and where do I put my files?
Under countly/frontend/express/public/localization there are three folders;

1. dashboard
2. help
3. pre-login

There are also three translation files on [Transifex](http://transifex.com/projects/p/countly/). In order to test your translation you can upload your translation file like dashboard_ru.properties, help_ru.properties, pre-login_ru.properties to the corresponding folder. In order to be able to switch between languages you need to edit:

1. [countly/frontend/express/views/dashboard.html](https://github.com/Countly/countly-server/blob/master/frontend/express/views/dashboard.html#L132) and add <a data-language-code="ru" class="item">Русский язык</a>
2. [login.html](https://github.com/Countly/countly-server/blob/master/frontend/express/views/login.html#L37) and add <a data-language-code="ru" class="item">Русский язык</a>

Repeat step 2 for forgot.html, setup.html and reset.html under the same folder.
