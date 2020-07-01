+++
categories = ["coursework", "web-dev"]
coders = []
date = 2019-05-01T23:00:00Z
description = "A simple social media app"
draft = true
github = ["https://github.com/samrobbins85/Progamming-REST-Coursework"]
image = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1593601766/reddit_jzxbda.svg"
title = "Slate my doggo"
type = ""
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1591793272/logos/logos_javascript_adj1dx.svg"
name = "JavaScript"
url = "https://www.ecma-international.org/memento/tc39.htm"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1593447212/nodejs-1_nrbgo0.svg"
name = "Node.js"
url = "https://nodejs.org/en/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1593601881/reddit_s5u1nb.svg"
name = "Reddit API"
url = "https://www.ecma-international.org/memento/tc39.htm"

+++
This site has a simple user interface with two buttons. The show me a random doggo button will select a random image, and the associated comments. The gimme more doggos button fetches new images using the Reddit API.

## API

A REST API was implemented to allow for interfacing with the backend. The API was implemented with three functions

### List

This is a GET request which will give you the JSON of an image with the appropriate links

### Add

This is a POST request which can be used to add new images

### Add comment

This is a POST request to allow the user to add new comments