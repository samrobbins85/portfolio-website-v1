+++
categories = ["web-dev"]
coders = []
date = 2020-09-03T23:00:00Z
description = "A website to compare DNS services"
github = ["https://github.com/samrobbins85/dns-comparison"]
image = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599384587/undraw_connected_world_wuay_brt5oo.svg"
site = "https://dns-compare.vercel.app/"
title = "DNS Comparison Website"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1597140056/next-black_csivx6.svg"
name = "Next.js"
url = "https://nextjs.org/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599384876/chartjs_bbnev1.svg"
name = "ChartJS"
url = "https://www.chartjs.org/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599384797/57233884-20344080-6fe5-11e9-8df3-0df1282e1574-removebg-preview_lmdhtx.png"
name = "Axios"
url = "https://github.com/axios/axios"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1597140224/tailwindcss_rnpshz.svg"
name = "Tailwind CSS"
url = "https://tailwindcss.com/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599472937/logo-light-66d4dd9109004332c863391e6d1cb309_a5sijd.svg"
name = "React Table"
url = "https://react-table.tanstack.com/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599385171/quad9-ar21_pvbbxd.svg"
name = "Quad9"
url = "https://www.quad9.net/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599385202/Cloudflare-logo-vector_vuznng.svg"
name = "Cloudflare DNS"
url = "https://www.cloudflare.com/dns/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599385236/google_j1hisv.svg"
name = "Google DNS"
url = "https://developers.google.com/speed/public-dns"

+++
This site compares the performance of different DNS services. It does this in a range of ways, depending on your requirements.

## Single domain comparison

The homepage allows you to compare a single domain to see if it is resolved on different services. To do this it makes DNS over HTTPS requests using Axios, with a modifier to also include the latency.

![](https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599472461/homepage_urjka3.png)

## Bulk domain comparison

If you have a list of domains you want to compare, then the above method may become tedious as you have to type in every domain and check the results. To solve this problem, I created a page for bulk comparison. This uses the same method as the single comparison but in parallel to make a lot of requests.

This uses Chart.js for the data visualisation and react-table for the paginated table.

![](https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599472616/Screenshot_2020-09-07_Bulk_Upload_DNS_Comparison_ik2lb8.png)

## Server generated results

While the bulk comparison is good for small amounts of domains, when the number gets larger you'd be waiting hours to get a result. To solve this, results based on open source datasets are processed on a server, which you can then view in the website. 

This uses papaparse to parse in a CSV and Chart.js for the data visualisation

![](https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599472803/Screenshot_2020-09-07_Server_Generated_Results_DNS_Comparison_ztf5hc.png)