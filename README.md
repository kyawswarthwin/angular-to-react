# Angular to React
## Scaffolding Project

**Angular**

```sh
npm install -g @angular/cli
ng new my-angular-app
```

**React**

```sh
npm create vite@latest my-react-project -- --template react-ts
```

## Developer Tools

[Angular](https://chrome.google.com/webstore/detail/angular-devtools/ienfalfjdbdpebioblfackkekamfmbnh)

[React](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

## Fragment

**Angular**

```html
<ng-container>
</ng-container>
```

**React**

```html
<>
</>
```

## Passing Data from Parent to Child

**Angular**

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-hello',
  template: '<p>Hello, {{ name }}!</p>',
  standalone: true,
})
export class HelloComponent {
  @Input() name?: string;
}
```

```html
<app-hello name="Ko Ko"></app-hello>
```

**React**

```typescript
// React Props
function Hello(props) {
  return <p>Hello, {props.name}!</p>;
}

function App() {
  return (
    <>
      <Hello name="Ko Ko" />
    </>
  );
}

export default App;
```

## Passing Non-String Data from Parent to Child

**Angular**

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-hello',
  template: '<p>You are {{ age }} year(s) old.</p>',
  standalone: true,
})
export class HelloComponent {
  @Input() age?: number;
}
```

```html
<app-hello [age]="17"></app-hello>
```

**React**

```typescript
// React Non-String Props
function Hello(props) {
  return <p>You are {props.age} year(s) old.</p>;
}

function App() {
  return (
    <>
      <Hello age={17} />
    </>
  );
}

export default App;
```

## Conditional Rendering

**Angular**

```typescript
import { NgIf } from '@angular/common';
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-hello',
  template: '<p>You are {{ age }} year<span *ngIf="age! > 1">s</span> old.</p>',
  standalone: true,
  imports: [NgIf],
})
export class HelloComponent {
  @Input() age?: number;
}
```

```html
<app-hello [age]="1"></app-hello>
```

**React**

```typescript
function Hello({ age }) {
  return (
    <p>
      You are {age} year{age > 1 && <span>s</span>} old.
    </p>
  );
}

function App() {
  return (
    <>
      <Hello age={1} />
    </>
  );
}

export default App;
```

## Dynamic Styling

**Angular**

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-hello',
  template: `
    <p [style]="{ backgroundColor: backgroundColor, color: color }">
      Hello, World!
    </p>
  `,
  standalone: true,
})
export class HelloComponent {
  @Input() backgroundColor?: string;
  @Input() color?: string;
}
```

```html
<app-hello backgroundColor="red" color="white"></app-hello>
```

**React**

```typescript
function Hello({ age }) {
  return (
    <p>
      You are {age} year{age > 1 && <span>s</span>} old.
    </p>
  );
}

function App() {
  return (
    <>
      <Hello age={1} />
    </>
  );
}

export default App;
```
