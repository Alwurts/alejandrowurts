---
layout: single
title: Creating my first website 
categories: blogs
header: 
     overlay_image: /assets/images/teaser/code-screen.jpg
     show_overlay_excerpt: true 
     teaser: /assets/images/teaser/code-screen.jpg
excerpt: My quest on creating my personal website alejandrowurts.com 
author_profile: true
comments: true
---

So I recently started my personal website as a way of getting my projects out in the internet as well as doing some writing about things that interest me, when looking at the options for making a website WordPress was the most popular way to go for, but the hosting that it requires was a little out of my budget, then I came across the option of using GitHub pages as a free hosting service for static websites the only downfall is that it requires a little more technical approach to making a website but me as I like to code and learn new skills I decided to dive in. 

If you don't have much experience with web page development like I do, it can seem to be little hard but with patience and plenty of hours of research I was able to get my website somewhat presentable in about 2 days of work, there is still a lot of work to be done to get it to where I want but it will eventually get there.

One option was to build the website from the ground up using html and css, but through my research I came across website builders specifically Jekyll which it's a great option with a lot of themes and plug-ins  that help you make a great looking website, another popular website builder is Hugo but for some reason or another I went with Jekyll.

After deciding on the website builder I researched free hosting options and got two options to choose from GitHub pages and Netlify, GitHub pages works out of the box with jekyll and it's a great option with some small limitations like not being able to use plug-ins. Netlify on the other hand has about everything you need for any static website and their free tier offers some great features, Thank you Netlify!. 

For both hosting instances the deployment files are hosted on a repository on GitHub. 
The normal work flow of updating the website is the next one:

- Edit or add files in a local repository on my computer. 
- Commit the files and push them to GitHub
- Netlify sees the new commit and builds my website. 

Once you have your website setup as you like adding new posts is as easy as writing them and pushing them to GitHub. 

As my experience goes if I can recommend something to someone just starting with jekyll is to choose a theme with an extensive documentation, I started to test jekyll with a theme with almost no documentations and things broke easily due to me not knowing how to use it. Currently I'm using a theme called minimal mistakes which has great documentation and I can't tell you enough how much time and frustration that saved me. 

As a final touch to bring a more professional look to my website I bought the domain alejandrowurts.com and set it as the custom domain for my website. Netlify does offer a domain but going custom is the way to go in my opinion. 

Below you can find a screenshot of the home page of my website as it looks at the time of writing this. 

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/website-screenshot.png){: .align-center}

By the way I'm very happy to tell you that this whole post including editing and adding the image was done from my android phone, if you have ever tried to use git from a phone you know is a pain in the ass but with some compromises donde I was able to find a way, more on that on another blog post. 

If you got through all this post thank you for doing so and expect more posts about technology making in general as well as the ocasional short travel blog.


