
# 2.7 Оператор rest

ES2015 вводит новый синтаксис для определения переменного числа параметров в функциях.

## До ES2015
Дополнительные аргументы можно было получить через специальную переменную `arguments`:
```javascript
function addPonies(ponies) {
  for (var i = 0; i < arguments.length; i++) {
    poniesInRace.push(arguments[i]);
  }
}
addPonies('Rainbow Dash', 'Pinkie Pie');
```
> Неочевидно, что можно передавать несколько значений, и параметр `ponies` не используется напрямую.

## Rest-параметры
```javascript
function addPonies(...ponies) {
  for (let pony of ponies) {
    poniesInRace.push(pony);
  }
}
```
Теперь `ponies` — это **настоящий массив**, по которому можно итерироваться.  
Здесь используется цикл `for...of`, который проходит именно по значениям коллекции (в отличие от `for...in`, который проходит по свойствам).

### Rest в деструктуризации
```javascript
const [winner, ...losers] = poniesInRace;
// winner = первый элемент массива
// losers = массив остальных элементов
```

## Rest vs Spread
Rest-оператор не стоит путать со **spread-оператором**.  
Rest собирает элементы в массив, а spread наоборот — **раскрывает** массив в набор аргументов:
```javascript
const ponyPrices = [12, 3, 4];
const minPrice = Math.min(...ponyPrices);
```
