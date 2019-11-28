# Angular

## Routing

### Passing Parameters

Parameters can be passed to the routes by adding parameters to the route definition in the 

```typescript
RouterModule.forRoot([
      {path: 'products', component: ProductListComponent},
      {path: 'products/:id', canActivate: [ProductDetailGuard], component: ProductDetailComponent},
      {path: 'welcome', component: WelcomeComponent},
      {path: '', component: WelcomeComponent, pathMatch: 'full'},
      {path: '**', component: WelcomeComponent, pathMatch: 'full'}
    ])
```

As we can see that for the path **products/:id** , paramater is id.

Next step on the routerLink definition, pass the variable that is going to **pass** the id value.

```html
<td><a [routerLink]="['/products',product.productId]">{{product.productName}}</a></td>
```

**product.productId** is the additional field passed to get the id from the route.

#### Reading the parameter value

You can read the parameter using the ActivatedRoute module.

```typescript
import { ActivatedRoute, Router } from '@angular/router';
export class ProductDetailComponent implements OnInit {
...
...
  ngOnInit() {
      const id = +this.route.snapshot.paramMap.get('id');
  }
}
```
There are two ways are reading the parameter. 
1. Using snapshot
2. Using observables

### Activate a Route with Code
1. Use the Router Service
  * Import the service
  * Define it as dependency
2. Create a method that calls the navigate method of the router service
  * Pass in the link parameters array
3. Add a user interface element
  * Use event binding to bind to the created method
  
### Protecting Routes with Guards

1. Buld a guard service
  * Implement the gaurd type (CanActivate)
  * Create the method (CanActivate())
2. Rgister the gaurd service provider
  * Use the providedIn property
3. Add the gaurd to the desired route.
