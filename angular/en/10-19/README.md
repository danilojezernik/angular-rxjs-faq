## 10. Explain dependency injection in Angular.

Dependency Injection (DI) is a design pattern used in Angular to achieve Inversion of Control (IoC) between classes and
their dependencies. It allows for better code modularity, testability, and manageability. In Angular, DI is used to
provide components with the services or objects they need, without having to create those services or objects
themselves.

### Key Concepts of Dependency Injection

1. **Injector**:

The injector is responsible for creating service instances and injecting them into components and other services.
Angular has a hierarchical injector system, meaning child injectors can inherit and override services provided by parent
injectors.

2. **Provider**:

A provider is a way to tell the injector how to create a service. Angular uses different types of providers
like `ClassProvider`, `ValueProvider`, `FactoryProvider`, and `ExistingProvider` to create services.

3. **Token**:

A token is a unique identifier for a service. In most cases, the token is the service class itself.

4. **Service**:

A service is a class that encapsulates shared functionality and is intended to be used by multiple parts of an
application.

5. **Decorator**:

Angular uses decorators like `@Injectable`, `@Component`, and `@NgModule` to define metadata that Angular's DI system
uses to determine how to create and inject dependencies.

### How Dependency Injection Works in Angular

1. Registering a Service:

- Services can be registered at different levels in Angular:
    - Root Level: Using providedIn: 'root' in the @Injectable decorator.
    - Module Level: Using the providers array in an @NgModule.
    - Component Level: Using the providers array in an @Component.

2. Injecting a Service:

- Services are injected into components or other services via constructor parameters.
- Angular's DI framework resolves dependencies and injects the required service instances.

### Benefits of Dependency Injection

1. **Modularity**: Dependencies are declared explicitly, making it easier to manage and understand module boundaries.
2. **Testability**: Services can be mocked or stubbed during unit testing, allowing for isolated testing of components.
3. **Maintainability**: Changing a service implementation is easier as you only need to change the service itself, not
   all the places where it is used.
4. **Reusability**: Services can be reused across different parts of the application, promoting code reuse.

Dependency Injection in Angular is a powerful design pattern that allows for better code organization, testability, and
maintainability. It decouples the creation of services from their consumption, enabling a more modular and flexible
application architecture. Angular's DI system is hierarchical and provides various ways to register and inject
dependencies, making it a core feature of the framework.

## 11. What is an Angular directive? Differentiate between structural and attribute directives.

An Angular directive is a class that can modify the structure of the DOM or the appearance and behavior of a DOM
element. Directives are a core feature of Angular and allow developers to extend the HTML vocabulary and build dynamic
and interactive web applications.

### Types of Directives

Angular provides three main types of directives:

1. Component Directives:
    - Description: These are the most common directives, defined using the @Component decorator. Components are
      essentially directives with templates.
    - Example:
      ```typescript
      @Component({
        selector: 'app-example',
        template: '<h1>Example Component</h1>'
      })
      export class ExampleComponent {}
      ```

2. Structural Directives:
    - Description: These directives change the structure of the DOM by adding or removing elements.
    - Common Examples: `*ngIf`, `*ngFor`, `*ngSwitch`
3. Attribute Directives:
    - Description: These directives change the appearance or behavior of an existing DOM element or component.
    - Common Examples: `ngClass`, `ngStyle`, custom attribute directives

### Differentiating Between Structural and Attribute Directives

### Structural Directives

- **Purpose**: Structural directives alter the layout of the DOM by adding, removing, or manipulating elements.
- **Prefix**: They typically have a * prefix when used in templates.
- **Functionality**: They can conditionally add or remove elements from the DOM.
- **Examples**:
    - `*ngIf`: Adds or removes an element based on a Boolean condition.
        ```html
        <div *ngIf="isVisible">Content is visible</div>
        ```
    - `*ngFor`: Repeats an element for each item in a collection.
        ```html
        <div *ngFor="let item of items">{{ item }}</div>
        ```
    - `*ngSwitch`: Switches between alternative views based on a condition.
        ```html
        <div [ngSwitch]="viewMode">
          <ng-template *ngSwitchCase="'map'">Map View</ng-template>
          <ng-template *ngSwitchCase="'list'">List View</ng-template>
          <ng-template *ngSwitchDefault>Default View</ng-template>
        </div>
        ```

### Attribute Directives

- **Purpose**: Attribute directives modify the behavior or appearance of an existing element.
- **Prefix**: They do not use a * prefix.
- **Functionality**: They can change styles, classes, or the properties of elements.

**Examples**:

### `ngClass`

is an Angular directive used to dynamically add or remove CSS classes on an HTML element based on certain conditions or
expressions. This allows you to apply different styles to elements depending on the state of your application.

```html

<div [ngClass]="{ 'active': isActive, 'disabled': isDisabled }">Content</div>
```

**Explanation**

- **isActive**: A boolean property in your component. If isActive is true, the active class will be applied to the div.
- **isDisabled**: Another boolean property. If isDisabled is true, the disabled class will be applied to the div.

**Example Component:**

```typescript
                // app.component.ts
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: [ './app.component.css' ]
})
export class AppComponent {
    isActive: boolean = true;
    isDisabled: boolean = false;
}
```

**CSS:**

```css
/* app.component.css */
.active {
    background-color: green;
    color: white;
}

.disabled {
    background-color: gray;
    color: darkgray;
}
```

In this example, when isActive is true, the div will have a green background with white text. If isDisabled is true, the
div will have a gray background with dark gray text.

### `ngStyle`

Is an Angular directive that allows you to set inline styles for an HTML element dynamically based on expressions. This
is useful for applying styles that are computed or based on dynamic values.

```html

<div [ngStyle]="{ 'color': textColor, 'font-size': fontSize }">Styled Content</div>
```

