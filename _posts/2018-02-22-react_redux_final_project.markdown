---
layout: post
title:      "React Redux final project"
date:       2018-02-22 19:25:46 +0000
permalink:  react_redux_final_project
---


After 14 days of coding, 181 git commits, and a lot of coffee my React and Redux final project is finished. I struggled with an idea for this project for almost a week, and I think a lot of that procrastination was due in part to not fully understanding concepts behind Redux and React. Thankfully I found this amazing course on Udemy, 'Modern React and Redux', so if you are reading this and some of the concepts are not 'sticking' with you then check it out.

My project is called 'Forest Dhamma' which isn't probably the best name for the app but it will make sense in a second. I spend time occasionally listening to talks from the monastic communities of the Thai Forest Buddhist tradition and I decided to make a web application that I would use that helps with organizing and listening to these talks all in one place instead of searching around a dozen different sites, and why not? There may be a great chance only a potential employer might look at my app so why not making something I will use and enjoy.

Forest Dhamma is a very simple app as far as functionality is concerned but it felt really complex building it, and I think this is a good time to bring up that making full stack apps on your own can be exhausting. The app allows a user to listen to talks from teachers of the Thai Buddhist Forest tradition and share their favorite talks with other users via using the API or the apps upload form.


## Selecting a monastery

On starting the app you'll be greeted by a landing page with (3) links, home, talks, and upload. If the user wants to find a talk then 'talks' link is where they start, upon clicking on the link they are presented with a list of 'monasteries' which are displayed as cards with the number of dhamma talks currently in the database for teachers of that monastery.

![](http://res.cloudinary.com/nic-alan/image/upload/c_scale,q_auto:good,w_450/v1519326224/forest-dhamma-app/Screen_Shot_2018-02-22_at_2.02.21_PM.png)


## Selecting a teacher
Once the user has selected a monastery they will be presented with a list of teachers as their next choice.

This React container is made up of (3) important components. The top one lists a teacher card for all teachers at that monastery currently in the database. The next component is the most recent talk. Using a return value from the API Rails server which is all talks at the monastery in JSON data, that data is searched through to present the most recently added talk, this is similar to the next component which is the most favorited talk for that monastery. The outcome is essentially the same for either of the three component choices as the user will be presented with the audio player container next.

![](http://res.cloudinary.com/nic-alan/image/upload/c_scale,w_450/v1519326222/forest-dhamma-app/Screen_Shot_2018-02-22_at_2.02.39_PM.png)

## Audio player

The audio player container presents the teacher with a page containing a full list of all his talks and loads his first talk into the audio player by default. The user can select any of the talks by clicking on the play button next to each talk. The other options like 'description' will display the currently playing talks description summary, and 'tags' presents a list of category tags for that talk. The tags section also includes a form element that allows a user to add a tag to that talk, on submission of the form the app will 'fire' a fetch 'POST' request to the server and add that tag to the talk.

![](http://res.cloudinary.com/nic-alan/image/upload/c_scale,w_450/v1519326221/forest-dhamma-app/Screen_Shot_2018-02-22_at_2.02.59_PM.png)


## Uploading 
![](http://)
The last page of the app is the 'upload' form which is a place for adding talks to the database. Its simple select a teacher, give it the data asked for in the form and submitting it will be successful if all the data passes the validations on the Rails model.


![](http://res.cloudinary.com/nic-alan/image/upload/c_scale,w_450/v1519326223/forest-dhamma-app/Screen_Shot_2018-02-22_at_2.03.17_PM.png)


On future updates of the app, I'll be adding file attachement to allow a User to directly upload audio files from their computer using AWS as file storage, a filter talks by tags feature, and a favoriting system for liking talks.

thank you for reading.
Nick

github repo: https://github.com/Nick-Damico/forest-dhamma
