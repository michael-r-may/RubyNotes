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
