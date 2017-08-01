---
layout: post
title:  "SVG Sprite Maps"
date:   2017-07-31 22:04:14 -0400
---

This last week and a half I've been working through SQL (Structured Query Language) which has been a nice change of things for me since I've been entrenched with Ruby for the past 60+ days and getting to see something different and new was a nice change. I've also always wanted to learn about databases and backend programming since all of my experience prior to starting at Flatiron has been exclusively Front End. Luckily after some hard work and time SQL and ORM are starting to become a whole lot clearer to me.

Early this morning, as I sat at work drinking coffee I knew that it was time for another blog, but unlike the past few months where I blogged about what I have been currently involved with at school I decided I wanted to share something I learned a while ago and was part of front end programming. I decided on SVG icons and making a sprite map. I will hopefully have a nice blog post soon on SQL though! But until then...

# Website Optimization
Website optimization is probably different for everyone and happens at different times during a site development process. For some, it might be at the end of the site build when they go back over their project and see where they can make improvements, and for others, it might be something they make consideration for at the very outset of the project in the 'planning stage' even before the first line of HTML or CSS is ever written.

One of these places in our sites that we consider when thinking of optimizing for the web is images. It might be adjusting an images resolution or quality in photoshop or similar program. It might be deciding if an `<img>` would be better suited for a different file type like replacing a `.png` with an `.svg`. Making a decision like this can have a huge impact on a sites performance. 

# HTTP Requests
Images and icons bring our sites to life and enhance the viewers experience. Images make sites more enjoyable, but if not handled properly can cause frustration for the user as well. This is due to the fact that each `<img>` is another file download and request to a server. This can be bad because the server requests can start to take longer then the actually downloading of the file. In the case of small icons like the social links that we include on our sites we can minimize these requests by combining them and make one request for all.

For this post I've marked up a small `<footer>` component that i'll be working with to demonstrate sprite maps. This is a somewhat typical footer component that you would find on a web page that includes a copyright on the left, and a set of social icons aligned to the right.

