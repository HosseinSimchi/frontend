1- To write documentation for components

- `compodoc`

2- Add to the `script` file:

- "compodoc": "sudo npx compodoc -p tsconfig.doc.json"
- "document": "sudo npm run compodoc",

3- Create `tsconfig.doc.json`

- ```javascript
  {
  "include": ["src/**/*.ts"],
  "exclude": ["src/test.ts", "src/**/*.spec.ts", "src/app/file-to-exclude.ts"]
  }
  ```

4- `npm run document`
