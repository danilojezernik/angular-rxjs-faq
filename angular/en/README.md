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

## 14. What are Angular pipes, and how do you use them? How do you create a custom pipe in Angular? How do you implement a custom pipe that accepts multiple parameters?

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

## 15. How to handle errors in async pipe in Angular? How to fix null in async pipe error?

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

## 16. What is Angular routing? How do you set up routing in an Angular application?

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

## 17. What is a guard in Angular routing, and how do you implement it?

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

## 18. What are Angular forms? Differentiate between template-driven and reactive forms in Angular and how do you do a basic validation.

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

## 19. What are the all the validation options for forms in angular and how to do a custom validators?

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

## 20. What is Angular Universal? Explain the concept of server-side rendering in Angular.

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

## 21. How do you handle HTTP requests in Angular? What is the HttpClientModule, and how do you use it?

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

## 22. How do you handle errors in Angular applications?

Handling errors in Angular applications involves using several strategies to ensure the application remains stable,
user-friendly, and easy to debug. Here’s a comprehensive guide on how to handle errors effectively in Angular:

### 1. Global Error Handling

Angular provides a global error handling service that you can use to catch and handle errors globally.

- **ErrorHandler Service**: You can create a custom error handler by extending the ErrorHandler class.

```typescript
import { ErrorHandler, Injectable } from '@angular/core';

@Injectable()
export class GlobalErrorHandler implements ErrorHandler {
    handleError(error: any): void {
        // Log the error to the console or a remote logging infrastructure
        console.error('An error occurred:', error.message);
        // Implement your custom error handling logic here
    }
}
```

You need to provide this custom handler in your module:

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { GlobalErrorHandler } from './global-error-handler';

@NgModule({
    declarations: [ AppComponent ],
    imports: [ BrowserModule ],
    providers: [ { provide: ErrorHandler, useClass: GlobalErrorHandler } ],
    bootstrap: [ AppComponent ]
})
export class AppModule {
}
```

### 2. HTTP Error Handling

Handling HTTP errors involves catching errors when making HTTP requests and providing appropriate feedback to the user.

- **HttpClient Interceptors**: You can use an interceptor to catch HTTP errors.

```typescript
import { Injectable } from '@angular/core';
import { HttpEvent, HttpInterceptor, HttpHandler, HttpRequest, HttpErrorResponse } from '@angular/common/http';
import { Observable, throwError } from 'rxjs';
import { catchError } from 'rxjs/operators';
import { MatSnackBar } from '@angular/material/snack-bar';

@Injectable()
export class HttpErrorInterceptor implements HttpInterceptor {
    intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
        return next.handle(req).pipe(
            catchError((error: HttpErrorResponse) => {
                let errorMsg = '';
                if (error.error instanceof ErrorEvent) {
                    // Client-side error
                    errorMsg = `Error: ${error.error.message}`;
                } else {
                    // Server-side error
                    errorMsg = `Error Code: ${error.status}\nMessage: ${error.message}`;
                }

                // Display error message to the user
                this.snackBar.open(errorMsg, 'Close', {
                    duration: 3000,
                });

                console.log(errorMsg);
                return throwError(errorMsg);
            })
        );
    }
}
```

**Provide this interceptor in your module**:

```typescript
import { HTTP_INTERCEPTORS } from '@angular/common/http';

@NgModule({
    providers: [
        { provide: HTTP_INTERCEPTORS, useClass: HttpErrorInterceptor, multi: true }
    ]
})
export class AppModule {
}
```

### 3. Component-Level Error Handling

Handling errors specific to a component, usually within try-catch blocks or by subscribing to Observables.

- **Try-Catch Block**:

```typescript
export class ExampleComponent {
    constructor() {
        try {
            // Code that may throw an error
        } catch (error) {
            console.error('Component error:', error);
        }
    }
}
```

- **Observable Error Handling**:

```typescript
import { Component, OnInit } from '@angular/core';
import { MyService } from './my-service.service';
import { catchError } from 'rxjs/operators';
import { of } from 'rxjs';

