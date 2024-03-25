# heroku-buildpack-telegraf

Based on [Skrud work](https://github.com/skrud/heroku-buildpack-telegraf)

A simple heroku buildpack to download, deploy and launch Telegraf on your dynos.

This buildpack downloads the latest Telegraf release (at the time of writing, 1.29.5), extracts it on your dyno and starts it via a .profile.d script.

You can use this buildpack for other observability platform (which support telegraf agent), just change the output in the config.

## Installation
From your heroku git directory download [this telegraf.conf](https://raw.githubusercontent.com/logzio/heroku-buildpack-telegraf/master/telegraf.conf).

    wget -O telegraf.conf https://raw.githubusercontent.com/logzio/heroku-buildpack-telegraf/master/telegraf.conf

## Enable enviroment variable

Repelace the following with the relevant paramters:

| Variable | Value |
|---|---|
| <<HEROKU_APP_NAME>> | your heroku app name (for example obscure-earth-56999 ) |
| <<LOGZIO_LISTENER>> | your Logzio listener (for example listener.logz.io )|
| <<LOGZIO_METRIC_TOKEN>> | your Logzio metrics token |
    
and run the following commands inside your heroku app directory:

    heroku labs:enable runtime-dyno-metadata -a <<HEROKU_APP_NAME>>
    
    heroku config:set LOGZIO_LISTENER=https://<<LOGZIO_LISTENER>>:8053   
    
    heroku config:set LOGZIO_TOKEN=<<LOGZIO_METRIC_TOKEN>>
    
    git add .
    
    git commit -m "Telegraf config" 
    
    git push heroku main
    
Then add the buildpack to the list of heroku buildpacks:

    heroku buildpacks:add --index 1 https://github.com/logzio/heroku-buildpack-telegraf.git
    
    git commit --allow-empty -m "Rebuild slug"
    
    git push heroku main
    
Wait a few seconds and you will see your dyno system metrics in Logz.io platform


