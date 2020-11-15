# 🏷 Typed `querySelector`

`querySelector` and `querySelectorAll` functions with better typing
by leveraging TypeScript 4.1 template literal type.

## 💿 Install

```
npm i typed-query-selector
```

## 🍉 Usage

### Automatic shim

All you need to do is to import this module,
then the `querySelector` and `querySelectorAll` function will be enhanced.

```typescript
import 'typed-query-selector'

document.querySelector('div#app') // ==> HTMLDivElement

document.querySelector('div#app > form#login') // ==> HTMLFormElement

document.querySelectorAll('span.badge') // ==> NodeListOf<HTMLSpanElement>

anElement.querySelector('button#submit') // ==> HTMLButtonElement
```

If you aren't going to use ES Modules you can modify your `tsconfig.json`,
however this is NOT recommended, unless you know what you're doing.

```json
{
  "compilerOptions": {
    "types": ["typed-query-selector"]
  }
}
```

### Use the parser

If you just want to use the selector parser itself, we've exported for you:

```typescript
import type { ParseSelector } from 'typed-query-selector/parser'

type MyElement = ParseSelector<'form#login'>
```

Please note that you should import `typed-query-selector/parser`, not `typed-query-selector`.
This is safe because this import doesn't patch to the `querySelector` and `querySelectorAll` function.

## 💡 Supported Use Cases

### With class, ID or attribute

```typescript
import { querySelector } from 'typed-query-selector'

querySelector('div.container') // ==> HTMLDivElement

querySelector('div#app') // ==> HTMLDivElement

querySelector('input[name=username]') // ==> HTMLInputElement
```

Even mix them:

```typescript
import { querySelector } from 'typed-query-selector'

querySelector('input.form-control[name=username]') // ==> HTMLInputElement
```

### Combinators

```typescript
import { querySelector } from 'typed-query-selector'

querySelector('body div') // ==> HTMLDivElement

querySelector('body > form') // ==> HTMLFormElement

querySelector('h1 + p') // ==> HTMLParagraphElement

querySelector('h2 ~ p') // ==> HTMLParagraphElement
```

### Grouping selectors

```typescript
import { querySelector } from 'typed-query-selector'

querySelector('div, span') // ==> HTMLDivElement | HTMLSpanElement
```

### Fallback

#### Web Components

If you passed an unknown tag, it will fall back to `Element`,
but you can override it by specifying concrete type.

```typescript
import { querySelector } from 'typed-query-selector'

querySelector('my-web-component') // ==> Element

querySelector<MyComponent>('my-web-component') // ==> MyComponent
```

#### Invalid selector

When passing an invalid selector which causes parsing error,
it will fall back to `Element`.

```typescript
import { querySelector } from 'typed-query-selector'

querySelector('div#app >') // ==> Element

querySelector('div#app ?') // ==> Element
```

## 📃 License

MIT License

Copyright (c) 2020-present Pig Fang
