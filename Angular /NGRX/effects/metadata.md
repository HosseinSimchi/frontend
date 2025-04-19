### Non-dispatching Effects

**Sometimes you don't want effects to dispatch an action (Add `{ dispatch: false }` to the createEffect function as the second argument.)**

**log.effects.ts**

```javascript
import { Injectable, inject } from '@angular/core';
import { Actions, createEffect } from '@ngrx/effects';
import { tap } from 'rxjs/operators';

@Injectable()
export class LogEffects {
  private actions$ = inject(Actions);

  logActions$ = createEffect(() => {
    return this.actions$.pipe(
        tap(action => console.log(action))
    );
    }, { dispatch: false });
}
```
