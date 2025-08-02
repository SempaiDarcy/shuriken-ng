
# 2.2 let

Если вы уже какое-то время пишете на JavaScript, то знаете, насколько `var` сложно декларировать переменную.  
Практически в любом другом языке переменная объявляется там, где её объявляют.  
Но в JavaScript есть концепция «поднятия» (hoisting), которая фактически объявляет переменную 
в начале функции, даже если вы объявили её позже.

## Пример с var
```javascript
function getPonyFullName(pony) {
  if (pony.isChampion) {
    var name = 'Champion ' + pony.name;
    return name;
  }
  return pony.name;
}
```
Эквивалентно объявлению в верхней части функции:
```javascript
function getPonyFullName(pony) {
  var name;
  if (pony.isChampion) {
    name = 'Champion ' + pony.name;
    return name;
  }
  // name доступна здесь
  return pony.name;
}
```

## Пример с let (ES2015)
```javascript
function getPonyFullName(pony) {
  if (pony.isChampion) {
    let name = 'Champion ' + pony.name;
    return name;
  }
  // name здесь не доступна
  return pony.name;
}
```

Переменная `name` теперь ограничена своим блоком.  
`let` была введена для замены `var` в долгосрочной перспективе, так что можно практически отказаться 
от использования старого `var` и начать использовать `let`.  
Самое замечательное, что использовать `let` легко, а если у вас это не получается, 
вы, вероятно, заметили ошибку в коде!
