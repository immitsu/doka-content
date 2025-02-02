---
title: "Булев тип"
description: "На некоторые вопросы нужно отвечать только «да» или «нет». Булев тип как раз про это."
cover:
  author: kirakusto
  desktop: 'images/covers/desktop.svg'
  mobile: 'images/covers/mobile.svg'
  alt: 'Тут парень, потеет и вытирает лоб, потому что перед ним выбор из двух кнопок: true и false — и он не знает, что нажать'
authors:
  - bespoyasov
editors:
  - tachisis
contributors:
  - nlopin
  - skirienko
keywords:
  - логический тип
  - тру фолс
related:
  - js/typecasting
  - js/if-else
  - js/expressions-vs-statements
tags:
  - doka
---

## Кратко

Логический или булев тип `boolean` может принимать лишь истинное (`true`) и ложное (`false`) значения. Назван он так в честь [Джорджа Буля](https://ru.wikipedia.org/wiki/Буль,_Джордж), одного из основателей математической логики.

Значения этого типа используются в [условных выражениях](/js/if-else/).

## Как пишется

Создать булево значение можно несколькими способами.

Первый — явно указать значение, используя ключевые слова `true` и `false`:

```js
// «Истина»
const truthyValue = true

// «Ложь»
const falsyValue = false
```

Второй способ — использовать метод `Boolean`:

```js
// «Истина»
const truthyValue = Boolean(1)

// «Ложь»
const falsyValue = Boolean('')
```

Как видите, даже значения других типов, например, числовые или строковые, приводятся к булеву типу.

Третий способ — использовать выражения, значениями которых будут «истина» или «ложь» (мы ниже [поговорим о таких выражениях подробнее](#vyrazheniya)).

Следующие два выражения истинны, потому что 4 действительно меньше 5.

```js
const truthyValue = Boolean(4 < 5)
const anotherTruthy = 4 < 5

console.log(truthyValue)
// true

console.log(anotherTruthy)
// true
```

Следующие два — ложны, потому что `2 * 2 === 4`:

```js
const falsyValue = Boolean(2 * 2 === 5)
const anotherFalsy = 2 * 2 === 5

console.log(falsyValue)
// false

console.log(anotherFalsy)
// false
```

Булевы значения можно использовать в [условных выражениях](/js/if-else/).

```js
const isCorrect = true
if (isCorrect) {
  // Выполнится эта ветка кода,
  // потому что оператор if проверяет,
  // истинно ли выражение в скобках,
  // и, если да, то выполняет этот код
} else {
  // Эта ветка не выполнится
}

const isWrong = false
if (isWrong) {
  // Теперь не выполнится эта ветка,
  // потому что выражение в скобках ложно
} else {
  // А вот эта — выполнится
}
```

## Как понять

Логические значения можно воспринимать как ответ на закрытый вопрос — «Да или нет?»

Это понимание позволяет придумывать более подходящие названия для булевых переменных.

Плохое название для логического значения не помогает понять, на какой вопрос отвечает переменная. Например, `waitResponse` — не очень хорошее название.

А вот переменная с именем `shouldWaitForResponse` отвечает на более чёткий вопрос «Должен ли процесс подождать ответа за запрос?». А переменная `isWaitingForResponse` — на вопрос «Ждёт ли процесс ответа прямо сейчас?»

Обычно логическим переменным дают названия, начинающиеся с английских глаголов _is_, _should_, _does_, _can_ и подобных.

### Выражения

Выше мы говорили о выражениях, которые можно привести к логическим значениям. В JavaScript такими выражениями часто пользуются, чтобы построить условия.

Булевым выражением в JavaScript может быть что угодно.

Хитрость в том, чтобы знать, какое выражение в какое значение в итоге будет преобразовано. Например, все эти выражения трансформируются в `false`:

```js
const falsy1 = Boolean(),
  falsy2 = Boolean(0),
  falsy3 = Boolean(null),
  falsy4 = Boolean(''),
  falsy5 = Boolean(false)
```

А все эти — в `true`:

```js
const truthy1 = Boolean(true),
  truthy2 = Boolean('true'),
  truthy3 = Boolean('false'),
  truthy4 = Boolean('Су Лин'),
  truthy5 = Boolean([]),
  truthy6 = Boolean({}),
  truthy7 = Boolean('0'),
  truthy8 = Boolean(' ')
```

Обратите внимание, что строка `'false'` преобразуется в логическое `true`. Так происходит потому, что непустая строка в JavaScript считается _truthy_ значением — то есть таким, которое приводится к `true`.

То же и с пустыми массивом `[]` и объектом `{}`. Они считаются _truthy_ значениями, поэтому приводятся к `true`.

Другой интересный нюанс: `'0'` превращается в `true`, как и `' '`, потому что это непустая строка.

Обратите внимание на списки [truthy](https://developer.mozilla.org/ru/docs/Словарь/Truthy) и [falsy](https://developer.mozilla.org/ru/docs/Словарь/Falsy) значений в JavaScript.

### Сравнить строку с числом

В JavaScript интерпретатор может сам [приводить типы](/js/typecasting/), из-за чего мы можем сравнивать разные типы данных друг с другом.

JavaScript многие за это не любят, потому что сравнивая число со строкой, можно наделать ошибок.

Например, если мы сравним:

```js
5 > '4'
// true
5 > '4 '
// true
5 > ' 4 '
// true
5 > '4.'
// true
```

При этом:

```js
5 > '4 .'
// false
```

Дело в том, что JavaScript попытается преобразовать строку в число. Если это получается, то мы сравниваем числа 5 и 4, а если нет, то 5 и [`NaN`](/js/number/#specialnye-znacheniya) (число, любое сравнение с которым всегда `false`).

Поэтому надо быть аккуратными со сравнениями, когда мы их используем как выражения для логических переменных.

### Отрицание

Чтобы инвертировать значение логического типа, можно использовать _логическое отрицание_. Логическое отрицание в JS записывается через унарный оператор `!`:

```js
const truthy = true
const falsy = !truthy

console.log(falsy)
// false
```

Оно также используется, чтобы проверять обратные условия. Функция `goToBed` выполнится, если `isSleeping === false`.

```js
const isSleeping = false

if (!isSleeping) {
  goToBed()
}
```
