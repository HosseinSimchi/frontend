**The createActionGroup function creates a group of action creators with the same source**

### `products-page.actions.ts`

```javascript
import { createActionGroup, emptyProps, props } from '@ngrx/store';

export const ProductsPageActions = createActionGroup({
  source: 'Products Page',
  events: {
    // defining an event without payload using the `emptyProps` function
    'Opened': emptyProps(),

    // defining an event with payload using the `props` function
    'Pagination Changed': props<{ page: number; offset: number }>(),

    // defining an event with payload using the props factory
    'Query Changed': (query: string) => ({ query }),
  },
});
```

**USAGE**

```javascript
this.store.dispatch(ProductsPageActions.opened());

this.store.dispatch(ProductsPageActions.paginationChanged({ page, offset }));
```
