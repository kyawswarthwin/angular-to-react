# Angular to React

Angular Developer တွေ React ကို အချိန်တိုအတွင်း အလျှင်မြန်ဆုံးနဲ့ အလွယ်ကူဆုံး ကူးပြောင်းနိုင်ဖို့အတွက် ရည်ရွယ်ပီး ရေးသားထားခြင်း ဖြစ်ပါတယ်။

## ပါဝင်သည့်အကြောင်းအရာများ

[Scaffolding Project](#scaffolding-project)

[Developer Tools](#developer-tools)

[Passing Data from Parent to Child](#passing-data-from-parent-to-child)

[Passing Non-String Data from Parent to Child](#passing-non-string-data-from-parent-to-child)

[Dynamic Styling](#dynamic-styling)

[Conditional Rendering](#conditional-rendering)

[Rendering Lists](#rendering-lists)

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

## Dynamic Styling

**Angular**

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-hello',
  template: `<p [style]="{ backgroundColor, color }">Hello, World!</p>`,
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
function Hello({ backgroundColor, color }) {
  return <p style={{ backgroundColor, color }}>Hello, World!</p>;
}

function App() {
  return (
    <>
      <Hello backgroundColor="red" color="white" />
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

## Rendering Lists

**Angular**

```typescript
import { NgFor } from '@angular/common';
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-contact-list',
  template: `
    <ul>
      <li *ngFor="let name of list">{{ name }}</li>
    </ul>
  `,
  standalone: true,
  imports: [NgFor],
})
export class ContactListComponent {
  @Input() list?: string[];
}
```

```html
<app-contact-list
  [list]="['Ko Ko', 'Nyi Nyi', 'Kyaw Gyi', 'Mya Mya']"
></app-contact-list>
```

**React**

```typescript
function ContactList({ list }) {
  return (
    <ul>
      {list.map((name) => (
        <li>{name}</li>
      ))}
    </ul>
  );
}

function App() {
  return (
    <>
      <ContactList list={['Ko Ko', 'Nyi Nyi', 'Kyaw Gyi', 'Mya Mya']} />
    </>
  );
}

export default App;
```

အပေါ်က Code က အလုပ်လုပ်ပေမယ့် Chrome DevTools ထဲ ဝင်ကြည့်ရင် Warning: Each child in a list should have a unique "key" prop. ဆိုပီး Error ပြနေပါလိမ့်မယ်။ အကြောင်းက React မှာ array item တစ်ခုစီတိုင်းအတွက် unique identifier တစ်ခုစီ လိုအပ်ပါတယ်။ အဲ့တာကို “key” prop နဲ့ သတ်မှတ်နိုင်ပါတယ်။ အများအားဖြင့် Database က id ကို သတ်မှတ်ကျပါတယ်။ မရှိရင် uuid generator တွေသုံးလို့ဖြစ်စေ၊ အောက်က ဥပမာထဲကလို index နဲ့ဖြစ်စေ ဖြေရှင်းနိုင်ပါတယ်။

```typescript
function ContactList({ list }) {
  return (
    <ul>
      {list.map((name, index) => (
        // Key Prop
        <li key={index}>{name}</li>
      ))}
    </ul>
  );
}

function App() {
  return (
    <>
      <ContactList list={['Ko Ko', 'Nyi Nyi', 'Kyaw Gyi', 'Mya Mya']} />
    </>
  );
}

export default App;
```