@Component({
    selector: 'app-example',
    templateUrl: './example.component.html'
})
export class ExampleComponent implements OnInit {
    constructor(private myService: MyService) {
    }

    ngOnInit() {
        this.myService.getData().pipe(
            catchError(error => {
                console.error('Component error:', error);
                return of([]); // Provide a fallback value
            })
        ).subscribe(data => {
            // Handle the data
        });
    }
}
```

### 4. User Feedback

Providing feedback to the user when an error occurs is crucial for a good user experience.

- **Display Error Messages**: Use Angular’s template syntax to show error messages in the UI.

```html

<div *ngIf="errorMessage" class="error">
    {{ errorMessage }}
</div>
```

- **Notification Services**: You can use Angular Material’s Snackbar or other notification libraries to show error
  messages.

```typescript
import { MatSnackBar } from '@angular/material/snack-bar';

export class ExampleComponent {
    constructor(private snackBar: MatSnackBar) {
    }

    showError(message: string) {
        this.snackBar.open(message, 'Close', {
            duration: 3000,
        });
    }
}
```

### 5. Logging Errors

Logging errors to an external service helps in monitoring and debugging issues.

- **Remote Logging**: Send error details to a remote logging infrastructure (e.g., Sentry, LogRocket).

```typescript
import * as Sentry from '@sentry/angular';

@Injectable()
export class GlobalErrorHandler implements ErrorHandler {
    handleError(error: any): void {
        Sentry.captureException(error.originalError || error);
        console.error('An error occurred:', error.message);
    }
}
```

### 6. Retry Mechanism

Retry failed operations using retry logic with RxJS operators.

- **Retry with RxJS**:

```typescript
import { retry } from 'rxjs/operators';

this.myService.getData().pipe(
    retry(3), // Retry up to 3 times before failing
    catchError(error => {
        console.error('Component error:', error);
        return of([]); // Provide a fallback value
    })
).subscribe(data => {
    // Handle the data
});
```

By implementing these strategies, you can effectively handle errors in Angular applications, making them more robust,
maintainable, and user-friendly.

## 23. What is Angular animation, and how do you implement it?

Angular animations provide a way to create dynamic and visually engaging transitions and effects in Angular
applications. Built on top of the standard Web Animations API, Angular offers a powerful yet easy-to-use API for
animating elements.

### Types of Animations in Angular

Angular provides several types of animations that can be used to enhance user experiences:

1. **State and Transition Animations**: Change the state of an element and animate between these states.
2. **Keyframe Animations**: Define multiple intermediate styles within a single animation.
3. **Sequence Animations**: Run a series of animations in sequence.
4. **Group Animations**: Run multiple animations simultaneously.

### Implementing Angular Animation

1. **Import the Angular Animation Module**

First, import the `BrowserAnimationsModule` in your application's main module. This module is necessary for enabling
animation capabilities.

```typescript
// app.module.ts
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';

@NgModule({
    declarations: [ AppComponent ],
    imports: [ BrowserAnimationsModule ],
    bootstrap: [ AppComponent ],
})
export class AppModule {
}
```

2. **Define Animations**

Define animations in a component by importing animation-specific functions from `@angular/animations` and using them in
the component metadata.

Here is a basic example of an Angular animation:

```typescript
import { Component } from '@angular/core';
import {
    trigger,
    state,
    style,
    animate,
    transition,
    keyframes,
    sequence,
    group
} from '@angular/animations';

@Component({
    selector: 'app-root',
    template: `
    <div [@openClose]="isOpen ? 'open' : 'closed'" (click)="toggle()">
      Click to toggle
    </div>
  `,
    animations: [
        trigger('openClose', [
            state(
                'open',
                style({
                    height: '200px',
                    opacity: 1,
                    backgroundColor: 'yellow',
                })
            ),
            state(
                'closed',
                style({
                    height: '100px',
                    opacity: 0.5,
                    backgroundColor: 'green',
                })
            ),
            transition('open => closed', [ animate('1s') ]),
            transition('closed => open', [ animate('0.5s') ]),
        ]),
    ],
})
export class AppComponent {
    isOpen = true;

