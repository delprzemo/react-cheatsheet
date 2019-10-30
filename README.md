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
```js
<Welcome name="Sara" />
```

Routing
=================
Router will be described for react-router-dom library, which I can recommend. 

Install:
```
npm install react-router-dom 
```

Sample for area where components matching to current url will be rendered:

```js
<Router>
   <Switch>
     <Route path="/help"><Help /></Route>
     <Route path="/list"><List /></Route>
     <Route path="/"><Home /></Route>
   </Switch>
 </Router>

```

Link changing current url:

```js
<Link className="nav-link" to="/list">List</Link>
```

Tip: Route and Link need to be in same Router element

## Nested routing
