#Installing Countly Android SDK

Installing Android SDK requires two very easy steps. Countly Android SDK uses OpenUDID (which comes ready with the zip file). First you need to make sure that OpenUDID requirements are met, following the steps below:

###1. Add this to your manifest:

* Add OpenUDID_manager.java and OpenUDID_service.java to your project under Eclipse.

<pre class="prettyprint">
&lt;service android:name=&quot;org.openudid.OpenUDID_service&quot;&gt;
    &lt;intent-filter&gt;
        &lt;action android:name=&quot;org.openudid.GETUDID&quot; /&gt;
    &lt;/intent-filter&gt;
&lt;/service&gt;</pre>

###2. Add main Countly SDK to your project using steps below:

* Add Countly.java to your project under Eclipse.
* Call `Countly.sharedInstance().init(context, "https://YOUR_SERVER", "YOUR_APP_KEY")` in onCreate, which requires your App key and the URL of your Countly server (use `https://cloud.count.ly` for Countly Cloud).
* Call `Countly.sharedInstance().onStart()` in onStart.
* Call `Countly.sharedInstance().onStop()` in onStop.

Additionally, make sure that *INTERNET* permission is set if there's none in your manifest file.

**Note:** Make sure you use App Key (found under Management -> Applications) and not API Key. Entering API Key will not work. 

**Note:** You need to call methods in "onCreate, onStart and onStop" events only for main activity.
