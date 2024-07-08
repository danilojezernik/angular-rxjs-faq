## 1. What is Angular, and how does it differ from AngularJS?

**Angular** is a platform and framework for building single-page client applications using HTML, CSS, and TypeScript.
Angular is developed and maintained by Google and is often referred to as Angular 2+ or simply Angular to distinguish it
from its predecessor, AngularJS.

**AngularJS**, on the other hand, is the original version of Angular, which is based on JavaScript and was released in

2010.

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

## 3. How an Angular App gets Loaded and Started? What are index.html, app-root, selector and main.ts?

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

## 4. What is a component in Angular?

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

## 5. How do you create a new component, service, pipe and directive in Angular? What other options are available for generating code in Angular?

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

## 6. Explain data binding in Angular. What are the different types of data binding in Angular?

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

## 7. How do you implement two-way data binding in Angular?

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

## 8. What are services in Angular? How do you create and inject a service in Angular?

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

## 9. Explain dependency injection in Angular.

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

## 10. What is an Angular directive? Differentiate between structural and attribute directives.

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
is an Angular directive used to dynamically add or remove CSS classes on an HTML element based on certain conditions or expressions. This allows you to apply different styles to elements depending on the state of your application.

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
Is an Angular directive that allows you to set inline styles for an HTML element dynamically based on expressions. This is useful for applying styles that are computed or based on dynamic values.

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
    styleUrls: ['./app.component.css']
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

In this combined example, the div will have the blue text with a font size of 20 pixels, and if isActive is true, it will have a green background with white text. If isDisabled is true, it will have a gray background with dark gray text.

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

## 11. How do you create a custom directive in Angular? Create a directive that changes the background of an element.

## 12. What is Angular CLI, and how is it used?

## 13. Explain the purpose of the @NgModule decorator.

## 14. What are Angular pipes, and how do you use them? How do you create a custom pipe in Angular? How do you implement a custom pipe that accepts multiple parameters?

## 15. How to handle errors in async pipe in Angular? How to fix null in async pipe error?

## 16. What is Angular routing? How do you set up routing in an Angular application?

## 17. What is a guard in Angular routing, and how do you implement it?

## 18. What are Angular forms? Differentiate between template-driven and reactive forms in Angular.

## 19. How do you implement form validation in Angular?

## 20. What is Angular Universal? Explain the concept of server-side rendering in Angular.

## 21. How do you handle HTTP requests in Angular? What is the HttpClientModule, and how do you use it?

## 22. How do you handle errors in Angular applications?

## 23. What is Angular animation, and how do you implement it?

## 24. How do you use Angular Material in an application?

## 25. What is the purpose of Angular Elements?

## 26. Explain the change detection mechanism in Angular.

## 27. How do you optimize the performance of an Angular application?

## 28. What are Angular interceptors, and how do you use them? Write an example of an interceptor

## 29. How do you use environment variables in Angular?

## 30. What is AOT (Ahead-Of-Time) compilation in Angular? Explain the difference between AOT (Ahead-Of-Time) and JIT (Just-In-Time) compilation.

**AOT** (Ahead-Of-Time) compilation is a feature in Angular that compiles your Angular application and its templates
during the build process, before the application runs in the browser. This process converts the Angular HTML and
TypeScript code into efficient JavaScript code, which can be executed by the browser.

### Benefits of AOT Compilation

1. **Faster Rendering**: Since the application is precompiled, the browser can directly render the application without
   waiting for the compilation process, resulting in faster initial loading times.
2. **Smaller Angular Framework**: The AOT compiler strips out Angular decorators, reducing the size of the framework
   code included in your bundle.
3. **Template Errors Detection**: AOT compilation catches template errors and type errors during the build time,
   providing better error detection and debugging.
4. **Improved Security**: AOT compilation reduces the risk of injection attacks by pre-compiling templates and
   eliminating the need for the client-side HTML/JavaScript evaluation.

### How AOT Compilation Works

