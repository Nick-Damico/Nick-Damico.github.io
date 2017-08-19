---
layout: post
title:  "Ruby require_relative"
date:   2017-08-19 00:46:17 -0400
---


I've learned so much in these past 3 months of school at Flatiron. Everyday, no matter if after work or early in morning on my days off, I login and start again on this path to becoming a web developer. To get to that goal of becoming a professional developer, I must learn and master these concepts and technologies that are part of that job.

I'm amazed with how much of this information that I've been able to learn, but unfortunately there are some concepts that I feel like my understanding of could be better. So i've made a list of these things and once a week try to do a 'deep dive' on one of those topics, maybe not to fully grasp it but to better understand it. One of those topics is `require_relative` and the best practices for requiring files in general since with Ruby there are a few different ways.

# How
We first see the need for requiring files once we move away from having our code in just one file. It's when our projects and apps start to grow that we need structure and a logical way of grouping our code into directories. It's with these projects with multiple files that we find ourselves in need of some way to make our code 'aware' of the other code in our projects so that it can perform its tasks and functions.

We do that with `require_relative` and similar results can be accomplished with `require and load` methods too. How does `require_relative` work. Lets say we have a file that wants to instantiate an instance of a class, lets say a class of `Car`.

`honda = Car.new("Honda")`

If the Class of Car isn't defined within this file, are we able to instantiate an instance of the Car class? The answer is `No`.  We will receive an error msg of `uninitialized constant Car (NameError)`.

Why is that? Well at the moment its because we haven't defined a car Class! Let's do that our first file is named `app.rb`, sounds good, and our next file will be named `car.rb`. This is what it looks like:

```
class Car	
	attr_accessor :name
	def	initialize(name=nil)
		@name = name
	end
end
```

So now if we call `Ruby app.rb` what's going to happen? Will `honda` hold an instance of `Car`? Nope! Once again we are receiving that `constant Car (NameError)`.  Before we had not defined a Class of Car and now we have in `car.rb` so why is that happening again? 

Even though the (2) files share the same directory they still are unaware that the other exists. That 'lack' of connection is what is keeping `app.rb` from instantiating from the Car class, and this is why we need `require_relative`. So let's add it too our app.rb file.

```
require_relative './car'

honda = Car.new("Honda")
```

Greet! we are no longer receiving our (NameError) message and when we enter in the local variable of `honda` we get

```
 honda = Car.new("Honda")
 => #<Car:0x007fb28e1e4220 @name="Honda"> 
```

How does this work..

First we should take a second and talk about `require`, which is a method that also connects our files to one another. But in this situation it will not work and that is because it is connected to a global constant named `$LOAD_PATH`. When we require a file it looks into the array $LOAD_PATH which is an array of absolute file paths. And it fails because your current directory isn't in that variable.

Now there is a way to store our current directory by manipulating the $LOAD_PATH, but there is a simpler way. And that is to follow the rule that Avi mentions in one of his lectures early on in the course when requiring our own files use `require_relative` and specify the file with a relative path from the directory in which you are calling it from. 

A few tips:
 1. When requiring your own files stick to `require_relative`.
 2. Use `require` when specify dependencies like gems
 3. `./` refers to your current directory
 4. `../` refers to your current directories parent directory.


Take Care, Nick D

