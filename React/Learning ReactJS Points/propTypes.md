### installation

```javascript
npm i prop-types
```

### All common types

1- `PropTypes.string`
2- `PropTypes.number`
3- `PropTypes.bool`
4- `PropTypes.object`
5- `PropTypes.func`
6- `PropTypes.symbol`
7- `PropTypes.array`
8- `PropTypes.arrayOf(PropTypes.number)`

### USAGE

```javascript
const Product = ({title, name, isTrusted}) => {
  return ()
}
// don't import propTypes
Product.propTypes = {
  title: PropTypes.string.isRequired,
  name: PropTypes.oneOf(["Ali", "Hossein"])
  isTrusted: PropTypes.oneOfType([PropTypes.string, PropTypes.bool])
}
```
