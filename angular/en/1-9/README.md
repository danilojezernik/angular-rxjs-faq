## 1. What is Angular, and how does it differ from AngularJS?

**Angular** is a platform and framework for building single-page client applications using HTML, CSS, and TypeScript.
Angular is developed and maintained by Google and is often referred to as Angular 2+ or simply Angular to distinguish it
from its predecessor, AngularJS.

**AngularJS**, on the other hand, is the original version of Angular, which is based on JavaScript and was released in 2010.

### Differences:

- **Language**: Angular uses TypeScript, while AngularJS uses JavaScript.
- **Architecture**: Angular has a component-based architecture, whereas AngularJS uses a scope and controller model.
- **Performance**: Angular provides better performance with improved dependency injection and change detection
  mechanisms.
- **Mobile Support**: Angular is designed with mobile support in mind, whereas AngularJS is not.
- **Tooling**: Angular comes with advanced tooling and CLI for efficient development, whereas AngularJS has more basic
  tooling.

### Example:

- **Angular (TypeScript):**

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: '<h1>Hello, Angular!</h1>',
})
export class AppComponent {
}
```

- **AngularJS (JavaScript):**

```javascript
angular.module('myApp', [])
    .controller('myController', function ($scope) {
        $scope.message = 'Hello, AngularJS!';
    });
```

## 2. Explain the architecture of an Angular application.

An Angular application is structured as a collection of modules, components, and services.

### Architecture:

- **Modules**: The fundamental building blocks. An Angular app typically has a root module and feature modules.
- **Components**: Define views using HTML templates. Every component has a TypeScript class, HTML template, and styles.
- **Templates**: Define the view and use directives and binding markup to connect the DOM with the component.
- **Services**: Provide business logic and data access. They are typically injected into components.
- **Dependency Injection (DI)**: Angular uses DI to provide components with the services they need.

### Example:

A simple Angular module with a component and a service:

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { DataService } from './data.service';

@NgModule({
    declarations: [ AppComponent ],
    imports: [ BrowserModule ],
    providers: [ DataService ],
    bootstrap: [ AppComponent ]
})
export class AppModule {
}
```

## 3. What are Angular modules, and why are they important? Describe the role of NgModule in Angular.

Angular modules are a way to organize an application and manage dependencies. They help encapsulate components,
directives, pipes, and services, making the code more modular and maintainable.

NgModule is a decorator that marks a class as an Angular module and provides metadata about the module.

### Importance:

- **Organization**: Modules group related components and services.
- **Reusability**: Modules can be reused across different parts of an application or even different applications.
- **Dependency Management**: Modules manage service instances and dependencies.

## 4. How an Angular App gets Loaded and Started? What are index.html, app-root, selector and main.ts?

5 Steps executed when client send request from browser:

1. **First**, request will hit `index.html` page.
2. **Second**, index.html will invoke `main.js` file which is the javascript version of main.ts
   file (`<script src="main.js" type="module"></script>`).
   ```html
   <html lang="en">
    <head></head>
     <body inmaintabuse="1">
     <app-root ng-version="16.2.12"></app-root>
     <script src="runtime.js" type="module"></script>
     <script src="polyfills.js" type="module"></script>
     <script src="styles.js" defer=""></script>
     <script src="vendor.js" type="module"></script>
     <script src="main.js" type="module"></script>
     </body>
   </html>
   ```
3. **Third**, main.ts compiles the web-app and bootstraps the `app.module.ts` file (`.bootstrapModule(AppModule)`).
   ```typescript
   import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
   import { AppModule } from './app/app.module';
   
   platformBrowserDynamic().bootstrapModule(AppModule)
   .catch(err => console.error(err));
   ```
4. **Fourth**, App-Module file will then bootstrap the `app-component` (`bootstrap: [AppComponent]`).

    ```typescript
    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';
    import { AppComponent } from './app.component';
    
    @NgModule({
      declarations: [AppComponent],
      imports: [BrowserModule],
      providers: [],
      bootstrap: [AppComponent]
    })
    export class AppModule { }
    ```
5. **Finally**, the App-component html will be displayed.

## 5. What is a component in Angular?

A component in Angular is a building block for the UI, consisting of a TypeScript class, an HTML template, and
optionally, styles.

