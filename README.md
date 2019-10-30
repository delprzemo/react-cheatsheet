# React Cheatsheet
Set of basic functionalities from React in one place. 

Cheatsheet was created by https://foreach.pl trainers for their students.

# Table of Contents


 Basic React commands
=================

| Command  | Notes | 
| ------------- | ------------- | 
| npx create-react-app {app name} | Create new React app |
| npm run build  | Build React app - create folder with files ready for deployment | 
| npm start  | Run project locally | 
| npm test  | run tests in React app |
| npm eject | remove the single build dependency from your project |

 

JSX
=================

JSX allows us to write HTML elements in JavaScript and place them in the DOM. Basically, it converts HTML tags into react elements.

## JSX - injection JS into HTML

```jsx
 const value = 'Hello world'
 return ( <div>{value}</div>);
```
'Hello world' will be injected and displyed inside `<div>` element

## JSX - element declaration

```jsx
 const value = 'Hello World'
 const element = <div className="App">{value}</div>
 return (element);
```
We can assign specific DOM fragment to particular variable (element above) and then (re)use it everywhere.

## JSX - function injection

```jsx
 function addNumbers(x1, x2) {
   return x1 + x2;
 }
 const element = <div className="App">{addNumbers(2, 5)}</div>
```
Not only string values can be injected into DOM. Result of above case will be div with 7 inside as addNumbers was injected into element.

## JSX - attributes
```jsx
  const avatarUrl = "img/picture.jpg"
  const element = <img src={user.avatarUrl}></img>;
```
JavaScript code can be also called for DOM element properites/events


Components
=================

"React lets you define components as classes or functions. Components defined as classes currently provide more features which are described in detail on this page"

## Function component

Sample component:
```jsx
function App() {
  return <div>Hello World</div>;
}
export default App;
```

Sample component with parameters:

```js
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}
```
```js
<Welcome name="Sara" />
```

## Class component

Sample component:
```js
class App extends React.Component  {
  render() {
    return <div>Hello World</div>;
  }
}
export default App;
```

Sample component with parameters:

```js
class Welcome extends React.Component  {
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}
export default App;
```
```jsx
<Welcome name="Sara" />
```

## Events

event in element:
```jsx
<a href="#" onClick={this.onClick}> Click me </a>
```

onClick function:
```jsx
onClick(e) {
    e.preventDefault();
    // some logic here
}

```

**Access to "this" inside event:**

1. bind this
```js
this.onClick = this.onClick.bind(this);
```

2. Arrow function 
```js
onClick = (e) => {
    e.preventDefault();
    console.log(this);
}
```

or

```jsx
 <a href="#" onClick={(e) => this.onClick(e)}> Click me</a>
```

**Child event**

Child component (somewhere in code):
```js
this.props.onChange(val1, val2,...)
```

Parent component: 

```jsx
 <Child 
   onChange={hasChanged} />
```

```js
function hasChanged(val1, val2,...) {
 // some logic here
}
```

## Conditional element

Show element depending of implemented condition

**Option 1:**
```js
function SomeElement(props) {
   const show = props.isShowed;
   if(show) {
      return <div>Here is element</div>;
   }         
	}
```
then: 
```jsx
<SomeElement  isShowed  = {true} />
```

**Option 2:**
```js
let element;      
if(this.state.isShow) {
 element  = <div> Here is element </div>;
} 
```

and then use element variable in jsx

**Option 3:**
```jsx
{this.state.isShow  ?  <div> Here is element </div> : 'No element'}
```

## List of elements

Recommended way to show list of same component is use "map" function, example:
```js
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((numer, index) =>
  <li key={number.toString()}>
    {number}
  </li>
);

```
Then just use listItems element in your jsx DOM

## Content projection

Content projection is inject some html from parent component to child component

Example:

Parent component:
```jsx
<MyElement><h1>Hello world</h1></MyElement>
```

Child (MyElement) component:

```jsx
<div>
	{this.props.children}
</div>
```

`<h1>Hello world</h1>` will be injected to place where `{this.props.children}`, so MyElement will look like:

```jsx
<div>
	<h1>Hello world</h1>
</div>
```


Routing
=================
Router will be described for react-router-dom library, which I can recommend. 

Install:
```
npm install react-router-dom 
```

Sample for area where components matching to current url will be rendered:

```jsx
<Router>
   <Switch>
     <Route path="/help"><Help /></Route>
     <Route path="/list"><List /></Route>
     <Route path="/"><Home /></Route>
   </Switch>
 </Router>

```

Link changing current url:

```jsx
<Link className="nav-link" to="/list">List</Link>
```

Tip: Route and Link need to be in same Router element

## Nested routing

Parent:
```jsx
<Route path="/some" component={SomeComponent}></Route>
```

SomeComponent: 
```jsx
function  SomeComponent({ match }) {
    return (
        <Router>
            <Switch>
                <Route path={`${match.path}/child`}><Child /></Route>
            </Switch>
        </Router>
    )
}
```

## Routing with parameters

```jsx
<Route path="/some/:id" component={SomeComponent}></Route>
```

and then in SomeComponent we have access to:

```jsx
{match.params.id}
```

## Authentication

Good idea is to create custom Route component that will show specific component only when our authentication logic is passed:

```jsx
function PrivateRoute({ component: Component, ...rest }) {
    return (
        <Route {...rest} render={(props) => (_isAuthentictedLogic_) ?
            (<Component {...props} />) :
            (<Redirect to={{ pathname: "/noAccess", state: { from: props.location } }} />
            )}
        />
    );
}
```

Then instead of Route use PrivateRoute

```jsx
<PrivateRoute path="/list" component={List}></PrivateRoute>
```


State and life cycle
=================

## State
The state decides about the update to a component’s object. When state changes, the component is re-rendered.

Declaring initial state: 
```js
constructor() {
    this.state = { userId: 2, userName: "Jannice"};
}
```

Using state:
```jsx
<div> this.state.date </div>
```

Updating state:
```js
this.setState({ userId: 3, userName: "Tom"});
```
After setState component will be re-rendered 

## Life cycle

| Life cycle  | Notes | 
| ------------- | ------------- | 
| componentDidMount | Called atthe beggining of component life - when component has been rendered |
| componentWillUnmount | This method is called before the unmounting of the component takes place.  |
| componentWillUpdate | Before re-rendering component (after change)  |
| componentDidUpdate | After re-rendering component (after change)  |
| shouldComponentUpdate | Deterimines whether component should be updated after change or not  |

Example:
```jsx
componentDidMount() {
    console.log("componentDidMount")
    // some logic here
}

componentWillUnmount() {
    console.log("componentWillUnmount")
    // some logic here
}
```

Forms
=================

Sample form:

```js
onValueChange  = (event) => {
    this.setState({ value:  event.target.value  });
}
```
```js
onSubmit = (e) => {
	e.preventDefault();
	// Submit logic
}

```
```jsx
<form onSubmit={this.handleSubmit}>
    <input type="text"
        value={this.state.value}
        onChange={this.onValueChange}
    />
    
    <input type="submit" value="Send" />
</form>
```

Validation is described here: https://webfellas.tech/#/article/5
