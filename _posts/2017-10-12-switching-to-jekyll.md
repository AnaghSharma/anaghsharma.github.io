---
layout: post
title: Switching to Jekyll & GitHub Pages
author: Anagh Sharma
read-time: 3m 55s
permalink: '/blog/switching-to-jekyll-and-github-pages/'
---

###### **OVERVIEW**
Ever since I decided to become a professional designer, I wanted to have a personal website where I could share my work and other life experiences. After several iterations, I recently launched my revamped website which is powered by Jekyll and Github pages. Before this I was using Wordpress as the platform but I had a lot of problems while working on it.

<br>
###### **WHY I SWITCHED?**
I started to shape up my website in the beginning of 2016. I asked one of my classmates to help me building it up. Due to our limited front-end knowledge we couldn’t build anything useful. After trying a lot and getting frustrated, I thought of using Wordpress to build my website. I did not want to code and wanted to set up the website with little effort as possible. I paid for the not so expensive domain and hosting.

<br>
Setting up the website was not that of a task. I set up the home page in a couple of days. I wanted to add more pages that I had in mind but adding more pages with same visual theme was cumbersome. Also, I wanted to write and publish a blog but then again I couldn’t have custom blog design matching the overall visual appearance of my website (maybe we can’t do it or I was not able to find out how to do it).

<br>
To summarise why I shifted from Wordpress to Jekyll & Github Pages- 
1. Domain and hosting are free with GitHub pages so you can basically set up a website without spending a dime.
2. With Jekyll, I have more power on the visual design. I am able to reuse a lot of layouts in order to avoid repetition. If I want to add a project case study, I can simply use the case-study layout. No need to create pages from scratch.
3. With Jekyll, I am easily able to maintain my blog. I set up a page to list all articles and a layout to show a specific article. If I want to publish a blog post, I would just add a markdown file and start writing. It is as easy as it gets.
4. To update assets and validate them, I do not have to upload media to a server again and again. Just update them locally and check if you are good to go.

<br>
###### **THE HOW**
I had not done any development work for a long time (The last time I developed and launched something was in October 2014). So I had to face a couple of problems in the beginning. I was asked to learn front-end at work, Foundation framework to be specific. I started learning it only to realise that I can’t learn it without working on a real project. Since I had been having a lot of problems with my Wordpress based website, I decided to pick it up and work on it as the project to learn.

<br>
After a little bit of research, I got to know about Jekyll and Github pages. The last time I had tried to use Jekyll was in 2013 when I knew almost nothing about it. I did a thorough research this time, compared the pros & cons and decided to stick with them. Using Jekyll and Github pages to set up a basic website is pretty easy and hardly takes 15 minutes to do so. Now the problem was - how to use Foundation with Jekyll. I had negligible experience working in front end. To my luck, I found a guide on GitHub which helped me set up everything required for the development (after a couple of tries of course).

<br>
In between the development I realised that adding paddings and margins in css classes were ceasing their reusability. I wanted to use a modular approach and that is when I found Tachyons - a css framework. Adding padding and margin decoupled from everything made life easier. Now I can directly alter an element’s margin and padding from HTML, no need to add a property in a css class.

<br>
Deploying the website is no rocket science - you just push your changes to the `master` branch of your repo. That’s it and your changes will be live within a couple of minutes. 

<br>
Working with blog posts is easier too. You create a `_posts` folder and add your posts in that folder in the format of `year-month-day-title.format`. Following this format is necessary in order for Jekyll to recognise them as articles. 

<br>
All in all, Jekyll and Github Pages fit into my requirements of updating the website without complications and hosting it.