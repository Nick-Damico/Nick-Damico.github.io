---
layout: post
title:  "CLI Project: Local Ski Report"
date:   2017-07-13 22:58:19 +0000
---


## Getting Started.
After ten days of work, i'm finally at the last few stages of my CLI gem portfolio project and its been a journey. I have learned a lot over this last ten days and feel that i've definitely improved my programming skills. I feel better equipped on how to approach a coding problem and figure out a solution. I have to thank Avi from Flatiron for his daily_deals CLI walkthrough and approaching the design of an app from the entry point, and in my case that was the user interface. By starting with the design of the interface first I was able to define how I wanted my program to work and then it was just a matter of creating the objects, methods, and getting the data to make it function.

## A little Background first.
Why a CLI gem of ski resort reports and ski areas? It's pretty simple and obvious, I have worked as a third shift snowmaker for the past 10 years at the only ski resort in Tennessee so the ski industry is close to me. But its more then that, I've also been skiing and now snowboarding since high school and when I found out the guidelines for the project it was the first idea that 'popped' into my head, it just seemed like a good fit for this kind of project that is data driven. 

The appeal of CLI apps was kind of missed on me at first, what use are they in a time when websites which are responsive and designed with consideration for mobile devices? And my answer to that over the last few days is speed. The 'speed' in which I can access information and data that i'm interested in. In fact, as of right now using my ski report you can get a ski report from any resort or ski area in probably the time it will take for you to locate a link for the resort you want. I'm impressed by it for sure.

## The interface.
The interface is simple probably like a lot of CLI apps. It consists of ordered lists which present a user with a series of lists, and then prompts them to make a choice, then presents them with the next choice until they ultimately have to decide on a ski resort or ski area to get the most recent published report. Here's what it looks like:

```
----------------------------------------
Welcome to Local Ski Report gem
----------------------------------------
Let's Get Your Local Ski Report
 
1. MIDWEST
2. NORTHEAST
3. NORTHWEST
4. ROCKIES
5. SOUTHEAST
6. WEST COAST
--------------------------------------------------
Which region would you like to check? type number: 
```

First, instead of hitting the user over the head with a huge, massive list of ski areas we narrow them down first, as you see above, is selecting a region. Then we list all the States within that region that have a ski area:

```
--------------------------------------------------
1. Alaska
2. Idaho
3. Oregon
4. Washington
--------------------------------------------------
Which State would you like to check? type number: 
```

Next, the user must decide on a state to narrow the search down further... Once that decision is made this allows the scraper class to run a method to scrap the data and return a list of resorts inside of that state; in this example I chose 1. Alaska :
```
--------------------------------------------------
1. Alyeska Resort
2. Eaglecrest Ski Area
3. Hilltop Ski Area
--------------------------------------------------
Select a Resort or Ski-Area for the latest Ski Report: 

```

And finally, this deploys the scraper object once more and returns the selected ski resort or areas latest report data in a table format:

```
+---------------------+--------------------+--------+----------+------------+------------+
|                                       Ski Report                                       |
+---------------------+--------------------+--------+----------+------------+------------+
| Resort Name         | Updated On         | Status | New Snow | Base Depth | Lifts Open |
+---------------------+--------------------+--------+----------+------------+------------+
| Eaglecrest Ski Area | Last Updated: 4/10 | Closed |    0"    | N/A - N/A  |        0/4 |
+---------------------+--------------------+--------+----------+------------+------------+
Type: 'more' for detailed report, 'new' for new search, 'exit' to Quit.
```

It's as simple as that! Then from this point a user can expand on this information by typing the command `more`, start an entirely new search with `new`, or quit the program with `exit`.

## Approach and Design.
Above, I explained why I decided to narrow the search and not overwhelm the user with choices by starting with an ordered list of regions followed by another ordered list of states. This decision was twofold. The first reason was to make it easier for a user to find what she or he is looking for. Secondly, it was to also allow them to construct the variables for the url which gets supplied to the scraper class to scrape the data and return initially the ordered list of resorts, and finally the data for the tabular data.

I made the decision during the rough draft of the interface to construct the regions and states with ski areas to a multi-dimensional array of hashes. At first, this was to simulate the app as working since I started with the interface before even writing a single Class. But later, I decided to stick with the regions being data native to the app instead of scraping because I feel confident that regions and states won't be changing any time soon, hopefully. But it was also two less times the scraper would have to go out and retrieve information. This is what that looks like:

```
 STATES_WITH_RESORTS = [
        { :midwest => ["Illinois", "Indiana", "Iowa", "Kansas", "Michigan", "Minnesota", "Missouri", "Ohio","Wisconsin"] },
        { :northeast => ["Connecticut", "Maine", "Massachusetts", "New Hampshire", "New Jersey", "New York", "Pennsylvania", "Rhode Island", "Vermont"] },
        { :northwest => ["Alaska", "Idaho", "Oregon", "Washington"] },
        { :rockies => ["Colorado", "Montana", "New Mexico", "Utah", "Wyoming"] },
        { :southeast => ["Alabama", "Georgia", "Maryland", "North Carolina", "Tennessee", "Virginia", "West Virginia"] },
        { :west_coast => ["Arizona", "California", "Nevada"] }
    ]
		```
		
The other decision I made was to create 4 Classes. The four Classes are:
1. CLI Class
2. Resort Class
3. Report Class
4. Scraper Class

I wanted to really get OOP founded into my brain here so I tried to implement as much as I could from the lessons and labs I had worked through at Flatiron in the OOP section prior to starting this project. I really liked the idea of collaboration between two objects even if they aren't necessarily directly related. I decided that I would practice the relationship 'has many' and 'belongs to' with my program. The Resort has attributes that define it and one of those is `:reports` which instead of being data stored as a simple primitive 'string' or 'array' I decided to have it contain an instance of Report object. I wanted code that I could get the number of ski lifts open for the day by typing `resort.report.liftsopen`. I feel like I accomplished this, even though it may not be the best example of collaboration.

## Final Thoughts.
I was dreading this project as I dread most coding projects because of fear, I think, is this going to be the one? The one project that I can't complete and will expose me as a 'fake' or 'imposter' programmer. I'm starting to realize now that I'm not the only one going down this path in learning something new and has these fears of being a 'fake'. I decided the night before starting this project that even if it takes me a month to finish it that I'm capable of it, with hard work we all are. I really enjoyed this experience and i'm looking forward to what I'll be learning and doing next.

Take care,
Nick



