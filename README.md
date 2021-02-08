# Assemble data of TTN in an InFluxDB

Goal
* TTN Application defined
    * data available via MQTT
* configure telegraf
    * application and credentials (separately, if possible)
* store/log data in an InfluxDB
* grafana for visualisation
    * add config for influxdb

## Influx config

edit .env and configure usernames and passwords

## telegraf config

* config in 'telegraf/telegraf.conf', cp from telegraf/telegraf.conf.template and edit, then chmod go-rwx
    * TODO: how to include credentials from .env or other way?

you may get default config template via

    docker run --rm telegraf telegraf config 

edit 

    username = "$INFLUXDB_USER"
    password = "$INFLUXDB_USER_PASSWORD"
    username = "$YOUR_APPNAME"
    password = "$YOUR_APPKEY"

## checking connectivity

source .env
curl -G http://localhost:29080/query -u "$INFLUXDB_USER:$INFLUXDB_USER_PASSWORD" --data-urlencode "q=SHOW DATABASES"
