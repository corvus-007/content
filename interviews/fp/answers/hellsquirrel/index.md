Композиция – основа функционального подхода. Операция композиции в теории категорий определяется для разных сущностей. Но сейчас мы обратим внимание именно на композицию функций.

Нам нужно создать функцию, которая принимает массив других функций и возвращает новую функцию.

Используем правило «Не думай, просто пиши» 🙂

```js
const compose = (...fns) => x => // функция которую нам надо реализовать
```
В условии нам подсказали как это сделать — `compose(f,g, ...) = f(g(...(x)))`.

Если сходу решение в голову не приходит, давайте попробуем посмотреть на примерах.
Композиция для одной функции — это сама функция:

```js
compose(f) = f
```

Композиция для двух функций:

```js
compose(f,g) = x => {
  const prevResult = g(x) // выполнили g
  return f(prevResult) // выполнили f
}
```

Тогда общее решение выглядит так:

```js
const compose = (...fns) => x => fns.reduceRight((acc, fn) => fn(acc), x)
```

Для каждой _предыдущей_ функции из массива вызовите её на результате выполнения _следующей_. Тут важно что функции выполняются справа налево.