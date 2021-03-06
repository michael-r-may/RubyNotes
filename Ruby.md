# RubyNotes
A collection of notes, tips and tricks that I want to remember when working with Ruby

Ruby devs seem to like being called Rubyists. ¯\\_(ツ)_/¯

Ruby has a special two-character symbol that is used all over the shop. It's called a rocket and it looks like this

```Ruby
=>
```

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

`greeting.length => 13`

`puts "\u{1F600}".length => 1`

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

####Constants
> A Ruby constant is like a variable, except that its value is _supposed_ to remain constant for the duration of the program. The Ruby interpreter _does not actually enforce the constancy of constants_, but it does issue a warning if a program changes the value of a constant.
Source: [rubylearning.com](http://rubylearning.com/satishtalim/ruby_constants.html)

```Ruby
A_CONST = 10
```

They should be in all upper and snake case (again, by convention only).

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

####Hashes
A hash is what we would call a Dictionary in Foundation Swift or Objective-C - a mutable unordered collection of key/value pairs.

```Ruby
event = {"id" => 1, "artist" => "Metronomy", "venue" => "The Alibi, Dalston, London"}; event['artist']
=> "Metronomy"
```

This feels like it should error but it doesn't

```Ruby
event = {"id" => 1, "artist" => "Metronomy", "venue" => "The Alibi, Dalston, London", "artist" => "Blur"}; event['artist']
=> "Blur"
event
=> {"id"=>1, "artist"=>"Blur", "venue"=>"The Alibi, Dalston, London"}
```

#####Hash Methods
######keys
Like allKeys in Foundation this returns all the keys in the hash.

```Ruby
event.keys
=> ["id", "artist", "venue"]
```

######values
Like allValues in Foundation this returns all the values in the hash.

####Symbols
It's common to use symbols as the keys for hashes. You can recognise a symbol because it is prefixed with a colon.

```Ruby
:artist
=> :artist
event[:artist]="MIA"
=> "MIA"
event
=> {"id"=>1, "artist"=>"Blur", "venue"=>"The Alibi, Dalston, London", :artist=>"MIA"}
```

Note how we now have different key/value pairs for "artist" and :artist.
 
Symbols are globally unique and immutable. Their value is basically irrelevant - it's their uniqueness that is key.

####If
If statements should look relatively familar, especially if you've done any shell scripting

```Ruby
  def magicNumbers(number)
    if number == 3
      puts 'The magic number'
    elsif number == 12
      puts 'The dirty dozen'
    elsif number == 13
      puts 'A bakers dozen'
    elsif number == 42
      puts 'The answer to life, the universe, and everything'
    else
      puts 'There is no magic here'
    end
  end
```

When your method only returns a boolean, the convention is to use a question mark suffix

```Ruby
    def isMagical?(number)
    if number == 3
      return true
    elsif number == 12
      return true
    elsif number == 13
      return true
    elsif number == 42
      return true
    end

    false
  end
```

####Binary Operators
Ruby has all of the common binary operators you would expect

``==, =, <, >, <=, >=, &&, ||``

####Nil
Much like in Objective-C and Swift, Ruby has the concept of nil.

You can get it when indexing out of an array bounds, for example.

```Ruby
ar[1]
=> nil
```

You can also check if an object is nil with the `.nil` method.

####Classes


####Credits
A great deal of the information for this came from [Ruby in 100 Minutes](http://tutorials.jumpstartlab.com/projects/ruby_in_100_minutes.html). I cannot recommend it enough as a gentle introduction.

####Further Resources
[Ruby In 20 Minutes](https://www.ruby-lang.org/en/documentation/quickstart/) 
[Try Ruby](http://tryruby.org/levels/1/challenges/0) for learning the basics of Ruby's syntax
[Getting Started With Ruby](http://guides.rubyonrails.org/getting_started.html) documentation, a really nice intro to building a simple Rails app)
[Ruby Gems](http://guides.rubygems.org/) the Ruby package management system
[Bundler](http://bundler.io/) is a tool to manage Gems
[Sinatra](http://www.sinatrarb.com/) is a framework for creating simple services
[Why's Poignant Guide To Ruby](http://www.rubyinside.com/media/poignant-guide.pdf) is a quirky introduction to Ruby
