# Angular Details

[Angular link](https://v14.angular.io/guide/what-is-angular#templates)

## Angular Main Points

1. A component-based framework for building scalable web applications

   ## Angular Application essentials

    1. Components are the building blocks that compose an application.
    2. A component includes a TypeScript class with a @Component() decorator, an HTML template, and styles.
    3. A **template** in @component is a block of HTML that tells Angular how to render the component in your application

        ```typescript
        //Normal Component
        import { Component } from '@angular/core';

        @Component({
        selector: 'hello-world',
        template: `
            <h2>Hello World</h2>
            <p>This is my first component!</p>
        `
        })
        export class HelloWorldComponent {
        // The code in this class drives the component's behavior.
        }

        // template added in the html
        <hello-world></hello-world>

        //Angular renders this component and the resulting DOM looks like
        <hello-world>
        <h2>Hello World</h2>
        <p>This is my first component!</p>
        </hello-world>
    3. Templates
        * Angular supports property binding []

            ```typescript
            <p
                [id]="sayHelloId"
                [style.color]="fontColor">
                You can set my color in the component!
            </p>
        * Declare event listeners to listen for and respond to user actions such as keystrokes, mouse movements, clicks, and touches. You declare an event listener by specifying the event name in parentheses:

            ```typescript
                            <button
                type="button"
                [disabled]="canClick"
                (click)="sayMessage()">
                Trigger alert message
                </button>

                //The one defined in the component class
                sayMessage() {
                alert(this.message);
                }

        ```typescript
                import { Component } from '@angular/core';

        @Component ({
        selector: 'hello-world-interpolation',
        templateUrl: './hello-world-interpolation.component.html'
        })
        export class HelloWorldInterpolationComponent {
            message = 'Hello, World!';


        }
        <p>{{ message }}</p>


        //output of the above one is 
        <p>Hello, World!</p>

        //

## Directives

1. Add features to your templates by using directives.
2. The most popular directives in Angular are *ngIf and*ngFor

   ## Dependency Injection

   ### Injection of a logger class

    ```typescript
    import { Injectable } from '@angular/core';

    @Injectable({providedIn: 'root'})
    export class Logger {
    writeCount(count: number) {
        console.warn(count);
    }
    }

    //html model
    import { Component } from '@angular/core';
    import { Logger } from '../logger.service';

    @Component({
    selector: 'hello-world-di',
    templateUrl: './hello-world-di.component.html'
    })
    export class HelloWorldDependencyInjectionComponent  {
    count = 0;

    constructor(private logger: Logger) { }

    onLogMe() {
        this.logger.writeCount(this.count);
        this.count++;
    }
    }

## Angular CLI

        Command  Details
        ng build  Compiles an Angular application into an output directory.
        ng serve  Builds and serves your application, rebuilding on file changes.
        ng generate Generates or modifies files based on a schematic.
        ng test  Runs unit tests on a given project.
        ng e2e  Builds and serves an Angular application, then runs end-to-end tests.

## First Party Angular Libraries

        Library          Details
        Angular Router  Advanced client-side navigation and routing based on Angular components. Supports lazy-loading, nested routes, custom path matching, and more.
        Angular Forms  Uniform system for form participation and validation.
        Angular HttpClient  Robust HTTP client that can power more advanced client-server communication.
        Angular Animations  Rich system for driving animations based on application state.
        Angular PWA  Tools for building Progressive Web Applications (PWA) including a service worker and Web application manifest.
        Angular Schematics  Automated scaffolding, refactoring, and update tools that simplify development at large scale.

## Angular Vacabolary or LIfe cycle Hooks

<https://v14.angular.io/guide/glossary#lifecycle-hook>


## Java Script full concepts with gif
https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif

## Data Binding:
-- String interpolation (ts ---> html) => {{variableName}}
-- property binding (ts => html) => [property(attribute)]= "variableName";
-- event binding (html ==> ts) ==> (eventName) = "function"
-- two way binding (banana in the box====(html to ts)) ===> [(propertyName)]="variableName"
         -- Example of two way binding : ngModel

## Direction
-- Structural Directive
   -- *ngIf (ng-template you will use using the # symbol),ngFor,ngSwitch
-- Attribute Directive:
   -- ngStyle (inline style and expression)
   -- ngClass (we need to mention the css class)
## Encapsulation in the Angular 
1. Types (link:->https://v14.angular.io/guide/view-encapsulation)
    ```typescript
    1. ViewEncapsulation.ShadowDom---->It covers the entire View of Html
    2. ViewEncapsulation.Emulated----> It covers what is inside the Html tag
    3. ViewEncapsulation.None-----> It covers the direct css styling.
    ## Where to use
        @Component({
    selector: 'app-no-encapsulation',
    template: `
        <h2>None</h2>
        <div class="none-message">No encapsulation</div>
    `,
    styles: ['h2, .none-message { color: red; }'],
    encapsulation: ViewEncapsulation.None,
    })
    export class NoEncapsulationComponent { }

    ## Angular adds the styles for this component as global styles to the <head> of the document.
    As already mentioned, Angular also adds the styles to all shadow DOM hosts, making the styles available throughout the whole application.  

 
## @input and @output property Binding (https://v14.angular.io/guide/component-interaction)
    1. Direct input binding
    2. Binding using the setter class method.
    3. Binding with the local variable
    4. Binding with the @viewChild so all the properties shall be accessed by the parent component as well.
## Components Styling 
    1. ::ng-deep helps for the global styling.
        Applying the ::ng-deep pseudo-class to any CSS rule completely disables view-encapsulation for that rule. Any style with ::ng-deep 
        applied becomes a global style. In order to 
        scope the specified style to the current 
        component and all its descendants, be sure to include the :host selector before ::ng-deep.'
         If the ::ng-deep combinator is used without 
         the :host pseudo-class selector, the style 
         can bleed into other component
    2. use @mixin 
    3. use ::part with the mixins
    4. 
## Components Content Projection
    1. https://v14.angular.io/guide/content-projection
    2. Content projection is a pattern in which you insert, or project, the content you want to use inside another component. For example, you could have a Card component that accepts content provided by another component.
        1. Types
            1. Single slot content projection.---><ng-content>()
            2. Multi-slot contenrt Projection.
                Default:
                    <ng-content></ng-content>

                    Question:
                    <ng-content select="[question]"></ng-content>
            3. Conditional content projection.
                    <ng-template>
                    The <ng-container></ng-container> element is a logical construct that is used to group other DOM elements; however, the ng-container itself is not rendered in the DOM tree.


## Dynamic Components
    1. 

## Angular elements:(using this we shall make a componentr to a custom tag)
The @angular/elements package exports a createCustomElement() API that provides a bridge from Angular's component interface and change detection functionality to the built-in DOM API.

Use the createCustomElement() function to convert a component into a class that can be registered with the browser as a custom element. After you register your configured class with the browser's custom-element registry, use the new element just like a built-in HTML element in content that you add directly into the DOM:
<my-popup message="Use Angular!"></my-popup>

## Steps to create a Angular project

## Templates
### Enhancing Templates
1. Angular does not support **script** element in the templates.
    Angular extends the HTML syntax in your templates with additional functionality.
    For example, Angular’s data binding syntax helps to set Document Object Model (DOM) properties dynamically.

2. {{}}---> Property Binding ****
    ```typescript
    <img alt="item" [src]="itemImageUrl">
    // ts file
    itemImageUrl = '../assets/phone.png';

    //Another example
            <!-- Bind button disabled state to `isUnchanged` property -->
        <button type="button" [disabled]="isUnchanged">Disabled Button</button>


    //child parent relationship
    <app-item-detail [childItem]="parentItem"></app-item-detail>

    //Toggling button using the property binding property

        <!-- Bind button disabled state to `isUnchanged` property -->
    <button type="button" [disabled]="isUnchanged">Disabled Button</button>

    //ts file
    isUnchanged = true;

    //Another object level usage of the property binding
    <app-item-list [items]="currentItems"></app-item-list>
    @Input() items: Item[] = [];
    //item.ts
        export interface Item {
    id: number;
    name: string;
    }
    //app.component.ts
            currentItems = [{
        id: 21,
        name: 'phone'
        }];

3. Event Binding
    ```typescript
    <button (click)="onSave()">Save</button>
    <input (keydown.shift.t)="onKeydown($event)" />
        ![alt text](image.png)
4. two way event binding
    ```typescript
     <app-sizer [(size)]="fontSizePx"></app-sizer>
     <div [style.font-size.px]="fontSizePx">Resizable Text</div>


## Property Binding

1. different types

    ```typescript
    //syntax of property binding
    <element [property]="expression"></element>

## Observable
1. RxJS (Reactive Extensions for JavaScript) is a library for reactive programming using Observables, which makes it easy to compose asynchronous or callback-based code
2. An Observable is a stream of events or data. Think of it like a sequence of values that are pushed to a subscriber over time. Unlike promises, which handle a single value at a time, Observables can handle multiple values over any amount of time (either synchronous or asynchronous).
3. ```typescript
    import { Observable } from 'rxjs';

        // Creating an observable
        const myObservable = new Observable(subscriber => {
        subscriber.next('Hello');
        subscriber.next('World');
        subscriber.complete(); // Indicates completion
        });

        // Subscribing to the observable
        myObservable.subscribe({
        next(value) { console.log(value); },   // Logs emitted values
        error(err) { console.error('Error:', err); },
        complete() { console.log('Completed'); }
        });

        //unSubscribe();
        myObservable.unsubscribe();
4. Observable Helper
    * ```typescript 
            // 1. of() --> Emits the provided arguments as values in sequence.
            import { of } from 'rxjs';
        const obs = of(1, 2, 3);
        obs.subscribe(console.log); // Outputs: 1, 2, 3
    * ```tyepscript 
            // 2. from() -->Converts an array, promise, or iterable into an observable.
             import { from } from 'rxjs';
            const obs = from([1, 2, 3]);
            obs.subscribe(console.log); // Outputs: 1, 2, 3
    * ```typescript 
                // 3. interval() -->  Emits an incremental number every specified interval of time.
                import { interval } from 'rxjs';
        const obs = interval(1000); // Emits a number every second
        obs.subscribe(console.log); // Outputs: 0, 1, 2, ...



5. Operators in Rxjs
    Operators are pure functions in RxJS that allow you to manipulate, transform, and filter data emitted by observables.

    ```typescript
        //map,filter,mergeMap,switchmap()
                import { of } from 'rxjs';
        import { map } from 'rxjs/operators';

        of(1, 2, 3).pipe(
        map(value => value * 10)
        ).subscribe(console.log);  // Outputs: 10, 20, 30

        //filter()..Emits only those values that pass the condition.
                import { filter } from 'rxjs/operators';

        of(1, 2, 3, 4, 5).pipe(
        filter(value => value % 2 === 0)
        ).subscribe(console.log);  // Outputs: 2, 4

        //mergeMap-->Flattens multiple observables into one, often used for making multiple HTTP requests.
            import { of } from 'rxjs';
            import { mergeMap } from 'rxjs/operators';

            const getData = (value) => of(`${value}: Data`);

            of(1, 2, 3).pipe(
            mergeMap(value => getData(value))
            ).subscribe(console.log);  // Outputs: '1: Data', '2: Data', '3: Data'
        //switchmap-->Similar to mergeMap, but cancels previous observables when a new value is emitted.
        import { fromEvent, interval } from 'rxjs';
        import { switchMap } from 'rxjs/operators';

        const clicks = fromEvent(document, 'click');
        const result = clicks.pipe(
        switchMap(() => interval(1000))
        );
        result.subscribe(console.log);  // Starts emitting numbers after each click
6. Subjects in Rxjs
    A Subject is both an Observable and an Observer, meaning it can emit data as well as subscribe to it. This makes it useful for multicasting data to multiple subscribers.

     ``` typescript
            import { Subject } from 'rxjs';

            const subject = new Subject();

            // Multiple subscribers to the same observable
            subject.subscribe(console.log);  // Subscriber 1
            subject.subscribe(console.log);  // Subscriber 2

            subject.next('Hello');  // Both subscribers receive this
            subject.next('World');  // Both subscribers receive this

            //cold Observable
                const obs = new Observable(subscriber => {
            subscriber.next(Math.random());  // Emits a new random value
            });
            obs.subscribe(console.log);  // Logs: 0.12345
            obs.subscribe(console.log);  // Logs: 0.67890 (different value)

            //Hot Observable

            const subject = new Subject();
            subject.subscribe(console.log);  // Logs emitted value
            subject.next(Math.random());     // Both subscribers receive the same value
## Reactive programming uses
    1. Streams
    2. Observer Pattern
    3. Asynchronous Event-driven
    4. Declaration
    5. Propagation of change
    3. Functional interface like Map,filter,reduce etc.


## Behavioural subject
    
```typescript
    //Remember asObservable is the Key which is used to subscribe the data for continuous usage.
    import { Injectable } from '@angular/core';
import { BehaviorSubject } from 'rxjs';

@Injectable({
  providedIn: 'root',
})
export class SharedService {
  // BehaviorSubject with initial value of an empty string
  private messageSource = new BehaviorSubject<string>('Initial Message');

  // Observable for the BehaviorSubject
  currentMessage = this.messageSource.asObservable();

  constructor() {}

  // Method to update the message in BehaviorSubject
  changeMessage(newMessage: string) {
    this.messageSource.next(newMessage);
  }
}



## Hints

1. **{{}}** ----> Used to render the property value as text.
2. **ActivateedRoute** ---> It is passed inside the constructor, ActivatedRoute is specific to each component that the Angular Router loads. ActivatedRoute contains information about the route and the route's parameters.

By injecting ActivatedRoute, you are configuring the component to use a service. The Managing Data step covers services in more detail.
3. **HttpClient** --->
Servers often return data in the form of a stream. Streams are useful because they make it easy to transform the returned data and make modifications to the way you request that data. Angular HttpClient is a built-in way to fetch data from external APIs and provide them to your application as a stream.
4. **why tslint** ?
TSLint reads the configuration from tslint.json when you run it (e.g., via a build script or directly in your IDE).
It analyzes your TypeScript files based on the specified rules and reports any violations.
Remember to tailor your tslint.json to your project’s needs.
5. what is **change detection** ?
The mechanism by which the Angular framework synchronizes the state of the UI of an application with the state of the data. The change detector checks the current state of the data model whenever it runs, and maintains it as the previous state to compare on the next iteration.

As the application logic updates component data, values that are bound to DOM properties in the view can change. The change detector is responsible for updating the view to reflect the current data model. Similarly, the user can interact with the UI, causing events that change the state of the data model. These events can trigger change detection.
6. Available **class decorators**?
           ---> @Component()
           ---> @Directive()
           ---> @Pipe()
           ---> @Injectable()
           ---> @NgModule()

7. **Data Binding**
           ---> Interpolation
           ---> Property binding
           ---> Event binding
           ---> Attribute binding
           ---> Class and style binding
           ---> Two-way data binding with ngModel
8. **Eager loading**
NgModules or components that are loaded on launch are referenced as eager-loaded, to distinguish them from those that are loaded at run time that are referenced as lazy-loaded.
9. **ECMAScript**
Not all browsers support the latest ECMAScript standard, but you can use a transpiler to write code using the latest features, which will then be transpiled to code that runs on versions that are supported by browsers. An example of a transpiler is TypeScript.
10. why **elementRef**?
Angular defines an ElementRef class to wrap render-specific native UI elements. In most cases, this allows you to use Angular templates and data binding to access DOM elements without reference to the native element.

The documentation generally refers to elements as distinct from DOM elements. Elements are instances of a ElementRef class. DOM elements are able to be accessed directly, if necessary.

11. why **FormControl**?
An instance of FormControl, which is a fundamental building block for Angular forms. Together with FormGroup and FormArray, tracks the value, validation, and status of a form input element.
12. **IVY**
Ivy is the historical code name for the current compilation and rendering pipeline in Angular. It is now the only supported engine, so everything uses Ivy.
13. **JIT**
The Angular just-in-time (JIT) compiler converts your Angular HTML and TypeScript code into efficient JavaScript code at run time, as part of bootstrapping.

JIT compilation is the default (as opposed to AOT compilation) when you run the ng build and ng serve Angular CLI commands, and is a good choice during development. JIT mode is strongly discouraged for production use because it results in large application payloads that hinder the bootstrap performance.
14. **Lazy loading**
A process that speeds up application load time by splitting the application into multiple bundles and loading them on demand. For example, dependencies can be lazy loaded as needed. The example differs from eager-loaded modules that are required by the root module and are loaded on launch.

The router makes use of lazy loading to load child views only when the parent view is activated. Similarly, you can build custom elements that can be loaded into an Angular application when needed.
15. **Lifecycle Hook**
An interface that allows you to tap into the lifecycle of directives and components as they are created, updated, and destroyed.

Each interface has a single hook method whose name is the interface name prefixed with ng. For example, the OnInit interface has a hook method named ngOnInit
--
    
    hook method Details (https://www.youtube.com/watch?v=Qts7H8P-FpI)
    1 **ngOnChanges**    When an input or output binding value changes.Useful when there is lot of input components.It detects the new memory , referneced memory not detected.
    2 ngOnInit      After the first ngOnChanges.
    3 ngDoCheck     Developer's custom change detection.It detects the reference memory 
    4 ngAfterContentInit  After component content initialized.
    5 ngAfterContentChecked    After every check of component content.
    6 ngAfterViewInit     After the views of a component are initialized.
    7 ngAfterViewChecked   After every check of the views of a component.
    8 ngOnDestroy        Just before the directive is destroyed.Mostly used in statemanagement system or storing the value. Helps in Angular Observables also in the setTimeintervals also.

16. **Module**
In general, a module collects a block of code dedicated to a single purpose. Angular uses standard JavaScript modules and also defines an Angular module, NgModule.

In JavaScript, or ECMAScript, each file is a module and all objects defined in the file belong to that module. Objects can be exported, making them public, and public objects can be imported for use by other modules.

17. **Observable**
A producer of multiple values, which it pushes to subscribers. Used for asynchronous event handling throughout Angular. You execute an observable by subscribing to it with its subscribe() method, passing callbacks for notifications of new values, errors, or completion.

Observables can deliver in one the following ways a single value or multiple values of any type to subscribers.

Synchronously as a function delivers a value to the requester
Scheduled
A subscriber receives notification of new values as they are produced and notification of either normal completion or error completion.

Angular uses a third-party library named Reactive Extensions (RxJS). 

18. Observer:
An object passed to the subscribe() method for an observable. The object defines the callbacks for the subscriber.

19. **Pipe**
A class which is preceded by the @Pipe{} decorator and which defines a function that transforms input values to output values for display in a view. Angular defines various pipes, and you can define new pipes

20. **Platform**

In Angular terminology, a platform is the context in which an Angular application runs. The most common platform for Angular applications is a web browser, but it can also be an operating system for a mobile device, or a web server.

Support for the various Angular run-time platforms is provided by the @angular/platform-* packages. These packages allow applications that make use of @angular/core and @angular/common to execute in different environments by providing implementation for gathering user input and rendering UIs for the given platform. Isolating platform-specific functionality allows the developer to make platform-independent use of the rest of the framework.

When running in a web browser, BrowserModule is imported from the platform-browser package, and supports services that simplify security and event processing, and allows applications to access browser-specific features, such as interpreting keyboard input and controlling the title of the document being displayed. All applications running in the browser use the same platform service.

When server-side rendering (SSR) is used, the platform-server package provides web server implementations of the DOM, XMLHttpRequest, and other low-level features that do not rely on a browser.

21. **rective forms**
A framework for building Angular forms through code in a component. The alternative is a template-driven form.

When using reactive forms:

The "source of truth", the form model, is defined in the component class.
Validation is set up through validation functions rather than validation directives.
Each control is explicitly created in the component class by creating a FormControl instance manually or with FormBuilder.
The template input elements do not use ngModel.
The associated Angular directives are prefixed with form, such as formControl, formGroup, and formControlName.
The alternative is a template-driven form. For an introduction and comparison of both forms approaches, see Introduction to Angular Forms.

22. **resolver**(for dynamic data )
A class that implements the Resolve interface that you use to produce or retrieve data that is needed before navigation to a requested route can be completed. You may use a function with the same signature as the resolve() method in place of the Resolve interface. Resolvers run after all route guards for a route tree have been executed and have succeeded.

23. **SSR(Server Side Rendering)**
A technique that generates static application pages on the server, and can generate and serve those pages in response to requests from browsers. It can also pre-generate pages as HTML files that you serve later.

This technique can improve performance on mobile and low-powered devices and improve the user experience by showing a static first page quickly while the client-side application is loading. The static version can also make your application more visible to web crawlers.

You can easily prepare an application for server-side rendering by using the Angular CLI to run the Angular Universal tool, using the @nguniversal/express-engine schematic.
24. **Service**
In Angular, a class with the @Injectable() decorator that encapsulates non-UI logic and code that can be reused across an application. Angular distinguishes components from services to increase modularity and reusability.

The @Injectable() metadata allows the service class to be used with the dependency injection mechanism. The injectable class is instantiated by a provider. Injectors maintain lists of providers and use them to provide service instances when they are required by components or other services.

25. **subscriber**()
A function that defines how to obtain or generate values or messages to be published. This function is executed when a consumer runs the subscribe() method of an observable.

The act of subscribing to an observable triggers its execution, associates callbacks with it, and creates a Subscription object that lets you unsubscribe.

The subscribe() method takes an observer JavaScript object with up to three callbacks, one for each type of notification that an observable can deliver.

The next notification sends a value such as a number, a string, or an object.
The error notification sends a JavaScript Error or exception.
The complete notification does not send a value, but the handler is run when the method completes. Scheduled values can continue to be returned after the method completes.

26. **transpile**
The translation process that transforms one version of JavaScript to another version; for example, down-leveling ES2015 to the older ES5 version.

27. **ng-Content**
This one helps to get the Html values from the parent directly to apply in the child component using the <ng-content /ng-content> tags

28. why ng-form is used for ?
ngModel is typically used in template-driven forms.
In reactive forms, Angular uses FormControl and FormGroup instead, which provides more control and flexibility for managing form state and validation.

29. Behavioural
