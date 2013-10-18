#Installing Countly iOS SDK

Countly iOS SDK includes necessary tools to track your application. In order to integrate SDK to your application, follow these steps.

1. Download Countly iOS SDK.
2. Add these files to your project under Xcode: `Countly.h` `Countly.m` `Countly_OpenUDID.h` `Countly_OpenUDID.m`
3. In the project navigator, select your project
4. Select your target
5. Select the **Build Phases** tab
6. Open **Link Binaries With Libraries** expander
7. Click the **+** button
8. Select CoreTelephony.framework, select **Optional** (instead of Required)
9. *(optional)* Drag and drop the added framework to the **Frameworks** group
10. In your application delegate, import `Countly.h`
and inside `application:didFinishLaunchingWithOptions:`  add the line;
`[[Countly sharedInstance] start:@"YOUR_APP_KEY" withHost:@"http://YOUR_API_HOST.com"];` at the beginning of the function.

***Note:*** if you use Countly Cloud, you must set withHost parameter to https://cloud.count.ly for step 10.

***Note:*** Make sure you use App Key (found under Management -> Applications) and not API Key. Entering API Key will not work.


It should finally look like this:

<pre class="prettyprint">
#import "Countly.h"  // newly added line
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
[[Countly sharedInstance] start:@"TYPE_HERE_YOUR_APP_KEY_GENERATED_IN_COUNTLY_ADMIN_DASHBOARD" withHost:@"http://TYPE_HERE_URL_WHERE_API_IS_HOSTED"]; // newly added line
// your code
}
</pre>

Note: If your project uses automatic reference counting (ARC), you should disable it for the sources `Countly_OpenUDID.m`, `Countly.m` and `CountlyDB.m`:

1. Select your project
2. Select the Build Phases tab
3. Open Compile Sources tab
4. Double click `Countly.m`, `Countly_OpenUDID.m`, `CountlyDB.m` and add `-fno-objc-arc` flag

Note: Before upgrading to a new SDK, do not forget to remove the existing, older SDK from your project.
