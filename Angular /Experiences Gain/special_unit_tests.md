### Components

## Example - 1

- If you have:

```javascript
customMethod(data: any){
  data.collapse();
  data.expand();

  return this.getDataByService(node);
}
```

- Test corresponding to the above method

```javascript
it("#customMethod - should call getDataByService()", () => {
  spyOn(component, "getDataByService");

  const data = {
    collapse: jasmine.createSpy("collapse"),
    expand: jasmine.createSpy("collapse"),
  };

  component.customMethod(data);

  expect(data.collapse).toHaveBeenCalled();
  expect(data.expand).toHaveBeenCalled();
  expect(component.getDataByService).toHaveBeenCalled();
});
```

## Example - 2

- If you have:

```javascript
customMethod(data: any){
    this.frmSignalDetails.get('name')?.disable();
}
```

- Test corresponding to the above method

```javascript
it("#customMethod - should disable the name input", () => {
  spyOn(component.frmSignalDetails.controls["name"], "disable");

  component.customMethod();

  expect(
    component.frmSignalDetails.controls["name"].disable
  ).toHaveBeenCalled();
});
```

## Example - 3 (get the latest value using BehaviorSubject)

- If you have:

```javascript
// getData!: Subscription;

customMethod(data: any){
    this.getData = this.customServiceSpy?.latestValue?.subscribe(
      {
        next: (response: any) => this.handleGetDataSuccess(response),
      }
    );
}
```

- Test corresponding to the above method

```javascript
//Edit the beforeEach setup
customServiceSpy.latestValue = new BehaviorSubject(0);

it("#customMethod - should get latest data value using BehaviorSubject", () => {
  spyOn(component, "handleGetDataSuccess");

  component.customMethod();

  customServiceSpy.latestValue.next(1);

  expect(component.handleGetDataSuccess).toHaveBeenCalledWith(1);
});
```
