# SE Phase 1 Lecture Guide

## Overview of Lectures

- [Intro to JavaScript](#intro)
- [JS DOM Review - Just Enough JS](#just-enough)
- [Intro to the DOM Continued](#intro-to-dom)
- [Events Intro](#events)
- [Event Listeners](#event-listeners)
- [JavaScript Promises and Fetch](#promises)
- [Fetch and the DOM](#fetch)
- [OOJS](#oo)

## Lecture Notes

---
title: Javascript Introduction
layout: post
---

# <a id="intro">Introduction to JavaScript</a>

No setup required for this lecture, but it can be helpful for students to see the outline of the information.

It's also helpful to show students which documentation to use. _Prefer MDN over W3Schools._

If there's enough time, go through a test file and demo how to work through it in a test-driven way as well as how to read the test.

## SWBATs
* Give a general outline of the history of JavaScript and its most recent changes
* Identify the key differences between Ruby and JavaScript
* Explain how JavaScript is loaded, interpreted, and executed in the browser
* Identify which data types are pass-by-value and which are pass-by-reference
* Write correct JavaScript syntax
* Run tests on labs

## Resources
* [Example Video](https://www.youtube.com/watch?v=-GN1dPbsvrQ)
* [Starter Code with Student Facing README][js-intro-starter]

## Outline


```text
  5m History of Javascript
  5m Review request Response cycle
  5m JavaScript Data Types Overview
  5m Constructors vs Literals
  10m Primitives
  20m Non-primitives
  5m Type Checking
  5m Doing Labs
  --
  60m Total
```

### History of JavaScript
* Early Days
  * Created by Brandon Eich at Netscape in 10 days in 1995
  * Was not a highly respected programming language for about 10 years
  * Based off of functional languages with some object-oriented patterns
  * Applications like Google Maps and Gmail were where JavaScript shone again
* Standards
  * The standard for JavaScript implementations is called ECMAScript
  * The standard is updated yearly and the standard for that year is called ECMAScript 20xx (or ES 20xx)
  * [Browser Wars](https://en.wikipedia.org/wiki/Browser_wars) still leave us with legacy JavaScript implementations (and weirdness)
  * We can use transpiling to write JavaScript according to the standard we want and convert it to code that can be used for the majority of JavaScript applications

### Review Request-Response Cycle
* Request-Response lifecycle
  * Some code makes a request to a server
  * We get a response back with data in binary, text, HTML, or JSON
  * We use that data in our application
* In the browser
  * A user enters an address in the address bar (or clicks a link)
  * A request is made to a server, which typically serves HTML
  * The user usually sees a loading indicator (like a spinning circle) near the address bar
  * Included in that HTML are links to images, fonts, stylesheets, and scripts
  * Each one of those links means another request by the browser but without refreshing the page
  * When all the external links have loaded, the page itself is finished loading
* Loaded JavaScript
  * JavaScript can be written directly in HTML through a `script` tag
  * It can also be loaded externally through a `script` tag with a `src` attribute
  * When the browser sees JavaScript, it attempts to run it immediately
* JavaScript implementations
  * Each browser has its own [JavaScript engine](http://en.wikipedia.org/wiki/JavaScript_engine) or implementation
  * The [Document Object Model](https://en.wikipedia.org/wiki/Document_Object_Model) is the interface between the loaded HTML and the JavaScript code we write
  * Most browsers are converging on agreeing on web standards, but browsers need ability to add proprietary features to CSS, JS, and DOM

### JavaScript Data Types Overview
There are seven data types in JavaScript:
  1. Symbol
  2. Undefined
  3. Null
  4. Boolean
  5. Number
  6. String
  7. Object  

Many have constructor functions (like classes in Ruby) and many use the literal values. Different data types are pass by reference and pass by value.

### Constructors versus Literals
```js
let anotherNum = 1;
let someNum = Number(1);
let someNewNum = new Number(1);
someNewNum === anotherNum; // => false
someNum === anotherNum; // => true
```

### Primitives
Pass-by-value - when you declare a variable and pass it to a function, a *copy* of the variable is passed, not the original object in memory.

* String
  * `'I'm a string in single quotes'`
  * `"I'm a string in double quotes"`
  * `` `I'm a string template with backticks and interpolation ${'Yay!'}` ``

* Number
  * Negative `-1`
  * Exponent `-1e2`
  * Float `-1.1e2`
  * NaN `'hello' * 3`
  * parseInt / parseFloat

      ```js
      parseInt('123')             // => 123
      parseInt('123.456')         // => 123
      parseFloat('123.456')       // => 123.456
      parseInt('one two three')   // => NaN
      ```

* Boolean
  * Falsey values
    * False: `false`
    * Zero: `0`
    * Empty string: `""`
    * Null: `null`
    * Undefined: `undefined`
    * Not a number: `NaN`
  * Truthy values (everything else)

* Undefined
  * A variable that is declared but not defined

    ```js
    let someVar;
    console.log(someVar); // => undefined
    ```

* Null
  * An assignment value that represents nothing, like `nil` in Ruby

    ```js
    let someVar = null
    console.log(someVar) // => null
    ```

* Symbol
  * Only used as somewhat private, unique identifiers for object properties, i.e. object keys. (Don't worry much about these.)

    ```js
    let sym = Symbol();
    console.log(sym); // => Symbol()
    ```

### Non-Primitives
**Pass-by-reference**: when you declare a variable and pass it to a function, the object in memory itself is passed, not a copy of the object.

* Object
  * A loaded word in JavaScript. Basically everything that's not a primitive is an object. Objects describe key-value pairs, like hashes in Ruby. They also describe arrays, functions, prototypes, and other complex data types.

  * Object literals
    * Also known as plain-old JavaScript objects (POJOs), these are really simple key-value pairs. The keys are strings (or Symbols), and the values are any data type, including other objects.

      ```js
      const fred = { name: 'Fred', age: 26 };
      const jone = { name: 'Jone' };
      const school = {
        students: [fred, jone]
      };
      ```
    * You access properties of objects in one of two ways: dot-notation or bracket-notation. With the brackets, the value that is passed in needs to evaluate to a String or a Symbol.

      ```js
      const nameKey = 'name';
      console.log(`${fred.name} is ${fred.age}`); // => "Fred is 26"
      console.log(`My friend's name is ${jone[nameKey]}`); // => "My friend's name is Jone"
      ```

* Function
  * There are two general ways to write functions in JavaScript. As a function expression, and as a function definition (aka declaration aka statement). The differences are subtle.

  * Another point to note is that _functions always return undefined unless explicitly returning otherwise_. There is only one case of implicit returns in JavaScript and that's with one-line arrow functions without braces.

  * Functions are POJO's that can be executed/called! This means that you can add properties to functions just like you do POJO's.

  * Function expression
    * This is like a function that can't live without being assigned to a variable, or a function that is defined right when it's used (as in as an argument to another function).

      ```js
      let arr = [1,2,3];
      let doSomething = function() { return true };
      let doSomethingElse = () => false;
      arr.map(function namedExpression(n) { return n + 1 });
      ```

  * Function declaration
    * This is simply a variable assignment and a function expression mashed into one. It ALWAYS begins with the `function` keyword and needs a name.

      ```js
      function doSomething() {
        return true;
      }

      console.log(doSomething); // f doSomething()
      ```

* Array
    * Arrays in JavaScript are similar to arrays in Ruby, but with different methods. Ruby has a robust enumerable library that can work on arrays and POJOs alike, but JavaScript is more DIY, so there are just enough enumerables to build what you need. Arrays can contain any data type.

    ```js
    let arr = [1, 2, 3, "a", "b", "c", { hello: 'world' }];
    arr.forEach(function(el) { console.log(el); }); // => prints 1, 2, 3, "a", "b", "c", { hello: 'world' }
    ```

### Type Checking
The original way of checking types, [`typeof`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof), is a little unreliable when looking at some objects like arrays, which return "object". This works best for primitive values.

Checking ancestry is the job of  [`instanceof`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof). It looks through the prototype (inheritance) chain to see if one object is an instance of some constructor.

[`obj.constructor`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor) returns the direct parent of, or the function that created, this object. For me, it's the most reliable to check parent-child types.

### Doing Labs
Running the `learn` command in Terminal should open a new browser window where the tests will run. When a file is updated in the directory where `learn` was executed, the web page with the tests should update automatically. If you need to debug your code, figure out which test is failing and put a `debugger` there. This works like `binding.pry` in Ruby.

**Keep in mind that in order for `debugger` to be triggered in your browser, you must have your developer console open.**

If you need quicker and more simple debugging, `console.log` or `console.dir` is the way to go.


[js-intro-starter]: https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/javascript/js-intro

---
title: Just Enough JS
layout: post
---

# <a id="just-enough">Just Enough JS</a>

## Outline

```text
   5m  | Introduction to "Just Enough JS"
   15m | DOM Overview
   25m | Modifying The DOM
   15m | Activity
  ----|----
  60m | Total
```

### Prework

* https://github.com/learn-co-curriculum/fewpjs-fewp-example
* https://github.com/learn-co-curriculum/fewpjs-stitching-together-the-three-pillars
* https://github.com/learn-co-curriculum/fewpjs-introducing-the-dom-and-just-enough-javascript
* https://github.com/learn-co-curriculum/fewpjs-changing-the-dom-with-dev-tools-and-javascript
* https://github.com/learn-co-curriculum/fewpjs-js-fundamentals-variables
* https://github.com/learn-co-curriculum/fewpjs-js-fundamentals-variables-lab
* https://github.com/learn-co-curriculum/fewpjs-js-fundamentals-calling-methods

### Prework learning goals

* Describe the difference between front-end and back-end web programming
* Describe the Document Object Model as a tree of objects
* Identify a specific DOM element using the DevTools
* Define querySelector
* Identify DOM elements using querySelector methods
* Use querySelector methods to assign an element to a variable
* Identify when a method returned a single element vs. a collection
* Use a querySelector methods to retrieve data from a DOM node

### Lesson learning goals

* Use different querySelectors to select single or multiple elements
* Determine when to target single vs. multiple elements of the DOM
* Identify pain points with imperatively manipulating the DOM

### Common Misconceptions

* How server-side and client-side code interact with each other
* Where to find JS documentation

## Starter Code

[Code])(https://github.com/learn-co-curriculum/lectures-starter-code/pull/32)

### Problem statement
> You've built a Rails application where users can manage a personal library. As a user, I can Create, Read, Update, and Delete Books. The functionality works, but the application isn't very interactive. Each click means an entire page refresh, and there's not much feedback for users as they navigate around the page.


### Activation
> Welcome to JavaScript! Today's lesson will be an exploration of what's possible in JS. Before we get started, take a few minutes to discuss the following with your partner.

> What are some of your favorite web applications? What are some of the features that make them work really well?

## Lesson

### Just Enough JS (5 minutes)

* Our goal for this lesson is to give you a foundation of just enough JavaScript to build an interactive web application. Take a look at this book lister application.
* It functions well enough, but it's not very interactive. We just discussed some things make web applications really cool.
* In order to implement those types of things, it would be nice if we had a programming language that could actually run in our web browser. Luckily, we do!
* Unlike most other programming languages, JS has an interpreter that ships inside of every modern web browser. This means that we can write JS code to interact with our users.

### DOM Overview (15 minutes)

#### Demonstration (10 minutes)

* Let's look now at The Document Object Model, or the DOM.
* What is the DOM?
  * Object-oriented representation of the webpage which allows programs to manipulate the properties and contents on the page
  * When HTML is read in by the browser, the DOM is created based on that HTML
  * Javascript is a language created to manipulate the DOM
  * Show image representing how the DOM is organized.

* Brief tour of Developer Tools
  * Open the Dev Tools by right-clicking on the page and selecting 'Inspect' from the context menu
  * View DOM in the 'Elements' tab
    * Show that HTML is directly editable in the main panel
    * Show 'Styles' tab to view and manipulate CSS
    * Show pointer feature to find elements by hovering over the DOM
  * JS Console
    * If they haven't seen it already, show them how the console works

#### Application (5 minutes)

* When our browser, the client, makes a request to the server, what happens?
  * Our server sends back a response.
  * In this case, contains HTML, CSS, and potentially JS code.
  * When our browser loads the HTML and CSS, creates a tree to represent all of those elements. This is the DOM
  * We can access this at the top level on the `document`. The document is a JavaScript Object with methods to allow us to Create, Read, Update, and Delete elements in our web app.
  * **Note** We're not going to go too far into JS objects during this lesson. Remember, we're learning "just enough JS"

### Modifying DOM Nodes (20 minutes)

#### Demonstration (5 minutes)

* We can select individual DOM nodes and save them to a variable. In JavaScript, we declare our variables using a keyword.
  * This let's the interpreter know what type of variable we want to use.
  * `const` is for constants - these are things that can't be reassigned.
  ```js
  const name = 'Ian'
  name = "Bob" // throws an error
  ```
  * `let` is for variables that can be reassigned.
  ```js
  let name = 'Ian'
  name = 'Bob' // No Problem
  name // => 'Bob'
  ```
  * A general good rule of thumb is to use `const` for everything, unless you need to reassign that variable. `let` is a good signal to other developers that the value could change over time.

* Now, let's select a DOM node and save it to a variable.
`const bodyElement = document.querySelector('body')`
* Let's break down what's happening here.
  * We're declaring a constant using `const` called `bodyElement`
  * Per JS convention, we're using lowerCamelCase for our variable names.
  * We're calling the document object, provided to us by the Browser API
  * The document has a method called `querySelector`. Like many other languages, JS allows us to call methods on objects.
  * Methods are simply pre-package behavior. We can execute the behavior using `()`. In this case, `querySelector` takes an argument of a string.
  * **Note** Again, not going too deep into methods here. It might be funny to say "Hashtag JustEnoughJS here"
* The element that we've selected here is the entire body. That's not super interesting, but we can be more specific using CSS selectors.
* To quickly touch on CSS Selectors
  * Individual selectors
    * Class `.class`
    * ID `#id`
    * Tag `div`
  * Combining Selectors
    * Space between `#parent .child`
    * Chain `div.image.highlighted`
  * Chain or nest CSS selectors to get greater specificity

#### Application (5 minutes)

* We can use the following methods on the document
* Notice that some methods return more that one element in a list. We can access those by index, ordered from 0 to the length of the list - 1.

  ```js
  document.querySelector('#unique-element')
  document.querySelectorAll('.some-shared-class')
  document.getElementsByTagName('body')[0]
  document.getElementById('unique-element')
  document.getElementsByClassName('some-shared-class')
  ```

#### Check for Understanding (5 minutes)

* So, our list of books is a `ul` with an id of `book-list`
* Two minute quick quiz: With a partner, using what we've learning so far, how would we do the following?
  * Create a variable called `bookList`, that cannot be overwritten, pointing to our unordered list?


#### Application (10 minutes)
* So, given our booklist now: `const bookList = document.querySelector('ul#book-list')`
* We can changing attributes `bookList.style.backgroundColor = red`
* We can also change what items are rendered.
  * `booklist.innerHTML = '<li>My Great Book</li>'`
* We can delete elements `document.removeChild(bookList)`
* Whoops, now we've deleted our bookList. Don't worry, we can re-create it as well
* We can instantiate new elements using: `const element = document.createElement('ul')`
* Adding attributes to elements `element.id = 'book-list'`
* Appending to node `document.body.appendChild(element)`

### Activity (15 minutes)
Students will go to their favorite websites and modify the DOM programmatically. Wikipedia and Twitter are good examples. During this time, circulate the room and check in with the different groups to see how they are comprehending the material.

* Students should:
  * Select elements and save them to variables
  * Delete at least 2 elements
  * Modify elements (e.g., replace image url, change text, change CSS)
  * Create new elements and add to page

* Encourage students to think programmatically about the DOM by giving them problems that involve iteration and the use of multiple CSS selectors
  * Change all instances of one word
  * Replace all images on only a certain portion of the DOM
  * Change every other header
  * Bonus (Hard): replace all elements of one tag to another (e.g., `p` to `h1`)

### Conclusion/Wrap Up

> You've now seen how we can create really interesting applications with just a few lines of JS code. We'll continue to build on these ideas over the course of the Module.

---
title: Javascript Intro To The Dom
layout: post
---

# <a id="intro-to-dom">Intro To The DOM JS</a>

## SWBATs
* Define the DOM and DOM nodes
* Query the DOM using selectors
* Manipulate the DOM by adding, removing, and editing the properties of DOM elements
* Use (or at least recognize) jQuery
* Use the Chrome Developer tools to debug

## Resources
* [The DOM](https://www.youtube.com/watch?v=oVp-CKK25NM)
* [Starter Code with Student Facing README][dom-intro-starter]

## Outline

```text
  10m | The Document Object Model and Developer Tools
   5m | CSS Selectors
  10m | Selecting DOM Nodes
  10m | Modifying DOM Nodes
  10m | Creating DOM Nodes
  15m | Activity
  ----|----
  60m | Total
```

### The Document Object Model
* What is the DOM?
  * Object-oriented representation of the webpage which allows programs to manipulate the properties and contents on the page
  * When HTML is compiled, the DOM is created based on that HTML
  * Javascript is a language created to manipulate the DOM

* Brief tour of Developer Tools
  * Open the Dev Tools by right-clicking on the page and selecting 'View Page Source' from the context menu
  * View DOM in the 'Elements' tab
    * Show that HTML is directly editable in the main panel
    * Show 'Styles' tab to view and manipulate CSS
    * Show pointer feature to find elements by hovering over the DOM
  * JS Console
    * If they haven't seen it already, show them how the console works

### CSS Selectors
* Individual selectors
  * Class `.class`
  * ID `#id`
  * Tag `div`
* Combining Selectors
  * Space between `#parent .child`
  * Chain `div.image.highlighted`

### Selecting DOM Nodes
* Understand types that are returned form selecting a DOM node with JavaScript
* Understand how to use CSS selectors
* Methods

  ```js
  node.querySelector('#unique-element')
  node.querySelectorAll('.some-shared-class')
  node.getElementsByTagName('body')[0]
  node.getElementById('unique-element')
  node.getElementsByClassName('some-shared-class')
  ```
  * Mention that `NodeList` is array-like, but does not have iterators built on it. Can be borrowed from `Array.prototype`
  * Chain CSS selectors to get greater specificity

### Modifying DOM Nodes
* Storing node in a variable `let body = document.querySelector('body')`
* Changing attributes `body.style.backgroundColor = red`
* `innerText` and `textContent` vs. `innerHTML`
* Removing elements `document.removeChild(body)`

### Creating DOM Objects
* Instantiating new elements `let element = document.createElement('img')`
* Adding attributes to elements `element.src = 'http://www.coooolimage.com'`
* Appending to node `document.body.appendChild(element)`

### Activity
Students will go to their favorite websites and modify the DOM programmatically. Wikipedia and Twitter are good examples.

* Students should:
  * Select elements and save them to variables
  * Delete at least 2 elements
  * Modify elements (e.g., replace image url, change text, change CSS)
  * Create new elements and add to page

* Encourage students to think programmatically about the DOM by giving them problems that involve iteration and the use of multiple CSS selectors
  * Change all instances of one word
  * Replace all images on only a certain portion of the DOM
  * Change every other header
  * Bonus (Hard): replace all elements of one tag to another (e.g., `p` to `h1`)


[dom-intro-starter]: https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/javascript/dom-intro


# <a id="events">Events Lesson Plan</a>


### Outline
* 10 min Activation: Intro to Events
* 5 min Events & Dom 
* 10 min Callbacks
* 10 Understanding Event Flow
* 25 Adding a Form

### Prework
### Scope, Hoisting and First Class Functions
* https://github.com/learn-co-curriculum/fewpjs-jsf-scope
* https://github.com/learn-co-curriculum/fewpjs-jsf-scope-chain
* https://github.com/learn-co-curriculum/fewpjs-js-fundamentals-scope-lab
* https://github.com/learn-co-curriculum/fewpjs-js-fundamentals-lexical-scoping
* https://github.com/learn-co-curriculum/fewpjs-jsf-hoisting
* https://github.com/learn-co-curriculum/fewpjs-fns-as-first-class-data-do-behavior/
* https://github.com/learn-co-curriculum/fewpjs-fns-as-first-class-data-array-o-functions/
* https://github.com/learn-co-curriculum/fewpjs-functions-in-javascript
* https://github.com/learn-co-curriculum/fewpjs-reviewing-javascript-functions-quiz
### Events
* https://github.com/learn-co-curriculum/fewpjs-javascript-eventing
* https://github.com/learn-co-curriculum/fewpjs-event-listening/
* https://github.com/learn-co-curriculum/fewpjs-reviewing-javascript-events-quiz
* https://github.com/learn-co-curriculum/fewpjs-document-onload/
* https://github.com/learn-co-curriculum/fewpjs-acting-on-events/
* https://github.com/learn-co-curriculum/fewpjs-eventing-master

### Prework learning goals

* List different keywords for variable declaration 
* Explain the concept of variable scope
* Use var, const, or let when declaring variables 
* Identify a globally scoped variable
* Recognize naming conventions for JavaScript functions and variables
* Summarize the difference between var, const, and let

### Common Misconceptions
* Event listeners can be attached at any point in your code
* Events are only "listened for" once and then no longer 
* One element can’t have more than one listener
* Passing a callback is not the same as calling a function

### Lesson Learning Goals
* Recall the different types of JavaScript Events
* Identify when the `DOMContentLoaded` event will trigger
* Use `addEventListener` to invoke a callback function after an event
* Implement a callback event handler
* Use `event.preventDefault` to override a form submission

### Problem statement

What if I want my user to click a button and increase the number of likes on a photo? How can I make the page interactive? We know how to interact with the page via Javascript's DOM. Users only have access to what they can see: html elements. Events are a way to control what happens when users interact with those elements. 

### Activation
Open a web page and navigate through it: clicking buttons, expanding menus, hovering over buttons, entering text in inputs. Ask students to identify what are the different actions you are taking.  _E.g. a navbar: some buttons lead you to another page and some buttons that will produce an extended menu. Each of these elements has event listeners attached to them_

- Note: events are happening on the page all the time, just because I click a <p> element doesn't mean something will happen,  I have to attach a listener in order to trigger an action _when_ it does
- Add event listeners to the DOM using addEventListener on DOM elements
- addEventListener is an HOF that takes two arguments: a string designating the event type and a callback
- Look at MDN Event Reference to know which type of event to listen for 
- Some common events are: 'click', 'hover', 'keyup, 'keydown', 'DOMContentLoaded'

### Lesson 

### Events & DOM
Events are attached to elements via the DOM. Whenever a page is loaded in the browser the DOM is created shortly after. (Useful to remind students that DOM isn't something that comes with HTML/JS files but created when they load) 
* If we attach listeners in our code before the DOM has loaded, they might not be attached
* DOMContentLoaded is an event we can listen for on the document
* document.addEventListener('DOMContentLoaded', attachListeners)

### Callbacks
* Ok, I'm listening for the event, now what? 
* addEventListener takes a second argument which is the callback or function to run _when_ the event happens
* Show students the difference between this 
```js
p.addEventListener('click', handleClick() )
```
VS 
```js
p.addEventListener('click', handleClick)
``` 
_Passing a callback is not the same thing as invoking a function_ 

* First Class Functions:
- We are able to do this because in JS functions are "first class". 
- This means functions can be stored in variables
- Functions can be passed as arguments 
- Functions can be returned from other functions

### Check for Understanding: Event Flow

```js
let alertBtn = document.querySelector("#alert")
let consoleBtn = document.querySelector("#log")

document.addEventListener('DOMContentLoaded', function(){
	//step 2: attach event listeners after Dom has loaded
	alertBtn.addEventListener('click', handleAlertClick)
	alertBtn.addEventListener('pointerover', handleAlertHover)

	consoleBtn.addEventListener('click', consoleSomething)
})

//determine what happens for each listener, when will these functions be run?
function handleAlertClick(){

	window.alert("THIS IS AMAZING")
}

function handleAlertHover(){

	console.log("This button will trigger an alert!")

}

function consoleSomething(){

	console.log("Hey this is important!!")
}
``` 
Based on the above code, what will happen when a user:
1. Clicks on the alert button
2. Moves the mouse pointer over the alert button
3. Clicks the console button
4. Moves the mouse pointer over the alert button

### Adding A Form 
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/javascript/events-intro-revamp/starter_code) 
* In order to obtain user input, we use input tags and use their value attribute to access their contents

* Input types
-text (default)
-number
-submit
-radio/checkbox
-...many more

* There are two typical ways to handle a submission: using a form with a submit event or a button with a click event
* Gotchas to using form submit event:
-submit events can only be triggered by form elements
-preventDefault to prevent the default action of a submit event: a page reload
-Can grab the relevant inputs using the event object only if theinputs are children of the form; otherwise the inputs must be found manually

* Gotchas to using click event submission
-Pressing the return key will not submit
-You will not be able to use the event object to locate the target inputs and instead must be found manually
-Typical flow for a form:
1. User enters input
2. An event triggers (form submission or click)
3. In the event, relevant input elements are found
4. Values are pulled from input elements
5. Those values are used for whatever purpose (storing, sent out in a fetch for storage in a database)
6. Usually ends in some sort of DOM manipulation (creation or edition of elements)


#### Building Out Book App

1. Begin the process of building your Single Page App.
2. Starter Code: An HTML file with a hard-coded list of books.
4. By the end of this lesson, implement
    + A Form to create a new book
    + The form should append the new book to the DOM when submitted
    + The form should append an error to the DOM if the title is less than four characters

* Checklist:
- Get user input from form
- Create elements from user input
- Select the correct element to append to
- Append created elementt

---
title: Javascript Event Listeners
layout: post
---

# <a id="event-listeners">Event Listeners</a>

## SWBATs
* Create event listeners
* Distinguish between event types
* Explain when and why to use event listeners
* Write event listeners as stand-alone functions and in-line functions
* Use event listeners to manipulate the DOM
* Delegate events using the `event.target`
* Synthesize knowledge of forms with event listeners

## Resources

* [JavaScript Events](https://www.youtube.com/watch?v=Wvt6cj87vYQ)
* [Starter Code with Student Facing README][events-starter-code]

## Outline
```text
  10m | Introduction to Events
  10m | Inside an Event Listener Callback
  15m | Basic Event Implementation
  10m | Events and Forms
  15m | Event Delegation
  ----|----
  60m | TOTAL
```

### Introduction to Events

* Why use event listners?
  * As programmers, we interact with the DOM using JS; typical end-users do not
  * In order for a user to interact with a page, events must be triggered to initiate JS code
  * May be useful to go to a real website with a lot of user interaction and describe the listeners that are on that page
* Add event listeners to the DOM using `addEventListener` on DOM elements
* `addEventListener` is an HOF that takes two arguments: a string designating the event type and a callback
  * Useful to show an event listener callback defined as a normal function, then in-line
* [MDN Event Reference](https://developer.mozilla.org/en-US/docs/Web/Events)
* [W3Schools Event Reference](https://www.w3schools.com/jsref/dom_obj_event.asp)
* Highlight common event types:
  * `click `
  * `keydown` vs `keyup` vs `keypress`
  * `submit`
  * `DOMContentLoaded`

### Inside an Event Listener Callback

* When an event listener is called, the listener attempts to pass the event object to provided callback, therefore the event object is only available if we declare it as an argument.
* Different events have different properties
  * Mouse events have mouse coordinates
  * Key events have information about pressed key
  * Etc.
* `event.target`
  * Returns the DOM element upon which the event was triggered
  * `event.target.children` gives array of all children of that target
* `this` inside an event listener callback is `undefined`; use `bind` or arrow functions to bind context

### Basic Event Implementation

* Main goal is to show the overall pattern of event listeners
  * User interaction with the DOM leads to a function chain that typically ends in DOM manipulation
    1. Find DOM element that will act as trigger
    2. Add event listener to DOM element
    3. Inside of event listener callback one might:
      * Prepare data
      * `setTimeout` or `setInterval`
      * Change attributes/values of target or other DOM elements
      * Add or remove DOM elements
* Using a static HTML page, add event listeners to HTML elements to change their properties.
* Examples of things to show:
  * Iterate through a list and add event listeners that change their styling properties and/or text on click
  * Add an event listener to a `div` that on `keydown` adds that key to the text of one or more DOM elements.
  * Add a button that starts and stops a timer
  * Make a delete listener that deletes any element on the page `onClick` **this is a great example to preview event delegation**

  ```js
  document.addEventListener("click", (event)=>{
    event.preventDefault()
    event.target.remove()
  })
  ```

### Events and Forms

* In order to obtain user input, we use `input` tags and use their `value` attribute to access their contents
* [Input types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)
  * text (default)
  * number
  * submit
  * radio/checkbox
  * ...many more
* There are two typical ways to handle a submission: using a form with a `submit ` event or a button with a `click` event
  * Gotchas to using form `submit` event
    * `submit` events can only be triggered by form elements
    * `preventDefault` to prevent the default action of a submit event: a page reload
    * Can grab the relevant inputs using the event object only if theinputs are children of the form; otherwise the inputs must be found manually
  * Gotchas to using `click` event submission
    * Pressing the return key will not submit
    * You will not be able to use the event object to locate the target inputs and instead must be found manually
* Typical flow for a form:
  1. User enters input
  2. An event triggers (form submission or click)
  3. In the event, relevant input elements are found
  4. Values are pulled from input elements
  5. Those values are used for whatever purpose (storing, sent out in a fetch for storage in a database)
  6. Usually ends in some sort of DOM manipulation (creation or edition of elements)


### Event Delegation
* Useful to show students HTML that is nested **and** can execute two different actions
  * An example of this is a `div` -> `ul` -> many `li` structure. The `li` can contain both some text and a button: clicking the text executes one action; clicking the button executes another. This allows us to show two types of delegation: delegation with a dynamic number of elements (i.e. the list) and delegation with different outcomes (i.e. the two actions)

    ```html
    <div>
      <ul>
        <li>
          <text>Meow</text>
          <button>Delete</button>
        </li>
        <li>
          <text>Woof</text>
          <button>Delete</button>
        </li>
        <li>
          <text>Quack</text>
          <button>Delete</button>
        </li>
      </ul>
    </div>
    ```

    ```js
    let textEls = document.querySelectorAll('text')

    textEls.forEach(text => {
      text.addEventListener("click", (event) => alert(event.target.textContent))
    })

    let buttons = document.querySelectorAll('button')

    buttons.forEach(button => {
      button.addEventListener("click", (event) => event.target.parentNode.remove())
    })
    ```
* Stress the point that without delegation, we would have to add event listeners to every element individually
  * A prebuilt form that `onSubmit` appends another element to the list would be handy. Show them that the event listeners need to be added at the time of the element's creation

    ```html
    //...above mentioned code

    <form>
      <input id="noise-input" type="text" placeholder="Make a noise!" />
      <input type="submit">Submit!</input>
    <form>
    ```
    
    ```js
    let form = document.querySelector('form')

    form.addEventListener('submit', (event) => {
      event.preventDefault()
      let input = document.querySelector("input#noise-input")
      let ul = document.querySelector("ul")


      let text = document.createElement("text")
      text.textContent = input.value
      text.addEventListener("click", (event) => alert(event.target.textContent))

      let button = document.createElement("button")
      button.textContent = "Delete"
      button.addEventListener("click", (event) => event.target.parentNode.remove())

      let li = document.createElement("li")
      li.append(text)
      li.append(button)

      ul.append(li)

      input.value = ""
    })

    ```
* Aside to bubbling and capturing
  * Events bubble up from children to parents all the way up to the top of document, triggering all event listeners along the way

    ```html
    <div id="container">
      <ul id="list">
        <li id="item">Click Me!</li>
      </ul>
    </div>
    ```

    ```js
    let div = document.getElementById("container")
    let ul = document.getElementById("list")
    let li = document.getElementById("item")

    function logThisAndTarget(event){
      console.log("THIS", this)
      console.log("TARGET", event.target)
    }
    div.addEventListener("click", logThisAndTarget)
    ul.addEventListener("click", logThisAndTarget)
    li.addEventListener("click", logThisAndTarget)
    ```

  * `stopPropagation` can be used to prevent bubbling
* We can use bubbling to our advantage by attaching the listener to a container element and using attributes of the `event` to identify the precise element upon which the event was triggered.
  * Use the event to identify which action to trigger

    ```js
    function listener(event){
      switch (event.target.tagName){
        case "LI":
          console.log("li things")
        case "BUTTON":
          console.log("button things")
        default:
          console.log("everything else")
      }
    }
    ```
  * Use the event to identify which item in a list was clicked using a dynamically generated id
    * Useful to show the use of the `data` attribute on HTML elements as a better alternative

    ```html
    <div id="noise-container">
      <ul>
        <li data-animal="cat">
          <text>Meow</text>
          <button>Delete</button>
        </li>
        <li data-animal="dog">
          <text>Woof</text>
          <button>Delete</button>
        </li>
        <li data-animal="duck">
          <text>Quack</text>
          <button>Delete</button>
        </li>
      </ul>
    </div>
    ```

    ```js
    let noiseContainer = document.querySelector("div#noise-container")

    noiseContainer.addEventListener('click', event => {

    })

    ```


[events-starter-code]: https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/javascript/events-intro

---
title: Javascript Promises And Fetch
layout: post
---

# <a id="promises">Promises and Fetch</a>

## SWBATs
* Distinguish between sync and async code
* Recognize code that uses Promises
* Use the `.then` method to add handlers for promise resolution
* Use the options to `fetch()` to configure requests

## Resources

If they haven't already seen the [loupe][loupe-site] video and playground when experimenting with events, students should play with this site to help them build an intuition for the execution stack.

#### [Intro to Promises][promises-video]
#### [Alternate Lecture Video][promises-video-alt]
#### [Starter Code with Student Facing README][ajax-fetch-starter]
#### [MDN Promises][mdn-promises]
#### [We Have a Problem With Promises][problem-promises]

## Outline

```text
  10m | Introduction to Async
  10m | What is a Promise?
  15m | Example of Promises with Fetch
  10m | Methods On The Promise Chain
  15m | Intro to `fetch`
  ----|----
  60m | TOTAL
```

## Introduction to Async

* Javascript is _synchronous_
  * It executes statements one at a time
* But... sometimes things take a long time
  * We don't want these things to block UI rendering
  * When we are waiting for javascript to run, the page is not responsive

```js
function sleep(n) {
  var i = 0
  while(i < (12 ** 8) * n) {
    i++
  }
}

sleep(10)
```

* Instead of waiting for things to happen _synchronously_, we want to have some code run later
* What patterns have we seen to handle this kind of problem already?
  * Callback functions as handlers for event listeners
  * `setTimeout` and `setInterval`
* That code runs _asynchronously_

## Examples of Sync and Async code
* Ask students to suggest examples of code that runs sync and async

Synchronous:
- Most of ruby
- `sleep`, `RestClient.get`

Asynchronous:
- `setTimeout` and `setInterval`
- event listeners
- database access
- network calls

* So far, we've used _callback functions_ to set up code to run later
* Promises are another way of writing async code

## What is a Promise?
* Promises are a container for data that will show up later
  * And, information about whether the data is there yet
* Metaphors:
  * Coffee that you've set to brew
  * Online order confirmation email / receipt

> Warning: Potential rabbit-hole. It’s tempting to go to deep into the Promise API - we want to make sure that students understand the high level of a Promise, and be ready to use lots of fetches. It’s rare that they’ll use the Promise constructor, Promise.resolve, Promise.race, or even Promise.all.

### Example of Promises with Fetch
* Let's see some real-live promises!
* We're going to use `fetch`, which is a function for sending HTTP requests
(in the console:)

```js
var url = "https://dog.ceo/api/breeds/image/random"
var promise = fetch(url)
promise
```

* See that the `promise` object doesn't have the _response_ but instead a _box with the response inside_
* `.then` - We can add a handler that runs when the response arrives

```js
function afterResolved() {
  console.log('resolved')
}
promise.then(afterResolved)
```

* `.then` is like adding an event handler - it has code to run later
* But we can also still see the promise itself - we have the object!

```js
function otherFunction() {
  console.log('another thing!?!?')
}
promise.then(otherFunction)
```

### Promise Methods: `then` and `catch`

* `then` is a little bit different from event listener callbacks.
* `then` is Chainable:

```js
var promise = fetch(url)
promise
.then(() => console.log('resolved'))
.then(() => console.log('after logging resolved'))
.then(() => console.log('after logging after resolved'))
```

_Common Bug_: evaluating a function instead of passing it to `then`

Q: When will the message be logged?
```js
var promise = fetch(url)
promise.then(console.log("message"))
```

A: Before the fetch resolves!

Fix is to use an anonymous function (with the `function` keyword or an arrow)

* Error Handling with `catch`
* If there's an error on the other end of the fetch, you can handle the error with `catch`

```js
fetch("https://www.google.com")
.then(res => console.log(res))
.catch(error => console.log("Here's the error:", error))
```

* The cool bonus that we get from `catch` - if there's an error somewhere in our `then` handler, we'll catch that too!

### An Intro to `fetch`
* Let's take a closer look at the `fetch` method.

```js
fetch("https://dog.ceo/api/breeds/list/all")
.then(res => console.log(res))
```

* We get back a Promise from `fetch`, which we can add handlers to with `then`
* The handler that we pass to `then` gets a `Response` object
* We can call the `.json` method on the `Response` to get a promise for the parsed json from the response

```js
fetch("https://dog.ceo/api/breeds/list/all")
.then(res => res.json())
.then(json => console.log(json))
```

* If the response is not formatted as JSON, we can use `.text` instead

```js
fetch("https://dog.ceo/api/breeds/list/all")
.then(res => res.text())
.then(text => console.log(text))
```

## Challenge

Starting with a file `index.js` with:

```js
var url = "https://dog.ceo/api/breeds/image/random/4"
```

and a standard `index.html` that loads the `index.js`

Add javascript so that
- on page load
- fetch the images
- parse the response as json
- add image elements to the DOM for each image in the array

## Resources

[loupe-site]: http://latentflip.com/loupe
[promises-video]: https://youtu.be/aVNzq8u0F0E
[promises-video-alt]: https://youtu.be/35VNmpGKJCE
[ajax-fetch-starter]: https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/javascript/ajax-fetch-intro
[mdn-promises]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[problem-promises]: https://pouchdb.com/2015/05/18/we-have-a-problem-with-promises.html

---
title: Javascript Fetch And Dom
layout: post
---

# <a id="fetch">Fetch and DOM Manipulation</a>

## SWBATs
* Understand why we request data asynchronously
* Create Fetch requests (including GET, POST, PATCH, DELETE)
* Manipulate the DOM in conjunction with fetch calls

## Resources
* [MDN Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
* [JSON Server](https://github.com/typicode/json-server)
* [Starter Code with Student Facing README](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/javascript/full-crud-ajax)

## Example Videos
* [Video1](https://www.youtube.com/watch?v=1jvtdnp33cc)
* [Video2](https://www.youtube.com/watch?v=CKcSkanVYZQ)

## Outline

```text
  5m | Introduction to SPA
  5m | Planning/Code Structure
  15m | GET Fetch (rendering objects to the DOM)
  15m | POST Fetch (and dynamically updating the page)
  5m | Optimistic Rendering vs Promise Callback
  10m | PATCH Fetch and/or DELETE Fetch (if time permits)
  5m | Problem Solving Tips
  ----|----
  60m | TOTAL
```

### Introduction to SPA
* Introduce them to the concept of SPA and how there is no page reload and no request is ever made to fetch a new webpage (only requests for more data are made)
* Reiterate why async is preferred (superior user experience)
* Show them an example of a simple SPA they can build out in class
* Quickly explain JSON server if needed

##### Example SPAs
![Example2](../assets/FetchDom2.png)

### Planning/Code Structure
* Before jumping into coding, have them plan out the app
* User stories
  - As a user, I should see pokemon when I visit the webpage
  - As a user, I should be able to fill out the form to create a new Pokemon
  - As a user, I should be able to remove Pokemon
* What event listeners will we need?
  - on load of the page
  - on submit of the form
  - on click of a Pokemon (to delete it)
* What functions/pseudo code can we write?

### GET Fetch (rendering objects to the DOM)
* On `DOMContentLoaded`, make a `GET fetch` request and render the contents onto the DOM
* Good idea to show them GET all vs. GET one and how the data looks different (object vs. array)

```js
function render(pokemon){
  let pokemonCard = document.createElement('div')
  pokemonCard.innerHTML +=`<div class='card'
    id='pokemon-${pokemon.id}'><h2>${pokemon.name}</h2>
    <img src="${pokemon.sprite}"/></div>`
  document.getElementById('pokemon-container').appendChild(pokemonCard)
}
function fetchAllPokemon(){
  fetch(`http://localhost:3000/pokemon/`)
  .then((response) => response.json())
  .then((jsonData) => {jsonData.forEach((pokemon) => render(pokemon))})
}
```

### POST Fetch (and dynamically updating the page)
* Will need a form most likely
* Explain difference between `GET fetch` and `POST fetch`

```js
fetch(url, {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  },
  body: JSON.stringify({   })
  .then(response => response.json())
  .then(pokemon => {render(pokemon)})
})
```
* Body data needs to be a string

### Optimistic Rendering vs Promise Callback
* You can manipulate the DOM synchronously (outside the `.then()`)
 * This is referred to as optimist rendering because you are not waiting for the async response to resolve
* Or you can manipulate the DOM asynchronously (inside the `.then()`) using the response from the server
 * This is make sure the data on your page is consistent with the database

### PATCH Fetch and or DELETE Fetch
* Explain the difference between POST, PATCH, and DELETE
 * PATCH requires the same headers but body only needs the data to be updated rather than the entire resource object
 * DELETE is like GET but has options object `{method: "DELETE"}`
 
 ```js
  fetch(`http://localhost:3000/pokemon/${id}`, {method: "DELETE"})
  .then((response) => {document.getElementById(`pokemon-${id}`).remove()})
 ```

### Problem Solving Tips
* Some students struggle with knowing what to do or where to start
* A common suggestion is to build out each feature iteratively and think about the features in the context of a user story. For example: “When <some event happens>, I want to make a <what kind of> fetch call and manipulate the DOM <in what way?>”
 * When the page loads, I want to make a GET `fetch` render a list of books
 * When a user clicks the ‘Edit’ button, I want to make a PATCH `fetch` and update this DOM element
 * When a user clicks the ‘New’ button, I want to make a POST `fetch` and render the new dog on the page
 * When a user clicks this ‘Delete’ button, I want to make a DELETE `fetch` and remove this element from the DOM

### Starter Code
 * [Pokedex App](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/javascript/full-crud-ajax)

### Other Starter Code Options
 * [Monster Challenge](https://github.com/learn-co-curriculum/monsters-practice-challenge)
 * [Pokemon Teams](https://github.com/learn-co-curriculum/pokemon-teams)
 * [Dumbo's Brew App](https://github.com/learn-co-students/dumbo-web-042318/tree/master/23_fetch)

 ---
title: Object Orientation
layout: post
weight: 10
hidden: true
---

# <a id="oo">Object Orientation:</a>

===


**Course**: Software Engineering   
**Mod**: 3                    
**Topic**: Object Orientation  
**Amount of time**: 1 hour 
**Author**: Joshua Miles


***

## Lesson Summary:

#### Topic:
JavaScript Object Orientation in the context of rendering visual elements.

#### Learn.co material:
- https://github.com/learn-co-curriculum/fewpjs-object-orientation-in-javascript/
- https://github.com/learn-co-curriculum/fewpjs-oo-classes-and-instances
- https://github.com/learn-co-curriculum/fewpjs-oo-classes-vs-instances-instrumental
- https://github.com/learn-co-curriculum/fewpjs-oo-initializing-instances
- https://github.com/learn-co-curriculum/fewpjs-oo-predicting-constructor-effects-instrumental
- https://github.com/learn-co-curriculum/fewpjs-adding-behavior-with-methods
- https://github.com/learn-co-curriculum/fewpjs-oo-predicting-method-returns-instrumental
- https://github.com/learn-co-curriculum/fewpjs-oo-method-types/
- https://github.com/learn-co-curriculum/fewpjs-getter-and-setter-methods
- https://github.com/learn-co-curriculum/fewpjs-oo-static-methods-lab

#### Prerequisite knowledge/ Prework:
- Define class in your own words
- Recognize the syntax of a class
- Define instance in your own words
- Identify the components of a class (class keyword, constructor, methods)
- Identify the object, method, and argument when invoking a method
- Define message receiver in the context of OOP
- Define this in OOP
- Define message in the context of OOP
- Explain the Single Responsibility Principle


#### Learning goals for this lesson:
- Implement a class which represents a real-world concept (i.e. Dog, Baby)
- Describe how to assign properties to instances of classes
- Explain when and why to use class properties and methods
- Implement a class which represents a piece of UI (Navbar, Form, etc.)


#### Misconceptions:
- A Class is an instance (object). Students often conflate the idea of a Class and an Instance of that Class. It is important to be extremely precise in defining and using these terms throughout a students attempts to master the concepts of Object Oriented JS.
- `floorTile.width` is the same as `width.floorTile`. We access properties using the `object.property` syntax, which will register for some students automatically, but will throw other students for a loop.
- `this` is the same as `self` in ruby. This is a particularly insidious misconception because the two concepts are *so* similar. But there is a difference. `this` is context specific, and `self` really isn't. This is not a rabbit trail we need to indulge at this exact moment in a student's journey, but it is important to proactively frame these keywords as being *similar*, not identical, from the beginning.

Be careful with the word Object when talking about classes in JS. Technically, classes are Objects, so we must differentiate between little-o and big-o objects.


***

## Lesson Outline:

**Step**: Problem 
**Time**: [ 5 ] min

_Goal/Scenario:_
As of our previous lesson, we have a working application which can peform CRUD operations on our collection of books. Today we are going to take a critical look at our code, and explore how JavaScript's `class` keyword can act as a tool for organizing the code for our application by grouping **data** and **behavior**.

_Learning Goals in sequence:_
- Implement a class which represents a real-world concept 
- Explain when and why to use class properties and methods
- Implement a class which represents a piece of UI 


**Step**: Activation 
**Time**: [ 5 ] min
Review the code from the prior exercise on events.
  * What is an instance of a class?
  * Define an instance as the combination of attributes (data) and methods (behavior), and show how both of these are present when we write a function (behavior) which creates a DOM element for to represent a specific book (data).
  * Hopefully this is a question students can already answer from Mod 1, reviewing here explicity Correlates this lecture to Ruby Object Orientation


**Step**: Learning Goal 1:  Implement a class which represents a real-world concept 
**Time**: [ 20 ] min

_Demonstrate_: 
Begin by building a simple class which represents a simple class which represents a square:
```javascript
class Square {

}
```
Clarify that the class is not an instance - it is simply a template that JavaScript will later use to create an object when we tell it to. We create objects (instances) from classes by using the `new` keyword.
Using the chrome console, create an instance of a square:
```javascript
    let floorTile = new Square
```
This is called **instantiating** a class, using the class to create a new object. Show how `floorTile != Square`- the former is a specific example of a square, the latter is just a template, a way for us to tell JavaScript how Squares should generally behave once we've created them. Of course, right now we haven't told JavaScript anything about how squares behave, because our class is empty! Let's add a **method**:
```javascript
class Square {
    constructor(){
        this.sideLength = 10
    }
}
```
The constructor method for a JavaScript class is the same as `initialize` in Ruby - describe how it is a method called when a class is instantiated. Throw  `console.log("A Square was created!")` into the `constructor`, then instantiate the object in the console: 
```javascript
let floorTile = new Square // => "A Square was created"
let ceilingTile = new Square // => "A Square was created"
```
Inspect `floorTile` and `ceilingTile`- they both have a `sideLength`, because our constructor is telling JavaScript that when a square is created, it should have a `sideLength` of "10". We can reference `floorTile.sideLength` or even change it's value:
```javascript
floorTile.sideLength = 5;
```
Contrast the difference here from how Ruby's objects work. In Ruby, object attributes cannot be accessed unless the attribute has a `reader`, an attribute cannot be changed unless it has a `writer`. In JavaScript, we don't need to define `writer`s or `reader`s.
Inside the class, we can reference the attribute as `this.sideLength`:
```javascript
class Square {
    constructor(sideLength){
        this.sideLength = sideLength
    }

    area(){
        return this.sideLength * this.sideLength
    }
}
```
Demonstrate how, after instantiation, we can call `.area()` on a Square instance, and get back the product of the squares sideLength.
Of course, not all squares are the same size, so we should replace "10" with a variable, and supply it when we create a new square:
```javascript
class Square {
    constructor(sideLength){
        this.sideLength = sideLength
    }

    area(){
        return this.sideLength * this.sideLength
    }
}
```
In the console:
```javascript
let floorTile = new Square(5) 
let ceilingTile = new Square (20)
```
Draw attention to the fact that variables "passed into" the "class" are actually sent to the constructor, then demonstrate that the `.area()` method returns different values depending on the size of the Square.

_Application_: 
Challenge the students to help you refactor the Square class to a more general rectangle class, acting as the navigator as you drive the code and guide them towards a working example:
```javascript
class Rectangle {
    constructor(height, width){
        this.height = height
        this.width = width
    }

    area(){
        return this.height * this.width
    }
}
```

**Step**: Learning Goal 2: Explain when and why to use class properties and methods 
**Time**: [ 10 ] min

_Demonstrate_: 
What if we wanted a method which returned the largest of an array of rectangles?
It wouldn't make sense for that to be an instance method for a *single* rectangle, because the logic must consider the sizes of *multiple* rectangles. 
And yet, we would prefer that the logic be contained inside the Rectangle class somehow. This is where **static** methods become handy.

Static methods are defined by simply putting static in front of a method name:
```javascript
class Rectangle {
    constructor(height, width){
        this.height = height
        this.width = width
    }

    area(){
        return this.height * this.width
    }

    static largestOf(rectangles){
        let largest = rectangles[0]
        rectangles.forEach( rectangle => {
            if(largest.area() < rectangle.area()){
                largest = rectangle
            }
        })
        return largest
    }
}
```
When a method is declared "statically", it can be accessed on the class itself, rather than on instances of that class, e.g., on `Square` rather than `floorTile`:

```javascript
Square.largestOf([ floorTile, ceilingTile ]) // ceilingTile
```

_Application_: 
Challenge the students to help you add a `smallestOf` static method, acting as the navigator as you drive the code and guide them towards a working example:
```javascript
class Rectangle {
    constructor(height, width){
        this.height = height
        this.width = width
    }

    area(){
        return this.height * this.width
    }

    static largestOf(rectangles){
        let largest = rectangles[0]
        rectangles.forEach( rectangle => {
            if(largest.area() < rectangle.area()){
                largest = rectangle
            }
        })
        return largest
    }

    static smallestOf(rectangles){
        let smallest = rectangles[0]
        rectangles.forEach( rectangle => {
            if(smallest.area() > rectangle.area()){
                smallest = rectangle
            }
        })
        return smallest
    }
}
```

**Step**: Learning Goal 3:  Implement a class which represents a piece of UI (Navbar, Form, etc.) 
**Time**: [ 5 ] min

_Demonstrate_: 
One way we can use classes in JavaScript is for a class to represent a piece of our interface! Typically, we do this by giving such classes a **render** method:
```javascript
class Rectangle {
    constructor(height, width){
        this.height = height
        this.width = width
        this.element = document.createElement('div')
    }

    area(){
        return this.height * this.width
    }

    render(){
        this.element.style.height = `${this.height}px`
        this.element.style.width = `${this.width}px`
        this.element.style.borderStyle = 'solid'
        return this.element
    }

    ...
}
```
Now we can use the render method to create visual representations of our object and append them to the DOM!
We can use all of the same DOM tools we've been learning in Mod 3 to create robust visual elements within the organizational context of a class.
```javascript
document.body.append(floorTile.render())
```

Continue to explore how we can make these DOM elements dynamic by adding event listeners to the `Rectangle#element`:
```javascript
class Rectangle {
    constructor(height, width){
        this.height = height
        this.width = width
        this.element = document.createElement('div')
        this.element.addEventListener('click', function(){
            console.log(`I am ${this.height}x${this.width}`)
        })
    }
    ...
}
```
Then instantiate a rectangle and append it to the DOM once again.
This is an excellent opportunity to poll the class and ask what we will get back if we click the rectangle- the seemingly obvious answer would be the logging of a message which includes the dimensions of the rectangle.
When you test this hypothesis, however, you will get a bizzare result, probably something like: `I am undefinedxundefined`. 
This is an **awesome** opportunity to explore how `this` is different than `self`- because we are inside of another fuction, a callback which is passed to `addEventListener`, the context of `this` has changed! Log `this` inside of the callback to show that it is no longer `floorTile`.
Show how we can use an **arrow function** to ensure that `this` keeps the correct value. Arrow functions are functions which effectively forfeit their right to a proper `this`- instead, `this` inside of an arrow function will be the exact same as `this` *where the arrow function is defined*. This is why arrow functions are extremely useful for defining callback functions.


_Application_: 
Challenge the students to help you to implement an event listener, such that when a rectangle is clicked, it doubles in size. Act as the navigator as you drive the code and guide them towards a working example:
```javascript
class Rectangle {
    constructor(height, width){
        this.height = height
        this.width = width
        this.element = document.createElement('div')
        this.element.addEventListener('click', () => {
            this.height = this.height * 2
            this.width = this.width * 2
            this.render()
        })
    }

    area(){
        return this.height * this.width
    }

    render(){
        this.element.style.height = `${this.height}px`
        this.element.style.width = `${this.width}px`
        this.element.style.borderStyle = 'solid'
        return this.element
    }
    ...
}
```


**Step**: Integration:  
**Time**: [ 15 ] min

_Synthesis_: 
Now that we've seen how to use JavaScript classes to create objects, and how to use objects to group together the data and behavior of a UI component, let's apply these concepts by modeling the UI of our book application with objects.

_Application_: 
This part will vary depending on how you've built out your application thus far. Break the refactoring into these basic steps:

* Create a BookListItem class
* As you map over books, create instances of the BookListItem class
* Append book.render() to the book_list
* Instantiate the BookListItem class when the new_book_form is submitted
* Append book.render() to the book_list

Here is a finished example:

```javascript
// BookListItem.js
class BookListItem {

    constructor(options){
        this.title = options.title
        this.author = options.author
        this.image = options.image
    }

    render(){
        this.element.innerHTML = ''
        this.element.className = 'card'

        const img = document.createElement('img')

        img.src = this.img

        const h3 = document.createElement('h3')

        h3.textContent = this.title

        const p = document.createElement('p')

        p.textContent = this.author

        //add all elements to this.element

        this.element.appendChild(img)

        this.element.appendChild(h3)

        this.element.appendChild(p)
        
        return this.element
    }

}
```


```javascript
// index.js
const book_list = document.querySelector('#book-list')
const new_book_form = document.querySelector('#new-book-form')

books.map(attributes =>{
    let book = new BookListItem(attributes)
	book_list.appendChild(book.render())
})

new_book_form.addEventListener('submit', e => {
    let book = new BookListItem({
        title: e.target.title.value,
        author: e.target.author.value,
        img: e.target.img.value,
    })
    book_list.append(book.render())
})

```

```html
<!-- index.html --> 
<!DOCTYPE html>
<html>
    <head>
        <title>Favorite Books</title>
        <link href="style.css" rel="stylesheet"/>
    </head>
    <body>
        <!-- Change the font from google fonts--> 
        <h1>Book List</h1>

        <form action='' id="new-book-form">
            Book Title:<br>
            <input type="text" name="title" value="">
            <br>
            Author:<br>
            <input type="text" name="author" value="">
            <br><br>
            Book Cover URL:<br>
            <input type="text" name="img" value="">
            <br>
            <input type="submit" value="Submit">
        </form> 

        <!-- add some css to the card div--> 
        <div id='book-list'>
            <div class = 'card'>
                <img src = 'https://images-na.ssl-images-amazon.com/images/I/31AYTZWPCPL._SX309_BO1,204,203,200_.jpg'/>
                <h3>Soul Kiss</h3>
                <p>Shay Youngblood</p>
            </div>
        </div>

        <script src ='BookListItem.js'></script>
        <script src ='books.js'></script>
        <script src='index.js' ></script>
    </body>
</html>
```
