### What's the benefit of Countly Messaging? ###

Countly handles all communication between device and server. This gives you competitive advantage as you do not have 
to write server code. 

* All transaction is handled on the server, so you do not have to think about handling all errors and issues.
* You can focus on writing your Android/iOS application and forget about what's happening behind the scenes. 

Generally speaking, a developer can both develop mobile UI and server backend, however a system excelled to deliver
messages to devices will help developer focus on the app itself, which will save considerable amount of time and money. 

### Simply speaking, how does it work? ###

These are the basic steps you need to do, before sending a message to a list of devices.

* Enable GCM or APNS and get necessary application IDs.
* Register on our site and create your application.
* Embed Countly SDK inside your application and run it on your device.
* From Countly dashboard, send a test message to your device.
* After development & tests are completed with your app, send it to AppStore or Google Play.
* Start sending them messages via API or directly from dashboard.

### What are the technical capabilities of Countly Messaging?###

* Countly Messaging communicates directly with your client using Countly SDK. 
* It sends messages to GCM server and resends them as needed. 
* It stores API key and client registration IDs so it's reused again. 
* It can send to a specific client or all clients in the list.

