
# 2.5 Деструктуризация присваивания

В ES2015 появилась возможность **быстро присваивать значения** переменным из объектов и массивов.

## Пример в ES5
```javascript
var httpOptions = { timeout: 2000, isCache: true };
// позже
var httpTimeout = httpOptions.timeout;
var httpCache = httpOptions.isCache;
```

## Пример в ES2015 (объекты)
```javascript
const httpOptions = { timeout: 2000, isCache: true };
// позже
const { timeout: httpTimeout, isCache: httpCache } = httpOptions;
```
> Это может немного сбивать с толку: ключ — это свойство объекта, а значение — это переменная, которой присваивается значение.

### Сокращённая запись
Если имена переменных совпадают с именами свойств:
```javascript
const httpOptions = { timeout: 2000, isCache: true };
const { timeout, isCache } = httpOptions;
// создаются переменные timeout и isCache с соответствующими значениями
```

### Вложенные объекты
```javascript
const httpOptions = { timeout: 2000, cache: { age: 2 } };
const {
  cache: { age }
} = httpOptions;
// переменная age = 2
```

## Пример с массивами
```javascript
const timeouts = [1000, 2000, 3000];
const [shortTimeout, mediumTimeout] = timeouts;
// shortTimeout = 1000, mediumTimeout = 2000
```

## Применение: возврат нескольких значений
```javascript
function randomPonyInRace() {
  const pony = { name: 'Rainbow Dash' };
  const position = 2;
  return { pony, position };
}

const { position, pony } = randomPonyInRace();
```

Если позиция не нужна:
```javascript
const { pony } = randomPonyInRace();
```
