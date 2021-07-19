## Основные правила

https://github.com/airbnb/javascript

1. Использовать более понятные переменные в однострочных функциях (map, filter, reduce, ...)
2. Использовать alias в путях импорта
3. Использовать именованые экспорты/импорты
4. Избегать any / unknown
5. Типизировать приходящие с сервера данные
6. Использовать комментарии в коде для доработок и фиксов на будущее
7. Обязательно использование eslint и prettier

_(Контент дополняется)_

## Правила оформления компонентов

1. Делать компоненты небольшими и функциональными
2. Для нескольких классов использовать библиотеку classnames https://www.npmjs.com/package/classnames
3. Оформление функционального компонента (IComponent - интерфейс, описывающий пропсы):

```jsx
export const Component: React.FC<IComponent> = (props: IComponent): JSX.Element => { ... };
```
```jsx
export const Component: React.FC<IComponent> = React.memo((props: IComponent): JSX.Element => { ... });
```
4. Использовать только именованный экспорт, do not use `export default`
5. Название компонентов всегда с большой буквы, расширение только `.tsx`

## Структура папки src

Описаны только основные файлы и структура папки, если в приложении используется роутинг

- index.tsx
- index.css / index.scss
- App.tsx
- App.module.scss
- \_variables.scss - для хранения глобальных переменных
- \_general.scss - для хранения глобальных классов всего приложения
- types.ts - файл для хранения глобальных типов и интерфейсов
- const.ts - файл для хранения глобальных констант
- functions.ts - файл для хранения функций, используемых многими компонентами. Функции должны быть прокомментированны Если функций много, может быть преобразован в папку
- pages - компоненты, отвечающие за страницы приложения
- shared - компоненты, используемые на более чес одной странице
- redux - все файлы редакс
- services - сервисы
- assets/svg - используемые в компонентах svg файлы


## Структура папки с компонентом

/SomeComponent/

- index.ts - файл для импорта. `import { SomeComponent } from '~/shared/SomeComponent'`
- types.ts - файл для хранения типов и интерфейсов, используемых только компонентом и его дочерними компонентами в этой папке
- functions.ts - файл для хранения функций, используемых только компонентом и его дочерними компонентами в этой папке
- styles.module.scss - файл стилей
- SomeComponent.tsx - компонент
- SomeComponent.test.ts - файл тестирования компонента _(если предусмотрено тестирование)_
- /AnotherComponent - компонент, используемый только компонентом SomeComponent


### Пример простого компонента

index.ts

```jsx
export * from './SomeComponent';
export { User } from './types';

```

types.ts

```jsx
export type ButtonType = 'primary' | 'outlined' | 'error';

export type User = {
  id: number;
  name: string;
};

```

SomeComponent.tsx

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

## Структура redux

_(Дополняется)_
