---
layout: post
title:      "Rails & jQuery Project: HikeIt"
date:       2018-01-09 23:21:26 +0000
permalink:  rails_and_jquery_project_hikeit
---


This project had me returning to my previous portfolio project from the Rails section named 'HikeIt'. In short, 'HikeIt' was my attempt to create a social app which brought together my passion for hiking and a way for people to share the experience of getting outside and enjoying the National Parks. 

![](http://res.cloudinary.com/nic-alan/image/upload/c_scale,w_600/v1515532650/hikeit/hikeit_login.png)

A Blog about the app with more info can be found[ here](https://nick-damico.github.io/rails_final_project_hikeit)

I  was surprised how easy this project was for me to jump into and start coding away at the requirements. This is probably a testament to how good of a job Flatiron has done with teaching not only JavaScript fundamentals but AJAX and API's. A true understanding of API's, not only how to dig through the documentation of an API but how to implement my own API endpoints for making data accessible to others through my app. I'm very excited how far I've come in my programming career so far with this program.

## Project Requirements

I'm going to touch quickly on a couple of the project requirements and briefly explain how I accomplished each.

***- Must render at least one index page (index resource - 'list of things') via jQuery and an Active Model Serialization JSON Backend. ***

HikeIt has two index views which display all resources for 'Hikes', these are hiking events that a User plans and gets posted to an upcoming hike board. The RESTful route for this is `/hikes.` The other index is `/hikingtrails` which is a collection of all trails in the Great Smoky Mountain National park which are updated and collected using a scraper class in the services directory that collects the data from http://www.hikinginthesmokys.com/. 

I made the decision to render the hikes index page because this is the most important resource in my app. I also knew this view used a lot of logic on the server to render and because of that would be a great challenge to replicate using only JSON data and JavaScript.

Once I had Active Model Serializers gem installed and used the `rails g serializer <modelname>` command to setup serializer classes for all my models, it was just a matter of getting the index route to return JSON data 
```
def index
		if params[:user_id] && @hikes = User.find_by(id: params[:user_id]).hikes
			@hikes
		else
			@hikes = Hike.all
		end
		respond_to do |format|
			format.html
			format.json { render json: @hikes, status: 200 }
		end
end
```

I used Bootstrap for layout and presentation along with a lot of custom CSS styles. Bootstrap can really clutter the markup with a lot of div's and nested complexity so using Handlebars.js was the right solution for me. I used `handlebars_assets` gem. I'm going to write a blog in the next week on how to setup this gem and structure it within a Rails project, but for now, here is a screenshot of my project directory.

![](https://i.gyazo.com/9392c4f55a1f4da9239eb0b3f8b16dd3.png)

In brief, the templates are stored in a `/templates` directory and sub-directory for each resource was made. For me, this was a `/hikes` directory which holds template files with the same name as my `.erb` views only with a `.hbs` extension. Partial files are handled with a similar convention as erb with an underscore _filename.

​
The Handlebars team decided to keep templates as logicless as possible, so there are if/else blocks and even an #each iterator block that can be used within templates but are limited to checking if an item or attribute is truthy or falsy but cannot make comparisons, for this you need helpers.My .erb views utilized a lot of logic which got tucked away in helper files so I was needing more than just the default blocks provided by Handlebars and that is what is stored in the directory `/handlebar-helper.js`. This is a place to register your Handlebar helper methods which can then be used in the templates.

Here is an example of one of these files: _hike-card.hbs. 
```
  {{#each hike}}
    <div class="index-hike-card col-8 col-sm-5 col-md-4 col-lg-3 border border-dark slow-grow hike-card mb-4 p-1 color bg-grey-red">
      {{#if trail_image}}
        <img class="img-fluid w-100 card-img" src="{{trail_image}}" alt="{{trail}} thumbnail">
      {{else}}
        <img options="{:size=>&quot;280x200&quot;}" class="img-fluid card-img w-100" src="/assets/btn-find-hike-692f3cf34feb3aa5adbcd529f76b0da701819af5d97c0c8ccc1f5569d4b9873a.jpg" alt="Btn find hike">
      {{/if}}
      {{#join_status hikers}}
      {{/join_status}}
    	<div class="col banner-content">
    		<h3><a class="font-w-300 color-burnt-orange show-hike-btn" href="/hikes/{{id}}">{{title}}</a></h3>
    		<h4 class="text-white font-w-100">{{trail}}</h4>

    		<ul class="no-style pl-0 font-w-100 color-slight-pink mb-1">
    			<li>{{description}}</li>
    			<li class="card-date-color">{{#formatted_date this}}{{/formatted_date}}</li>
    		</ul>
    	</div>
      {{#hike_banner hike_type}}
      {{/hike_banner}}
    </div>
  {{/each}}
```

**-The rails API must reveal at least one has-many relationship in the JSON that is then rendered to the page.**

**-Must translate the JSON responses into Javascript Model Objects.**

The only thing left to do now was to hijack the 'find hikes' button and stop its default behavior using jQuery. I used $.ajax method to make my requests and handle the response. I built JavaScript Model Objects using constructor functions and stored them within the oop.js file. Once the response was received from the AJAX request I used the return data to model objects for each of the returned hikes and users which have a many_to_many relationship that data is then passed to the HandlebarsTemplates method which renders HTML for output to the DOM.

```
.done(function(data) {
    let hike = new Hike(data);
    let users = User.buildUsers(data.users);
    let html = HandlebarsTemplates['hikes/show']({ hike: hike, users: users });
    mainContentAppend(html);
  });
```

Here are the final results.
![](https://i.gyazo.com/263b05f1ea5623dc1ee4cc5396a8c31b.gif)


Show view for a hike. Displays a has_many relationship between a user and hikes.
![](https://i.gyazo.com/9f4e3916d3d9c3331799c011d1c8b200.gif)


I have also implemented per the requirements an AJAX 'post' request to create a new resource of a hike which submits the request and renders the new instance in a show view similar to the one shown in the GIF above. 

Overall this was one of the more enjoyable projects that I've completed. I left this section really feeling like I've grown as a programmer and some concepts that have caused me a large amount of confusion and frustration in the past seem a lot more manageable. I struggled in the past before Flatiron to have a good working knowledge of both API's and OOP JavaScript. I was able to take my experience from this section of the school and build the Tic-Tac-Toe project using the newer class expressions and class declarations, and I even finished a few FreeCodeCamp projects for practice which I wasn't confident in doing until now.

thanks for reading,
Nick D
