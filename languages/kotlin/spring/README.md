# Spring

## Аннотации

**@RestController**
Помечает класс как контроллер, который возвращает JSON.

**@GetMapping**
Мапит путь урла на определенный метод.

```java
@GetMapping("/greeting")
    public Greeting greeting(@RequestParam(value = "name", defaultValue = "World") String name) {
        return new Greeting(counter.incrementAndGet(), String.format(template, name));
    }
```

**@RequestParam**
Мапит параметер из запросы в переменную

# Разобрать
https://habr.com/ru/post/490586/
- [JPA](https://habr.com/ru/post/435114/)
