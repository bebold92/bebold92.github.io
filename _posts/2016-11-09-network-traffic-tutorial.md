---
layout: post
title: Searching for Snowplow's Structured Events
---

This is a turtioul on how to look for any type of strucutred event that Snowplow or other event based web analaytics tools collects. This will help understand how a server call is built and how the data is sent to your backened system. In the case of Dollar Shave club that is Looker. 

First we will want to click on a web element that we know has a strucutred event attached to it. If you do not know if a web element has an event attached to it, click everywhere and they we can see if a structed event pops up. I want to know the number of clicks on a web elements on our FAQs sections.

![My helpful screenshot]({{ site.url }}/images/snowplow/click_event.gif)

After that I need to look at the Developer Console in Chrome to see what click that button actually did. Right click on the page and then click "Inspect", just like below.

![My helpful screenshot]({{ site.url }}/images/snowplow/opening_dev_console.gif)

From here you will need to look at specificly the "Network" tab. There will be alot of noice here because website constatally make request to alots of website. If you do no see anything, refresh the page and leave this tab open. Repeat the step above and click the element again. 

After you start to see lots of rows load up, we need to search only for Snowplow network calls. These network calls are what is sending data to your servers. For our Snowplow code, we host it on "analytics.dollarshaveclub.com". So I type that into the filter window so I only see the calls I am interested in.

![My helpful screenshot]({{ site.url }}/images/snowplow/open_network_tab.gif)

After that we now want to look at what that call consist of. For Snowplow there is two primary types of calls, pageview and structured events. When **e=pv** that is a pageview and will show up in the backend as a page. when **e=se** that is a strucuted event. This is what we are searching for right now. Below I go thought several different calles to show some examples of the infomation that is collected.

In the case of the structued events, there is normally three different values assoicated that the call. Those three values are Catagory, Action, Label. They will apear in an heighirical order, the table below shows what each value matches into the backend

| Values   | Paramaters | 
| :------: |:----------:| 
| Catagory | se_ca      | 
| Action   | se_ac      | 
| Label    | se_la      |
{:.mbtablestyle}


![My helpful screenshot]({{ site.url }}/images/snowplow/packet_sniffing.gif)

After we look at the network calls, we can jump into our database and start to look for the data. Open Looker and Explore the Events table, this is where we keep out Snowplow data. Then click Events on the left and scrolls down to **Structured Event Label** and then click FILTER.

![My helpful screenshot]({{ site.url }}/images/snowplow/serach_looker.gif)

This will open the tab that will let you search for the network calls that you just looked at in the Network tab. You can search the Category, Action, or the Label. 

![My helpful screenshot]({{ site.url }}/images/snowplow/custom_query.gif)

I hope this tutorial will help you understand how to look for the data that you are interested in.