    toggle() {
        this.isOpen = !this.isOpen;
    }
}
```

3. **Using Animations in Templates**

Bind the animation to an element using Angular's animation binding syntax. This example toggles the state between open
and closed when the div is clicked.

```html
<!-- app.component.html -->
<div [@openClose]="isOpen ? 'open' : 'closed'" (click)="toggle()">
    Click to toggle
</div>
```

### Types of Angular Animations in Detail

#### State and Transition Animations

State and transition animations allow you to define different styles for different states and transition between these
states.

```typescript
trigger('openClose', [
    state('open', style({ height: '200px', opacity: 1, backgroundColor: 'yellow' })),
    state('closed', style({ height: '100px', opacity: 0.5, backgroundColor: 'green' })),
    transition('open => closed', [ animate('1s') ]),
    transition('closed => open', [ animate('0.5s') ]),
])
```

#### Keyframe Animations

Keyframe animations define multiple intermediate styles within a single animation, providing finer control over the
animation.

```typescript
trigger('bounce', [
    transition('* => *', [
        animate('1s', keyframes([
            style({ transform: 'translateY(0)', offset: 0 }),
            style({ transform: 'translateY(-30px)', offset: 0.5 }),
            style({ transform: 'translateY(0)', offset: 1.0 })
        ]))
    ])
])
```

#### Sequence Animations

Sequence animations run a series of animations in sequence.

```typescript
trigger('sequenceAnimation', [
    transition('* => *', sequence([
        animate('1s', style({ opacity: 0 })),
        animate('1s', style({ opacity: 1 }))
    ]))
])
```

#### Group Animations

Group animations run multiple animations simultaneously.

```typescript
trigger('groupAnimation', [
    transition('* => *', group([
        animate('1s', style({ width: '100px' })),
        animate('1s', style({ height: '100px' }))
    ]))
])
```

### Summary

Angular animations are a robust tool for creating engaging and dynamic user interfaces. By importing
BrowserAnimationsModule, defining animations
using `trigger`, `state`, `style`, `animate`, `transition`, `keyframes`, `sequence`, and
`group` functions, and binding these animations in your templates, you can easily add various types of animations to
your
Angular applications.

## 72. When to use Angular animations instead of CSS animations? How to animate a button click event to fade in/out a block?

Angular animations are best used for complex, state-driven animations tightly integrated with Angular components. For
simple animations, CSS might suffice.

### Angular Animations:

- **Complex State Transitions**: When you need to animate complex state transitions that involve multiple elements and
  conditions.
- **Dynamic Animations**: If the animation needs to respond to runtime conditions or user interactions in a more dynamic
  way.
- **Component-based Animations**: For animations that are tightly coupled with Angular components and require the use of
  Angular's state management.
- **Advanced Sequencing**: When animations need advanced sequencing and orchestration.

### CSS Animations:

- **Simple Animations**: For basic animations that do not depend on application state, such as hover effects or simple
  transitions.
- **Performance**: CSS animations are generally more performant because they are handled by the browser's rendering
  engine.
- **Ease of Use**: When you want to quickly implement animations without the need for Angular-specific syntax.

### How to Animate a Button Click Event to Fade In/Out a Block

To animate a button click event to fade in/out a block using Angular animations, follow these steps:

1. Install Angular Animations: Ensure you have Angular animations package installed.

```bash
npm install @angular/animations
```

2. Import Necessary Modules: Import the BrowserAnimationsModule in your `app.module.ts`.

```typescript
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';

@NgModule({
    imports: [ BrowserAnimationsModule, ... ]
})
export class AppModule {
}
```

3. Define Animations in Component: Define the animations in your component.

```typescript
import { Component } from '@angular/core';
import { trigger, state, style, transition, animate } from '@angular/animations';

@Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    animations: [
        trigger('fadeInOut', [
            state('void', style({
                opacity: 0
            })),
            transition(':enter, :leave', [
                animate(500)
            ])
        ])
    ]
})
export class AppComponent {
    show = false;

    toggle() {
        this.show = !this.show;
    }
}
```

4. Update Template: Update your component template to use the defined animation.

```html

