### If you encounter the following error during testing

- ##### Reference error: global in not defined

### Just enter the following code in the first line of all the SPEC files

- ```javascript
  (window as any).global = window;
  ```

