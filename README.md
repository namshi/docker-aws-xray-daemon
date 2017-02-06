# AWS X-Ray Daemon
[![](https://images.microbadger.com/badges/image/namshi/aws-xray.svg)](https://microbadger.com/images/namshi/aws-xray)

This is aws x-ray daemon which runs in a container. This eliminates the need for running the daemon in every docker container.

## Requirement

* AWS user credential or AWS iam role with aws managed policy `AWSXrayWriteOnlyAccess`

## Running in ec2 environment with iam instance role

```
docker run -d -p 2000/udp:2000/udp \
--name aws-xray namshi/aws-xray:latest
```

## Running in non-ec2 environment or ec2 environment without iam instance role
```
docker run -d -p 2000/udp:2000/udp \
-e AWS_ACCESS_KEY_ID=aws_access_key \
-e AWS_SECRET_ACCESS_KEY=aws_secret_key \
-e AWS_REGION=aws_region \
--name aws-xray namshi/aws-xray --local-mode
```

## Sending metrics from another container to the x-ray daemon container

```
docker run -d --link aws-xray \
-e AWS_XRAY_TRACING_NAME=myapp
-e AWS_XRAY_DAEMON_ADDRESS=
-e AWS_XRAY_DEBUG_MODE="true"
myorg/myapp:latest
```


## Guide on AWS X-Ray for Java

http://docs.aws.amazon.com/xray/latest/devguide/xray-sdk-java.html

## Guide on AWS X-Ray for Node.js

http://docs.aws.amazon.com/xray/latest/devguide/xray-sdk-nodejs.html

## Guide on AWS X-Ray for .NET

http://docs.aws.amazon.com/xray/latest/devguide/xray-sdk-dotnet.html
