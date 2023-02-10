# React State

## Objectives
1. Understand what state is and why it matters
1. Initialize and change state with the useState hook.
1. Understand where to define state - container and presentation components; unidirectional data flow

## Pre Reqs
1. Basic React (components, props, JSX & event handlers)
1. Basic JavaScript (arrays, objects, iteration, conditionals, functions)


### What is State?

State in React Applications can be thought of like a backpack a college student carries around. Just like a student may put different items in their backpack throughout the day, a React component can hold different values in its state. And just like how a student may need to access their backpack to get their notebook or pen, a component can access its state to display or update information on the page. But simmarly how a student can only access the contents of their own backpack, a component can only access and update its own state, not the state of other components.

In React, you use the state to store data that will change over time, and then you render components based on that data. When the state changes, React will automatically update the components to reflect the new state, making it easier for you to manage the data in your app.

This `reactivity` is exciting because it means we can create applications that can receive fresh data after the its already running in the browser and change its display or behavior as a result.

Think about Google Maps... You have all used Google Maps

If you type in a certain address the application receives the address you gave it and stores it in the applications state, it then uses that address to make queries etc about that address and then displays to you how long it would take you to get from where you currently are to the address you entered. You can also keep changing that state to different addresses and the application will update accordingly.

It's like magic.

![](https://i.imgur.com/CpgQYsj.png)

Any other apps like this that come to mind?

Let's see something more simple in action.

### The useState Hook

The useState hook allows us to generate special state variables, as updating them would trigger your component and its children to update.

First step is always importing the useState hook.

```js
import { useState } from "react"
```

Inside the body of your component function you can then initiate a state variable. The name convention is to use the a descriptive name to describe the state for the variable and "set" + that variable name for the function that updates the states value.

If I wanted to create state for a counter it would look like this.

```js
// initiate counter at 0, setCounter let's me update counter
const [counter, setCounter] = useState(0)
```

So a simple counter component would look like this...

```jsx
import { useState } from "react"

export default function Counter(props) {
  // Declare the state
  const [counter, setCounter] = useState(0)

  // Function to add one to the state
  const addOne = () => {
    // sets counter to its current value + 1
    setCounter(counter + 1)
  }

  // The h1 display the counter and button runs addOne function
  return (
    <div>
      <h1>{counter}</h1>
      <button onClick={addOne}>Click Me to Add One</button>
    </div>
  )
}
```
![img](https://i.imgur.com/ocJl48O.png)

That's as simple as it gets. What happens when the button is clicked.

![img](https://i.imgur.com/ffqwO3f.png)

- setCounter is passed the current value + 1
- React then compares this new value to the old value of counter
- If they are the same, React does nothing (beware of references as values when it comes to objects and arrays, make sure you understand pass by value vs pass by reference)

![img](https://i.imgur.com/I0sM27A.png)

- If they are different then React updates something called the VirtualDOM (more on this in a second) based on a re-render of the component and its children
- It then compares the VirtualDOM to the real browser DOM(that you are used to) and only updates the places in which they differ(which is more efficient than replacing the entire dome)

The above process is why variables that are "State" are reactive, meaning the DOM will updates when the value updates. All other variables are not reactive and will not trigger updates when changed.

**NOTE**: If the state is an object or array, make sure you pass a new array or object and not just modify the old one. Objects and Arrays are reference types, so if you pass the old array with modified values the references will still be equal so there will be no update to the DOM.

Example...

Don't do this

```js
// modify the existing state
state[0] = 6
// then setState as the existing state, triggering NO update
setState(state)
```

also don't do this
```js
// these two variables are both pointing to the same position in memory
const updatedState = state
// no update is triggered
setState(updatedState)
```

Do this

```js
// create a unique copy of the array
const updatedState = [...state]
// modify the new array
updatedState[0] = 6
// set the State to the updatedArray, DOM will update
setState(updatedState)
```

### The Virtual DOM

The Virtual DOM is a lightweight JavaScript representation of the actual DOM, or Document Object Model, which is the tree structure of HTML elements in a web page. The Virtual DOM allows React to make changes to the DOM without having to reload the page or redraw the page.

The Virtual DOM works by creating a lightweight representation of the current DOM and comparing it to the desired state of the DOM. When a change is made, React runs a diffing algorithm which looks for differences between the virtual DOM and the actual DOM. The diffing algorithm then determines which parts of the DOM need to be changed and updates only those parts, instead of having to redraw the entire page. This makes changes to the DOM faster and more efficient.

If you have ever looked at a DOM Node on a website and looked at the shear number of properties attached to a DOM Node and pieces of data you normally don't use, you could imagine how large the DOM is.

As a matter of fact lets look at a Website

Lets select any element using `document.querySelector`

![img](https://i.imgur.com/jywNtj8.png[/img)

Now lets view all of it's properties in the console.


As you can see DOM elements are gigantic, and virtualDOM nodes only have a small ammount of data that is relevent to rendering the element, this makes updating it way less `expensive`.

This is why we love React.

### More would follow but to fall in line with time constraints I think this outlines what's needed

● Provide the connecting context and use case when describing new concepts
(why should students care?)
- I believe I provided the use case by describing Google Maps, and I would demo this website live in class with the students, as well as use the whiteboard if I am in person or draw on the screen if I am in Zoom.
● Provide intentional opportunities for students to engage with the lesson, ask
questions, and demonstrate their current understanding.
- I believe I allowed this when I say 'you have all heard of google maps' I would also expect students to respond to the prompt? What other things like this come to mind, and if they don't give me an example, I will bring up Netflix, or Door Dash. I also might consider showing a fully created React APP on my device and showing the actual data flow, one of the easiest ways to do this is an Ecommerce or Todo App.
● Be aware of the space you’re taking up in the room. Ideally, lessons include
significant contributions from both the instructors and the students.
- Agreed
● Avoid technical jargon when explaining new concepts unless explicitly defined.
- I believe State and The Virtual DOM are explained well for beginners and we can continue to build on it as we go through the lesson.
● Avoid going too deep into superfluous technical details.
- I believe I only explained what was necessary. Superfluous things to me would include, talking about Dispatch Methods etc and all of the other things that go into making a hook work
● Do use analogies, visuals, or reference points to help students connect to new
topics.
- Agreed
● Strike the right balance in debugging between guiding them and helping
them discover the issue.
- Agreed
● Help students to learn the areas to check first when different issues come up
- Agreed