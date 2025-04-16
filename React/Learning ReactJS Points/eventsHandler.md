### USAGE (class components)

```javascript
const Product = () => {
  myFunction(){ }

  return <button onClick={myFunction}>Click me</button>;
};
```

#### TO use `this` object inside the method. (**CLASS COMPONENTS**)

1- The First Approach

```javascript
return <button onClick={this.myFunction.bind(this)}>Click me</button>;
```

1- The Second Approach

```javascript
return <button onClick={() => this.myFunction()}>Click me</button>;
```
