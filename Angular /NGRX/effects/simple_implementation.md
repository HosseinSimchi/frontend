### `movies.service.ts`

```javascript
@Injectable({
  providedIn: 'root',
})
export class MoviesService {
  private http = inject(HttpClient);

  getAll(): Observable {
    return this.http.get('/movies');
  }
}
```

### Create `movies.effects.ts`

```javascript
import { Injectable, inject } from '@angular/core';
import { Actions, createEffect, ofType } from '@ngrx/effects';
import { of } from 'rxjs';
import { map, exhaustMap, catchError } from 'rxjs/operators';
import { MoviesService } from './movies.service';

@Injectable()
export class MoviesEffects {
  private actions$ = inject(Actions);
  private moviesService = inject(MoviesService);

  loadMovies$ = createEffect(() => {
    return this.actions$.pipe(
      ofType('[Movies Page] Load Movies'),
      exhaustMap(() => this.moviesService.getAll()
        .pipe(
          map(movies => ({ type: '[Movies API] Movies Loaded Success', payload: movies })), // or call loadSucces(movies)
          catchError(() => of({ type: '[Movies API] Movies Loaded Error' })) // or call of(loadError())
        )
      )
    );
  });
}
```

### USAGE (`component.ts`)

```javascript
  private store = inject(Store<{ movies: Movie[] }>);
  protected movies$ = this.store.select(state => state.movies);

  ngOnInit() {
    this.store.dispatch({ type: '[Movies Page] Load Movies' });
  }
```
