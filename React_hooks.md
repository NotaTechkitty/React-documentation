# React Hooks
**React 16.8**

What is Hook ?

\- Hook is a ***special function*** let you **hook into** function Components some React features ( state, life cycle, ... ) into Function Components.

Why using Hook ?

\- When using React Features, we need to write complicated Class Components. With React Hook, instead, we write Function Component + Hook.

Where should we use Hook ?

```javaScript
Function Component(props)  {
  // You can use Hooks here!
  return <div />;
}
```
Can Hooks be used in Class ?

\- **No**. They are used instead of class
## UseState

Function Components can't hold and change **state** like Class Components.

 => UseState Hooks :
 - Add local states to function components
 - Changing **state** by a function **setState** with custom name. useState takes one arguments as initial state or undefined if not taking any. ```const [count, setCount] = useState(0)```
 - Use array_destructuring to declare useState variable.
 - Can use object and array to store multiple values as one state.

Using Class components :

```javascript
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
  }
  increCounter() {
    this.setState({ count: this.state.count + 1 });
  }
  render() {
    return (
      <div>
        <h2>this is counter : {this.state.count}</h2>
        <button type="button" onClick={() => this.increCounter()}>
          Increase counter
        </button>
      </div>
    );
  }
}
}
 ```

Using UseState Hooks :
 ```javascript
 function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div className="d-flex">
      <h2>this is counter : {count}</h2>
      <button type="button" onClick={() => setCount(count - 1)}>
        Decrease counter
      </button>
      <button type="button" onClick={() => setCount(count + 1)}>
        Increase counter
      </button>
    </div>
  );
}
 ```
## UseEffect

- Component lifecyle hook, tell the component what to do after render, the function passed in is called **effect**.
- Place useEffect inside component to let it use local state variable of the component.
- Effect is called every render including the first.
- Effect happens not need to be synchronous.
- After render, the effect called different from previous effect.


Using class ES6 :

```javascript
class TaskCounter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  componentDidMount() {
   GetTask(this.state.count)
  }
  componentDidUpdate() {
   GetTask(this.state.count)
  }

  render() {
    return (
      <div>
        <p>You get {this.state.count} task</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Get Task
        </button>
      </div>
    );
  }
}
```

Using useEffect Hook

```javascript
function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    GetTask(count);
  });

  return (
    <div>
      <p>You get {count} task</p>
      <button onClick={() => setCount(count + 1)}>
        Get Task
      </button>
    </div>
  );
}
```
### Optional argument:

In the case above, useEffect is called **every time** the component re-render, though the count state not changing anything. This will handle the problem :

```javascript
useEffect(() => {
    GetTask(count);
  },[count]);
```

We could also use the optional argument like this: 

```javascript
// this will run once after the first render ~ ComponentDidMount.
useEffect(() => {
    GetTask(this.state.count);
  },[]);
```

```javascript
// this will skip the first run
const useDidUpdateEffect = (func, deps) => {
    const didMount = useRef(false);
    useEffect(() => {
      if (didMount.current) {
        func();
      } else {
        didMount.current = true;
      }
    }, deps);
  };
```

## useRef

- useRef return a mutable ref object.
- Use .current method to get its value.
- Pass into an argument as an initial value
- The value of useRef variable persist in full component life time and changing the value **won't trigger re-render**