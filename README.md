# README #

A serverless lambda that ships cloudwatch logs to sumologic.
This is a deployment specific implementation of
https://github.com/SumoLogic/sumologic-aws-lambda/tree/master/cloudwatchlogs

### How do I get set up? ###

Firstly you must create a hosted collector on sumologic. A hosted collector
is the endpoint for where logs are shipped to and determines how incoming
logs are classified. See
https://help.sumologic.com/Send-Data/Sources/02Sources-for-Hosted-Collectors/HTTP-Source

This variable must be set into the environment as SUMO_ENDPOINT=.

### Adding Logs to reporting

All the logs that flow through this lambda are going to be reported to the same
sumologic endpoint and so will be classified as the same sumologic
\_sourceCategory. Because of that if you wish to group specific lambda logs
together you should look at deploying another lambda.

To add another endpoint you must tell serverless to respond to the event. To do
this we add an entry like:

  - cloudwatchLog: /aws/lambda/my-function-to-monitor

To the function.

### How do I deploy ###

* add AWS credential in .aws/credential
* npm install
* set environment variable SUMO_ENDPOINT=YOUR_HTTP_COLLECTOR_ENDPOINT and CLOUDWATCH_LOG=/aws/lambda/my-function-to-monitor
* run serverless deploy -v inside Serverless service directory (sumologic)


edited by Jamie and Ray
