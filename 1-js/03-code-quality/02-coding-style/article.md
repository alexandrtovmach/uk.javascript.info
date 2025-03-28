# Стандарт оформлення коду

Наш код повинен бути настільки зрозумілим та читабельним, наскільки це можливо.

Насправді, мистецтво програмування — це брати складну задачу і писати код, який одночасно і вирішує задачу, і залишається зрозумілим людині. Саме тут хороший стиль коду стає у нагоді.

## Синтаксис

Деякі запропоновані правила наведені у цій шпаргалці (*нижче розписано більш детально*):

![](code-style.svg)
<!--
```js
function pow(x, n) {
  let result = 1;

  for (let i = 0; i < n; i++) {
    result *= x;
  }

  return result;
}

let x = prompt("x?", "");
let n = prompt("n?", "");

if (n < 0) {
  alert(`Степінь ${n} не підтримується,
    Будь ласка введіть додатне число`);
} else {
  alert( pow(x, n) );
}
```

-->

Давайте детальніше розглянемо ці правила і причини їх появи.

```warn header="Немає обов'язкових правил"
Залізних правил немає. Все це стильові уподобання, а не релігійні догми.
```

### Фігурні дужки

У більшості JavaScript проєктів фігурні дужки написані у так званому "Єгипетському" стилі, де відкриваюча дужка знаходиться не на новому рядку, а на тому ж, що й відповідне ключове слово. Також потрібно додавати пробіл перед відкриваючою дужкою, наприклад:

```js
if (condition) {
  // зробити це
  // ...і це
  // ...і це
}
```

Чи потрібно ставити дужки, коли конструкція складається лише з одного рядка, наприклад `if (condition) doSomething()`?

Нижче наведені різні варіанти розташування дужок з коментарями, щоб ви змогли самостійно вирішити який варіант є найбільш читабельним.

1. 😠 Початківці іноді викорустовують таку конструкцію. Це поганий приклад, фігурні дужки не потрібні:
    ```js
    if (n < 0) *!*{*/!*alert(`Степінь ${n} не підтримується`);*!*}*/!*
    ```
2. 😠 Ніколи не розподіляйте конструкцію на декілька рядків без фігурних дужок - дуже легко зробити помилку при додаванні нового рядка:
    ```js
    if (n < 0)
      alert(`Степінь ${n} не підтримується`);
    ```
3. 😏 Писати в один рядок без дужок є прийнятним варіантом, якщо рядок короткий:
    ```js
    if (n < 0) alert(`Степінь ${n} не підтримується`);
    ```
4. 😃 Найкращий варіант:
    ```js
    if (n < 0) {
      alert(`Степінь ${n} не підтримується`);
    }
    ```

Для дуже короткого коду один рядок є прийнятним, наприклад `if (cond) return null`. Але блок коду (останній варінт) зазвичай є більш читабельним.

### Довжина рядка

Ніхто не любить читати довгий горизонтальний рядок коду. Хорошою практикою є розподіляти його на декілька рядків.

