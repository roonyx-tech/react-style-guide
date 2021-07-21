## Core rules

We are following https://github.com/airbnb/javascript style guide in general.


1. Use meaningful names for one-line functions, like `map`,`filter, `reduce`.
1. Use aliases for import path.
1. Use named imports/exports.
1. Try to avoid `any` / `unknown`. 
1. Define types for data retrieved from server.
1. Use `@todo` and `@hack` comments for future improvements and fixes.
1. Always use `eslint` and `prettier`.

🚧 _Content is under development._

---

## Component guidelines

1. Keep components small and functional.
1. Use [classname](https://www.npmjs.com/package/classnames) package for defining multiple css classes.

1. Always use named export, avoid `export default`.
1. Use `UpperCamelCase` for files containing components.
1. Use `.tsx` extension for components

### Functional component template

```jsx
// Defines props types
export interface IComponent {
}

export const Component: React.FC<IComponent> = (props: IComponent): JSX.Element => { ... };
```


```jsx
export const Component: React.FC<IComponent> = React.memo((props: IComponent): JSX.Element => { ... });
```

### Component folder structure 

`/SomeComponent/` folder content:

- `index.ts` - should re-export component and used for imports, e.g. `import { SomeComponent } from '~/shared/SomeComponent'`
- `types.ts` - should contain types and interfaces used for component and it's child components (which should be placed in the same folder).
- `functions.ts` - same thing, but for functions.
- `styles.module.scss` - component styles.
- `SomeComponent.tsx` - component itself.
- `SomeComponent.test.ts` - file for component specs _(if necessary)_
- `/AnotherComponent` - folder for child component, used only as part of `SomeComponent`

#### Component example

`index.ts` file:

```jsx
export * from './SomeComponent';
export { User } from './types';

```

`types.ts` file:

```jsx
export type ButtonType = 'primary' | 'outlined' | 'error';

export type User = {
  id: number;
  name: string;
};

```

`SomeComponent.tsx` file:

```jsx
import React, { useState } from 'react';
import cn from 'classnames';

import { AnotherComponent } from './AnotherComponent';
import { ButtonType, User } from './types';
import s from './SomeComponent.module.scss';

interface ISomeComponentProps {
  users: User[];
  onSelectUser: (userId: number) => void;
  onDelete: () => void;
  type?: ButtonType;
  className?: string;
  disabled?: boolean;
}

export const SomeComponent: React.FC<ISomeComponentProps> = (props: ISomeComponentProps): JSX.Element => {
  const { children, users, onSelectUser, className, type = 'primary', onDelete, disabled } = props;
  const [count, setCount] = useState<number>(0);

  return (
    <>
      {users.map((user: User) => (
        <AnotherComponent
          key={user.id}
          username={user.name}
          onClick={() => onSelectUser(user.id)}
        />
      ))}

      {/* Some code */}

      <button onClick={onDelete} className={cn(s.button, { [s.disabled]: disabled }, className)}>
        {children}
      </button>
    </>
  );
};
```


## Project structure

Describes only core files and folders assuming that project uses routing.

`/src/` folder content:
- `index.tsx`
- `index.css / index.scss`
- `App.tsx`
- `App.module.scss`
- `\_variables.scss` - use for global variables
- `\_general.scss` - use for global classes
- `types.ts` - use for global types and interfaces
- `const.ts` - use for global constants
- `functions.ts` - use for reusable functions. Always comment all functions. In case of unexpected growth we prefer to create folder instead and separate functions to multiple files.
- `pages` - use for components responsible for app pages.
- `shared` - use for shared components.
- `redux` - use for redux related files.
- `services` - use for services.
- `assets/svg` - use for `svg` files.

## Redux structure

🚧 _Content is under development._
