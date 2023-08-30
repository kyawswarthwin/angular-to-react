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