#### During the build process:

1. **Angular Compiler**: The Angular compiler translates Angular components and templates into JavaScript.
2. **Static Analysis**: The compiler performs static analysis of the code to ensure all templates are syntactically
   correct and all dependencies are resolved.
3. **Generated Code**: The compiler generates TypeScript code that is then compiled into JavaScript code.

### Enabling AOT Compilation

AOT compilation can be enabled by using the `--aot` flag in the Angular CLI during the build process:

```bash
ng build --aot
```

In production builds, AOT is enabled by default:

```bash
ng build --prod
```

### JIT (Just-In-Time) Compilation

JIT (Just-In-Time) compilation is the default mode in Angular during development. In JIT compilation, the Angular
application and its templates are compiled in the browser at runtime. This was the default until Angular 8.

### Differences between AOT and JIT Compilation

| Feature          | AOT (Ahead-Of-Time)                      | JIT (Just-In-Time)                 |
|------------------|------------------------------------------|------------------------------------|
| Compilation Time | During the build process                 | In the browser at runtime          |
| Rendering Speed  | Faster initial rendering                 | Slower initial rendering           |
| Bundle Size      | Smaller (due to removal of decorators)   | Larger (includes Angular compiler) |
| Error Detection  | Errors detected at build time            | Errors detected at runtime         |
| Security         | More secure (prevents injection attacks) | Less secure                        |
| Use Case         | Preferred for production builds          | Preferred for development builds   |
| Build Command    | `ng build --aot` or `ng build --prod`    | `ng build`                         |
| Loading Speed    | Faster due to precompilation             | Slower due to runtime compilation  |
| Default Version  | Default since Angular 9                  | Default until Angular 8            |

### Key Points

- **Both JIT and AOT**: Used to compile Angular TypeScript components into JavaScript, since browsers understand
  JavaScript, not TypeScript.
- **Default Compilation**: JIT was the default until Angular 8. AOT became the default starting in Angular 9.
- **Latest Angular Versions**: Use AOT by default to compile TypeScript into JavaScript.
- **Advantage of AOT**: Loading is much quicker than JIT because the code is already compiled at build time.

### Summary

- **AOT (Ahead-Of-Time) Compilation**: Compiles the Angular application during the build process, resulting in faster
  rendering, smaller bundle sizes, improved security, and catching errors at build time. It is ideal for production
  environments and has been the default since Angular 9.
- **JIT (Just-In-Time) Compilation**: Compiles the Angular application in the browser at runtime, making it suitable for
  development due to faster build times and better debugging capabilities. This was the default until Angular 8.

Understanding the differences between AOT and JIT compilation helps in optimizing the build and performance of Angular
applications based on the environment and requirements.

## 31. Explain the role of the ngOnInit lifecycle hook. What are the different lifecycle hooks in Angular?

## 32. How do you handle component communication in Angular?

## 33. What is the purpose of the ng-content directive?

## 34. How do you use the Renderer2 service in Angular?

## 35. What is Angular Ivy? How does it improve the Angular framework?

## 36. How do you test an Angular application?

## 37. What are the best practices for structuring an Angular project?

## 38. Explain the purpose of Angular decorators.

## 39. How do you handle state management in Angular applications?

## 40. What is the purpose of the APP_INITIALIZER token in Angular?

## 42. What is a feature module in Angular, and how do you use it?

## 43. Explain how Angular handles change detection.

## 45. Explain the difference between an Angular module and a JavaScript module.

## 46. How do you secure an Angular application?

## 47. Explain lazy loading in Angular and how you can lazy load components and modules in Angular and what are the benefits of lazy loading?

## 48. Write an example of how to inject a module with some configuration using forRoot

## 49. What are Angular schematics, and how are they used?

## 50. Explain how to use Angular with Web Workers.

## 51. How do you create a dynamic component in Angular?

## 52. How do you use dependency injection tokens in Angular?

