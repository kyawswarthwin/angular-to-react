# Angular to React

Angular Developer တွေ React ကို အချိန်တိုအတွင်း အလျှင်မြန်ဆုံးနဲ့ အလွယ်ကူဆုံး ကူးပြောင်းနိုင်ဖို့အတွက် ရည်ရွယ်ပီး ရေးသားထားခြင်း ဖြစ်ပါတယ်။

## ပါဝင်သည့်အကြောင်းအရာများ

[Scaffolding Project](#scaffolding-project)

[DevTools](#devtools)

[Passing Data from Parent to Child](#passing-data-from-parent-to-child)

[Passing Non-String Data from Parent to Child](#passing-non-string-data-from-parent-to-child)

[Dynamic Styling](#dynamic-styling)

[Conditional Rendering](#conditional-rendering)

[Rendering Lists](#rendering-lists)

[Handling Events](#handling-events)

[State Management](#state-management)

[Forms](#forms)

[Lifecycle Hooks](#lifecycle-hooks)

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

## DevTools

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

#### The Key Prop
အပေါ်က Code က အလုပ်လုပ်ပေမယ့် Chrome DevTools ထဲ ဝင်ကြည့်ရင် `Warning: Each child in a list should have a unique "key" prop.` ဆိုပီး Error ပြနေပါလိမ့်မယ်။ အကြောင်းက React မှာ array item တစ်ခုစီတိုင်းအတွက် unique identifier တစ်ခုစီ လိုအပ်ပါတယ်။ အဲ့တာကို “key” prop နဲ့ သတ်မှတ်နိုင်ပါတယ်။ အများအားဖြင့် Database က id ကို သတ်မှတ်ကျလေ့ရှိပါတယ်။ မရှိရင် uuid generator တွေသုံးလို့ဖြစ်စေ၊ အောက်က ဥပမာထဲကလို index နဲ့ဖြစ်စေ ဖြေရှင်းနိုင်ပါတယ်။

```typescript
function ContactList({ list }) {
  return (
    <ul>
      {list.map((name, index) => (
        // React Key Prop
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

## Handling Events

**Angular**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: '<button (click)="handleClick()">Click me</button>',
})
export class AppComponent {
  handleClick() {
    alert('You clicked me!');
  }
}
```

**React**

```typescript
function App() {
  function handleClick() {
    alert('You clicked me!');
  }

  return (
    <>
      <button onClick={handleClick}>Click me</button>
    </>
  );
}

export default App;
```

## State Management

**Angular**

Angular Signals မတိုင်ခင်က Angular မှာ State Management အတွက် zone.js ကိုသုံးပါတယ်။ Angular Component တွေမှာ Mutable State ရှိနေပီးသားပါ။ အဲ့တော့ Angular မှာ React လို setState မလိုအပ်ခဲ့ဘူး။ Solid.js ကစခဲ့တဲ့ Signals ဟာ Angular 16 မှာ ပါဝင်လာပီဖြစ်ပါတယ်။ Signals သုံးတဲ့ တစ်ခြား Framework တစ်ခုလဲရှိပါသေးတယ်။ အဲ့တာက Qwik ပါ။ Angular ကို ထွင်တဲ့အဖွဲ့ထဲက Misko Hevery ကပဲ ထပ်ထွင်ထားတာပါ။

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <button (click)="count = count + 1">count is {{ count }}</button>
  `,
})
export class AppComponent {
  count: number = 0;
}
```

**Angular Signals**

```typescript
import { Component, signal } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<button (click)="handleClick()">count is {{ count() }}</button>`,
})
export class AppComponent {
  count = signal(0);

  handleClick() {
    this.count.update((value) => value + 1);
  }
}
```

**React**

```typescript
import { useState } from 'react';

function App() {
  const [count, setCount] = useState(0);

  return (
    <>
      <button onClick={() => setCount((count) => count + 1)}>
        count is {count}
      </button>
    </>
  );
}

export default App;
```

#### Updating Arrays in State
JavaScript မှာ Array တွေက Mutable ဖြစ်တယ်။ Angular Component တွေမှာ Mutable State ရှိနေပီးသား ဖြစ်တဲ့အတွက် Mutate ဖြစ်လို့ရတယ်။ React မှာတော့ Array တွေကို Add, Remove, Replace နဲ့ Sort လုပ်တဲ့အခါ Mutate ဖြစ်စေမယ့်အရာတွေကို ရှောင်ရှားဖို့လိုတယ်။

[အသေးစိတ်လေ့လာရန်](https://react.dev/learn/updating-arrays-in-state)

## Forms

**Angular**

Angular မှာ Reactive forms နဲ့ Template-driven forms ဆိုပီး ရေးပုံရေးနည်း ၂ နည်းရှိပါတယ်။

[အသေးစိတ်လေ့လာရန်](https://angular.io/guide/forms-overview)

**React**

React မှာတော့ Angular လို built-in form validation စနစ် မပါဝင်ပါဘူး။ Don't reinvent the wheel ဆိုတဲ့အတိုင်း ကိုယ်တိုင်ရေးမယ့်အစား 3rd party librarie တွေကို အသုံးပြုကြပါတယ်။ အဲ့ဒီ့ထဲမှာ React Hook Form နဲ့ Formik ကအသုံးများပါတယ်။

[React Hook Form](https://www.react-hook-form.com/)

[Formik](https://formik.org/)

## Lifecycle Hooks

**Angular**

ngOnInit, ngOnChanges, ngOnDestroy တို့အကြောင်းကို အောက်ပါ Link မှာ အသေးစိတ် ဖတ်ပါ။

[အသေးစိတ်လေ့လာရန်](https://angular.io/guide/lifecycle-hooks)

**React**
