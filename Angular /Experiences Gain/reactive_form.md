### To define a form using FormBuilder, we proceed as follows:

```javascript
constructor(private fb: FormBuilder) {}

this.myForm = this.fb.group({
  username: [""],
  password: [""],
  host: ["", Validators.required],
  port: ["", Validators.required],
});
```

### If we want to make changes immediately when the value of an input changes, we need to listen to that input. Similar to the following:

```javascript
ngOnInit(){
    this.myForm.get('host').valueChanges.subscribe(type => {
      this.customMethod(type);
    });
}
```

### Some important functions on inputs:

```javascript
this.myForm.get("username").clearValidators();
this.myForm.get("username").disable();
this.myForm.get("username").setValidators([Validators.required]);
this.myForm.get("username").enable();
this.myForm.get("username").updateValueAndValidity();
this.myForm.valid; //returns true/false
```

### USAGE

```html
<input formControlName="host" class="form-control" placeholder="Enter host" />
```
