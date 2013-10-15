### Google Cloud Messaging ###

Google Cloud Messaging for Android (GCM) is a service that's provided by Google. With this service, you can use a server to send data to any Android device that accepts this information. It's also possible to receive messages from another mobile devices. GCM cloud service handles every aspects of sending, handling and re-sending the message from server/device to the receiving party. 

GCM allows 3rd party servers (e.g Countly) to send messages to a specific application. Here, you can control which device(s) and app(s) will get the message. In order for a device to receive a message, underlying device should have at least Android 2.2 and a logged in Google account if the device version is lower than 4.0.4. For versions more than 4.0.4, a Google account is not required. The application doesn't have to be downloaded from Google Play store. 

![Architectural overview](http://developer.android.com/images/gcm/GCM-arch.png)


Countly Messaging makes a connection between GCM cloud and Countly server so a message is delivered to the device using HTTP. In order for an application to receive a message, this application doesn't have to be running (unlike in Apple Push Notifications Service). If a message is received, Android wakes up the application by sending an Intent broadcast event. If the application is set up with proper broadcast receiver and permissions, it'll wake up (or directly receive) this message and can run a function if properly set up. 

Developer of the application is responsible from what to do with the raw data that is received by the application. Different use cases include showing a notification to the user, displaying a custom interface, trigger downloading data or updating configuration of the application. 

## Setting up SDK and client ##

Configuring your SDK and client takes a few steps. Completing these steps is a requirement before using Countly Messaging.

* First, setup and configure Google Play Services SDK by downloading it. For more information about this step, see 
[Setup Google Play Services SDK](http://developer.android.com/google/play-services/setup.html).