**Explanation**

- `textColor`: A string property in your component that holds a color value.
- `fontSize`: Another string property that holds a font size value.

**Example Component:**

```typescript
// app.component.ts
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: [ './app.component.css' ]
})
export class AppComponent {
    textColor: string = 'blue';
    fontSize: string = '20px';
}
```

#### Combining `ngClass` and `ngStyle`

You can use both ngClass and ngStyle together to apply dynamic classes and styles to an element.

**Example usage:**

```html
<!-- HTML Template -->
<div
        [ngClass]="{ 'active': isActive, 'disabled': isDisabled }"
        [ngStyle]="{ 'color': textColor, 'font-size': fontSize }">
    Styled and Classed Content
</div>
```

**Example Component:**

```typescript
// app.component.ts
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: [ './app.component.css' ]
})
export class AppComponent {
    isActive: boolean = true;
    isDisabled: boolean = false;
    textColor: string = 'blue';
    fontSize: string = '20px';
}
```

**CSS:**

```css
/* app.component.css */
.active {
    background-color: green;
    color: white;
}

.disabled {
    background-color: gray;
    color: darkgray;
}
```

In this combined example, the div will have the blue text with a font size of 20 pixels, and if isActive is true, it
will have a green background with white text. If isDisabled is true, it will have a gray background with dark gray text.

### Custom Attribute Directive:

- **Description**: Change the appearance or behavior of an element.

**Example**: Highlight Directive

```typescript
import { Directive, ElementRef, HostListener } from '@angular/core';

@Directive({
    selector: '[appHighlight]'
})
export class HighlightDirective {
    constructor(private el: ElementRef) {
    }

    @HostListener('mouseenter') onMouseEnter() {
        this.highlight('yellow');
    }

    @HostListener('mouseleave') onMouseLeave() {
        this.highlight(null);
    }

    private highlight(color: string) {
        this.el.nativeElement.style.backgroundColor = color;
    }
}
```

**Usage:**

```html
<p appHighlight>Highlight me!</p>
```

### Summary

- **Structural Directives**: Modify the DOM structure by adding or removing elements. Examples include *ngIf, *ngFor,
  and *ngSwitch.
- **Attribute Directives**: Change the behavior or appearance of existing elements. Examples include ngClass, ngStyle,
  and custom directives like the Highlight Directive.

Understanding the difference between these directives is essential for effectively manipulating the DOM and enhancing
the interactivity and appearance of Angular applications.

## 12. What are Angular pipes, and how do you use them? How do you create a custom pipe in Angular? How do you implement a custom pipe that accepts multiple parameters?

Angular pipes are a feature in Angular that allows you to transform data in your templates. Pipes are used to format
strings, currency amounts, dates, and other display data. Angular comes with several built-in pipes, such
as `DatePipe`, `UpperCasePipe`, `LowerCasePipe`, `CurrencyPipe`, and `PercentPipe`.

### Usage of Built-in Pipes.

To use a pipe, you apply it within the double curly braces `{{ }}` in your template, using pipe operator `|`

#### Example:

```html
<p>{{ currentDate | date:'short' }}</p>
<p>{{ amount | currency:'USD' }}</p>
<p>{{ message | uppercase }}</p>
```

### Creating a Costume Pipe

To create a custom pipe in Angular, you need to do the following:

1. Generate a Pipe: You can generate a pipe using Angular CLI with the command `ng generate pipe pipeName`. With this
   command you will also update your module.
2. Define the Pipe: Implement the Pipe in the generated file

#### Example:

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
    name: 'exponentialStrength'
})
export class ExponentalStrengthPipe implements PipeTransform {
    transform(value: number, exponenet: number = 1): number {
        return Math.pow(value, exponenet);
    }
}
```

3. Use the Pipe: You can use the custom pipe in your template by applying it with the pipe operator `|`.

#### Example:

```html
<p>{{ 2 | exponentialStrength: 10 }}</p> <!-- Outputs: 1024 -->
```

### Creating a Pipe with multiple parameters

To create a custom pipe that accepts multiple parameters, you define them in the transform method of your pipe class.
Parameters are passed in the template separated by colons.

#### Example:

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
    name: 'multiParam'
})
export class MultiParamPipe implements PipeTransform {
    transform(value: number, param1: number, param2: number): number {
        return value + param1 * param2;
    }
}
```

#### Usage in template:

```html
<p>{{ 5 | multiParam:2:3 }}</p> <!-- Outputs: 11 (5 + 2 * 3) -->
```

### Summary

1. **Built-in Pipes**: Use Angular's built-in pipes for common transformations.
2. **Custom Pipes**: Create custom pipes by implementing the PipeTransform interface and defining the transformation
   logic.
3. **Multiple Parameters**: Pass multiple parameters to custom pipes by defining them in the `transform` method and
   passing them in the template separated by colons.
   By leveraging pipes, you can keep your Angular templates clean and concise while applying complex data
   transformations.

## 13. How to handle errors in async pipe in Angular? How to fix null in async pipe error?

The async pipe in Angular is used to subscribe to an Observable or Promise and automatically handle the subscription and
unsubscription. However, handling errors in the async pipe can be a bit tricky because the async pipe doesn't provide a
direct way to handle errors within the template. Here are a few strategies to handle errors when using the async pipe:

### 1. Using RxJS `catchError` Operator:

One common approach is to handle errors in the component class using RxJS operators such as `catchError`.

#### Example:

