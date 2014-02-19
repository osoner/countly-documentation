##Installing Countly iOS SDK

Countly iOS SDK includes necessary tools to track your application. In order to integrate SDK to your application, follow these steps.

1. Download Countly iOS SDK (or clone it in your project as a git submodule).
2. Add these files to your project under Xcode: `Countly.h` `Countly.m` `Countly_OpenUDID.h` `Countly_OpenUDID.m` `CountlyDB.h` `CountlyDB.m` and `Countly.xcdatamodeld`
3. For an OS X target, skip to step 11. For iOS, continue with step 4.
4. Select your project in the Project Navigator
5. Select the **Build Phases** tab
6. Open **Link Binaries With Libraries** expander
7. Click the **+** button
8. Select CoreTelephony.framework, select **Optional** (instead of Required)
9. Select CoreData.framework
10. *(optional)* Drag and drop the added framework to the **Frameworks** group
11. In your application delegate, import `Countly.h`
and inside `application:didFinishLaunchingWithOptions:`  add the line;
`[[Countly sharedInstance] start:@"YOUR_APP_KEY" withHost:@"https://YOUR_API_HOST.com"];` at the beginning of the function.

**Note:** If you use Countly Cloud, you must set withHost parameter to https://cloud.count.ly for step 11.
Or you can use `[[Countly sharedInstance] startOnCloudWithAppKey:@"YOUR_APP_KEY"];` directly.

**Note:** Make sure you use App Key (found under Management -> Applications) and not API Key or App ID. Entering API Key or App ID will not work.

It should finally look like this:

<pre class="prettyprint">
#import "Countly.h"  // newly added line
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
[[Countly sharedInstance] start:@"TYPE_HERE_YOUR_APP_KEY_GENERATED_IN_COUNTLY_ADMIN_DASHBOARD" withHost:@"http://TYPE_HERE_URL_WHERE_API_IS_HOSTED"]; // newly added line
// your code
}
</pre>

**Note**: If your project uses automatic reference counting (ARC), you should disable it for the sources `Countly.m`, `Countly_OpenUDID.m` and `CountlyDB.m`:

1. Select your project
2. Select the **Build Phases** tab
3. Open **Compile Sources** tab
4. Double click `Countly.m`, `Countly_OpenUDID.m` and `CountlyDB.m` and add `-fno-objc-arc` flag

**Note**: Before upgrading to a new SDK, do not forget to remove the existing, older SDK from your project.