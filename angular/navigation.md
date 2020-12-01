---
title: Routing & Navigation
parent: Angular
has_children: true
nav_order: 1
has_toc: false
---

# Routing & Navigation
## Pass param in the url and hide it when page loaded
_origin.component.ts_
```javascript 
 this.router.navigate(['/contact-form/thankYou'], { queryParams: { id: id } });
```
_destination.component.ts_
```javascript
if (this.location.path().includes('?')) {
  this.location.go(this.location.path().substring(0, this.location.path().indexOf('?')));
}
```

## Remove query params
```javascript 
this.router.navigate([], {
  queryParams: {
    'yourParamName': null,
    'youCanRemoveMultiple': null,
  },
  queryParamsHandling: 'merge'
};
```

## Showing spinner until page fully loaded
_app.component.ts_
``` javascript
export class AppComponent {
  showLoadingIndicator = true;
  
  constructor( private router: Router ) {
    this.router.events.subscribe((routerEvent: Event) => {
      if(routerEvent instanceof NavigationStart) {
        this.showLoadingIndicator = true;
      }
      
      if(routerEvent instanceof NavigationEnd ||
         routerEvent instanceof NaviagtionError ||
         routerEvent instanceod NavigationCancel) {
        this.showLoadingIndicator = false;   
      }
    });
  }
}
``` 

_app.component.html_
``` html
<div *ngIf="showLoadingIndicator" class="spinner"></div>
```
