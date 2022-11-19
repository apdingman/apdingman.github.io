---
title: "Resource Level AWS IoT Logging"
date: 2022-04-10T22:06:15-05:00
draft: false
---
**TL;DR:** AWS recently announced the ability to configure log levels by client ID, source IP, or principal ID. See how to do it here.

Are you managing a fleet of devices on AWS IoT Core? If so, you likely know that the CloudWatch log group AWSIotLogsV2 can be your best friend for troubleshooting connectivity issues between devices and the IoT core broker. Scraping through logs in this log group can highlight some key information about the successes/failures of your device’s connectivity like seen in Figure 1.

![Figure 1](/images/image-1.png)
Figure 1

## Account-Level Logging

Most of the time, you’re only looking for messages with a log level of Error, but sometimes, you might want to see things from a little more granular view. You can subsequently flip the log level setting in IoT Core on the account level to Warning, Info, or if you’re really feeling froggy, Debug.

![Figure 2](/images/image-2.png)
Figure 2

Easy right? Right. BUT….if you have more than a couple dozen devices connecting to the broker, pumping Debug level logs into CloudWatch can get expensive FAST! I may just have a few scars from an account that had 500k+ devices in the fleet. Thankfully, there are options to help with this. However, they’re buried a little deeper than you might expect.

## Resource Level Logging by Thing Group

The option that has been around a while is to throw the things you want to increase the log level on into a thing group and set a unique log level for that thing group using the AWS CLI command set-v2-logging-level.

```shell-session
aws iot set-v2-logging-level \
  --log-target targetType=THING_GROUP,targetName=THINGGROUP1 \
  --log-level DEBUG
```

## Resource Level Logging by Client ID, Source IP, or Principal ID

What about if you just want to set the log level to debug on just a couple things without dinking around with creating and managing a thing group? **Well, in February 2022, the AWS IoT core product team delivered by announcing support for setting fine-grained logging levels using client ID, source IP, or principal ID.**

It’s quite simple to take advantage of this new capability as they baked it right into the same aws cli command set-v2-logging-level. You simply just pass a targetType of CLIENT_ID, SOURCE_IP, or PRINCIPAL_ID instead of THING_GROUP.

```shell-session
aws iot set-v2-logging-level \ 
  --log-target targetType=CLIENT_ID,targetName=THING1 \
  --log-level DEBUG
```

See here for the AWS official documentation on resource-specific logging in AWS IoT: <https://docs.aws.amazon.com/iot/latest/developerguide/configure-logging.html#fine-logging-cli>
