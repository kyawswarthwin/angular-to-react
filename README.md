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

```html
<child-component [age]="17"></child-component>
```

**React**

```typescript
// React Non-String Props
function ParentComponent() {
  return <ChildComponent age={17} />;
}

function ChildComponent(props) {
  return <div>{props.age}</div>;
}
```
