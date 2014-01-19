#Increasing performance for high traffic mobile applications

Countly Community Edition can serve up to several million users on a single server, and it'll work happily out of the box. Most of the time, a small server can handle several hundred users online and you'll only need to deal with the uptime and general server maintainance.

However, sometimes it might be necessary to tweak performance of the underlying system - database and server, in order to make Countly work in high traffic environment. With high traffic, we mean a few billion hits on the server per month, which is quite a big number - congratulations if your mobile app did it this high!

Countly Enterprise Edition is different in architecture. It can serve tens of billions of hits per month on a scalable infrastructure and is available for big customers. For more information about Enterprise Edition, [see this link](https://count.ly/products/editions/enterprise).



## Recommended server configuration

* Running your Countly instance on a dedicated server greatly increases network throughput performance
* Instead of using hard disks, using SSD will also decrease time to write on disk. Even high performance hard disks will [perform less than SSDs](http://blog.serverdensity.com/mongodb-performance-ssds-vs-spindle-sas-drives/). Reliability of SSD disks are also much higher than traditional disks (0.6% per year vs 2.0% per year).
* Countly will benefit from RAM on the server. At least index of your MongoDB instance should reside in the RAM. Have at least 4GB of memory, and the more the better.
* Countly performance is heavily dependent on MongoDB performance, so we suggest you read [Monitoring & Diagnostics](http://www.mongodb.org/display/DOCS/Monitoring+and+Diagnostics).

By default, Countly operates real-time and doesn't do any batch jobs or heavy pre-processing. Data is immediately inserted to MongoDB as they arrive, therefore there's no "work sans-real-time" option with Countly. Majority of work done is writing the data to memory and/or disk.

When you login to the administration panel, you only read aggregated data, which is in turn visualized on the browser. This is a very lightweight process compared to writing data to MongoDB.

##Share your experience

Since Countly doesn't produce very large data sets, the bottleneck (if there's any) would be caused by lack of RAM and improper server configuration/setup. If you are running Countly on a high traffic server, let us know about your experience.
