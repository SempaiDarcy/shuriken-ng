# template-literals

Составление строк всегда было болезненным в JavaScript, так как обычно приходилось использовать конкатенацию:

```javascript
const fullname = 'Miss ' + firstname + ' ' + lastname;
```

**Template literals** — это небольшое новое улучшение, где вы используете обратные кавычки (`` ` ``) вместо кавычек или апострофов, и получаете базовую систему шаблонов с поддержкой многострочности:

```javascript
const fullname = `Miss ${firstname} ${lastname}`;
```

Поддержка многострочности особенно полезна при написании HTML-строк, что мы будем делать в наших Angular-компонентах:

```javascript
const template = `<div>
  <h1>Hello</h1>
</div>`;
```

Ещё одна функция — это возможность **тегировать** шаблонные строки. Вы можете определить функцию и применить её к шаблонной строке.  
Например, `askQuestion` добавляет знак вопроса в конце строки:

```javascript
const askQuestion = strings => strings + '?';
const template = askQuestion`Hello there`;
```

Чем это отличается от обычной функции?  
Тег-функция на самом деле получает несколько аргументов:

- массив статических частей строки
- значения, полученные в результате вычисления выражений

Например, если у нас есть шаблонная строка с выражениями:

```javascript
const person1 = 'Cedric';
const person2 = 'Agnes';
const template = `Hello ${person1}! Where is ${person2}?`;
```

то тег-функция получит различные статические и динамические части.  
Здесь у нас есть тег-функция, которая переводит имена участников в верхний регистр:

```javascript
const uppercaseNames = (strings, ...values) => {
  // `strings` — массив статических частей ['Hello ', '! Where is ', '?']
  // `values` — массив вычисленных выражений ['Cedric', 'Agnes']
  const names = values.map(name => name.toUpperCase());
  // `names` теперь ['CEDRIC', 'AGNES']
  // объединяем массивы `strings` и `names`
  return strings.map((string, i) => `${string}${names[i] ? names[i] : ''}`).join('');
};
const result = uppercaseNames`Hello ${person1}! Where is ${person2}?`;
// вернёт 'Hello CEDRIC! Where is AGNES?'
```

Теперь давайте поговорим об одном из крупных изменений, которые были введены: модули.