```typescript
import { Component } from '@angular/core';
import { Observable, of } from 'rxjs';
import { catchError } from 'rxjs/operators';
import { DataService } from './data.service';

@Component({
    selector: 'app-my-component',
    template: `
    <ng-container *ngIf="data$ | async as data; else errorTpl">
      <!-- Template when data is available -->
      <p>{{ data }}</p>
    </ng-container>
    <ng-template #errorTpl>
      <!-- Template when an error occurs -->
      <p>Error loading data</p>
    </ng-template>
  `
})
export class MyComponent {

    constructor(private dataService: DataService) {
    }

    data$: Observable<any> = this.dataService.getData().pipe(
        catchError(error => {
            // Handle error and return a fallback value or empty observable
            console.error(error);
            return of(null); // or return an observable with a fallback value
        })
    );

}
```

### 2. Using a service for error handling:

You can create a service that handles errors and provides a fallback observable.

#### Example:

```typescript
import { Injectable } from '@angular/core';
import { Observable, of } from 'rxjs';
import { catchError } from 'rxjs/operators';
import { HttpClient } from '@angular/common/http';

@Injectable({
    providedIn: 'root'
})
export class DataService {
    constructor(private http: HttpClient) {
    }

    getData(): Observable<any> {
        return this.http.get('/api/data').pipe(
            catchError(error => {
                console.error('Error occurred:', error);
                return of('Fallback data'); // Fallback data
            })
        );
    }
}
```

### Fixing `null` in Async Pipe Error

The `null` error typically occurs when the observable returns a `null` or `undefined` value. You can handle this by
ensuring your observables always return a defined value and by using Angular's template syntax to handle
potential `null` values gracefully.

#### 1. Using default values

Ensure your observable never returns `null` by providing a default value:

```typescript
import { Injectable } from '@angular/core';
import { Observable, of } from 'rxjs';
import { map } from 'rxjs/operators';
import { HttpClient } from '@angular/common/http';

@Injectable({
    providedIn: 'root'
})
export class DataService {
    constructor(private http: HttpClient) {
    }

    getData(): Observable<any> {
        return this.http.get('/api/data').pipe(
            map(data => data || 'Default value') // Provide a default value
        );
    }
}
```

#### 2. Using safe navigation operator in template

Use Angular's safe navigation operator (`?.`) in the template to handle `null` or `undefined` values in the template:

```html
<p>{{ data$ | async | json }}</p>
<p>{{ (data$ | async)?.property }}</p>
```

### Example Combining Both

#### Component:

```typescript
import { Component, OnInit } from '@angular/core';
import { Observable, of } from 'rxjs';
import { catchError } from 'rxjs/operators';
import { DataService } from './data.service';

@Component({
    selector: 'app-my-component',
    template: `
    <ng-container *ngIf="data$ | async as data; else errorTpl">
      <p>{{ data }}</p>
    </ng-container>
    <ng-template #errorTpl>
      <p>Error loading data or no data available</p>
    </ng-template>
  `
})
export class MyComponent implements OnInit {
    data$: Observable<any>;

    constructor(private dataService: DataService) {
    }

    ngOnInit() {
        this.data$ = this.dataService.getData().pipe(
            catchError(error => {
                console.error(error);
                return of('Default value'); // Fallback or default value
            })
        );
    }
}
```

By handling errors in the service or component and using default values, you can prevent `null` errors and provide a
better user experience.

## 14. What is Angular routing? How do you set up routing in an Angular application?

Angular routing is a feature of the Angular framework that allows developers to navigate between different views or
pages within a single-page application (SPA). Routing is essential for creating a seamless user experience by enabling
dynamic view rendering based on the application's URL. It helps in managing the state of the application and can load
components, modules, or data dynamically.

### Setting Up Routing in an Angular Application

Setting up routing in an Angular application involves several steps, including configuring the routes, importing the
necessary Angular modules, and defining the navigation links. Here's a step-by-step guide to setting up routing in an
Angular application:

#### 1. Generate a New Angular Application

If you don't already have an Angular application, you can create one using Angular CLI:

```bash
ng new my-angular-app
cd my-angular-app
```

#### 2. Generate Components

Generate some components that will be used in the routing:

```bash
ng generate component home
ng generate component about
ng generate component contact
```

#### 3. Define Routes

