# Сбалансированные скобки

Здача: реализовать функцию, которая принимает на вход строку, состоящую только из открывающих и закрывающих круглых скобок, и проверяет является ли скобки сбалансированными. Сбалансированность скобок означает, что каждый открывающий символ имеет соответствующий ему закрывающий, и пары скобок правильно вложены друг в друга. Рассмотрим несколько строк корректно сбалансированных скобок:

```
(()()()())

(((())))

(()((())()))
```

Сравним их со следующими, несбалансированными:

```
((((((())

()))

(()()(()
```

## Решение

Данную задачу можно решить несколькими способами:
- Через счетчик
- Через стек

Решение через счетчик выглядит следующим образом: мы итерируемся по строке, и увеличивием счетчик на 1, если встретили открывающую скобку и уменьшаем на 1, если встретили закрывающую скобку. Важно проверять каждую итерацию, не стал ли наш счетчик отрицательным. Если стал - возвращаем `false`.

```go
func isBalanced(s string) bool {
	var count int
	for _, ch := range s {
		if string(ch) == "(" {
			count++
		} else {
			if string(ch) == ")" {
				count--
				if count < 0 {
					break
				}
			}
		}
	}

	if count == 0 {
		return true
	}

	return false
}
```

Но данный метод перестает работать, если у нас появляются  скобки разных видов `([{}])`. Поэтому правильнее решать через [стек](../../data_stracture/stack/README.md).

```go
func main() {
	println(isBalanced("((()())())"))
	println(isBalanced("()"))
	println(isBalanced("([{}])"))
	println(isBalanced(")(())("))
	println(isBalanced("())("))
	println(isBalanced("[({}])"))

	println(isBalanced("[({4})"))
}

func isBalanced(brackets string) bool {
	s := stack.New()

	for _, ch := range brackets {
		if _, ok := openBrackets[string(ch)]; ok {
			s.Push(string(ch))
			continue
		}

		if ob, ok := closeBrackets[string(ch)]; ok {
			last_ob, err := s.Pop()
			if err != nil {
				return false
			}

			if last_ob != ob {
				return false
			}
		}
	}

	return s.Len() == 0
}
```