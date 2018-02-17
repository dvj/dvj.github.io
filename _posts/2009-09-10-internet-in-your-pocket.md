---
id: 103
title: Internet in your pocket
date: 2009-09-10T22:29:03+00:00
author: dvj
layout: post
guid: http://dvjohnston.wordpress.com/?p=103
permalink: /internet-in-your-pocket/
categories:
  - Uncategorized
---
I pretty much take internet access for granted these days. It's right there on my nightstand when I wake up in the morning, groggily checking email on my iphone. It's there all day long, ready to answer any and all programming questions (and provide plenty of distraction_ while at work. It's on my lap in the evenings, bouncing around my house at 2.4GHz.

But alas, there still do exist places where the Digital Intertube Connection has not yet left it's tangled web. Trolling the far reaches of the ocean is a prime example. Of course, access is still possible via [satellites](http://www.iridium.com/), but this is still a limited (and rather expensive) proposition. [Long range radio's](http://www.winlink.org/) also offer some service, but reliving the bad old days of 2400 baud is frightening. 

So then, what is a traveler amidst the endless blue to do? Why, put the internet in their pocket of course! I've been using Google's [Web History](http://www.google.com/history) feature for a couple years now, which gives me a pretty good idea of what I use the internet for. 26,857 Google searches later, this is what my temporal usage looks like:<img src="http://107.170.213.142/wp-content/uploads/2009/09/screen-shot-2009-09-10-at-10-50-58-pm.png" alt="Google Searches" title="Google Searches" width="500" height="286" class="alignnone size-full wp-image-104" srcset="http://dvjohnston.com/wp-content/uploads/2009/09/screen-shot-2009-09-10-at-10-50-58-pm.png 847w, http://dvjohnston.com/wp-content/uploads/2009/09/screen-shot-2009-09-10-at-10-50-58-pm-300x171.png 300w" sizes="(max-width: 500px) 100vw, 500px" />
  
And in case you were wondering what my top query at 3am is: &#8220;generalized laplacian.&#8221; Sometimes you just can't sleep until you figure out a good set of laplace coefficients, am I right?

Anyway; What do I really _use_ the internet for? Well, searching google is by far the number one thing: nearly 27000 times since the middle of 2006. And that number only includes searches done while signed into Google. That works out to at least a couple dozen searches a day. 

Now, lots of times when I'm looking for information on the web, I'm looking for something that I _know_ that I've seen before. I've been to the web page, I've read the text, I just cant remember where I saw it. In a prefect world, this would be exactly what Google Web History chould be used for: take this list of web pages that I've gone to before, and run my query against _just those pages._ Unfortunately, this is not how the feature works, not even close. That's right &#8211; searching your histroy doesn't actually search your history. It doesn't even search the urls in your history. It looks over the past few weeks and returns relevant results based on your history. This sucks. So I've been forced to take matters into my own hands.

I whipped up a little python script which will log me into my Google account and download (link by link) my entire web history, as stored by Google. Trimmed down to just the URLs and page titles of sites that I've visited, this is a modest 16MB file. Now, at least I have a starting point. Now if I remember part of a url, or some of the page title I can figure out where I was. 

But lots of times I can only remember some of the text on the page. In order to search this, I need to actually be able to look through all the pages I've viewed on the internet. Well, OK, using the history file I have, this turns into a one-liner:
  
`cat webHistory.html | cut -f 2 -d '"' | grep http  | xargs -n1 -I % wget -U "Mozilla" -p -k -E %`
  
This will go out and fetch a full copy of every page I've visited. I index this using Google Desktop Search, and viola &#8211; any time I need to look for something I've seen, I can find it.

But let's do one better. I've modified the python script to grab my history up to present, and write out to file the date of the most recent item. Running the script again, it will read in that date and only gather sites that I've visited more recently than last time I ran it. Now, set this script to run daily in a cron job, followed by the wget command, and I automatically get a copy of my own personal internet, as seen through my eyes.

But what else do I use the internet for? Coming in 2nd (behind Google) in my most visited sites is wikipedia. Wikipedia is one of those truly useful sites. In fact, it's useful enough that I want it for my own. Luckily, they allow my to do just that: http://download.wikipedia.org hosts compressed images of the xml data that drives the wikimedia site, and is updated frequently (usually weekely). After downloading the 5GB article index, you can throw it into a local copy of wikimedia, and then have it write out static html files containing all of the articles on wikipedia. All told this comes out to just shy of 100GB of data in uncompressed html. While 100GB is a good chunk of data, this really is nothing when put on a 1TB harddrive, and well worth it for reference material when internet access isn't possible.