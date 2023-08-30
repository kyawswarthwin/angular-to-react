## Scaffolding Project

#### Angular

```sh
npm install -g @angular/cli
ng new my-first-project
```

#### React

```sh
npm create vite@latest my-first-project -- --template react
```

## Fragment

#### Angular

```html
<ng-container>
</ng-container>
```

#### React

```html
<>
</>
```

## Passing Data from Parent to Child
#### Angular

```typescript
@Input()
```

#### React

```typescript
// React Props
function ParentComponent() {
  return <ChildComponent message="Hello from parent" />;
}

function ChildComponent(props) {
  return <div>{props.message}</div>;
}
```

## Passing Non-String Data from Parent to Child
#### Angular

```html
<child-component [age]="17"></child-component>
```

#### React

```typescript
// React Non-String Props
function ParentComponent() {
  return <ChildComponent age={17} />;
}

function ChildComponent(props) {
  return <div>{props.age}</div>;
}
```
