# RubyNotes
A collection of notes, tips and tricks that I want to remember when working with Ruby

Ruby devs seem to like being called Rubyists. ¯\_(ツ)_/¯

##REPL (Read, Evaluate, Print, Loop)
The Ruby REPL is called IRB. It is bundled with every Mac.

##Variable Naming
###Imposed by Ruby

* Always start with a lowercase letter and have no spaces
* You can start a variable with an underscore though it is uncommon
* You cannot use special characters (e.g. $, @, and &)

###Common conventions
* Use [snake_case](https://en.wikipedia.org/wiki/Snake_case) 
* Name variables after the meaning of their contents, not the type of their contents
* Avoid abbreviations

##Strings
Normal strings should be wrapped in single quotes `'like this'`
Strings with interpolation should be wrapped in double quotes `"like #{this}"`
Use array index style access to get substrings. E.g.

```ruby
greeting='Hello Michael'
greeting[0]
greeting[0..4]    // from index 0 to index 4
greeting[7..-1]   // from index 7 to one before the end
```

You should favour the non-negative syntax where possible. I presume because the cognitive load is less.

####Complex String Operations
#####length
Will give you the total number of characters in the string.

`greeting.length` => 13

`puts "\u{1F600}".length` => 1

#####split
Split divides the string into separate elements delimited by space (by default). This is very similar to `NSString.componentsSeparatedByCharactersInSet`. 

`greeting.split` => ["Hello", "World"]

`greeting.split("l")` => ["He", "", "o Wor", "d"]

#####sub and gsub
AKA substitute and globally substitute. This is very similar to `NSString.stringByReplacingOccurrencesOfString:withString:` where sub does only the first occurance and gsub does all occurances.

`greeting.sub("l","L")` => "HeLlo World"

`greeting.gsub("l","L")` => "HeLLo WorLd"

#####concatenation
Join strings with +

`greeting + " of Warcraft"` => "Hello World of Warcraft"

Interpolate with #{var}

`name="Michael"; greeting = "Hi #{name}"` => "Hi Michael"

Evaluate and interpolation

`name="The answer to life, the universe, and everything is #{14*3}"` => "The answer to life, the universe, and everything is 42"

####Numbers
Ruby supports integers and floats, as you might expect. They are complex types and so can have methods called on them, as well the usual infix operator style application.

`5+2 => 7`

`5+2.0 => 7.0`

`5.methods => [:to_s, :inspect, :-@, :+, :-, :*, :/, :div, :%, :modulo,...`

Ruby will implicitly cast for you, including integers to floats. 

####Loops
For a loop of N iterations

```Ruby
5.times do
  puts "Hello, World!"
end
```

####Blocks
Ruby has blocks, just like Swift and Objective-C. They are either wrapped in do/end as we saw above

```Ruby
5.times do
  puts "do/end block :allthethings"
end
```

For single line blocks the bracket syntax is preferred

```Ruby
5.times { puts "do/end block :allthethings" }
```

But you can put multiple lines in the brackets too, so which should you use. It seems for small blocks then { } are peferred but for larger ones do/end is preferred.

`{}` also has a higher precedence order which can [sometimes make a difference](http://stackoverflow.com/a/26218840)

Note that some unexpected (to me) methods take an optional block. For example, gsub can take a block instead of second argument. 

```Ruby
"Hello World".gsub("l") { puts "there goes an l" }
there goes an l
there goes an l
there goes an l
=> "Heo Word"
```

#####Block Parameters
The example above is somewhat abusing the gsub block syntax really since it is just using it to iterate through the string and find l rather than any useful substituting (although substituting for nothing may be just what we want).

```Ruby
"hello harry".gsub("h") {|letter| letter.upcase }
=> "Hello Harry"
```

####Return
Return is implicit in Ruby. So the above block returns the uppercased letter value which becomes the value to subsitute into the string. 

####Arrays
Arrays are indexed from 0 and accessed/created using the typical square bracket syntax.

```Ruby
["Hello", "Harry"]
=> ["Hello", "Harry"]
```

```Ruby
["Hello", "Harry"][0]
=> "Hello"
```

#####Array Methods
Arrays have all the usual suspects.

```Ruby
[].methods
=> [:inspect, :to_s, :to_a, :to_ary, :frozen?, :==, :eql?...
```

Of common interest are the likes of 

######sort
Sorts strings and numbers in the way you might expect. 

######each
Iterates through each element. Like `for..in` or `for each`.

######join
Concatenates arrays together.

######index
Returns the index of an item in the array.

######include?
Checks if an item is present in the array.

######first
Returns the first item in the array

######last
Returns the last item in the array




####Credits
A great deal of the information for this came from [Ruby in 100 Minutes](http://tutorials.jumpstartlab.com/projects/ruby_in_100_minutes.html). I cannot recommend it enough as a gentle introduction.

