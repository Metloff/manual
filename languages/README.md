# Языки
Описание ...

- [Golang](go/README.md)
- [OOP](OOP/README.md)
- [<- назад](../README.md)

## Классификация языков программирования

**Императивные и декларативные**

Императивный подход - это когда ты перечисляешь, шаг за шагом, `как` выполнить задачу.
```js
    function double (arr) {
        let results = []
        for (let i = 0; i < arr.length; i++){
            results.push(arr[i] * 2)
        }
        return results
    }
```

Декларативный подход - когда ты описываешь `что` нужно сделать.
```js
    function double (arr) {
        return arr.map((item) => item * 2)
    }
```
https://tproger.ru/translations/imperative-declarative-programming-concepts/