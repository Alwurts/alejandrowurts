---
layout: single
title: Using jekyll from my android phone
categories: blogs

---


Trying out if I can post to my jekyll website 
------
I have my jekyll website hosted on Netlify with the files hosted on a github repository. 

The aren't any good options for using git on Android, for jekyll there is MrHyde it at the moment of writing this is not in the playstore they are currently updating its services. 

So the work flow that I used goes something like this:

- Download a Android code editor, preferably it should have markdown support.  I'm using Turbo editor. 

- Create and edit a file with proper name for a jekyll post which is year-month-day-nameofpost.md and insert in it the proper yaml front matter for your website. To make this easier I have created a template and upload it to the cloud, when I need to write a new post I download it and modify it. 

- Once the file is ready go to the desktop version of github and access your website repository. 

- Go to your post folder and upload your file to it and commit. 

- Since I'm hosting on Netlify that's all I have to do, Netlify sees the changes and deploys mi website. 

It's not the most convinient workflow but it works and if I need to do a little more detailed work I can always edit the repo file on my computer. 