## 53. What is the role of NgZone in Angular?

## 54. How do you handle memory leaks in Angular applications?

## 55. Explain the concept of control value accessor in Angular.

## 56. How do you create a custom decorator in Angular?

## 57. What are Angular resolvers, and how do you use them?

## 57. What are Angular guards? Write an example of code to protect a route with both sync and async ways.

## 59. Explain the use of forwardRef in Angular.

## 60. How do you set up an Angular application to use service workers for offline capabilities?

## 61. How do you implement internationalization (i18n) in Angular?

## 62. What is the role of ViewChild and ContentChild in Angular? How to access the child component from parent component with ViewChild? What is the difference between ContentChild & ContentChildren? Compare ng-Content, ViewChild, ViewChildren, ContentChild & ContentChildren?

## 63. Create a UsersService and getUsers method to make a GET request to http://localhost:3004/users and return a users stream. Write the code to get this data in a component.

## 64. Write an example of how to inject a module with some configuration using forRoot.

## 65. What is unsubscribe in Angular? Why is it important? What are the ways to unsubscribe?

## 66. What is change detection? How does onPush work? Why is onPush important?

## 67. What is Angular SSR (Server-Side Rendering)? What are the pros and cons of SSR?

## 68. How to use standalone components in Angular? What are the benefits?

## 69. How to use Angular signals? What are the benefits?

## 70. How to fix Angular input has no initializer error?

## 71. What is NgRx? How does it work? Are you familiar with Redux or NgRx?

## 72. When to use Angular animations instead of CSS animations? How to animate a button click event to fade in/out a block?

## 73. What is ng-container, ng-template, ng-content, and ng-template-outlet?

## 1. What is Angular, and how  it differ from AngularJS?

## 2. What are Angular advantages?

## 3. What is NPM?

## 4. What is Angular CLI, and how is it used?

## 5. What is Typescript? What are the advantages of Typescript over Javascript?

## 6. Where to store static files in an Angular project?

## 7. What is the role of angular.json file in Angular?

## 8. Explain the architecture of an Angular application.

## 10. What are Components in Angular?

## 11. What is a Selector and Template?

## 12. What is Module in Angular? What is app.module.ts file?

## 13. How an Angular App gets Loaded and Started? What are index.html, app-root, selector, and main.ts?

## 14. What is a Bootstrapped Module & Bootstrapped Component?

## 15. What are Angular modules, and why are they important? Describe the role of NgModule in Angular.

## 16. What is a component in Angular?

## 17. How do you create a new component in Angular?

## 18. Explain data binding in Angular. What are the different types of data binding in Angular?

## 19. What is String Interpolation in Angular?

## 20. What are services in Angular? How do you create and inject a service in Angular? Explain with an example!

## 21. What is Hierarchical Dependency Injection?

## 22. What is Provider in Angular?

## 23. What is the role of @Injectable Decorator in a Service?

## 24. Explain dependency injection in Angular. How does dependency injection work?

## 26. What is an Angular directive? Differentiate between structural and attribute directives and how do you create them?

## 106. What is ng-container, ng-template, ng-content, and ng-template-outlet?

## 27. What are Angular pipes, and how do you use them? How do you create a custom pipe in Angular?

## 28. Explain what lazy loading is in Angular and how you can lazy load components and modules in Angular. What are the benefits?

## 29. What is Angular routing? How do you set up routing in an Angular application?

## 30. How do you add routing to an Angular application? When can global routing be bad? What is router-outlet? How do you create a router link?

## 31. What is a guard in Angular routing, and how do you implement it?

## 32. What are lifecycle hooks in Angular? When are they called?

## 33. What is a Constructor in Angular?

## 34. What is ngOnChanges lifecycle hook in Angular?

## 35. What is ngOnInit lifecycle hook in Angular? What is the difference between constructor and ngOnInit?

## 37. What are Parent-Child Components?

## 36. How do you handle component communication in Angular?

## 40. What are the various ways to communicate between the components?

