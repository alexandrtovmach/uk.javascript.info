# Коментарі

Як нам відомо з розділу <info:structure>, коментарі можна писати як на одному рядку: починаючи його з `//` так і на декількох рядках, розділяючи їх за допомогою `/* ... */`.

Зазвичай ми використовуємо коментарі для опису того, як і чому наш код працює.

На перший погляд, коментування може здаватись очевидним, проте початківці часто використовують їх неправильно.

## Погані коментарі

Початківці намагаються використовувати коментарі, щоб пояснити "що саме відбувається у коді". Наприклад:

```js
// Цей код зробить це (...) а потім ось це (...)
// ...і хто знає що ще...
дуже;
складний;
код;
```

Проте в якісному коді, кількість таких "пояснювальних" коментарів повинна бути мінімальною. Серйозно, код повинен бути зрозумілим без них.

Є хороше правило з приводу цього: "якщо код настільки не зрозумілий, що потребує коментарів, можливо його краще переписати".

### Рецепт: виносьте код у функції

Іноді має сенс замінити частину коду на функцію, наприклад:

```js
function showPrimes(n) {
  nextPrime:
  for (let i = 2; i < n; i++) {

*!*
    // перевірка чи є `i` простим числом
    for (let j = 2; j < i; j++) {
      if (i % j == 0) continue nextPrime;
    }
*/!*

    alert(i);
  }
}
```

Кращим варінтом було б помістити код в окрему функцію `isPrime`:


```js
function showPrimes(n) {

  for (let i = 2; i < n; i++) {
    *!*if (!isPrime(i)) continue;*/!*

    alert(i);
  }
}

function isPrime(n) {
  for (let i = 2; i < n; i++) {
    if (n % i == 0) return false;
  }

  return true;
}
```

Тепер ми можемо легко зрозуміти код. Сама функція замінила нам коментар. Такий код називається *самоописним*.

### Рецепт: створюйте функції

І якщо ми маємо такий довгий фрагмент коду:

```js
// тут ми додаємо віскі
for(let i = 0; i < 10; i++) {
  let drop = getWhiskey();
  smell(drop);
  add(drop, glass);
}

// тут ми додаємо сік
for(let t = 0; t < 3; t++) {
  let tomato = getTomato();
  examine(tomato);
  let juice = press(tomato);
  add(juice, glass);
}

// ...
```

Тоді кращим варінтом буде замінити його на окремі функції:

```js
addWhiskey(glass);
addJuice(glass);

function addWhiskey(container) {
  for(let i = 0; i < 10; i++) {
    let drop = getWhiskey();
    //...
  }
}

function addJuice(container) {
  for(let t = 0; t < 3; t++) {
    let tomato = getTomato();
    //...
  }
}
```

Знову ж таки, ім'я функцій самі описують, що в них відбувається. Немає потреби коментувати такий код. Також кращою є структура коду, коли він розподілений. Стає зрозумілим, що функція робить, що вона приймає і що повертає.

Насправді, ми не можемо уникнути повністю "пояснювальних" коментарів. Є складні алгоритми. Також існують деякі "прийоми" для оптимізації. Проте, як правило, ми повинні намагатись залишати код простим та самоописним.

## Хороші коментарі

Тож, пояснювальні коментарі зазвичай погані. Які ж тоді хороші?

Описуйте архітектуру
: Додавайте опис компонентів висого рівня, як вони взаємодіють, який потік управління мають у різних обставинах... Якщо коротко - огляд коду з висоту пташиного польоту. Є спеціальна мова [UML](https://uk.wikipedia.org/wiki/Unified_Modeling_Language) для побудови діаграм високорівневої архітектури коду. Її однозначно варто вчити.

Документуйте параметри функції та її використання
: Існує спеціальний синтаксис [JSDoc](https://uk.wikipedia.org/wiki/JSDoc) для документації функції: її використання, параметри, значення, що повертає.

Наприклад:
    
```js
/**
 * повертає x у n-й степені.
 *
 * @param {number} x число, що треба піднести до степеня.
 * @param {number} n cтепінь, повинно бути натуральним числом.
 * @return {number} x піднесене у n-нну степінь.
 */
function pow(x, n) {
  ...
}
```

Такі коментарі дозволяють нам зрозуміти мету функції та використовувати її правильно без потреби зазирати у її код.

До речі, багато редакторів, наприклад [WebStorm](https://www.jetbrains.com/webstorm/) можуть їх розуміти та використовувати для автодоповнення і деякої автоматичної перевірки коду.

Також є інструменти, наприклад [JSDoc 3](https://github.com/jsdoc3/jsdoc), які можуть генерувати HTML-документацію з коментарів. Ви можете почитати більше про JSDoc тут: <http://usejsdoc.org/>.

Чому завдання було вирішено у такий спосіб?
: Те, що написано є дуже важливим. Проте, те, що *не* написано може бути ще більш важливим, щоб зрозуміти, що саме відбувається. Чому завдання було вирішено саме у такий спосіб? Код не дає відповідь на це питання.

Якщо існує декілька способів вирішення завдання, чому саме цей? Особливо, якщо цей спосіб не самий очевидний.

Без таких коментарів можлива наступна ситуація:
1. Ви (або ваш колега) відкриває код, написаний колись раніше, і бачить, що він "неоптимальний".
2. Ви думаєте: "Який я був недосвідчений, і наскільки розумнішим я став зараз", і переписуєте код використовуючи "більш очевидний і правильний" варіант.
3. ...Бажання переписати код було хорошим. Але в процесі ви помічаєте, що "більш очевидне" рішення не є оптимальним. Ви навіть смутно пригадуєте чому воно так, тому що колись давно вже намаглись спробувати такий варіант. Ви вертаєте правильне рішення, проте час було витрачено даремно.

Коментарі, які пояснюють рішення є дуже важливими. Вони допомагають продовжувати розробку правильним шляхом.

Чи є якісь тонкощі у коді? Де вони використовуються?
: Якщо код має якісь тонкощі та неочевидні речі, його точно варто коментувати.

## Підсумки

Коментарі є важливою ознакою хорошого розробника: як їх наявність, так і їх відсутність.

Хороші коментарі полегшують нам підтримку коду, вертатись до нього через деякий час та використовувати його більш ефективно.

**Коментуйте наступне:**

- Загальну архітектуру, опис "високого рівня".
- Використання функцій.
- Важливі рішення, особливо, якщо вони не є очевидним.

**Уникайте коментарі:**

- Які описують, як код працює і що він робить.
- Пишіть їх тільки у тому випадку, коли не має змоги написати простий та самоописний код, якому пояснення не потрібні.

Коментарі також використовуються інструментами для автоматичної генерації документації, наприклад JSDoc3 - вони читають їх та генерують HTML-документи (або документи у іншому форматі).