Open `app-routing.module.ts` (or create it if it doesn't exist) and define the routes. This file is typically created
automatically when you create a new Angular application with routing enabled.

Example:

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';
import { ContactComponent } from './contact/contact.component';

const routes: Routes = [
    { path: '', redirectTo: '/home', pathMatch: 'full' }, // Default route
    { path: 'home', component: HomeComponent },
    { path: 'about', component: AboutComponent },
    { path: 'contact', component: ContactComponent },
    { path: '**', redirectTo: '/home' } // Wildcard route for a 404 page
];

@NgModule({
    imports: [ RouterModule.forRoot(routes) ],
    exports: [ RouterModule ]
})
export class AppRoutingModule {
}
```

#### 4. Import the AppRoutingModule

Open `app.module.ts` and import the `

Example:

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';
import { ContactComponent } from './contact/contact.component';

@NgModule({
    declarations: [
        AppComponent,
        HomeComponent,
        AboutComponent,
        ContactComponent
    ],
    imports: [
        BrowserModule,
        AppRoutingModule
    ],
    providers: [],
    bootstrap: [ AppComponent ]
})
export class AppModule {
}
```

#### 5. Create Navigation Links

In your `app.component.html`, create navigation links to navigate between different routes:

Example:

```html

<nav>
    <a routerLink="/home">Home</a>
    <a routerLink="/about">About</a>
    <a routerLink="/contact">Contact</a>
</nav>
<router-outlet></router-outlet>
```

- `routerLink`: This directive is used to link to different routes defined in the routing module.
- `<router-outlet>`: This directive acts as a placeholder where the routed component will be displayed.

#### 6. Add Router Module and Configuration

Ensure that `AppRoutingModule` is correctly imported and configured in your `app.module.ts`.

### Summary

1. **Generate an Angular Application**: Use Angular CLI to generate a new application.
2. **Generate Components**: Create the components that will be navigated between.
3. **Define Routes**: Set up routes in `app-routing.module.ts`.
4. **Import AppRoutingModule**: Import and configure the routing module in `app.module.ts`.
5. **Create Navigation Links**: Use routerLink and `<router-outlet>` in your template to navigate and display routed
   components.

By following these steps, you can set up routing in your Angular application, enabling seamless navigation between
different components and views.

## 15. What is a guard in Angular routing, and how do you implement it?

In Angular, a guard is a feature used to control access to routes in an application. Guards are implemented as services
that can be added to route configurations to determine whether a user can activate a route, deactivate a route, load a
module, or unload a module. Angular provides several types of guards:

1. **CanActivate**: Determines if a route can be activated.
2. **CanActivateChild**: Determines if child routes can be activated.
3. **CanDeactivate**: Determines if a route can be deactivated.
4. **Resolve**: Pre-fetches data before activating a route.
5. **CanLoad**: Determines if a module can be loaded.

### Implementing a guard in Angular

Let's implement a `CaActivate` guard to control access to a route based on a condition, such as whether a user is
authenticated.

#### Step-by-Step implementation

1. **Generate a Guard**

Use Angular CLI to generate a new guard:

```bash
ng generate guard auth
```

This command creates a new file named `auth.guard.ts` in the `src/app` directory.

2. **Implement the Guard logic**

Open the generated auth.guard.ts file and implement the logic. In this example, we'll use a simple authentication
service to check if a user is logged in.

**Example**:

```typescript
import { Injectable } from '@angular/core';
import { ActivatedRouteSnapshot, CanActivate, Router, RouterStateSnapshot, UrlTree } from '@angular/router';
import { Observable } from 'rxjs';
import { AuthService } from './auth.service';

@Injectable({
    providedIn: 'root'
})
export class AuthGuard implements CanActivate {

    constructor(private authService: AuthService, private router: Router) {
    }

    canActivate(
        next: ActivatedRouteSnapshot,
        state: RouterStateSnapshot): Observable<boolean | UrlTree> | Promise<boolean | UrlTree> | boolean | UrlTree {
        if (this.authService.isLoggedIn()) {
            return true
        } else {
            this.router.navigate([ '/login' ])
            return false
        }
    }

}
```

In this example, `AuthService` is a service that contains the method `isLoggedIn()`, which checks if the user is
authenticated.

3. **Define the AuthService**

Create the `AuthService` that contains the authentication logic.

**Example**:

```typescript
import { Injectable } from '@angular/core';

@Injectable({
    providedIn: 'root'
})
export class AuthService {
    private loggedIn = false

    isLoggedIn(): boolean {
        return this.loggedIn
    }

    login() {
        this.loggedIn = true
    }

    logout() {
        this.loggedIn = false
    }
}
```

4. **Add the Guard to Routes**

Open the routing module (e.g., `app-routing.module.ts`) and add the `AuthGuard` to the route(s) you want to protect.

#### Example:

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';
import { ContactComponent } from './contact/contact.component';
import { LoginComponent } from './login/login.component';
import { AuthGuard } from './auth.guard';

const routes: Routes = [
    { path: '', redirectTo: '/home', pathMatch: 'full' },
    { path: 'home', component: HomeComponent },
    { path: 'about', component: AboutComponent },
    { path: 'contact', component: ContactComponent, canActivate: [ AuthGuard ] },
    { path: 'login', component: LoginComponent },
    { path: '**', redirectTo: '/home' }
];

@NgModule({
    imports: [ RouterModule.forRoot(routes) ],
    exports: [ RouterModule ]
})
export class AppRoutingModule {
}
```

In this configuration, the `ContactComponent` route is protected by the `AuthGuard`. If the user is not logged in, they
will be redirected to the `/login` route.

### Summary

1. **Generate a Guard**: Use Angular CLI to generate a guard.
2. **Implement the Guard Logic**: Define the logic to control route access in the guard.
3. **Create an AuthService**: Implement the authentication service that the guard will use.
4. **Add the Guard to Routes**: Apply the guard to the routes you want to protect in the routing module.

By implementing guards, you can control access to various parts of your Angular application based on custom logic, such
as user authentication or authorization.

## 16. What are Angular forms? Differentiate between template-driven and reactive forms in Angular and how do you do a basic validation.

Angular forms are a fundamental part of the Angular framework, used for capturing user input, validating it, and taking
appropriate actions based on the user’s data. Angular provides two approaches for handling forms: template-driven forms
and reactive forms. Both approaches serve the same purpose but offer different ways of handling and managing forms in an
application.

### Template-Driven Forms

Template-driven forms rely on Angular's data-binding and directives to handle form creation, validation, and data
management within the template. They are suitable for simpler use cases where forms are not very complex.

#### Characteristics of Template-Driven Forms

1. **Declarative Approach**: Forms are created using HTML with Angular directives.
2. **Two-Way Data Binding**: Uses `[(ngModel)]` for two-way data binding.
3. **Asynchronous Validation**: Validators are defined using directives in the template.
4. **Less Boilerplate Code**: Minimal TypeScript code is required, making it easier to implement.
5. **Simplicity**: Best for simpler forms where complex validation logic is not needed.

**Example of Template-Driven Form**

#### Template (HTML):

```html

<form #myForm="ngForm" (ngSubmit)="onSubmit(myForm)">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" ngModel required>

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" ngModel required email>

    <button type="submit" [disabled]="!myForm.valid">Submit</button>
</form>
```

#### Component (Typescript):

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-template-form',
    templateUrl: './template-form.component.html'
})
export class TemplateFormComponent {
    onSubmit(form: any) {
        console.log('Form Submitted!', form);
    }
}
```

### Reactive Forms

Reactive forms, also known as model-driven forms, provide a more structured approach to handling forms by defining the
form model explicitly in the component. This approach is suitable for complex forms with intricate validation logic.

#### Characteristics of Reactive Forms

1. **Programmatic Approach**: Forms are created and managed in the component class.
2. **FormControl and FormGroup**: Uses `FormControl` and `FormGroup` classes to manage form inputs and their state.
3. **Synchronous Validation**: Validators are defined as functions in the component class.
4. **More Control**: Provides more control over form handling, validation, and reactive changes.
5. **Scalability**: Better suited for complex and large-scale forms.

#### Example of Reactive Form

#### Component (TypeScript):

```typescript
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormControl, Validators } from '@angular/forms';

