## Rendering in React 
### DOM ( Document Object Model )
DOM is a structured representation of HTML element that are presented in a webpage or web-app. DOM represent the entire UI of the application. For example :

![DOM example](Image\DOM_example.PNG "DOM example")

Each UI element is a node in DOM tree. DOM is useful  helping developer modify specified content and update through method : getElementById(), getElementByClass(). 

### Virtual DOM
When DOM changed, browser has to re-render the the webpage and it's time costly.

For example : when submit event, in JQuery :
- Access all related node
- Update if necessary

==> Time cosly ==> Solution : Reactjs using Virtual DOM

Virtual is a exactly like DOM but can't interact with the UI. Working with React is working with object in Virtual DOM not with the DOM. Reactjs handles low-level HTML DOM API to update the DOM :

- React takes a Snapshot of Virtual DOM ( state draft ) and compare with the last updated Virtual DOM then update it.
- After updating, React using Diffing to compare to determine where the changes occured on real DOM then update exactly elements.

