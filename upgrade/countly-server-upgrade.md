# Upgrading Countly

Upgrading to the latest Countly Community Edition does not involve any complicated operations and you can complete it manually by following these 2 steps:

1. Extract **countly-server-vXX.YY.zip** to your previous installation directory (or do a `git pull` if you cloned the [repo from GitHub](https://github.com/Countly/countly-server)). All files & directories should be overwritten.
2. Run upgrade script `bin/upgrade.sh` under Countly folder.

The first step will overwrite all old files with new ones, and second script will restart Countly related services.
