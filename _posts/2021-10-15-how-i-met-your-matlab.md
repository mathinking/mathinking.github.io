---
layout: single
title: "How I met your MATLAB"
excerpt: Kids, I am going to tell you an incredible story, the story of how I met your... MATLAB
date:  2021-10-15 07:00:00 +0100
categories: [en]
tags: [personal]
classes: wide
toc: false
toc_label: In this post
toc_sticky: false

header:
  teaser: /assets/images/2021/how-i-met-your-matlab/sofa.jpg
  overlay_color: "#000"
  overlay_filter: "0.1"
  overlay_image: /assets/images/2021/how-i-met-your-matlab/sofa.jpg
  caption: "Photo credit: [Call Me Fred](https://unsplash.com/s/photos/sofa?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
---

I was 16 when I first met your MATLAB. 

I remember having some math homework to do:

> _Obtain the integral of function_ ![sin(x)/x](https://render.githubusercontent.com/render/math?math=\Large{f(x)=\frac{sin(x)}{x}})

I do remember writing in my notebook:

> ![Integral of sin(x)/x](https://render.githubusercontent.com/render/math?math=\Large{\integral\frac{sin(x)}{x}dx = ?})

And that was as far as I got (on paper). 

After investing a considerable amount of time, I concluded that I could not solve this integral with the techniques that I had available. Could this be a non-integrable function? Why would our teacher give us non-solvable homework? Had I made a mistake while writing down the assignment from the blackboard?

So, after being frustrated for a while, I thought I could maybe solve it numerically. Years later, during my degree in Mathematics, I learned about Taylor series expansions, Laplace transforms, and other techniques that could help solve the definite integral.

Back to my 16 years old, I went online and started looking into tools to help me answer this puzzle. I do not remember exactly how, but I ended up surfing [MathWorks.com](http://www.mathworks.com), a +500 people (at the time) company based in Natick, Massachusetts. They were the developers of a powerful programming language and software called MATLAB:

![MathWorks - Wayback Machine](/assets/images/2021/how-i-met-your-matlab/mathworks-archive.jpg)

_MathWorks website back then. Image obtained from [The Internet Archive Wayback's Machine](https://web.archive.org/)._

I do not remember trying to download a trial license at the time. I had a friend whose brother was doing a Ph.D. in Engineering and called him to see if I could use his computer for a few hours. He said yes, and I went over to my friend's house. After spending more time than I had initially foreseen, learning how to code in MATLAB (my only coding experience was reading a few chapters of an introduction to Basic), I was ready to write a simple script to compute the definite integral. 

I have tried to find that script for this blog post. Unfortunately, after that many years, it's long gone. But I do remember, years after while studying a course in Numerical Analysis at the University, that the approximation I had made years back (between 0 and pi) was quite decent. 

Today, we could simply type:

```
>> integral(@(x) sin(x)./x, 0, pi)

ans =
    1.8519
```

Back at school, our teacher made fun of those of us who had tried to solve it, and claimed to be teaching us a lesson for the future. I never admitted having given, at least in some way, an answer to the problem. 

And that's _how I met your MATLAB_.

P.S. I still haven't figured out what the teacher thought that crucial lesson was. 