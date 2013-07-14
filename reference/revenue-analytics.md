#Revenue analytics

Countly now has revenue analytics for tracking your in-app-purchase revenues. Information you will get from revenue analytics will be;

- Total revenue 
- Avg. revenue per user
- Avg. revenue per paying user 
- Paying user count
- Paying/total users

There are two steps to start using revenue analytics right away;

## 1. Define an iap event

In order to make revenue analytics simple to use as always, we made the process pretty straightforward. There are two ways to define an event as the **in-app-purchase event**.

You can type in the iap event key while creating or editing your app;

<img src="/images/resources/revenue/app_edit.png" />

Or if you already have data for the event you plan to use as the iap event, you can choose it from event management popup;

<img src="/images/resources/revenue/events_edit.png" />

## 2. Sit back and enjoy

Well, first step was pretty much all you had to do in order to use revenue analytics. Payment data will be retrieved from the `sum` property of your selected event. We will record the paying user counts based on the users who perform your **iap-event**.

<img src="/images/resources/revenue/iap_data.png" />

<img src="/images/resources/revenue/dashboard_data.png" />