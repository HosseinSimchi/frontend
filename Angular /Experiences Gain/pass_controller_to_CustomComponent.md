### Sending one of the form inputs from parent to child to control the form value in the parent.

**parent component**

```javascript
this.contactForm = this._fb.group({
  id: [""],
  name: ["", [Validators.required]],
});
```

```html
<harvest-input [controller]="$any(contactForm).get('name')"></harvest-input>
```

**child component**

```javascript
  @Input() controller!: FormControl;
```

```html
<input matInput [formControl]="controller" />
```