@Component({
    selector: 'app-reactive-form',
    templateUrl: './reactive-form.component.html'
})
export class ReactiveFormComponent implements OnInit {
    myForm: FormGroup;

    ngOnInit() {
        this.myForm = new FormGroup({
            name: new FormControl('', Validators.required),
            email: new FormControl('', [ Validators.required, Validators.email ])
        });
    }

    onSubmit() {
        console.log('Form Submitted!', this.myForm.value);
    }
}
```

#### Template (HTML):

```html

<form [formGroup]="myForm" (ngSubmit)="onSubmit()">
    <label for="name">Name:</label>
    <input type="text" id="name" formControlName="name">
    <div *ngIf="myForm.get('name')!.invalid && myForm.get('name')!.touched">
        Name is required
    </div>

    <label for="email">Email:</label>
    <input type="email" id="email" formControlName="email">
    <div *ngIf="myForm.get('email')!.invalid && myForm.get('email')!.touched">
        Enter a valid email
    </div>

    <button type="submit" [disabled]="myForm.invalid">Submit</button>
</form>
```

**Note**: There is a non-null assertion operator `!` used in the template due to the TypeScript strict null checks. So
you are basically tell TypeScript that `get('name')` will not be null before accessing their properties.

#### Differences Between Template-Driven and Reactive Forms

| Feature                     | Template-Driven Forms                    | Reactive Forms                           |
|-----------------------------|------------------------------------------|------------------------------------------|
| Approach                    | Declarative (HTML-based)                 | Programmatic (TypeScript-based)          |
| Data Binding                | Two-way data binding using `[(ngModel)]` | Explicit and immutable data binding      |
| Form Model                  | Defined implicitly by directives         | Defined explicitly in component class    |
| Validation                  | Asynchronous, defined in templates       | Synchronous, defined in component class  |
| Control over Form Structure | Less control, suitable for simpler forms | More control, suitable for complex forms |
| Boilerplate Code            | Less boilerplate code                    | More boilerplate code, but more robust   |
| Change Detection Strategy   | Angular change detection                 | Reactive, observable-based               |

### When to Use Which Approach

- **Template-Driven Forms**: Use when you have simple forms and want to leverage Angular's data-binding with minimal
  TypeScript code.
- **Reactive Forms**: Use when dealing with complex forms, custom validation logic, or if you need more control over the
  form's behavior and structure.

By understanding the differences and characteristics of both template-driven and reactive forms, you can choose the
appropriate approach for your specific use case in Angular applications.

## 17. What are the all the validation options for forms in angular and how to do a custom validators?

### Template-Driven Validators

Template-driven forms rely on Angular's directives to handle validation directly within the HTML template.

#### Common Validators

1. Required Validator

```html
<input type="text" name="name" ngModel required>
```

2. Minimum Length Validator

```html
<input type="text" name="name" ngModel minlength="3">
```

3. Maximum Length Validator

```html
<input type="text" name="name" ngModel maxlength="20">
```

4. Pattern Validator

```html
<input type="text" name="name" ngModel pattern="[a-zA-Z ]*">
```

5. Email Validator

```html
<input type="email" name="email" ngModel required email>
```

#### Example

In the template-driven form example using `ngModel`, the `myForm.controls['name']` and `myForm.controls['email']` are
checked
with the optional chaining operator `?.`. This ensures that if `controls['name']` or `controls['email']` is `null`
or `undefined`,
it does not throw an error and instead safely returns undefined. This way, TypeScript does not raise any issues because
it knows that the expression can handle `null` or `undefined` values.

#### Template (HTML):

```html

<form #myForm="ngForm" (ngSubmit)="onSubmit(myForm)">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" ngModel required minlength="3" maxlength="20">
    <div *ngIf="myForm.controls['name']?.invalid && myForm.controls['name']?.touched">
        <div *ngIf="myForm.controls['name']?.errors?.['required']">Name is required.</div>
        <div *ngIf="myForm.controls['name']?.errors?.['minlength']">Name must be at least 3 characters long.</div>
        <div *ngIf="myForm.controls['name']?.errors?.['maxlength']">Name cannot be more than 20 characters long.</div>
    </div>

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" ngModel required email>
    <div *ngIf="myForm.controls['email']?.invalid && myForm.controls['email']?.touched">
        <div *ngIf="myForm.controls['email']?.errors?.['required']">Email is required.</div>
        <div *ngIf="myForm.controls['email']?.errors?.['email']">Enter a valid email.</div>
    </div>

    <button type="submit" [disabled]="myForm.invalid">Submit</button>
</form>
```

#### Component (TypeScript):

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-template-form',
    templateUrl: './template-form.component.html'
})
export class TemplateFormComponent {
    onSubmit(form: any) {
        console.log('Form Submitted!', form.value);
    }
}
```

### Reactive Form Validation

Reactive forms use explicit form model management in the component class. This approach is suitable for more complex
forms and provides greater control over form validation.

#### Common Validators

