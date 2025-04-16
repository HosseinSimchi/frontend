**1- App.jsx**

```javascript
<User name="Hossein" />
```

**2- User.jsx**

```javascript
const User = ({ name }) => {
  return <p> {name} </p>;
};
```

### spread syntax to send props

**1- App.jsx**

```javascript
const AllProducts = [{id:1, name:'kafoor'},{id:8, name:'bastani'}]

<Product {...AllProducts[0]} />
<Product {...AllProducts[1]} />
```

**2- Product.jsx**

```javascript
const Product = ({ id, name }) => {
  return (
    <p>
      {" "}
      {name} {id}{" "}
    </p>
  );
};
```

### Change the name of the recieved prop

```javascript
const Product = ({ name: ProductName }) => {
  return <p>{ProductName}</p>;
};
```

### Default value

```javascript
const Product = ({ name = "titab" }) => {
  return <p>{name}</p>;
};
```

### Children Prop

**1- App.jsx**

```javascript
<Product>
  <p> My name is Hossein Simchi</p>{" "}
</Product>
```

**2- Product.jsx**

```javascript
const Product = ({ children }) => {
  return <>{children}</>;
};
```
