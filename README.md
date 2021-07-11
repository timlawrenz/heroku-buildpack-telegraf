# heroku-buildpack-telegraf

Based on [Skrud work](https://github.com/skrud/heroku-buildpack-telegraf)

A simple heroku buildpack to download, deploy and launch Telegraf on your dynos.

This buildpack downloads the latest Telegraf release (at the time of writing, 1.19.0), extracts it on your dyno and starts it via a .profile.d script.

You can use this buildpack for other observability platform, just change the output in the config.

## Installation
Download [this telegraf.conf](telegraf.conf) to your app's home directory and run the following commands:

    heroku labs:enable runtime-dyno-metadata -a <<your-app-name>>
    
    heroku config:set LOGZIO_LISTENER=https://<<LOGZIO_LISTENER>>:8053   
    
    heroku config:set LOGZIO_TOKEN=<<LOGZIO_METRIC_TOKEN>>
    
    
Then add the buildpack to the list of heroku buildpacks:

    heroku buildpacks:add --index 1 https://github.com/logzio/heroku-buildpack-telegraf.git
    
    git commit --allow-empty -m "Rebuild slug"
    
    git push heroku master
    
Wait a few seconds and you will see your dyno system metrics in Logz.io platform