1. Required Validator

```typescript
Validators.required
``` 

2. Minimum Length Validator

```typescript
Validators.minLength(minLength)
```

3. Maximum Length Validator

```typescript
Validators.maxLength(maxLength)
```

4. Pattern Validator

```typescript
Validators.pattern('[a-zA-Z ]*')
```

5. Email Validator

```typescript
Validators.email
```

#### Example

In the reactive form example, TypeScript enforces stricter null checks and does not assume that `get('name')`
or `get('email')` will always return a valid form control. As a result, you need to use the non-null assertion
operator `!` to assert that these controls are not null.

#### Component (TypeScript):

```typescript
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormControl, Validators } from '@angular/forms';

@Component({
    selector: 'app-reactive-form',
    templateUrl: './reactive-form.component.html'
})
export class ReactiveFormComponent implements OnInit {
    myForm!: FormGroup;

    ngOnInit() {
        this.myForm = new FormGroup({
            name: new FormControl('', [ Validators.required, Validators.minLength(3), Validators.maxLength(20) ]),
            email: new FormControl('', [ Validators.required, Validators.email ])
        });
    }

    onSubmit() {
        console.log('Form Submitted!', this.myForm.value);
    }
}
```

#### Template (HTML):

```html

<form [formGroup]="myForm" (ngSubmit)="onSubmit()">
    <label for="name">Name:</label>
    <input type="text" id="name" formControlName="name">
    <div *ngIf="myForm.get('name')!.invalid && myForm.get('name')!.touched">
        <div *ngIf="myForm.get('name')!.errors?.['required']">Name is required.</div>
        <div *ngIf="myForm.get('name')!.errors?.['minlength']">Name must be at least 3 characters long.</div>
        <div *ngIf="myForm.get('name')!.errors?.['maxlength']">Name cannot be more than 20 characters long.</div>
    </div>

    <label for="email">Email:</label>
    <input type="email" id="email" formControlName="email">
    <div *ngIf="myForm.get('email')!.invalid && myForm.get('email')!.touched">
        <div *ngIf="myForm.get('email')!.errors?.['required']">Email is required.</div>
        <div *ngIf="myForm.get('email')!.errors?.['email']">Enter a valid email.</div>
    </div>

    <button type="submit" [disabled]="myForm.invalid">Submit</button>
</form>
```

### Custom Validators

Custom validators can be created for both template-driven and reactive forms to handle specific validation logic.

### Synchronous Custom Validator

#### Example: Forbidden Name Validator

1. Create the Validator Function:

```typescript
import { AbstractControl, ValidationErrors, ValidatorFn } from '@angular/forms';

export function forbiddenNameValidator(nameRe: RegExp): ValidatorFn {
    return (control: AbstractControl): ValidationErrors | null => {
        const forbidden = nameRe.test(control.value);
        return forbidden ? { forbiddenName: { value: control.value } } : null;
    };
}
```

2. Use the Custom Validator in Reactive Forms:

```typescript
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormControl, Validators } from '@angular/forms';
import { forbiddenNameValidator } from './forbidden-name.validator';

@Component({
    selector: 'app-reactive-form',
    templateUrl: './reactive-form.component.html'
})
export class ReactiveFormComponent implements OnInit {
    myForm!: FormGroup;

    ngOnInit() {
        this.myForm = new FormGroup({
            name: new FormControl('', [ Validators.required, Validators.minLength(3), Validators.maxLength(20), forbiddenNameValidator(/bob/i) ]),
            email: new FormControl('', [ Validators.required, Validators.email ])
        });
    }

    onSubmit() {
        console.log('Form Submitted!', this.myForm.value);
    }
}
```

Template (HTML):

```html

<form [formGroup]="myForm" (ngSubmit)="onSubmit()">
    <label for="name">Name:</label>
    <input type="text" id="name" formControlName="name">
    <div *ngIf="myForm.get('name')!.invalid && myForm.get('name')!.touched">
        <div *ngIf="myForm.get('name')!.errors?.['required']">Name is required.</div>
        <div *ngIf="myForm.get('name')!.errors?.['minlength']">Name must be at least 3 characters long.</div>
        <div *ngIf="myForm.get('name')!.errors?.['maxlength']">Name cannot be more than 20 characters long.</div>
        <div *ngIf="myForm.get('name')!.errors?.['forbiddenName']">Name "bob" is forbidden.</div>
    </div>

    <label for="email">Email:</label>
    <input type="email" id="email" formControlName="email">
    <div *ngIf="myForm.get('email')!.invalid && myForm.get('email')!.touched">
        <div *ngIf="myForm.get('email')!.errors?.['required']">Email is required.</div>
        <div *ngIf="myForm.get('email')!.errors?.['email']">Enter a valid email.</div>
    </div>

    <button type="submit" [disabled]="myForm.invalid">Submit</button>
</form>
```

### Asynchronous Custom Validator

#### Example: Unique Username Validator

1. Create the Validator Function:

```typescript
import { AbstractControl, ValidationErrors } from '@angular/forms'; // Import necessary types from Angular forms
import { Observable, of } from 'rxjs'; // Import Observable and 'of' function from RxJS
import { delay, map } from 'rxjs/operators'; // Import delay and map operators from RxJS

// Define a custom validator function to check for unique usernames
export function uniqueUsernameValidator(existingUsernames: string[]): (control: AbstractControl) => Observable<ValidationErrors | null> {
    // The function returns another function that takes an AbstractControl and returns an Observable of ValidationErrors or null
    return (control: AbstractControl): Observable<ValidationErrors | null> => {
        // Create an observable from the existing usernames array
        return of(existingUsernames).pipe(
            delay(1000), // Simulate a server delay of 1000ms (1 second)
            map(usernames => {
                // Check if the control's value is in the existing usernames array
                const isUnique = !usernames.includes(control.value);
                // If the username is unique, return null (no error)
                // If the username is not unique, return a validation error object
                return isUnique ? null : { uniqueUsername: { value: control.value } };
            })
        );
    };
}

```

