# TWAIN Cloud
Reference implementation of TWAIN Cloud specification.

[![Build Status](https://travis-ci.org/hazy-bits/twain-cloud.svg?branch=master)](https://travis-ci.org/hazy-bits/twain-cloud)

## Overview
TWAIN Cloud reference implementation includes two main components:

- [TWAIN Cloud API](https://github.com/twain/twain-cloud) (this repository)
- [TWAIN Cloud Web Frontend](https://github.com/hazy-bits/twain-cloud-web)

TWAIN Working Group and HazyBits maintain hosted version of TWAIN Cloud APIs and Web Frontend, accessible
at https://twain.hazybits.com.

## Authentication
Reference implementation relies on [serverless authentication boilerplate](https://github.com/laardee/serverless-authentication-boilerplate) to integrate with social OAuth providers. 
Facebook and Google supported out of the box, custom implementation can be added as needed. Example of the
custom OAuth provider can be found [here](https://github.com/laardee/serverless-authentication-boilerplate#custom-provider).

## Differences between public and private environment
[Travis-CI job](https://travis-ci.org/hazy-bits/twain-cloud) is configured to build and deploy 
this repository to HazyBits AWS infrastructure. This is so-called **public** deployment of TWAIN Cloud 
that is managed by HazyBits.

Alternative **private** deployments of TWAIN Cloud is possible - the process of setting up the environment
is specified below.

### AWS Account
First, you need an AWS account (you can create a free one [here](https://portal.aws.amazon.com/billing/signup))
and configured [AWS CLI tools](https://aws.amazon.com/cli/).

### Clone repository and setup dependencies
Clone the repository and install necessary dependencies using

```
npm install
```

### Update deployment settings
This repository contains two sets of deployment settings:

- ```serverless.deployment.public.yml``` - settings for public hosted version of TWAIN Cloud
- ```serverless.deployment.private.yml``` - template for alternative TWAIN Cloud deployments

You need to update ```serverless.deployment.private.yml``` by specifying the following:

- AWS IoT Endpoint for MQTT pub/sub events
- Social OAuth2 providers settings

### Deploy private TWAIN Cloud stages
It is possible to have multiple TWAIN Cloud **stages**. *Stage* is an independent copy
of the infrastructure that allows you to test changes on one stage without affecting users of another.
It is common to have  *dev* and *prod* stages.

Run the following commands to deploy TWAIN Cloud to the appropriate stage:

```
npm run deploy-dev
```
or
```
npm run deploy-prod
```

## AWS IoT Endpoint
To find out AWS IoT Endpoint for your account, go to **IoT Core** service and open **Settings** screen:

You may need to enabled IoT endpoint if it is your first time of working with IoT services.

Use the value of the endpoint to set **TWAIN_IOT_ENDPOINT** variable in deployment configuration.

## Social OAuth2 provider settings




Here is the steps:

 - Register [AWS account](https://aws.amazon.com/) and [configure CLI appropriately](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)
 - Clone TWAIN Cloud repository
 - Make the following changes in serverless.yml:
  - Set value for TWAIN_IOT_ENDPOINT variable

 - Run ```npm install``` to download all necessary dependencies
 - Run ```npm run deploy``` to build and deploy the project
 
Once deployed, you will be provided with AWS endpoints for TWAIN Cloud API methods. Use them to call the APIs directly, or configure [TWAIN Cloud Postman Collection](https://www.getpostman.com/collections/a3edceb5eeaa17e92167) to use your base URLs.
 
 
