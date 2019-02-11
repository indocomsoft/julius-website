---
title: "Fluminus"
date: 2019-02-11T23:56:24+08:00
author: "Julius Putra Tanu Setiaji"
tags:
  - reverse-engineering
---
Some of you may have realised that I wrote a files downloader for the brand-new LumiNUS. Check it out [here](https://github.com/indocomsoft/fluminus) if you haven't!

So, just like most entities with an old full-stack website, NUS has decided to upgrade its LMS (Learning Management System) from the full-stack IVLE to the separate frontend-backend LumiNUS! All new and shiny!

At that time, I wasn't excited by this since IVLE worked just fine, and I just wrote [NUSIVLEBot](https://github.com/indocosmoft/NUSIVLEBot), a telegram bot for push notification of announcements on IVLE. Many people in the NUS School of Computing would know about (and have even used) the [IVLE LAPI](https://wiki.nus.edu.sg/display/ivlelapi/Home). My NUSIVLEBot [consumed it](https://github.com/indocomsoft/nusivlebot/blob/master/lib/api.js), the backend for Source Academy that I was involved in [used it](https://github.com/source-academy/cadet/blob/master/lib/cadet/accounts/ivle.ex), and so does [ivle-sync](https://github.com/goweiwen/ivle-sync), a script to automatically download files from IVLE.

I was quite assured back [in February 2018](https://wiki.nus.edu.sg/pages/viewpage.action?pageId=204506221&navigatingVersions=true) when I checked the LumiNUS API page, which promised the release of "Powerful RESTful API documentation on Swagger" by **March 2018**.

[![First Promise](/blog/201901-fluminus/api-feb.png)](/blog/201901-fluminus/api-feb.png)

When March 2018 arrived, they [updated the page](https://wiki.nus.edu.sg/pages/viewpage.action?pageId=211977749&navigatingVersions=true) to change the release date to **April 2018**.

[![Second Promise](/blog/201901-fluminus/api-mar.png)](/blog/201901-fluminus/api-mar.png)

May 2018 came and went, but nothing was released. Then in June 2018, they [again updated the page](https://wiki.nus.edu.sg/pages/viewpage.action?pageId=223186317&navigatingVersions=true) to change the release date to **August 2018**.

[![Third Promise](/blog/201901-fluminus/api-jun.png)](/blog/201901-fluminus/api-jun.png)

Hmm, how convenient.

![big thonk](/blog/201901-fluminus/bigthonk.gif)

And then on October 2018, apparently they just [gave up](https://wiki.nus.edu.sg/pages/viewpage.action?pageId=227163074&navigatingVersions=true).

[![No Promise](/blog/201901-fluminus/api-oct.png)](/blog/201901-fluminus/api-oct.png)

Meanwhile, the timeline given by NUS CIT is for partial phaseout of IVLE in AY2018/2019 with LumiNUS in beta, and full transition to LumiNUS in AY2019/2020. I released that if I were to wait for full API, I may not have time to actually implement things that I want to implement. So one random day in AY2018/2019 Semester 2 I just decided to reverse-engineer the IVLE API and build something similar to `ivle-sync`.

So I opened LumiNUS, and was promptly greeted with this announcement:

[![LumiNUS Slowness](/blog/201901-fluminus/luminus-slow.png)](/blog/201901-fluminus/luminus-slow.png)

> The root cause is deep-seated.

Heh. Just as I suspected, they did not write LumiNUS to be greatly scalable, probably with some O(n^2) or O(n^3) algorithm inside somewhere, calling the performance good enough for 10-20 people, and then deploying LumiNUS for all 40,000+ students in NUS. When I consistently get >5 seconds response time, it is clear that there's something wrong with LumiNUS' design.

[![LumiNUS Slowness Proof](/blog/201901-fluminus/luminus-slow-proof.png)](/blog/201901-fluminus/luminus-slow-proof.png)

Rants aside, I started the process of reverse-engineering by looking at the source code. Apparently it's just an empty HTML page with scripts, so clearly everything in client-rendered. A quick search in the main javascript bundle revealed that the frontend was written using Angular.

[![Angular](/blog/201901-fluminus/angular.png)](/blog/201901-fluminus/angular.png)

Also interestingly, the main bundle is not minified at all. So I switched from Firefox to Chrome since the latter can actually read sourcemaps. And, voila! I can now see the webpack-transpiled code for LumiNUS.

[![Source map](/blog/201901-fluminus/sourcemap.png)](/blog/201901-fluminus/sourcemap.png)

When going through the source code, I found this gem.

[![Environment](/blog/201901-fluminus/environment.png)](/blog/201901-fluminus/environment.png)

I did not really check what I can do with the YouTube API key, but I would assume that I will not be able to do much about it. However, I became quite intrigued at what `verso` is. So I googled with the term "luminus verso", and found [this company](https://verso.digital/) to whom NUS CIT has outsourced LumiNUS to. Sigh. I guess this is why LumiNUS is so bad, with slow backend and bad UI and UX for frontend. I might make another post in the future about how awful LumiNUS frontend UI and UX is. I wonder if Verso even has any designer in their team because the location and animation of everything seems like they were decided by the roll of a dice.

TBC.
