
# 2.9. Промисы

Промисы — это не совсем новая концепция, и вы, возможно, уже знаете их или даже используете, так как они были важной частью AngularJS 1.x.  
Но так как в Angular вы будете активно использовать промисы, и даже если вы работаете только с JavaScript, важно сделать на них остановку.

Промисы призваны упростить асинхронное программирование. Наш JavaScript-код полон асинхронных операций, таких как AJAX-запросы, и обычно для обработки результата и ошибок мы используем обратные вызовы (callbacks).  
Но колбэки внутри колбэков создают беспорядок и делают код сложным для чтения и сопровождения.  
Промисы намного удобнее, так как они «выпрямляют» код и делают его легче для понимания.

Рассмотрим простой пример: нужно получить пользователя, затем его права и обновить меню.

## С использованием колбэков
```javascript
getUser(login, function (user) {
  getRights(user, function (rights) {
    updateMenu(rights);
  });
});
```

## С использованием промисов
```javascript
getUser(login)
  .then(function (user) {
    return getRights(user);
  })
  .then(function (rights) {
    updateMenu(rights);
  })
```
Мне нравится эта версия, потому что она выполняется так же, как читается:  
получить пользователя → получить его права → обновить меню.

---

Как видно, промис — это **thenable**-объект, то есть объект, у которого есть метод `then`.  
Этот метод принимает два аргумента: колбэк успешного завершения и колбэк ошибки.  

## Состояния промиса
- **pending** — промис ещё не завершён (например, запрос к серверу ещё выполняется).  
- **fulfilled** — промис успешно завершён (например, сервер вернул статус OK).  
- **rejected** — промис завершился с ошибкой (например, сервер вернул 404).

Когда промис успешно выполнен, вызывается success-колбэк с результатом в аргументе.  
Если промис отклонён, вызывается reject-колбэк с ошибкой или значением отклонения.

---

## Создание промиса
Очень просто: есть новый класс `Promise`, конструктор которого принимает функцию с двумя параметрами `resolve` и `reject`:
```javascript
const getUser = function (login) {
  return new Promise(function (resolve, reject) {
    // асинхронные действия, например запрос к серверу
    if (response.status === 200) {
      resolve(response.data);
    } else {
      reject('No user');
    }
  });
};
```

После создания промиса можно регистрировать колбэки с помощью метода `then`.  
Этот метод может принимать два параметра: колбэки для успеха и для ошибки.  
В этом примере передан только колбэк успеха:
```javascript
getUser(login)
  .then(function (user) {
    console.log(user);
  })
```
Когда промис будет выполнен, вызовется переданный колбэк (в данном случае — просто вывод данных пользователя в консоль).

---

## Цепочки промисов
Промисы делают код более «плоским». Например, если ваш колбэк `resolve` тоже возвращает промис, можно записать так:
```javascript
getUser(login)
  .then(function (user) {
    return getRights(user) // getRights возвращает промис
      .then(function (rights) {
        return updateMenu(rights);
      });
  })
```
но красивее:
```javascript
getUser(login)
  .then(function (user) {
    return getRights(user); // getRights возвращает промис
  })
  .then(function (rights) {
    return updateMenu(rights);
  })
```

---

## Обработка ошибок

### Обработка для каждого промиса
```javascript
getUser(login)
  .then(
    function (user) {
      return getRights(user);
    },
    function (error) {
      console.log(error); // вызовется, если getUser завершится с ошибкой
      return Promise.reject(error);
    }
  )
  .then(
    function (rights) {
      return updateMenu(rights);
    },
    function (error) {
      console.log(error); // вызовется, если getRights завершится с ошибкой
      return Promise.reject(error);
    }
  )
```

### Общая обработка для всей цепочки
```javascript
getUser(login)
  .then(function (user) {
    return getRights(user);
  })
  .then(function (rights) {
    return updateMenu(rights);
  })
  .catch(function (error) {
    console.log(error); // вызовется при любой ошибке в цепочке
  })
```

---

## Итог
Промисы серьёзно изменили подход к написанию API, и практически каждая библиотека их использует.  
Даже стандартные: например, **Fetch API** тоже возвращает промис.