2. Use the Custom Validator in Reactive Forms:

```typescript
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormControl, Validators } from '@angular/forms'; // Import necessary Angular form classes and validators
import { uniqueUsernameValidator } from './unique-username.validator'; // Import the custom validator

@Component({
    selector: 'app-reactive-form',
    templateUrl: './reactive-form.component.html' // Path to the component's template file
})
export class ReactiveFormComponent implements OnInit {
    myForm!: FormGroup; // Declare a FormGroup property to manage the form
    existingUsernames = [ 'john', 'jane', 'admin' ]; // Define an array of existing usernames for validation

    // Initialize the form group and controls when the component initializes
    ngOnInit() {
        this.myForm = new FormGroup({
            username: new FormControl('', {
                validators: [ Validators.required ], // Add a required validator to the username field
                asyncValidators: [ uniqueUsernameValidator(this.existingUsernames) ], // Add the custom async validator for unique username
                updateOn: 'blur' // Run async validation when the input field loses focus
            }),
            email: new FormControl('', [ Validators.required, Validators.email ]) // Add required and email validators to the email field
        });
    }

    // Function to handle form submission
    onSubmit() {
        // Log the form's value to the console if the form is submitted
        console.log('Form Submitted!', this.myForm.value);
    }
}

```

#### Template (HTML):

```html

<form [formGroup]="myForm" (ngSubmit)="onSubmit()">
    <label for="username">Username:</label>
    <input type="text" id="username" formControlName="username">
    <div *ngIf="myForm.get('username')!.invalid && myForm.get('username')!.touched">
        <div *ngIf="myForm.get('username')!.errors?.['required']">Username is required.</div>
        <div *ngIf="myForm.get('username')!.errors?.['uniqueUsername']">This username is already taken.</div>
    </div>

    <label for="email">Email:</label>
    <input type="email" id="email" formControlName="email">
    <div *ngIf="myForm.get('email')!.invalid && myForm.get('email')!.touched">
        <div *ngIf="myForm.get('email')!.errors?.['required']">Email is required.</div>
        <div *ngIf="myForm.get('email')!.errors?.['email']">Enter a valid email.</div>
    </div>

    <button type="submit" [disabled]="myForm.invalid">Submit</button>
</form>
```

#### Summary

- **Template-Driven Forms**: Use Angular directives `(ngModel)` and handle null/undefined values with the optional
  chaining operator `?.`. This ensures that any attempt to access properties on potentially undefined objects does not
  result in an error.
- **Reactive Forms**: Use explicit form model management (`FormGroup`, `FormControl`) and require the non-null assertion
  operator `!` to assure TypeScript that form controls are not null. This informs TypeScript that the value will not be
  null, preventing runtime errors and ensuring type safety.
- **Custom Validators**: Create both synchronous and asynchronous custom validators to handle specific validation logic.
  Implement custom validation logic and use it in reactive forms to enhance form validation capabilities.

## 18. What is Angular Universal? Explain the concept of server-side rendering in Angular.

Angular Universal is a technology that enables server-side rendering (SSR) for Angular applications. It allows Angular
applications to be rendered on the server instead of the client’s browser, which can improve performance, search engine
optimization (SEO), and accessibility.

### Concept of Server-Side Rendering (SSR) in Angular

Server-side rendering (SSR) is a technique where the HTML for a web page is generated on the server instead of in the
client’s browser. This pre-rendered HTML is then sent to the client, allowing the page to be displayed more quickly. In
the context of Angular, SSR involves rendering the Angular application on the server and then sending the generated HTML
to the client.

#### Benefits of Server-Side Rendering

1. **Improved Performance**:
    - Faster initial page load times because the HTML is pre-rendered on the server.
    - Reduced time to first meaningful paint, as the browser can display content immediately.


2. **Better SEO**:
    - Search engines can easily index the pre-rendered HTML content, improving the website's search engine ranking.
    - Web crawlers from search engines that have difficulty executing JavaScript can still read the content.


3. **Enhanced Accessibility**:
    - Users with slow internet connections or older devices can see the content faster.
    - Users who disable JavaScript can still access the content.

### How Angular Universal Works

Angular Universal works by using a server-side platform, such as Node.js, to render Angular applications. Here’s a
high-level overview of how it works:

1. Server-Side Rendering:
    - The Angular application runs on the server using a platform like Node.js.
    - When a request is made to the server, the Angular application renders the requested page to HTML.
    - The server sends this pre-rendered HTML to the client.

2. Client-Side Bootstrapping:
    - Once the pre-rendered HTML is loaded in the browser, Angular takes over and bootstraps the client-side
      application.
    - This process is known as "hydration" and it involves attaching event listeners and making the application
      interactive.

### Setting Up Angular Universal

To set up Angular Universal in your Angular application, follow these steps:

1. **Install Angular Universal**: Use Angular CLI to add Angular Universal to your project.

```bash
ng add @nguniversal/express-engine
```

2. **Update Server-Side Code**: This command will create several files and update your project configuration. Key files
   include:
    - `server.ts`: The main server-side entry point.
    - `app.server.module.ts`: The server-side application module.

3. **Configure Angular Universal**: The `ng add @nguniversal/express-engine` command automatically configures your
   application for SSR. However, you might need to update some configuration settings or make adjustments based on your
   application’s requirements.

4. Build and Serve the Application:
    - Build the client and server bundles using Angular CLI.
   ```bash
   npm run build:ssr
   ```
    - Serve the application using the server bundle.
    ```bash
    npm run serve:ssr
    ```

