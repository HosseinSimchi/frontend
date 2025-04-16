**All generated selectors have the "select" prefix, and the feature selector has the "State" suffix**

### `state.ts`

**In this example, the name of the feature selector is selectBooksState, where "books" is the feature name. The names of the child selectors are selectBooks and selectLoading, based on the property names of the books feature state.**

```javascript
interface State {
  books: Book[];
  loading: boolean;
}

const initialState: State = {
  books: [],
  loading: false,
};
```

### `createFeature`

```javascript
export const booksFeature = createFeature({
  name: "books",
  reducer: createReducer(
    initialState,
    on(BookListPageActions.enter, (state) => ({
      ...state,
      loading: true,
    })),
    on(BooksApiActions.loadBooksSuccess, (state, { books }) => ({
      ...state,
      books,
      loading: false,
    }))
  ),
});

export const {
  name, // feature name
  reducer, // feature reducer
  selectBooksState, // feature selector
  selectBooks, // selector for `books` property
  selectLoading, // selector for `loading` property
} = booksFeature;
```

### NOTE

_Also_

```javascript
provideState(booksFeature);
```

_Feature states can also be registered in the providers array of the route config._

```javascript
export const routes: Route[] = [
  {
    path: "books",
    providers: [provideState(booksFeature)],
  },
];
```

### The generated selectors can be used independently or to create other selectors:

```javascript
import { createSelector } from "@ngrx/store";
import { booksFeature } from "./books.reducer";

export const selectBookListPageViewModel = createSelector(
  booksFeature.selectBooks,
  booksFeature.selectLoading,
  (books, loading) => ({ books, loading })
);
```
