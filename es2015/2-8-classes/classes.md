
# 2.8 Классы

ES2015 ввёл поддержку **классов** в JavaScript. Ранее использовалась прототипная модель наследования,
но её было сложно понять начинающим разработчикам. Теперь синтаксис стал проще и привычнее.

## Объявление класса
```javascript
class Pony {
  constructor(color) {
    this.color = color;
  }

  toString() {
    return `${this.color} pony`;
    // использование шаблонных строк (template literals)
  }
}

const bluePony = new Pony('blue');
console.log(bluePony.toString()); // blue pony
```
> В отличие от функций, объявления классов **не поднимаются** (hoisting), поэтому их нужно определять до использования.

## Статические методы
```javascript
class Pony {
  static defaultSpeed() {
    return 10;
  }
}

const speed = Pony.defaultSpeed(); // 10
```
> Статические методы вызываются на самом классе, а не на его экземплярах.

## Геттеры и сеттеры
```javascript
class Pony {
  get color() {
    console.log('get color');
    return this._color;
  }

  set color(newColor) {
    console.log(`set color ${newColor}`);
    this._color = newColor;
  }
}

const pony = new Pony();
pony.color = 'red';   // set color red
console.log(pony.color); // get color → red
```

## Наследование
```javascript
class Animal {
  speed() {
    return 10;
  }
}
class Pony extends Animal {}

const pony = new Pony();
console.log(pony.speed()); // 10 (унаследовано от Animal)
```

### Переопределение методов
```javascript
class Animal {
  speed() {
    return 10;
  }
}
class Pony extends Animal {
  speed() {
    return super.speed() + 10;
  }
}

const pony = new Pony();
console.log(pony.speed()); // 20
```
> `super` используется для вызова методов и конструкторов родительского класса.

### Использование super в конструкторах
```javascript
class Animal {
  constructor(speed) {
    this.speed = speed;
  }
}

class Pony extends Animal {
  constructor(speed, color) {
    super(speed);
    this.color = color;
  }
}

const pony = new Pony(20, 'blue');
console.log(pony.speed); // 20
```
