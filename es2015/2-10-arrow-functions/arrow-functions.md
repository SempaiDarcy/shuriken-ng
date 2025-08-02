
# 2.10. Стрелочные функции

Одна из вещей, которая мне очень нравится в ES2015, — это новый синтаксис стрелочных функций с использованием оператора «толстая стрелка» (`=>`). Он ТАК полезен для обратных вызовов и анонимных функций!

Давайте возьмём наш предыдущий пример с промисами:

```javascript
getUser(login)
  .then(function (user) {
    return getRights(user); // getRights возвращает промис
  })
  .then(function (rights) {
    return updateMenu(rights);
  })
```

Это можно записать с помощью стрелочных функций следующим образом:

```javascript
getUser(login)
  .then(user => getRights(user))
  .then(rights => updateMenu(rights))
```

Как это круто? ОЧЕНЬ круто!

Обратите внимание, что возврат также неявный, если отсутствует блок: нет необходимости писать `user => return getRights(user)`. Но если блок есть, то возврат нужно писать явно:

```javascript
getUser(login)
  .then(user => {
    console.log(user);
    return getRights(user);
  })
  .then(rights => updateMenu(rights))
```

У стрелочных функций есть особая «фишка», дающая им огромное преимущество перед обычными функциями: `this` остаётся лексически привязанным, что означает, что такие функции не создают новое значение `this`, как это делают обычные функции. Рассмотрим пример, когда вы итерируете массив с помощью функции `forEach`, чтобы найти максимум.

## В ES5:

```javascript
var maxFinder = {
  max: 0,
  find: function (numbers) {
    // итерация
    numbers.forEach(function (element) {
      // если элемент больше, устанавливаем его как максимум
      if (element > this.max) {
        this.max = element;
      }
    });
  }
};

maxFinder.find([2, 3, 4]);
// вывод результата
console.log(maxFinder.max);
```

Можно ожидать, что это сработает, но нет. Если вы внимательны, вы могли заметить, что `forEach` в функции `find` использует `this`, но `this` не привязан к объекту. Поэтому `this.max` не является `max` объекта `maxFinder`… Конечно, это можно легко исправить, используя псевдоним:

```javascript
var maxFinder = {
  max: 0,
  find: function (numbers) {
    var self = this;
    numbers.forEach(function (element) {
      if (element > self.max) {
        self.max = element;
      }
    });
  }
};

maxFinder.find([2, 3, 4]);
// вывод результата
console.log(maxFinder.max);
```

или связывание `this`:

```javascript
var maxFinder = {
  max: 0,
  find: function (numbers) {
    numbers.forEach(
      function (element) {
        if (element > this.max) {
          this.max = element;
        }
      }.bind(this)
    );
  }
};

maxFinder.find([2, 3, 4]);
// вывод результата
console.log(maxFinder.max);
```

или даже передача его как второго параметра функции `forEach` (как это и было задумано):

```javascript
var maxFinder = {
  max: 0,
  find: function (numbers) {
    numbers.forEach(function (element) {
      if (element > this.max) {
        this.max = element;
      }
    }, this);
  }
};

maxFinder.find([2, 3, 4]);
// вывод результата
console.log(maxFinder.max);
```

Но теперь есть ещё более элегантное решение с использованием синтаксиса стрелочных функций:

```javascript
const maxFinder = {
  max: 0,
  find: function (numbers) {
    numbers.forEach(element => {
      if (element > this.max) {
        this.max = element;
      }
    });
  }
};

maxFinder.find([2, 3, 4]);
// вывод результата
console.log(maxFinder.max);
```

Это делает стрелочные функции отличным кандидатом для анонимных функций в обратных вызовах!