### Example:

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-hello',
    template: '<h1>Hello, {{name}}!</h1>',
    styles: [ 'h1 { color: blue; }' ]
})
export class HelloComponent {
    name: string = 'World';
}
```

## 6. How do you create a new component, service, pipe and directive in Angular? What other options are available for generating code in Angular?

In Angular, creating new components, services, pipes, and directives can be done using the Angular CLI (Command Line
Interface). Below are the steps and commands for each:

### **1. Component:**

To create a new component, use the following command:

```bash
ng generate component component-name
```

or shorthand:

```bash
ng g c component-name
```

This command will generate a new folder named `component-name` containing the component's **TypeScript**, **HTML**, *
*CSS**, and **spec** files.

Additional options:

- `--skip-tests`:  Skip generating spec files.
- `--standalone`: Generate a standalone component without a folder.
- `--style none`: Generate a component without styles.
- `--change-detection OnPush`: Set the change detection strategy to OnPush.
- `--view-encapsulation None | Emulated | ShadowDom`: Set the view encapsulation.

### **2. Service:**

To create a new service, use the following command:

```bash
ng generate service service-name
```

or shorthand:

```bash
ng g s service-name
```

This command will generate a service-name.service.ts file with a basic service class and a spec file for testing.

### **3. Pipe:**

To create a new pipe, use the following command:

```bash
ng generate pipe pipe-name
```

or shorthand:

```bash
ng g p pipe-name
```

### **4. Directive**

To create a new directive, use the following command:

```bash
ng generate directive directive-name
```

or shorthand:

```bash
ng g d directive-name
```

### **5. Enum:**

To create a new enum, use the following command:

```bash
ng generate enum enum-name
``` 

or shorthand:

```bash
ng g e enum-name
```

### 6. **Interface**

To create a new interface, use the following command:

```bash
ng generate interface interface-name
```

or shorthand:

```bash
ng g i interface-name
```

### 7. **Environments**

To create a new environment file, use the following command:

```bash
ng generate environments environment-name
```

## 7. Explain data binding in Angular. What are the different types of data binding in Angular?

Data binding in Angular is a core concept that allows for the synchronization of data between the component's class (the
model) and its template (the view). This means that when data in the model changes, the view is automatically updated,
and when data in the view changes, the model is updated as well. Angular provides different ways to achieve this
synchronization through various types of data binding.

### 1. Interpolation (One-Way Data Binding):

- **Syntax**: `{{ expression }}`
- **Direction**: From TypeScript (TS) to HTML.
- **Description**: Interpolation allows you to embed expressions in the template. Angular evaluates these expressions
  and inserts the resulting text into the HTML. This type of data binding is unidirectional, meaning it only goes from
  the component class to the view.
- **Example**:
     ```html
     <h1>{{ title }}</h1>
     ```

### 2. Property Binding (One-Way Data Binding):

- **Syntax**: `[property]="expression"`
- **Direction**: From TypeScript (TS) to HTML.
- **Description**: Property binding is used to bind the value of a component's property to an element's property in the
  view. It updates the view whenever the data in the component changes.
- **Example**:
     ```html
     <img [src]="imageUrl">
     ```

### 3. Attribute Binding (One-Way Data Binding):

- **Syntax**: `[attr.attributeName]="expression"`
- **Direction**: From TypeScript (TS) to HTML.
- **Description**: Attribute binding is similar to property binding but is used to bind attributes that are not native
  properties of an HTML element.
- **Example**:
     ```html
     <button [attr.aria-label]="buttonLabel">Click me</button>
     ```

### 4. Class Binding (One-Way Data Binding):

- **Syntax**: `[class.className]="expression"`
- **Direction**: From TypeScript (TS) to HTML.
- **Description**: Class binding allows you to conditionally add or remove CSS classes based on the value of an
  expression in the component.
- **Example**:
     ```html
     <div [class.error]="isError">Error message</div>
     ```

### 5. Style Binding (One-Way Data Binding):

- **Syntax**: `[style.styleProperty]="expression"`
- **Direction**: From TypeScript (TS) to HTML
- **Description**: Style binding is used to set inline styles for an element based on the evaluation of an expression.
- **Example**:
     ```html
     <div [style.backgroundColor]="bgColor">Content</div>
     ```

### 6. Event Binding (One-Way Data Binding):

- **Syntax**: `(event)="handler"`
- **Direction**: From HTML to TypeScript (TS).
- **Description**: Event binding allows you to listen to events triggered by the user in the view (e.g., click, input,
  etc.) and execute a function in the component.
- **Example**:
     ```html
     <button (click)="onClick()">Click me</button>
     ```

### 7. Two-Way Data Binding:

- **Syntax**: `[(ngModel)]="property"`
- **Direction**: Both ways - from TypeScript (TS) to HTML and from HTML to TypeScript (TS).
- **Description**: Two-way data binding combines property binding and event binding. It allows for a bidirectional
  exchange of data between the component and the view, meaning changes in the view are reflected in the model and vice
  versa. This is commonly used with form elements.
- **Example**:
     ```html
     <input [(ngModel)]="username">
     ```

Data binding in Angular ensures that the model and view stay in sync, providing a dynamic and responsive user
experience. The different types of data binding cater to various needs, from simple one-way binding (from TS to HTML) to
complex two-way data binding (both ways), offering a flexible and powerful way to build interactive applications.

## 8. How do you implement two-way data binding in Angular?

Two-way data binding in Angular allows for the synchronization of data between the component's class (the model) and the
template (the view). This means that when data in the model changes, the view is automatically updated, and when data in
the view changes (e.g., through user input), the model is updated as well.

To implement two-way data binding in Angular, you typically use the ngModel directive. Here's a step-by-step guide:

### 1. Install FormsModule:

Ensure that `FormsModule` is imported into your Angular module. `FormsModule` provides the necessary directives and
services to work with forms in Angular, including `ngModel`.

```typescript
// app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms'; // Import FormsModule

