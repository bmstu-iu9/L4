# Задачи на лабораторную работу № 10

## Задача 1. `count_words(text)`, 4 балла

Написать функцию `count_words(text)`, которая подсчитывает число слов в тексте.
Под словом подразумевается непрерывная последовательность букв.

    >>> count_words('Мама мыла раму')
    3
    >>> count_words('"Привет всем!" — сказал я сегодня утром.')
    6
    >>> count_words('однослово')
    1
    >>> count_words('!@#$%^&*()')
    0
    >>> count_words('a,b,c,d,e,f')
    6
    >>> count_words('a b c d e f')
    6
    >>> count_words('a,b c+d e~f')
    6

## Задача 2. `extract_words(text)`, 4 балла

Написать функцию `extract_words(text)`, которая извлекает все слова из текста,
возвращая их в виде списка.

Под словом также подразумевается непрерывная последовательность букв.

    >>> extract_words('Мама мыла раму')
    ['Мама', 'мыла', 'раму']
    >>> extract_words('"Привет всем!" — сказал я сегодня утром.')
    ['Привет', 'всем', 'сказал', 'я', 'сегодня', 'утром']
    >>> extract_words('однослово')
    ['однослово']
    >>> extract_words('!@#$%^&*()')
    []
    >>> extract_words('a,b,c,d,e,f')
    ['a', 'b', 'c', 'd', 'e', 'f']
    >>> extract_words('a b c d e f')
    ['a', 'b', 'c', 'd', 'e', 'f']
    >>> extract_words('a,b c+d e~f')
    ['a', 'b', 'c', 'd', 'e', 'f']
