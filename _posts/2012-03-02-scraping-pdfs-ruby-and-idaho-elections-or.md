---
id: 1292
title: 'Scraping pdfs, Ruby and Idaho elections, or &#8230;'
date: 2012-03-02T13:18:02-07:00
author: Nathaniel Hoffman
layout: post
guid: http://www.paleomedia.org/?p=1292
permalink: /2012/03/02/scraping-pdfs-ruby-and-idaho-elections-or/
aktt_notify_twitter:
  - 'no'
dsq_thread_id:
  - "596517892"
image: /wp-content/themes/tma/images/mapsample-437x198.jpg
categories:
  - Features
  - Journalism 2.0
tags:
  - Ben Ysursa
  - Brett Nelson
  - elections
  - Google
  - Idaho
  - journalism
  - Kevin Richert
  - Maps
---
&#8230; why I am never going to be a programmer. Last week I saw several reporters tweeting about checking the Idaho Secretary of State&#8217;s Election&#8217;s page throughout the day so as not to miss any new candidate filings during the current Idaho elections filing period.

https://twitter.com/KevinRichert/status/174613454685081600

I feel for Kevin and the rest of the Idaho Capitol Press Corps. While the Secretary of State does make a good effort to provide public information, and Secretary of State Ben Ysursa has been a champion of public records, there has got to be a better way.

<figure id="attachment_1307" aria-describedby="caption-attachment-1307" style="width: 248px" class="wp-caption alignright">[<img loading="lazy" src="http://www.paleomedia.org/wp-content/themes/tma/images/mapsample-248x300.jpg" alt="" title="mapsample" width="248" height="300" class="size-medium wp-image-1307" srcset="http://www.paleomedia.org/wp-content/themes/tma/images/mapsample-248x300.jpg 248w, http://www.paleomedia.org/wp-content/themes/tma/images/mapsample.jpg 437w" sizes="(max-width: 248px) 100vw, 248px" />](http://www.paleomedia.org/maps/2012_map.html)<figcaption id="caption-attachment-1307" class="wp-caption-text">See the live map here!</figcaption></figure>This is what happens now: The Secretary of State updates a .pdf file two or more times a day during the filing period and posts it on his web page. That means that anyone interested in the intrigue of candidate filing in Idaho&#8217;s newly refigured legislative districts has to bookmark the page, reload it several times a day and scan it for new entries.

I&#8217;ve been reading a lot about [data journalism](http://danwin.com/2012/02/code-dont-tell-programming-as-an-essential-journalism-skill/) and thought I could follow some of the tutorials out there and create a nice little web scraper to tease out the scoops on candidate registration. I am really inspired by sites like ProPublica, which puts together awesome databases like [this one on what influenced support on SOPA/PIPA](http://projects.propublica.org/sopa/) or [one on unequal course offerings in schools](http://projects.propublica.org/schools/states/id) across the nation that incorporates maps. I like maps. The Guardian in the UK is also doing amazing things with [data journalism](http://www.guardian.co.uk/data) and making information public and available and accessible. These guys make it look easy.

<figure style="width: 100px" class="wp-caption alignleft"><img loading="lazy" alt="" src="https://lh3.googleusercontent.com/--XS9-sH9qm0/AAAAAAAAAAI/AAAAAAAAAIQ/ieNuxdHwhcI/s200-c-k/photo.jpg" title="Brett Nelson" width="100" height="100" /><figcaption class="wp-caption-text">Brett Nelson, AKA "The Ruby"</figcaption></figure>So I took a Boise City Community Education class on Ruby programming last week, thinking I could pick up a few new skills. The only thing I really learned was that I&#8217;m going to stick with WordPress as a blog platform and it&#8217;s unlikely that I&#8217;ll ever be a real programmer. But I suggested to the teacher, [my friend Brett Nelson](https://plus.google.com/101964825753829360899/posts), who works at [Customated.com](http://customated.com/), that I had this idea to grab the candidate .pdf from the Secretary of State, convert it into a useful format and post it somewhere automatically so that my reporter friends don&#8217;t have to work so hard.

As with anything, it&#8217;s harder than it looks, and Brett ended up doing all of the heavy lifting on this.

Here is what (I think) we did:

  1. Wrote a ruby script (a little computer program) that automatically downloads the .pdf from the Secretary of State&#8217;s website as often as we like, converts it to text using [Xpf](http://www.foolabs.com/xpdf/about.html), which preserves the spacing, and then uses [Regular Expressions](http://www.regular-expressions.info/) to parse the text into fields: District, Office, Party, Name, Address. The program runs remotely, on a server and activates itself. Yeah, it&#8217;s a bot.
  2. Use our nicely formated text file to build a [Google Fusion table](http://www.google.com/fusiontables/Home/). Again, this is automated, using Google Maps/Fusion API commands. Google Fusion Tables allows us to easily place candidates on a Google Map, though it&#8217;s a bit more difficult to actually build the map on a web page, and requires a working knowledge of Javascript, another programming language.
  3. I told Brett I&#8217;d take it from there, but again, it was not that simple. First of all, I could not figure out how to embed all the javascript I&#8217;d need in a blog post on this blog, so I had to just make [a new web page](http://paleomedia.org/maps/2012_map.html), that looks like it&#8217;s on this blog. Also, I really don&#8217;t get the details of javascript anyway. So once again, Brett bailed me out.
  4. I found a [cool use of fusion tables](http://gmaps-samples-v3.googlecode.com/svn/trunk/fusiontables/chicago-homicides.html) that I wanted to emulate, allowing the user to select Senate, House A or House B races to display on the map so that they could easily see which districts had contested races. I spent hours trying to customize the Chicago homicide map linked above to my own needs, but gave up in desperation. Brett figured out the right calls we&#8217;d need to redraw the map (it&#8217;s not really that complicated, but it&#8217;s like learning a foreign language).
  5. Finally, after I&#8217;d say 25 hours between us, though my hours were much less valuable than his, we had a workable map. I&#8217;m still bummed it&#8217;s not as pretty and full of functionality as the Propublica projects are, but I think it&#8217;s quite useful. 

So what can you do with this web app? First of all, I think it&#8217;s the first Google map of the [newly drawn legislative districts](http://www.legislature.idaho.gov/redistricting/adopted_plans.htm). I converted the .shp file (L93) that the Commission published to a .kml file (which Google Maps reads) using [Qgis](http://www.qgis.org/) on my Mac. So now people cal fly around the new districts, find their house, <del datetime="2012-03-02T21:15:50+00:00">make sure that candidates actually live in their districts</del>, figure out which legislators have the best nearby hunting spots, etc. UPDATE: The locations plotted for candidates are their filing addresses, not necessarily their home addresses, and thus may be located in a different district.

Second of all, you can easily see which races are contested for the May 15 Primary Elections by selecting one of the three Legislative races and looking for red or blue markers on the map. This map is constantly updated with new filing information. Candidate filing closes in a week, on March 9, so we will have to figure out how to make this information useful on an ongoing basis. I&#8217;d like to add web links and Twitter feed info for candidates and links to news articles about the races (if anyone wants to help, please speak up)!

Please let us know what you think and feel free to use any of the info you glean from our web app!