## React-Router-dom

React router is a routing library in React, synchronizing between URL and the UI. Meaning URL => Route => Corresponding UI.

Installation :
```
npm install react-router-dom
```
```
yarn add react-router-dom
```

## Primary component

- routers : Browser Router and Hash Router
- route matchers : Route and Switch ( Routes RouterV6)
- navigation : Link, NavLink, Redirect

Example :
```javascript
 imported { BrowserRouter, Route, Link } from "react-router-dom";
```
### Router

Router is the main core in every React Router Web application. BrowserRouter and HashRouter is mainly used in React Web project.

To use Router, wrap ( ussually ) App component ( highest level component ) inside a Router

### Router matchers

There are 2 matching component : Switch and Route

When Switch is rendered, it choose the first child ( route ) that has the path match the current URL and then ignore others. If no matched path route, Switch return null.



***Note :***
- Write the most specified route first.
- Route path matches the begining of URL. So the path ( like below ) always match every URL. 
``` javascript
<Route path="/"><Home/> </Route>"
```
So we can put this Route the last in Switch. The other way, we can use ```exact``` to tell that ```Route``` will rendered if only the whole URL match the it's path.
- Note recommend using route without path but using hook instead. ( useRouteMatch )
- In react-router-dom V6 exact is default in all Route, ```Switch``` now changed to ```Routes``` 

### Navigation ( Route changer )

- ```<Link>``` component, when rendered, it renders ```<a>``` in HTML document.

- ```<NavLink>``` is special types of <Link> which can styles itself when active ( its ```to``` props match the current location ).

- ```<Redirect>``` force navigate using its ```to``` props.
## BrowserRouter vs HashRouter
- Different in URL and the way they communicate the server.
- **BrowserRouter** is used more often. Using History API in HTML5 to track the history. It uses regular URL ( best looking ). Required server configured correctly. Specifically, web server serve same page for all URL. ***out of the box*** in development, and ***comes with instruction*** on how to configure the server. 
```html
<a href="/home>
```
```javascript
import {BrowserRouter as Router} from 'react-router-dom'
```
*Props:*

**basename: string** define the base URL for all route.

**getUserConfirmation: func** use confirm navigation. 
Default using window.confirm.
```javascript
<BrowserRouter
  getUserConfirmation={(message, callback) => {
    // this is the default behavior
    const allowTransition = window.confirm(message);
    callback(allowTransition);
  }}
/>
```
**forceRefresh: bool** if true, refresh full page whenever navigating.

**keyLength : number**

- **HashRouter** Using hash of URL (window.location.hash), stores the current location in hash portion of URL. The hash is never sent to the server. Not required congfiguration on server.
```html
<a href="#/home">
```
```javascript
import {HashRouter as Router} from 'react-router-dom'
```
## React-router object
### History 
History object is a stack of entries, has some methods:
- length : number of entries in history stack.
- action(string)
  + push: add on the stack.
  + replace : replace current entries with the top instead of adding more.
  + pop : remove the top entries
  + go(n) : move the pointer in stack n entries
  + goBack : go(-1)
  + goFoward : go(1)
  + block(prompt) function prevent navigation, give message to confirm navigate with ```window.confirm```
- location : object show the current location with properties :
  + pathName : (string) The path of Url.
  + search : query url string.
  + hash : url hash fragment
  + state

History is mutable object so History.Location can't be used in side effect. Recommended Location object instead.

### Location

Location shows where the webpage is now.  A location object never mutated so can be use in lifecycle hooks to determine when navigation happens.

### match
A match object  contains information how a Route is matched with url.
- params (object) : pairs parsed from url corresponding the dynamic segment of the path.
## Route

A mapping between an URL and a component. When access to an URL, the corresponding component will be rendered. Usually used in ```Switch```.

```javascript
<Switch>
        <Route exact path="/" >
             <Home/>
        </Route>
        <Route path="/About" >
             <About/>
        </Route>
        <Route path="/Contact" >
             <Contact/>
        </Route>
        <Route exact path="/other" >
             <NotFound/>
        </Route>
</Switch>
```
with 
- **exact** : tell the Route rendered only if the URL matches exactly the path
- **path** : the base URL
- **component:** render coressponding compoent when the URL is matched
## Scroll Restoration

In the page with long content, when navigating to another location, the view is stayed at scroll down. We need a scroll top component to handle this issue.  

```javascript
function ScrollToTop() {
  useEffect(() => {
    window.scrollTo(0, 0);
  }, []);

  return null;
}
```

## Link

Similar to ```<a>``` to link to another resources.
```javascript
<Link to="/about">About</Link>
```
with :
- ```to:```  string URL(pathname + search), Function ( return string URL or Location object), Location object ( pathname, search, hash, state to persist to the location )

optional:

- ```replace:``` when true, replace current entry in history stack instead of adding new one.

- ```component:``` passing a component props
## NavLink
A version of Link with styling.
In react Router v6, activeClass and active style is removed and replaced with ```className``` and ```style``` that return function taking props ```isActive```.

- **className:** string or function ( return String )

- **style:** object .CSSproperties or function return object properties. 

- **exact: bool** if true, the class/style will only applied if the location matched exactly. 

## Redirect

Navigate to a new location and override the current location in History stack.
- **to(string)** : A valid URL path
- **to(Object)** : An object with pathName, URL params, state.
- **push(boolean)** : push instead of override
- **from(string) ... to(string)** : navigate from old pathName to new pathname. Only used in Switch. All URL parameter are provided in ```to```.


## WithRouter
A HOC ( higher order component ). It will pass updated match, location and history props into wrapped component.

**Note** : WithRouter does not re-render on route transition unless its parents component re-render.

***All non-react specific static methods and properties of the wrapped component are automatically copied to the "connected" component.***
### Component.WrappedComponent
### wrappedComponentRef: func
## React Router Hook
### useHistory
Get the history object.
```javascript
// v5
const history = useHistory();
history.push('/home');
history.replace('/home');
history.push('/home', {state: state});
history.go(1)
history.goBack()
history.goForward()
```


```javascript
// v6
const navigate = useNavigate()
navigate('/home');
navigate('/home', {replace: true});
navigate('/home', {state: state});
navigate(1)
```

### useLocation
Return the location object.
```javascript
const location = useLocation();
// location.pathname
// location.params()
```
### useParams
Return an object of key/value pairs of URL parameters.
```javascript
const params = useParams();
```
### useRouteMatch