Наприклад:
```js
// Зворотні апострофи ` дозволяють розподіляти рядок на декілька
let str = `
  Робоча група TC39 організації ECMA International -
  це група JavaScript-розробників, спеціалістів з інтеграції, науковців тощо, 
  які працюють разом зі спільнотою над підтримкою та розвитком мови JavaScript.
`;
```

Або для `if`:

```js
if (
  id === 123 &&
  moonPhase === 'Зростаючий місяць' &&
  zodiacSign === 'Терези'
) {
  letTheSorceryBegin();
}
```

Максимальну довжину рядка визначається командою. Зазвичай це `80` або `120` символів.

### Відступи

Є два види відступів:

- **Горизонтальні відступи: 2 або 4 пробіли.**

    Горизонтальний відступ робиться за допогою двох або чотирьох пробілів, або за допомогою табуляції (клавіша `key:Tab`). Який відступ вибирати - вирішувати вам. Відступ з пробілам більш поширений на сьогодні.

    Однією з переваг пробілів є те, що пробіли дозволяють більш гнучку конфігурацію відступів, ніж табуляція.

    Наприклад, ми можемо вирівняти аргументи відносно відкритої дужки:

    ```js no-beautify
    show(parameters,
         aligned, // 5 пробілів зліва
         one,
         after,
         another
      ) {
      // ...
    }
    ```

- **Вертикальні відступи: пусті рядки для розподілу коду на "логічні блоки" .**

    Навіть окрема фунція може бути розподілена на логічні блоки. У наведенному нижче прикладі, ініціалізація змінних, основний цикл та повернення результату розподілені вертикально:

    ```js
    function pow(x, n) {
      let result = 1;
      //              <--
      for (let i = 0; i < n; i++) {
        result *= x;
      }
      //              <--
      return result;
    }
    ```

    Вставляйте додатковий рядок в тому випадку, коли це робить код зрозумілішим. Не повинно бути більше дев'яти рядків коду підряд без вертикального розподілу.

### Крапка з комою

Крапку з комою треба ставити після кожного виразу, навіть тоді, коли є можливість їх пропустити.

Є мови програмування, у яких крапка з комою є дійсно необов'язковими і рідко використовуються. Проте у JavaScript є ситуації коли перенос строки не інтерпретується як крапка з комою, залишаючи код вразливим до помилок. Більше детально про це знайдете у розділі <info:structure#semicolon>.

Якщо ви досвідчений JavaScript програміст, ви можете обрати стиль коду без крапки з комою, наприклад [StandardJS](https://standardjs.com/). Інакше, краще використовувати крапку з комою для того, щоб уникнути підводних каменів. Більшість розробників використовують крапку з комою.

### Рівні вкладеності

Намагайтесь уникати великої кількості рівнів вкладеності.

Наприклад, у циклі, іноді хорошим варіантом є використання директиви [`continue`](info:while-for#continue) для уникнення вкладеності.

Наприклад, замість додавання умови `if`:

```js
for (let i = 0; i < 10; i++) {
  if (cond) {
    ... // <- ще один рівень вкладеності
  }
}
```

ми можемо написати:

```js
for (let i = 0; i < 10; i++) {
  if (!cond) *!*continue*/!*;
  ...  // <- немає вкладеності
}
```

Схожим чином ми можемо змінити `if/else` та `return`.

Наприклад, дві конструкції нижче є ідентичними.

Перша:

```js
function pow(x, n) {
  if (n < 0) {
    alert("Від'ємні значення 'n' не підтримуються");
  } else {
    let result = 1;

    for (let i = 0; i < n; i++) {
      result *= x;
    }

    return result;
  }  
}
```

Друга:

```js
function pow(x, n) {
  if (n < 0) {
    alert("Від'ємні значення 'n' не підтримуються");
    return;
  }

  let result = 1;

  for (let i = 0; i < n; i++) {
    result *= x;
  }

  return result;
}
```

Друга конструкція є більш зрозумілою, тому що умова `n < 0` обробляється з самого початку. Коли перевірка закінчена ми можемо переходити до "головного" коду без потреби у додатковому рівні вкладеності.

## Розташування функцій

Якщо ви пишете декілька допоміжних функцій і код, що їх використовує, є три способи організувати функції.

1. Оголосити функції *перед* кодом, що їх використовує:

    ```js
    // *!*оголошення функій*/!*
    function createElement() {
      ...
    }

    function setHandler(elem) {
      ...
    }

    function walkAround() {
      ...
    }

    // *!*код, що їх використовує*/!*
    let elem = createElement();
    setHandler(elem);
    walkAround();
    ```
2. Спочатку код, потім функції

    ```js
    // *!*код, що використовує функції*/!*
    let elem = createElement();
    setHandler(elem);
    walkAround();

    // --- *!*допоміжні функції*/!* ---
    function createElement() {
      ...
    }

    function setHandler(elem) {
      ...
    }

    function walkAround() {
      ...
    }
    ```
3. Змішаний варіант: функція оголошена там, де вона вперше використовується.

Зазвичай, віддають перевагу другому варіанту.

Причиною цього є те, що коли ми читаємо код, перш за все ми хочемо зрозуміти *що він робить*. Якщо головний код іде першим - це стає зрозумілим з самого початку. Тоді, можливо ми навіть не будемо читати функції взагалі, особливо якщо їх імена відповідають тому, що вони роблять.

## Посібники зі Стилю Коду

Посібник зі стилю коду містить загальні правила "як писати" код, наприклад, які лапки використовувати, скільки пробілів ставити для відступу, максимальну довжину рядка, і таке інше. Тобто, багато дрібниць.

Коли всі члени команди використовують посібник зі стилю, код виглядає однаковим, незалежно від того, хто з команди його написав.

Звичайно, кожна команда може завжди створити свій посібник зі стилю, але зазвичай в цьому не має потреби. Є багато посібників, серед яких можна вибрати найбільш підходящий.

Деякі популярні посібники:

- [Google JavaScript Style Guide](https://google.github.io/styleguide/javascriptguide.xml)
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- [Idiomatic.JS](https://github.com/rwaldron/idiomatic.js)
- [StandardJS](https://standardjs.com/)
- (і ще багато інших)

Якщо ви початківець, почніть зі шпаргалки наведеної в початку цього розділу. Потім ви зможете обрати один з існуючих посібників, щоб визначити ті правила, які вам більше підходять.

## Автоматичні засоби перевірки (лінтери)

Автоматичні засоби перевірки, так звані "лінтери" - це інструменти, що автоматично перевіряють стиль коду та вносять пропозиції щодо його вдосконалення.

Найкраще в них те, що вони також можуть знайти деякі програмні помилки, наприклад друкарську помилку у назві змінної чи функції. Завдяки цій особливості, рекомендують використовувати лінтер навіть тоді, коли ви не збираєтесь дотримуватись якогось конкретного "стилю коду".

Ось декілька добре відомих засобів для перевірки:

- [JSLint](http://www.jslint.com/) -- один з перших лінтерів.
- [JSHint](http://www.jshint.com/) -- має більше налаштувань ніж JSLint.
- [ESLint](http://eslint.org/) -- напевно, найсучасніший лінтер.

Всі вони роблять свою справу. Автор використовує [ESLint](http://eslint.org/).

Більшість лінтерів інтегровані в популярні редактори: просто увімкніть відповідний плаґін в редакторі і налаштуйте стиль.

Наприклад, для ESLint вам потрібно зробити наступне:

1. Встановіть [Node.js](https://nodejs.org/).
2. Встановіть ESLint, використовуючи команду `npm install -g eslint` (npm – це менеджер JavaScript пакетів (модулів)).
3. Створіть файл конфігурації `.eslintrc` в корні вашого JavaScript проєкту (у директорії, що містить всі ваші файли).
4. Встановіть/увімкніть плаґін для вашого редактора, який інтегрується з ESLint. Більшість редакторів мають такий плаґін.

Ось приклад файлу `.eslintrc`:

```js
{
  "extends": "eslint:recommended",
  "env": {
    "browser": true,
    "node": true,
    "es6": true
  },
  "rules": {
    "no-console": 0,
    "indent": ["warning", 2]
  }
}
```

Директива `"extends"` означає, що конфігурація базується на наборі налаштувань "eslint:recommended". Після цього, ви вказуєте ваші власні.

Крім того, можна завантажити набори правил з мережі та розширити їх. Дивіться <http://eslint.org/docs/user-guide/getting-started> для отримання більш детальної інструкції зі встановлення.

Також, деякі середовища розробки (IDE) мають вбудовані засоби первірки коду, що є зручним, але не таким гнучким в налаштуванні рішенням, як ESLint.

## Підсумки

Всі правила синтаксису, які описані у даному розділі (і в посиланнях на посібники зі стилю коду) мають на меті поліпшити читабельність вашого коду. Всі вони є дискусійними.

Коли ми прагнемо писати код "краще", ми повинні задати собі наступні питання: "Що робить код більш читабельним та зрозумілим?" і "Що нам допоможе уникнути помилок?". Це головні  моменти, що треба брати до уваги, коли ви вибираєте та дискутуєте з приводу стилю коду.

Читання популярних посібників зі стилю коду дозволить вам бути в курсі найкращих практик та останніх ідей щодо стилю коду.
