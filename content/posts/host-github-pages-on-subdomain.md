---
date: '2025-04-16T02:10:55+07:00'
draft: false
title: 'Host Github Pages Using Custom Subdomain!'
tags: ['tutorial']
toc: true
readTime: true
autonumber: false
math: false
showTags: false
hideBackToTop: false
---
I've spend a useless amount of time dabbling in this, the github docs are quite confusing to me so here's my summary of it, there will be a lot of images to accomodate non-native english speaker (like myself) and you will enjoy it

## Have static pages ready
Github pages only allows static pages, create it yourself or use framework like i did (i use Hugo)

## CNAME configuration
Go to your dns manager, make a new CNAME record like this:
![adding new cname record](/img/host-gh-pg/dns.png "notice the `.` at the end? yea dont forget that")
`blog` is the subdomain whereas `kkkfasya.github.io.` is the domain it points to and nope you dont need to specify the repo `kkkfasya.github.io/blog` like that, github automatically will figure it out.

Then make sure you also make one CNAME file in your root project directory and write your domain name in the first line (including the subdomain), such as this:

![cname file](/img/host-gh-pg/cname.png "ai could never draw as beautiful as this")
Then... go to github pages and just put your domain name!  

![cname file](/img/host-gh-pg/gh.png "")

## Common Misconception & SSL Error
This is one is on me, i first thought that you need to set up `A` record for your apex domain too but turns out its not! also for ssl error, try deleting the domain on github pages setting and add it again, that's what works for me.  
Enjoy your free hosting for your stupid blog with its stupid retarded opinion and tutorials, cheers!
