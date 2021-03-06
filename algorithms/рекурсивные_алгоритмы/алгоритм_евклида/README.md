# Алгоритм Евклида

Это алгоритм поиска наибольшего общего делителя (greatest common divisor (GCD))

**Описание**
```
gcd(a, b) = gcd(b, r), где 

a = b*q + r,
0 <= r <= b
```

**Работа алгоритма**
```
1 Function gcd(x, y) :
    Вход :(x, y) — неотрицательные целые числа, x > 0
    Выход : НОД(x, y)
2   if y == 0 then
3       return x
4   end
5   return gcd(y, x mod y)
6 end
```

- Получив на вход **a** и **b** алгоритм проверяет, что `a > b`
- Проверка `b == 0`
  - Если нет, то вычисляет остаток от деления `a / b` и рекурсивно вызывает себя, где `a = b, b = остаток от деления`
  - Если да, возвращает **a**

**Пример**

```
gcd(91, 35) = gcd(35, 21) = gcd(21, 14) = gcd(14, 7) = gcd(7, 0)

```

**Сложность алгоритма**

`Сложность: O(N)` 

Докажем:

Остаток от деления `a / b`, назовем его `r`, будет меньше половины а (`r < a/2`). Это легко увидеть из рисунка:

![](../../assets/img/alg_2.jpeg)

Если представить число `a` в двоичной системе, то при делении на два, мы просто отбрасываем последний бит. Т.е. если 
- `a = an, an-1, ..., a1, a0`, то  
- `a / 2 = an, an-1, ..., a1`

Поэтому, длинна двоичной записи `r` как минимум на 1 меньше длинны двоичной записи `a`.

После первого шага алгоритма, длинна двоичной записи `a` уменьшается на 1, затем на место `a` становится `b`, затем, после второго шага алгоритма, длинна двоичной записи `b` тоже уменьшается на 1. Таким образом, за два шага алгоритма, длинна входных данных (`a` и `b`) уменьшится на 1.

Поэтому алгоритму потребуется не больше чем `2N` шагов. Следовательно сложность алгоритма `O(N)`


## Итеративный алгоритм Евклида

Это алгоритм Евклида, который не использует рекурсию.
```
Вход :(x, y) — неотрицательные целые числа, x > 0
Выход : НОД(x, y)
1 while y > 0 do
2   b = x mod y
3   x = y
4   y = b
5 end
6 return x
```

```go
func gcd(a, b int) int {
    for (b > 0) {
        r := a % b
        a = b
        b = r
    }

    return a
}
```