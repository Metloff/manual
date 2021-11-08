# Map

## Реализация
- [Описание реализации от Dave Cheney](https://dave.cheney.net/2018/05/29/how-the-go-runtime-implements-maps-efficiently-without-generics)
- [Структурыкоторые могут быть ключами](https://golangbyexample.com/interface-comparison-golang/)


## Особенности
Если конкурентно писать и читать из мапы, может возникнуть паника. Поэтому лучше обкладывать мапу мьютексами.

Если в примере ниже убрать мьютексы на чтение, будет паника.
```go
package main

import (
	"fmt"
	"math/rand"
	"sync"
	"time"
)

func main() {
	var state = make(map[int]int)
	var mutex = &sync.RWMutex{}
	wg := sync.WaitGroup{}
	wg.Add(1)

	go func() {
		for {
			mutex.RLock()
			fmt.Printf("%+v %v\n", state[1], state[2])
			mutex.RUnlock()
		}
	}()

	go func() {
		for {
			mutex.Lock()
			println("locked by 1")
			state[1] = rand.Intn(5)
			mutex.Unlock()
			println("unlocked by 1")
		}

		wg.Done()
	}()

	wg.Wait()

	time.Sleep(2 * time.Second)
}

```

# Разобрать
https://www.youtube.com/watch?v=Tl7mi9QmLns