## 42. What is Template Reference Variable in Angular?

## 43. What is the role of ViewChild in Angular? How to access the child component from parent component with ViewChild?

## 45. What is ContentChild? What is the difference between ContentChild & ContentChildren? Compare ng-Content, ViewChild, ViewChildren, ContentChild & ContentChildren?

## 48. How do you use the Renderer2 service in Angular?

## 49. What is Angular Ivy? How does it improve the Angular framework?

## 50. Explain the purpose of Angular decorators and how do you create them?

## 51. How do you test an Angular application?

## 52. What are the best practices for structuring an Angular project?

## 53. How do you handle state management in Angular applications?

## 54. What is the purpose of the APP_INITIALIZER token in Angular?

## 55. How do you implement a custom form control in Angular?

## 56. What is a feature module in Angular, and how do you use it?

## 57. Explain how Angular handles change detection.

## 58. How do you implement a custom pipe that accepts multiple parameters?

## 59. Explain the difference between an Angular module and a JavaScript module.

## 60. How do you secure an Angular application?

## 61. What are Angular schematics, and how are they used?

## 62. Explain how to use Angular with Web Workers.

## 63. How do you create a dynamic component in Angular?

## 64. How do you use dependency injection tokens in Angular?

## 65. What is the role of NgZone in Angular?

## 66. How to execute code outside Angular change detection using ngZone? When does it make sense? Write a small example.

## 67. How do you handle memory leaks in Angular applications?

## 68. Explain the concept of control value accessor in Angular.

## 70. What are Angular resolvers, and how do you use them?

## 71. How do you handle route guards with complex conditions?

## 72. Explain the use of forwardRef in Angular.

## 73. How do you set up an Angular application to use service workers for offline capabilities?

## 74. How do you implement internationalization (i18n) in Angular?

## 75. What is Authentication & Authorization in Angular?

## 76. What is JWT Token Authentication in Angular?

## 77. How to Mock or Fake an API for JWT Authentication?

## 78. How to implement the Authentication with JWT in Angular?

## 79. What is Auth Guard?

## 80. What is HTTP Interceptor? Write an example of an interceptor.

## 81. How to Retry automatically if there is an error response from API?

## 82. What are the parts of JWT Token?

## 83. What is Postman?

## 84. Which part of the request has the token stored when sending to API?

## 85. What are Angular Forms? What are the type of Angular Forms?

## 86. What is the difference between Template Driven Forms & Reactive Forms?

## 87. How to setup Template Driven Forms?

## 88. How to apply Required field validation in template driven forms?

## 89. What is Form Group and Form Control in Angular?

## 90. How to setup Reactive Forms?

## 91. How to do validations in reactive forms?

## 92. What is AOT (Ahead-Of-Time) compilation in Angular? Explain the difference between AOT (Ahead-Of-Time) and JIT (Just-In-Time) compilation.

## 93. How to use environment variables in Angular?

## 95. What ways of binding data exist in Angular? Provide examples.

## 96. Write a DatesService with methods getTomorrow(), getYesterday(), getToday().

## 97. Why is it bad to call a function in an Angular template?

## 98. What is Angular generator? How to use generators?

## 99. What are Angular guards? Write an example of code to protect a route with both sync and async ways.

## 100. Write an example of how to inject a module with some configuration using forRoot.

## 101. What is as keyword in Angular? What does it do? Did you use it with combineLatest?

## 104. Create a directive that changes the background of an element.

## 105. How do pipes in Angular work? What built-in pipes do you know? Create a simple pipe.

## 107. How do Angular forms work? What forms are available in Angular? How do they differ?

## 108. How to fix Angular input has no initializer error?

## 109. What is NgRx? How does it work? Are you familiar with Redux or NgRx?

## 110. How to use inject in Angular? What are the benefits?

## 111. How to use standalone components in Angular? What are the benefits?

## 112. How to use Angular signals? What are the benefits?