<button (click)="toggle()">Toggle Block</button>
<div *ngIf="show" @fadeInOut>
    <p>This block will fade in and out</p>
</div>
```

### Explanation:

- **Importing Required Modules**: Import `BrowserAnimationsModule` to enable animations.
- **Defining Animations**: Define a trigger named `fadeInOut` with two states: `void` (when the element is not in the
  DOM) and the default state. Use the `transition` function to define the enter and leave transitions with a 500ms
  duration.
- **Template Binding**: Use Angular's structural directive `*ngIf` to conditionally include the block and bind the
  animation trigger to the element.

## 25. What is the purpose of Angular Elements and give an example of how to use it.

The purpose of Angular Elements is to enable Angular components to be used as Web Components. This allows Angular
components to be integrated into non-Angular applications, broadening the scope of where Angular components can be
utilized. Here are the key benefits and purposes of Angular Elements:

### 1. Integration with Non-Angular Projects:

Angular Elements allows developers to wrap Angular components as custom elements (Web Components), which can then be
embedded in any HTML page, regardless of whether the page uses Angular or another framework.

### 2. Reusability:

By converting Angular components into Web Components, those components become reusable across different projects and
frameworks. This promotes a high level of code reusability and consistency across various parts of an organization's
applications.

### 3. Ease of Use:

Web Components created with Angular Elements can be used just like any other HTML element, making it straightforward for
developers who are not familiar with Angular to use these components in their projects.

### 4. Standardization:

Angular Elements leverages the Web Components standard, ensuring that the components created are compatible with all
modern browsers and can work with any front-end framework that supports Web Components.

### 5. Simplified Upgrades and Maintenance:

As Angular Elements are standard Web Components, the Angular code inside these components can be updated independently
from the rest of the application. This modularity can simplify maintenance and upgrades.

### 6. Enhanced Collaboration:

Teams using different frameworks or working on different parts of a large project can collaborate more effectively.
Angular Elements allows for the encapsulation of functionality within Angular components that can be shared and used by
other teams.

Overall, Angular Elements provides a way to extend the reach of Angular components, making them versatile, reusable, and
easy to integrate into a wide variety of web applications.

### Using Angular Elements:

First, ensure you have Angular CLI installed. If not, you can install it using:

```bash
npm install -g @angular/cli
```

Then, create a new Angular project:

```bash
ng new angular-elements-demo
cd angular-elements-demo
```

Next, create a new Angular component:

```bash
ng generate component hello-world
```

This will generate a new component `HelloWorldComponent`. For simplicity, modify the `hello-world.component.ts` to look
like this:

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-hello-world',
    template: `<h1>Hello, {{name}}!</h1>`,
    styles: [ `h1 { font-family: Lato; }` ]
})
export class HelloWorldComponent {
    name: string = 'Angular Elements';
}
```

Now you need to add Angular Elements and the Angular Builder Custom Elements to your project:

```bash
ng add @angular/elements
npm install @webcomponents/custom-elements
```

Now, let's modify the `app.module.ts` to include Angular Elements and define our custom element:

```typescript
import { NgModule, Injector } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { createCustomElement } from '@angular/elements';
import { AppComponent } from './app.component';
import { HelloWorldComponent } from './hello-world/hello-world.component';

@NgModule({
    declarations: [
        AppComponent,
        HelloWorldComponent
    ],
    imports: [
        BrowserModule
    ],
    providers: []
})
export class AppModule {
    constructor(private injector: Injector) {
    }

    ngDoBootstrap() {
        const helloWorldElement = createCustomElement(HelloWorldComponent, { injector: this.injector });
        customElements.define('hello-world', helloWorldElement);
    }
}
```

Then, build your project:

```bash
ng build
```

This will generate your web components in the `dist/angular-elements-demo` directory. You can then serve this component
using any web server.

