---
layout: single
title: "Enabling comments while preserving your privacy"
excerpt: Searching for an optimal way to preserve my reader's privacy on the blog
date:  2021-04-04 08:00:00 +0100
classes: wide
categories: [en]
tags: [personal]
toc: false

header:
  teaser: /assets/images/2021/enabling-comments-preserving-privacy/privacy.jpg
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/2021/enabling-comments-preserving-privacy/privacy.jpg
  caption: "Photo credit: [Tobias Tullius](https://unsplash.com/@tobiastu?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)" 

---

Ever since I thought of putting together this blog, I have been thinking on the best approach to provide readers with the ability to comment on posts. Should I provide that option or not.

Having a static site provides several benefits but makes self-hosting of comments quite a challenge. Jekyll provides integration with several commenting systems, like Disqus or Facebook, to mention a few. But using such systems comes with a cost to the user’s privacy, with annoying and unnecessary cookies and trackers.

I strongly respect the user’s privacy on the internet, and do not feel like contributing to more online rights violation. Privacy gives us the power to choose our thoughts and feelings and who we share them with. It seems that this is already a lost battle in several fields across the web... so my requirements for my commenting system were:
* No cookies
* No ads
* No trackers

This might seem obvious to a lot of people, but frankly, it reduces the options to just a few.

Since this site is hosted on GitHub Pages, my thinking was, why not use it then to store comments as GitHub issues? The idea being, making requests to the GitHub API to publish comments and retrieve them to render them for each post.

Fortunately, some bloggers had already thought of this strategy and there are even a few Open-Source projects facilitating such integration. Thus, I have enabled comments by using [utterances](https://utteranc.es/). 

First, I had to install the utterances app on the repo to allow reading and writing of issues. Then, to comment, users must authorize the utterances app to post on their behalf using the GitHub OAuth flow. Alternatively, users can comment on the GitHub issue directly. To me, this provides the basic functionality required by a commenting system, while preserving the user's privacy. Yes, you need to have a GitHub account to submit a comment, but this might be a good thing after all. :wink:

Looking forward to reading your comments!