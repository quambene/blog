<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD024 -->

# Angular

- [Component](#component)
- [Module](#module)
- [Data binding](#data-binding)
  - [Text interpolation](#text-interpolation)
  - [Property binding](#property-binding)
  - [Event binding](#event-binding)
  - [Two-way binding](#two-way-binding)
  - [Attribute binding](#attribute-binding)
- [Directives](#directives)
  - [ngIf](#ngif)
  - [ngFor](#ngfor)
  - [ngSwitch](#ngswitch)
  - [ngStyle](#ngstyle)
  - [ngClass](#ngclass)
- [Services](#services)

### Component

``` typescript
import { Component } from '@angular/core';

@Component({ 
   selector: 'app-root', 
   templateUrl: './app.component.html', 
   styleUrls: ['./app.component.css'] 
})
export class AppComponent implements OnInit, OnDestroy {  
    constructor(public myService: MyService) {
        // ...
    }

    ngOnInit(): void {
        // ...
    }

    ngOnDestroy(): void {
        // ...
    }
}
```

``` html
<!doctype html>
<html lang="en">

<head>
    <meta charset="utf-8">
</head>

<body>
    <app-root></app-root>
</body>

</html>
```

### Module

``` typescript
import { BrowserModule } from '@angular/platform-browser'; 
import { NgModule } from '@angular/core'; 
import { AppComponent } from './app.component';

@NgModule({ 
   declarations: [ 
      AppComponent 
   ], 
   imports: [ 
      BrowserModule 
   ], 
   providers: [], 
   bootstrap: [AppComponent] 
})
export class AppModule { }
```

### Data binding

#### Text interpolation

``` typescript
export class MyComponent { 
   title = "My Title"; 
}
```

``` html
<h1>
    {{ title }}
</h1>

<!-- Expression -->
<p>The sum of 1 + 1 is {{1 + 1}}.</p>
```

#### Property binding

##### Pass data from component to views

``` typescript
export class MyComponent { 
   isDisabled = true;
}
```

``` html
<button type="button" [disabled]="isDisabled">Disabled Button</button>
```

##### Pass data between components

###### Child component

``` typescript
export class MyItemComponent { 
   @Input() childItem: Item;
}
```

###### Parent component

``` html
<div *ngFor="let parentItem of parentItems">
    <app-my-item [childItem]="parentItem"></app-my-item>
</div>
```

#### Event binding

##### Pass data from views to component

``` typescript
export class MyComponent {
    public myFlag = false;

    onToggle() {
        this.myFlag = !this.myFlag;
    }
}
```

``` html
<button (click)="onToggle()">My Button</button>
```

##### EventEmitter

###### Child component

``` typescript
export class MyItemComponent {
    @Input() item: Item;
    @Output() deleteItem: EventEmitter<Item> = new EventEmitter();

    delete() {
        this.deleteItem.emit(this.item);
    }
}
```

``` html
<button type="button" (click)="delete()">Delete</button>
```

###### Parent component

``` typescript
export class MyParentComponent {
    onItemDeleted(item: Item) {
        // ...
    }
}
```

``` html
<app-my-item (deleteItem)="onItemDeleted($event)" [item]="currentItem">
</app-my-item>
```

#### Two-way binding

``` html
<app-my-item [(item)]="currentItem"></app-my-item>
```

#### Attribute binding

``` html
<div [style.<cssproperty>]="myVariable"></div>
<div [style.background-color]="'blue'"></div>

<button class="btn" [class.btn-primary]="true" type="submit">My Button</button>
```

### Directives

#### ngIf

``` html
<div *ngIf="showImage">
    <img src="../assets/my-image.svg">
</div>
```

#### ngFor

``` html
<li *ngFor="let name of names">{{ name }}</li>

<li *ngFor="let notification of notifications | async">{{ notification }}</li>
```

#### ngSwitch

``` html
<div [ngSwitch]="myVariable">
    <div *ngSwitchCase="'A'">Var is A</div>
    <div *ngSwitchDefault>My default text</div>
</div>
```

#### ngStyle

``` html
<div [ngStyle]="{'margin-left.px': myVariable}"></div>
```

#### ngClass

``` html
<div [ngClass]="{bordered: myVariable}"></div>
```

### Services

``` typescript
import { Injectable } from '@angular/core';

@Injectable({
    providedIn: 'root'
})
export class MyService {
    // ...
}
```
