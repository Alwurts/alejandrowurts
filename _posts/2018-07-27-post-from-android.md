---
layout: single
title: Using Jekyll and Github from my Android Phone
categories: blogs
header: 
     overlay_image: /assets/images/teaser/desk-phone.jpg
     show_overlay_excerpt: true 
     teaser: /assets/images/teaser/iphone.jpg
excerpt: How I managed to be able to post to my website on the go. 
author_profile: true
comments: true
---

I have my jekyll static website hosted on Netlify with the deployment files hosted on a github repository, this makes for an easy way to add posts or pages if i have my computer with my prefered IDE (Currently Visual Studio); But what happends if and when im on the go and get a moment of enlightenment and decide to write something?, well one would think to go to the phone and simply write it on any notes app; What if i want to post it right away?, thats when it gets tricky there is no exact or for that matter nice way to do so instead you have to crawl your way through several apps which is not convinient at all nevertheless I went for it.

My initial approach was to get a git client on Android, as I went about my search I found out about MrHyde which does exactly what I want, sadly when looking for it on the Play Store it was nowhere to be found and when reaching out to the developers they told me they took it down in order to update the license; Hopefully they will have everything sorted out soon and we will get to try it. 

In the mean time another option I came across was Mgit, I decided to give it a try only to be somewhat disappointed, the current version has a lot of bugs in the text editor which was what I need it for, however it seems to have a lot of potential so I reccomend keeping and eye on that one.

So what I had left was using the GitHub.com webpage to upload and download my files the old way I guess; I went for it and to my surprise if you have enough patience is a somewhat acceptable method to get things done, so below its my experience using this method so far.

As mentioned before this website wich I made with Jekyll is hosted on Netlify with the deployment files hosted on a GitHub repository, the same principle of posting should work no matter if you use GitHub pages or Netlify as long as your initial deployment files are hosted in a github repository the following should work. 

So the work flow that I used goes something like this:

- If the post is new then simply create a file with an Android code editor and assign the proper name scheme for a jekyll post which is year-month-day-nameofpost.md and insert in it the proper yaml front matter for your website. To make this easier I have created a template and upload it to the cloud, when I need to write a new post I download it and modify it. 

- If it's not a new post and im simply goin to edit an old one, then I need to download the file from my GitHub repo to my phone to that matter I used OpenHub which is a GitHub viewing client, it's almost the same as opening your repository on the browser but it gives me the option of downloading individual files to my phone; Be aware that if I make changes said file outside of my phone I have to re-download the newest version of it.

- After getting the file to my phone, I simply edit it using any Android code editor, preferably it should have markdown support.  I'm using Turbo editor which works well so far.

- Extra step: If im using an image that is not in my repository, I it resize to my liking using Pixlr app for android and upload the file to the assets folder before I upload the post file.

- Once the file is ready I go to the desktop version of GitHub on a web browser and access my website repository and in this case the post folder. 

- Once I am in the correct folder I proceed to click on upload new file and select the previos created/edited file from my phone storage and commit it.

- Since I'm hosting on Netlify that's all I have to do, Netlify sees the changes to my repo and deploys my website, I dont have much experience with GitHub pages but I think the same is true. 

It's not the most convinient workflow, the hardest part is that I have to be always aware of changes I do to a certain post outside of my phone so that they are always in sync which is also a manual job.

That said, it's something I can definetely get used to until a better tool comes out (looking at you MrHyde) and I have already written and published two post which proves it can be done.
