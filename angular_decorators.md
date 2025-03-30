
# Angular Decorators: @Input, @Output, and @ViewChild

## 1. @Input Decorator
The `@Input` decorator is used to pass data from a parent component to a child component.

### Example:
#### Parent Component (`app.component.ts`)
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<app-child [message]="parentMessage"></app-child>`
})
export class AppComponent {
  parentMessage = "Hello from Parent!";
}
```

#### Child Component (`child.component.ts`)
```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<p>Message from parent: {{ message }}</p>`
})
export class ChildComponent {
  @Input() message: string = '';
}
```

---

## 2. @Output Decorator
The `@Output` decorator allows a child component to send events/data to its parent component.

### Example:
#### Parent Component (`app.component.ts`)
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<app-child (childEvent)="receiveMessage($event)"></app-child>
             <p>Message from child: {{ receivedMessage }}</p>`
})
export class AppComponent {
  receivedMessage = '';

  receiveMessage(message: string) {
    this.receivedMessage = message;
  }
}
```

#### Child Component (`child.component.ts`)
```typescript
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<button (click)="sendMessage()">Send Message</button>`
})
export class ChildComponent {
  @Output() childEvent = new EventEmitter<string>();

  sendMessage() {
    this.childEvent.emit("Hello from Child!");
  }
}
```

---

## 3. @ViewChild Decorator
The `@ViewChild` decorator allows access to child components or elements inside the parent component.

### Example:
#### Parent Component (`app.component.ts`)
```typescript
import { Component, ViewChild, AfterViewInit } from '@angular/core';
import { ChildComponent } from './child.component';

@Component({
  selector: 'app-root',
  template: `<app-child></app-child>
             <button (click)="changeChildText()">Change Child Text</button>`
})
export class AppComponent implements AfterViewInit {
  @ViewChild(ChildComponent) child!: ChildComponent;

  ngAfterViewInit() {
    console.log("Child Component Loaded:", this.child);
  }

  changeChildText() {
    this.child.message = "Updated by Parent!";
  }
}
```

#### Child Component (`child.component.ts`)
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<p>{{ message }}</p>`
})
export class ChildComponent {
  message = "Initial Child Message";
}
```

---

## Summary:
- `@Input`: Used to pass data from **parent to child**.
- `@Output`: Used to send data/events from **child to parent**.
- `@ViewChild`: Used to get a reference to a **child component or DOM element** in the parent component.

These decorators are crucial in component communication and are widely used in real-world Angular applications.

