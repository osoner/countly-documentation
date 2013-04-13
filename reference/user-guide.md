#Countly User's Guide

Countly is an innovative, real-time mobile analytics software, focusing on ease of use, extensibility and feature richness. Countly includes a server and a mobile component, both of which you can freely use in your own company for your applications under license terms.

The server part of Countly consists of a service that runs on port 80, allowing the system administrator connect to the user interface and get insights about applications tracked. The mobile part consists of SDKs for different smart phones and tables. In order to start tracking your application, you need to do the following:

1. Choose a compliant server operating system (e.g Ubuntu 10.04 or later).
2. Install the server application so it’s ready to collect data.
3. Put the SDK in your application.
4. Put the application in your mobile phone and test.
5. If tests are successful, send the application to Appstore/Google Play.

Should you feel brave enough, (4) is optional. After all steps are completed, you are ready to get insights from Countly dashboard. Installation of the server and using SDK is explained in relevant manuals, and won’t be covered here again.

# 1. Dashboard overview

Countly provides a dashboard for a quick glimpse of the latest status of application usage. There are three things you notice here.

1. Navigation bar
2. Real-time panel
3. Quick date selector
4. Analytics panel

![mobil_analiz_ekran.png](http://support.count.ly/help/assets/b7bcf5da8110be5eaede2ced7b31968ee4fca7da/mobil_analiz_ekran_normal.png)

**Note:** Real-time panel is not present in open source version.

Let’s have a look at each component.

## Navigation bar

At the top of the navigation bar, you’ll see a list of applications. Each can be selected at once, and dashboard will adopt itself showing the numbers for the selected application. Dashboard is the initial view, and Analytics menu includes several other views that can be of interest, including detailed carrier, country, user retention and session frequency metrics. User and application management is also carried out using links here.

At the bottom of this part, you can see the current user, together with a link to logout and password change option.

## Real-time panel

Have you ever wondered how many users are currently using your application at that moment? This tiny but powerful widget shows you exactly this: online users and newcoming online users. There's also a live, flowing chart on the right hand side that shows the status of your users - you can easily have an insight about whether number of online & new users are increasing and decreasing.

**Note:** This feature is only available for Countly Cloud users.

## Quick date selector

On the top right of the screen you’ll see a list of days. Here, you can either use a defined time frame, or select a date from time selector. Note that if you select a time here, it’ll be automatically selected as you click on other natigation links (e.g *Users*, *Carriers*, etc). In order to select a date, click on the selector, then start and finish dates and click on Apply. Graphs and corresponding boxed widgets will automatically be updated.

## Analytics panel

This panel gives a brief overview of what’s happening on the dashboard. On the top, there are 6 widgets. When clicked, the chart under these widgets are automatically refreshed to show relevant data group.


![mobil_analiz_ekran3.png](http://support.count.ly/help/assets/0ee015265d979ad5893fba47ec937f957bf036fb/mobil_analiz_ekran3_normal.png)


Each widget shows the following:

1. **Total sessions:** Number of times your application is opened. Click this item to see a time series representation of total sessions.
2. **Total users:** Number of unique devices your application is used from. Click this item to see a time series representation of total users.
3. **New users:** Number of first time users. Click this item to see a time series representation of new users.
4. **Time spent:** Total time spent for your application. Click this item to see a time series representation of average time spent per user.
5. **Average time spent:** Total time spent using your application divided by total user count. Click this item to see a time series representation of average time spent per user.
6. **Average requests received:** Number of write API requests Countly Server received for this application divided by total user count. Click this item to see a time series representation of average events per user.

For each time series chart, there is a light gray and dark gray line. Ligh gray line shows the previous time 
frame for comparison purposes.

For example:

* Click on 7 days and light lines will show stats between -14 days & -7 days.
* Click on Today and light lines will show stats for yesterday.
* Click on Apr and light lines will show corresponding days of March.

Below the chart, there are 4 black widgets that show the top platform (e.g Android or iOS), top resolution, top carrier as retrieved from device and top users. If you move your mouse over the line graphics here, you’ll see that data will change and show you 2nd and 3rd larges data source (if exists).

Under black widgets, there’s a colorful world map showing which countries use your application more. The greener a country is, the more your application is used in corresponding geographic area. On the left to the world map, you’ll see a list of countries (top 7) where your application is used most. Each number next to a country name shows the total number of session.

# 2. Getting in-depth analytics

Countly’s dashboard provides a quick analysis and gives a glimpse of how your application is performing. It’s mostly useful for marketing people with an intent to understand what’s going on immediately.


![mobil_analiz_ekran2.png](http://support.count.ly/help/assets/b66e5bf9ef96110866ce07b5a783196eee179fa3/mobil_analiz_ekran2_normal.png)


Navigation pane on the left gives more, detailed information about users, sessions, countries, carriers and more. Below we’ll have a look at each menu item.

## Users
Users tab is one of the most important part of the analytics. Here you’ll see an overview of total, new and returning users based on day. This is the menu you’ll need to keep track of most. This tab will give you the answer to the question *"How many users do I have?"*

## Sessions
If the user opens an application, it counts as a session until he closes it. This menu shows an overview of sessions, together with total sessions, unique sessions and new sessions, broken into time. This menu will give you the answer to the question *"How many times your application is opened?"*

## Countries
This menu gives an overview of which countries your applications are used most. Table below the world map total users, total sessions and new users. This menu will give you the answer to the question *"Where do my users connect from?"*

## Devices
In this menu, you’ll see 3 main blocks of device information. On the top, there’s a list of devices, and at the bottom, these devices are shown in a table. In the middle, there are 3 blocks of information, showing top platform, top operating system version and top resolution, respectively. Try hovering on each color line and you’ll see other top information.

This menu will give you the answer to the question "*Which smartphone types do my users have?*"

## Application versions
This page shows different versions of applications, in case they are defined. A stacked chart shows totel sessions and new users. The table under the chart shows total sessions, total users and new users, respectively for each application version. This menu will give you the answer to the question *"How do my application versions compare?"*

## Carriers
Carriers page shows a table of all carriers, together with total sessions, total users and new users for a given period. On the top of the page, there are two pie charts; showing total users and new users of top carriers. There are only 3 carriers shown in this chart for compatibility, so refer to the table for a detailed carrier breakdown. This menu will give you the answer to the question "*Which operator do they use?*"

## Platforms
Countly provides an intuitive interface to show how different platforms (operating systems) perform. If you use the same app key (Management > Applications), then it’s possible to aggregate this information and see it under this menu.

This menu will give you the answer to the question "*Which operating systems do my users have?*"

# 3. Engagement view

## User retention

Retention is condition of keeping your customers. This page shows you active days (e.g days your customer used your application) after first session. On the top right corner, you can have a breakdown of daily, weekly and monthly retention. This is one of the most important metrics for app analytics.

**Note:** User retention module is not present in open source version.

## User loyalty
User loyalty shows how many users started a specific number of sessions. Table shows number and percentage of each loyalty group compared with number of sessions (e.g one session, 2 sessions etc). This menu will give you the answer to the question *"How many users started a specific number of sessions?"*

## Session frequency
Session frequency shows how often do you see your mobile users open your application. It can be used to calculate the trend - or how often your application is used during a given period of time. The session frequency graph is very straightforward - here you’ll see a breakdown of number of sessions and corresponding number and percentage of users for each group. Most of the time, you’ll see that many users will be accumulated in “1st session” and “2nd session” row.

This menu will give you the answer to the question *"How often do you see your users open your app?"*

# 4. Events

Countly benefits from custom events. It helps product developers and user experience specialists get an understanding how how their application performs, by sending data from inside the application and analysing this information. Just like other information retrieved, custom events are true real-time with Countly, so you don't have to wait for hours for visualization to appear in dashboard.


![Screen_Shot_2012-11-13_at_22.26.47.png](http://support.count.ly/help/assets/54bbadcb38ad918501ed3be6c650b74b8e27d49c/Screen_Shot_2012-11-13_at_22.26.47_normal.png)


For more information about how to capture and send events to Countly server, see [Custom Events](/resources/reference/custom-events) article. For references and hands-on examples, please see [SDK methods for custom events](http://support.count.ly/kb/reference/sdk-methods-for-custom-events).


# 5. Managing applications & users

Countly provides a user interface to manage applications and system users.

## Managing applications

Applications can be managed by global users (more information later). To add an application, follow the steps below:

1. Go to Management > Applications
2. Click “Add”
3. Enter your application name, category, the time zone you are in, and application icon.
4. Click “Add Application”

You’ll be given an app key which is unique to that application. This key should be written in the SDK code snippet which in turn will be embedded in your application - please see SDK integration guides on how to do it.


![Screen_Shot_2012-11-13_at_22.28.51.png](http://support.count.ly/help/assets/9a89bee8ea3d8af1c3821dfa2dd7230540c4d142/Screen_Shot_2012-11-13_at_22.28.51_normal.png)


If you want to delete an application, simply click on “Delete”. There may be some cases where you only want to delete all data associated with an application, but keep the application keys and other information. In this case, use “Clear data” to remove all incoming data from this application and start fresh.

## Managing users

Countly provides a way to manage different types of users (e.g global admin, admin or user). Each user will be able to do that’s assigned to them. For example, you may want your marketing team to be able to see the whole dashboard, whereas the website manager, as the global admin, can easily add/remove applications, define other users and manage whole interface.

Different types of users have different authorization levels:

1. **Global admin** can add/remove/edit users, add/remove/edit applications and typically can do whatever is assigned them on the user interface. This is the most powerful user.
2. **Admin** can manage applications, e.g add an application, edit it or remove it completely from the management dashboard. If you are the global admin and your organization controls other sub-organizations or companies, then probably you’ll want to add different admins to manage different applications.
3. **User** is basically at the bottom of the hieararchy, and can only see the dashboard, without having the ability to manage other applications and users.


![Screen_Shot_2012-11-13_at_22.29.46.png](http://support.count.ly/help/assets/e719848587efe27463996a97f4817a5f7895c901/Screen_Shot_2012-11-13_at_22.29.46_normal.png)

In order to add a user, you must be global admin. Click “Create a new user” to have a drop-down menu where you can enter user information and credentials. Fill in the details here and click “Create user”. Editing a user is straightforward - go to the user row, and click. You’ll be presented with an editable form.

## Getting help

Countly provides inline help for users. In order to enable help mode, toggle Management > Help button. In this mode, hover on the window you want to get help about. Until you toggle the help button again, user interface autorefreshing is disabled.