![](https://res.cloudinary.com/nic-alan/image/upload/c_scale,w_645/v1501542194/sprite_map_iorctw.png)

The icons on the right were previously `.png` and after being redesigned as `.svg`'s. We not only save on bandwidth but our icons stay looking sharp due to svgs being vector graphics. Here is a look at our images in the developer panel of Chrome. This gives us a look at the 'network' impact of the images currently.

![](http://res.cloudinary.com/nic-alan/image/upload/c_scale,w_626/v1501550278/before_map_k6rmj3.jpg)


As we can see above that the impact is minimal. The total download of these files is less then 5kbs! But that doesn't mean things can't be improved. In fact we can minimize network impact by reducing the number of requests to the server. We can take these (3) SVG's and combined them to just one file and with the help of the HTML5 elements they will still appear exactly as pictured above but cost our network only (1) server request. Let's get started.

# Combining SVGS

If we open our SVG files inside of our code editor, i'm using Sublime Text 3, you'll see something similar to this:

```
<?xml version="1.0" encoding="utf-8"?>
<!-- Generate more at customizr.net -->
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg id="facebook-square" class="custom-icon" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 100 100" style="height:100px;width:100px;"><circle class="outer-shape" cx="50" cy="50" r="48" style="opacity: 1; fill: rgb(165, 172, 186);"></circle>
	<path class="inner-shape" style="opacity:1;fill:#fff;" transform="translate(25,25) scale(0.5)" d="M82.667,1H17.335C8.351,1,1,8.351,1,17.336v65.329c0,8.99,7.351,16.335,16.334,16.335h65.332 C91.652,99.001,99,91.655,99,82.665V17.337C99,8.353,91.652,1.001,82.667,1L82.667,1z M84.318,50H68.375v42.875H50V50h-8.855V35.973 H50v-9.11c0-12.378,5.339-19.739,19.894-19.739h16.772V22.3H72.967c-4.066-0.007-4.57,2.12-4.57,6.078l-0.023,7.594H86.75 l-2.431,14.027V50z"></path>
</svg>

```

First thing we need to do is create a new file in our project that will hold all these svgs. I've named mine ```img/social_svgs.svg```.  To start we will need create an `<svg>` element to contain the images. This is what that should look like...

```
<svg xmlns="http://www.w3.org/2000/svg" style="display:none;" class="custom-icon">
<svg>
```

Great! We need to create a container for the SVGs and we will be using an element called ```<symbol>```. We can go ahead and add a ```<symbol>``` element for each one of our icons. 

```
<symbol id="twitter" viewbox="">
</symbol>

<symbol id="instagram" viewbox="">
</symbol>

<symbol id="facebook" viewbox="">
</symbol>
```

Now we will open our icons SVG file one at a time and get the information that we will use to populate these elements and its attributes with. Starting with the attribute `viewbox=` lets copy the value of the Twitter icons viewbox value and paste it into the new symbol viewbox attribute inside our social_svgs.svg file.

```
<symbol id="twitter" viewbox="0 0 100 100">
   // SVG Goes Here
</symbol>
```

Next we will go back to our file and copy the contents of the icon which is everything between the `<svg>` element tags and paste it in between our `<symbol>` open and closing tags.

```
<symbol id="twitter" viewbox="0 0 100 100">
		<circle cx="50" cy="50" r="48" style="fill:rgb(165,172,186);"/>
        <g transform="matrix(0.5,0,0,0.5,25,25)">
            <path d="M99.001,19.428C95.395,21.036 91.521,22.123 87.454,22.612C91.604,20.109 94.792,16.146 96.295,11.423C92.41,13.741 88.108,15.423 83.527,16.331C79.86,12.4 74.634,9.944 68.851,9.944C57.747,9.944 48.744,18.998 48.744,30.167C48.744,31.752 48.921,33.295 49.264,34.776C32.554,33.931 17.739,25.881 7.822,13.645C6.092,16.633 5.1,20.107 5.1,23.813C5.1,30.83 8.65,37.021 14.045,40.647C10.749,40.543 7.648,39.633 4.939,38.118C4.937,38.203 4.937,38.288 4.937,38.373C4.937,48.172 11.868,56.345 21.066,58.204C19.378,58.667 17.603,58.914 15.769,58.914C14.473,58.914 13.214,58.787 11.986,58.551C14.545,66.585 21.97,72.433 30.768,72.596C23.887,78.02 15.217,81.253 5.797,81.253C4.174,81.253 2.574,81.157 1.001,80.971C9.899,86.709 20.468,90.058 31.821,90.058C68.803,90.058 89.027,59.241 89.027,32.515C89.027,31.638 89.007,30.767 88.968,29.898C92.896,27.045 96.305,23.482 99.001,19.428Z" style="fill:rgb(247,247,247);fill-rule:nonzero;"></path>
         </g>
	</symbol>
```

Awesome, we are getting closer. Let's go ahead and repeat these steps for all of our icons. When we finish this is what our file should look like.

```
<svg xmlns="http://www.w3.org/2000/svg" style="display:none;" class="custom-icon">

	<symbol id="twitter" viewbox="0 0 100 100">
		<circle cx="50" cy="50" r="48" style="fill:rgb(165,172,186);"/>
        <g transform="matrix(0.5,0,0,0.5,25,25)">
            <path d="M99.001,19.428C95.395,21.036 91.521,22.123 87.454,22.612C91.604,20.109 94.792,16.146 96.295,11.423C92.41,13.741 88.108,15.423 83.527,16.331C79.86,12.4 74.634,9.944 68.851,9.944C57.747,9.944 48.744,18.998 48.744,30.167C48.744,31.752 48.921,33.295 49.264,34.776C32.554,33.931 17.739,25.881 7.822,13.645C6.092,16.633 5.1,20.107 5.1,23.813C5.1,30.83 8.65,37.021 14.045,40.647C10.749,40.543 7.648,39.633 4.939,38.118C4.937,38.203 4.937,38.288 4.937,38.373C4.937,48.172 11.868,56.345 21.066,58.204C19.378,58.667 17.603,58.914 15.769,58.914C14.473,58.914 13.214,58.787 11.986,58.551C14.545,66.585 21.97,72.433 30.768,72.596C23.887,78.02 15.217,81.253 5.797,81.253C4.174,81.253 2.574,81.157 1.001,80.971C9.899,86.709 20.468,90.058 31.821,90.058C68.803,90.058 89.027,59.241 89.027,32.515C89.027,31.638 89.007,30.767 88.968,29.898C92.896,27.045 96.305,23.482 99.001,19.428Z" style="fill:rgb(247,247,247);fill-rule:nonzero;"></path>
         </g>
</symbol>

<symbol id="instagram" viewbox="">
		<circle class="outer-shape" cx="50" cy="50" r="48" style="opacity: 1; fill: rgb(165, 172, 186);"></circle>
            <path class="inner-shape" style="opacity:1;fill:#f7f7f7;" transform="translate(25,25) scale(0.5)" d="M88.2,1H11.8C5.85,1,1.026,5.827,1.026,11.781V88.22C1.026,94.174,5.85,99,11.8,99H88.2c5.95,0,10.774-4.826,10.774-10.78 V11.781C98.973,5.827,94.149,1,88.2,1z M49.946,31.184c10.356,0,18.752,8.4,18.752,18.762c0,10.361-8.396,18.761-18.752,18.761 s-18.752-8.4-18.752-18.761S39.589,31.184,49.946,31.184z M87.513,83.615c0,2.165-1.753,3.919-3.917,3.919H16.341 c-2.164,0-3.917-1.755-3.917-3.919v-41.06h8.508c-0.589,2.35-0.904,4.807-0.904,7.34c0,16.612,13.459,30.079,30.063,30.079 s30.063-13.466,30.063-30.079c0-2.533-0.315-4.99-0.904-7.34h8.263L87.513,83.615L87.513,83.615z M87.764,27.124 c0,2.165-1.754,3.919-3.918,3.919H72.723c-2.164,0-3.917-1.755-3.917-3.919v-11.13c0-2.165,1.754-3.919,3.917-3.919h11.123 c2.165,0,3.918,1.755,3.918,3.919V27.124z"></path>
</symbol>

<symbol id="facebook" viewbox="">
		 <circle class="outer-shape" cx="50" cy="50" r="48" style="opacity: 1; fill: rgb(165, 172, 186);"></circle>
            <path class="inner-shape" style="opacity:1;fill:#f7f7f7;" transform="translate(25,25) scale(0.5)" d="M82.667,1H17.335C8.351,1,1,8.351,1,17.336v65.329c0,8.99,7.351,16.335,16.334,16.335h65.332 C91.652,99.001,99,91.655,99,82.665V17.337C99,8.353,91.652,1.001,82.667,1L82.667,1z M84.318,50H68.375v42.875H50V50h-8.855V35.973 H50v-9.11c0-12.378,5.339-19.739,19.894-19.739h16.772V22.3H72.967c-4.066-0.007-4.57,2.12-4.57,6.078l-0.023,7.594H86.75 l-2.431,14.027V50z"></path>
</symbol>

<svg>
```


# Adding the Sprite Map.
We have our new SVG file built out with all of our icons. Its now time to add it to our HTML page. We will be copying the contents of that entire page and pasting it right after the opening `<body> ` tag on the HTML page `<index.html>`. With that done all that is left to do now is replace the `<img>` elements nested inside of my anchor elements with `<svg>` tags. Before this change here is the original markup for each img icon.

```
<a href="http://twitter.com">
  <img src="twitter.svg" />
</a>

<a href="http://instagram.com">
  <img src="instagram.svg" />
</a>                    

<a href="http://facebook.com">
  <img src="facebook.svg" />
</a>
	
```

This is how we should layout our icons which reference our symbol elements with the` <use>` element and its attribute `xlink:href ` should have its value set to the #id attribute of the` <symbol>`. This should be the end result.

```               
<a href="http://twitter.com">
	<svg>
			<use xlink:href="#twitter" />
  </svg>
</a>

<a href="http://instagram.com">
  <svg>
	  <use xlink:href="#instagram" />
	</svg>
</a>                    

<a href="http://facebook.com">
  <svg>
	  <use xlink:href="#facebook" />
	</svg>
</a>
```

The final product.

![](https://res.cloudinary.com/nic-alan/image/upload/c_scale,w_631/v1501549486/sprite_map_kxna5r.png)

The request are now all gone!

![](http://res.cloudinary.com/nic-alan/image/upload/c_scale,w_663/v1501550278/after_map_alt4ju.jpg)


# Finished!
Well there you have it. The result is that we are now using SVG's for our social icons and we now have our images stored inside of our HTML page and removed an HTTP request for each of those images. And best of all, its optimized and looks exactly like our original design. I hope this is something that will be useful to you in the future and another tool in your optimization toolbox.

I've pushed this example to Github if you would like to look at the files for yourself and experiment.

[Sprite Map HTML Example. GitHub Repo](https://github.com/Nick-Damico/sprite_map_example/tree/master)

take care,
Nick


