#Implementation and configuration scenarios

Countly is an extensible, open source mobile analytics solution for mobile application developers. It tracks applications, customer behaviour or game mechanics - so you can focus on increasing user loyalty and engagement. With Countly, collected data is converted into meaningful information in true real-time, benefiting from underlying infrastructure with [MongoDB](http://mongodb.org), [Node.js](http://nodejs.org) and [Nginx](http://nginx.org).

Countly [provides two APIs](/references/reference/server-api) to write and read data. In order to write data, Countly provides SDKs (e.g [Android](https://github.com/Countly/countly-sdk-android), [iOS](https://github.com/Countly/countly-sdk-ios), [Windows Phone](http://github.com/Countly/countly-sdk-windows-phone) and [Blackberry](https://github.com/Countly/countly-sdk-blackberry-webworks)) to be used within applications on mobile devices. SDK collects usage information and sends it to Countly server. Read API can be used to retrieve data from Countly server. The whole dashboard retrieves information and visualizes in a graphical form using this Read API.

Countly is a true real-time service, showing updates every 10 seconds from user interface – which is also a configurable parameter.

## Installation

It’s advised to install Countly on a separete server to provide maximum compatibility, performance and usability. Since Countly runs on port 80 to serve its dashboard, there shouldn’t be any other web service running on the same port.

Installation is well tested on Ubuntu instances from 10.04 to 12.04. We strongly advise to get Ubuntu LTS (long term support) series to get updates timely. Installation script that is included in Countly package automates the process by; adding new repositories, downloading required files and installing to target operating system. In case Countly needs to be updated, corresponding update scripts can be used that come with package.

In its basic form, installer is used for a single instance, e.g doesn’t configure the system to work on multiple nodes. Therefore a single node is capable of handling a limited number of sessions coming from devices. A mid-range server can handle *300+ requests* per second (more than *25 million requests per day*), which is equivalent to roughly *10.000 users at the same time*. If the user base is more than that, MongoDB should be replicated and proper load balancing scenarios should be used.

<div class="centered">
<img src="http://support.count.ly/help/assets/ea7a0a214a43f37d7dd8bf0836e83029b8fdcf81/1_normal.png"/>
</div>

Countly is also [installable on Heroku](https://github.com/gabrielrinaldi/Countly-Frontend-Heroku), a PaaS service, so it’s possible to extend Countly with PaaS offerings by Heroku. We strongly advise you to take a look with this option, if you are willing to go with a hosted solution rather than on-premise.

## Device SDKs

Countly is an open source project -both for server and client side code- that is, a developer writes his own device SDK (e.g Samsung Smart TV) and benefit from Countly’s infrastructure to collect packages and then analyse outputs. If the device can make HTTP GET requests and provides required information, then it’s basically possible to write an SDK for the corresponding device. Any language can be used to write the SDK.

This chapter shows a simple explanation of how an SDK sends packages to Countly server. Initially, device sends the following data to the server:

* **app_key:** App key of the  application. This is retrieved when the application is registered on Countly management interface.
* **device_id:** Device’s UDID. Countly uses OpenUDID to generate its unique identity.
* **sdk_version:** Currently not used, but you can put “1” here for a placeholder.
* **begin_session:** Use “1” here. It defines the beginning of a session.
* **metrics:** All device specific information JSON data. An example metric is shown below:

***
<pre class="prettyprint">
{
   ”_device”:”Galaxy S II”,
   ”_os”:”Android”,
   ”_os_version”:”2.3.3”,
   ”_carrier”:”Vodafone”,
   ”_resolution”:”480x800”,
   ”_locale”:”en_US”,
  }
</pre>
***

After sending this first bulk information, device sends the following every 30 seconds to server:

* **app_key:** *(same as before)*
* **device_id:** *(same as before)*
* **session_duration:** Seconds has passed since the last message. This is generally 30 seconds, but it’s possible to extend or stretch this period.

When the application is terminated, or sent to background, following data ise sent:

* **app_key:** *(same as before)*
* **device_id:** *(same as before)*
* **end_session:** “1” *(showing that this session has ended)*
* **session_duration:** Seconds has passed since the last message. This should be calculated by you.

If the application is sent to background, then you need to send an `end_session` packet. Likewise, as user puts the information to the foreground again, send a `begin_session` packet. This ensures highest granularity and eliminates potential miscalculations.

## Installation scenarios

In this chapter we’ll have a look at different installation options for Countly. The first one is already covered before (single node option), which is a straightforward way to install Countly if you have a few million users daily, and not more than 10.000 users at the same time. It’s important to provide a failover mechanism, so that if Countly server goes down for a reason (e.g hardware failure, DB crash etc), you can rely on the other option and continue without interfering your service.

Note that SDK’s are designed so that if they cannot reach internet, or cannot reach the server for some reason, they do not crash the application they are bound to, and end gracefully so end user doesn't get notified at all. Therefore, if you server is down, then the only drawback will be not to get relevant data from devices, and corresponding visualization will not show data.

While the sharding is optional and depends on the data load, for high availability and disaster recovery, replica sets should be used.

## Splitting the database (sharding)

Sharding is the method MongoDB uses in order to split its data across two or more servers (called clusters). Countly uses MongoDB, and it’s possible to use MongoDB’s simple sharding technology to balance load across several instances. This way, it’s possible to make the cluster always available for each and every read and write process. Countly servers are mainly dependent on high number of writes issued from mobile devices, compared to very low number of reads coming from administration dashboard.

Converting an unsharded database to a sharded one is seamless, therefore it’s much better to go for sharding in case there’s a need for it. As a minimum, there are 3 config servers for a shard, and at least 2 sharded MongoDB instances. On config servers, also MongoDB instances are run, with a minor difference that they are configured to act as configuration servers.

<div class="centered">
<img src="http://support.count.ly/help/assets/44299239ef8435a23d8f8ae1c0ee25410976a928/2_normal.png"/>
</div>

Since reads in MongoDB are much faster than writes, it’s best to dedicate a higher percentage of system resources to writes (e.g by using faster disks). MongoDB writes are in RAM and they eventually get synced to disk since MongoDB uses memory mapped files.

**Note:** Sharding is available only in Enterprise Edition. 

## High availability and disaster recovery (replica sets)

While gathering analytics data is not as critical as gathering a customer information data and keeping it safe, we must make sure that all data is replicated, and recovered in case of a failure occurs. Major advantages of replica sets are business continuity through high availability, data safety through data redundancy, and read scalability through load sharing (reads).

With replica sets, MongoDB language drivers know the current primary. All write operations go to the primary. If the primary is down, the drivers know how to get to the new primary (an elected new primary), this is auto failover for high availability. The data is replicated after writing. Drivers always write to the replica set's primary (called the master), the master then replicates to slaves. The primary is not fixed – the master/primary is nominated.

<div class="centered">
<img src="http://support.count.ly/help/assets/b4bb70bb8a63c8ba648ee0203671a2e1c1000be4/3_normal.png"/>
</div>

Typically you have at least three MongoDB instances in a replica set on different server machines. You can add more replicas of the primary if you like for read scalability, but you only need three for high availability failover. If there are three instances and one goes down, the load for the remaining instances only go up by 50%  (which is the preferred situation). If business continuity is important, then having at least three instances is the best plan.

## Putting it all together

Figure below shows how the complete system with sharding and replication enabled.

<div class="centered">
<img src="http://support.count.ly/help/assets/f5ad07ee21884fa2b9035cd35844226ea281195c/4_normal.png"/>
</div>

Here, you’ll easily see that:

* Each replica set consists of a shard. There are 3 shards with 3 replica sets
* Shard config servers are on the left, with separate instances. However, since the load is low, they can be located on replica sets.
* Nginx drives mongos routing servers.
* Each mongos routes traffic to shards. Node.js on mongos serves as web server.

There are two dashboards on two routing servers, however one is redundant and can be omitted.

## Conclusion

Countly is developed with scalability and performance in mind, and this document describes potential implementation scenarios. While a single server can handle several tens of million requests per day, in some circumstances a high performance, high throughput server farm is necessary to handle incoming traffic. Once the steps towards sharding and replication are complete, scaling the cluster will be as simple as putting another server and adding it in configuration database.
