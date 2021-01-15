### Phase 2

- [React Intro](#intro)
- [React Best Practices](#best-practices)
- [React Props and State](#props-and-state)
- [React State and Forms](#state-and-forms)
- [React Component Lifecycle](#lifecycle)
- [React Router](#router)

## Lecture Notes

---
title: React Intro
layout: post
---

# <a id="intro">Intro To React</a>

## SWBATs

* Understand build tools and show how webpack works
* Use historical context and the Mod 3 experience to explain why React and declarative programming is special
* Start to understand the Virtual DOM
* See what a React Component actually is (an object, made by a class or function)
* Build custom components and see initial JSX

## Resources

* [Example Video](https://www.youtube.com/watch?v=_RrcmQcfRkQ)
* [Super Minimal Starter Code](https://github.com/learn-co-curriculum/react-lecture-1-starter)
  * _'webpack' branch has boilerplate webpack setup_

## Outline

     5m Discuss Vanilla JS
     5m Brief History/Context
    15m Project Set Up
     5m Briefly on Virtual DOM
    15m myCreateElement
    20m Navbar Student Exercise
    15m JSX
    ===
    80m Total

### Discuss Vanilla JS

I like to start by asking students what was hard about building a project in Module 3 and record their responses. Generally you'll get at least a few responses that are pretty on point. Examples:

* Updating the DOM to reflect changes in your data
* Managing State
* state lives in different places
* difficult to keep the DOM in sync correctly
* keep track of changes to state
* How to organize code

point out what React is designed to solve and what it isn't.

### Brief History/Context

React is made by Facebook. I like to point out that if anyone's ever heard about the licensing thing (i.e. you can't build an app that competes with FB in React) that's no longer true and React uses the MIT open source license. There are two libraries `react`, `react-dom`, this is to divide up the functionality and enables `react-native`, `react-vr`, etc.

### Project Set Up

To start I will not use webpack or anything special. I'll just include react and react-dom in my index.html.

_Though I point out and stress that I am not doing this like how the weekend labs are set ups:_

* _I am not going to write `import React from 'react'`_
* _I am not going to run `npm start`_
* _I am just doing this like in last module._

_When I break into some exercises later everyone asks why they cant run npm start and why they won't be importing React, I remind them that we are just including some js files in out html like last module._

First, `npm install --save react react-dom semantic-ui-css`. Discuss how npm differs from installing gem. Show node_modules folder, (mention that if a student can't see their directory-- it's there-- they just need to enable seeing .gitignore'd files in atom). Show that we're just linking to js/css files in our index.html. I've had some issues if I do not use these specific links:

```html
<link rel="stylesheet" type="text/css" href="node_modules/semantic-ui-css/semantic.min.css">
<script src="node_modules/react/umd/react.development.js"></script>
<script src="node_modules/react-dom/umd/react-dom.development.js"></script>
```

Now in index.js
`ReactDOM.render` take two args:

```js
ReactDOM.render(whatToAddToDOM, whereToPutIt);
```

Demonstrate that the second arg is the **only place we will be using code from mod 3 such as `document.getElementById('main')`**. This is also why we won't be bringing in jQuery. It'd be overkill to import a huge library to run one line of code `$('#main')`

whatToAddToDOM: we need to add a React Element! First thing I'd do is to write like:

```js
ReactDOM.render(React.createElement('h1'), document.getElementById('main'));
```

And inspect the HTML, an h1 will be there, but we won't see any text. Change it to:

```js
// mention that we won't quite talk about
// this second arg, the 'props' yet
ReactDOM.render(
  React.createElement('h1', {}, 'hello'),
  document.getElementById('main')
);
```

And we'll see it on the page!

### Briefly on Virtual DOM

Put a debugger and look what `React.createElement` returns. Ask what that looks like: an object-- that's it! That's what the Virtual DOM is, a plain JS object that builds up a picture of what the real DOM should look like. Reminder: html is just a string, the DOM is a _representation_ of that string we can interact with programmatically, ask questions to, etc. Virtual DOM is a representation of that representation. React will be in charge of making sure the real DOM looks like and will always be in sync with the virtual DOM. Declarative vs. Imperative.

### myCreateElement

If `React.createElement` just returns an object we should be able to write this on our own. Here's the bare minimum needed. (Refs we wont talk about today, symbols they maybe haven't seen (but they're basically just like Ruby symbols), and we'll talk more about props soon)

```js
const myCreateElement = (type, props = {}, children) => {
  return {
    $$typeof: Symbol.for('react.element'),
    type: type,
    props: { children: children },
    ref: null
  };
};
```

Use your function instead of React's. Cool!

Now present the problem of wanting to create an "Article", i.e. some type of title in an h1, followed by the text in a p tag. How can we do this?

Someone should know that you'll have to wrap the whole thing in another element such as a div. Point out that this isn't like a React thing its just a programming thing. CreateElement is a function that returns an object. You can't return 2 things from a function. Talk through children being an array (not nested nodes, but siblings)

```js
ReactDOM.render(
  myCreateElement('div', {}, [
    myCreateElement('h1', {}, 'My Title'),
    myCreateElement('p', {}, 'some text of article')
  ]),
  document.getElementById('main')
);
```

Refactor to a function:

```js
const Article = props => {
  return myCreateElement('div', {}, [
    myCreateElement('h1', {}, props.title),
    myCreateElement('p', {}, props.text)
  ]);
};

ReactDOM.render(
  Article({ title: 'Title', text: 'some text' }),
  document.getElementById('main')
);
```

What if you wanted to add a CSS class. Why can't we use the keyword 'class'. Make sure to change myCreateElement to merge in props. Talk about ES2015 all the time.

```js
const myCreateElement = (type, props = {}, children) => {
  return {
    $$typeof: Symbol.for('react.element'),
    type: type,
    props: { ...props, children: children },
    ref: null
  };
};

const Article = props => {
  // show how we'll see this in the HTML
  // virtual dom = picture of what html should look like
  return myCreateElement('div', { className: 'article' }, [
    myCreateElement('h1', { className: 'header' }, props.title),
    myCreateElement('p', { className: 'body' }, props.text)
  ]);
};
```

### Navbar Student Exercise

If we were able to write a function which returns a React element which produces some html, we should be able to continue building out functions which return React elements.

I provide them some markup for a navbar with semantic ui css (provided in starter code)

```js
// <div class="ui inverted orange menu">
//     <a class='item'>
//       <h2 class="ui header">
//         <i class="paw icon"></i>
//         <div class="content">
//           ZooKeepr
//         </div>
//         <div class="sub header">
//           Keep track of your animals
//         </div>
//       </h2>
//     </a>
//   </div>
```

Student Task: write a function called Navbar I would expect to be used like this:

```js
const Navbar = props => {
  // ...
};

ReactDOM.render(
  Navbar({
    title: 'ZooKeepr',
    icon: 'paw',
    color: 'green',
    description: 'keep track of your animals'
  }),
  document.getElementById('main')
);
```

_A lot of students will try do like `class Navbar extends React.Component`.... NOPE! we are just writing a function which returns an object! Students will raise their hands and ask why `npm start` doesn't work. NOPE! They should just open the index.html in their browser like before_

Be very clear about it's just playing this nesting game of React.createElement inside of React.createElement. Have them look at the example markup and identify how many children each element has to determine if they need to pass an array or another element. Perhaps get them started on right track.

### JSX

Show solution, ok cool, but if this was how we had to write React it would not be the popular framework it is. Refactor to using JSX (on webpack branch). Ask why we would need to import React even if we don't see the variable used. Because JSX is just sugar for React.createElement!! It's all just JavaScript!!

Compare `{}` in JSX to ERB. They mean "evaluate this as JavaScript". Show an example like `<h1>props.title</h1>` vs. `<h1>{props.title}</h1>`

Start pulling things into different files. Mention no way around `import React from 'react'` in each file, that's normal get used to it, learn to like it. Time permitting show an `App` component that renders other components, `Navbar` + `Article`. Start defining Components.

---
title: React Best Practices
layout: post
---

# <a id="best-practices">React Best Practices</a>

## Overview
```
15m - What makes a good component?
15m - Syntax and Convention
10m - Exercise - refactoring a big component
5m - Common Gotchas
5m - How to think about React Performance
5m - A Peek at React's Advanced Features
5m - Developer tools and learning more
--
60m
```

> Note: There's more here than can be covered in the time allotted. Focus on what makes a good component and the refactoring exercise. Mention the performance, advanced features, patterns, and developer tools, but don't get bogged down in covering all of them.

## Resources
[Video](https://youtu.be/B1IArTphY1k)

### Architecture - What makes a good component?
- Container vs. Presentational Components
- Many small components is better than a few big components
- logic in `render` vs. extracting
- If you have a method that returns JSX, consider making it a component
- Reduce State
- Reduce options
- Avoid `style=` and `className=` by using well-named components

consider:

```
<div style={{float: ‘left’, width: ‘80%’}}>
  Main content
</div>
<div style={{float: ‘left’, width: ‘20%’}}>
  Sidebar content
</div>
```

vs:

```
<Main>
  Main content
</Main>
<Sidebar>
  Sidebar content
</Sidebar>
```

### Syntax and Convention
- Destructuring Props
- Spread and Rest operators
- name props well (clear, consistent, concise)
  - Use the same key/value name in your objects
- constructor vs. ES7 instance variables (`state = { count: 0 }`)
- defaultProps and function default values
- Conditional rendering: ternaries vs. methods vs. short circuiting vs. IIFEs
- classnames [helper](https://github.com/JedWatson/classnames)
- separate your imports
- colocate your files
- avoid unneeded callbacks, e.g.:

```
const isActive = el => el.active;

flights.filter(flight => isActive(flight));
flights.filter(isActive);
```

### Gotchas
- https://github.com/timhwang21/react-gotchas
- capitalize ComponentNames
- set `displayName` property of component
- JSX Comments `{ /* comment  */ }` (not `// <Component>`)
- setting state from props (but if you do, use `getDerivedStateFromProps` not `componentDidUpdate`)
- setState is asynchronous
  - second arg to setState is called as a callback after state is actually set
  - if you pass a function to `setState`, it can return a new state
- short circuiting pattern leads to `"0"` rendering (coerce conditions to booleans if you want to use `&&`)

```
{ myCondition && <ComponentToShow> }
```

Renders '0' if `myCondition` is 0, because

```
0 && Something
=> 0
```

### Performance
> *Warning: Premature Optimization!* You usually don't have to think about performance issues. Don't actually do this until you need it!

**Initial load (time to interactive) vs. Update performance**

Performance improvements usually fall into two buckets: 
- improving how fast the page initially loads (TTI or Time to Interactive)
- improving how fast updates feel (e.g. there's a lag when typing into an input)

Most React Performance guides have to do with the second. You're more likely to _actually_ want to improve the first. Improving initial load is hard, because it usually means reducing your _bundle size_. That usually means thinking about webpack and the packages you are using, not about React and on-page performance.


**Update performance tips:**
- Use the production build of React - it's different (and faster!) than the development build
- implementing `shouldComponentUpdate` is the heart of most react performance debugging
- extending PureComponent gives you a default implementation that will often lead to speedups
- indexes as array keys are slow -- unique, stable, predictable keys are fast
- Inline arrow functions get created on every render as a new object (slow) vs. methods on the class get declared once (`this.handleSomething`) 


Resources and Tools:
- See more at https://reactjs.org/docs/optimizing-performance.html
- [why did you update](https://github.com/maicki/why-did-you-update)
- [using the chrome dev tools](https://building.calibreapp.com/debugging-react-performance-with-react-16-and-chrome-devtools-c90698a522ad)
- [using the react dev tools profiler](https://reactjs.org/blog/2018/09/10/introducing-the-react-profiler.html)


### Advanced React Features

You don't need to use these in your apps, but you should read about them in the docs and know that they exist!

- Fragment: reduce your extra divs
- PropTypes: ensure that the right kinds of props are passed into your components (Typescript and Flow are more general solutions to this problem)
- Error Boundaries: when one component has an error, limit how much damage it will do to the rest of your app
- Portal: render a child somewhere else in the DOM
- Context: pass data to your descendants, skipping intermediate children
- Refs: get access to a DOM element or React component that you're rendering

### Advanced React Patterns
- Components that add behavior instead of adding DOM elements to the page
- Composition vs. Inheritance
  - HOCs (higher-order components): functions that take in components and return components
  - render props: props that are a) React components to render or b) functions to call, to render the result
  - callable function children: children are a function to be called instead of react components

### Tools

There are lots of awesome tools you can use that can make your React development process faster, safer, and easier.

- React Dev Tools
- Prettier
- Linter
- Snippets
- Syntax Highlighting
- React Storybook

### Learning and Improving
- React Docs
- awesome-react
- https://github.com/kylpo/react-playbook

---
title: React Props And State
layout: post
---

# <a id="props-and-state">Props and State</a>

## SWBATs

* Learn how to identify components on a page, visually
* Understand how `create-react-app` works and what it offers a developer
* Learn the difference between props and state, and why one would use one or the other
* Get more familiarity with component hierarchy and the flow of information

## Resources

* [Example Video](http://youtu.be/Sjla00Wrj20)
* [Starter Code](https://github.com/learn-co-curriculum/react-starter-103017)
  * `webpack` branch

## Outline

    10m Identify Components
    10m create-react-app
    10m Passing Props
     5m Optional aside: Solidfying props
    10m Intro to State
    20m Ramping Up on State
    ===
    65m Total

### Identify Components

When building React Apps I think it's super helpful to wireframe out what you are building and start identifying what is a component. I use [a web whiteboard](https://www.awwapp.com) to draw different colored squares around what will be a component in these pre-made images (made with free trial of balsamic that i took screenshots of). I'll show the first image and have students start identifying what they think is a component.

<img src="../assets/props_and_state.png" width="300" />
<img src="../assets/props_and_state_example.png" width="300" />

In this app we'll use the JSON data in resources/painting_data.js to mimic data we'd be getting from an API. For the moment I say to ignore the 'votes' part.

Talk about why you might need a PaintingList Component, single responsibility, it's job is to receive some data and render out individual Painting components (or PaintingItem or PaintingCard or whatever you want to call it).

### create-react-app

Show how `create-react-app` is the `rails new` of react.

* `npm install -g create-react-app` (if they haven't)
* `create-react-app my-app` cd into it.
* `npm install --save semantic-ui-css` talk about what the --save does (adds to package.json, why do we care, etc.)
* _Get rid of everything in c-r-a that we don't know what it is. Service workers, css, tests... delete it all_
* Build out static version of the app with right component structure. (bring in Navbar component from morning) Mention that often in React there's like a certain minimum amount of boilerplate needed to be written to get your app up and rendering. I would make components such as

```js
import React from 'react';

const PaintingList = () => {
  return <div>PaintingList</div>;
};

export default PaintingList;
```

so you can see things rendering correctly on page. Reminder that these are _just functions_. A bit different than class-based components seen in labs, but very very similar and all we have seen in lecture thus far. (Students will continue to have confusion over functional components though I show them every lecture, a deficiency in the curriculum?)

### Passing Props

In a top level component like App import the json data from painting_data and show that you can console.log it (in render) and have access to it. Ask the question of how you are going to get this data to the other components that need to know about it?

The answer, via props. _There is one way to pass data from one component to another in React, that is props. They go one direction, down from parent to child. In lecture 1, we passed props as arguments to a function. Even when using JSX that's really how you should think of props._ **Props are like arguments to a function. A component does not own it's own props they are passed to it from outside.** This is in contrast to state which we'll talk about next.

Pass the props from App to PaintingList and console.log them again. Now you are in a situation where you have an array of plain JS objects. What you want back is an array of the same number of elements, but each element should be a React component. What function does that sound like? `map`! We'll use `map` here for the same reason we would use map to take an array of numbers and double each number.

_**Quick Aside: The React Mod 4 2.1 curriculum teaches class-based components first, and then goes into functional components and their differences much later. It might be a good idea for you to teach only class-based components for now and get into some other structural patterns later, to be consistent with the labs. Use your best judgement. **_

```js
// ====================================
// Step 1
// PaintingList.js
// see the same number of things we should expect
import React from 'react'

const PaintingList = (props) => {
  const allPaintings =  props.paintings.map(painting => <li>hi</li>)

  return (
    <div>
      <ul>
        {allPaintings}
      </ul>
    </div>
  )
}

export default PaintingList

// ====================================
// Step 2
// PaintingList.js
// render Painting Components
import React from 'react'
import Painting from './Painting'

const PaintingList = (props) => {
  const allPaintings =  props.paintings.map(painting => <Painting />)

  return (
    <div>
      <ul>
        {allPaintings}
      </ul>
    </div>
  )
}

export default PaintingList

//Painting.js
import React from 'react'

const Painting = (props) => {
  return <li>Painting Component</li>
}

export default Painting

// ====================================
// Step 3
// show the titles
import React from 'react'
import Painting from './Painting'

const PaintingList = (props) => {
  const allPaintings =  props.paintings.map(painting => <Painting title={painting.title}/>)

  return (
    <div>
      <ul>
        {allPaintings}
      </ul>
    </div>
  )
}

export default PaintingList

//Painting.js
import React from 'react'

const Painting = (props) => {
  return <li>{props.title}</li>
}

export default Painting

// ====================================
// Step 4
// fill out Painting Component
// maybe discuss why it's nicer to pass a prop 'painting'
// vs. a title prop, image prop, artist name prop, dimension prop, etc.
import React from 'react'
import Painting from './Painting'

const PaintingList = (props) => {
  const allPaintings =  props.paintings.map(painting => <Painting painting={painting}/>)

  return (
    <div>
      <ul>
        {allPaintings}
      </ul>
    </div>
  )
}

export default PaintingList

//Painting.js
import React from 'react'

const Painting = (props) => {
  return (
    <li>
      <img src={painting.imageUrl} />
      <h1>{`${painting.title} by ${painting.artist.name}`}</h1>
      <p>{painting.date}</p>
      <p>{`${painting.dimensions.width} x ${painting.dimensions.height}`}</p>
    </li>
  )
}

export default Painting
```

Cover the whole flow again, how props get passed down multiple levels, get mapped over, etc. I do briefly talk about the `key` prop warning. Basically it's for React's internal workings so it can quickly know what components to update when it's doing that thing of updating the real DOM to look like the virtual DOM

If you want to make the Painting Component look fancy here's some markup: (_NOTE: this also adds the vote button I'll use later_)

```js
<div className="item">
  <div className="ui small image">
    <img src={props.painting.image} alt={props.painting.slug} />
  </div>
  <div className="middle aligned content">
    <div className="header">{`"${props.painting.title}" by ${
      props.painting.artist.name
    }`}</div>
    <div className="description">
      <a>
        <i className="large caret up icon" />
        {props.painting.votes} votes
      </a>
    </div>
  </div>
</div>
```

### Optional aside: Solidfying props

If you have time, it may be worth it to show them this bit of code to solidify their understanding of props and why we use components in the first place. I recommend having this code in a separate React app, so you can quickly spin it up.

```js
//App.js

import React, { Component } from 'react';
import {Donalds, PhilA, Dees} from './Restaurants'

class App extends Component {
  render() {
    return (
      <div className="App">
        <Donalds />
        <PhilA />
        <Dees />
      </div>
    );
  }
}
export default App;


//Restaurants.js
import React from 'react'
import Meat from './meat.js'

const Donalds = (props) => {
  return <Meat stuff="Xanthan Gum"/>
}

const PhilA = (props) => {
  return <Meat type="Chicken"/>
}

const Dees = (props) => {
  return <Meat type="Beef"/>
}

export {Donalds, PhilA, Dees}


//Meat.js
import React from 'react'

const Meat = (props) => {
  return <h1>{props.type}</h1>
}

export default Meat
```

Take the students on a quick tour of the code, showing the relationship between the components and showing how we have three different components (Donalds, PhilA, and Dees) rendering the same component (Meat). Explain that the reason we use components is their reusability. Spin up this code on your server, but before showing them the results, put the Restaurants and Meat code side by side and ask them what they anticipate will appear on the page. Students may think that "Xanthan Gum", "Chicken", and "Beef" will appear as h1's, but because the name of the prop bassed by Donalds is `stuff` rather than `type`, only "Chicken" and "Beef" will be rendered. To drive this home, log the props inside Meat to show them how they're different. Explain that components don't care who their parent is, so long as their parent passes props using names that they can understand. You can even modify the code to pass different data types under the "type" prop to show another layer of flexibility.

Maybe take a break, move on to state

### Intro to State

To introduce state I add a button to the Navbar that says 'Change Color', here's the component and an array of valid semantic colors

```js
import React from 'react';

const colors = [
  'red',
  'orange',
  'yellow',
  'olive',
  'green',
  'teal',
  'blue',
  'violet',
  'purple',
  'pink',
  'brown',
  'grey',
  'black'
];

const Navbar = props => {
  return (
    <div className={`ui inverted ${props.color} menu`}>
      <a className="item">
        <h2 className="ui header">
          <i className={`${props.icon} icon`} />
          <div className="content">{props.title}</div>
          <div className="sub header">{props.description}</div>
        </h2>
      </a>
      <div className="right menu">
        <div className="item">
          <div className="ui button">Change Color</div>
        </div>
      </div>
    </div>
  );
};

export default Navbar;
```

The idea is clicking the button should randomly change the color of the Navbar. Reinforce that `onClick` takes a callback, console.log something onClick. I try to change the color using props in various ways and see it break and/or do nothing.

```js
<div
  onClick={() => {
    props.color = 'blue';
  }}
  className="ui button"
>
  Change Color
</div>
```

So this isn't what props are for. Props, like we said, are arguments to a function. We need something like an instance variable, just like how a Dog instance holds onto it's own `@name`, we need this Component to hold onto it's own color. This is state. **It's like an instance variable that a component manages itself and can change over time**

For a component to have state it needs to be a class-based component, refactor.

```js
class Navbar extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      color: 'green'
    };
  }

  render() {
    return (
      <div className={`ui inverted ${this.state.color} menu`}>
        <a className="item">
          <h2 className="ui header">
            <i className={`${this.props.icon} icon`} />
            <div className="content">{this.props.title}</div>
            <div className="sub header">{this.props.description}</div>
          </h2>
        </a>
        <div className="right menu">
          <div className="item">
            <div
              onClick={() => {
                this.state.color = 'blue';
              }}
              className="ui button"
            >
              Change Color
            </div>
          </div>
        </div>
      </div>
    );
  }
}
```

Nothing will happen. Conceptually, remember React is _declarative_, we just _describe what we want the DOM to look like and React will take over updating it._ We need to tell React, 'hey we are changing the state and you should re-render' (put console.logs in render and see them get called twice on changing state). To do this we have to do use the `this.setState` api.

```js
render() {
  console.log('Navbar renders');
  return (
    <div className={`ui inverted ${this.state.color} menu`}>
      {/* ... more code ... */}
        <div className="item">
          <div
            onClick={() => {
              this.setState({color: 'blue'})
            }}
            className="ui button"
            >
            Change Color
          </div>
        </div>
    </div>
  );
}
```

Cool, pull this out into a function

```js
class Navbar extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      color: 'green'
    };
  }

  handleClick() {
    this.setState({ color: 'blue' });
  }

  render() {
    return (
      <div className={`ui inverted ${this.state.color} menu`}>
        <a className="item">
          <h2 className="ui header">
            <i className={`${this.props.icon} icon`} />
            <div className="content">{this.props.title}</div>
            <div className="sub header">{this.props.description}</div>
          </h2>
        </a>
        <div className="right menu">
          <div className="item">
            <div onClick={this.handleClick} className="ui button">
              Change Color
            </div>
          </div>
        </div>
      </div>
    );
  }
}
```

Huh? It will error. When you pass the function as a callback you _lose the context_. You have to bind `this`. I show them that there are many ways to do this. `.bind`, wrap an arrow function around it, and I encourage binding in the constructor as the easiest, 'set it and forget it' way. Show that `this` is the instance of the component.

```js
constructor(props) {
  super(props);
  this.state = {
    color: 'green'
  };

  this.handleClick = this.handleClick.bind(this)
}
```

If anyone gives pushback on not understanding this remind them of code like this

```js
var x = 10;
x = x + 1;
// the new value of x is equal to the old
// value of x changed in some way
```

Finish:

```js
handleClick() {
  console.log(this);
  const newColor = colors[Math.floor(Math.random() * colors.length)];
  this.setState({ color: newColor });
}
```

### Ramping Up on State

Now that we know the basics of state, I ramp up significantly. State, events, forms need a lot of time and tomorrow we'll cover everything in depth. Right now I throw a bunch at them.

Ok so looking back at the original pictures, paintings have a number of votes.

We expect two things, 1) We can upvote paintings and increase the number of votes and 2) they should always be ordered by num votes (this I'll leave them to do post lecture).

If the order of the Paintings array will change based on user interaction.... that seems like state. I make the necessary changes, import dummy data directly into PaintingsList, change to a class based component, set the initial state, change props.paintings to this.state.paintings, etc. Reinforce that it's normal that what to PaintingList is it's state, an individual Painting component only knows about as props. The pattern will be very common. One component higher up has state, it passes it down to children components as props.

##### Show the Problem

(This section could use more explanation)

Think about an upvote, we know that we have to say something like `this.setState` where _`this` is the PaintingList-- that's what holds the state_... yet the component that knows about the click event is the Painting, a child. How do we pass data to components? As props! functions are data, pass down the props as a callback and don't forget to bind.

I stress this aspect a ton and cover the flow over and over. Take a bunch of intermediate steps, add console logs, how are you going to pass data to the callback? Go slow and repeat yourself.

The only things left to show are the alternate `setState` syntax (pass a callback invoked with previous state, this is the preferred way if you are updating state based on previous state)

I finish by getting the upvotes to work and leave them with the task of keeping paintings sorted by votes. Remind that JS native sort is destructive and you have to be sure not to destructively modify state.

---
title: React State And Forms
layout: post
---

# <a id="state-and-forms">State, Events, and Forms</a>

_This lecture and the next one have the same notes, but it's a reflection of the necessity to repeat information for students to really internalize the given topics. We can cover it all in one lecture, but it helps to reiterate the same concepts with a second example._

## SWBATS

* Explain the difference between imperative and declarative programming
* Differentiate between presentational(dumb) and container(smart) components
* Instantiate state in and out of the constructor
* Trigger rerenders by calling `setState`
* Manipulate the DOM by changing values in state
* Create event handler callbacks that manipulate state
* Write fully controlled forms

## Resources

> TODO: Choose video

* [091817 State, Events, Forms](http://youtu.be/d1EUrKXg_Wg) | [Code](https://github.com/learn-co-curriculum/091817-state-examples)
* [100917 State, Events, Forms](http://youtu.be/dnJrDmeKTwI)||[Code](https://github.com/learn-co-curriculum/100917-react-state-and-forms)
* [103017 State, Events, Forms](http://youtu.be/qIXCRdfSXfI) | [Code](https://github.com/learn-co-students/web-103017/tree/master/26_state_and_events/state-and-events-practice)

## Outline

```
		 5m | Imperative vs. Declarative Programming
		 5m | Introduction to State
		10m | Using State
		15m | Conditional Rendering
		 5m | Presentational vs Container Components
		 5m | BREAK
		15m | React Synthetic Events and Event Handlers
		15m | Controlled Forms

```

### Imperative vs. Declarative Programming

* Imperative Programming
	* Explicitly tell your program every step it needs to execute
	* In Vanilla JS, this looks like the following when an event listener triggers
		1. Find or create the relevant DOM elements
		2. Programatically read and/or update attributes of DOM elements
		3. Append/remove DOM elements
* Declarative programming
	* Program acts as a sort of template that automatically updates itself in response to changes in certain internal values

	```jsx
	//Change the color prop and show them that you are 'declaring' the color for this div

	class MyComp extends React.Component {
		render(){
			let color = 'red'
			return <div style={{color}}>The colors Duke, the colors!</div>
		}
	}
	```
	* JSX is your template that automatically responds to changes to its internal values. But what values is it responding to?

### Introduction to State

* State is a special attribute of an instance of a component and is typically accessed inside of a component by running `this.state`. Other attributes can be created for a component (e.g. `this.beef = "steak"`), but the name `state` is special
* State is just an object containing key-value pairs
* Component must be a _class_ component in order to make use of state
* It is a reflection of the current state of a component (e.g. is this card currently flipped? should I render component X or component Y? what data am I currently carrying?)
* Can be initialized in and out of the `constructor`

```jsx
class MyComp extends React.Component {
	constructor(){
		super()
		this.state = {
			color: "red"
		}
	}

	// Or simply in the body of the class...
	state = {
		color: "red"
	}

	render(){
		return <div style={{color: this.state.color}}>The colors Duke, the colors!</div>
	}
}
```


### Using State

* State represents the paradigm shift of moving from imperative to declartive programming - whenever a problem requires some sort of DOM manipulation, the thought process should shift from obtaining/creating DOM elements to manipulating state and making your template (the JSX in `render`) depend on the values of state
* `setState`
	* Changing the state object by ordinary assignment does nothing - mutating state directly will change the object's values, but the problem is that the `render` function of our component is not called, so the DOM will not respond to these changes
	* We use `setState` because in addition to changing the object, `setState` will call the `render` function, this time using the newly updated state values 
	* Gotchas
		* Changing state is asynchronous. `console.log` the state value that was supposed to be set below `setState`
		* `setState` takes 2 arguments:
			1. Either an object or a callback that accepts a parameter of the previous state and returns an object
			2. A callback that can be called whenever `setState` is finished updating state and rerendering
		* `setState` does a shallow comparison, meaning that even without spreading or copying state, only the properties that are specified in the object received by `setState` are changed while the others remain intact. However, this is only true for that first layer of properties: nested objects will have their values overwritten
* A simple example would be to write a ternary in `render` that depends on a boolean and switches between two texts "off" and "on"

```jsx
class MyComp extends React.Component {
	state = {
		on: true
	}

	handleClick = (event) => {
		this.setState({
			on: !this.state.on
		})
	}

	render(){
		return <p onClick={this.handleClick}>{this.state.on ? "on" : "off"}</p>
	}
}
```

* If you want to wait before showing them an event handling, you can just write a `setTimeout` inside `render` that updates state
* Ask them to come up with something simple of their own and build through it with the class

### Conditional Rendering

* If we write our JSX such that its values depend on state, we can use state as a proxy for the DOM, allowing _changes to state_ to progrmatically manipulate the DOM
* Examples of things to build through:
	1. A toggle that depends on a boolean
	2. Some text on the page that depends on a string in state
	3. Very important to show: a list of items that depends on an array of objects
* Useful to show how one would pass state values as props to children and how changes to state in a parent can also affect the children whose props are determined by state

### Presentational vs Container Components

* There are 2 distinctions for components that are mostly overlapping, but slightly different
* Class vs Functional Components
	* This difference is focused more on syntax and is pretty self-explanatory: class components use class syntax and functional components are just functions that return JSX
* Container(Smart) vs Presentational(Dumb) Components
	* Containers contain most of the programming logic and/or are used to manage state. As they often need state and component lifecycle methods, containers are usually class components, though it is entirely possible to write a container component as a functional component, as in cases where the container needs a lot of logic, but makes no use of state
	* Presentational components contain little-to-no logic and are typically almost entirely dependent on their parent components for the data they use to display
	* Because of the way information trickles down from parent to child in a component hierarchy via props, fewer, more centralized sources of data and functionality are much more manageable at scale

### React Synthetic Events and Event Handlers

* React Synthetic Events
	* [List](https://reactjs.org/docs/events.html)
	* It is useful to enter a `debugger` and examine the `event` object and note for them that even though React generates special synthetic events, these are more or less the same as your typical event objects
	* Students often will try to put event handlers on their own components, so it is important that you tell them that event handlers can only be attached to built-in JSX components (e.g. div, p)
* Students should be able to draw on their knowledge of how to use events in JS
	* Come up with a feature (e.g. toggle, Konami code) and ask the class how they would have handled that in Vanilla JS 
	* They should mention that when the event handler is triggered, a DOM element must be found/created before updating/appending it to the DOM
	* Event triggering is the same, the difference is that rather than manually finding and editing DOM nodes, we will eventually call `setState` and let changes to state generate the desired DOM changes
* Event handler callbacks should be written as arrow functions to avoid losing context

### Controlled Forms

* Form submission in Vanilla JS involves obtaining user input by manually grabbing the desired input elements and obtaining their the values of their `value` attributes
	* We still want access to user input in React, but if we do not access the DOM directly, how can make user input accessible to us?
* Controlled inputs
	* The following code is a good starting point to show a piece of state monitoring the values of a form
	
	```jsx
	class NewThang extends React.Component {
		state = {
			author: ""
			thang: ""
		}
		handleSubmit = (event) => {
			event.preventDefault()
			console.log(this.state)
		}
		handleAuthor = (event) => {
			this.setState({
				author: event.target.value
			})
		}
		handleThang = (event) => {
			this.setState({
				thang: event.target.value
			})
		}
		render(){
			return (
				<form onSubmit={handleSubmit}>
					<input placeholder="Who are you?" onChange={handleAuthor}/>
					<input placeholder="What's your thang?" onChange={handleThang}/>
					<input type="submit"/>
				</form>
			)
		}
	}
	```

	* After the above code, one can iterate and improve the process by:
		1. Abstracting the `onChange` handlers to a single function using the event object and `name` values on the inputs
		2. Make the inputs fully controlled by assigning the `value` to its respective value in state
		3. Clearing state `onSubmit` to clear the input fields, which illustrates the importance of making the input fully controlled (to drive this home, try removing the `value` attributes on your inputs and show how the inputs do not respond to state changes)
	* Form submission should eventually take the values from state and use them to create a new object in a parent's state. Points to drive home:
		1. How to pass a function from parent to child to update the parent's state
		2. How holding data (e.g. array of comment objects) in state allows us to add DOM elements by simply adding to the data
		3. If the form and the components displaying the data are siblings, the only way for the data from the form to reach those components is to change state in a common ancestor
---

---
title: React Component Lifecycle
layout: post
---

# <a id="lifecycle">Component Lifecycle Methods</a>

## SWBAT
* Write methods that interact with data at different points throughout a component's life
* Identify why we fetch data using ComponentDidMount
* Recognize the most-used lifecyle methods

## Resources
* [React Docs](https://reactjs.org/docs/react-component.html#the-component-lifecycle)
* [React Lifecycle Methods Diagram](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/react/react-lifecycle-starter-code)
* [Solution Code]()

## Outline
```
   10m Show Parent & Child Lifecycles
   15m ComponentDidMount for Fetch Requests
   15m Passing Functions to Update State
   20m ComponentWillUnmount
   20m ComponentDidUpdate
   ===
   80m Total
```

### Show Parent & Child Lifecycles
Start with a simple parent, child and grandchild app. Show students the order that the parent, child and grandchild hit their lifecycle methods. It goes from the top down for constructor and then the bottom up for mounting and updating. You can use the below dynamic code in each class to log the methods and class names.

```
constructor() {
  super()
  console.log(this.__proto__.constructor.name, "constructor")
}

componentDidMount() {
  console.log(this.__proto__.constructor.name, "mounting")
}

componentDidUpdate() {
    console.log(this.__proto__.constructor.name, "did update")
}
```

### ComponentDidMount
This is the lifecycle method most students will use in their projects (and code challenges). If you run `json-server db.json` you will get an API of koala photos running on localhost:3000. Demonstrate a fetch request to `http://localhost:3000/koalas` from App and select a koala at random to pass as a koala prop to the RandomKoala component. Use that prop to render a koala image in the component.

*Remember to discuss the importance of setting up a default state so the application can render without waiting for the data to be fetched.*

### Passing Functions
Comment out the RandomKoala from App. Our next demo is to create a widget that switches between showing a clock and a stock ticker on click. WidgetSelector should be a child of app which has siblings of DigitalClock and StockTicker. (Changing the structure will cause the CSS to not work properly.) Our app should have a state which determines which widget (clock or stock) is currently showing. App should pass down to WidgetSelector a function which can change the App state. WidgetSelector will call this on button click. If you want to console your lifecycle methods again, you can demonstrate that the component unmounts when the switch happens.

*Remind students that in order for a child to update parent state, it needs a function to be passed down as props.*

### ComponentWillUnmount
Start building the DigitalClock which we will use to demonstrate componentWillUnmount. This component will hold a time state which we will initialize in the constructor. Then we will setInterval to update this state once a second in componentDidMount.

Since we have the switch widget feature built out, if we switch to our StockTicker we should get the following error:

> Warning: Can't call setState (or forceUpdate) on an unmounted component. This is a no-op, but it indicates a memory leak in your application. To fix, cancel all subscriptions and asynchronous tasks in the componentWillUnmount method.

The students should be able to tell you that you have an interval set which never gets unset. Using componentWillUnmount, cancel the interval. Talk about how if you had websockets open every time you returned to this component (which never closed), you would end up with multiple sockets open for the same channel and might be getting double (or triple) the response data.

### ComponentDidUpdate
Start building the StockTicker to demonstrate componentDidUpdate. Create a function which will randomly generate a two-digit stock price. Like our clock, setInterval so the stock price changes every second. Tell the students you want the price to show green if it has gone up or red if it has gone down. This means you will need access to the prevState and current state in order to compare the prices. Using componentDidUpdate we can compare both states. Based on the difference, we can update a second state which says what color our ticker should be.

Demonstrate to students how we can get in an infinite loop of updating state. Every time we change the state, we will hit componentDidUpdate. It will check the previous price against the current price and set a state for the color which will cause us to hit componentDidUpdate again. We keep evaluating the prices, setting the colors and having to reevaluate the prices.

Show the students we need to give our componentDidUpdate the equivalent of a recursive base case. If the previous and current prices are the same, we should not update the state. In the case where the prices are the same, that means we are in the componentDidUpdate because the color was just updated in state. That means we have no more work to do and should just return out of the method so the component can render with the right color.

### Extra Credit: Analog Clock
If you have extra time or an ambitious class, you can push the lecture code and have students refactor the App so the widget toggles between the Analog and Digital clocks. Tell students they will have to move the time state and pass it as props to both clocks.

## More Reading on Lifecycle Methods
### Most Commonly Used Methods
- *constructor(props)*
- *render()*
- *componentDidMount()*
- *componentDidUpdate(prevProps, prevState, snapshot)*
- *componentWillUnmount()*

### Birth (Mounting)
- *constructor(props)*
  - called before it is mounted
  - set initial state here
- static getDerivedStateFromProps(props, state)
  - invoked right before calling the render method, both on the initial mount and on subsequent updates. It should return an object to update the state, or null to update nothing.
- *render()*
  - called after mounting and updating
- *componentDidMount()*
  - invoked immediately after a component is mounted (inserted into the tree).
  - this is where you should request data from remote endpoints

### Life (Updating)
- static getDerivedStateFromProps(props, state)
  - invoked right before calling the render method, both on the initial mount and on subsequent updates. It should return an object to update the state, or null to update nothing.
- shouldComponentUpdate(nextProps, nextState)
  - invoked before rendering when new props or state are being received
  - returns boolean which determines if render should be called
- *render()*
  - called after mounting and updating
- getSnapshotBeforeUpdate(prevProps, prevState)
  - invoked right before the most recently rendered output is committed to e.g. the DOM. It enables your component to capture some information from the DOM (e.g. scroll position) before it is potentially changed. Any value returned by this lifecycle will be passed as a parameter to componentDidUpdate()
- *componentDidUpdate(prevProps, prevState)*
  - invoked immediately after updating occurs. This method is not called for the initial render
  - watch out for infinite loops if setting state!

### Death (Unmounting)
- *componentWillUnmount()*
  -  invoked immediately before a component is unmounted and destroyed. Perform any necessary cleanup in this method, such as invalidating timers, canceling network requests, or cleaning up any subscriptions that were created in componentDidMount().

---
title: React Webpack
layout: post
---

---
title: React Router
layout: post
---

# <a id="router">React Router</a>

We want students to be caught up to Lifecycle Methods by the time they're here. I recommend starting with an application that already has some components, so there's something to work with, and you don't need to spend time building out the structure

## SWBATs

* Understand why routing is important and how it is different in React Router
* Set up React Router in a React App
* Go over `BrowserRouter`, `Link`, `Route`, and `Switch`.

## Resources

* [Example Video](https://www.youtube.com/watch?v=lps-Eq2QWxk)
* [Starter Code]()

* [React Router Quickstart](https://reacttraining.com/react-router/web/guides/quick-start)
* [Learn's Intro to Client-Side Routing](https://github.com/learn-co-curriculum/react-introduction-to-react-router)
* [A Simple React Router v4 Tutorial](https://medium.com/@pshrmn/a-simple-react-router-v4-tutorial-7f23ff27adf)

## Outline

    10m Theoretical Prerequisites
     5m But what does React Router Actually Do?
     5m Setup and Components
    40m Using the Router Components
    ===
    60m Total

### Theoretical Prerequisites

##### Static vs. Dynamic Routing

Static routing is what we're used to with Rails. Basically, we define the routes beforehand, and then render their actions separately.

React Router is Different. Basically, the app "renders" routes _while_ rendering all of the JSX. This means no external `routes.*` configuration.

##### Client-side routing

Now that the React stack is handling routing, that means none of our routes require a new `GET` request to the backend to get that page's HTML. This allows us to enforce the "Single Page App", since we can render the new route's page without refreshing.

##### Why do we even need routes?

* The user can use forward/back to navigate your app
* The user can navigate via urls
* We can make urls describe the action that the user might be taking

##### What are the drawbacks to client-side routing?

* We're loading all of our frontend at once, so it might add to the initial load time
* We have to design all of our routes to be coupled with our component structure (which can be a good thing long-term)

### But what does React Router Actually Do?

Ultimately, we're still in a Single-Page application. Show that you can use vanilla JS to change the route in the terminal using the following commands.

```js
window.history.pushState({}, null, 'page');
```

```js
window.history.back();
```

All router does is wrap this functionality in components that make it easy to transform the browser's URL.

### Setup and Components

You can use `create-react-app` in conjunction with `react-router`, just install with `npm install react-router-dom`.

Now, we can add the requisite components with

```js
import { BrowserRouter as Router, Route, Link, Switch } from 'react-router-dom';
```

Here are the components we use:

#### Router

We'll use this in one place in our application (and one place only). Very top level, essentially listening for when the route changes, and making that info accessible.

#### Route

Conditionally render a certain component based on what the route looks like.

#### Link

Changes the url we see in the browser, must have a 'to' prop.

#### Switch

Pick one of the following routes (the first that matches), don't look at the others (like an if/ else if/ else if).

#### Redirect

Forces a redirect to a particular route. We won't use this here.

### Using the Router Components

Go through the process of building a app with routing. Start by wrapping your top-level app in the router in `index.js`:

```jsx
<BrowserRouter>
  <App />
</BrowserRouter>
```

Now you can make your app render different components using `<Render />` At this stage, it helps to have a separation of information and navigation, so the links can live on their own.

##### Basic Routing

In your `App.js`, add something that looks like this:

```jsx
<Switch>
  <Route path="/login" component={Login} />
  <Route path="/paintings" component={PaintingsContainer} />
  <Route path="/" component={About} />
</Switch>
```

Explain that `Switch` allows router to choose the route that matches the url when loading that particular component. Show that the `component` props takes a function, and passes in extra information through props. If you want to initialize a component using your own props but don't want to los React Router's props, pass a function into `render` instead.

You can set up a default `Route` by setting `path="/"`, and add a `<Route exact path="/" />` to catch the base path.

##### Nested Routes

You can have `Switch` anywhere, including inside a component. Here, you can catch specific paintings with a slug via:

```jsx
<Route
  path="/paintings/:slug"
  render={({ match }) => {
    return <PaintingItem painting={getPainting(match.params.slug)} />;
  }}
/>
```

##### Links

Now, you can update your navbar with links that go towards specific paths.

```jsx
<Link to="/paintings" className="item">
  Paintings
</Link>
```

_Try asking your students what the child of the `Link` component is, and where that comes through in the props._

Try navigating around your app, and adding new routes!
