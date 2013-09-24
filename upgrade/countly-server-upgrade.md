# Upgrading Countly

All Countly Server packages come with an upgrade script ([/bin/countly.upgrade.sh](https://github.com/Countly/countly-server/blob/master/bin/countly.upgrade.sh)) that makes it easy to upgrade from the previous version. 

Upgrading to the latest Countly Community Edition does not involve any complicated operations 
so you can alternatively do it manually by following these 3 steps:

1. Extract **countly-server-vXX.YY.zip** to your previous installation directory (or do a `git pull` if you cloned the [repo from GitHub](https://github.com/Countly/countly-server)) 
2. Stop Countly processes `stop countly-supervisor`
3. Start Countly processes `start countly-supervisor` 
