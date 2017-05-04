# Docker-sensu

## Start (aka TL;DR)
```
docker-compose up -d
```

open a browser to http://localhost:3000 or http://docker-ip:3000

## Internals

3 containers:
* Sensu-server
* Redis
* Client

Client and Server connect to Redis. 
Server contains checks [See sensu/checks ](tree/master/sensu/checks)
Client contains plugins and subscriptions [See client/client.json ](tree/master/client/client.json)


## Websites:
Sensu: https://sensuapp.org/
Sensu-plugins: http://sensu-plugins.io/
