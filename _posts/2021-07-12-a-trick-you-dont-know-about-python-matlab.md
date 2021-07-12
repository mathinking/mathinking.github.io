---
layout: single
title: "A trick you don't know about Python: MATLAB"
excerpt: Five reasons why a Python user would want to use MATLAB. A peak into my talk at Python Madrid Meetup
date:  2021-07-12 11:00:00 +0100
categories: [blog, en]
tags: [python, matlab]
classes: wide
toc: false
toc_label: In this post
toc_sticky: false

header: 
  teaser: assets/images/2021/a-trick-you-dont-know-about-python-matlab/trick.jpg
  overlay_color: "#000"
  overlay_filter: "0.3"
  overlay_image: assets/images/2021/a-trick-you-dont-know-about-python-matlab/trick.jpg
  caption: "Photo credit: [AbsolutVision](https://unsplash.com/@freegraphictoday?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
  
---

In the last couple of years at MathWorks, I have been working mainly in machine learning & friends (deep learning, reinforcement learning, etc.) and integrating languages with MATLAB (frequently bringing servers or the Cloud into the equation). In the topic of programming languages integration, I'd like to expand on some ideas I recently shared in the [Python Madrid](https://www.meetup.com/es/python-madrid/) meetup, where I recently delivered the talk: 

[**A trick you don't know about Python: MATLAB**](https://www.meetup.com/python-madrid/events/278296241/)

Over these years, I have met a lot of people in the open-source community. Interestingly, the organizers of [Python Madrid](https://www.meetup.com/es/python-madrid/)  got interested in the integration of Python and MATLAB together.

It's worth noting that these communities do have more in common than what people may think in the first place, and, as I stated in the abstract of the talk: 

> The world is not so simple as to be divided between Pythonists and MATLABers

One of the most significant challenges in software development is integrating different technologies or product stacks efficiently, streamlining development, and facilitating collaboration between teams. In this sense, MATLAB provides flexible, bi-directional integration with many programming languages, including Python. This integration allows different teams to collaborate, integrate their developments, and take them to production regardless of their programming language preference.

Why would a Python user want to use MATLAB? After some exciting discussions with my colleagues [Yann](https://www.linkedin.com/in/yann-debray-70305026) and [Mike](https://twitter.com/walkingrandomly), we narrowed them down to the following:

![Why call MATLAB from Python?](/assets/images/2021/a-trick-you-dont-know-about-python-matlab/reasons.png)

Following this post, I will be sharing other posts to exemplify each of these reasons. **Stay tuned and navigate to these posts below for more details:**

- [X] [Need to integrate MATLAB code from a colleague](../../../blog/en/a-trick-you-dont-know-about-python-matlab-integrate)
- [ ] Facilitate development by using a simplified workflow
- [ ] Need functionality only available in MATLAB (e.g. Simulink)
- [ ] Want to validate conclusions by running equivalent MATLAB code
- [ ] Leverage the work from the MATLAB community

Also, you may revisit the slides: 

<div>
  <div style="position:relative;padding-top:56.25%;">
    <iframe src="https://content-mathworks.highspot.com/viewer/60c31bd0659e935e6f4086a5?iid=60bf49ba628ba20f9d8a747e" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen
      style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
  </div>
</div>

and the presentation from June 3rd (in Spanish):

{% include video id="qh8sgV36KZo" provider="youtube" %}

If you want to discuss your workflow or have feedback on integrating MATLAB and Python, feel free to post a comment in the section below or reach out to me! 