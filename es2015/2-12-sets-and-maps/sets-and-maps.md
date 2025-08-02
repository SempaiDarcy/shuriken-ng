# sets-and-maps

Это короткая глава: теперь в ES2015 появились полноценные коллекции. Ура \o/!  
Раньше мы использовали обычные объекты как словари для роли карты (map), но теперь у нас есть класс `Map`:

```javascript
const cedric = { id: 1, name: 'Cedric' };
const users = new Map();
users.set(cedric.id, cedric); // добавляем пользователя
console.log(users.has(cedric.id)); // true
console.log(users.size); // 1
users.delete(cedric.id); // удаляем пользователя
```

Также у нас есть класс `Set`:

```javascript
const cedric = { id: 1, name: 'Cedric' };
const users = new Set();
users.add(cedric); // добавляем пользователя
console.log(users.has(cedric)); // true
console.log(users.size); // 1
users.delete(cedric); // удаляем пользователя
```

Вы можете перебирать коллекцию с помощью нового синтаксиса `for...of`:

```javascript
for (let user of users) {
  console.log(user.name);
}
```

Вы увидите, что синтаксис `for...of` именно тот, который команда Angular выбрала для перебора коллекций в шаблоне.
