# async-await

Мы уже говорили о промисах ранее, и стоит знать, что был введён ещё один ключевой оператор для их более синхронной обработки: `await`.

Эта функция появилась не в ECMAScript 2015, а в ECMAScript 2017, и для использования `await` ваша функция должна быть помечена как `async`.  
Когда вы используете ключевое слово `await` перед промисом, выполнение вашей асинхронной функции приостанавливается, ожидает завершения промиса и затем возобновляется.  
Возвращаемое значение будет значением, с которым промис завершился.

Таким образом, мы можем переписать наш предыдущий пример, используя `async/await`, вот так:

```javascript
async function getUserRightsAndUpdateMenu() {
  // getUser возвращает промис
  const user = await getUser(login);
  // getRights возвращает промис
  const rights = await getRights(user);
  updateMenu(rights);
}
await getUserRightsAndUpdateMenu();
```

И теперь ваш код выглядит как синхронный!  
Ещё одна крутая особенность `async/await` заключается в том, что вы можете использовать простой `try/catch` для обработки ошибок:

```javascript
async function getUserRightsAndUpdateMenu() {
  try {
    // getUser возвращает промис
    const user = await getUser(login);
    // getRights возвращает промис
    const rights = await getRights(user);
    updateMenu(rights);
  } catch (e) {
    // будет вызвано, если getUser, getRights или updateMenu завершатся с ошибкой
    console.log(e);
  }
}
await getUserRightsAndUpdateMenu();
```

Обратите внимание, что `async/await` всё ещё остаётся асинхронным, несмотря на синхронный вид.  
Выполнение функции приостанавливается и возобновляется, но, как и при использовании колбэков, это не блокирует поток: другие события JavaScript могут обрабатываться, пока выполнение приостановлено.
