---
title: Routing & Navigation
parent: Angular
has_children: true
nav_order: 1
---

# Routing & Navigation
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
