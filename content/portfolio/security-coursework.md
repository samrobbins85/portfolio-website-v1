+++
categories = ["coursework"]
coders = []
date = 2019-12-06T00:00:00Z
description = "Performing a Pentest and CTF on a Virtual Machine"
draft = true
github = ["https://github.com/samrobbins85/NS-Security-Coursework"]
image = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1598985945/undraw_safe_bnk7_dimo8p.svg"
site = ""
tech = []
title = "Security Coursework"

+++
For this coursework we were to find vulnerabilities in a system and explain how they could be mitigated, along with solving a murder mystery in the system, which required finding and decoding a range of files.

# Vulnerabilities

## Database file can be opened by any user

There was a file in the database folder named `Database.db`, this could be opened using `sqlite` and with the command `SELECT * FROM Users`, you could find personal information on the users, such as passwords.

This could simply be mitigated by not providing the file to users. Further mitigation though would be to hash passwords and redact credit card information.

## Program vulnerable to buffer overflow

There was a program that could be used to get details about a Bitcoin wallet. However the password input for this was vulnerable to buffer overflow by inserting a password of 64 characters, followed by `\0x01`, this overwrites a the variable to decide if the password is correct from 0 to 1, allowing you to see the private key.

This could be mitigated using `fgets` rather than `gets` as `fgets` allows you to limit the number of characters you take in, for example to 64.