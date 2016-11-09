---
layout: post
title: Searching for Snowplow's Structured Events
---

This is a tutorial on how to look for any type of structured event that Snowplow or other event based web analytics tools collects. This will help understand how a server call is built and how the data is sent to your backend system. In the case of Dollar Shave Club that is Looker. 

First, we will want to click on a web element that we know has a structured event attached to it. If you do not know if a web element has an event attached to it, click everywhere and them we can see if a structured event pops up in the network tab. Right now I want to know the number of clicks on on our FAQs sections.

![My helpful screenshot]({{ site.url }}/images/snowplow/click_event.gif){:class="center-image"}

After that I need to look at the Developer Console in Chrome to see what click that button actually did. Right click on the page and then click "Inspect", just like below.

![My helpful screenshot]({{ site.url }}/images/snowplow/opening_dev_console.gif){:class="center-image"}

From here you will need to look at specifically the "Network" tab. There will be a lot of noise here because websites constantly make requests to lots of other websites. If you do no see anything, refresh the page and leave this tab open. Repeat the step above and click the element again. 

After you start to see lots of rows load up, we need to search only for Snowplow network calls. These network calls are what is sending data to your servers. For our Snowplow code, we host it on **"analytics.dollarshaveclub.com"**. So I type that into the filter window so I only see the calls I am interested in.

![My helpful screenshot]({{ site.url }}/images/snowplow/open_network_tab.gif){:class="center-image"}

After that, we now want to look at what that call consist of. For Snowplow there is two primary types of calls, pageviews and structured events. When **"e=pv"** that is a pageview and will show up in the backend as a page. When **"e=se"** that is a structured event. This is what we are searching for right now. Below I go through several different calls to show some examples of the information that is collected.

In the case of the structured events, there is normally three different values associated that call. Those three values are Catagory, Action, and Label. They will appear in a hierarchical order in the database, the table below shows how each value matches with the network call.

{:class="mbtablestyle"}
| Values   | Paramaters | 
| :------: |:----------:| 
| Catagory | se_ca      | 
| Action   | se_ac      | 
| Label    | se_la      |

Look at the network call syntax and you will see these three values.

![My helpful screenshot]({{ site.url }}/images/snowplow/packet_sniffing.gif){:class="center-image"}

After we look at the network calls, we can jump into our database and start to look for the data. Open Looker and Explore the Events table, this is where we keep our Snowplow data. Then click Events on the left and scrolls down to **Structured Event Label** and then click FILTER.

![My helpful screenshot]({{ site.url }}/images/snowplow/serach_looker.gif){:class="center-image"}

This will open the tab that will let you search for the network calls that you just looked at in the Network tab. You can search the Category, Action, or the Label. 

![My helpful screenshot]({{ site.url }}/images/snowplow/custom_query.gif){:class="center-image"}

I hope this tutorial will help you understand how to look for the data that you are interested in. 
