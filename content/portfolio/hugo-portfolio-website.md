+++
categories = ["web-dev"]
coders = []
date = 2020-06-19T23:00:00Z
description = "A portfolio website made with Hugo"
github = ["https://github.com/samrobbins85/hugo-developer-portfolio", "https://github.com/samrobbins85/portfolio-website"]
image = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1591793276/logos/logos_hugo_h2xbne.svg"
title = "Hugo Portfolio Website"
type = "post"

+++
I created my portfolio website using Hugo and UIKit, it serves as an online resume containing all my work.

This has been created as a theme so that others can use and adapt it.

## Sections

### Homepage

![Homepage Screenshot](https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1591885280/screenshot_aexm2m.png "Homepage Screenshot")

The homepage provides the basic information about you, including links to social media, skills you have, things you've done and your education. This page makes good use of UIKit grid and cards for organising all the information and ensuring it is responsive to work on mobile devices. The hackathon section of this page uses code from [https://github.com/web-tiki/responsive-grid-of-hexagons](https://github.com/web-tiki/responsive-grid-of-hexagons "https://github.com/web-tiki/responsive-grid-of-hexagons") to ensure that the hexagons tile correctly.

### About

![About Screenshot](https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1592844637/Screenshot_2020-06-22_Sam_Robbins_1_xop4uu.png "About Screenshot")

This is the page for a description about you, along with non-technical skills. This uses UIKit grid and cards in a very similar way to the homepage.

### Blog

![](https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1593263737/Screenshot_2020-06-27_Sam_Robbins_koy2no.png)

If you want to have a blog, this page will serve that purpose. I may end up changing this to a column view rather than a column view in the future, but for the present I think it looks fine.

### Portfolio

![](https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1593263791/Screenshot_2020-06-27_Sam_Robbins_1_xa3yvj.png)

This allows you to describe the projects you have created in order to showcase them to people looking at your site.

### Contact

![](https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1593263826/Screenshot_2020-06-27_Sam_Robbins_ce7qsx.png)

This provides a simple contact form which allows users of the site to send you a message. I implemented this using [https://formspree.io/](https://formspree.io/ "https://formspree.io/") as it has a generous free plan and is very simple to integrate. 