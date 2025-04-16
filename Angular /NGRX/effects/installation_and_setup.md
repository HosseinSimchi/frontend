### Installation

```javascript
ng add @ngrx/effects@latest
```

### Setup

```javascript
bootstrapApplication(AppComponent, {
  providers: [provideStore(), provideEffects(MoviesEffects, actorsEffects)],
});
```

_or_

```javascript
export const routes: Route[] = [
  {
    path: "movies",
    providers: [provideEffects(MoviesEffects, actorsEffects)],
  },
];
```
