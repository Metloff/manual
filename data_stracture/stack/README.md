# Stack (стек)

**Стек** (иногда говорят “магазин” - по аналогии с магазином огнестрельного оружия) - это абстрактный тип данных, представляющий собой упорядоченную коллекцию элементов, где добавление нового или удаление существующего всегда происходит только на одном из концов. Этот конец обычно называют “вершиной”, а противоположный ему - “основанием”.

Элемент, добавленный последним, расположен на той позиции, с которой будет удалён в первую очередь. Такой принцип организации иногда называется **LIFO**(англ. last in — first out, «последним пришёл — первым вышел»). Пример - стопка  книг:

![](../../assets/img/bookstack.png)

Стек  может использоваться для хранения посещенных страниц в браузере, чтобы всегда можно было нажать кнопку "назад"  и  вернуться к предыдущей странице. Так же, стек  используется при рекурсивных вызовах (туда записываются значения переменных и трока, на которую необходимо вернуться).

## Операции со стеком
Базово имеет операции:
- PUSH - добавление элемента
- POP - извлекает элемент с верхушки стека
- PEEK - возвращает верхний элемент стека, но не удаляет его.  
- EMPTY - проверяет стек на пустоту
- LEN - возвращает количество элементов в стеке

## Реализация

```go
package stack

import (
	"errors"
	"sync"
)

type Stack struct {
	size int
	lock sync.RWMutex
	val  []interface{}
}

func New() *Stack {
	return &Stack{
		val: make([]interface{}, 0),
	}
}

func (s *Stack) Push(item interface{}) {
	s.lock.Lock()
	defer s.lock.Unlock()

	s.val = append(s.val, item)
	s.size++
}

func (s *Stack) Pop() (interface{}, error) {
	s.lock.Lock()
	defer s.lock.Unlock()

	if s.size == 0 {
		return nil, errors.New("Empty stack")
	}

	res := s.val[s.size-1]
	s.val = s.val[:s.size-1]
	s.size--

	return res, nil
}

func (s *Stack) Len() int {
	s.lock.RLock()
	defer s.lock.RUnlock()
	return s.size
}

func (s *Stack) Peek() (interface{}, error) {
	s.lock.RLock()
	defer s.lock.RUnlock()

	if s.size == 0 {
		return nil, errors.New("Empty stack")
	}

	return s.val[s.size-1], nil
}

```

Вместо [слайса](../dynamic_array/README.md) можно использовать  [связный список](../linked_list/README.md). Это даже предпочтительней, т.к. память, выделенная под массив не возвращается, поэтому с долго живущими очередями это может стать проблемой. 