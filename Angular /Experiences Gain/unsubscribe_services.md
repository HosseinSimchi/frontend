### When subscribing to a service, some memory is occupied. Using the following technique, the allocated resources are terminated when we are done with the component.

1- define `subject` property:

- ```javascript
  private readonly unsubscribe$ = new Subject<void>();
  ```

2- define the service using `takeUntil` rxjs operator:

- ```javascript
  this.customService
    .get()
    ?.pipe(takeUntil(this.unsubscribe$))
    ?.subscribe({
      next: (response: any) => {
        // ...
      },
      error: (error: any) => console.error(error),
    });
  ```

3- `ngOnDestroy()`:

- ```javascript
  this.unsubscribe$.next();
  this.unsubscribe$.complete();
  ```
