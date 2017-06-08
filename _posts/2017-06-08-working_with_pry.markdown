---
layout: post
title:  "Working with Pry"
date:   2017-06-08 19:01:03 -0400
---


## IRB
If you are learning Ruby either from an online tutorial or book chances are you have worked with IRB. If you haven't, IRB means 'Interactive Ruby', the RB is a reference to the .rb extension of Ruby files. It's a Ruby shell that runs in the command line and it allows us to experiment with code and receive a immediate response that executes our code and shows its return value. Below we open the 'irb' shell with the command `irb`. Then we are free to experiment:

```
$ irb
2.4.0 :001 > 2 + 2
 => 4 
2.4.0 :002 > num = 2+2
 => 4 
2.4.0 :003 > num * 2
 => 8  
2.4.0 :004 > num.size
 => 8 
```

Its really wonderful, if we are curious about a return value of a method on a String, Hash, or Array class we can find out immediately using it, but after some time we will realize its limitations.


## Pry
Pry is a REPL similar to IRB, but expands upon its functionality and allows us to 'pry' into our code and see whats going on inside of our functions and methods, this makes it extremely powerful as a debugging tool.

Installing Pry
```
$ gem install pry
```

Launching Pry within the command line:
```
$ pry
```

We are then free to experiment with code just like before with IRB:
```
[1] pry(main)> 
[2] pry(main)> "foo-" + "bar"
=> "foo-bar"
```

One thing the example above doesn't show is that Pry has syntax highlighting which helps you identify what kind of data or class you are working with.

## Debugging
Let's experiment with getting inside a block of code and seeing what is going on. This is done by inserting ```binding.pry``` within the body of a function.
```
pry(main)> def string_length(str)
pry(main)*   length = str.size
pry(main)*   length
pry(main)*   binding.pry
pry(main)* end  
=> :string_length
```

Now if we call the string_length function when interpreter encounters the ```binding.pry``` it will freeze and allow us to see if our code is working as expected.
```
[20] pry(main)> string_length("Hello")

From: (pry) @ line 48 Object#string_length:

    45: def string_length(str)
    46:   length = str.size
    47:   length
 => 48:   binding.pry
    49: end

[1] pry(main)> length
=> 5
[2] pry(main)> 
```

As we can see above we can inspect the length variable to see if the ```length``` contains the supplied strings character length, and it does.

Obviously the above is very simple and probably not a unnecessary use of ```binding.pry``` . But we can see how powerful this can be once we have a more complex function that is doing more complex manipulation to data.

let's try iterating through an Array:
```
def print_array(arr)
pry(main)*   arr.each do |item|
pry(main)*     puts item
pry(main)*     binding.pry
pry(main)*   end  
pry(main)* end  
=> :print_array
```

We call the method ```print_array(["Ruby", "javaScript", "HTML", "CSS"])``` and pass an argument array of languages.

On first pass $stdout of ```puts item``` is "Ruby":
```
[10] pry(main)> print_array(["Ruby", "javaScript", "HTML", "CSS"])
Ruby

From: (pry) @ line 18 Object#print_array:

    15: def print_array(arr)
    16:   arr.each do |item|
    17:     puts item
 => 18:     binding.pry
    19:   end
    20: end

[1] pry(main)> puts item
Ruby
=> nil
```

We can step forward one iteration with command ```control + d```. Now the $stdout of ```puts item``` is:

```
pry(main)> puts item
javaScript
=> nil
```


## A few commands that help

* Clear Pry console: **control + l**
* Step forward in code block loop: **control + d**
* Exit Pry: **exit**
* Force exit Pry: **exit!**
* Escape endless loop: **control + c**







