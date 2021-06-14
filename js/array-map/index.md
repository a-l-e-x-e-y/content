---
title: "Array.map"
tags:
  - doka
authors:
  - windrushfarer
contributors:
  - skorobaeus
  - nlopin
  - furtivite
---

## Кратко

Метод `map` позволяет произвести трансформацию исходного массива в другой массив, используя переданную функцию-колбэк. Переданная функция будет вызвана для каждого элемента массива в том же порядке. Из результатов вызова функции будет собран новый массив.

## Пример

```js
const nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]

// Сделаем массив квадратов
const squares = nums.map(function (num) {
  return num * num
}) // [1, 4, 9, 16, 25, 36, 49, 64, 81]

// Либо можно сделать массив с объектами
const objects = nums.map(function (num) {
  return {
    field: num,
  }
}) // [ { field: 1 }, { field: 2 }, ... { field: 9 } ]
```

Интерактивный пример

<iframe title="Используем map для изменения значений массива" src="demos/index.html"></iframe>

## Как пишется

Как и другим похожим методам, для `map` необходимо передать колбэк-функцию, которая должна возвращать какое-то значение. Именно это значение попадёт в итоговый трансформированный массив.

Функция, которую мы передаём в метод `map` , может принимать три параметра:

- `item` — элемент массива в текущей итерации
- `index` — индекс текущего элемента
- `arr` — сам массив, который мы перебираем

```js
const nums = [0, 1, 2, 3]

const transformed = nums.map(function (num, index, arr) {
  // Трансфомируем в сумму числа, его индекса и длинны массива
  return num + index + arr.length
}) // [4, 6, 8, 10]
```

💡 `map` возвращает __новый__ массив, при этом исходный массив __никак не изменится__.

💡 При работе с `map` необходимо возвращать значение из функции-колбэка. Если забыть вернуть значение, например забыв обработать какую-то ветку условия, то в итоговом массиве будет `undefined`:

```js
const nums = [1, 2, 3, 4, 5]

const transformed = nums.map(function (num) {
  if (num <= 3) {
    return "less"
  }
  // забыли обработать эту ветку условий
}) // ['less', 'less', 'less', undefined, undefined]
```

## Как это понять

Часто возникают ситуации, когда на основе одного массива, нужно получить другой массив, трансформировав каким-либо образом исходные значения. Это можно сделать используя обычные циклы `for` или `while`.

```js
const nums = [1, 2, 3, 4, 5]

const transformed = []

for (let i = 0; i < nums.length; i++) {
  const num = nums[i]
  const item = `${i}-${num}`
  transformed.push(item)
}

console.log(squares) // ['0-1', '1-2' , '2-3', '3-4', '4-5']
```

Задача решена, однако как и другие встроенные методы массива, `map` позволяет написать код короче и проще в понимании.

```js
const nums = [1, 2, 3, 4, 5]

// Результат тот же, но короче и проще
const transformed = nums.map(function (num, i) {
  return `${i}-${num}`
})
```