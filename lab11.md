# Задачи на лабораторную работу № 11

## Задача 1. `revw(text)`, 2 балла

Написать функцию `revw(text)`, которая принимает строку и строит новую строку,
в которой слова исходной строки записаны в обратном порядке.

Считаем, что слова это просто последовательности знаков, разделённые одним
или несколькими пробелами.

В результирующей строке слова должны разделяться ровно одним пробелом.

    >>> revw('the quick brown fox jumps over the lazy dog')
    'dog lazy the over jumps fox brown quick the'
    >>> revw('     the     quick    brown   fox    ')
    'fox brown quick the'
    >>> revw('         ')
    ''
    >>> revw('oneword')
    'oneword'

## Задача 2. `all_substr_k(line, k)`, 2 балла

Написать функцию `all_substr_k(line, k)`, возвращающую список всех подстрок
длины `k` исходной строки `line`. Если `k` больше длины строки, то возвращается
пустой список. Строки могут повторяться.

    >>> all_substr_k('abracadabra', 4)
    ['abra', 'brac', 'raca', 'acad', 'cada', 'adab', 'dabr', 'abra']
    >>> all_substr_k('abracadabra', 7)
    ['abracad', 'bracada', 'racadab', 'acadabr', 'cadabra']
    >>> all_substr_k('abracadabra', 11)
    ['abracadabra']
    >>> all_substr_k('abracadabra', 12)
    []

Порядок подстрок в вашем решении может отличаться от порядка подстрок в примере.

## Задача 2. `all_substr(line)`, 2 балла

Написать функцию `all_substr(line)`, возвращающую список всех непустых подстрок
исходной строки `line`. Строки могут повторяться.

    >>> all_substr('abrac')
    ['a', 'b', 'r', 'a', 'c', 'ab', 'br', 'ra', 'ac', 'abr', 'bra', 'rac',
     'abra', 'brac', 'abrac']

Порядок подстрок в вашем решении может отличаться от порядка подстрок в примере.
