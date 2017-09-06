---
layout: post
title:  "What is this File Class?"
date:   2017-09-05 19:58:50 -0400
---


I have this list of things I don't quite understand, well actually I mean its a list of things about the programming concepts or things within the programming languages I'm studying that I don't quite understand. This list grows by the day and I'm sure this is normal. Its a normal thing I feel to not understand it all, no matter how much we want to. We encounter these things that are rare use cases, or they seem too deep to tackle at the present moment, so we pass them by and make a mental note to return to it later, or in my case write it down on a list. 

I decided recently to use my blog as a means to mark one of these misunderstood or inferred programming concepts off my list. This is where the Ruby Class `File` comes in. I had assumptions of what the `File` class and its methods were doing from my programming experience. I look at code like this `file.split(file_name)` or this thing `__FILE__`.. I tell myself I have a good idea what this is doing, but Its time to open up my text editor and start working with some code so that I can really understand.


# class File
File is defined in Ruby documentation as an abstraction of any File object accessible by our program, see [Class: File](http://https://ruby-doc.org/core-2.2.0/File.html), but what does this mean? We typically link to our code using `require` or `require_relative` so that we can read and use the data and methods within those files. Likewise, If we need to create a new file we drop over to the command line and type `touch new_code.rb`, but we have the ability to work with these files directly from within our code using `File`. This class gives us the ability to read and write code within a file, and we can even create new files and directories within our projects using `Ruby` code.

To avoid risking the chance of going to broad with this topic I decided to focus on a few 'key' methods in the File class that I think will be useful. I'm going to stick to the pattern of CRUD that we see a lot in programming, so I'll run through examples of creating files, reading files, updating them and deleting them in this post.

# Creating a File
In this example we will create a file. I have a small bit of code I have been writing while working through the book 'Grounded Rubyist'. 

```
puts "What temperature would you like to convert to Fahrenheit?"
celsius = gets.to_i
fahrenheit = (celsius * 9/5) + 32
results = "The result is: #{fahrenheit}."
```

In this file, which I named `c2f.rb`, we have a few lines of code which captures a users input of an integer that represents a temperature in degrees celsius, converts the temp to fahrenheit, and assigns the value to a variable of `fahrenheit`. That variable is then added to a string of text using interpolation and assigned to `results`, simple stuff. What we will do now is add a line of code to `create` a new file using the `File.new` method.

```
f = File.new('fahrenheit_results.rb', "w+")
```

A file with the name of `fahrenheits_result.rb` will appear in our directory after this file is executed with `ruby c2f.rb`
The `.new` method will take multiple additional arguments which are optional, but above the first is the string name of the desired file name, and the second argument is for file options or permissions. Here I used `w+` which means create this file with both reading and writing permissions.

# Write a file
Above we have successfully created a file, but at the moment its blank. We can fix this using the `.write` method. We stored an instance of the File.new to a variable `f` above. Now to write or update that file with some text we use `f.write` and pass in an argument of a string which will be printed into that page.

```
f.write("#{result}")
```

Now we will run `ruby c2f.rb`, we get prompted to supply an integer, hit enter on the keyboard, and a second later there is our new file `fahrenheit_result.rb`, and if we open it inside we will see the line of text reading.. btw, I type 80:

```
The result is: 176..
```

# Reading a file
Like all things in Ruby there are a lot of ways to do one thing, some better then others, and I will show in the next example how to get the contents of the file we created `fahrenheit_results` and read that information. We could potential use the info that gets read for other purposes which I won't be demonstrating here, i'll leave that up to you.

I've aptly named this new file `file_read.rb`. Inside this file I accessed our file using `.open` method where I passed the file name as a string argument.

```
f = File.open("fahrenheit_result.rb")
```

Now this variable of `f` doesn't hold the text from our file, but an instance of the File class. For us to be able to get to that text we will need the `.read` method. I'm using `puts` here to output that text to the console

```
puts "#{f.read}"
```

execute the code

```
ruby file_read.rb
The result is: 176.
```

Once the file is called using `ruby` we will see the output in the console with the results from our celsius to fahrenheit converter.

# Finally Deleting

Unfortunately this last method won't be a revelation for anyone, but its the final part of our basic CRUD functions using the File class. I'm going to keep this method of `.delete` simple like the rest and add a final line of code to our last file `file_read.rb`.  The file is a class method so we will need to specify the receiver as `File` followed by `.delete` where we will pass in... you guessed it, a string argument of the file name.

```
f = File.open("fahrenheit_result.rb")
puts "#{f.read}"
File.delete("fahrenheit_result.rb")
```

Once we execute this code with `ruby` will get our puts message with the results and the file with the results will be deleted. That's it.

Thanks for hanging in for this simple explanation of File and a few of the many methods it has. I appreciate it.

Take care,
Nick D
