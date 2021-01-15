### Phase 3

- [Ruby Intro](#intro)
- [Ruby Variable Types and Mehods](#variables)
- [Ruby Debugging](#debugging)
- [Ruby Arrays](#arrays)
- [Object-Orientation in Ruby](#oo)
- [Ruby OO Review](#oo-review)
- [Ruby One to Many Relationships](#one-to-many)
- [Ruby Many to Many Relationships](#many-to-many)
- [Ruby Has Many Through Review](#has-many-through)
- [Ruby Intro to Inheritance Review](#inheritance)
- [Ruby Modules](#modules)
- [Ruby Hashes and the Internet](#hashes-and-internet)
- [Ruby Test-Driven Development](#tdd)
- [SQL Intro](#sql)
- [ORMs Intro](#orms)
- [ORMs Review](#orms-review)
- [Dynamic ORMs](#dynamic-orms)
- [Active Record Intro](#ar)
- [Active Record Associations](#ara)

## Lecture Notes

---
title: Intro To Ruby
layout: post
---

# <a id="intror">Intro to Ruby</a>

## SWBATS

- Use the Learn IDE
- Create and run a ruby program
- Differentiate plaintext and richtext
- Calmly read and debug error messages

## Overview

```
5m Introduction to the Sandbox
5m Introduction to Ruby and IRB
5m Our First Program
10m Reading Error Messages
--
20m Total
```

### The Learn IDE

- Introduce the sandbox
- Explain that we can create files
- Demonstrate that we can edit and save the files
- Demonstrate the ruby REPL
- Demonstrate running a ruby file from the command line

### Intro to Ruby

- Overview of what a programming language is
  - A set of instructions that tell the computer what to do
  - For Ruby, a program that reads in our code (from a text file), and executes it 
- Rich text vs. Plaintext
- Ruby on the REPL
- Code-along: evaluate some expressions in irb

## Our first program

- In the grand tradition of programmers, let's print 'hello world' from `hello_world.rb`

`puts "hello, world"`

- run with `ruby hello_world.rb`
- What did this program do?
- What is `puts`?
- Why do we need to put `"hello, world"` in quotes?
- Strings vs. Code

## Fast Feedback Loop and Reading Error Messages

- Introduce the fast feedback loop
- Introduce learn gem and TDD
- We want to write a small piece of code, then run it to see if it works
- When we get an error, hooray! We know what the next step should be.
- How to deal with an error:

1. Breathe - errors are good!
2. Read the error message - if it tells you what to fix, fix it!
3. If you don't understand the error message, _Google_!
4. If you still don't understand, ask your neighbor / an instructor

## Debugging

- Sometimes, the program isn't working, but we **don't have an error message**
- This is much worse! We don't know what to fix. (Emphasize that errors are good)
- How do we debug?

1. Breathe - debugging is a chance to learn!
2. Form a hypothesis for what is happening. E.g. "I think that the variable is not defined"
3. Check your hypothesis. E.g. `puts` the variable to see what the value is
4. If your hypothesis is right (e.g. the variable was not defined), then you can fix the bug. If your hypothesis is wrong, you have to _locate the bug_ before you can fix it. Go back to step 2 - don't flail.

### Common Ruby errors:

```text
- Syntax Errors
    - unexpected end-of-input, expecting keyword_end 
    - ruby doesn't understand what we typed!
    - Fix is to change our syntax so that it is valid ruby
- NoMethodError
    - Undefined ** for Nil Class
    - Undefined local variable or method
    - You're trying to use a name that ruby doesn't know about
    - Check if that name is defined
- TypeError:
    - 1 + "1" => String can't be coerced into Fixnum
    - Those things don't belong together
    - Ruby doesn't know how you want to do that thing
    - Should `1 + "1"` equal `2` or `"11"`?
```

### Labs
- [Hello World](https://learn.co/tracks/full-stack-web-development-v6/intro-to-ruby-development/intro-to-programming/hello-world)
- [Welcome to Tic Tac Toe](https://learn.co/tracks/full-stack-web-development-v6/intro-to-ruby-development/intro-to-programming/welcome-to-tic-tac-toe)
- [Reading Error Messages](https://learn.co/tracks/full-stack-web-development-v6/intro-to-ruby-development/debugging/reading-error-messages)

---
title: Ruby Variables Types Methods
layout: post
---

# <a id="variables">Ruby Variables, Types, and Methods</a>

## SWBATS
- assign names to values with variables
- create numbers
- use the basic number operators - `+`, `-`, `*`, `/`
- distinguish strings from code
- use basic string methods, `+`, `.length`, `.downcase`, `.upcase`
- create arrays, add elements, and access them
- recognize `nil` values
- define methods with `def`

## Outline 

```text
 5m Introduce Variables and Types
 5m Demonstrate number methods
 5m Strings and String Methods
 5m Arrays and array access
 5m Booleans and Nil
10m Methods
--
35m Total
```

## Variables

- When we use `""` to create a string, or mention a number like `5`, we are using it _literally_
- We don't always know what the value is going to be when we are writing the program - we need a way to refer to data without using the literal value
- We can use _variables_! 
- In ruby, we can assign a name to a value like `name="Rob"` or `number=6`
- Then, when we mention `name` or `number` later, we get the value out!
- Demonstrate in REPL
- Demonstrate in ruby files

```ruby
> name = "Rob"
=> "Rob"
> name
=> "Rob"
> number = 6
=> 6
> number
6
```


## Types: Strings, Numbers, Arrays

- When we are programming, our values have different _types_
- We want to do different operations depending on what kind of data something is
- If it's a number, we want to do "mathy" things with it
- If it's text, we want to do "texty" things with it
- We're going to focus on Numbers, Strings, and Arrays

### Numbers

- We can create a number in ruby by typing the number - `5` or `-100` or `61342`
- Ruby also knows how to do math
- We can use operations like `+` and `*` and `-` and `/`

```ruby
> 5 + 5
=> 10
> 3 * 4
=> 12
> 9 - 8
=> 1
> 100 / 10
> 10
```

- Ruby also knows some more fancy operators!

- `**` for exponents:

```ruby
> 6 ** 2
=> 36
> 8 ** 2
=> 64
> 3 ** 3
=> 27
```

What other operators can you find? Try looking up more ruby number operators with Google and the Ruby docs!

### Strings
- In order to distinguish the _text we want to print_ from the _code that we want to execute_, we wrap our words in `"quote marks"`.
- In ruby, these _things in quotes_ are called **Strings**
- What kinds of operations can we do on Strings?

`+` adds strings together:

```ruby
> "cat" + "dog"
=> "catdog"
> "I'm going to the" + " store " + " to buy " + " some groceries " + "."
```

`.length` reports on the string's length:

```ruby
> "abracadabra".length
=> 11
> "Zap".length
=> 3
> "Zap!".length
=> 4
```

`.upcase` creates an UPPERCASE version of the string
```ruby
> "shouting".upcase
=> "SHOUTING"
```

Similarly, `.downcase` returns a lowercase version

```ruby
> "ALAKAZAM!".downcase
=> "alakazam!"
```

There are lots of other string methods! Browse the ruby docs to see more.

### Arrays 

- Arrays are lists of values
- We use `[]` to create arrays


```ruby
> array = [1,2,3]
=> [1,2,3]
```

- We can add new values to the array with the `<<` "shovel" method

```ruby
> array << 4
=> [1,2,3,4]
```

- We can get an item out of the array ('access' it) with `[]`

```ruby
> array[0]
=> 1
> array[1]
=> 2
```

- Notice that array indices start at `0` - the first element is the 0th element, the second element has index `1`, etc.



### Nil
- Sometimes we want to represent that 'nothing is there'
- We use a special value `nil` to mean 'nothing'

```ruby
> nil
=> nil
```

It'll pop up, so that's what it means when you see it.

## Methods

- Typing everything that happens every time is annoying
- DRY - don't repeat yourself!
- Instead of copying and pasting, lets write a method!
- A _method_ in ruby is a set of instructions that we can run later (the word _function_ is used interchangeably)
- we create a method with 

```ruby
def greet
  # body of method
  puts "Hello, world!"
end
```

- We run the method ("call" or "invoke" the method) by calling its name

```ruby
greet
```

## Arguments

- We want to be able to customize our methods
- Methods can take input
- We declare what _arguments_ a method takes when we define the method
- We can refer to those arguments in the body of the method, and customize what the method does

```ruby
def greet_person(name)
  puts "Hello, " + name
end
```

- Then we "pass in" values when we call the method

```ruby
greet_person("Rob")
```

If we want methods to accept more than one argument, we mention multiple arguments when we define the method
```ruby
def print_product(first, second)
  puts first * second
end

print_product(6, 7)
```

The order of the values that we pass in is important! Each argument will get 'matched up' with the argument in that position in the method's definition.

```ruby
def print_in_order(name_one, name_two, name_three, name_four)
  puts "Hello " + name_one
  puts "Welcome " + name_two
  puts "Hi " + name_three
  puts "Greetings, " + name_four
end

print_in_order("Hillary", "Jake", "Ann", "Rob")
```

If we pass in the values in a different order, the values will be assigned to different names in the body of the method

```ruby
print_in_order("Rob", "Hillary", "Jake", "Ann")
print_in_order("Ann", "Rob", "Hillary", "Jake")
```

### Labs
- [Variable Assignment Lab](https://learn.co/tracks/full-stack-web-development-v6/intro-to-ruby-development/variables/variable-assignment-lab)
- [Tic Tac Toe Board](https://learn.co/tracks/full-stack-web-development-v6/intro-to-ruby-development/variables/tic-tac-toe-board)
- [Say Hello](https://learn.co/tracks/full-stack-web-development-v6/intro-to-ruby-development/methods/say-hello)
- [Display Tic Tac Toe Board](https://learn.co/tracks/full-stack-web-development-v6/intro-to-ruby-development/methods/display-tic-tac-toe-board)

---
title: Ruby Debugging
layout: post
---

# <a id="debugging">ruby-debugging</a>

## Debugging in Ruby

### SWBATs

### Resources

### Example Video

### Outline

Title: Debugging Creator: Yomi Lajide &lt;@Joll59&gt; Type: Notes

How to use your team members time effectively

```text
- WHAT is the error message?
    - What does it say?
    - What method/what line of code is affected?
- WHAT are you aiming to accomplish?
- Have you confirmed your assumptions (re: variable values/types, etc.)
- What am I doing with the argument given by the specs?
    - Side Note
        - Parameter is variable in the declaration of function.
        - Argument is the actual value of this variable that gets passed to function.
- Have you looked at the documentation?
- WHERE is binding.pry?
```

Common Ruby errors:

```text
- NoMethodError
    - Undefined ** for Nil Class
    - Undefined local variable or method
- Syntax Errors
    - unexpected end-of-input, expecting keyword_end    - TypeError:
    - 1 + "1" => String can't be coerced into Fixnum
- Division Errors:
    - (1/0) => ZeroDivisionError: divided by 0.
- ArgumentError:
    - Wrong number of arguments(given 0, expected 1)
```

```ruby
begin
    # Any exceptions in here...
    1/0
  rescue => e
    puts "Exception Class: #{ e.class.name }"
    puts "Exception Message: #{ e.message }"
    puts "Cause: #{e.cause}"
  end
```

## Using Pry/Pry-byebug:

### Pry [screencast](https://vimeo.com/26391171)

### Pry-byebug Documentation can be found [here](https://github.com/deivid-rodriguez/pry-byebug)

Lets take a quick look at some functionality of Pry.

```text
$ pry
[1] pry(main)> help
```

You can take a closer look at these commands by appending `-help`

As you can see, Byebug is included here as well, as pry-byebug brings in all of byebugs improved functionality into pry. Adding `next` ,`step`, `finish` and `continue` commands to Pry for stepping through your program's code and `up`, `down` and `frame` commands for callstack navigation.

To alias these commands add these lines to your ~/.pryrc file.

```text
if defined?(PryByebug)
  Pry.commands.alias_command 'c', 'continue'
  Pry.commands.alias_command 's', 'step'
  Pry.commands.alias_command 'n', 'next'
  Pry.commands.alias_command 'f', 'finish'
end
```

Commands to be mindful of:

1. binding.pry, obj.pry
2. `cd`, `ls`, `help`, `.`, `cd -`
3. `reload-code`
4. `!!!`,`!!@`
5. `$`,`?`,`@` `[show-source,show-doc,whereami]`
6. `c`,`f`,`n`,`s` `[continue,forward,next,step]`_all alias provided by byebug_
7. `hist`, `hist --replay`, `hist --show`, `hist --clear` `[enter line number as argument and you can enter a range]`
8. `nesting`, `jump-to` 

---
title: Ruby Arrays Fasttrack
layout: post
---

# <a id="arrays">Arrays and Array Methods</a>

## SWBATs

* Create and populate an array
* Retrieve items from an array
* Identify elements in an array based on their index number
* Add to an array, destructively and non-destructively
* Delete from an array, destructively and non-destructively

## Outline

```text
5m Introduce topic
10m - Array CRUD

===
15m Total
```

### Introduce topic

* Array is like a list or a basket, it can hold values
* Keeps us from having to assign multiple similar variables

  ```ruby
  student1 = "Harry Potter"
  student2 = "Ron Weasley"
  student3 = "Hermione Granger"
  student4 = "Draco Malfoy"

  students = ["Harry Potter", "Ron Weasley", "Hermione Granger", "Draco Malfoy"]
  ```

* Arrays can hold any kind of value
* Strings, Numbers, booleans, nil, or a mix!

### Array CRUD

#### Creating an array

```ruby
  # literal constructor
  my_array = []
```

#### Reading from an array

- You can use the index of an array element to read from it.
- Arrays start at index[0]

```ruby
  instructors = ["Rob", "Humzah", "Ann", "Hillary"]
  puts instructors[0] #=> "Rob"
  puts instructors[1] #=> "Humzah"
  puts instructors[2] #=> "Ann" 
  puts instructors[3] #=> "Hillary"
  puts instructors[4] #=> nil
```

- See that last one? If we try to access an element that doesn't exist, we get back `nil`

- What about if we wanted to get elements from the end of the array?
- Well, we could get the array's length with `.length`
- and then use `.length - 1` to get the last element

```ruby
  instructors = ["Rob", "Humzah", "Ann", "Hillary"]
  instructors.length #=> 4
  instructors[instructors.length - 1] #=> "Hillary"
```

- Ruby gives us a shortcut!
- If we access the array at `-1`, we'll get from the end

```ruby
instructors = ["Rob", "Humzah", "Ann", "Hillary"]
instructors[-1] #=> "Hillary"
```

#### Changing what's in an array

- We can add to an array with the `<<` 'shovel'

```ruby
  # Shovel Method
  famous_cats = ["lil' bub", "grumpy cat", "Maru"]
  famous_cats << "nala cat"
  puts famous_cats.inspect
  # > ["lil' bub", "grumpy cat", "Maru", "nala cat"]
```

- Or we can add with `push`

```ruby
  #.push Method
  famous_cats = ["lil' bub", "grumpy cat", "Maru"]
  famous_cats.push("nala cat")
  puts famous_cats.inspect
  # > ["lil' bub", "grumpy cat", "Maru", "nala cat"]
```

- If we want to add to the _front_ of the array, we can use `unshift`

```ruby
  #.unshift Method
  famous_cats = ["lil' bub", "grumpy cat", "Maru"]   
  famous_cats.unshift("nala cat")
  puts famous_cats.inspect
  # > ["nala cat", "lil' bub", "grumpy cat", "Maru"]
```

- Why is it called `unshift`?
- Because `shift` removes the first element from the array!

```ruby
  #.shift
  famous_cats = ["lil' bub", "grumpy cat", "Maru"]
  lil_bub = famous_cats.shift

  puts famous_cats.inspect
  # > ["grumpy cat", "Maru"]
  puts lil_bub
  # > lil' bub
    #note .shift has a return value of the element that was removed from the array
```

- The opposite operation from `push` is called `pop`
- It 'pops' an item off of the end of the array

```ruby
  #.pop method
  famous_cats = ["lil' bub", "grumpy cat", "Maru"]
  maru_cat = famous_cats.pop
  puts famous_cats.inspect
  # > ["lil' bub", "grumpy cat"]
  puts maru_cat
  # > Maru
  #note .pop has a return value of the element that was removed from the array
```

---
title: Ruby Oo
layout: post
---

# <a id="oo">ruby-oo</a>

You can start with an empty rb file. You'll want to use Pry in some way to run/debug your code, so maybe have a Gemfile with `gem "Pry"`.

## SWBATs

* Define `object` in programming domain
* Explain the concept of sending messages
* Create a class and instantiate an instance of the class
* Explain the difference between a class and an instance
* Pass arguments to `new` by defining an initialize method in class
* Create instance methods
* Call methods on the implicit or explicit `self`
* Define attribute readers and writers using `attr_` macros
* Get more practice with array compositions \(`each`, `map`, `select`/`filter`\)
* Explain the need for variable scope and why it's important to not utilize global variables

## Resources

* [Example Video](https://youtu.be/Zk37IdHYz2E)
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/ruby/intro-oo)

## Outline

```text
15m Everything is an Object in Ruby
10m What is an object?
35m Creating our own Objects
===
 1h Total
```

### Everything is an Object in Ruby

_"Everything in Ruby is an object."_ What does that mean? Go through some example code, and ask students to break down what's happening at each level:

```ruby
# what is the data type of x?
# what is the value of x?
x = 3
puts x.class
puts x

# what happens when we run this code?
# what is split and where does it come from?
# how does x know what to do with split?
# what's happening when we run this code?
x = "hello how are you"
x.split
```

Methods, on a lower level, are known as "messages" in object-oriented programming. Methods are called _on_ objects and messages are sent _to_ objects. Objects respond to messages by doing some work. The exact work that it should do is _defined_ on the object's class.

[https://ruby-doc.org/core-2.5.0/Object.html\#method-i-send](https://ruby-doc.org/core-2.5.0/Object.html#method-i-send)

```ruby
x = 3

# what does message name mean here?
message_name = :+

# what does send do?
# what does the argument to send specify?
# what other arguments does send take?
x.send(message_name, 1) === x + 1

# most operators in Ruby are just messages sent to objects
names = [
  "Ian",
  "Sophie",
  "JJ",
  "Rishi",
  "Johann",
  "Esmery",
  "Terrance"
]
names[0]
names.[](0)
names.send(:[], 0)

# objects complain when they don't know how to respond to messages
# objects complain when they don't know how to execute methods
names.respond_to_undefined_method

# check if an object responds to a message
names.responds_to? message_name
```

Why is it important to remember everything is an object in ruby? Because everything can respond to a message. If you have a background in C or Java, 1.odd? seems bizarre; know that not all languages have this functionality but we get to use it in ruby.

### What is an object?

Generally, an object is a copy of some class template. We can make generic objects with `Object.new()` and Ruby assigns this object an `id` to this object in the computer's memory. Ask the students to reason through uniqueness and why each object would have an `id`.

```ruby
o = Object.new # <Object:0x007f870d02d550>
o.object_id # 70109007801000

# Where does object ID come from?
# https://stackoverflow.com/questions/2818602/in-ruby-why-does-inspect-print-out-some-kind-of-object-id-which-is-different
(o.object_id * 2).to_s(16) # 7f870d02d550
"%x" % (o.object_id << 1) # 7f870d02d550
```

Objects keep track of and define how to update their personal state. Objects have their own scope rules.

### Creating our own Objects

Why do we want to do this? Give examples of cases where you want to repeat specific functionality about an entity, but you don't want to write your code over and over again.

_Remember, programming is about removing simple, repetitive decisions so that we can focus on harder, higher-order problems. Whenever you have to do something more than once, you should probably automate it._

Let's make an object. This is a fun way to let the class give you input. For this example, we'll use `BankAccount`. First, try storing all of that metadata in a hash.

```ruby
bank_account = {"user_id": 3, "balance": 100}
```

Why is this inefficient?

* You might have typos, which breaks the schema.
* Changing properties on the hash requires accessing attributes using `[]` syntax.

Build up to a more full bank account model following the example below. Keep in mind, many students may not have seen `attr_` macros, class methods, `initialize`, and class and instance variables. Define each of these through your steps leading up to the following code.

```ruby
class BankAccount
  attr_reader :user_id, :balance

  @@all = []

  def initialize(user_id, balance)
    @user_id = user_id
    @balance = balance

    @@all << self
  end

  def deposit(amount)
    @balance = @balance+amount
  end

  def widthdraw(amount)
    @balance = @balance-amount
  end

  def self.all
    @@all
  end
end
```

Here is a recommended order to go over each of these concepts:

1. `initialize` with `@user_id` and `@balance` as instance variables _You should discuss how scoping works and how instance variables live in the scope of the class. Demo this by accessing this variable in another method like _`deposit`_._
2. Create custom getters and setters for instance properties. Then show `attr_accessor` macro to add getters and setters to your instance variables, and `attr_reader` and `attr_writer` to be more specfic.
3. Add `@@all` as a class variable that lives outside each instance. This is an opportunity to hold on to all of the created instances of this class in memory in a place that is separate from each of the instances themselves. When adding new instances add `@@all << self` to `initialize`.
4. Adding a method that interacts with one of the instance methods. This showcases implicit `self`. This is a good chance to use defined getters and setters inside of other methods to understand how Ruby interprets variables / method calls more deeply.
5. What is `self` in each context? Use `binding.pry` to show that `self` is the class outside of any method, and use that intuition to write `BankAccount.all`. You can show that `BankAccount.new` is also a class method.

Once you've got some fun objects to play with, you can do array operations on `BankAccount.all`! Have the students do some `map`, `select`, `find`, and `each` commands with you.

---
title: Ruby Oo Review
layout: post
---

# <a id="oo-review">ruby-oo-review</a>

## SWBATs

* Build a class isolated from other class with
  * Instance methods
  * Class methods
  * Instance variables
  * Class variables
  * Readers/Writers/Accessors
* Call methods from one class inside other classes
* Distinguish instance variable versus getter/setter method behavior
* Explain the need for using the explicit `self`

## Resources

* [Example Video](https://youtu.be/2QtVGS_m290)
  * The domain in this video is different than below, but as with reviews or any other lecture, feel free to use your own domain or get one from the class
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/ruby/oo-review)

## Outline

```text
10m Build Bank Account Class
10m When to Use Self
10m Instance Variables v Getters/Setters
20m Exercise: Build Transfer Class Related to Bank Account
===
40m Total
```

### Building Bank Account Class

* At some point you will get stuck because you spelled `initialize` wrong
  * Use `dfi` shortcut
* Start with attr\_accessors and then scope down what you don't need
* talk about the `@@all` that clarify that this is acting as pseudo-database

```ruby
def deposit(amount)
  self.balance += amount
end

def display_balance
  "Your balance is $#{balance}."
end
```

### When to Use Self

* Why does `deposit` need to use `self.balance`?
* It has to do with how Ruby processes barewords
* First it checks for local variables then methods
* `balance += amount` is shorthand for `balance = balance + amount`
* Ruby reads this as setting a local variable `balance`
* Since `balance` is being defined circularly, it never gets assigned a value
* Since it has no value, we can't use the addition operator on it
* We get the error: `NoMethodError: undefined method '+' for nil:NilClass`

### Instance Variables or Setter/Getter Methods

* With all this confusion, why not just use instance variables?
* Remember we like to fail loudly

> Inside one of the instance methods, try calling `dog` and `@dog`.

* `dog` returns `NameError: undefined local variable or method 'dog' for #<BankAccount:0x007faab901fca0>`
* `@dog` returns nil because you are telling Ruby to look for a variable which has not been defined
* We want the error, we don't want to track down where a `nil` is coming from

### Transfer Class

* Make sure to think of the real world situation
  * Checking the sender balance stumps everyone

```ruby
def execute_transaction
  if status == "pending" && sender.valid? && sender.balance > amount
    sender.balance -= amount
    receiver.balance += amount
    self.status = "complete"
  else
    self.status = "rejected"
    "Transaction rejected. Please check your account balance."
  end
end
```

---
title: Ruby One To Many Relationships
layout: post
---

# <a id="one-to-many">ruby-one-to-many-relationships</a>

## SWBATs

* Implement one object to many objects relationship
  * One object has many objects
  * One object belongs to another object
* Practice passing custom objects as arguments to methods
* Demonstrate single source of truth
* Infer type of method \(class or instance\) through naming conventions

## Resources

* [Example video](https://youtu.be/69PMa8I_P7E)
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/ruby/one-to-many)
  * This starter code has a `run.rb` file, so this is a good lecture to introduce a single point of entry for the app if you haven't already.
  * If you choose not to use the starter code, it's an opportunity to ask the students to give you prompts and become more invested in the code.

## Outline

```text
15m Introduce topic
 5m Introduce deliverables
10m Build the classes
10m Explore single source of truth
10m Student exercise
10m Review exercise
10m More on objects and methods (optional)
===
70m Total
```

### Introduce topic

* _Model_: A class whose primary responsibility is to store data
* _Domain_: The subject matter of the problem, \(e.g., Learn's domain is online education\)
* _Domain modeling_: Creating models for your domain to represent real or abstract ideas \(e.g., Learn's domain model includes modules, cohorts, assignments as well as their relationships\)
* _Relationships_: How one model or thing is connected to another model or thing
  * _One to many relationship_: A relationship describing a single model that contains or keeps track of other models \(a tree has many leaves, an organism has many cells, the universe has many galaxies\)
  * _Many to many relationship_: Next time
  * _Other relationships_: Next time

_Why do we care so much about codifying and being really specific about the terminology of has-many/belongs-to?_ The terms are very powerful because we can use the same idea to describe relationships across many different types of domains. The relationship between artist and song, is the same as book and author, user and tweets, etc.

I'll draw out some simple domain diagrams using [web whiteboard](https://awwapp.com/) or [draw.io](https://www.draw.io/)

### Introduce deliverables

```text
* Create a User class. The class should have these methods:
  * `User#initialize` which takes a username
  * `User#username` reader method
  * `User#tweets` that returns an array of Tweet instances
  * `User#post_tweet` that takes a message, creates a new tweet, and adds it to the user's tweet collection
* Create a Tweet class. The class should have these methods:
  * `Tweet#message` that returns a string
  * `Tweet#user` that returns an instance of the user class
  * `Tweet.all` that returns all the Tweets created.
  * `Tweet#username` that returns the username of the tweet's user
```

> **Note:** We are no longer in the world where something something like `song.artists` would return an array of strings of song names. We are now always favoring objects going forward. In this example, expect `user.tweets` to return a collection of _Tweet instances_

### Build the classes

Set up a `run.rb` file to be the _single point of entry_ for your application. This file should require the other two and you should run `ruby run.rb` in the terminal to test your application generally.

Get outlines for classes in their own files, and write method definitions without method bodies at first. Start building the `User` class without a single source of truth.

To test the code I'll make an example Twitter User. I show [coffee\_dad](https://twitter.com/coffee_dad). Nice short tweets to type such as 'having coffee'

```ruby
class User

  attr_reader :username, :tweets

  def initialize(usernmae)
    @username = username
    @tweets = [] # this is the idea that we will remove later
  end

  def post_tweet(message)
    # create a new tweet
    tweet = Tweet.new(message, self)
    # add that tweet to this users collection of tweets
    add_tweet(tweet)
  end

  private

  def add_tweet(tweet)
    self.tweets << tweet
  end

end

class Tweet
  attr_reader :message, :user

  @@all = []

  def initialize(message, user)
    @message = message
    @user = user

    @@all << self
  end

  def self.all
    @@all
  end
end
```

### Explore single source of truth

Demonstrate why we want single source of truth...

* Create a user and have that user post a few tweets.
* Remove a tweet from `Tweet.all`.
* Call `user.tweets` to see it's still there.

There's not a single source of truth here. Does that tweet still belong to the user or not? Which class has the responsibility of knowing definitively which tweets exist. The Tweet class seems a better choice. Lets have that be the SSoT.

### Student exercise

> **Exercise** Allow the students to continue working on the deliverables provided at the beginning of the survey.

### Review exercise

After they get this the `post_tweet` method can be significantly simplified utilizing single source of truth. Talk a little bit about how SSoT relates to Ruby code but also foreshadow the use of relational databases, where SSoT really shines.

```ruby
class User
  # ...

  def tweets
    Tweet.all.select do |tweet|
      # Q: what would tweet.user.class return??
      tweet.user == self
    end
  end

  def post_tweet(message)
    Tweet.new(self, message)
  end
end
```

### More on objects and methods

* Implicit receivers
  * ruby will try to send the method to `self` if it doesn't have a local variable
  * Three types of things in Ruby
    * data
    * Ruby keywords
    * bare words that are defined
  * Where does puts come from?
    * Module called 'Kernel' which communicates with printing to the screen - this method is defined there
    * We're really calling 'self.puts'
  * _Must use explicit receiver with = method_ -&gt; show why
    * When you need the explicit receiver
  * private methods
    * Add additional methods to organize my code better
    * Make it more readable
    * Imagine a codebase with hundreds or thousands of files - you don't want other programmers to use those methods
    * The method were just for readability
    * Try to use them to make this read like a story
    * What makes a method private?
      * It can only be called on the implicit `self`

---
title: Ruby Has Many Through Review
layout: post
---

# <a id="has-many-through">ruby-has-many-through-review</a>

## Has Many ... Through


### Outline

Title: Has Many Through Review Creator: Niky Morgan &lt;@nikymorg&gt; Type: Review

## Learning Objectives

* Calling methods inside other classes
* Understanding the benefit of "through" relationships
* Single Source of Truth

### Tips

* Run one test at a time with `rspec --f-f`
* To start, do the minimum the test needs to pass
* At some point you will get stuck because you spelled `initialize` wrong
  * Use `dfi` shortcut
* Start with attr\_accessors and then scope down what you don't need

### Common Confusions

* You can call a method belonging to another class inside another class or instance
* You can call a method belonging to an instance of another class inside another class or instance if you have access to that instance
* Be aware of the data types of arguments and returns
* If two instances are related \(a song and a genre\), you will need to tell each instance that it is related to the other

## Artist

* Follow the tests to set up `initialize`

#### add\_song

* Tell the song about the artist
* Tell the artist about the song
* What data is the test passing through to add\_song?

```ruby
def add_song(song)
  song.artist = self
  self.songs << song
end
```

#### genres

* Single Source of Truth and DRY
* Without "through" we'd have a more complicated workflow
* Artist records a new song in a new genres
  * Add genre to artist.genre
  * Add artist to genre.artists
  * Add song to artist.songs
  * Add artist to song.artists
  * Add genre to song
  * Add song to genres.songs

```ruby
def genres
  songs.map{|song| song.genre}.uniq
end
```

## Genres

* Follow the tests to set up `initialize`

#### songs

* We've created a reader method for `songs`, but we never write to it
* When/where does it make the most sense to connect songs and genres?

#### artists

* Why am I not making @artists a separate instance variable with separate attr\_accessors?
* If we keep all these independent, we are more likely to have issues in the long run
  * More moving parts, more places to update

---
title: Intro Inheritance Oo Pets Review
layout: post
---

# <a id="inheritance">ruby-object-architecture</a>

## SWBATs

* Modules and Inheritance

## Resources

* [Example video](https://youtu.be/MLj9PeC8wuI)
* [Starter Code](https://github.com/learn-co-curriculum/my-pets-modules-redo-starter)

## Outline

```text
Run the specs and see the pattern
Slowly refactor
What if one of the classes needed some custom behavior?
Modules
```

### Run the Specs and see the pattern

```text
Cat
  can initialize a cat
  initializes with a name
  can't change its name
  initializes with a nervous mood
  can change its mood

Dog
  can initialize a dog
  initializes with a name
  can't change its name
  initializes with a nervous mood
  can change its mood

Fish
  can initialize a fish
  initializes with a name
  can't change its name
  initializes with a nervous mood
  can change its mood
```

Seeing the same code repeated 3 times in a row is a great sign that there is an underlying abstraction. Two times and you might not fully understand the abstraction and per Sandi Metz ["prefer duplication over the wrong abstraction"](https://www.sandimetz.com/blog/2016/1/20/the-wrong-abstraction)

As you can see all these classes share the same interface.

|  | Class Question |
| --- | --- |
| **Q** | What does 'inheritance' mean in the real world, beyond coding? |
| **A** | Something you receive from your predecessors |

In code, inheritance is a mechanism of message forwarding. You are sending a message to an object, if that object does not respond to that message, we can indicate another place 'up the chain' to look for that method.

```ruby
# show that we can use the `.methods` method

"hello".methods
# => [..., ..., ...]

# define an empty class

class Dog
end

# when you write the following loc what should you expect to see

Dog.new.methods.length

# The answer is not 0! it's 58! whats going on???

Dog.ancestors
# => [Dog, Object, Kernel, BasicObject]

# All ruby classes Inheriet from other classes.
# If the Dog class receives a message it doesnt respond to,
# it looks up the chain and asks the ancestors if they respond to it
```

### Slowly refactor

Create a Pet class and let your classes inherit from Pet. Run tests frequently.

```ruby
class Pet
  attr_reader :name
  attr_accessor :mood

  def initialize(name)
    @name = name
    @mood = 'nervous'
  end

end
```

### What if one of the classes needed some custom behavior?

```ruby
class Cat < Pet

  attr_reader :num_lives

  def initialize(name)
    @num_lives = 9
  end

end
```

Run code and watch the above code fail. Talk about super. Talk about what we just learned about Ruby's order of checking classes.

```ruby
class Cat < Pet

  attr_reader :num_lives

  def initialize(name)
    super
    @num_lives = 9
  end

end
```

Talk about limits of inheritance. Only can inherit from one class. Another tool for code sharing is modules/ mix-ins.

### Modules

In the owner class there is all the behavior for persisting owner instances: an `ALL` array, `self` shoveled in on initialization. Slowly refactor to this:

```ruby
# owner.rb
class Owner

  ALL = []

  extend Persistable::ClassMethods # extend signifies bringing in class level methods
  include Persistable::InstanceMethods # include signifies bringing in instance level methods

  attr_accessor :name, :pets
  attr_reader :species

  def initialize(name)
    @name = name
    @species = 'human'
    @pets = {:fishes => [], :dogs => [], :cats => []}
    super
  end

 # ...
end

# concerns/persistable.rb

module Persistable


  module ClassMethods
    def all
      self::ALL
    end

    def reset_all
      all.clear
    end

    def count
      all.length
    end
  end

  module InstanceMethods

    def initialize(*args)
      self.class.all << self
    end

  end

end
```

When working through the problem it gives you a nice opportunity to talk about namespacing, i.e. in a few days when we see something like `ActiveRecord::Base` we know that in the source code we'd find something like:

```ruby
module ActiveRecord
  class Base
    # ...
  end
end
```

---
title: Ruby Modules
layout: post
---

# <a id="modules">ruby-modules</a>

## Modules in Ruby

### SWBATs

### Resources

### Example Video

### Outline

Title: Modules Review Creator: Yomi Ladije &lt;@Joll59&gt;

## Objectives

1. Basics of ruby modules
2. Nested modules/module namespacing.
3. Refactoring using modules.

### Ruby Modules

Modules can provide a collection of methods, classes and constants which can be made available to any number of classes.

Modules are similar to Classes when it comes the inheritance chain, except you can include/extend/prepend multiple modules, and you can not instantiate a module.

Example of a Module.

```ruby
module FlatironSchool
  def accept_Student
    puts "Welcome to Flatiron School"
  end
end
```

### Roles of modules within classes:

Modules can be:  
 **Included** within a class with the `include` keyword, allowing classes to use all of the methods of the included module as instance methods.  
 **Extended** to a class with the `extend` keyword, lending the module's methods to the class as class methods.  
 **Prepeneded** to a class with the `prepend` keyword, this makes the methods from the module **"stronger"** and executes them first.

include: _Instance methods_.  
 extend: _Class methods_.

### Utilizing modules within classes.

```ruby
require_relative "RELATIVE FILE PATH"
#(in this instance the file path pointing to my FlatironSchool module)

class FreshStudents
  extend FlatironSchool
end

FreshStudents.accept_Student
=> "Welcome to Flatiron School"
```

If the module had been included instead of extended, What are the differences?

Lets refactor some code using modules. [Intro to modules lab.](https://learn.co/tracks/web-development-immersive-2-0-module-one/object-oriented-ruby/object-architecture/intro-to-modules-lab)

Before refactoring:

* Determine the responsibility or the behavior of the code that is being extracted.

**Changes to the Lab is outlined below.**

Class method

```ruby
def self.reset_all
  @@songs.clear
end

def self.count
  self.all.count
end
```

Module method

```ruby
module Memorable

  def reset_all
    self.all.clear
  end

  def count
    self.all.count
  end

end
```

* Why eliminate `self` in module method names?

Class method.

```ruby
def self.find_by_name(name)
  @@songs.detect{|a| a.name == name}
end
```

Module method

```ruby
module Findable
  def find_by_name(name)
    self.all.detect{|a| a.name == name}
  end
end
```

* Now, either inlcude or extend this module into our classes to have access to the method.

class method

```ruby
def to_param
  name.downcase.gsub(' ', '-')
end
```

module method

```ruby
module Paramable
  def to_param
    name.downcase.gsub(' ', '-')
  end
end
```

* Now, either inlcude or extend this module into our classes to have access to the method.

The next part will incorporate the concept of nested modules and namespacing.

Example of nested modules and namespacing.

```ruby
module FlatironSchool

    module Instructors
      def early_morning_action
        puts "deploy labs"
      end
    end

    module Administration
      def accept_Student
        puts "Welcome to Flatiron School"
      end
    end

    module Students
      def pick_a_name
        puts "we are awesome!"
      end
    end

    class NewStudents
      puts "here to learn"
    end
end
```

```ruby
class FreshStudents
  extend FlatIronSchool::Students
end
```

The `Parent::Child` syntax is called **namespacing**

**NOW WHAT?**

To gain access to a namespaced class, use module name followed by the class name or have your class inherit from the Namespaced class.

```ruby
class FreshStudents
  extend FlatironSchool

  john = FlatironSchool::NewStudents::FreshStudents.new

  ## this creates a new instance of the class FreshStudents, which is
  ## utilizing the NewStudents class namespaced in the FlatironSchool
  ##w module.

end

or

class FreshStudents < FlatIronSchool::NewStudents

end
```

Continuing with the lab.

```ruby
module Memorable

  module InstanceMethods
    def initialize
      self.class.all << self
    end
  end

  module ClassMethods
    def reset_all
      self.all.clear
    end

    def count
      self.all.count
    end
  end

end
```

Implement the code below in the Artist/Song Class to reference the modules.

```ruby
extend Memorable::ClassMethods, Findable
include Paramable, Memorable::InstanceMethods
```

Before continuing, add one more line of code to the artist initialize method.

```ruby
def initialize
  super
  @songs = [ ]
end
```

The super is looking for a parent method `initialize` method and adding its functionality to the current instance method.

Prepend vs Include in super.

```ruby
class NewInstructor
  include FlatironSchool::Instructors
  def early_morning_action
    puts "Smile, its a lovely day"
    super()
  end
end
```

What happens if `include` is changed to `prepend`?  
 `prepend` guarantees the parent method is called before the instance method.

[Ruby modules vs PORO\(Plain Old Ruby Object\)](https://www.google.com/webhp?hl=en&sa=X&ved=0ahUKEwiI3IfVm_zTAhVErlQKHUUnALgQPAgD#hl=en&q=ruby+modules+vs+poro): This is a healthy debate between rubyist in favor of not using modules, instead use ruby objects.

### EXTRA

Popular Ruby Atom Snippets!

```text
rw + tab:  attr_accessor :attr_names
r + tab:  attr_reader :attr_names
w + tab:  attr_writer :attr_names
dfi + tab:  def initialize argument end
def + tab: def method end
defs + tab: def self.method end

cl + tab:  class  Name  end
mod + tab:  module Name end
c + tab: case statements
if + tab: if statements
el + tab: elsif statements
e + tab: each {|e|}
m + tab: map {|e|}
f + tab: find{|f|}


The idea is simple, try button(s) see drop down menu, you
will be pleasantly surprised. The shortcuts are determined by the
file type you are in. So, it changes with every programming
language atom supports.

'⌘ + /' --> comment.
'⌘ + ,' --> settings.
'⌘ + d' --> select matching words (⌘ + click works too)
'⌘ + \' --> hides file tree.
'⌘ + [' or '⌘ + ]' --> auto indents or reverses indent relative to parent scope.
'i' while file tree is selected will show hidden files.
'a' while file tree is selected will add a new file.
'shift + a' will add a new folder.
```

---
title: Ruby Hashes And The Internet
layout: post
---

# <a id="hashes-and-internet">ruby-hashes-and-the-internet</a>

_This lecture is to get students ready for the Hashes and the Internet lab that is usually a day long pairing lab. Since students don't usually have exposure to making requests programmatically, we have to walk them through what that looks like and with which tools._

## SWBATs

* Recognize the parts of the request-response lifecycle
  * Define client and describe setting up the request
  * Define server and describe how the response is formatted
  * Identify HTML as a response type
  * Identify and define JSON
* Define Application Programming Interface \(API\)
  * Describe the API of a Ruby Array
  * Explain the uses of an API on the internet
* Practice making requests to an API and parsing and examining the result
* Practice writing a command line application \(CLI\)

## Resources

* [Example Video](https://youtu.be/Jqmo0ZpCSh4)
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/ruby/hashes-and-the-internet)

## Outline

```text
 5m   Intro
 5m   How the internet works
 5m   Ruby gems for working with APIs
15m   Making requests to Google Books API
15m   Student Exercise
15m   Refactoring with Single Responsibility Principle
===
 1h   Total
```

### Intro

In hasketball couldn't we just have done this instead of going deep into `map`

```ruby
def get_players
  # game_hash.values.map do |team_info|
  #   team_info[:players]
  # end.flatten
  game_hash[:home][:players] + game_hash[:away][:players]
end
```

> **Q:** Anyone have a reason why we wouldn't just do that?  
> **A:** If our data every changed, we had info about all teams in the league, all games in a season.

But... Currently we don't have a way to dynamically get data, all data comes from the specs \(like in Deli Counter interview\) and is made-up.

So we know a bunch about Ruby _What do we know about Ruby?_

* Methods
* Return Values
* Data Structures

... but who cares? this is all with made up data, can we use what we know to interact with real data

### How the internet works

Students may not yet understand these concepts:

* GET requests
* Server responses
* Developer console
* APIs
* JSON \(string formatted as a hash/object\)
* Ruby Gems

Navigate to "reddit.com" in the browser. What happens? What do we see? How is what we see described in code? It's HTML. The HTML is sent from another computer \(server\) to my browser and my browser reads it, interprets it, and displays it for me.

Navigate to "reddit.com/.json". What type of information am I getting here? Does it look like anything we've seen before? Similar to a hash.

Define JSON: a language-agnostic data format that we can get from websites. It's a convention of the internet.

Recommend downloading a JSON viewer Chrome extension.

We could imagine writing ruby code to do this programmtically

```ruby
response = make_request('www.reddit.com/.json')

reddit_hash = parse_into_hash(response)
```

### Ruby gems for working with APIs

Gems are just code that other people have written that we can download and use in our own programs.

Gems have dependencies \(required other programs\).

`rest-client` is a gem that allows us to make HTTP requests.

`json` is a module in the Ruby standard library that allows us to parse and create JSON.

Popular Gems have documentation that have instructions as well as examples. You can also always look at the source code of the Gem if you're feeling very daring.

Look at the documentation for `rest-client` to show the example of how to make a request.

```bash
gem install rest-client
gem install pry
```

```ruby
require 'pry'
require 'rest-client'
require 'json'
```

### Making requests to Google Books API

[Google Books API](https://www.googleapis.com/books/v1/volumes?q=ruby+programming)

Hard code in a search term and show the response from google books api `"https://www.googleapis.com/books/v1/volumes?q=ruby+programming"` Code along, every step of the way checking what each subsequent method call returns with `.class`. Ask what's the type, what's the type, what's the type?

Keys as strings instead of symbols with JSON.

Start writing all the code all in one big block. It will get messy as you start having to check for edge cases such as authors being not an Array, but `nil` or description being `nil`

Getting back `nil` is fine, but trying to do something to `nil` is an issue. `nil` doesn't respond to the message `join`, etc.

```ruby
if  book["volumeInfo"]["authors"]
 authors = book["volumeInfo"]["authors"].join(" and ")
else
 authors = "No authors found"
end
```

```ruby
if  book["volumeInfo"]["description"]
 description  = book["volumeInfo"]["description"][0..140]
else
 description = "No description available"
end
```

All this logic in one big block will get messy and the code is not great.

> **Q:** What principle did we mention yesterday that we are breaking?  
> **A:** Single responsibility

### Student Exercise

```bash
# Deliverables
# 1. Write an application that takes a search term from a user
# 2. Make a Request to the GoogleBooks API and get back some results
# 3. Display the titles, author names, and description for each book
```

### Refactoring with Single Responsibility Principle

Build out methods like `get_authors` or `get_title` Ask students to determine what are good candidates for further _Encapsulation_ \(&lt;- define\)

end with code like this:

```ruby
require 'pry'
require 'rest-client'
require 'json'


# write an application that takes in some user input
def welcome
  puts "Welcome to the BookSearcher"
  puts "Please enter a term:"
end

def get_user_input
  gets.chomp
end


# make a request to the google books api using term

def fetch_books(term)
  response = RestClient.get("https://www.googleapis.com/books/v1/volumes?q=#{term}")

  JSON.parse(response.body)
end


def get_title(book)
  book["volumeInfo"]["title"]
end

def get_author(book)
  if  book["volumeInfo"]["authors"]
   book["volumeInfo"]["authors"].join(" and ")
  else
   "No authors found"
  end
end

def get_description(book)
  if book["volumeInfo"]["description"]
    book["volumeInfo"]["description"][0..140] + "..."
  else
    "No description available"
  end
end

def print_book(title, authors, description)
  puts "*" * 30
  puts "Title: #{title}"
  puts "Authors: #{authors}"
  puts "Description: #{description}"
end


def run
  welcome
  search_term = get_user_input

  fetch_books(search_term)["items"].each do |book|
    title = get_title(book)
    authors = get_author(book)
    description = get_description(book)

    print_book(title, authors, description)
  end
end

# and display a list of books, including title, author and description, that are found
run
```

# <a id="tdd">ruby-tdd</a>

## SWBATs

* Explain the need for testing in general
* Install RSpec in a project
* Define Test-Driven development
* Describe what a testing framework is and what the RSpec framework does
* Write tests for a basic function while considering entire problem space
* Describe the difference between failing, passing, and pending test cases
* Define assertions and matchers in the context of test cases
* Use output from a testing framework to guide their development

## Resources

* [Example Video](https://www.youtube.com/watch?v=eyFD0mTGktc&feature=youtu.be)
* Starter Code
  * [Beginning](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/ruby/intro-tdd/start)
  * [Break Example](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/ruby/intro-tdd/break)
  * [End](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/ruby/intro-tdd/end)
* [Software Testing](https://ocw.mit.edu/ans7870/6/6.005/s16/classes/03-testing/)
* [RSpec documentation](http://rspec.info/documentation/)
* [Rspec-Rails Documentation](https://github.com/rspec/rspec-rails)

## Overview

```text
10m Breaking Code While Refactoring
5m Installing Rspec 
10m Using Unit Tests to Protect Ourselves
15m Using Unit Tests to Drive Our Development
10m Conclusion
===
 50m Total
```

### Breaking Code While Refactoring
The point of this section is to demonstrate just how easy it is to break working code without realizing it:
* Introduce students to the code base. You have 4 deliverables: 

========================================================================

## tdd-ruby-code

* Create a "Hero" Class 
  * Accepts an array of abilities
  * Each ability will be represented by a hash with a name and "coolness" rating
* Create a method which returns the hero's coolest ability
* Create a method which returns the hero's ability names ordered alphabetically
* Create method add_ability, which accepts an ability and adds it to the array

========================================================================

* The first two are already finished, and there is a console that will allow you to show that the `coolest_ability` method works.
* Begin implementing our second deliverable, `ordered_abilities`, which will return the names of the abilities ordered alphabetically
  * Create a method which gets the ability names and then returns them sorted, like so: 
  ```
    # Returns abilities Ordered Alphabetically 
    def ordered_abilities 
       abilities = @abilities.map do | ability |
            ability[:name]
        end
        abilities.sort
    end
  ```
  * Refactor the method into single responsibility methods: 
  ```
   def abilities
        @abilities.map do | ability |
            ability[:name]
        end
    end

    # Returns abilities Ordered Alphabetically 
    def ordered_abilities 
       abilities.sort
    end
  ``` 
    * Show how the ordered_abilities method meets our objective in the console 
* Reveal that our implementation has broken `coolest_ability`
* Discuss how, as projects grow, it becomes easier to break code unrelated to the code we are working on. This becomes even easier as our projects grow in complexity; most of our large code projects are more like frankenstein's monster or the Power Ranger's Megazord than anything else:

![](https://media.giphy.com/media/14lpUNhInOSz9S/giphy.gif) 
* Unit tests provide us with a way to check all of the features of our code without having to do so manually
* Rspec is a tool which helps us to write unit tests
* Briefly describe why the code broke, as many will be curious (def abilities overrides our default getter for abilities, a getter we were using in `coolest_ability`). I like to add that this is only for those who are interested, and that if students get lost, they shouldnt worry, as the cause of the breakage is not the point of this segment.

### Installing Rspec
Go through the process of adding rspec to an existing project. The idea is that hopefully they will do this with the Mod 1 projects they are currently working on. Add rspec to your gem file, run `bundle install`, and then run `rspec --init`. Review the folders/files that have been added to our project:
* app
* config
* **spec/**
  * **spec\_helper.rb**
* tools
* **.rspec**	 
* Gemfile	  
* Gemfile.lock
* README.md

Tests go into the `spec` folder shown above. The pattern for naming tests is usually `<some feature>_spec.rb` when using RSpec. When using other testing frameworks for other languages, there may be other conventions, so be sure to read the documentation before writing tests.	 
We'll create a file called `hero_class_spec.rb` and place it in our `spec` folder.

### Using Unit Tests to Protect Ourselves
* Write the unit test for the `coolest_ability` method:
  * First, you have to require the file that you want to test. This may seem obvious, but it's not done for you automatically.
  * Second, you will want to give some context to your set of tests, and this part of the spec is called the `describe` block. Usually, this will just say which part of the program you're testing, so here, we can just use `coolest_ability` as the description.
  * Third, you will want to give some context to each individual test you write. We accomplish this using the `it` block, which describes what function of our subject we are testing.
  And lastly, you will need to write your actual assertion which is in the form `expect(<some executable code>).to be <some value>`. There are a few pieces to this, but we will just use this pattern for the first few tests.
    * I think it is beneficial to break down each method in the assertion and what it is returning to make rspec feel less magical. These are just methods returning objects we call new methods on.
* Show how the test alerts us that the method is broken. 
* Fix your the hero class by renaming `abilities` to the more appropriate name `ability_names`, and show that the test passes.

### Using Unit Tests to Drive Our Development
Now we segue into test driven development as compared to unit testing. Test-driven development \(TDD\) is all about **tests being the real fuel that helps you write your code**. The general rule here is called "red, green, refactor", which means that you'll:

1. Write your test, run your test suite, and **look for the failure**
2. Implement a **naive, passing solution** to your failing test
3. **Rewrite your original solution** to optimize it or make it more readable

* Write the test for our third deliverable for the hero class 'Create method `add_ability`, which accepts an ability and adds it to the array'. 
* Show that the test breaks, because the method has not been defined yet
  * Discuss how this gives us a clear path forward in our development 
* Implement the method
* Show the passing test 
* Close this section by disucssing the types of tests we want to test:
  * the base case or the happy path; behavior that we expect to work
  * the sad path; behavior that we expect to break
  * extreme edge cases; things like bad inputs or system errors

### Conclusion
* There is a difference between code that works and code that is good. The latter can be extended, understood by future developers and built upon as our software increases in complexity.
* Writing code that can be easily tested leads us to write code which has good seperation of concerns and a degree of idempotency, which will help us down the line as our code is resused.
* Segue into a discussion about unit testing in the workplace. Unit tests are not always part of a development teams process because it is often viewed by nonprogrammers as inessential. As good developers we should know and lobby for good programming practices even if we don't always have the opportunity to follow them.

---
title: Sql Intro
layout: post
---

# <a id="sql">sql-intro</a>

## SWBATs

* Explain persistence and the need for using SQL
* Define SQL
* Explain the difference between SQLite3 and SQL
* Explore provided data through SQLite Browser
* Perform CRUD actions on a single table
* Perform CRUD actions across related tables

## Resources

* [Example Video](https://youtu.be/24maeY3xe-c)
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/databases/intro-sql)

## Outline

```text
10m What is SQL?
50m Practice SQL CRUD
===
60m  Total
```

### What is SQL?

SQL stands for Structured Query Language and is a language that allows us to do:

* Store / persist information
* Manipulate that information

SQLite3 is a relational database.

Some specific actions that we can do are CRUD actions, a common acronym we'll see throughout the program, web development, and computing in general:

* Create data
* Read data
* Update data
* Delete data

### Practice SQL CRUD

Investigate the schema of the database; the structure of the database. If in the command line, use `.schema`, if in browser, use "Database Structure" tab.

After each challenge, check the database structure to verify that the changes were made successfully.

When you get to problem four, ask students about relationships between tables and cover the definition of relational databases.

> **Student Challenges:**
>
> 1. Write the SQL to return all of the rows in the artists tables
>
>    `SELECT * FROM artists`
>
> 2. Write the SQL to select the artist with the name "Black Sabbath"
>
>    `SELECT * FROM artists WHERE name = 'Black Sabbath'` &gt; `SELECT * FROM artists WHERE LIKE = 'Black Sabbath'`
>
> 3. Write the SQL to create a table named 'fans' with an autoincrementing ID that's a primary key and a name field of type text
>
>    `CREATE TABLE fans (id INTEGER PRIMARY KEY, name TEXT)`
>
> 4. Write the SQL to alter the fans table to have an artistId column of type integer
>
>    `ALTER TABLE fans ADD COLUMN artistId INTEGER`
>
> 5. Write the SQL to add yourself as a fan of the Black Eyed Peas \(artistId = 169\) `INSERT INTO fans (name, artistId) VALUES ("Your name", 169)`
>
>    Don't add an ID manually, but show that you can do it
>
> 6. Return fans that are not fans of the Black Eyed Peas \(artistId = 169\) `SELECT * FROM fans WHERE artistId IS NOT 169`
>
> 7. Return artists name next to their album title

---
title: Orms Custom Intro
layout: post
---

# <a id="orms">orms-custom-intro</a>

## SWBATs

* Define Object Relational Mapper \(ORM\)
* Distinguish between ORM and SQL
* Demonstrate that ORMs are the pattern connecting scripting languages and databases
* Explain how the `sqlite` gem works as a driver or wrapper around SQL
* Implement HEREDOCs to be saved in variables to be executed by SQL driver
* Perform persistent CRUD actions on two separate models

## Resources

* [Example Video ](https://www.youtube.com/watch?v=fbXSQ7ehoW8)
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/ruby/intro-orms)

## Outline

```text
10m One to Many Relationship in SQL
15m Many to Many Relationship in SQL
 5m CRUD in SQL and Ruby
 5m ORM Pattern
10m App Demo and Structure
20m Selecting and Inserting
10m Saving and Updating
===
75m Total
```

### One to Many Relationship in SQL

* Foreign key versus primary key
* Which table is the foreign key placed on? \(has many or belongs to\)
* Show the pain of not putting the foreign key on the child
* Find all books written by a certain author by ID

### Many to Many Relationship in SQL

* who is the parent? both
* how do we implement an author having many books and a book having many authors
* join table having two foreign keys
* write the sql to find all books written by a certain author given their name
* highlight order of writing sql syntax
* another example with tweets and tags

### CRUD in SQL and Ruby

* What are the 4 ways we can interact with data?
* How do we write these in SQL?
* How do we want to write these in Ruby?
* How do we map these SQL applications to Ruby?

### ORM Pattern

* each table in the db should correspond to our ruby class \(models\)
* each row represents an instance in the database
* each column represents an attribute for our instances
* why do we need a database? persistence

### App Demo and Structure

* demo current app
* little bit of file structure and bundler review
* SQLite3 gem is giving you code to interact with SQLite3 database
* Creating rake tasks
* Environment file
* Gemfile
* Run file

### Selecting and Inserting

* Working with SQLite3 Gem in the console
* class with attributes and initialize method
* write all class method with db execute call
* map results from select \* to create new tweet instances
* mass assignment
* adding IDs to mapped instance

### Saving and Updating

* writing the save method
* parameterized queries and database security
* what's the difference between calling new and create?

---
title: Orms Custom Dynamic
layout: post
---

# <a id="orms=review">orms-custom-dynamic</a>

## SWBATs

* Explain how inheritance works in Ruby
* Demonstrate inheritance on Ruby classes without persistence
* Refactor code that is common to two separate custom ORMs into a shared parent class
* Apply meta-programming to create and act on methods in child classes
* BONUS: Implement relationship macros in custom dynamic ORM

## Resources

* [Example Video](https://www.youtube.com/watch?v=ANV1Ghh7dDA)
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/ruby/dynamic-orms)

## Outline

```text
10m Single ORM Review
10m Building Abstract Model with Inheritance
10m Private Methods
30m Finish Abstracting Private Interface
30m Begin Defining Relationships* (bonus)
===
60m Total (without bonus)
```

### Single ORM Review

* private methods
* mass assignment
* meta programming
* `send`

### Building Abstract Model with Inheritance

* explain abstract model
* talk about inheritance
* compare two single models
* start cutting code from single model to abstract model
* get table name from the class name \(establish convention\)
* class methods aren't private by default

> **Note:** Test after each step! Or have tests written for this lecture

### Private Methods

* why have private methods

### Abstract the Private Interface

* get column names with PRAGMA table\_info\(table\_name\_plural\)
* why use explicit self?
* splat operator
* running code at the class level requires the method to be defined above
* inherited lifecycle hook

### Begin Defining Relationships

* much more metaprogramming
  * define\_method\(\)
  * Object.const\_get\(\)
* much more SQL

```ruby
sql = <<-SQL
  SELECT #{relationship}.*
  FROM #{self.class.table_name}
  JOIN #{through}
    ON #{through}.#{self.class.foreign_key} = #{self.class.table_name}.id
  JOIN #{relationship}
    ON #{through}.#{relationship[0...-1]}_id = #{relationship}.id
  WHERE #{self.class.table_name}.id = #{self.id}
SQL
```

---
title: Orms Custom Dynamic
layout: post
---

# <a id="dynamic-orms">orms-custom-dynamic</a>

## SWBATs

* Explain how inheritance works in Ruby
* Demonstrate inheritance on Ruby classes without persistence
* Refactor code that is common to two separate custom ORMs into a shared parent class
* Apply meta-programming to create and act on methods in child classes
* BONUS: Implement relationship macros in custom dynamic ORM

## Resources

* [Example Video](https://www.youtube.com/watch?v=ANV1Ghh7dDA)
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/ruby/dynamic-orms)

## Outline

```text
10m Single ORM Review
10m Building Abstract Model with Inheritance
10m Private Methods
30m Finish Abstracting Private Interface
30m Begin Defining Relationships* (bonus)
===
60m Total (without bonus)
```

### Single ORM Review

* private methods
* mass assignment
* meta programming
* `send`

### Building Abstract Model with Inheritance

* explain abstract model
* talk about inheritance
* compare two single models
* start cutting code from single model to abstract model
* get table name from the class name \(establish convention\)
* class methods aren't private by default

> **Note:** Test after each step! Or have tests written for this lecture

### Private Methods

* why have private methods

### Abstract the Private Interface

* get column names with PRAGMA table\_info\(table\_name\_plural\)
* why use explicit self?
* splat operator
* running code at the class level requires the method to be defined above
* inherited lifecycle hook

### Begin Defining Relationships

* much more metaprogramming
  * define\_method\(\)
  * Object.const\_get\(\)
* much more SQL

```ruby
sql = <<-SQL
  SELECT #{relationship}.*
  FROM #{self.class.table_name}
  JOIN #{through}
    ON #{through}.#{self.class.foreign_key} = #{self.class.table_name}.id
  JOIN #{relationship}
    ON #{through}.#{relationship[0...-1]}_id = #{relationship}.id
  WHERE #{self.class.table_name}.id = #{self.id}
SQL
```

---
title: Orms Active Record Intro
layout: post
---

# <a id="ar">orms-active-record-intro</a>

## SWBATs

* Define Object Relational Mapper \(ORM\)
* Describe how gems work and the value of shared code
* Implement ActiveRecord in their projects
* Practice creating migrations for updating the database structure
* Explain how `rake` works and how to run rake tasks
* Distinguish between and define "model", "class", and "table"
* Practice with ActiveRecord::Base instance and class methods
* Perform persistent CRUD actions on one model using ActiveRecord

## Resources

* [Example Video](https://youtu.be/kO4fTpLq_b4)
  * This video also covers associations. Some times, we have separated these into two lectures to give each time to sink in
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/ruby/active-record-intro)

## Outline

```text
10m Rake and File Structure
15m Migrations and Database Structure
15m Connecting Models to ActiveRecord
20m Methods from ActiveRecord
===
60m Total
```

### Rake and File Structure

* Rake
  * Define tasks, based off of a similar tool in C-lang called Make
  * We have a Rakefile that defines tasks to be run from the command line
  * To view tasks, run `rake -T` in directory with Rakefile in itself or parent
  * Tasks can be arbitrary, they're just a way to encapsulate reusable ruby code that you want to execute from the command line
  * We're getting some tasks from the `sinatra/activerecord/rake` library which gives us easy to use ActiveRecord tasks
* File structure
  * Gemfile
  * `lib` folder holds models and app code
  * `db` directory holds migrations and seeds.rb file
  * `config` holds environment file
    * `require 'bundler'` and `Bundler.require` load all of the gems in our Gemfile
    * `ActiveRecord::Base.establish_connection` sets up our database with options hash
    * `require_all` loads all of our application code

### Migrations and Database Structure

* we want to create our first model \(class + table\)
* to get our database set up, we need to use the `rake db:create_migration` task
  * run without passing a name parameter and show the error and walk through it
  * run it with a name parameter that's meaningful like `create_<table_name>`
  * create the migrations you know you'll need up-front
* check out the migrations in the `db/migrations` folder
  * what is the sequence of numbers in the beginning of the file name?
  * how and why does activerecord use this?
  * defining `change` methods and `up` and `down` methods in migrations
  * make sure the two models you choose are related \(one-to-many\)
* `create_table` method which takes a block, the block takes a table builder
  * why do we use the `t` variable?
  * `t.string :name` what is the `string` method declaring?
  * what is the argument to the `string` method and the data type? `:name`
  * the methods defined on the table `t` are the data types we want to use
  * how do we add foreign keys to a related table? which table does it go on?
* run migrations `rake db:migrate`
  * it's nice to put an error in your code to show students what errors look like and have them work through how to solve them
  * fix the error and re-run
  * show what a successful migration looks like
  * run the migrations again to show what it looks like when all of your migrations are run
  * break down the output of the success and error outputs
* how does activerecord keep track of migrations that have been run?
  * reread the output of a successful migration, look at the number
  * compare the number with the number in the filename for that migration
  * the schema and db files are generated from the migrations with sqlite3
  * look at `schema.rb` which is the authoritative representation of the database structure
  * look at the `version` argument in the schema to fsee if it matches with the last successful migration
* !!! some students will run into errors with their migrations because of the lab gem versions
  * make sure to read errors carefully because some migrations won't be successful without version number
* migration conventions
  * file name and class name must match up exactly, but in different case
  * create\_table block argument is usually a `t`
* blowing up the database
  * delete db
  * delete schema.rb
  * !!! don't do this, just in this module, and don't do it if you can't easily get your data back
* gracefully fixing the db
  * reset the schema completely
  * migrate all migrations
  * create a new migration for more quantity \(like adding a column!\)
  * migrate, but decide you don't want that change anymore
  * demonstrate rolling back one step and then multiple steps
  * delete the migration files you don't want to keep
* we don't need to create migration files by hand anymore, thank goodness!

### Connecting Models to ActiveRecord

* create a model file in `lib/models`
  * convention is to have the model class name singular and the sql table plural
* create a class in that folder with your model name and inherit from `ActiveRecord::Base`
* see if we can already create instances by opening up the console
* check first to see if Book is defined
  * it will say uninitialized constant if it's not defined
* create a few instances with `Model.create(attributes)`
  * inspect the model and view how the object is output as a string
  * look at the class name as well as the attributes
* create an associated model with `AssociatedModel.create(attributes)`
  * associate these models by using the foreign key instead of AR associations
* inspect either model by calling these methods
  * `instance.class` shows the class name and the columns
  * `instance.methods`
    * even without writing any methods in the class, there are a TON \(362?\)
    * look for the attribute accessors that are auto-generated from column names
* write a method on the models
  * a nice first method to write is the association \(not using macros\) for each

```ruby
class Book < ActiveRecord::Base
  def author
    Author.find(self.author_id)
  end
end
#...
class Author < ActiveRecord::Base
  def books
    Book.where(author_id: self.id)
  end
end
```

### Methods from ActiveRecord

* Model.new
  * creates a new instance in local memory without persistence
* Model\#save
  * inserts or updates instance in db
* Model.create
  * Model.new + Model\#save
* Model.all
  * all instances
* Model.first
  * instance with the lowest ID in the db
* Model.find
  * also find by id
* Model.find\_by\({ attribute: value }\)
  * can find by one attribute-value pair or multiple
* Custom sql with Model

---
title: Orms Active Record Associations
layout: post
---

# <a id="ara">orms-active-record-associations</a>

## SWBATs

* Explain how ActiveRecord works for non-related models
* Implement one-to-many relationships using ActiveRecord `has_many` and `belongs_to`
* Implement many-to-many relationships using ActiveRecord `has_many, :through`
* Describe the methods that the relationship macros add to a model
* Practice looking up library documentation
  * Specifically, looking up documentation for ActiveRecord
    * Migrations
    * Association Macros
    * Rake tasks

## Resources

* [Example Video](https://www.youtube.com/watch?v=UDv6n9ryFXs)
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/ruby/active-record-associations)

## Outline

```text
25m Project Setup (files, migrations, models)
10m Our First ActiveRecord Relationships
20m Macros and Methods Created
10m Wrap Up
```

### Project Setup

#### File structure

Follow project setup from previous lectures, but go over them once more to explain what each file is doing, why we have each directory, and how everything fits together.

This is a time to go over the domain as well. Make a domain that has both types of relationships that we go over: one-to-many and many-to-many.

#### Migrations

* syntax for creating a migration in the command line
* writing out the actual migration in the migration file
* start with models that don't need foreign keys and migrate those
* show the schema.rb after each migration
* write out migrations that need foreign keys and question the class as to why they need them on those tables
* run all migrations and check the schema before moving on

#### Models

* setup your models one-on-one and test each
* use `ActiveRecord::Base.logger = Logger.new(STDOUT)` to show sql queries from AR

### Our First ActiveRecord Relationships

* set up a belongs\_to association and demo it in console `doctor.department.name`
* set up a has\_many association and demo it `department.doctors`
  * this is like an array, but inspect the class and view the methods
* emphasize inverse relationships
* set up a has\_many through association and demo it `patient.doctors`
* build out all relationships, test, and view sql queries

### Macros and Methods Created

* define macro as a method call that creates functions
* show rails guide and how each association creates new methods for class
* shovel items into a through collection and view sql
* mass assignment with instances of other classes instead of native types
* show how join instances are created automatically

### Wrap Up

* demonstrate what activerecord::base gives us
* difference between new \(+ save\) and create
* difference between changing attributes \(+ save\) and update
* if something has a foreign\_key it belongs to the table from the foreign key
* if we do the belongs\_to, we need to include the inverse has many
* if you get an undefined method error, you need to include the macros
* if there are linked relationships, you can use through as an option to has many
* 1000 times easier than writing sql

### Optional Instructor Notes

* When demonstrating associations and creating them use the 'old school as an example in the model'

```ruby
class Author < ApplicationRecord
  has_many :books
  # Is the same as:
  def books
    Book.all.find(self.id)
  end

 has_many :written_books, classname: "Book"
  # can be written as:
  def written_books
    Book.all.find(self.id)
  end
end

class Book < ApplicationRecord
  belongs_to :author
end

```
