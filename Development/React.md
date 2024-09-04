

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Whisper&display=swap" rel="stylesheet">


<div style="font-family: 'Whisper', cursive;">

---
<img src="./Illustrations/React.gif"   />

---
[React Handbook](https://reacthandbook.dev/)
[Docs](https://react.dev/) 
<details>
<summary>
## Contents

</summary>
 
* [Setup](#sparkles-setup)
* [Components](#sparkles-components)
* [Props](#star-props)
* [Splitting Components](#sparkles-splitting-components)
* [Making reusable wrapper components in react](#sparkles-making-reusable-wrapper-components-in-react)
* [Events in react](#sparkles-events-in-react)
* [State](#star2-state)
  * [useState hook](#useState-hook)
  * [prev](#prev)
  * [Using state with event listeners](#using-state-with-event-listeners)
  * [Working with multiple states](#working-with-multiple-states)
* [Working with forms and two way binding](#sparkles-working-with-forms-and-two-way-binding)
* [Passing data from child to parent and lifting the state](#star-passing-data-from-child-to-parent-and-lifting-the-state)
* [Lists in React](#sparkles-lists-in-react)
  * [Stateful Lists](#stateful-lists)
* [Rendering conditional content in React](#sparkles-rendering-conditional-content-in-react)
* [Fragments, Portals and Refs](#star-fragments-portals-and-refs)
  * [Fragments](#fragments)
  * [Portals](#portals)
  * [Refs](#refs)
* [Side Effects and useEffect()](#star2-side-effects-and-useEffect)
* [useReducer()](#star2-useReducer)
* [Context](#star2-context)
* [Using Context Provider to handle state](#using-the-Context-Provider-to-handle-state)
* [frowardRef](#sparkles-forwardRef)
* [Optimizing React app](#star2-optimizing-react-app)
  * [React.memo()](#reactmemo)
  * [useCallback()](#useCallback)
  * [useMemo()](#useMemo)
  * [making request using useEffect and useCallback](#making-requests-using-useEffect-and-useCallback)
* [Making Custom Hooks](#star2-making-custom-hooks)
* [Redux](#star2-redux)
  * [using Redux](#using-redux)
  * [using redux with redux toolkit](#using-redux-with-redux-toolkit)
  * [Using multiple slices in redux](#using-multiple-slices-in-redux)
  * [Thumb rule for pure vs async code](#thumb-rule-for-pure-vs-async-code)
  * [Handling async state logic with custom action creators](#handling-async-state-logic-with-custom-action-creators)
* [Routing](#star-routing)
  * [Adding Routes and Links](#adding-routes-and-links)
  * [Adding a root route to outlet different subroutes](#adding-a-root-to-outlet-different-subroutes)
  * [Error page, Navlink and navigating programmatically](#error-page-navlink-and-navigating-programmatically)
  * [Dynamic Routes](#dynamic-routes)
  * [Relative vs Absolute Path](#relative-vs-absolute-path)
  * [Relative attribute in Link tag](#relative-attribute-in-link-tag)
  * [Index Routes](#index-routes)
  * [Using Loaders](#using-loaders)
  * [Customising Error thrown while Routing](#customising-error-thrown-while-routing)
  * [Throwing json](#throw-json)
  * [Using dynamic route params in loaders](#using-dynamic-route-params-in-loaders)
  * [useRouteLoaderData() hook](#useRouteLoaderData-hook)

</details>

### :sparkles: Setup

* **Install node.js**. Also **npm install create-react-app**.
* To create a **new react project** just **make a working directory** and **run npx create-react-app <Project Name>**.
* Open the folder in vscode and get started.
* Often to share our work, or to reduce disk occupied disk space we delete the node modules folder of the project.
* We can regain this folder using **npm install** in the project directory, given the package.json is present.
* We run the project using **npm start** which opens up the project in the browser.
* React code is written in **JSX**. This is a html in js mix syntax. In React using jsx we can also import assets like image,css files into the jsx file. 
* React embraces **declarative** way of writing code, where we just define the starting and final states and React takes care of heavy lifting behind the scenes.
* React creates a **virtual dom** that finalises the changes before doing them in DOM of browser to make the process fast.


### :sparkles: Components

[Docs](https://react.dev/learn/describing-the-ui)

* React app is divided into **Components**. 
* Component is a single js function that returns jsx code. Detailed usage of jsx in react can be found [here](https://react.dev/learn/writing-markup-with-jsx) and [here](https://react.dev/learn/javascript-in-jsx-with-curly-braces).
* We make our app by chaining and nesting Components together. 

This is an example CustomComponent that is defined in CustomComponent.js and is then imported and used in App.js. Each component js file can also add its **own styling by adding a css file of same name(eg.CustomComponent.css)**. Styles from parents are also applied. Also, css classes are applied using **className inside the component tag**.

CustomComponent.js:
```jsx
import React from "react";
import './CustomComponent.css';

const CustomComponent=()=>{
    return <div>This is an example of custom component.</div>
}

export default CustomComponent;
 ```
App.js:
```jsx
import logo from './logo.svg';
import './App.css';
import CustomComponent from './CustomComponent';

function App() {
  return (
    <div className="App">
      <CustomComponent/>
    </div>
  );
}

export default App;
```
* It should be noted that it is best practice to render data dynamically using jsx syntax instead of hard coding the values.

Example:
```jsx
import React from "react";

const CustomComponent=()=>{
    let x=10;
    let name='Shubhanjan';
    let message='This is an example of passing components through variables.'
    return <div>{x}. {name}: {message}</div>
}

export default CustomComponent;
```
* While working with components, it is always recommended to keep each component small and managable.
* When component size begins to increase, it is advisable to consider splitting it.
* Its best practice to keep the returned jsx from the Components lean and compute any logic in the component before rendering it in the Component.

### :star: Props 

[Docs](https://react.dev/learn/passing-props-to-a-component)

#### Using props

* Props are a way to re-use Components, by passing data that we want to it.
* When **we add a custom component tag to another component**, **we pass values using keys and values inside the tag** itself and this collection of **keys and values is recieved automatically by the component using an argument, which we usually name props**.

Data fed into CustomComponent using props:

```jsx
import logo from './logo.svg';
import './App.css';
import CustomComponent from './CustomComponent';

function App() {
  let x=10;
  let name='Shubhanjan';
  let message='Example of working of props.';
  return (
    <div className="App">
      <CustomComponent x={x} name={name} message={message}/>
    </div>
  );
}

export default App;
```

CustomComponent.js recieves data via props:

```jsx
import React from "react";

const CustomComponent=({x,name,message})=>{
    return <div>{x}. {name}: {message}</div>
}

export default CustomComponent;
```

* We can also use destructuring to pass the attributes as props.

For example here we use the data from an object array and pass the properties of the object as props using destructuring in the App.jsx.
Another thing to note here, destructuring supports default value assignment and we can leverage this in our components as seen in the DataComponent.jsx.

data.jsx:

```jsx
export const CORE_CONCEPTS = [
  {
    title: "Components",
    description:
      "The core UI building block - compose the user interface by combining multiple components.",
  },
  {
    title: "JSX",
    description:
      "Return (potentially dynamic) HTML(ish) code to define the actual markup that will be rendered.",
  },
  {
    title: "Props",
    description:
      "Make components configurable (and therefore reusable) by passing input data to them.",
  },
  {
    title: "State",
    description:
      "React-managed data which, when changed, causes the component to re-render & the UI to update.",
  },
];
```

App.jsx:

```jsx
import { CORE_CONCEPTS } from "./data";
import DataComponent from "./DataComponent";
function App() {
  let c = 0;
  return (
    <div>
      {CORE_CONCEPTS.map((item) => (
        <DataComponent {...item} key={c++} />
      ))}
    </div>
  );
}
export default App;
```

DataComponent.jsx:

```jsx
export default ({title,description="default description."}) => {
  return (
    <>
      <p>{title + "\n"}</p>
      <p>{description + "\n"}</p>
    </>
  );
};
```

#### Making reusable wrapper Components in React

* By default, using custom components are meant to used in the self-closing fashion. 
* If we want to use components are wrappers, like custom HTML tags then we need to tweak the code of these components to produce desired behavior.
* To show all the components between opening and closing tags of this custom wrapper component we return props.children wrapped in a div.
* To apply all the css styles through className as you would apply to a div, in the wrapper component, we recieve the className via props and add that to the className of the tag that it returned.

For example, this is a wrapper component with children and applied classes. This is used in CustomComponent.js. If we wouldn't have used destructuring and applied the classes in the div inside the wrapper component, the test and id prop would not have been used inside the Wrapper component and would have been lost.

Wrapper.js:

```jsx
import React from "react";

const Wrapper = ({children,...props})=>{
    return <div {...props}>{children}</div> 
}

export default Wrapper;
```

CustomComponent.js:

```jsx
import React from "react";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';
const CustomComponent=({x,name,message})=>{
    return (
        <Wrapper id='new' test="True">
            <div>
                {x}. {name}: <CustomMessageComponent message={message}/>
            </div>
        </Wrapper>
    );
}

export default CustomComponent;
```

We use destructuring in the tag itself to directly forward all the recieved props to the child such as css classes and other information. This is a common and effective prop forwarding pattern.

Wrapper.js

```jsx
export default ({richText,placeholder,type,...props})=>{
  return(
      <>
      <input {...props} type={richText?"textarea":"text"} placeHolder={placeholder}></input>
      </>
      );
}
```

#### Passing Components as props

* We can also pass inbuilt html tags and our custom components as props into other components.
* We can use this to dynamically set and use components as we pass them into components.

For example, here we have a Dummy.jsx that is configured to accecpt two components as props. We demonstrate how to pass both inbuilt html tags and custom component Dummy2.jsx. Using default parameters is also possible, see Dummy.jsx.

App.jsx :

```jsx
import Dummy from './Dummy';
import Dummy2 from './Dummy2';
const App=()=>{
    return (
            <div>
              <Dummy Component1="menu" Component2={Dummy2}></Dummy>
            </div>
    );
}
export default App;
```

Dummy.jsx : 

```jsx
export default ({Component1="ul",Component2})=>{
  return(
  <>
  <Component1>
  <li>Hi</li>
  <li>hello</li>
  </Component1>
  <Component2/>
  </>
  );
}
```

Dummy2.jsx

```jsx
export default ()=>{
  return(<>This is sparta!</>);
}
```

### :sparkles: Events in React 

[Docs](https://react.dev/learn/responding-to-events)

* We listen to events in react using event listners that are defined in react itself.
* For a component the event listner is passed in the tag like a prop and the value assigned is a function that must execute when the event occurs.
* The function that is assigned to the event listner can be an anonymous function, or a function referenced somewhere else.

Here is an example of an anonymous arrow function being used as an event handler for a button we created in our component. 

CustomComponent.js:

```jsx
import React from "react";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';

const CustomComponent=(props)=>{
    return (
        <Wrapper className='new'>
            <div>
                {props.x}. {props.name}: <CustomMessageComponent message={props.message}/>
                <button onClick={()=>{console.log("Anon func ran on click! ")}}>Click here.</button>
            </div>
        </Wrapper>
    );
}

export default CustomComponent;
```

Here is another example of referenced function being called upon when an event occurs.

CustomComponent.js:

```jsx
import React from "react";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';
const CustomComponent=(props)=>{
    const clickHandler=()=>{
        console.log("Referenced func ran on click! ");
    }
    return (
        <Wrapper className='new'>
            <div>
                {props.x}. {props.name}: <CustomMessageComponent message={props.message}/>
                <button onClick={clickHandler}>Click here.</button>
            </div>
        </Wrapper>
    );
}

export default CustomComponent;
```

It should be noted that you can pass your desired event handlers to the components via props as well and it is also best practice to do so.

Also, instead of making many event handlers that handler similar tasks, we can make one event handler that can do task for different element based on the argument  passed to it. We can achive this behavior by, passing an anonymous function and calling our handler with appropriate argument on the event property of a tag.

For Example, here we have multiple buttons and we can handle the clicking of all buttons with a single event handler.

App.jsx:

```jsx
function App() {
  const clickHandler=(name)=>{
    console.log(name+" was clicked!")
  }
  return (
    <div className="App">
      <button onClick={()=>clickHandler("Button1")}>Button 1</button>
      <button onClick={()=>clickHandler("Button2")}>Button 2</button>
      <button onClick={()=>clickHandler("Button3")}>Button 3</button>
    </div>
  );
}
export default App;
```

When we pass a function as an event handler, that function is passed an event object by react, which can be dereferenced to get access event and element specific attributes.

For example, we can access the text value of an input field using the event object passed to handler to set the state. More in the state section.

CustomComponent.js:

```jsx
import React,{useState} from "react";

const CustomComponent=(props)=>{
    const [text,setText]=useState('');
    const textHandler=(event)=>{
        setText(event.target.value);
    }
    return (
        <>
          <input type="text" onChange={textHandler}/>
        </>
    );
}

export default CustomComponent;
```

### :star2: State 

[Docs](https://react.dev/learn/state-a-components-memory)

* We now know how to define components and use them in React. We now need to make the components "reactive" to actions of the user.  
* We can listen to actions of the user using event listeners, but once react renders a component, it cannot re-evaluate a component unless we tell it changes in which variables must trigger a re-evaluation.  
* Without such a mechanism we can change the variable rendered in the components in event-listeners but cannot reflect the changes on the page.
* **The collection of variables that tells React to re-evaluate components when they change is called State**.  
  
#### useState hook

* The way we use the concept of State in React is by using its **useState hook**.
* We import it from 'react' and whenever we need to add a variable to the state of the component, we use this hook.
  
This is an example of a change in some text of the page when a button is clicked. We imported the hook first.  
**useState hook takes a default value and returns a variable and a function to update the variable**. We destructure them to use them in our components and event-listeners.

CustomComponent.js: 

```jsx
import React,{useState} from "react";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';

const CustomComponent=({x,name,mssg})=>{
    const [message,setMessage]=useState(mssg);
    const clickHandler=()=>{
        setMessage(message!=='Message1'?'Message1':'Message2');
        console.log('Message updated.');
    }
    return (
        <Wrapper className='new'>
            <div>
                {x}. {name}: <CustomMessageComponent message={message}/>
                <button onClick={clickHandler}>Click here.</button>
            </div>
        </Wrapper>
    );
}
```

* A point to note here is we declare the **state variable we want to change as const** because that change is handled by react using the state change function that the hook returns. That way, we can only change the variable by declaring it const by using the function, and thats how it should be.

#### prev

* Whenever we change state to a new value based on its previous state, it is not recommended to use the name of variable to access it's latest state. This is simply because, React schedules State changes and the variable may not have the latest value that we have changed it to.
* But React guarantees us that we recieve the latest snapshot of the value by using **prev**. This variable can be accessed by any using an anonymous function inside the state updating function.

In the following example we toggle a certain text based on button click. To ensure we get the latest updated value of the text, we use **prev** in the state updating function.

CustomComponent.js:

```jsx
import React,{useState} from "react";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';

const CustomComponent=({x,name,mssg})=>{
    const [message,setMessage]=useState(props.mssg);
    const clickHandler=()=>{
        setMessage((prev)=>{return prev!=="Message1"?"Message1":"Message2";});
    }
    return (
        <Wrapper className='new'>
            <div>
                {x}. {name}: <CustomMessageComponent message={message}/>
                <button onClick={clickHandler}>Click here.</button>
            </div>
        </Wrapper>
    );
}

export default CustomComponent;
```

#### Using State with event-listeners

* We not only use states to re-evaluate components but also to save values of input fields so that we can use the inputs later.
* Whenever we use a eventlistener in React, the function that we reference to handle that event recieves a event object through argument and we use event.target.value to capture the text entered in input on every keystroke.

Here is an example of a text input with onChange event-listener that saves the value on every keystroke using a state variable.

CustomComponent.js:

```jsx
import React,{useState} from "react";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';

const CustomComponent=({x,name,message})=>{
    const [text,setText]=useState('');
    const textHandler=(event)=>{
        setText(event.target.value);
    }
    return (
        <Wrapper className='new'>
            <div>
                {x}. {name}: <CustomMessageComponent message={message}/>
                <label>Dummy label :</label>
                <input type="text" onChange={textHandler}/>
                <button >Click here.</button>
            </div>
        </Wrapper>
    );
}

export default CustomComponent;
```

#### Working with multiple states

* While working with a component which has **multiple state variable**, we can either **use useState hook multiple times for each variable**, or we can use a single object that has multiple variable and use it as our state variable. 
* In this case, we need the **prev state**, so we can spread it and change the variable we need to change.

Here is an example where we handle the state of three text inputs using a single state.

CustomComponent.js:

```jsx
import React,{useState} from "react";
import './CustomComponent.css';

export default (props)=>{
    const [state,setState]=useState({
        text1:'',
        text2:'',
        text3:''
    });
    const textHandler=(event,x)=>{
        setState((prev)=>{return {...prev,["text"+x]:event.target.value}});
    }
    return (
            <div>
                <label>Dummy label :</label>
              {[1,2,3].map((item)=><input type="text" key={item} onChange={(i)=>textHandler(i,item)}/>)}
              <div>{state.text1}</div>
              <div>{state.text2}</div>
              <div>{state.text3}</div>
            </div>
    );
}
```
### :sparkles: Working with forms and Two way binding

* We often work with forms that take user input.
* The desired behavior to capture data from a form is to **save text data in state variables**, and assign a onSubmit event handler to the form tag.
* In the event handler function, we first use **event.preventDefault()** to prevent the page from reloading on form submission.
* We need to have **value property of input fields set to their respective state variable**, so that we can use the state to clear the fields on form submission.
* **This way of capturing data from the input fields using states and then using states to clear the input fields is called two way binding.**

For example, we apply **two way binding to a form** and **log the input data to the console** and **clear the fields on submission of the form**.

CustomComponent.js:

```jsx
import React,{useState} from "react";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';

const CustomComponent=(props)=>{
    const [state,setState]=useState({
        text1:'',
        text2:'',
        text3:''
    });
    const textHandler=(event,text)=>{
        setState((prev)=>({...prev,[text]:event.target.value}));
    }
    const submitHandler=(event)=>{
        event.preventDefault();
        console.log(state);
        setState({
            text1:'',
            text2:'',
            text3:''
        })
    }
    return (
        <Wrapper className='new'>
                {props.x}. {props.name}: <CustomMessageComponent message={props.message}/>
                <label>Dummy label :</label>
                <form onSubmit={submitHandler}>
                    <input type="text" value={state.text1} onChange={(e)=>textHandler(e,"text1")}/>
                    <input type="text" value={state.text2} onChange={(e)=>textHandler(e,"text2")}/>
                    <input type="text" value={state.text3} onChange={(e)=>textHandler(e,"text3")}/>
                    <button type="submit" >Click here.</button>
                </form>
        </Wrapper>
    );
}

export default CustomComponent;
```

### :star: Passing data from child to parent and Lifting the state

* We saw how parent can communicate with child and pass data to child via props.
* When we have some data in the child (e.g. some input data that we want to pass to the parent component), we make a function in the parent component, pass its reference down in props and then call the function passing the data in the argument in the child component. 
* The function should be defined in a way to recieve data and this function call we made in the child component gets called through the parent component where we actually defined the function. 

Here is a working example, the text data from three input fields that we have in CustomComponent.js can be accessed by App.js

CustomComponent.js:

```jsx
import React,{useState} from "react";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';

const CustomComponent=(props)=>{
    const [state,setState]=useState({
        text1:'',
        text2:'',
        text3:''
    });
    const text1Handler=(event)=>{
        setState((prev)=>{return {...prev,text1:event.target.value}});
    }
    const text2Handler=(event)=>{
        setState((prev)=>{return {...prev,text2:event.target.value}});
    }
    const text3Handler=(event)=>{
        setState((prev)=>{return {...prev,text3:event.target.value}});
    }
    const submitHandler=(event)=>{
        event.preventDefault();
        props.onSubmission(state);
        setState({
            text1:'',
            text2:'',
            text3:''
        })
    }
    return (
        <Wrapper className='new'>
            <div>
                {props.x}. {props.name}: <CustomMessageComponent message={props.message}/>
                <label>Dummy label :</label>
                <form onSubmit={submitHandler}>
                    <input type="text" value={state.text1} onChange={text1Handler}/>
                    <input type="text" value={state.text2} onChange={text2Handler}/>
                    <input type="text" value={state.text3} onChange={text3Handler}/>
                    <button type="submit" >Click here.</button>
                </form>
                
            </div>
        </Wrapper>
    );
}

export default CustomComponent;
```

App.js:

```jsx
import logo from './logo.svg';
import './App.css';
import CustomComponent from './CustomComponent';
function App() {
  let x=10;
  let name='Shubhanjan';
  let message='Example of working of props.';

  const getData=(textData)=>{
    console.log(textData);
  }
  return (
    <div className="App">
      <CustomComponent x={x} name={name} message={message} onSubmission={getData}/>
    </div>
  );
}

export default App;
```

* Not only calling functions passed to the child but passing data back to the parent is called **Lifting the State up**.
* We communicate between sibling component via a parent component by lifting the state up. Otherwise this communication wont be possible.
* We usually end up having a few components that manage state and many of its child components are present just to output data. The components that manage state are called **Stateful Components** whereas the components that do not manage state are called **Stateless Components**. 

### :sparkles: Lists in React

#### Rendering an array of Components dynamically

* To render components based on data from some array, we need to use javascript inside the jsx.
* We do so by using map function on the array and define the component to be rendered.
* The Component must also recieve a prop called key, to differentiate between the array elements.

For example, here we render a bunch of People.js components which recieve a name and age in props, from App.js.

People.js:

```jsx
import React from "react";

const People=(props)=>{
    return <div>{props.name} - {props.age}</div>
}

export default People;
```

App.js:


```jsx
import logo from './logo.svg';
import './App.css';
import People from './People';

function App() {
  let arr=[{key:0,
            name:'Ramesh',
            age: 23},
           {key:1,
            name:'Pushpa',
            age:22},
           {key:2,
            name:'Bobby',
            age:50}]

  return (
    <div className="App">
      {arr.map((x)=>{return <People key={x.key} name={x.name} age={x.age}/>})}
    </div>
  );
}

export default App;
```

#### Stateful Lists

* There will be many instances where we work with an array of data and when we take input from a certain component, we would want that input to the array and make the changes visible (For instance a to do app).
* Then we have to add that list to the state so that changes to it will be reflected in the output. 
* In reality it is not that different from working with a state variable.

For instance, lets say from the [previous example](#-star-passing-data-from-child-to-parent-and-lifting-the-state-) where we made a submission from the child component and logged it from the parent component, say we need to show all submissions in the page. In that case we can set an array of submissions and add it to the state. That way every time we make a submission we update the array using state updating function and the array gets re-evaluated. Notice that we are also managing the key of every array element using state.

CustomComponent.js:

```jsx
import React,{useState} from "react";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';

const CustomComponent=(props)=>{
    const [state,setState]=useState({
        text1:'',
        text2:'',
        text3:''
    });
    const text1Handler=(event)=>{
        setState((prev)=>{return {...prev,text1:event.target.value}});
    }
    const text2Handler=(event)=>{
        setState((prev)=>{return {...prev,text2:event.target.value}});
    }
    const text3Handler=(event)=>{
        setState((prev)=>{return {...prev,text3:event.target.value}});
    }
    const submitHandler=(event)=>{
        event.preventDefault();
        props.onSubmission(state);
        setState({
            text1:'',
            text2:'',
            text3:''
        })
    }
    return (
        <Wrapper className='new'>
            <div>
                {props.x}. {props.name}: <CustomMessageComponent message={props.message}/>
                <label>Dummy label :</label>
                <form onSubmit={submitHandler}>
                    <input type="text" value={state.text1} onChange={text1Handler}/>
                    <input type="text" value={state.text2} onChange={text2Handler}/>
                    <input type="text" value={state.text3} onChange={text3Handler}/>
                    <button type="submit" >Click here.</button>
                </form>
                
            </div>
        </Wrapper>
    );
}

export default CustomComponent;
```

App.js:

```jsx
import logo from './logo.svg';
import './App.css';
import CustomComponent from './CustomComponent';
import { useState } from 'react';
import People from './People';

function App() {
  let x=10;
  let name='Shubhanjan';
  let message='Example of working of props.';
  const getData=(textData)=>{
    textData={key:key,...textData};
    setTexts((prev)=>{return [textData,...prev]});
    setKey((prev)=>{
      return prev+1  
    });
  }
  const [key,setKey]=useState(0);
  const [texts,setTexts]=useState([{
    key:key,
    text1: "Dummy text1",
    text2: "Dummy text2",
    text3: "Dummy text3"
  }]);

  return (
    <div className="App">
      <CustomComponent x={x} name={name} message={message} onSubmission={getData}/>
      {texts.map((x)=>{return <p key={x.key}>{x.text1}    {x.text2}   {x.text3}</p>})}
    </div>
  );
}

export default App;
```

### :sparkles: Rendering conditional content in React

* We can render content in our React app conditionally using ternary operator or logical and operator.
* Both the and operator and ternary operator return the content to the page.
* But it is best practice to move the conditional logic outside of the return statement to keep the jsx code lean.

Example of using a ternary operator, which shows "No texts found" if the texts array is empty. Else it just renders the array.

App.js: 

```jsx
import logo from './logo.svg';
import './App.css';
import CustomComponent from './CustomComponent';
import { useState } from 'react';
import People from './People';

function App() {
  let x=10;
  let name='Shubhanjan';
  let message='Example of working of props.';
  const getData=(textData)=>{
    textData={key:key,...textData};
    setTexts((prev)=>{return [textData,...prev]});
    setKey((prev)=>{
      return prev+1  
    });
  }
  const [key,setKey]=useState(0);
  const [texts,setTexts]=useState([]);

  return (
    <div className="App">
      <CustomComponent x={x} name={name} message={message} onSubmission={getData}/>
      {texts.length===0? <p>No texts found</p>: texts.map((x)=>{return <p key={x.key}>{x.text1}    {x.text2}   {x.text3}</p>})}
    </div>
  );
}

export default App;
```

We can change the jsx as the following to demonstrate the working of logical and operator that performs the same task.

```jsx
return (
    <div className="App">
      <CustomComponent x={x} name={name} message={message} onSubmission={getData}/>
      {texts.length===0 && <p>No texts found</p>}
      {texts.length!==0 && texts.map((x)=>{return <p key={x.key}>{x.text1}    {x.text2}   {x.text3}</p>})}
    </div>
  );
```

Moving the conditional part out of the jsx code would look like so.

App.js:

```jsx
import logo from './logo.svg';
import './App.css';
import CustomComponent from './CustomComponent';
import { useState } from 'react';
import People from './People';

function App() {
  let x=10;
  let name='Shubhanjan';
  let message='Example of working of props.';
  const getData=(textData)=>{
    textData={key:key,...textData};
    setTexts((prev)=>{return [textData,...prev]});
    setKey((prev)=>{
      return prev+1  
    });
  }
  const [key,setKey]=useState(0);
  const [texts,setTexts]=useState([]);
  let textContent=texts.length===0? <p>No texts found</p>: texts.map((x)=>{return <p key={x.key}>{x.text1}    {x.text2}   {x.text3}</p>});

  return (
    <div className="App">
      <CustomComponent x={x} name={name} message={message} onSubmission={getData}/>
      {textContent}
    </div>
  );
}

export default App;
```

Also a point to note is that we can move the whole conditional part to another component and pass data to it via props. And in that component return jsx based on length of the texts array accessed via props.

### :star: Fragments, Portals and refs

#### Fragments

[Docs](https://react.dev/reference/react/Fragment)

* Wrapping Components in divs and returning them from other Components makes it cumbersome to work with the final app because we end up with a div soup that is not very optimal.
* There are various methods to work within the rules of jsx and still avoid using divs.
* Such methods include using Custom Wrapper Components and **Fragments** with Fragments being the solution provided by React.
* Instead of using divs to wrap our Components and then returning them, we use fragments to wrap our jsx code and end up with a much clear final html.
  
We must use Fragments carefully, because css classes cannot be applied to Fragments and if we require to do so we must use a div instead.
  
App.js:

```jsx
import logo from './logo.svg';
import './App.css';
import { Fragment } from 'react';

function App() {
  return (
    <Fragment>
      {/* some jsx code */}
    </Fragment>
  );
}

export default App;
```

You don't even need to import and use Fragment. Empty opening and closing tags are now being used as Fragments instead of importing ans using them.

App.js:

```jsx
import logo from './logo.svg';
import './App.css';
import { Fragment } from 'react';

function App() {
  return (
    <>
      {/* some jsx code */}
    </>
  );
}

export default App;
```

#### Portals

* Sometimes we write some jsx code which we want to ultimately show up near the body tag of the html when the page loads, but it is actually nested in some components. This phenomenon is required when we work with modals and dialogs etc. 
* If the modal shows up near the body tag, it look a lot cleaner, instead of being nested inside the html. This is also not limited to modals.
* This is where Portals are used. They render jsx code written somewhere between the Components in a place in the real DOM.
* A point to note here is **we can only 'portal' jsx code to a position in the real dom** and not to any other component.

This is a working example of a modal, that appears if we try to submit by leaving a field empty in our CustomComponent text fields.
The jsx code of the modal is ultimately rendered in the div in index.html where we have configured it to appear.

BasicModal.js:

```jsx
import * as React from 'react';
import Box from '@mui/material/Box';
import Button from '@mui/material/Button';
import Typography from '@mui/material/Typography';
import Modal from '@mui/material/Modal';

const style = {
  position: 'absolute',
  top: '50%',
  left: '50%',
  transform: 'translate(-50%, -50%)',
  width: 400,
  bgcolor: 'background.paper',
  border: '2px solid #000',
  boxShadow: 24,
  p: 4,
};

export default function BasicModal(props) {

  return (
    <div>
      <Modal
        open={props.open}
        onClose={props.onClose}
        aria-labelledby="modal-modal-title"
        aria-describedby="modal-modal-description"
      >
        <Box sx={style}>
          <Typography id="modal-modal-title" variant="h6" component="h2">
            One or more fields empty.
          </Typography>
          <Typography id="modal-modal-description" sx={{ mt: 2 }}>
            Please fill up all fields.
          </Typography>
          <Button onClick={props.onClose}>OKAY</Button>
        </Box>
      </Modal>
    </div>
  );
}
```

CustomComponent.js:

```jsx
import React,{useState} from "react";
import ReactDOM from "react-dom";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';
import BasicModal from './BasicModal';

const CustomComponent=(props)=>{
    const [modal,setModal]=useState(false);
    const [state,setState]=useState({
        text1:'',
        text2:'',
        text3:''
    });
    const text1Handler=(event)=>{
        setState((prev)=>{return {...prev,text1:event.target.value}});
    }
    const text2Handler=(event)=>{
        setState((prev)=>{return {...prev,text2:event.target.value}});
    }
    const text3Handler=(event)=>{
        setState((prev)=>{return {...prev,text3:event.target.value}});
    }
    const submitHandler=(event)=>{
        event.preventDefault();
        if(state.text1===''||state.text2===''||state.text3===''){
            setModal(true);
        }
        else{
            props.onSubmission(state);
            setState({
                text1:'',
                text2:'',
                text3:''
            })
        }
    }
    const closeModal=()=>{
        setModal(false);
    }
    return (
        <Wrapper className='new'>
            {ReactDOM.createPortal(<BasicModal open={modal} onClose={closeModal}/>,document.getElementById('portal'))}
            {props.x}. {props.name}: <CustomMessageComponent message={props.message}/>
            <label>Dummy label :</label>
            <form onSubmit={submitHandler}>
                <input type="text" value={state.text1} onChange={text1Handler}/>
                <input type="text" value={state.text2} onChange={text2Handler}/>
                <input type="text" value={state.text3} onChange={text3Handler}/>
                <button type="submit" >Click here.</button>
            </form>
        </Wrapper>
    );
}

export default CustomComponent;
```

index.html:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    <!--
      manifest.json provides metadata used when your web app is installed on a
      user's mobile device or desktop. See https://developers.google.com/web/fundamentals/web-app-manifest/
    -->
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <!--
      Notice the use of %PUBLIC_URL% in the tags above.
      It will be replaced with the URL of the `public` folder during the build.
      Only files inside the `public` folder can be referenced from the HTML.

      Unlike "/favicon.ico" or "favicon.ico", "%PUBLIC_URL%/favicon.ico" will
      work correctly both with client-side routing and a non-root public URL.
      Learn how to configure a non-root public URL by running `npm run build`.
    -->
    <title>React App</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="portal"></div>
    <div id="root"></div>
    <!--
      This HTML file is a template.
      If you open it directly in the browser, you will see an empty page.

      You can add webfonts, meta tags, or analytics to this file.
      The build step will place the bundled scripts into the <body> tag.

      To begin the development, run `npm start` or `yarn start`.
      To create a production bundle, use `npm run build` or `yarn build`.
    -->
  </body>
</html>
```

#### refs

* **refs** provide a direct way to a component in react and changing the DOM directly(which is not usually preferred).
* We can access a components value,etc using ref.
* To use refs, we use the useRef hook from react and add it as a prop named ref to the element we want to access.
* We can access the element's value using element.current.value or put focus on it using element.current.focus(), etc.

Here is an example of how we use ref instead of state in our custom component, but loose the ability to capture every keystroke and also, we interact directly with the DOM which is not preferred.

CustomComponent.js:

```jsx
import React,{useState,useRef} from "react";
import ReactDOM from "react-dom";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';
import BasicModal from './BasicModal';

const CustomComponent=(props)=>{
    const [modal,setModal]=useState(false);
    const ref1=useRef('');
    const ref2=useRef('');
    const ref3=useRef('');
    const submitHandler=(event)=>{
        event.preventDefault();
        if(ref1.current.value===''||ref2.current.value===''||ref3.current.value===''){
            setModal(true);
        }
        else{
            props.onSubmission({text1:ref1.current.value, text2:ref2.current.value, text3:ref3.current.value});
            ref1.current.value='';
            ref2.current.value='';
            ref3.current.value='';
            
        }
    }
    const closeModal=()=>{
        setModal(false);
    }
    return (
        <Wrapper className='new'>
            {ReactDOM.createPortal(<BasicModal open={modal} onClose={closeModal}/>,document.getElementById('portal'))}
            {props.x}. {props.name}: <CustomMessageComponent message={props.message}/>
            <label>Dummy label :</label>
            <form onSubmit={submitHandler}>
                <input type="text" ref={ref1}/>
                <input type="text" ref={ref2}/>
                <input type="text" ref={ref3}/>
                <button type="submit" >Click here.</button>
            </form>
        </Wrapper>
    );
}

export default CustomComponent;
```

App.js:

```jsx
import logo from './logo.svg';
import './App.css';
import CustomComponent from './CustomComponent';
import { useState } from 'react';
import People from './People';

function App() {
  let x=10;
  let name='Shubhanjan';
  let message='Example of working of props.';
  const getData=(textData)=>{
    textData={key:key,...textData};
    setTexts((prev)=>{return [textData,...prev]});
    setKey((prev)=>{
      return prev+1  
    });
  }
  const [key,setKey]=useState(0);
  const [texts,setTexts]=useState([]);
  let textContent=texts.length===0? <p>No texts found</p>: texts.map((x)=>{return <p key={x.key}>{x.text1}    {x.text2}   {x.text3}</p>});
  return (
    <div className="App">
      <CustomComponent x={x} name={name} message={message} onSubmission={getData}/>
      {textContent}
    </div>
  );
}

export default App;
```

### :star2: Side effects and useEffect()

* In React, useEffect is a Hook that allows you to **perform side effects in functional components**. Side effects refer to any operation that changes the state outside the scope of the current function, such as fetching data, manipulating the DOM, or setting up event listeners.

* The useEffect Hook takes two arguments: **a callback function** that performs the side effect, and **an array of dependencies** that specify when the effect should be triggered. The callback function is executed after the initial rendering and after every re-evaluation of the component. The dependencies array is optional and allows you to specify which variables the effect depends on. When any of these variables change, the effect is triggered again.

* Also, useEffect() support **a cleanup function** that runs before useEffect() runs again, after running once.  

* Any function other than component reevaluation cycle, such as checking if user is logged in localStorage, sending requests, performing validation, etc. which in some cases may lead to infinite loops, or is not convienient to work with using our current tools.

Some example use cases of useEffect():

* Case 1:  
 * For instance, if we had some to make a request everytime the component loads and change some state and then do nothing after that,using a http request to **Set** state of some variable just inside the component may lead to that component reevaluating again and that request being made again and the state being **Set** again resulting in an infinite loop.
 * If we had a function that ran only once to make a request and set the State and not run again, this problem will be solved.

We can use useEffect to solve the problem in the above scenario.

App.js:

```jsx
import logo from './logo.svg';
import './App.css';
import { useState,useEffect } from 'react';
import People from './People';

function App() {
  let [arr,setArr]=useState([]);
  useEffect(()=>{
    fetch('https://randomuser.me/api/?results=3')
  .then(response=>response.json())
  .then(data=>{
    let data2=data.results.map(x=>{return {key:x.login.uuid,gender:x.gender,name:x.name}})
    setArr(data2);
  })
  .catch(error=>{
    console.log(error);
  });
  },[])
  return (
    <div className="App">
      {arr.map((x)=>{return <People key={x.key} name={x.name} gender={x.gender}/>})}
    </div>
  );
}

export default App;
```
Since we provide no values in the array of dependencies, the function will just run once when component renders for first time.

* Case 2: 
 * For instance, we perform password and email validations in our event-listners. If there was any once place that we can peform validations, it would be much easy to debug later if problems arise and make the code less cumbersome.
 * And it is better that event-listners should just update state in general and validation must be handled somewhere else for code legibility and from a design point of view.
 * We can leverage the cleanup function to do things like check validation every 500ms to avoid validating on every keystroke. The cleaup function can be used to reset the timer of the previous callback, allowing us to validate 500ms after user stops typing.

Here we perform the validation using useEffect() hook.

CustomComponent.js:

```jsx
import React,{useState,useEffect} from "react";
import ReactDOM from "react-dom";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';
import BasicModal from './BasicModal';

const CustomComponent=(props)=>{
    const [error,setError]=useState(true);
    const [modal,setModal]=useState(false);
    const [state,setState]=useState({
        text1:'',
        text2:'',
        text3:''
    })
    useEffect(()=>{
        const timeout= setTimeout(()=>{
            if(state.text1!=='' && state.text2!=='' && state.text3!==''){setError(false)}
            else{setError(true)}
        },500)

        return ()=>{
            clearTimeout(timeout);
        }        
    },[state]);

    const textHandler=(event)=>{
        setState(prev=>{
            return {...prev,[event.target.name]:event.target.value};
        })
    }
    const submitHandler=(event)=>{
        event.preventDefault();
        if(error){
            setModal(true);
        }
        else{
            props.onSubmission({text1:state.text1, text2:state.text2, text3:state.text3});
            setState({
                text1:'',
                text2:'',
                text3:''
            });     
        }
    }
    const closeModal=()=>{
        setModal(false);
    }
    return (
        <Wrapper className='new'>
            {ReactDOM.createPortal(<BasicModal open={modal} onClose={closeModal}/>,document.getElementById('portal'))}
            {props.x}. {props.name}: <CustomMessageComponent message={props.message}/>
            <label>Dummy label :</label>
            <form onSubmit={submitHandler}>
                <input type="text" value={state.text1} name="text1" onChange={textHandler}/>
                <input type="text" value={state.text2} name="text2" onChange={textHandler}/>
                <input type="text" value={state.text3} name="text3" onChange={textHandler}/>
                <button type="submit" >Click here.</button>
            </form>
        </Wrapper>
    );
}

export default CustomComponent;
```

### :star2: useReducer()

* The useReducer() hook is used for more complex state management.
* If we have many states in our component and setting of one state is dependent upon some other state, then it is preferable to merge these states together and use a reducer.
* useReducer() returns a **state variable** and **dispatch function**. The **state variable is used to access states** and **dispatch function is used to set state**. Its takes a reducer function, initial state and init function as argument.
* When we use the dispatch function and pass an action object to it, React takes that object and latest state snapshot and passes it to the reducer function, which contains logic defined by us and returns the updated state.
* The component then re-evaluates based on the updated state.

For instance we have three text fields which follow two way binding to the reducer which does the validation and state updation. We call the dispatch function in the event listner to update the text states and text in the fields.

CustomComponent.js:

```jsx
import React,{useState,useEffect,useReducer} from "react";
import ReactDOM from "react-dom";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';
import BasicModal from './BasicModal';

const func=(state,action)=>{
    if(action.type.slice(0,-1)==="text"){
        state={...state,[action.type]: action.val}
        state.error= state.text1==='' || state.text2==='' || state.text3===''
        return state;
    }
    else{
        return {
            text1:'',
            text2:'',
            text3:'',
            error: true
        }
    }
    
};
const CustomComponent=(props)=>{
    const [text, dispatchText]=useReducer(func,{
        text1:'',
        text2:'',
        text3:'',
        error: true
    })
    const [modal,setModal]=useState(false);

    const textHandler=(event)=>{
        dispatchText({type:event.target.name, val:event.target.value});
    }
    const submitHandler=(event)=>{
        event.preventDefault();
        if(text.error){
            setModal(true);
        }
        else{
            props.onSubmission({text1:text.text1, text2:text.text2, text3:text.text3});
            dispatchText({type:'RESET'});     
        }
    }
    const closeModal=()=>{
        setModal(false);
    }
    return (
        <Wrapper className='new'>
            {ReactDOM.createPortal(<BasicModal open={modal} onClose={closeModal}/>,document.getElementById('portal'))}
            {props.x}. {props.name}: <CustomMessageComponent message={props.message}/>
            <label>Dummy label :</label>
            <form onSubmit={submitHandler}>
                <input type="text" value={text.text1} name="text1" onChange={textHandler}/>
                <input type="text" value={text.text2} name="text2" onChange={textHandler}/>
                <input type="text" value={text.text3} name="text3" onChange={textHandler}/>
                <button type="submit" >Click here.</button>
            </form>
        </Wrapper>
    );
}

export default CustomComponent;
```

In general, if we are setting state based on some other state, then we have to have to use reducers(because they guarantee latest state snapshot among different state variables) and/or useEffect() (since it recieves and sets state variables after rendering cycle is complete).

### :star2: Context

#### Making and using a Context

* In React, while working on an app, we will have multiple stateful and stateless components. Sometimes state of a component is managed by other components which are not in direct relation to the component and therefore the state must to lifted and passed through many components that may not use or manage the state, but just pass it through props.
* Context is a way of eliminating these long prop chains by taking certain state values and making them available to the components that we want.
* We first define a context using a createContext that takes our desired component wide state variable as argument. We assign it to a const and default export it.
* The context has a provider Component,i.e Context.Provider, that can be used to wrap the Component that we want the state variables to be available in, and all the children nested inside the component will now have access to the context. This Context.Provider component also takes a value attribute on its tag, that contains an object that maps names and the required state variables.
* Now, the functions and states we define in this object can be accesed from the context using the name given, as you would do for a prop by using the attribute name to access the function passed in that attribute.
* The way we consume the context is by using Context.Consumer or using useContext() hook from React (using the hook is cleaner).
* The useContext hook takes the Context to be used as argument and returns an object. If the context is provided, we can access state values, functions,etc by calling them from the return object. 
* We must use it carefully since it makes component reuse difficult.

We use context in this example to make a function from a parent available to a child component that consumes it.

SampleContext.js:

```jsx
import React from "react";

const SampleContext= React.createContext({
    onSubmission:()=>{}
});

export default SampleContext;
```

App.js:

```jsx
import './App.css';
import CustomComponent from './CustomComponent';
import { useState} from 'react';
import SampleContext from './SampleContext';

function App() {
  let x=10;
  let name='Shubhanjan';
  let message='Example of working of props.';
  const getData=(textData)=>{
    textData={key:key,...textData};
    setTexts((prev)=>{return [textData,...prev]});
    setKey((prev)=>{
      return prev+1  
    });
  }
  const [key,setKey]=useState(0);
  const [texts,setTexts]=useState([]);
  let textContent=texts.length===0? <p>No texts found</p>: texts.map((x)=>{return <p key={x.key}>{x.text1}    {x.text2}   {x.text3}</p>});

  return (
    <SampleContext.Provider value={{onSubmission: getData}}>
      <div className="App">
      <CustomComponent x={x} name={name} message={message} />
      {textContent}
    </div>
    </SampleContext.Provider>
    
  );
}

export default App;
```

CustomComponent.js:

```jsx
import React,{useState,useEffect,useReducer,useContext} from "react";
import ReactDOM from "react-dom";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';
import BasicModal from './BasicModal';
import SampleContext from './SampleContext';

const func=(state,action)=>{
    if(action.type.slice(0,-1)==="text"){
        state={...state,[action.type]: action.val}
        state.error= state.text1==='' || state.text2==='' || state.text3===''
        return state;
    }
    else{
        return {
            text1:'',
            text2:'',
            text3:'',
            error: true
        }
    }
    
};
const CustomComponent=(props)=>{
    const ctxt=useContext(SampleContext);
    const [text, dispatchText]=useReducer(func,{
        text1:'',
        text2:'',
        text3:'',
        error: true
    })
    const [modal,setModal]=useState(false);

    const textHandler=(event)=>{
        dispatchText({type:event.target.name, val:event.target.value});
    }
    const submitHandler=(event)=>{
        event.preventDefault();
        if(text.error){
            setModal(true);
        }
        else{
            ctxt.onSubmission({text1:text.text1, text2:text.text2, text3:text.text3});
            dispatchText({type:'RESET'});     
        }
    }
    const closeModal=()=>{
        setModal(false);
    }
    return (
        <Wrapper className='new'>
            {ReactDOM.createPortal(<BasicModal open={modal} onClose={closeModal}/>,document.getElementById('portal'))}
            {props.x}. {props.name}: <CustomMessageComponent message={props.message}/>
            <label>Dummy label :</label>
            <form onSubmit={submitHandler}>
                <input type="text" value={text.text1} name="text1" onChange={textHandler}/>
                <input type="text" value={text.text2} name="text2" onChange={textHandler}/>
                <input type="text" value={text.text3} name="text3" onChange={textHandler}/>
                <button type="submit" >Click here.</button>
            </form>
        </Wrapper>
    );
}

export default CustomComponent;
```

#### Using the Context Provider to handle state

* Now, instead of defining the Context.Provider component and using it directly on some component, we may define a new wrapper component in the Context file itself and use Context.Provider there to wrap its children.
* This way, we can move the state management logic of different states that we use in the context to the Conetext file itself and execute them in the wrapper component.
* Now, component-wide state access and management is done in one centralized place,i.e., in the Context file and the Components of the Apps become more leaner.

For example here we wrap the App component itself using the Context wrapper to move the state management logic from App.js to the Context.

SampleContext.js:

```jsx
import React,{useState} from "react";

const SampleContext= React.createContext({
    onSubmission:()=>{}
});

export const ContextProvider=(props)=>{
    const getData=(textData)=>{
        textData={key:key,...textData};
        setTexts((prev)=>{return [textData,...prev]});
        setKey((prev)=>{
          return prev+1  
        });
      }
      const [key,setKey]=useState(0);
      const [texts,setTexts]=useState([]);
    return <SampleContext.Provider value={{onSubmission:getData,texts:texts}}>{props.children}</SampleContext.Provider>
}
export default SampleContext;
```

index.js:

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import { ContextProvider } from './SampleContext';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
   <ContextProvider><App /></ContextProvider>
);

reportWebVitals();
```

App.js:

```jsx
import './App.css';
import CustomComponent from './CustomComponent';
import { Fragment } from 'react';
import SampleContext from './SampleContext';
import { useContext } from 'react';

function App() {
  let x=10;
  let name='Shubhanjan';
  let message='Example of working of props.';
  const ctxt=useContext(SampleContext);
  let textContent=ctxt.texts.length===0? <p>No texts found</p>: ctxt.texts.map((x)=>{return <p key={x.key}>{x.text1}    {x.text2}   {x.text3}</p>});
  return (
    <Fragment>
    <div className="App">
      <CustomComponent x={x} name={name} message={message} />
      {textContent}
    </div>
    </Fragment>
  );
}

export default App;
```

### :sparkles: forwardRef

* Sometimes we use ref of html components to access their values, put focus,etc.(which is not always recommended).
* But if we want to use ref to access Components, this does not work because refs in general can only be assigned to dom elements.
* But if we want to use refs for our Components( say a custom input Component) we have to modify our Components a bit.
* First we must use useRef in the component itself to target the dom elements we want to use.
* Next we must define functions in that component that makes use of those refs and performs desired operations.
* Then we use useImperativeHandle() hook from react and use it in the Component. It takes the **ref** property that gets passed to the Component like props and a function that returns an object mapping function names (that will be used on the component ref) and functions that are defined in the Component itself that refer the dom elements in the component.
* Finally for the component to support this refs, in the Component file, instead of exporting the Component function we export React.forwardRef(Component) with the component function as its argument. Now we can use refs on our Component, which is not recommended, but can be handy in niche cases.

For example, here we use three custom Input components and we use refs to put focus on the last field that had an invalid input.

Input.js:

```jsx
import React,{useRef,useImperativeHandle} from "react";

const Input=React.forwardRef((props,ref)=>{
    const inp=useRef();
    const activate=()=>{
        inp.current.focus();
    }
    useImperativeHandle(ref,()=>{
        return {focus:activate}
    })
    return <input ref={inp} type="text" value={props.value} name={props.name} onChange={props.onChange}/>
});

export default Input;
```

CustomComponent.js:

```jsx
import React,{useState,useReducer,useContext, useRef} from "react";
import ReactDOM from "react-dom";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';
import BasicModal from './BasicModal';
import SampleContext from './SampleContext';
import Input from "./Input";

const func=(state,action)=>{
    if(action.type.slice(0,-1)==="text"){
        state={...state,[action.type]: action.val}
        state.error1=state.text1===''
        state.error2=state.text2===''
        state.error3=state.text3===''
        state.error= state.error1 || state.error2 || state.error3
        return state;
    }
    else{
        return {
            text1:'',
            text2:'',
            text3:'',
            error1:true,
            error2:true,
            error3:true,
            error: true
        }
    }
    
};
const CustomComponent=(props)=>{
    const t1=useRef();
    const t2=useRef();
    const t3=useRef();
    const ctxt=useContext(SampleContext);
    const [text, dispatchText]=useReducer(func,{
        text1:'',
        text2:'',
        text3:'',
        error1:true,
        error2:true,
        error3:true,
        error: true
    })
    const [modal,setModal]=useState(false);

    const textHandler=(event)=>{
        dispatchText({type:event.target.name, val:event.target.value});
    }
    const submitHandler=(event)=>{
        event.preventDefault();
        if(text.error){
            setModal(true);
            if(text.error1) {t1.current.focus();}
            else if(text.error2) {t2.current.focus();}
            else {t3.current.focus();}

        }
        else{
            ctxt.onSubmission({text1:text.text1, text2:text.text2, text3:text.text3},ctxt.note);
            dispatchText({type:'RESET'});     
        }
    }
    const closeModal=()=>{
        setModal(false);
    }
    return (
        <Wrapper className='new'>
            {ReactDOM.createPortal(<BasicModal open={modal} onClose={closeModal}/>,document.getElementById('portal'))}
            {props.x}. {props.name}: <CustomMessageComponent message={props.message}/>
            <label>Dummy label :</label>
            <form onSubmit={submitHandler}>
                <Input ref={t1} value={text.text1} name="text1" onChange={textHandler}/>
                <Input ref={t2} value={text.text2} name="text2" onChange={textHandler}/>
                <Input ref={t3} value={text.text3} name="text3" onChange={textHandler}/>
                <button type="submit" >Click here.</button>
            </form>
        </Wrapper>
    );
}

export default CustomComponent;
```

### :star2: Optimizing React app

#### React.memo()

* The react app doesnt do Real DOM manipulations repeatedly. Instead, it finalizes all the changes in the virtual DOM and finally makes necessary changes in Real DOM since manipulating real DOM is expensive. 
* After each change that tiggers a re-evaluation, react re-runs all the child Components again, irrespective of whether they will actually change in this re-evaluation or not.
* A child component of a component will be re-run if there is some state change in that child component or parent component. And, state change of parent component will not affect this child component if the props it recieves are unchanged, thus making the child component re-run after parent component re-evaluation repetitive.
* Therefore, we must tell react to re-run the child component only if the props it recieved have changed.
* We can achieve this using **React.memo()**.
* When we export the child component, we wrap that export as a argument in React.memo().
* After every re-run of a component React checks if props of components wrapped in memo have changed, and re-runs them if such a change has happened.

Here we have a CustomMessageComponent, whose Contents can only change if the props it recieves changes, which it recieves from its parent. Here we set React.memo() on this CustomMessageComponent so that it doesnt get re-run if its props didn't change.

CustomMessageComponent.js:

```jsx
import React from "react";

const CustomMessageComponent= (props) =>{
    return <div>{props.message}</div>;
}

export default React.memo(CustomMessageComponent);
```

CustomComponent.js:

```jsx
import ReactDOM from "react-dom";
import CustomMessageComponent from "./CustomMessageComponent";
import Wrapper from './Wrapper';
import './CustomComponent.css';

const CustomComponent=(props)=>{
    return (
        <Wrapper className='new'>
            {props.x}. {props.name}: <CustomMessageComponent message={props.message}/>
        </Wrapper>
    );
}

export default CustomComponent;
```

* A thing to note here is, React.memo() should be used keeping the props comparison opeartion of React.memo() in mind.

* But this only takes care of props that are of primitive data type. During component re-runs function are re-created and hence comparing them using React.memo() using their reference is not possible.
* If the CustomMessageComponent had recieved some function as a prop and the same function is passed to CustomMessageComponent again, React.memo() won't be able to handle that since function references change on Component re-evaluations and same function end up with different reference after an re-evaluation.

* To prevent re-creating the same function everytime after re-evaluation, we use **useCallback()**.

#### useCallback()

* We use useCallback on functions so that these functions are not recreated everytime the component re-evaluates. 
* One of the advantage of that can be to use function along with React.memo().
* useCallback takes a function as an argument, and an array of dependencies. Only when one of the dependencies change, the function will be recreated.

For example, say we have two custom button components and one button toggles some text in a paragraph and other toggles the functionality of that first button using a boolean state.

Both the button handlers are set with useCallback. One button has no dependency and other has a state as a dependency. Using conventional React operation, both these handlers would have been re-created everytime text changed or the first button is disabled. 
Using useCallback, the first handler is just created once, and second handler is re-created everytime it dependency state changes.

If we just useCallback on the second handler and not pass the state as a dependency, then it will just save the value of the state and reuse it, defeating the purpose of state in general. Passing the state as a dependency, ensures normal functioning and prevents function recreation on every re-evaluation. Thus, we can use React.memo() on our custom Button Component as well while using functions from the props.

Button.js:

```jsx
import React from "react";

const Button=(props)=>{
    console.log("Created Button.")
    return <button onClick={props.onClick}>{props.children}</button>
}

export default React.memo(Button);
```

CustomComponent2.js:

```jsx
import React, {useCallback, useState } from "react";
import Button from "./Button";
const CustomComponent2=()=>{
    const [permission,setPermission]= useState(true);
    const [text,setText]= useState('Blue');
    const permissionToggleHandler=useCallback(()=>{
        setPermission(prev=> !prev);
    },[]);
    const toggleTextHandle=useCallback(()=>{
        if(permission){
            setText(prev=> prev==='Blue'?'Red':'Blue');
        }
    },[permission]);
    return (
    <>
        <Button onClick={toggleTextHandle}>Toggle Text</Button>
        <Button onClick={permissionToggleHandler}>Toggle Button permission.</Button>
        <p>{text}</p>
    </>
    );
}

export default CustomComponent2;
```

#### useMemo()

* Similar to how we persisted references to functions using useCallback, we can persist references to objects using useMemo().
* useMemo() takes a function as its first argument and a list of dependencies as its second argument and returns an object. Now this object will change and return a new reference only when the dependecies change.
  
For example we pass an array to some component which sorts it consumes that object in some way. This means that our child component that recieves the array sorts it every time it is re-evaluated due to internal re-evaluation or due to re-evaluation of the parent.

Also, even if the parent component passes a hard-coded array, a new reference will be passed to the child because, references change upon re-evaluation.

So to prevent the passing a new reference for a hard-coded value we can use useMemo() here and again to prevent the child from sorting the same array again we add a useMemo there and give the passed prop as one of the dependecy.

SortedList.js:

```jsx
import React, { useMemo } from "react";

const SortedList=(props)=>{
    
    let sortedList=useMemo(()=>{
        console.log("Ran sort");
        return props.list.sort();
    },[props.list]) 
    
    return (
    <>
    {sortedList.map(x=>x)}
    </>);
}

export default SortedList;
```

CustomComponent3.js:

```jsx
import React, { useMemo, useState } from "react";
import SortedList from "./SortedList";

const CustomComponent3= ()=>{
    const [x,setX]=useState(false);

    let list=useMemo(()=>{
        return [5,4,3,2,1];
    },[])
    const clickHandler=()=>{
        setX(prev=>!prev);
    }
    return (
    <>
    <SortedList list={list}/>
    <button onClick={clickHandler}>Click!</button>

    </>
    );
}

export default CustomComponent3;
```

#### making requests using useEffect and useCallback 

* To fetch data, we use the fetch api which is supported by the browser.
* We usually fetch data in response to some action, or we are fetching that data on render, we use useEffect hook.
* We use state to take the fetched data and re-evaluate the component.
* Sometimes, when we are using a function to fetch data and using useEffect to call that function after initial rendering, we must pass the pointer of the function in the dependencies(since it is a dependency and also since it may change due to some state change inside it).
* Since references change in every re-evaluation, to prevent useEffect from calling the function, setting state, and repeats over and over( since we passed the pointer into the useEffect and it is changing on every reevaluation), we use useCallback on the function that makes the request, and pass the states that it depends on as dependencies so that function gets recreated only if one of its dependencies change.

Here, we use load button to make a request and show that data on the screen and use another toggle button to fetch data from another url. The function fetches data according to value of a state variable which we can toggle. We also use useEffect() to call this function on startup as well. We wrap the function using useCallback and pass state as one of the dependencies.

CustomComponent4.js:

```jsx
import React, { useState,useEffect,useCallback } from "react";
import People from './People';
const CustomComponent4=()=>{
    const [x,setX]=useState(true);
    const [arr,setArr]=useState([]);
    const loadHandler=useCallback(async ()=>{
        if(x){
            fetch('https://randomuser.me/api/?results=5')
            .then(response=>response.json())
            .then(data=>{
                let data2=data.results.map(x=>{return {key:x.login.uuid,gender:x.gender,name:x.name.first+" "+x.name.last}})
                setArr(data2);
            })
            .catch(error=>{
                console.log(error);
            });
        }
        else{
            fetch('http://universities.hipolabs.com/search?name=indian')
            .then(response=>response.json())
            .then(data=>{
                let data2=data.map(x=>{return {key:x.name,gender:x.country,name:x.name}})
                setArr(data2.slice(0,5));
            })
            .catch(error=>{
                console.log(error);
            });
        }
        
    },[x]);
    useEffect(()=>{
        loadHandler();
    },[loadHandler])
    
    const toggleHandler=()=>{
        setX(prev=>!prev);
    }
    return(
        <>
        {arr.map((x)=>{return <People key={x.key} name={x.name} gender={x.gender}/>})}
        <button onClick={loadHandler}>Load!</button>
        <button onClick={toggleHandler}>Toggle Content!</button>
        </>
    ); 
}

export default CustomComponent4;
```

We can send post requests using fetch api as follows.

```jsx
const objectHandler=async (object)=>{
    const response= await.fetch('sample-url',{
        method:'POST',
        body:JSON.stringify(object),
        headers:{
            'Content-Type': 'application/json'
        }
    });

    const data=await response.json();
    console.log(data);
}
```

### :star: Connecting to a database

* React is frontend code that runs in the browser of the client and hence we should not attempt to connect to a database using react. Our React app usually talks to a backend that connects to a database and sends us the data via http requests.
* We should make a backend that provides functionality by exposing endpoints from which sending and recieving data is possible.
* 


### :star2: making custom Hooks

* We can make custom hooks in react by creating a function whose name starts with 'use', we define this function to be used with other hooks and use it as one.
* Custom hooks are used to make function that manage some state logic, as state logic cannot be managed by normal functions since use of hooks is not allowed in functions that are not react components.
* We make hooks when we have some code that is duplicated, or can be compressed to a single configurable function and it manages some state logic.
* Making custom hooks need careful use of useMemo() and useCallback() wherever necessary to prevent inifinite re-evaluations and other bugs in general.
* It should be noted that making and using custom hooks without proper design can lead to bugs and performance issues.
* In addition to this, it should be noted that all other hook both custom or pre-defined can be used in other hooks. We use other hooks as per necessity.

In this example we make an custom hook newHook() that returns a method sendRequest, that can both send and recieve data with respect to a source that is also externally configurable and uses state functions of the component to update the state. We use this hook to interact with an api that posts and gets data as per our request and the data is reflected on the screen as it is posted using a form.

use-newhook.js

```jsx
import { useCallback } from "react";
const useNewHook=()=>{
    const sendRequest=useCallback(async(config,func=null)=>{
        try{
            const response= await fetch(config.url,{
            method:config.method?config.method:'GET',
            body:config.inputText?JSON.stringify(config.inputText):null,
            headers: config.headers? config.headers:{}
        });
        const data= await response.json();
        console.log(data);
        if(func){
            func(data);
        }
        }
        catch(error){
            console.log(error);
        }
    },[]);
    return [sendRequest];
}

export default useNewHook;
```

CustomComponent5.js

```jsx
import React, { useEffect, useState , useCallback,useMemo } from "react";
import useNewHook from './use-newhook';

const CustomComponent5= ()=>{
    const url='https://fir-project-8ad16-default-rtdb.firebaseio.com/texts.json';
    const getInput=useMemo(()=>{return {url:url}},[]);
    const [inputText,setInput]=useState('');
    const [texts,setTexts]=useState([]);
    const [sendRequest]=useNewHook();

    const func1=useCallback((data)=>{
        let arr=[];
            for(let x in data){
                arr.push(data[x]);
            }
        setTexts(arr);
    },[]);

    const get=useCallback(async()=>{
        await sendRequest(getInput,func1);
    },[sendRequest,getInput,func1]);

    const post=async()=>{
        await sendRequest(
            {url:url,
            method:'POST',
            inputText:inputText,
            headers:{
                        'Content-Type': 'application/json'
                    }
        });
    }
    useEffect(()=>{
        get();
    },[get]);

    const inputTextHandler=(event)=>{
        setInput(event.target.value);
    }
    const makeSubmission=async(event)=>{
        event.preventDefault();
        setInput('');
        await post();
        await get();
    }
    return(
        <>
            <form>
                <input type="text" value={inputText} onChange={inputTextHandler}></input>
                <button onClick={makeSubmission}>Submit</button>
                <div>
                {texts.map(x=> <p key={x}>{x}</p>)}
                </div>
            </form>
        </>
    );
}

export default CustomComponent5;
```

### :star2: Redux

#### Using Redux

* Usually we use hooks and props and context to manage state of components. When we need some state to be available to many components, we can't use useState/useReducer and props because of long prop chains. Also, using Context can become cumbersome if we have many contexts. Providing them to Components can result in complex context nesting or long un-maintainable context files.
* Redux can be a solution for writing maintainable state wide logic for our React apps.
* Basic operation of Redux can boil down to something similiar to operating a reducer.
* To use redux, we have to npm install **redux** and **react-redux**.
* We first import createStore from redux.
* We define a redux **store** const by calling createStore().
* This function accepts a **reducer function** which is similar to a reducer function from useReducer, and is called whenever we dispatch an action. We must define a reducer function before passing it.
* Then we default export the **store const**.
* This redux store acts as a central state managing unit. Anywhere in the app, if we dispatch some action, the reducer function will be call with the action given to update the state.
* We use this component wide state created by using **two functions from react-redux called useSelector and useDispatch**.
* useDispatch returns a function that we can use to dispatch actions. useSelector takes a function which must return the necessary state components, which we store in a const. We use useSelector to extract the part of the overall state that we are working with in the current component.
* Note that, the dispatch function sholud not mutate the state, i.e., changing something in the state and returning it. We must use the previous snapshot of the state to create a new state object which contains the necessary changes. We return this new object. Mutating state object can lead to bugs and app malfunctions.

Suppose we define our store as an object containing a count field (given a value of 0 by default). We define our reducer to take increment and decrement actions which returns a state object with counter increased or decreased.

store/index.js:

```jsx
import { createStore } from "redux";

const reducer=(state={counter:0},action)=>{
    if(action.type==="increment"){
        return {counter: state.counter+1};
    }
    if(action.type==="decrement"){
        return {counter: state.counter-1};
    }
    if(action.type==="reset"){
        return {counter: 0}
    }
    return state;
}

const store=createStore(reducer);

export default store;
```

CustomComponent7.js:

```jsx
import { useSelector, useDispatch } from "react-redux";
const CustomComponent7=()=>{
    const dispatch=useDispatch();
    const counter=useSelector(state=> state.counter);
    return(
        <>
        {counter}
        <button onClick={()=>{dispatch({type : "increment"})}}> Increment </button>
        <button onClick={()=>{dispatch({type : "decrement"})}}> Decrement </button>
        <button onClick={()=>{dispatch({type : "reset"})}}> Reset</button>
        </>

    );
}

export default CustomComponent7;
```

#### Using Redux with Redux toolkit

* Redux is a state management library in general and is react independent. To make working with redux more simple, use use redux toolkit.
* We **npm install @reduxjs/toolkit**.
* In our reducer file, instead of defining a reducer, we now define a const which calls createSlice().
* This create slice creates a slice for managing a part of our overall state.
* Its takes an object as argument, which must contain a name field , an initialState field and a reducers field which contains an object that has functions which handle state change. Instead of using our action object to make changes in our state, we now use these functions. All these functions can recieve arguments of our previous state snapshot and an action object, which contains **a payload field** that contains the arguments passed in the function calls.
* These functions are different from the reducer function from normal redux in the sense that, it's fine to mutate state in these functions because toolkit uses **immer**, which looks for these mutations and handles them internally.
* Instead of creating a store, we call configureStore() which accepts an object with mandatory **reducer** field, whose value must be pointed to **slice.reducer**(both singular collective **reducer**).
* We export slice.actions to use the reducers we defined before.
* We default export the configureStore const.
* We import useSelector, useDispatch as we normally would and we also import the actions from the store.
* We use useSelector to extract the necessary state slice and useDispatch to get a dispatch function.
* In every dispatch call, we **call** the necessary reducer function imported from actions, passing arguments to it if necessary.

Here, we define a slice with initialState of counter set to 0, and necessary reducers and use them in a component.

store/index.js:

```jsx
import { createSlice, configureStore } from "@reduxjs/toolkit";

const slice=createSlice({
    name: 'counter',
    initialState : {counter : 0},
    reducers:{
        increment(state){
            state.counter++;
        },
        decrement(state){
            state.counter--;
        },
        reset(state){
            state.counter=0;
        }
    }
});

export const actions=slice.actions;

const store=configureStore({
    reducer: slice.reducer
});

export default store;
```

CustomComponent7.js:

```jsx
import { useSelector, useDispatch } from "react-redux";
import { actions } from "./store";
const CustomComponent7=()=>{
    const {reset,decrement,increment}=actions;
    const dispatch=useDispatch();
    const counter=useSelector(state=> state.counter);
    return(
        <>
        {counter}
        <button onClick={()=>{dispatch(increment())}}> Increment </button>
        <button onClick={()=>{dispatch(decrement())}}> Decrement </button>
        <button onClick={()=>{dispatch(reset())}}> Reset</button>
        </>

    );
}

export default CustomComponent7;
```

#### using multiple slices in Redux

* We ususally split the state slices into different files.
* In each of these files we export the reducers to index.js (store file) and export the actions created by slice from the slice file itself.
* Now we can import respective slice action from the slice file and use them in our components to dispatch actions.

For example, here we have a counter slice which handless the state of a counter component and a text slice that handles the state of a text field that. The counter has increment, decrement and reset options, and the text state is just used to display that text in a paragraph.

store/index.js:

```jsx
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./counterSlice";
import textReducer from "./textSlice";
import cartReducer from "./cartSlice";
const store=configureStore({
    reducer: {counter: counterReducer, text: textReducer}
});

export default store;
```

CounterSlice.js:

```jsx
import { createSlice } from "@reduxjs/toolkit";

const counterSlice=createSlice({
    name: 'counter',
    initialState : {counter : 0},
    reducers:{
        increment(state){
            state.counter++;
        },
        decrement(state){
            state.counter--;
        },
        reset(state){
            state.counter=0;
        }
    }
});

export const counterActions=counterSlice.actions;

export default counterSlice.reducer;
```

TextSlice.js:

```jsx
import { createSlice } from "@reduxjs/toolkit";

const textSlice=createSlice({
    name:'text',
    initialState:{text:''},
    reducers:{
        update(state,action){
            state.text=action.payload;
        },
        clear(state){
            state.text='';
        }
    }
});

export const textActions=textSlice.actions;

export default textSlice.reducer;
```

#### thumb rule for pure vs async code 

* All the code written in Redux must be pure(non-async).
* We want all the synchronous state logic in the reducers so that we can have lean components and let the reducers handle the state logic.
* Async code must be handled using hooks in components (useEffect) or by making custom action creators.
* Following this pattern logically makes sense and makes our code easier to work with.


#### handling async state logic with custom action creators

* Redux dispatch function can be used to call the action creators created by the state slice.
* But, we can make function that returns another function that recieves a dispatch function as argument, and dispatch some actions there and write async code there as well.
* This function can be dispatched like any other action creator, and the function returned by this function is passed on the dispatch function and redux runs that function for us.
* We usually define this action creator in the slice for which it is used and export it.

For example here we define an action creator for updating a variable in our dummy backend. We update the state using other default action creators and then use our custom action creator along with useEffect to send a PUT request.

store/textSlice.js:

```jsx
import { createSlice } from "@reduxjs/toolkit";

const textSlice=createSlice({
    name:'text',
    initialState:{text:'',status:null},
    reducers:{
        update(state,action){
            state.text=action.payload;
        },
        clear(state){
            state.text='';
        },
        setStatus(state,action){
            state.status=action.payload;
        }
    }
});

export const sendTextData=(text)=>{
    return async (dispatch)=>{
        dispatch(textSlice.actions.setStatus('sending'));
        const func=async()=>{
            const data=await fetch('https://fir-project-8ad16-default-rtdb.firebaseio.com/new.json',{
            method: 'PUT',
            body: JSON.stringify(text),
            headers:{
                'Content-Type': 'application/json'
            }
            });
            return data;
        }
        try{
            const response= await func();
            if(!response.ok){
                throw Error('Something went wrong');
            }
            console.log(response);
            dispatch(textSlice.actions.setStatus('success'));
            
        }
        catch{
            dispatch(textSlice.actions.setStatus('error'));
        }
    }
}
export const textActions=textSlice.actions;

export default textSlice.reducer;
```

CustomComponent7.js:

```jsx
import { useSelector, useDispatch } from "react-redux";
import { counterActions } from "./store/counterSlice";
import { textActions } from "./store/textSlice";
import { sendTextData } from "./store/textSlice";
import { useEffect } from 'react';
const CustomComponent7=()=>{
    const {reset,decrement,increment}=counterActions;
    const {setStatus,update,clear}=textActions;
    const dispatch=useDispatch();
    const counter=useSelector(state=> state.counter.counter);
    const text=useSelector(state=> state.text.text);
    const status=useSelector(state=>state.text.status);
    useEffect(()=>{
        console.log('calling send func.')
        const timeout=setTimeout(()=>{
            dispatch(sendTextData(text));
        },500);
        
        return ()=> clearTimeout(timeout);
    },[text,dispatch])
    useEffect(()=>{
        const timeout=setTimeout(()=>{
            if(status==='error'||'success'){
                dispatch(setStatus(null));
            }
        },2000);
        return ()=> clearTimeout(timeout);
    },[status,dispatch,setStatus])
    return(
        <>
        <p>{counter}</p>
        <button onClick={()=>{dispatch(increment())}}> Increment </button>
        <button onClick={()=>{dispatch(decrement())}}> Decrement </button>
        <button onClick={()=>{dispatch(reset())}}> Reset</button>
        <div>
            <p>{text}</p>
            <input onChange={(event)=>dispatch(update(event.target.value))} value={text}></input>
            <button onClick={()=>dispatch(clear())}>Clear</button>
            <p>{status}</p>
        </div>
        </>

    );
}

export default CustomComponent7;
```

### :star: Routing

#### Adding routes and links
* npm install react-router-dom.
* We simulate routing in spas using some routing library, here we use react-router-dom. We define the path and components to be rendered in those paths and pass them as an array of objects to a util named createBrowserRouter(). This function returns a router object.
* We also import the RouterProvider Component and pass the router object to it.
* The route provider component shows content based on the route that is followed.
* We can change routes using <Link to={}></Link> tags that take a route as attribute. We add these tags to Components the text thta is provided between these tags becomes clickable to reroute us.

Example, here we have added Component6 and Component7 to the routes using '/' route for Component7 and '/6' route for Component6.
In the App component we add these routes to createBrowserRouter and add that router to the RouteProvider component.

App2.js:

```jsx
import './App.css';
import { createBrowserRouter,RouterProvider } from 'react-router-dom';
import CustomComponent7 from './CustomComponent7';
import CustomComponent6 from './CustomComponent6';

const router= createBrowserRouter([
  {path:'/',element:<CustomComponent7/>},
  {path:'/6',element:<CustomComponent6/>}
]);

const App2=()=> {
  
  return ( 
    <RouterProvider router={router}/>
  );
}

export default App2;
```

CustomComponent7.js:

```jsx
//imports
import { Link } from "react-router-dom";
const CustomComponent7=()=>{
    //code
    return(
        <>
        {/* jsx */}
        <Link to={'/6'}>go to /6</Link>
        </>

    );
}

export default CustomComponent7;
```

CustomComponent6.js:

```jsx
//imports
import { Link } from "react-router-dom";
const CustomComponent6=()=>{
    //code
    return(
        <>
        {/* jsx */}
        <Link to={'/'}>go to root</Link>
        </>

    );
}

export default CustomComponent6;
```

#### Adding a root to outlet different subroutes

* Usually when we route, we need to have a root component, that holds the components that are common to all subroutes.
* To define routes like this, we need to make a root component that holds a <Outlet/> tag in its jsx where it renders components based on subroutes.
* All subroutes are defined in the children attribute of the root route.
* Components like navigation component etc are rendered in the root.

For example, following the previous routing example, we add the Links to the root components and render the components there based on subroutes.

App2.js:

```jsx
import './App.css';
import { createBrowserRouter,RouterProvider } from 'react-router-dom';
import CustomComponent7 from './CustomComponent7';
import CustomComponent6 from './CustomComponent6';
import Root from './Root';

const router= createBrowserRouter([
  {path:'/',
  element:<Root/>,
  children:[
    {path:'/',element:<CustomComponent7/>},
    {path:'/6',element:<CustomComponent6/>}
  ]}
  
]);

const App2=()=> {

  return ( 
    <RouterProvider router={router}/>
  );
}

export default App2;
```

Root.js:

```jsx
import { Outlet } from "react-router-dom";
import { Link } from "react-router-dom";
const Root=()=>{
    return (
    <>
    <h1>Root</h1>
    <Link to={'/'}>go to root</Link>
    <br/>
    <Link to={'/6'}>go to /6</Link>
    <Outlet/>
    </>
    );
}

export default Root;
```

#### error page, NavLink and navigating programmatically 

* When we define a router using createBrowserRouter we can add another errorElement attribute that can be used to render a error component, if some undefined route is accessed with respect to route of the router.

App2.js:

```jsx
import './App.css';
import { createBrowserRouter,RouterProvider } from 'react-router-dom';
import CustomComponent7 from './CustomComponent7';
import CustomComponent6 from './CustomComponent6';
import ErrorPage from './ErrorPage';
import Root from './Root';

const router= createBrowserRouter([
  {path:'/',
  element:<Root/>,
  errorElement: <ErrorPage/>
  children:[
    {path:'/',element:<CustomComponent7/>},
    {path:'/6',element:<CustomComponent6/>}
  ]}
  
]);

const App2=()=> {

  return ( 
    <RouterProvider router={router}/>
  );
}

export default App2;
```

* Its common in navigation bars to highlight the current active route. react-router-dom has a tag called NavLink whose className attribute can hold a function. This function is passed an object from react, that contains an isActive attribute. We can target its value to apply conditional classes to NavLink active routes.
* Suppose if some path is active and the navbar also has another path which is a part of the current path, then it is considered active as well by default. To stop this behavior we can use end attribute in the NavLink.

Root.js:

```jsx
import { NavLink, Outlet } from "react-router-dom";
const Root=()=>{
    return (
    <>
    <h1>Root</h1>
    <NavLink to={'/'} className={({isActive})=>isActive?'activeClass':'normalClass' } end>go to root</NavLink>
    <br/>
    <NavLink to={'/6'} className={({isActive})=>isActive?'activeClass':'normalClass'} end>go to /6</NavLink>
    <Outlet/>
    </>
    );
}

export default Root;
```

* We can navigate programmatically using the useNavigation hook provided by react-router-dom that returns a function, where we can pass a route and we redirect to that route.

Example, here we use useEffect to route to another after 3s of rendering the component.

CustomComponent6.js:

```jsx
import React from "react";
import useInput from './use-inputhook';
import { useEffect } from "react";
import { useNavigate } from "react-router-dom";
const CustomComponent6=()=>{
    const navigate=useNavigate();
    useEffect(()=>{
        const timeout=setTimeout(()=>{
            navigate('/');
        },3000);

        return ()=>clearTimeout(timeout);
    },[navigate]);
    // logic//
    return (
    <>
    {/* jsx */}
    </>
    );
}

export default CustomComponent6;
```

#### Dynamic routes

* We defining routes for dynamic components, we must use a route that is dynamic. For example, route to each product displayed in a products page.
* To define such routes, we just add colon and a route variable name. Now we can use and modify this dynamic route to show content.
* The element that is rendered for this dynamic route, can access the route variable we defined by using useParam() and calling the route variable name on the object returned.

For example we have a dummy array of products that has id, titles,etc. We show each of these in a product component and are added dynamically. For each product we go to products/id and this id is variable. 

App2.js:

```jsx
import './App.css';
import { createBrowserRouter,RouterProvider } from 'react-router-dom';
import CustomComponent6 from './CustomComponent6';
import Root from './Root';
import ErrorPage from './ErrorPage';
import CustomComponent8 from './CustomComponent8';
import Home from './Home';
const router= createBrowserRouter([
  {path:'/',
  element:<Root/>,
  errorElement:<ErrorPage/>,
  children:[
    {path:'',element:<Home/>},
    {path:'products',element:<CustomComponent8/>},
    {path:'products/:urlString',element:<CustomComponent6/>}
  ]}
]);

const App2=()=> {

  return ( 
    <RouterProvider router={router}/>
  );
}

export default App2;
```

CustomComponent8.js:

```jsx
import React from "react";
import { Link } from "react-router-dom";
const dummyProducts=[
    {id:'1',title:'Product 1'},
    {id:'2',title:'Product 2'},
    {id:'3',title:'Product 3'},
    {id:'4',title:'Product 4'},
    {id:'5',title:'Product 5'},
    {id:'6',title:'Product 6'}
]
const CustomComponent8=()=>{
    return(
        <>
        <ul>
            {dummyProducts.map((prod)=> <li><Link key ={prod.id} to={prod.id}>{prod.title}</Link></li>)}
        </ul>
        </>

    );
}

export default CustomComponent8;
```

CustomComponent6.js:

```jsx
import React from "react";
import useInput from './use-inputhook';
import { Link, useParams } from "react-router-dom";
const CustomComponent6=()=>{
    const params=useParams();
    // code //   
    return (
    <>
    <form onSubmit={submitHandler}>
        <>
        {params.urlString}
        <Link to={'..'} relative='path'>Back</Link>
        </>
    </form>
    </>
    );
}

export default CustomComponent6;
```

#### relative vs absolute path 

* When we start the path for a route with '/' we define its absolute path. This means that while routing the whole path defined here is used.
* Where as, if we just write without using '/' from the start, the route is path we give on top of the path of the root.
* Defining absolute paths in components and routes can get cumbersome if we change route definitions later on.

#### relative attribute in Link tag

* While using relative path, we have the option of using a relative attribute in Link tag. It supports values like path and route. By default this is set to route and subseqent navigations will be dependent upon the route definition, setting this attribute to path makes use of the current relative path instead.

For example here in the route definition, root element has two child routes. Going to relative path '..' in 'products/id' page by default, the page is routed to Home since that is the relative 'back' path. Setting the relative attribute in Link as path going 'back' in 'products/id' page takes us to 'products' page instead.

App2.js:

```jsx
import './App.css';
import { createBrowserRouter,RouterProvider } from 'react-router-dom';
import CustomComponent6 from './CustomComponent6';
import Root from './Root';
import ErrorPage from './ErrorPage';
import CustomComponent8 from './CustomComponent8';
import Home from './Home';
const router= createBrowserRouter([
  {path:'/',
  element:<Root/>,
  errorElement:<ErrorPage/>,
  children:[
    {path:'',element:<Home/>},
    {path:'products',element:<CustomComponent8/>},
    {path:'products/:urlString',element:<CustomComponent6/>}
  ]}
]);

const App2=()=> {

  return ( 
    <RouterProvider router={router}/>
  );
}

export default App2;
```

CustomComponent6.js:

```jsx
import React from "react";
import useInput from './use-inputhook';
import { Link, useParams } from "react-router-dom";
const CustomComponent6=()=>{
    const params=useParams();
    // code //   
    return (
    <>
    <form onSubmit={submitHandler}>
        <>
        {params.urlString}
        <Link to={'..'} relative='path'>Back</Link>
        </>
    </form>
    </>
    );
}

export default CustomComponent6;
```

#### index routes

* While defining routes in router, we define the default page (routed at rootpath/'') by giving the path as ''.
* Instead of doing this, we can define this 'index' object by defining an index attribute in it instead of path attribute and this will show the same behavior as giving path as ''.
* This also keeps the code more readable.

App2.js:

```jsx
import './App.css';
import { createBrowserRouter,RouterProvider } from 'react-router-dom';
import CustomComponent6 from './CustomComponent6';
import Root from './Root';
import ErrorPage from './ErrorPage';
import CustomComponent8 from './CustomComponent8';
import Home from './Home';
const router= createBrowserRouter([
  {path:'/',
  element:<Root/>,
  errorElement:<ErrorPage/>,
  children:[
    {index: true,element:<Home/>},
    {path:'products',element:<CustomComponent8/>},
    {path:'products/:urlString',element:<CustomComponent6/>}
  ]}
]);

const App2=()=> {
  return ( 
    <RouterProvider router={router}/>
  );
}

export default App2;
```

#### using loaders

* Usually we switch to a page which does some async operations after rendering to re-evaluate and show the page.
* We can run the async code that is needed for loading the contents and render that page after the components have been fetched using react-router-dom.
* This async function can be set up in the router using a loader attribute in the route object.
* We usually define this function in its respective component and export it. We import and use its reference in the router.
* The data fetched using loader can be accessed using useLoaderData hook in the component.
* It should be notes that the loader can return promises, custom Responses and throw errors as well.

Here we define the loader for CusotmAsyncComponent in its file. We import this function in the router. This hook provides the closest loader data.

CustomAsyncComponent.js:

```jsx
import { useLoaderData } from "react-router-dom";

const CustomAsyncComponent=()=>{
    const text=useLoaderData();
    return(
    <>
    <p>{text}</p>
    </>);
}

export const loader=async()=>{
    const response=await fetch('https://fir-project-8ad16-default-rtdb.firebaseio.com/new.json');
    return response.json();
}
export default CustomAsyncComponent;
```

App2.js:

```jsx
import './App.css';
import { createBrowserRouter,RouterProvider } from 'react-router-dom';
import CustomComponent6 from './CustomComponent6';
import Root from './Root';
import ErrorPage from './ErrorPage';
import CustomComponent8 from './CustomComponent8';
import Home from './Home';
import { loader } from './CustomAsyncComponent';
import CustomAsyncComponent from './CustomAsyncComponent';
const router= createBrowserRouter([
  {path:'/',
  element:<Root/>,
  errorElement:<ErrorPage/>,
  children:[
    {index:'',element:<Home/>},
    {path:'products',element:<CustomComponent8/>},
    {path:'products/:urlString',element:<CustomComponent6/>},
    {path:'message',element:<CustomAsyncComponent/>,loader:loader}
  ]}
]);

const App2=()=> {

  return ( 
    <RouterProvider router={router}/>
  );
}

export default App2;
```

* When we switch to a page that runs some async code before showing the page, there might be a slight delay since the page loads after the data has been fetched.
* react-router-dom provides a hook that returns an object which can be used to monitor the status of the data being fetched and some indicators can be returned components like navigation component and show this status.
* This hook is called useNavigation hook and the object it returns has a status property which we use.

We implement the useNavigation hook in the navigation component.

Root.js:

```jsx
import { NavLink, Outlet, useNavigation } from "react-router-dom";
const Root=()=>{
    const navigation=useNavigation();
    return (
    <>
    <h1>Root</h1>
    <NavLink to={''} className={({isActive})=>isActive?'activeClass':'normalClass' } end>go to root</NavLink>
    <br/>
    <NavLink to={'products'} className={({isActive})=>isActive?'activeClass':'normalClass'} end>go to products</NavLink>
    <br/>
    <NavLink to={'message'} className={({isActive})=>isActive?'activeClass':'normalClass' } end>go to message</NavLink>
    <br/>
    {navigation.state==='loading' && "Loading"}
    <Outlet/>
    </>
    );
}

export default Root;
```

#### Customising error thrown while routing

* The errorElement Component that is passed in the router, is used to handle any errors thrown during routing. This component is also used to handle error thrown from loaders.
* So while throwing error from loaders, we can throw customized Responses and use them to display a specialised error message in the error page.
* We can access the error thrown using useRouteError from react-router-dom and access properties like status or parse the json and take the message out of it.

CustomAsyncComponent.js:

```jsx
import { useLoaderData } from "react-router-dom";

const CustomAsyncComponent=()=>{
    const text=useLoaderData();
    return(
    <>
    <p>{text}</p>
    </>);
}

export const loader=async()=>{
    const response=await fetch('https://fir-project-8ad16-default-rtdb.firebaseio.com/new.json');
    if(!response.ok){
        throw new Response(JSON.stringify({message:'Loading failed'}),{status:505});
    }
    else{
        return response.json();
    }
}
export default CustomAsyncComponent;
```

ErrorPage.js:

```jsx
import React from "react";
import {useRouteError } from "react-router-dom";
import NavComponent from "./NavComponent";
const ErrorPage=()=>{
    const error=useRouteError();
    const message= JSON.parse(error.data).message; 
    return (
        <>
        <NavComponent/>
        <p>{message}</p>
        </>
    );
}

export default ErrorPage;
```

#### throw json

* To simplify throwing new Responses from loaders, react-router-dom has a special function called json, which can be use to throw a new response.
* This is similar to throwing new Response, but syntax is cleaner and we dont have to parse the json in the error page.

Equivalent statements:
```jsx
throw new Response(JSON.stringify({message:'Loading failed'}),{status:505});

throw json({message:'Loading failed'},{status:505});
```

#### using dynamic route params in loaders

* While using dynamic routes(for example, while working with a product page) we need a param from the url to then make a fetch request to get data for the specific param.
* We may want to use loader for fetching the data. React router passes the request data and params as arguments to the loader when it is called.

For example here we use loader to fetch data using params and pass that data to CustomComponent6 using useLoaderData hook.

CustomComponent6.js

```jsx
import { useLoaderData } from "react-router-dom";
const CustomComponent6=()=>{
    const data= useLoaderData();
    //code
    return (
    <>
    <form >
        {/* jsx */}
        {data.urlString}
        {/* jsx */}
    </form>
    </>
    );
}

export default CustomComponent6;

export const utilLoader=({requests,params})=>{
    // some async operations that gives data
    return data;
}
```

#### useRouteLoaderData() hook

* Sometimes we may need data that was loaded by some other loader in the route but we need it some other page in the route, be it parent or child.
* To access the loader data of other loader in the same route we use useRouteLoaderData() hook and pass an id string to it, which must be defined in the path object for that page in the router.
* By doing so, we can access the data of any currently rendered route pages.

Here is an example of a nested route and how we use useRouteLoaderData() to supply data to different pages in the same route.

App2.js:

```jsx
import './App.css';
import { createBrowserRouter,RouterProvider } from 'react-router-dom';
import CustomComponent6, { utilLoader } from './CustomComponent6';
import Root from './Root';
import ErrorPage from './ErrorPage';
import CustomComponent8 from './CustomComponent8';
import Home from './Home';
import { loader } from './CustomAsyncComponent';
import CustomAsyncComponent from './CustomAsyncComponent';
import CustomComponent9 from './CustomComponent9';
const router= createBrowserRouter([
  {path:'/',
  element:<Root/>,
  errorElement:<ErrorPage/>,
  children:[
    {index:'',element:<Home/>},
    {path:'products',
    children:[
      {index:true,
      element:<CustomComponent8/>},
      {path:':urlString',
      id:'loader-id',
      loader:utilLoader,
      children:[
        {index:true, element:<CustomComponent6/>},
        {path:'edit', element:<CustomComponent9/>}
      ]
      }
    ]
    },
    {path:'message',element:<CustomAsyncComponent/>,loader:loader}
  ]}
]);

const App2=()=> {

  return ( 
    <RouterProvider router={router}/>
  );
}

export default App2;
```

CustomComponent6.js:

```jsx
import React from "react";
import useInput from './use-inputhook';
import { Link, useRouteLoaderData } from "react-router-dom";
const CustomComponent6=()=>{
    const params=useRouteLoaderData('loader-id');
    //code
    return (
    <>
    <form onSubmit={submitHandler}>
        {/* jsx */}
        {params.urlString}
        {/* jsx */}
    </form>
    </>
    );
}

export default CustomComponent6;

export const utilLoader=({requests,params})=>{
    return params;
}
```

CustomComponent9.js:

```jsx
import { useRouteLoaderData } from "react-router-dom";

const CustomComponent9=()=>{
    const data=useRouteLoaderData('loader-id');
    return(
        <>
        <p>{data.urlString}</p>
        </>
    );
}

export default CustomComponent9;
```
</div>
