# Server installation 

This document explains how to install Countly server version 12.08, 12.09, 12.12 and 13.04

<center>
<p><a class="sign-in" href="http://sf.net/projects/countly">Download Countly Community Edition</a></p>
</center>

### Requirements

Countly can be installed on Ubuntu Linux, running 10.04 LTS, 11.10 or 12.04 LTS. We highly recommend that you use
a dedicated VPS for Countly. By default, Node.js (the web server Countly needs) need to run on port 80, so make sure 
this port is free, i.e Apache is not running.

In this article, we will not be talking about securing your web server, like disabling root ssh, 
private keys, closing default ports etc. for the sake of keeping things focused. 

*IMPORTANT NOTE:* Easy installation script provided inside ZIP file (`countly/bin/coountly.install.sh`) takes care of all the steps listed below. We strongly suggest you use that script instead.

This is how you'll fire the easy installation script that comes with Countly: 

<pre class="prettyprint lang-sh">
cd bin
bash countly.install.sh
</pre>

If you are brave enough, go on :-)

## 1. First things first

Update your repository information.

<pre class="prettyprint lang-sh">sudo apt-get update</pre>

## 2. Install python-software-properties

<pre class="prettyprint lang-sh">sudo apt-get install python-software-properties</pre>

## 3. Add Node.js & MongoDB repos

Node.js:
<pre class="prettyprint lang-sh">sudo apt-add-repository ppa:chris-lea/node.js</pre>

MongoDB:
<pre class="prettyprint lang-sh">
sudo echo "deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen" > /etc/apt/sources.list.d/mongodb-10gen-countly.list
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10
</pre>

## 4. Update package list once more

<pre class="prettyprint lang-sh">sudo apt-get update</pre>

## 5. Install Nginx

<pre class="prettyprint lang-sh">sudo apt-get install nginx</pre>

**Nginx** web server is used as a proxy to our API and Dashboard nodes. We will configure and start our nginx server after completing all package installations.

## 6. Install Node.js and NPM

<pre class="prettyprint lang-sh">sudo apt-get install nodejs npm</pre>

**Node.js** is our primary web server that our API and Dashboard nodes run on. **NPM** is the package manager for Node.js.

## 7. Install MongoDB

<pre class="prettyprint lang-sh">sudo apt-get install mongodb-10gen</pre>

## 8. Install Supervisor, Imagemagick, Sendmail and Build Essential

<pre class="prettyprint lang-sh">
sudo apt-get install supervisor
sudo apt-get install imagemagick
sudo apt-get install sendmail
sudo apt-get install build-essential
</pre>


**Supervisor** is the process monitor that is used to run API and Dashboard processes of Countly. If any of them die Supervisor will restart the process and keep things working. **Imagemagick** is used for processing your application icons. **Build essential** package contains necessary tools to compile some node modules and libraries Countly depends on.


## 9. Extract ZIP file

If you haven't downloaded Countly yet, [do it now](/resources/source/download-server). Copy the zip file 
in a directory that can be used to serve files (e.g /usr/local).

Extract the file:

<pre class="prettyprint lang-sh">
unzip countly-server-versionNumber.zip
</pre>

## 10. Install Node.js time module

<pre class="prettyprint lang-sh">
cd countly/api
sudo npm install time
</pre>

## 11. Create Supervisor upstart script

Create `/etc/init/countly-supervisor.conf` with the below contents;

<pre class="prettyprint lang-sh">
description     "countly-supervisor"

start on runlevel [2345]
stop on runlevel [!2345]

respawn
exec /usr/bin/supervisord --nodaemon --configuration YOUR_PATH_TO_COUNTLY/countly/bin/config/supervisord.conf
</pre>

Don't forget to change `YOUR_PATH_TO_COUNTLY` to the directory where you have extracted the Countly server ZIP package.

## 12. Create API and Dashboard configuration files

<pre class="prettyprint lang-sh">
cp countly/api/config.sample.js countly/api/config.js
cp countly/frontend/express/config.sample.js countly/frontend/express/config.js
</pre>

## 13. Start Supervisor

Supervisord starts api and app nodes that corresponds to API and Dashboard.

<pre class="prettyprint lang-sh">
start countly-supervisor
</pre>

## 14. Create frontend JS configuration from sample

<pre class="prettyprint lang-sh">
cp countly/frontend/express/public/javascripts/countly/countly.config.sample.js countly/frontend/express/public/javascripts/countly/countly.config.js
</pre>

## 15. Configure & start Nginx

Nginx default configuration file is located under **/etc/nginx/sites-enabled/default**. We will take a backup of the existing file first and add our own configuration file.

<pre class="prettyprint lang-sh">
cp /etc/nginx/sites-enabled/default /YOUR_BACKUP_DIRECTORY_OF_CHOICE
rm /etc/nginx/sites-enabled/default
vi /etc/nginx/sites-enabled/default
</pre>

And add the below contents to the file;

<pre class="prettyprint lang-sh">
server {
  listen   80;
	server_name  localhost;
	
	access_log  off;

	location = /i {
		proxy_pass http://127.0.0.1:3001;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header X-Real-IP $remote_addr;
	}
	
	location ^~ /i/ {
		proxy_pass http://127.0.0.1:3001;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header X-Real-IP $remote_addr;
	}

	location = /o {
		proxy_pass http://127.0.0.1:3001;
	}
	
	location ^~ /o/ {
		proxy_pass http://127.0.0.1:3001;
	}

	location / {
		proxy_pass http://127.0.0.1:6001;
		proxy_set_header Host $http_host;
	}
}
</pre>

*We have added a server configuration for localhost. You need to change localhost to your domain (count.ly for ex.) if you want to access your Dashboard and API from your domain.*

Save and exit from vi;
<pre class="prettyprint lang-sh">
:wq!
</pre>


Start Nginx server;
<pre class="prettyprint lang-sh">
/etc/init.d/nginx start
</pre>

## Congratulations!

You have successfully installed Countly on your server. Now go to `http://YOUR_SERVER_IP_OR_DOMAIN` in order to create your admin account and login to your dashboard.
