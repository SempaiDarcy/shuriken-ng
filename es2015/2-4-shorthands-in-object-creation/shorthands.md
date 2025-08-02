
# 2.4 Shorthands in object creation

В ES2015 появилась возможность создавать объекты с сокращённой записью свойств и методов,
если имя переменной совпадает с именем свойства.

## Пример (до ES2015)
```javascript
function createPony() {
  const name = 'Rainbow Dash';
  const color = 'blue';
  return { name: name, color: color };
}
```

## Пример (ES2015)
```javascript
function createPony() {
  const name = 'Rainbow Dash';
  const color = 'blue';
  return { name, color };
}
```

## Методы в объектах
Также можно сокращённо определять методы объекта.

### До ES2015
```javascript
function createPony() {
  return {
    run: () => {
      console.log('Run!');
    }
  };
}
```

### ES2015
```javascript
function createPony() {
  return {
    run() {
      console.log('Run!');
    }
  };
}
```