### Example of Server-Side Rendering

Here’s a simplified example of how Angular Universal sets up SSR:

1. `app.server.module.ts`: This module is used to bootstrap the server-side application.

```typescript
import { NgModule } from '@angular/core';
import { ServerModule } from '@angular/platform-server';
import { AppModule } from './app.module';
import { AppComponent } from './app.component';

@NgModule({
    imports: [
        AppModule,
        ServerModule,
    ],
    bootstrap: [ AppComponent ],
})
export class AppServerModule {
}
```

2. `server.ts`: The main server-side entry point.

```typescript
import 'zone.js/dist/zone-node';
import { ngExpressEngine } from '@nguniversal/express-engine';
import * as express from 'express';
import { join } from 'path';
import { APP_BASE_HREF } from '@angular/common';
import { existsSync } from 'fs';
import { AppServerModule } from './src/main.server';

const app = express();

const DIST_FOLDER = join(process.cwd(), 'dist');
const domino = require('domino');
const fs = require('fs');
const template = fs.readFileSync(join(DIST_FOLDER, 'browser', 'index.html')).toString();
const win = domino.createWindow(template);

global['window'] = win;
global['document'] = win.document;

app.engine('html', ngExpressEngine({
    bootstrap: AppServerModule,
}));

app.set('view engine', 'html');
app.set('views', join(DIST_FOLDER, 'browser'));

app.get('*.*', express.static(join(DIST_FOLDER, 'browser')));

app.get('*', (req, res) => {
    res.render('index', { req, providers: [ { provide: APP_BASE_HREF, useValue: req.baseUrl } ] });
});

const PORT = process.env.PORT || 4000;

app.listen(PORT, () => {
    console.log(`Node Express server listening on http://localhost:${PORT}`);
});
```

#### Summary

- Angular Universal enables server-side rendering (SSR) for Angular applications.
- Server-Side Rendering (SSR) improves performance, SEO, and accessibility by rendering the Angular application on the
  server and sending pre-rendered HTML to the client.
- Benefits include faster initial page loads, better search engine indexing, and enhanced accessibility for users with
  slower connections or older devices.
- Setting Up Angular Universal involves installing Angular Universal, configuring the server-side code, and
  building/serving the application with SSR.
  By using Angular Universal, you can significantly enhance the performance and SEO of your Angular applications,
  providing a better user experience.

## 19. How do you handle HTTP requests in Angular? What is the HttpClientModule, and how do you use it?

In Angular, handling HTTP requests is achieved using the HttpClient service, which is part of the `@angular/common/http`
package. The `HttpClientModule` is the Angular module that needs to be imported to enable HTTP services within your
application.

### HttpClientModule

The `HttpClientModule` provides the necessary services to perform HTTP requests in an Angular application. To use it,
you need to import it into your root module (`AppModule`) or any other specific module where you plan to make HTTP
requests.

Here’s how you import and set up the `HttpClientModule`:

1. **Import HttpClientModule**: First, import the `HttpClientModule` in your `AppModule` or the respective module.

```typescript
   import { BrowserModule } from '@angular/platform-browser';

import { NgModule } from '@angular/core';
import { HttpClientModule } from '@angular/common/http';

import { AppComponent } from './app.component';

@NgModule({
    declarations: [
        AppComponent
    ],
    imports: [
        BrowserModule,
        HttpClientModule // Import HttpClientModule here
    ],
    providers: [],
    bootstrap: [ AppComponent ]
})
export class AppModule {
}
```

2. **Using HttpClient**: Once `HttpClientModule` is imported, you can inject `HttpClient` into your services or
   components to
   make HTTP requests.

### Making HTTP Requests

To make HTTP requests, follow these steps:

1. **Create a Service**: It is a best practice to handle HTTP requests within a service. Create a service using Angular
   CLI:

    ```bash
    ng generate service data
    ```
   This command will create a `data.service.ts` file.


2. Inject HttpClient into the Service: In the created service, import HttpClient and inject it through the constructor.

```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
    providedIn: 'root'
})
export class DataService {

    private apiUrl = 'https://api.example.com/data';

    constructor(private http: HttpClient) {
    }

    // Method to GET data
    getData(): Observable<any> {
        return this.http.get<any>(this.apiUrl);
    }

    // Method to POST data
    postData(data: any): Observable<any> {
        return this.http.post<any>(this.apiUrl, data);
    }

    // Method to PUT data
    updateData(id: string, data: any): Observable<any> {
        return this.http.put<any>(`${this.apiUrl}/${id}`, data);
    }

    // Method to DELETE data
    deleteData(id: string): Observable<any> {
        return this.http.delete<any>(`${this.apiUrl}/${id}`);
    }
}
```

3. Using the Service in a Component: Now, you can use the service in your components to make HTTP requests.

```typescript
import { Component, OnInit } from '@angular/core';
import { DataService } from './data.service';

@Component({
    selector: 'app-root',
    template: `
    <div *ngIf="data">
      <pre>{{ data | json }}</pre>
    </div>
  `
})
export class AppComponent implements OnInit {
    data: any;

    constructor(private dataService: DataService) {
    }

    ngOnInit(): void {
        this.dataService.getData().subscribe(response => {
            this.data = response;
        });
    }
}
```

#### Summary

- **HttpClientModule**: Import this module to use HTTP functionalities in your Angular app.
- **HttpClient**: Use this service to perform HTTP requests.
- **Service**: Create a service to handle HTTP requests, encapsulating the logic and making it reusable across
  components.
- **Component**: Inject the service into components to use the data fetched from HTTP requests.
  By following these steps, you can efficiently manage HTTP requests in your Angular application using
  the `HttpClientModule` and `HttpClient` service.