---
id: 58a25bcff9fc0f352b528e7d
title: Асинхронне перетворення паролів на дані та їх порівняння
challengeType: 2
forumTopicId: 301578
dashedName: hash-and-compare-passwords-asynchronously
---

# --description--

Нагадуємо, що цей проєкт створюється на основі наступного стартового проєкту на <a href="https://replit.com/github/freeCodeCamp/boilerplate-bcrypt" target="_blank" rel="noopener noreferrer nofollow">Replit</a> або клонований з <a href="https://github.com/freeCodeCamp/boilerplate-bcrypt/" target="_blank" rel="noopener noreferrer nofollow">GitHub</a>.

Оскільки процес перетворення паролів на дані (хешування) вимагає великого об'єму обчислень, рекомендується виконувати його асинхронно на сервері, щоб запобігти блокуванню вхідних підключень під час хешування. Все, що вам необхідно зробити для асинхронного хешування пароля це ввести

```js
bcrypt.hash(myPlaintextPassword, saltRounds, (err, hash) => {
  /*Store hash in your db*/
});
```

# --instructions--

Додайте цю функцію хешування на свій сервер (ми вже визначили змінні для вас) та запишіть її в консоль, щоб побачити! Як правило на цьому етапі ви збережете функцію хешування у вашій базі даних.

Тепер коли вам необхідно з'ясувати чи нові вхідні дані відповідають даним перетворених паролів, використовуйте функцію порівняння.

```js
bcrypt.compare(myPlaintextPassword, hash, (err, res) => {
  /*res == true or false*/
});
```

Додайте це до наявної функції хешування (оскільки вам необхідно очікувати закінчення процесу перед тим як запускати функцію порівняння) після того, як ви записали про завершене хешування та ввели 'res' на консолі. На консолі з'являться дані перетворення та значення 'true'! Якщо ви зміните 'myPlaintextPassword' в функції порівняння на 'someOtherPlaintextPassword' - це призведе до помилки.

```js
bcrypt.hash('passw0rd!', 13, (err, hash) => {
  console.log(hash);
  //$2a$12$Y.PHPE15wR25qrrtgGkiYe2sXo98cjuMCG1YwSI5rJW1DSJp0gEYS
  bcrypt.compare('passw0rd!', hash, (err, res) => {
    console.log(res); //true
  });
});

```

Підтвердіть вашу сторінку, якщо все зрозуміло.

# --hints--

Асинхронне перетворення паролів на дані необхідно правильно згенерувати і правильно синхронізувати.

```js
(getUserInput) =>
  $.get(getUserInput('url') + '/_api/server.js').then(
    (data) => {
      assert.match(
        data,
        /START_ASYNC[^]*bcrypt.hash.*myPlaintextPassword( |),( |)saltRounds( |),( |).*err( |),( |)hash[^]*END_ASYNC/gi,
        'You should call bcrypt.hash on myPlaintextPassword and saltRounds and handle err and hash as a result in the callback'
      );
      assert.match(
        data,
        /START_ASYNC[^]*bcrypt.hash[^]*bcrypt.compare.*myPlaintextPassword( |),( |)hash( |),( |).*err( |),( |)res[^]*}[^]*}[^]*END_ASYNC/gi,
        'Nested within the hash function should be the compare function comparing myPlaintextPassword to hash'
      );
    },
    (xhr) => {
      throw new Error(xhr.statusText);
    }
  );
```

# --solutions--

```js
/**
  Backend challenges don't need solutions, 
  because they would need to be tested against a full working project. 
  Please check our contributing guidelines to learn more.
*/
```
