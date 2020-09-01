+++
categories = ["web-dev", "hackathon"]
coders = ["samrobbins85", "tomnudd"]
date = 2020-08-08T23:00:00Z
description = "A tool to make setting up DMARC on Vercel easy"
github = ["https://github.com/samrobbins85/easy-dmarc"]
image = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1597139963/Logo_GCA_DMARC-removebg-preview_qjgl3w.png"
site = "https://dmarc.vercel.app/"
title = "Easy DMARC"
type = ""
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1597140162/Vercel_zgou38.svg"
name = "Vercel API"
url = "https://vercel.com/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1597140056/next-black_csivx6.svg"
name = "Next.js"
url = "https://nextjs.org/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1597140224/tailwindcss_rnpshz.svg"
name = "Tailwind CSS"
url = "https://tailwindcss.com/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1591793278/logos/logos_react_z0nqxp.svg"
name = "React"
url = "https://reactjs.org/"

+++
## About
This application sets up DMARC on your Vercel domains, and in the process also sets up SPF. In combination, these secure your domain by protecting you from fraud as it is much more difficult for people to send emails pretending to be your domain.

The impact of this for domain owners is that people won't regard emails from them as spam if criminals are sending fraudulent emails pretending to be them. Alongisde this, it ensures better delivery to other people as they can verify that the email is coming from the sender. For the wider public it reduces the amount of spam and cybercrime as there are fewer domains from which criminals can send emails.

## How it works
You log in to Vercel, and it uses the token generated from this to list your domains. You select a domain and fill out the form to specify the options you want and click submit and then two generated DNS records will be added to your domain on Vercel, these are all that is needed for DMARC and SPF.


## Tech Stack Used
Next.js, React, Vercel API, Tailwind CSS, Vercel Hosting

## How to use it
This application is hosted at dmarc.vercel.app

For local development first clone the repository using
```shell
git clone https://github.com/samrobbins85/easy-dmarc.git
```

Then move into the directory and run
```shell
npm install
```
to install it, then
```shell
npm run dev
```
to start the dev server. The application can then be found at localhost:3000

## License
This project is licensed under MIT