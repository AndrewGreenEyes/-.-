## Сортировка слиянием

Слияние переводится как объединение. Сначала сортировка разделяет а потом объединяет. Сортировка разделяет исходный список до тех пор пока в нём 2 части не будут состоять из одного элемента. После того как это случилось объеденяем этот список и проверяем второй элемент больше первого если да то меняем их местами и т.д. Протокол работа алгоритма на списке {5, 1, 4, 2, 3}: Протокол mergesort: [5, 1] mergesort: [5]

```mergesort
	mergesort:  [1]
		Merge[In]:  [5] [1]
		Merge[Out]:  [1, 5]


mergesort:  [4, 2, 3]
	mergesort:  [4]

	mergesort:  [2, 3]
		mergesort:  [2]

		mergesort:  [3]
			Merge[In]:  [2] [3]
			Merge[Out]:  [2, 3]

		Merge[In]:  [4] [2, 3]
		Merge[Out]:  [2, 3, 4]

	Merge[In]:  [1, 5] [2, 3, 4]
	Merge[Out]:  [1, 2, 3, 4, 5]
```

Рассмотрим рекурсивную реализацию алгоритма сортировки:

```python
def slianye(a, b):
    result = []
    i = 0
    j = 0
    sizeA = len(a)
    sizeB = len(b)
    while i < sizeA and j < sizeB:
        if a[i] <= b[j]:
            result.append(a[i])
            i += 1
        else:
            result.append(b[j])
            j += 1
    result.extand(a[i:])
    result.extend(b[j:])
    return result

def slianyeSort(liston):
    if len(liston) <= 1:
        return liston
    k = len(liston) // 2
    return slianye(slianyeSort(liston[:k]), slianyeSort(liston[k:]))
```

Сортировка слиянием одна из быстрых сортировок За О(𝑁∗𝑙𝑜𝑔𝑁) А теперь рассмотрим нерекурсивную реализацию этого алгоритма сортировки. Теперь сделаем так: Пусть мы будем сортировать по какому-то ключу. Например по его остатку от деления. Тогда сделаем так:

```python
def sky(a):return a
STDKEY = sky
def slianye(a, b, key):
    result = []
    i = 0
    j = 0
    sizeA = len(a)
    sizeB = len(b)
    while i < sizeA and j < sizeB:
        # a[i] <= b[j]
        if key(a[i]) <= key(b[j]):
            result.append(a[i])
            i += 1
        else:
            result.append(b[j])
            j += 1
    result.extand(a[i:])
    result.extend(b[j:])
    return result
def slianyeSort(liston, key=STDKEY):
    if len(liston) <= 1:
        return liston
    k = len(liston) // 2
    return slianye(slianyeSort(liston[:k]), slianyeSort(liston[k:], key))
```
Код по чему сортировать называется ключ. Такая программа почти и реализована в Python. А вот в в С++ не так. Если написать как в C++ тогда программа выглядела так:

```python
def sky(a):return True
STDKEY = sky

def slianye(a, b, comparetor):
    result = []
    i = 0
    j = 0
    sizeA = len(a)
    sizeB = len(b)
    while i < sizeA and j < sizeB:
        # a[i] <= b[j]
        if comparetor(a[i], b[j]):
            result.append(a[i])
            i += 1
        else:
            result.append(b[j])
            j += 1
    result.extand(a[i:])
    result.extend(b[j:])
    return result

def slianyeSort(liston, comparetor=STDKEY):
    if len(liston) <= 1:
        return liston
    k = len(liston) // 2
    return slianye(slianyeSort(liston[:k]), slianyeSort(liston[k:], comparetor))
```

В таком случае такой ключ называется компаратором. Заметим что компаратор возвращает booleanType т.е. True или False. Иначе сортировка может выдать ошибку.

Встроенная сортировка Встроенная сортировка в Python это сортировка слиянием где слияние производится методом вставок. В C++ теперь такая же сортировка. Но есть такая тонкость - стандартная сортировка если компаратор возращает False сортирует как попало! Чтобы избежать этой штуки нужно писать код так: 

Код С++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// определение функций

int main(){
    // операции
    stable_sort(список.begin(), список.end(), comparatorfun);
    // операции
    return 0;
}
```
