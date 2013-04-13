#Installing Countly BlackBerry WebWorks SDK

Installing Countly BlackBerry WebWorks SDK is very easy. First you need to 
add some tags to your config.xml file (as shown below), to reach the phone's 
private data; such as PIN number, OS version etc. Use your server URL below instead of cloud.count.ly 
if you are hosting your own Countly server.

<pre class="prettyprint">
&lt;access uri="https://cloud.count.ly" subdomains="true" /&gt;
&lt;feature id="blackberry.identity" /&gt;
&lt;feature id="blackberry.system" /&gt;
&lt;feature id="blackberry.app" /&gt;
&lt;feature id="blackberry.app.event" /&gt;
</pre>


Then you just need to copy jQuery library and CountlyApi.js to your project path. 
After that, Include the jQuery library and CountlyApi.js as shown below to your html file; 
which you defined as content src in your config.xml file.

<pre class="prettyprint">
&lt;head&gt;
    &lt;script type="text/javascript" src="jquery.js"&gt;&lt;/script&gt;
    &lt;script type="text/javascript" src="CountlyApi.js"&gt;&lt;/script&gt;
&lt;/head&gt;
</pre>

Next, define your countly server url and your app_key before you initiliaze your 
Countly BlackBerry WebWorks SDK, as shown below.

<pre class="prettyprint">
countly.setURL('http://cloud.count.ly') ;
countly.setAppKey('YOUR_APP_KEY');
</pre>

PS: In the URL part above, use your server URL if you are hosting your own Countly server.

Now you are ready to initialize your Countly BlackBerry WebWorks SDK (as shown below). 

<pre class="prettyprint">
countly.init();
</pre>

When Countly BlackBerry WebWorks SDK initializes, it will start session and send your phone 
data to the Countly server automatically. Now just you need to do is define your special events (shown below).

<pre class="prettyprint">
countly.eventSender('testevent');
countly.eventSender('testevent', 1.3, {'mykey' : 'myvalue'});
</pre>

In the first example the eventSender method just creates an event named 'testevent' and 
sends that event to the server if the loop size and session duration conditions are satisfied.
In the second example; we are giving some specific information about our event, such 
as 'sum' and 'segment'. If you want to learn more about these optional parameters, 
[you can check out this address](/resources/reference/server-api).

All you need to do is defining your event, nothing more. You don't need to care about 
things like ending your session or closing link with Countly server. Your Countly BlackBerry WebWorks SDK 
does the heavy work for you.

##Known issues
It's not possible to retrieve carrier name using BB SDK for WebWorks, so this code always returns "Carrier" for carrier name.