Finally, create an `index.html` file in the `dist/angular-elements-demo` directory to use your custom element:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Angular Elements Demo</title>
</head>
<body>
<hello-world></hello-world>
<script src="runtime.js"></script>
<script src="polyfills.js"></script>
<script src="main.js"></script>
</body>
</html>
```

You can serve this file using a simple HTTP server, such as `http-server`:

```bash
npx http-server ./dist/angular-elements-demo
```

Open `http://localhost:8080` (or the port number displayed) in your browser to see your Angular component rendered as a
Web Component.

This example demonstrates the basic setup to create an Angular component, wrap it as a custom element using Angular
Elements, and serve it as a Web Component.

## 26. Explain the change detection mechanism in Angular.

In Angular, change detection is a mechanism that updates the view whenever the application state changes. This ensures
that the UI is always in sync with the underlying data model. The key components and steps involved in Angular's change
detection mechanism are as follows:

### Key Components

#### 1. Zone.js:

Angular uses Zone.js to detect and manage asynchronous operations. It patches asynchronous APIs
like `setTimeout`, `XHR`,
and promises, allowing Angular to be notified when these operations complete.

#### 2. NgZone:

Angular's `NgZone` service builds on Zone.js to run change detection automatically when certain asynchronous operations
complete, such as event handlers, HTTP requests, or timers.

#### 3. ChangeDetector:

Each component in Angular has an associated change detector. These change detectors form a tree that parallels the
component tree, allowing Angular to check each component for changes.

### Change Detection Strategies

Angular provides two change detection strategies:

#### 1. Default:

This is the default strategy where Angular checks every component in the component tree for changes. It is eager but can
be inefficient for large applications because it checks all components even if some have not changed.

#### 2. OnPush:

This strategy is used to optimize performance. Angular only checks the component and its subtree if an `@Input` property
changes, an event originated from the component, or a change detection is explicitly triggered. This strategy relies on
immutability and pure functions to determine if changes have occurred.

### Change Detection Process

#### 1. Application State Change:

An application state change can be triggered by user interactions (e.g., button clicks), asynchronous operations (e.g.,
HTTP requests), or direct model updates.

#### 2. Run Change Detection:

Angular uses Zone.js to detect when the application state might have changed. When an asynchronous operation completes
or an event occurs, Zone.js triggers Angular’s change detection process.

#### 3. Change Detection Tree Traversal:

Angular traverses the change detector tree starting from the root component. It checks each component to see if its
model has changed. If a change is detected, Angular updates the view to reflect the new state.

#### 4. View Update:

If changes are detected, Angular updates the DOM to match the new application state.

### Optimizing Change Detection

#### 1. Immutable Data Structures:

Using immutable data structures ensures that change detection is efficient. When data changes, Angular can quickly
determine if a change has occurred by checking object references.

#### 2. TrackBy Function in ngFor:

When using `ngFor` to loop through a list of items, specifying a `trackBy` function helps Angular track items by a
unique
identifier, reducing the number of checks and DOM manipulations.

#### 3. Manual Change Detection Control:

Angular allows for manual control of change detection via methods such as `ChangeDetectorRef.detectChanges()` and
`ChangeDetectorRef.markForCheck()`. These methods enable developers to trigger or defer change detection explicitly.

#### 4. Using OnPush Strategy:

Adopting the `OnPush` change detection strategy for components can greatly improve performance by reducing the frequency
of change detection checks.

In summary, Angular's change detection mechanism ensures that the view is always in sync with the application state. By
using a combination of Zone.js, `NgZone`, and change detectors, Angular efficiently detects and propagates changes,
keeping the UI updated. Developers can optimize this process through various strategies and techniques to enhance
performance.

## 27. How do you optimize the performance of an Angular application?

## 28. What are Angular interceptors, and how do you use them? Write an example of an interceptor and how to handle error with interceptor.

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

## 68. How to use standalone components in Angular? What are the benefits?

## 69. How to use Angular signals? What are the benefits?

## 70. How to fix Angular input has no initializer error?

## 71. What is NgRx? How does it work? Are you familiar with Redux or NgRx?

## 72. When to use Angular animations instead of CSS animations? How to animate a button click event to fade in/out a block?

## 73. What is ng-container, ng-template, ng-content, and ng-template-outlet?