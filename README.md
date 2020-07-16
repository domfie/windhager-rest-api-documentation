# Windhager Webserver Touch (RC 7030)
Documentation of the rest functionality of the windhager mesinfinity webserver RC7030 (integrated in the biowin boiler). (Windhager, MesInfinity and InfoWIN are registrated trademarks of the Windhager Zentralheizung GmbH Deutschland)
API-Docs (Swagger 1.2!) available under http://rc7030-ip/api-docs

Open Ports:
- 22 SSH with key auth
- 80 Apache
- 111 Portmapper

Each API-Endpoint has an info and settings endpoint. The info endpoint returns the version of the queried endpoint, the settings endpoint the settings like database location etc.

## APIs
- DcmRC7030
- InfoWinFehlerlog
- InfoWinHeartbeat
- RestApiRC7030
- WsAdmin
- WsFUP7030
- dprecorder

### DcmRC7030
  
According to api-docs this is the datapoint recorder API
It lets you PUT messages in the format 1025 into the recorder.
I guess it is used to create measurement points for the logger from external applications

### InfoWinFehlerlog
This endpoint lets you view errors and post errors to the log

### InfoWinHeartbeat
This endpoint gives information about the heartbeat between the control and the burner

### RestApiRC7030
All settings which are accessible via the panel, retrieve datapoints etc

- config
- datapoint
- datapoints
- dynip
- lookup
- nodes
- object
- scan
- user
- vpn

### WsAdmin
Endpoint for triggering firmware updates, set systemtime and user credentials. Also lookup led status which are no longer assembled on the touch display but were assembled on the RC7030

- led
- systemtime
- update
- user

### WsFUP7030

Firmware update processor?

- LON
- config
- hwtest
- info
- led
- lonscan
- notification
- settings
- srv0620
- srv0621
- srv0622
- srv0623
- srv1024
- srv1025
- windyndata
- winservice

### dprecorder
Lets you define oid to be recorded

/datalog/

## How to query / change values (datapoints)

### Query values
- Get request
- Digest Auth
- Default username: Service
- Default password: 123
- If connected to Windhager APP, the password is visible under advanced settings
- OID of value can be read out in the webinterface

![](windhager.png)

Example:
http://Service:123@192.168.1.104/api/1.0/lookup/1/15/0/3/21/0


### Change values
- Put request
- JSON Body
- Digest auth
- Username same as query

Example:  
#!/bin/bash  
curl --request PUT http://192.168.1.104/api/1.0/datapoint --digest --user Service:123 --data-raw "{\"OID\":\"$1\",\"value\":\"$2\"}"

## Read more (german)
https://www.mikrocontroller.net/topic/353671