import { AppComponent } from './app.component';

@NgModule({
    declarations: [
        AppComponent
    ],
    imports: [
        BrowserModule,
        FormsModule // Include FormsModule in imports array
    ],
    providers: [],
    bootstrap: [ AppComponent ]
})
export class AppModule {
}
```

### 2. Use ngModel in Template:

Use the `ngModel` directive in your template to bind the form control (e.g., an input element) to a property in your
component's class. This creates two-way data binding.

```html
<!-- app.component.html -->
<input [(ngModel)]="username" placeholder="Enter your username">
<p>Your username is: {{ username }}</p>
```

### 3. Define the Bound Property in the Component:

Define the property in your component's class that will be bound to the form control.

```typescript
// app.component.ts
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: [ './app.component.css' ]
})
export class AppComponent {
    username: string = ''; // Define the property
}
```

### 4. If you are using standalone component, you can import FormsModule directly in the component.

```typescript
import { Component } from '@angular/core';
import { FormsModule } from '@angular/forms';

@Component({
    selector: 'app-standalone',
    standalone: true,
    imports: [ FormsModule ], // Import FormsModule directly
    template: `
    <input [(ngModel)]="username" placeholder="Enter your username">
    <p>Your username is: {{ username }}</p>
  `,
    styleUrls: [ './standalone.component.css' ]
})
export class StandaloneComponent {
    username: string = ''; // Define the property
}
```

## 9. What are services in Angular? How do you create and inject a service in Angular?

Services in Angular are singleton objects that encapsulate shared functionality and logic, making them available to
different parts of an application. They are typically used for tasks like data retrieval, business logic, logging, and
more. By using services, you can create reusable and testable code, adhering to the principle of separation of concerns.

### Creating a Service:

1. **Generate a Service**:

Use the Angular CLI to generate a service. This command will create a service file and register it with the root
injector by default.

```bash
ng generate service service-name
``` 

This will create two files:

- `my-service.service.ts`
- `my-service.service.spec.ts` (for testing)

2. Define the Service:

Implement the desired functionality within the generated service file.

```typescript
// my-service.service.ts
import { Injectable } from '@angular/core';

@Injectable({
    providedIn: 'root', // This makes the service available application-wide
})
export class MyService {
    constructor() {
    }

    getHello(): string {
        return 'Hello, World!';
    }
}
```

**@Injectable**: This decorator marks the class as a service that can be injected. The `providedIn` property within the
decorator allows you to specify the scope and lifecycle of the service. Here are the different options for `providedIn`:

- `providedIn: 'root'`: Ensures that the service is provided at the root level, making it a singleton across the entire
  application. This is the most common option and means the service is available throughout the app.
  ```typescript
  @Injectable({
   providedIn: 'root',
  })
  export class MyService {
    // Service code here
  }
  ```
- `providedIn: 'platform'`: Registers the service with the platform injector. This means the service is shared across
  multiple Angular applications running on the same page.
  ```typescript
  @Injectable({
   providedIn: 'platform',
  })
  export class MyService {
    // Service code here
  }
  ```
- `providedIn: 'any'`: Creates a new instance of the service for each lazy-loaded module. This can be useful when you
  want a separate instance of a service for each module.
  ```typescript
  @Injectable({
   providedIn: 'any',
  })
  export class MyService {
    // Service code here
  }
  ```
- `providedIn: Type<any>`: Allows you to specify a particular module where the service should be provided. This can
  limit the service's scope to that module.
  ```typescript
  @Injectable({
   providedIn: SomeModule,
  })
  export class MyService {
    // Service code here
  }
  ```

In addition to using the `providedIn` property, you can also register services in the `providers` array of an `NgModule`
or a component to control their scope and lifecycle more precisely.

### NgModule Example

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { MyService } from './my-service.service';

@NgModule({
    declarations: [
        AppComponent
    ],
    imports: [
        BrowserModule
    ],
    providers: [ MyService ], // Register the service here
    bootstrap: [ AppComponent ]
})
export class AppModule {
}
```

### Component-Level Example

```typescript
import { Component } from '@angular/core';
import { MyService } from './my-service.service';

@Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: [ './app.component.css' ],
    providers: [ MyService ] // Register the service here
})
export class AppComponent {
    constructor(private myService: MyService) {
    }
}
```

By using these options, you can control how and where your services are provided, ensuring that they are only created
when needed and are available in the appropriate scope.