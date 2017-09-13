---
layout: post
title:  "Sinatra Project: Auction Calendar"
date:   2017-09-13 18:27:57 +0000
---

I feel today is a big milestone in my programming career, after 6 days of coding I've built my first dynamic web app. This is no small feat for me, or for anyone who is just getting started coding. It's something I've been working toward doing for a lot longer then I want to admit here. I started with development years ago but all my coding efforts up until this point were front-end and probably could be categorized as design more then programming. I had a good understand of the front-end but everything else about app development for the web was a mystery to me. 

Luckily FlatironSchool has given me a direct path for learning this and not only teach me the things I needed to learn to understand full web app development, but they also have given me the confidence to go out and build something I thought up and wanted to bring to life. Thinking about all the parts that took to make this accomplishable, and the fact I was able to finally understand the bigger picture of a few things I've wanted to understand for a long time now. I've built forms with HTML and CSS a lot over the last few years, but they were useless without backend coding. I wondered how CMS's functioned and now I've built one on my own!! This stuff makes me excited about whats to come as I continue to further my abilities.

Okay now onto my app: Auction Calendar

![](http://res.cloudinary.com/nic-alan/image/upload/c_scale,w_900/v1505324294/auction-calendar--landing_l4rmyo.png)


The back story for this app is that i've been an auctioneer part-time for the past ten years working for my father's auction company. The spec's and guidelines for this project said, "keep track of something important to me", so I decided keeping track of our auction schedule would be a good fit. I hope with some additional work in the future I can use this as a CMS with an existing site I built for our auction business a few years ago too, [dealershipappraisals](http://dealershipappraisals.com).

The app is simple. The models are: `User`, `Auctions`, `Auctioneers`. The relationships are a user has_many auctions, a auction belongs_to a user, a auction has_many auctioneers, and auctioneers also have many auctions. To accomplish the relationship of auctions to auctioneers which is a many to many relationship I had to setup a join table, called auction_auctioneers. I graphed this out to make it easier to understand my models relationships.

I struggled with this a little at first but with some helpful suggestions from the flatiron community and a few attempts I was able to successfully setup my database and models.

The http requests are managed by three controller classes: `auction_controller`, `auctioneer_controller`, and `user_controller` which inherit from a basic controller model setup in `application_controller`. The views for these controller actions have basic CRUD functionality. A view to see individual instances, all instances, a form to create, update and delete these instances. Here are few examples of what that looks like:

All Auctions View:

![](http://res.cloudinary.com/nic-alan/image/upload/c_scale,w_800/v1505326008/all-auction-view_psho6a.png)

All Auctioneers:

![](http://res.cloudinary.com/nic-alan/image/upload/c_scale,w_800/v1505326006/all-auctioneers_agcl5h.png)

Create auction form:

![](http://res.cloudinary.com/nic-alan/image/upload/c_scale,w_800/v1505326008/create-auction_ytdsfv.png)

One of the requirements was to use validations which I used ActiveRecords validation macros defined within my models and methods like `.valid?` inside of controller actions to do this. I took this an additional step by using the `required` HTML attribute on inputs in my forms for creation and editing.

Finally, I spent an extra day or two focusing on the front end styling a little bit with CSS. I've been wanting to try out Bootstrap V4 which is still in beta. I found it a little difficult for a few reasons to pick up at first since I really haven't used Bootstrap in over a year, but overall with just a little custom css overrides I'm happy with how it looks. I hope to return and continue to improve the design one day.

[Auction Calendar Github Page](https://github.com/Nick-Damico/Auction-Calendar)

Take care,
Nick D

