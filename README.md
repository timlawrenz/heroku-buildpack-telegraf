# WIP - shouldnt be used

# heroku-buildpack-telegraf

Based on [Skrud work](https://github.com/skrud/heroku-buildpack-telegraf)

A simple heroku buildpack to download, deploy and launch Telegraf on your dynos

This buildpack downloads the latest Telegraf release (at the time of writing, 1.19.0), extracts it on your dyno and starts it via a .profile.d script.

## Installation
Download the telegraf.conf to your app's home directory.


Then add the buildpack to the list of heroku buildpacks:

    heroku buildpacks:add --index 1 https://github.com/logzio/heroku-buildpack-telegraf.git


