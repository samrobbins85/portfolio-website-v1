+++
categories = ["coursework", "python"]
coders = []
date = 2019-12-06T00:00:00Z
description = "Creating a bulletin board using Python socket programming"
github = ["https://github.com/samrobbins85/NS-Networks-Coursework"]
image = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599477038/undraw_messages1_9ah2_qjfjxw.svg"
site = ""
title = "Bulletin Board"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1598898170/Python_logo_and_wordmark_hi8qjl.svg"
name = "Python"
url = "https://www.python.org/"

+++
This coursework was to implement a client-server system for a simple anonymous bulletin board system using TCP.

This system makes heavy use of the `socket` Python library for communicating between the client and server.  There is also a large amount of error checking involved to ensure that commands can be properly executed.

## Error checking

The following errors were checked for

* Unavailable/busy port
* No message boards defined
* Specified board doesn't exist
* Invalid message

## Logs

The server program keeps logs of every request it receives during all client-server communication