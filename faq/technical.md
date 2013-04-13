#Technical FAQ

##How does Countly platform work?
After your install Countly SDK in your application, users of this application start sending event data to Countly server. From these events, Countly gathers information about what they do, how they behave, which operator they are on, etc.

##Which language is Countly written with?
We are using [Node.js](http://nodejs.org/) and [MongoDB](http://www.mongodb.org/). Both backend and frontend are completely written in javascript. You can take a look at the [API code](https://github.com/Countly/countly-server/blob/master/api/api.js) which collects data from client SDKs and writes this data to database.

##How are event and session data sent to Countly?
As the user opens the application, Countly SDK starts collecting data the way you define. Events and sessions are collected and then sent to Countly (or your) servers using HTTP request every 30 seconds.

##Does Countly show my data in real-time?
All reports and charts are shown in real-time. There are no batch processes running in the background to visualize or collect data, so you don't have to wait for the next process to run.

##Will Countly slow down my mobile application?
Our lightweight SDK works asynchronously and doesn't block any function calls inside your code.

##What happens if SDK cannot send requests?
If your mobile application cannot send an event information (mainly due to the fact that device is not connected to internet, user is on a plane or underground), then this information is stored in memory. As soon as the connection is established, it's sent to the server.

##How many users can a Countly server handle?
In our tests, a decent server can handle 700 events per second, which is roughly 20.000 concurrent mobile users. See [implementation and configuration scenarios](/resources/reference/implementation-scenarios) for potential installation alternatives.

##Where should I put my Countly start code for Android? 
In as much activity as you can, preferably in each activity.

##When I compare iTunes data with Countly dashboard, I see slight difference regarding new users. What can be causing this?
Countly counts new user as unique device IDs, that is, if a user downloads the same app to iPhone and iPad, it's counted twice. Apple counts it once.

##What's the hostname I should write inside SDK when I use Countly Cloud?
You must use https://cloud.count.ly when you use our service, instead of your own server.

##How can I test my new translations and where do I put my files?
Under countly/frontend/express/public/localization there are three folders;

1. dashboard
2. help
3. pre-login

There are also three translation files on [Transifex](http://transifex.com/projects/p/countly/). In order to test your translation you can upload your translation file like dashboard_ru.properties, help_ru.properties, pre-login_ru.properties to the corresponding folder. In order to be able to switch between languages you need to edit:

1. [countly/frontend/express/views/dashboard.html](https://github.com/Countly/countly-server/blob/master/frontend/express/views/dashboard.html#L132) and add <a data-language-code="ru" class="item">Русский язык</a>
2. [login.html](https://github.com/Countly/countly-server/blob/master/frontend/express/views/login.html#L37) and add <a data-language-code="ru" class="item">Русский язык</a>

Repeat step 2 for forgot.html, setup.html and reset.html under the same folder.
