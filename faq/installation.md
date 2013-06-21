#Installation FAQ

##Where can I download Countly?

* [Download Countly server in source code](http://github.com/Countly/countly-server)
* [Download Countly in zip file from Sourceforge](http://sf.net/projects/countly)
* [Download Countly client libraries (SDKS) in source code](/resources/source/download-sdk)

##How much time does it take to install Countly?
If your server has all the requirements, then it takes approximately 5-15 minutes 
to install Countly and start collecting data from devices. 
Follow the instructions in the [Server Installation Manual](/resources/installation/countly-server-installation). Note that installation and configuration does not need any developer skills but only a **dedicated** server for this purpose.

In the future we'll provide [Amazon Machine Images](https://aws.amazon.com/amis) with Countly preinstalled, so you'll be up and running in a few minutes of time. You can also deploy these images on your own cloud/premises and run on a hypervisor to have a better control.

##There are two methods for installation in documentation, which one should I choose?##

We **strongly** suggest you use the automated installation scripts given in Countly package.

##What are the system requirements?
We develop, test and use Countly on Linux (specifically, Ubuntu). A decent Linux machine can handle several hundreds (if not thousands) requests per second coming from mobile devices. If your application is not Angry Birds or Draw Something, you can use a single server for all your hardware requirements. Countly runs happily on a virtualized hardware, too.

##What's the minimum Ubuntu server requirement?
We develop and test County on Ubuntu 10.04, 11.04, 11.10 and 12.04. Countly depends on modest software and a recent version of MongoDB, Node.js and nginx. Therefore it shouldn't be a problem if you have these packages in your Linux distribution (e.g Fedora, OpenSUSE, etc), however, you need to install them by hand.

##Which hosting provider do you suggest?

Any will do. We do our tests on both Linode and Amazon.

##Which browsers does Countly run on?
We tested Countly on Chrome, Firefox and IE9+. A recent(ish) version of these modern browsers works well. We do not support IE8.

##What's the programming language and underlying infrastructure?
Countly relies on [MongoDB](http://www.mongodb.org/), Node.js and Nginx. Main programming language is Javascript. Countly doesn't use any other web server, application server or database.

##How can I keep the system up-to-date?
You can download new version and install it on your server. In the future, we'll provide automatic updates for our subscribers.

##How much bandwidth does Countly SDK consume?
Every 30 seconds, Countly SDK connects to server and updates connection information. Each connection includes 60-70 bytes of data to be written to the database, excluding package overhead. Therefore the network overhead is very negligible.

##What's the minimum mobile operating system requirement?
Countly needs a minimum of Android 2.1 and iOS 3.1 to work.

##What's the recommended installation directory?
Any directory (your user home dir, /var directory, /usr/local etc) is just tine. If you happen to have a setup that reveals some folder to public access (for ex. public_html folder) you may want to avoid extracting Countly there.

##I'm getting errors while installing node's time module
Username that you are using while installing Countly is very important especially while installing time module using Node Package Manager (npm). Since Linux treats "sudo su" and "sudo" differently, you should choose one method. We prefer running "sudo ./countly.install.sh".

##Do I need a mail server?
Starting from version 12.06, Countly needs an MTA to send emails to the user created by admin. MTA can be any SMTP server (e.g Postfix, Exim or Sendmail) that's installed on your server, or you can use remote SMTP and let another server handle the mail sending process. By default, Countly automated installer will use Sendmail, however you can change the installation script so it installs Postfix or Exim.

##Is it possible to use Apache mod_proxy instead of Nignx?

Yes. [See this thread](http://support.count.ly/discussions/suggestions/16-apache2-proxy)

## How can I restart Countly?

In order to restart Countly, type the following as root:

<pre class="prettyprint">
# stop countly-supervisor
# start countly-supervisor
</pre>

##How do I reinstall Countly?

Deleting the `countly` directory, extracting the new package to the same directory and executing `countly.install.sh` should do the trick.
