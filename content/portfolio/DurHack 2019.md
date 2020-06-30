---
title: Durhack 2019
date: 2020-01-01T15:19:11.000+00:00
image: https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1592764375/logo19_feyze9.svg
categories:
- web-dev
- hackathon
description: A tool to help people with dementia
type: post
coders:
- samrobbins85
- tomnudd
- karina-talibzhanova
- MAGGithub1
github:
- https://github.com/tomnudd/durhack
tech:
- name: Node.js
  logo: https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1593447212/nodejs-1_nrbgo0.svg
  url: https://nodejs.org/en/
- name: MongoDB
  logo: https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1593368862/MongoDB-Logo_gq5otw.svg
  url: https://www.mongodb.com/
- name: Capital One
  logo: https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1593368806/capital-one-2_zhtqjq.svg
  url: https://www.capitalone.co.uk/
- name: Twilio
  logo: https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1593368747/twilio-2_rqhhfg.svg
  url: https://www.twilio.com/

---
![](https://res.cloudinary.com/samrobbins/image/upload/v1591793300/images/portfolio/images_portfolio_durhack2019_pyn6xr.png)

Our project was to build a tool to help people with dementia remember things, this is implemented in various ways, as described below.

### Capital One

For this, we used the Capital One API to model new transactions coming in and checking if repeat payments are being made. This is done by checking the location and cost of the payment against the previous payments. The reason why this would be useful is that for people with dementia they may forget that they have already bought things, and so buy it again, wasting money. This will allow them to save money by giving them a guess as to if they have already bought that item

### Twilio

We use Twilio to notify the person about important things they should remember. We simplified this process by creating a one-line solution to sending a message through Twilio to any phone number.

### MongoDB hosted on the Google Cloud

We store user account data on the Google Cloud and authenticate users with Auth0. The database also stores information about each user, such as their hobbies and interests, to help them retain their sense of self despite memory loss.