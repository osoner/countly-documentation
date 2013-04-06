#Installing Countly Android SDK

Installing Android SDK requires two very easy steps. Countly Android SDK uses OpenUDID (which comes ready with the zip file). First you need to make sure that OpenUDID requirements are met, following the steps below:

###1. Add this to your manifest:


<pre class="prettyprint">
&lt;service android:name=&quot;org.openudid.OpenUDID_service&quot;&gt;
    &lt;intent-filter&gt;
        &lt;action android:name=&quot;org.openudid.GETUDID&quot; /&gt;
    &lt;/intent-filter&gt;
&lt;/service&gt;</pre>

2. Call `void OpenUDID_manager.sync(Context yourContext);` to initialize the OpenUDID
3. Call `boolean OpenUDID_manager.isInitialized();` to check if the initialization is over (it's asynchronous)
4. Call `String OpenUDID_manager.getOpenUDID();` to retrieve your OpenUDID

###2. Now it's time to add main Countly SDK to your project using steps below:

* Add Countly.java to your project under Eclipse.
* Call `Countly.sharedInstance().init(..)` in onCreate.
* Call `Countly.sharedInstance().onStart()` in onStart.
* Call `Countly.sharedInstance().onStop()` in onStop.

Additionally, make sure that *INTERNET* permission is set if there's none in your manifest file.

**Note:** You need to call methods in "onCreate, onStart and onStop" events only for main activity.