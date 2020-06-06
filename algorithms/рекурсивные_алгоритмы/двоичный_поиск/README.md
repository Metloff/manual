# Двоичный поиск (Binary Search)

**Свойства:**
- рекурсивный алгоритм
- применим только на отсортированном массиве
- **Временная сложность:** `O(logN)`
  
Подводные камни:
- вычисление середины может выйти за пределы типа (`leftIDx + rightIDx`)

**Описание:**

Алгоритм находит середину массива `midIDx`, извлекает значение и сравнивает его с искомым значением. 
- Если они равны - то алгоритм возвращает `midIDx`.
- Если искомое значение больше значения среднего члена массива, то берется *правая* часть массива (от `midIDx + 1` и до конца) и проделывается та же самая операция.
- Если искомое значение меньше значения среднего члена массива, то берется *левая* часть массива (от начала и до `midIDx - 1`) и проделывается та же самая операция.

## Рекурсивная форма

``` go
    func binarySearch(arr []int, target, leftIDx, rightIDx int) int {
        if len(arr) == 0 {
            return -1
        }
        if leftIDx > rightIDx {
            return -1
        }

        midIDx := leftIDx + (rightIDx-leftIDx)/2

        midValue := arr[midIDx]
        if midValue == target {
            return midIDx
        }
        if midValue > target {
            rightIDx = midIDx - 1
        }
        if midValue < target {
            leftIDx = midIDx + 1
        }

        return binarySearch(arr, target, leftIDx, rightIDx)
    }
```

## Итеративная форма

``` go
    func search(nums []int, target int) int {
        leftIDx := 0
        rightIDx := len(nums) - 1

        for leftIDx <= rightIDx {
            // Исключает выход за пределы инта. В данном случае число не будет больше rightIDx.
            // Если делать стандартным способом (leftIDx + rightIDx) / 2, то сумма в скобках может
            // быть больше максимального значения.
            midIDx := leftIDx + (rightIDx-leftIDx)/2

            midValue := nums[midIDx]
            if midValue == target {
                return midIDx
            }
            if midValue > target {
                rightIDx = midIDx - 1
            }
            if midValue < target {
                leftIDx = midIDx + 1
            }
        }

        return -1
    }
```

# Литература
- [Wiki](https://en.wikipedia.org/wiki/Binary_search_algorithm)