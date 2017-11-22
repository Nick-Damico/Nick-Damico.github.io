---
layout: post
title:      "Rails Final Project: HikeIt"
date:       2017-11-22 04:59:18 +0000
permalink:  rails_final_project_hikeit
---

I can say after two weeks and 218 commits to Github that I've completed the requirements of the Rails section final project! There are so many things I want to continue to add to this project and I will over the next few months. This is definitely one project that I look forward to coming back to in the months after graduation to continue to maintain and improve my skills.

The day after successfully completing Sinatra a friend from Twitter noticed I would be starting Rails and posted on my page, "Rails is so much fun, you are going to love it!". That excited me so much to hear, but I wasn't prepared for how difficult it was going to be for me. I'm sure a lot of students will agree that it takes some time for Rails to sink in, and in particular, the forms and nested forms. Hey, I should have seen it coming, Avi the Dean of FlatironSchool, says in one of the intro videos to the section that Rails is massive and somewhere north of 90K lines of code. I should have known it would have some complexity to it and the abstraction is difficult at first to get used to especially if you are someone who enjoys the details. It can be confusing because they get buried underneath all the helpers and methods built into the many different Ruby libraries within that make-up Rails.

Anyway, I can say now that I understand what my friend was talking about when she said its fun, she was right just like riding a bike is fun, once you get the hang of it. That's when you get to imagine something that doesn't yet exist and create it. The thing I decided to set out and create was an app called 'Hikeit'. 

HikeIt is a social hiking application that is very basic. Once users register and sign in they are presented with two simple choices 'Plan Hike' or 'Find Hike'. Planning a hike is filling out a form and your first choice is selecting a hiking trail. I built a scraper class and stored it in my services directory for now. I used this scraper to collect data for all the hiking trails in Smoky Mountain National Park and build objects of hiking trails into the database for a user to select from. There is also a nested form for defining a hiking trail which belongs to a hike, so this allows a user to plan a hike on a trail not listed. If all the required fields are filled in then the hike will be moved to the hikes directory page.

If users are feeling like joining a hike versus planning one they just need to click on 'Find Hike'. This will take them to the index view for all Hikes. Here they will see all hikes presented in a card-style grid column and row layout. These listings will give a few intro details on the available upcoming hikes. If the title is clicked the user will be taken to the show page with expanded details of the hike, the ability to join a hike or leave a hike if already joined.

There are two additional links in the navbar of the app which are 'trails' and 'profile'. The trails link will take the user to a table based layout of all trails in the GSMNP(https://www.nps.gov/grsm/index.htm) this includes a lot of useful information for a user to view so they can find the right trail for their next hike. It also has a link to the national park website to give even more information and history of the trail. The profile page displays a users information and gives the user the ability to edit their details. This page also serves to list the users planned hikes and joined hikes.

Devise is how I'm handling authenticating and Authorizing a user, along with the omniauth-facebook provider Gem. I struggled with getting the bugs worked out of logging in a user using Facebook in this project and lab for the devise omniauth section. Devise can be complicated just make sure to read the documentation. The GitHub repo is the most helpful place to look when you feel lost. If you are looking to customize views or the controllers you will need to use commands like `rails generate devise: views user`.

Styling the app was once again handled with Bootstrap v4, here are the gems I have installed:

```
gem 'bootstrap', '~> 4.0.0.beta2'
gem 'jquery-rails'
```

I utilized a lot of layout and positioning classes from Bootstrap's library. I really enjoy using Bootstrap for these kinds of projects because love it or hate it you can get a pages general layout pretty quick. Although this time I really spent some time and pushed myself with styling elements on the pages. This might be looked at as unnecessary since these projects don't specify any requirements on presentation outside of functioning, but I love doing front end work and find it equally enjoyable to building the functionality of the application. I typically will mockup a site in Affinity Designer or Sketch before starting to code but this time I did the designing from in the browser and forgot how easy this is with Google developer tools. They really are amazing especially when you need to get pixel perfect placement of an element. The application ended up with a much darker color scheme then I initially intended, at first I thought something brighter, maybe binge-watching 'Stranger Things'  last week might be what influenced the design.

Here is a pic which shows the apps landing, home, and hikes index view:
![](http://res.cloudinary.com/nic-alan/image/upload/v1511321240/collage_g13fok.jpg)


Thanks for reading!
Nickd
[HikeIt Github](https://github.com/Nick-Damico/HikeIt)
