---
layout: post
title:  "RSpec getting started."
date:   2017-06-28 02:19:34 +0000
---

One of the most popular Ruby libraries right now is RSpec. It's a tool for applying a Test Driven Development approach to application design where we first write tests and follow up with code that meets the test expectations. It is how our labs are structured at FlatironSchool. It allows us to concentrate first on writing a solution then going back and refactoring. It takes a lot of frustration and mystery out of what isn't working with our programs.

To get started we first need to create a project folder. This can be done with the terminal command '`mkdir`' followed by the name of our project folder. I've chosen to name mine 'tdd-project', but its up to you to choose one of your own or use an existing project if you want.

`$ mkdir tdd-project`

Once we have a project folder setup we can 'change directory' and move inside of our project folder using the '`cd`' bash command:

`$ cd tdd-project`

Now let's start by giving our project another directory to store our Ruby program files using once more the '`mkdir`' command:

```
$ mkdir lib
```

The `'lib/`' folder will contain our Ruby files. This is where we will be writing the code that meets the expectations of our RSPEC tests. 

Now that we have a folder for our Ruby program files lets install the gem RSpec, type: 

`$ gem install rspec`

We should see the following or something similar that lets us know that RSpec was successfully installed and the version number that was installed.

```
Successfully installed rspec-3.6.0
Parsing documentation for rspec-3.6.0
Installing ri documentation for rspec-3.6.0
Done installing documentation for rspec after 0 seconds
1 gem installed
```

Great Success! RSpec installed and we see the version installed was rsepc-3.6.0. Now we need to setup our project to use RSpec, lets run the following command:

`$ rspec --init`

```
create   .rspec
create   spec/spec_helper.rb
```

This will create a `.rspec` file and a directory called `spec/` with a file called `spec_helper.rb`. If we type the commad `ls` this will list the files and folders in our directory, right now our project folder should look like this:

```
$ ls
config	lib	spec
```

And if we want to see the hidden .rpsec file, we use the command `ls -la` that lists with long format and shows hidden files with permissions.

# Writing our first spec.
Lets take a moment and talk about tests. A test should express a 'single' expectation. This helps keep our tests to one specified behavior at a time, and this will help us was we are developing to find the error for the failing test and write the code to meet the expectation then move to the next one.

To keep things very simple at first we are going to write a spec test for a method called #hello_world, very original I know. So lets create an .rb file first for our code that will be tested:

`$ touch lib/hello_world.rb`

Now we need to create a spec .rb file in our `spec/` directory for our tests:

`$ touch spec/01_hello_world.spec.rb`

We need to require our `lib/hello_world.rb` file inside of the `spec_helper.rb` file for our tests to run. Using your text editor add the following line at the top of the file:

`require_relative "../lib/hello_world"`

Now open up the` 01_hello_world_spec.rb file` and add at the top:

`require	'spec_helper'`

# Writing the test.

Finally, we are ready to write our first test, and we start by describing what it is we are testing. Here we are describing the #hello_world method. We do this with the a `describe` block which has a parameter of a `String` which tells the user what we are describing, followed by a code block using the `do / end`. 

```
describe '#hello_world' do

end
```

Next comes the `context` block, it will help with keeping our tests organized and clear to us and others on what the expectation for this method is. What is our expectation for #hello_world? I think we can agree it should output a string of 'Hello World!', and that is exactly what we will test for, that very specific string which includes capitalization and ending with an exclamation mark.

This `context` block goes inside of the describe block and starts with the keyword `it` followed with a String parameter also just like the `describe` block. The parameter for the context block states the action of calling the method `hello_world`. The actual test goes inside of the `context` block and its syntax can change depending on what we are testing. 

```
describe '#hello_world' do
	it 'when called' do
		
		expect{hello_world}.to output("Hello World!\n").to_stdout

	end
end
```

* Quick note on why the `\n` at the end of the string `Hello World!\n`. Its a newline return which is added to the end of a string when you use the `puts` method. This can be removed a few ways like using the .`chomp` method, but we are wanting to test for a simple `puts` output and know to add this character in our expectation.

# Running our test

We have our test defined inside of our 01_hello_world.spec.rb file and now it is time to run it, type `rspec spec` or `rspec spec/01_hello_world_spec.rb`. You should see the following:

```
rspec spec/
F

Failures:

  1) #hello_world when called
     Failure/Error: expect{hello_world}.to output("Hello World!\n").to_stdout
     
     NameError:
       undefined local variable or method `hello_world' for #<RSpec::ExampleGroups::HelloWorld:0x007fc34f042828>
     # ./spec/001_hello_world_spec.rb:6:in `block (3 levels) in <top (required)>'
     # ./spec/001_hello_world_spec.rb:6:in `block (2 levels) in <top (required)>'

Finished in 0.00309 seconds (files took 0.09995 seconds to load)
1 example, 1 failure

Failed examples:

rspec ./spec/001_hello_world_spec.rb:4 # #hello_world when called
```

Great it failed! We see above we have 1 example, 1 failure so our test ran and failed. We see the error was a NameError which is an undefined local variable or method 'hello_world'. If we look a little further up at the error message we see our String parameters from the `describe` and `context `blocks we defined in the spec file.

# Passing the test
We have defined our test and now its time to fix that failure and write some code that meets the expected output of #hello_world. We know from running our test the error received was NameError undefined local variable or method, so this one is easy to solve because #hello_world is a method that has yet to be defined. Open the file `lib/hello_world.rb` in your text editor and lets get started.

First, define a method hello_world

```
def hello_world
	# code here
end
```

Next, lets look at our error again: `Failure/Error: expect{hello_world}.to output("Hello World!\n").to_stdout` If we remember `puts` method is short for ('put string') and it outputs using standard output. I think its clear that we need to output` 'Hello World!'`

```
def hello_world
	puts "Hello World!"
end
```

Fingers crossed, lets run that test once more, type `rspec spec` or `rspec spec/01_hello_world_spec.rb`...

```
 rspec spec/
.

Finished in 0.00314 seconds (files took 0.09703 seconds to load)
1 example, 0 failures
```

Yay!! We did it. Awesome job. We installed and setup RSpec, coded our first test, and finally wrote the code which passed and meet the expectations defined. 

Just to keep these steps fresh in our mind lets break them down again.

We:
1. Setup our project directory.
2. Installed RSpec gem
3. Setup the project to use RSpec.
4. Created a .rb file in our lib/ directory for code.
5. Created a .rb file for our test spec in spec/ directory
6. Described What we are testing.
7. Stated the context and expectation for our test.
8. Ran RSpec and failed
9. Coded the solution to the test
10. Ran rspec again and passed.

That was a lot and its only the beginning. I hope this is helpfully and below are some links to other resources to help you on your journey to learning more about Test Driven Development.

http://rspec.info/ 
http://www.betterspecs.org/

Take Care
-Nick D






