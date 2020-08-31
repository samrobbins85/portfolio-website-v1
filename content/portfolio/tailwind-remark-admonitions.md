+++
categories = ["web-dev"]
coders = []
date = 2020-08-17T23:00:00Z
description = "Alternate styling for remark admonitions"
github = ["https://github.com/samrobbins85/tailwind-remark-admonitions"]
image = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1598877402/admonition_tkwgpn.png"
site = "https://tw-remark-admonitions.vercel.app/"
title = "Tailwind Remark Admonitions"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1597140224/tailwindcss_rnpshz.svg"
name = "Tailwind CSS"
url = "https://tailwindcss.com/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1598868717/remark_y8xkpo.png"
name = "Remark"
url = "https://remark.js.org/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1597140056/next-black_csivx6.svg"
name = "Next.js"
url = "https://nextjs.org/"

+++
This was a small project I produced while working on my university notes website. The problem I was facing is that the new CSS for remark admonitions is produced with Infima, a CSS framework only used by Docusaurus. My aim was to build these same styles using Tailwind CSS, a much more popular framework, and one that allows compiling to raw CSS.

I did this for the classic style and like how they look, however I decided to move to a solution built with React components and so didn't progress to make more styles, but I may in the future.

I also created a website to display these styles using Next.js and MDX, this was very simple to set up and doesn't contain any crazy styling, but serves it's purpose and gives a good demonstration of what the different variants look like.