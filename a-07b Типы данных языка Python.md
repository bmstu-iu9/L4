Типы данных языка Python
========================

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" id="MathJax-script" async="true"
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>

<div id="toc"></div>
<script src="toc.js"></script>
<script>
makeTOC.localizedHeader = "Содержание"
makeTOC.localizedShow = "Показать";
makeTOC.localizedHide = "Скрыть";
window.MathJax = {
  tex: {
    inlineMath: [['$', '$'], ['\\(', '\\)']]
  }
};
</script>

Данные в языке Python делятся на две группы: простые (обозначают единственное
значение) и составные (хранят в себе несколько значений). Рассмотрим основные
типы данных языка Python.

1. Простые типы данных:
   1. `int` — целое число.
   2. `float` — вещественное (дробное, действительное) число.
   3. `str` — строка.
   4. `bool` — булевский (логический) тип.
2. Составные типы данных:
   1. `list` — список, _изменяемый_ набор значений, пронумерованных целыми
      числами, начиная с `0`.
   2. `tuple` — кортеж, _неизменяемый_ набор значений, пронумерованных целыми
      числами, начиная с `0`.
   3. `dict` — словарь (ассоциативный массив) — изменяемый набор значений,
      индексируемый неизменяемыми типами данных (числа, строки, кортежи).
   4. `set` — множество — неупорядоченный набор значений без повторений.

Целые числа (`int`)
-------------------

Целые числа могут быть записаны в разных системах счисления. В десятичной форме
они записываются как последовательности десятичных цифр. В шестнадцатеричной
форме — как последовательности шестнадцатеричных цифр (`0`…`9`, `A`…`F`),
предварённых знаком `0x`. Восьмеричные числа — последовательности восьмеричных
цифр, начинаются на `0t`. Двоичные — начинаются `0b`.

    >>> 10
    10
    >>> 0xA
    10
    >>> 0t12
    10
    >>> 0b1010
    10

Если у операций `+`, `-`, `*`, `//`, `%` оба операнда целые, то результат будет
целым. Если хотя бы один из операндов вещественный — результат вещественный.
Результат операции `/` всегда вещественный.

Размер целых чисел неограничен. Длина целого числа ограничивается лишь доступной
памятью компьютера.

Тип целых чисел в Python называется `int`. Одновременно, `int` можно
как встроенную функцию, преобразующую свой аргумент в целое число:

    >>> int(3.1415926)
    3
    >>> int('1000000')
    1000000

Вещественные числа
------------------
**Вещественные числа** в Python моделируют действительные числа в математике.
В отличие от целых чисел, вещественные числа имеют ограниченный диапазон
и ограниченную точность.

Диапазон от 10<sup>−323</sup> до 10<sup>+308</sup>. Если при расчётах получится
меньшее число, то оно представляется как ноль, если большее — произойдёт ошибка
переполнения. Точность ограничена ≈15 десятичными знаками после запятой.

Нижняя граница:

    >>> 10.0**-323
    1e-323
    >>> 10.0**-324
    0.0

Верхняя граница:

    >>> 10.0**308
    1e+308
    >>> 10.0**309
    Traceback (most recent call last):
      File "<pyshell#24>", line 1, in <module>
        10.0**309
    OverflowError: (34, 'Result too large')

Точность:

    >>> 1.0 + 0.000000000000001
    1.000000000000001
    >>> 1.0 + 0.0000000000000001
    1.0

Вещественные числа, в отличие от целых, всегда содержат или знак разделителя
целой и дробной части (точку, `.`), или показатель степени (`e`). Разделителем
целой и дробной части является точка, т.к. запятая используется для разделения
параметров функции и при построении составных типов данных (массивы, кортежи
и т.д.)

Вещественное число может быть записано в показательной форме в виде

    ‹мантисса›e‹степень›

которое означает `‹мантисса›`×10<sup><tt>‹степень›</tt></sup>. Примеры:

    6.022e23       # число Авогадро
    1.38e-23       # постоянная Больцама
    3e8            # округлённое значение скорости света в м/с

Класс вещественных чисел в Python называется `float`, он же — встроенная
функция-конструктор, преобразующая свой аргумент к вещественному числу:

    >>> float('3.1415926')
    3.1415926
    >>> float('10000000000000000000000000000000000000000')
    1e+40

Математическая библиотека (`math`)
----------------------------------
В Python есть библиотека, содержащая основные математические функции,
работающие с вещественными числами: тригонометрия, логарифмы и т.д.
Называется она `math`, подключается к программе как

    from math import *                 # №1
    from math import sin, pi           # №2
    import math                        # №3

В форме №1 в программе становятся доступными все константы и функции,
определённые в библиотеке.

    from math import *

    print(sin(pi/2))
    print(cos(pi/2))

В форме №2 — те, что явно перечислены после ключевого слова `import`.

    from math import sin, pi

    print(sin(pi/2))
    print(cos(pi/2))                   # ОШИБКА! cos не виден!

В форме №3 — в программе доступен объект `math`, функции библиотеки
доступны как поля и методы этого объекта.

    import math

    print(math.sin(math.pi/2))
    print(math.cos(math.pi/2))

Функции библиотеки можно посмотреть во встроенной документации:

    >>> import math
    >>> help(math)
    ‹длинная справка›
    >>> help(math.sin)
    Help on built-in function sin in module math:

    sin(x, /)
        Return the sine of x (measured in radians).

### Преобразование между целыми и вещественными числами

Для преобразования, во-первых, можно использовать конструкторы `float`
и `int`. В библиотеке `math` есть функции `floor`, `ceil` и `round`.
Разобраться с ними самостоятельно.

### Функция `abs(x)`

Функция `abs(x)` возвращает абсолютное значение числа:

    >>> abs(7)
    7
    >>> abs(-7)
    7
    >>> abs(-273.15)
    273.15

Строки
------
Строка (класс `str`) представляет последовательность печатных знаков. Знаки,
которые представляют строки в Python 3, являются символами Юникода, т.е.
включают в себя буквы разных алфавитов, цифры, знаки препинания, иероглифы,
пиктограммы, математические знаки и эмодзи. В противоположность, в Python 2.7
строки состояли из однобайтовых символов конкретной кодировки (например,
кодировки Windows-1251 на Windows в русскоязычной локализации).

Строки занимают промежуточное положение между простыми и составными типами
данных. С одной стороны, они хранят несколько значений. А с другой стороны,
у этих значений нет собственного типа — операция индексации `s[i]` возвращает
не печатный символ, а строку из одного знака.

Строки — **неизменяемый тип данных.**

Конструктор строки — функция `str`, которая для аргумента любого типа построит
строку. Если ей передать строку — то вернётся точная копия строки.

    >>> str(True)
    'True'
    >>> str(100500)
    '100500'
    >>> str(1000000000000000000.0)
    '1e+18'
    >>> str(None)
    'None'
    >>> str('hello')
    'hello'
    >>> str(str)
    "<class 'str'>"

### Запись строк в программе
Строки записываются в одинарных `'...'` или двойных `"..."` кавычках. В каких
кавычках записывать — это дело принятого стиля программирования. Чаще пишутся
одинарные кавычки.

Если строка записана в одинарных кавычках, то внутри можно использовать
двойные:

    'Он сказал: "Привет!"'

Если в двойных — внутри можно использовать одинарные (апострофы):

    "Let's go, Brandon!"

Помимо обычных, печатных символов, существуют особые управляющие символы,
например, символ перевода строки. Для записи подобных символов используются
так называемые **escape-последовательности** — последовательности знаков,
начинающися со знака `\`. (Клавиша «\» рядом с Backspace или «Ъ»
на клавиатуре, не путать с «/», расположенной между «Ю» и Shift!)

Escape-последовательность | значение
--------------------------|---------
`\\`                      | Собственно, знак `\`
`\n`                      | Перевод строки
`\r`                      | Возврат каретки (возврат к началу строчки)
`\t`                      | Знак табуляции (клавиша Tab)
`\xNN`                    | Символ с шестнадцатиричным кодом NN
`\uNNNN`                  | Символ с шестнадцатиричным кодом NNNN
`\UNNNNNNNN`              | Символ с шестнадцатиричным кодом NNNNNNNN
`\b`                      | Возврат на символ назад при печати
`\a`                      | При печати выдаёт звуковой сигнал
`\"`                      | Двойная кавычка
`\'`                      | Одинарная кавычка (апостроф)

Примеры на `\r` и `\b` (нужно запускать в окне консоли, в IDLE не работает):

    >>> print('abcdefghi\r!!!')
    !!!defghi
    >>> print('hello\b!')
    hell!
    >>> print('hello\b\b\b!')
    he!lo
    >>> print('\a')                    # слышен системный звуковой сигнал

Другие примеры (работают в IDLE):

    >>> print("abc\ndef\nghi")
    abc
    def
    ghi
    >>> print('\x30')
    0
    >>> print('\x40')
    @
    >>> print('\u0040')
    @
    >>> print('\u03BB')
    λ
    >>> print('\u2261')
    ≡
    >>> print('7 \u2264 7, 8 \u2265 7')
    7 ≤ 7, 8 ≥ 7
    >>> print('Пример на табуляцию:\na\tbb\tccc\tdddd\teeeee\t!')
    Пример на табуляцию:
    a	bb	ccc	dddd	eeeee	!
    >>> print('1\t1\n22\t22\n333\t333\n4444\t4444\n55555\t55555')
    1	1
    22	22
    333	333
    4444	4444
    55555	55555

Из всех escape-последовательностей чаще всего мы будем пользоваться переводом
строки (`\n`), чуть реже табуляцией (`\t`), представлением самого знака `\`
(`\\`) и кавычками, чтобы их записывать внутри строк (`\'`, `\"`).

Символ перевода строки `\n` при печати выполняет переход на новую строку.

**Одна escape-последовательность представляет 1 символ строки.** Например,
строка `\n\n\n` состоит из трёх символов — трёх переводов строки.


### Операции, применимые к строке

К строкам применима операция `+`, выполняющая конкатенацию (склеивание)
строк:

    >>> "штука" + 'турка'
    'штукатурка'

Для целых чисел из курса 1 класс известно, что 3×5 = 3+3+3+3+3 (5 раз).
В Python это же применимо и к строкам:

    >>> 'строка' * 3
    'строкастрокастрока'
    >>> 20 * '*'
    '********************'

Можно использовать сокращённые операторы присваивания:

    >>> s = 'штука'
    >>> s += 'турка'
    >>> s
    'штукатурка'

Строки можно сравнивать при помощи операций отношения, сравнение
осуществляется в алфавитном порядке (точнее, по номерам символов в таблице
Юникода):

    >>> 'арбуз' < 'дыня'
    True
    >>> 'штукатурка' > 'штука'
    True
    >>> 'hello' <= 'bye'
    False
    >>> 'адвокат' > 'антрекот'
    False
    >>> 'адвокат' < 'антрекот'
    True

Если одна строка является префиксом другой, то более короткая строка считается
меньше.

Для строк есть ещё одна операция отношения — `in`, проверяет вхождение подстроки

    >>> 'кот' in 'антрекот'
    True
    >>> 'пёс' in 'антрекот'
    False
    >>> 'пёс' not in 'антрекот'
    True
    >>> 'ад' not in 'адвокат'
    False

Операция `not in` противоположна операции `in`.

К строкам применима встроенная функция `len(•)`, возвращающая длину строки:

    >>> len('штукатурка')
    10
    >>> len('')
    0
    >>> len('\\\\')
    2
    >>> len('\n\n\n')
    3

Можно обращаться символу в строке по номеру, используя операцию
индексации `s[i]`, где `s` — строка, `i` — **индекс** или номер символа. Индекс
может быть положительным от `0` до `len(s)-1`, где `len(s)` — длина строки
(символы строки нумеруются с нуля).

Либо отрицательным от `-len(s)` до `-1`, в этом случае имеется ввиду номер
от конца строки. Если индекс отрицательный, например `s[-x]`, то подразумевается
индекс `s[len(s)-x]`. Т.е. чтобы из отрицательного индекса получить настоящий,
нужно его прибавить к длине строки.

    >>> s = 'Hello!'
    >>> s[0]
    'H'
    >>> s[1]
    'e'
    >>> s[2]
    'l'
    >>> s[5]                           # это последний, т.к. индекс должен быть
    '!'                                # от 0 до len(s)−1
    >>> len(s)
    6
    >>> s[-1]                          # обращение к последнему
    '!'
    >>> s[-2]                          # предпоследний
    'o'
    >>> s[-6]                          # начальный
    'H'

### Полезные методы строк
Строки, как и другие типы данных Python, являются объектами, и у них есть свои
методы. Все методы строк можно получить во встроенной справке:

    >>> help(str)

Некоторые полезные методы:

* `s.split()` — разбивает строку по пробельным символам,
* `s.split(sep)` — разбивает строку по указанному разделителю,
* `s.join(xs)` — объединяет элементы последовательности `xs` с разделителем `s`,
  `xs` — должна быть последовательностью строк,
* `s.startswith(t)`, `s.endswith(t)` — `True`, если строка `s` начинается или
  заканчивается на `t`,
* `s.find(t)` — ищет индекс, начиная с которого подстрока `t` входит в строку
  `s`, `-1`, если не найдено.
* `s.trim()` — удаляет из строки начальные и конечные пробельные символы
  (пробелы, табуляции, `\n`, `\r`),
* семейство методов, проверяющих содержание — `True`, когда строка непустая
  и все символы заданного типа:
  * `s.isdigit()` — все цифры,
  * `s.isalpha()` — все буквы,
  * `s.isalnum()` — все либо буквы, либо цифры,
  * `s.isspace()` — все пробельные символы (пробел, `\t`, `\n`, `\r`),
  * `s.ispunct()` — все знаки пунктуации и т.д.

Примеры:

    >>> 'раз   два три  четыре'.split()
    ['раз', 'два', 'три', 'четыре']
    >>> 'one,two,,three'.split(',')
    ['one', 'two', '', 'three']
    >>> '+'.join(['раз', 'два', 'три'])
    'раз+два+три'
    >>> '+'.join('hello')
    'h+e+l+l+o'
    >>> '   \n\t  строка   \t\t\n\r\n    '.trim()
    'строка'
    >>> 'штукатурка'.startswith('штука')
    True
    >>> 'штукатурка'.startswith('привет')
    False
    >>> 'штукатурка'.endswith('турка')
    True
    >>> 'штукатурка'.endswith('грек')
    False
    >>> 'раз два три'.find('раз')
    0
    >>> 'раз два три'.find('два')
    4
    >>> 'раз два три'.find('четыре')
    -1
    >>> '       Привет, штукатурка!     '.trim()
    'Привет, штукатурка!'
    >>> '\n\n\nПривет, штукатурка!\n\n\n'.trim()
    'Привет, штукатурка!'
    >>> '       Привет, штукатурка!     '.ltrim()
    'Привет, штукатурка!     '
    >>> '       Привет, штукатурка!     '.rtrim()
    '       Привет, штукатурка!'
    >>> 'привет'.isalpha()
    True
    >>> 'привет!'.isalpha()
    False
    >>> ''.isalpha()
    False
    >>> '1'.isdigit()
    True
    >>> 'один'.isdigit()
    False
    >>> 'привет'.isalnum()
    True
    >>> '100500'.isalnum()
    True
    >>> 'Агент007'.isalnum()
    True
    >>> 'B-52'.isalnum()
    False
    >>> '           '.isspace()
    True
    >>> '\n\n\n'.isspace()
    True
    >>> '\t\t\t'.isspace()
    True
    >>> '            !'.isspace()
    False

### Функции `chr(n)` и `ord(n)`

**Юникод** — международный стандарт на кодирование символов. В таблицу Юникода
входят символы различных алфавитов, знаки пунктуации, математические символы,
управляющие символы (`\n`, `\t`, `\r`, `\b`...), смайлики (эмодзи) и так далее.

В таблице Юникода каждому символу сопоставляется его номер, т.н. **кодовая
точка.** Всего в Юникоде возможно 1 114 112 (`2**20 + 2**16`), многие из кодовых
точек до сих пор не распределены.

Функция `chr(n)` возвращает символ с кодовой точкой `n`:

    >>> chr(48)
    '0'
    >>> chr(0x3bb)
    'λ'
    >>> 0x3bb
    955
    >>> chr(955)
    'λ'

Функция `ord(c)` возвращает кодовую точку символа `c`:

    >>> ord('@')
    64
    >>> ord('λ')
    955
    >>> ord('Ы')
    1067
    >>> ord(' ')
    32
    KeyboardInterrupt
    >>> ord('😊')
    128522
    >>> chr(128522)
    '😊'

**UTF-8** — один из способов кодирования символов Юникода в виде
последовательности байтов. При данном способе кодирования различным символам
Юникода назначаются последовательности длиной от 1 до 4 байтов. Символы,
входящие в таблицу ASCII (латинские буквы, десятичные цифры, основные знаки
пуктуации) кодируются 1 байтом, греческие и кириллические буквы — двумя,
иероглифы и смайлики — 3–4 байтами в зависимости от кода.


Булевский тип (`bool`)
----------------------
Мы о нём уже говорили, когда обсуждали логические выражения, условный оператор
и цикл с предусловием (`while`). Конструктор булевского типа — функция `bool`,
принимает любое значение и трактует его как истину или ложь.

    >>> bool(100)
    True
    >>> bool(0)
    False
    >>> bool('Непустая строчка')
    True
    >>> bool('')
    False
    >>> bool(None)
    False

Операции с логическим типом `and`, `or`, `not` мы подробно рассматривали ранее.

Функция `abs(x)`, которая возвращает абсолютное значение числа, как ни странно,
применима и для логических значений. Возвращает `1` для истины, `0` для лжи:

    >>> abs(True)
    1
    >>> abs(False)
    0

Литералы типа `bool`: `True` и `False`.

Списки (`list`)
---------------

**Список** — изменяемый контейнер значений, индексируемый целыми числами
в диапазоне от `0` до некоторой величины — длины списка.

Литерал списка — элементы списка, перечисленные через запятую в квадратных скобках

**Пример:**

    [2, 3, 5, 7, 11, 13, 17]

Это список из 7 значений, которые являются первыми 7 простыми числами.

Конструктор списка — функция `list`, которая принимает любую итерируемую
последовательность и формирует список с этими элементами:

    >>> list('Привет!')
    ['П', 'р', 'и', 'в', 'е', 'т', '!']
    >>> list([5, 7, 7])
    [5, 7, 7]
    >>> list(range(10))
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

Длину списка можно узнать при помощи встроенной функции `len(xs)`:

    >>> len([5, 7, 7, 8])
    4

### Операции, применимые к списку

**Операция индексирования.** К элементам списка можно обращаться по номеру,
используя квадратные скобки. Нумерация может быть как положительной — от `0`
до `len(‹список›)−1`, так и отрицательной — от `−1` до `−len(‹список›)`.
Положительный индекс позволяет обратиться к элементу, начиная с начала,
отрицательный — начиная с конца (`xs[-1]` — последний элемент, `xs[-len(xs)]` —
первый элемент). Т.е. тут аналогично со строками:

    >>> xs = [2, 3, 5, 7, 11]
    >>> xs[0]
    2
    >>> xs[4]
    11
    >>> xs[-1]
    11
    >>> xs[-5]
    2
    >>> xs[3]
    7

Но, в отличие от строк, список является изменяемой структурой данных. Обращение
к элементу списка может располагаться слева в операторе присваивания:

    >>> xs[2] = 10
    >>> xs
    [2, 3, 10, 7, 11]
    >>> xs[-1] *= 5
    >>> xs
    [2, 3, 10, 7, 55]
    >>> xs[0] = 0
    >>> xs
    [0, 3, 10, 7, 55]

**«Сложение и умножение».** Тут тоже похоже на строки: операция `+` позволяет
склеивать два списка:

    >>> [1, 2, 3] + [4, 5, 6]
    [1, 2, 3, 4, 5, 6]

Операция `*`, применённая к списку и целому числу, конкатенирует (склеивает)
список с собой указанное количество раз:

    >>> [1, 2] * 5
    [1, 2, 1, 2, 1, 2, 1, 2, 1, 2]
    >>> ys = [0] * 10
    >>> ys
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]

В примере с `ys` мы создали список из нулей длины 10. Вообще, это распространённый
приём. Если в задаче требуется иметь список чисел заданной длины, заполненный
изначально нулями, то просто умножаем список из одного нуля `[0]` на заданную
длину: `[0] * n`.

К спискам применимы и сокращённые операторы присваивания:

    >>> a = [2, 3, 4]
    >>> a += [5, 7, 8]
    >>> a
    [2, 3, 4, 5, 7, 8]
    >>> b = [1, 2]
    >>> b *= 3
    [1, 2, 1, 2, 1, 2]

Операция `in` позволяет узнать, есть ли в списке данное значение:

    >>> 5 in [2, 3, 5, 7]
    True
    >>> 10 in [2, 3, 5, 7]
    False
    >>> 10 not in [2, 3, 5, 7]
    True

### Полезные методы списков

Самый распространённый метод — `xs.append(x)` — добавляет элемент в конец
списка.

    >>> xs = []
    >>> xs.append(10)
    >>> xs.append('hello')
    >>> xs.append([])
    >>> xs.append(True)
    >>> xs
    [10, 'hello', [], True]

Метод `xs.sort()` сортирует список на месте. Список можно отсортировать,
если к его элементам применимы отношения `>`, `<`, `>=` и т.д., в противном
случае получим ошибку.

    >>> xs = [12, 54, 15, 11, 20, 21]
    >>> xs.sort()
    >>> xs
    [11, 12, 15, 20, 21, 54]

Список сортируется _на месте,_ т.е. его содержимое изменяется.

Метод `xs.count(x)` возвращает количество элементов с заданным значением:

    >>> xs = [1, 2, 5, 7, 1, 5, 1, 1, 2, 0, 2, 1]
    >>> xs.count(1)
    5

### Полезные функции, работающие со списками

На самом деле, многие из рассмотренных функций могут работать не только
со списками, но и с любыми другими итерируемыми последовательностями,
но об этом поговорим позже.

Функция `max(xs)` возвращает наибольшее значение в списке. Список должен
быть не пустым. `min(xs)` — соответственно, наименьшее значение.

    >>> max([13, 1, 15, 11, 20, 21])
    21
    >>> min([13, 1, 15, 11, 20, 21])
    1

Функция `sorted(xs)` возвращает новый список со значениями, отсортированными
по возрастанию. _Исходный список не меняется._

    >>> xs = [12, 54, 15, 11, 20, 21]
    >>> ys = sorted(xs)
    >>> xs
    [12, 54, 15, 11, 20, 21]
    >>> ys
    [11, 12, 20, 21, 54]

Функция `reversed(xs)` строит итерируемую последовательность элементов списка
в обратном порядке. Чтобы её сделать списком, её нужно передать конструктору
`list`:

    >>> rs = reversed([12, 54, 15, 11, 20, 21])
    >>> rs
    <list_reverseiterator object at 0x000001602264DE80>
    >>> ys = list(rs)
    >>> ys
    [21, 20, 11, 15, 54, 12]


Кортежи (`tuple`)
-----------------

**Кортеж** — неизменяемый контейнер с элементами, нумеруемыми последовательными
целыми числами. Используется для группировки нескольких значений в одно.

Конструктор типа — функция `tuple`, работает аналогично функции `list`.

Запись кортежей — перечисление элементов через запятую в круглых скобках, иногда
снаружи круглые скобки можно опустить:

    >>> xs = (2, 3, 5, 7, 11)
    >>> xs
    (2, 3, 5, 7, 11)
    >>> ys = 2, 3, 5, 7, 11
    >>> ys
    (2, 3, 5, 7, 11)
    >>> xs == ys
    True

Чтобы создать кортеж из одного элемента, нужно после него добавить запятую:

    >>> number_one = (1)
    >>> number_one
    1
    >>> tuple_with_one = (1,)
    >>> tuple_with_one
    (1,)
    >>> other_tuple_with_one = 1,
    >>> other_tuple_with_one
    (1,)

Запятая после 1 означает, что это кортеж, а не просто число.

Кортеж можно считать аналогом списка, содержимое которого запрещено изменять:

    >>> xs = [1, 2, 3]
    >>> xs[0]
    1
    >>> xs[0] = 10
    >>> xs
    [10, 2, 3]
    >>> ys = (1, 2, 3)
    >>> ys[0]
    1
    >>> ys[0] = 10
    ‹СООБЩЕНИЕ ОБ ОШИБКЕ›

В программе, как правило, списки используют для представления набора однородных
данных (список чисел, список строк, список каких-то объектов) неизвестной длины
(длина определяется входными данными), который можно менять. Кортежи используются
для представления разнородных данных, они небольшого размера и длина известна
программисту на момент написания программы.

Упаковка и распаковка списков и кортежей
----------------------------------------

Если длина списка или кортежа известна, то его содержимое можно распаковать
оператором присваивания. Для этого слева нужно перечислить через запятую столько
переменных, сколько элементов в самом контейнере:

    >>> xs = [2, 3, 4]
    >>> a, b, c = xs
    >>> a
    2
    >>> b
    3
    >>> c
    4
    >>> ys = 7, 5, 9, 8
    >>> a, b, c, d = ys
    >>> c
    9

Такой приём удобен, если список или кортеж небольшой. Если контейнер справа
в операторе присваивания большой, то при помощи распаковки можно выделить
несколько значений в начале, в конце, а всё, что между ними — поместить
в новый _список._ Перед переменной, куда будет помещён список, нужно поставить
звёздочку:

    >>> xs = [1, 2, 3, 4, 5, 6, 7]
    >>> a, b, *ys, c, d = xs
    >>> a
    1
    >>> b
    2
    >>> c
    6
    >>> d
    7
    >>> ys
    [3, 4, 5]

Переменная со звёздочкой может быть только одна, в эту переменную всегда
попадает список, даже если справа находится не список:

    >>> xs = 1, 2, 3, 4
    >>> *ys, z = xs
    >>> ys
    [1, 2, 3]
    >>> z
    4

Распаковка контейнеров позволяет элегантно **обменивать значения двух
переменных:**

    >>> a = 7
    >>> b = 8
    >>> a, b = b, a
    >>> a
    8
    >>> b
    7

Справа в операторе присваивания строится кортеж `(b, a)` (скобки тут опущены),
который тут же распаковывается.

### Возврат нескольких значений из функции

В Python, в отличие от языков типа C++ или Pascal, нет параметров-ссылок, т.е.
нет возможности из функции изменить значение переменной, которая передана
как параметр:

    def some_function(‹какие-то параметры›):
        ...
        a = 100
        b = [1, 2, 3]
        other_function(a, b)
        ...

После вызова `other_function` переменные `a` и `b` будут иметь те же значения,
что и до вызова — в `a` будет лежать число `100`, в `b` — ссылка на тот же список
(хотя содержимое списка может измениться). В Python нет возможности изменить
значения переменных из вызванной функции.

Поэтому поступить как в Паскале или C++ — передать параметр по ссылке и изменить
его внутри функции, мы не можем.

Единственный способ передать из вызова функции наружу — вернуть значение при
помощи `return`.

Если мы хотим передать из функции несколько значений — нам нужно упаковать их
в какой-нибудь контейнер и вернуть контейнер. В качестве такого контейнера
чаще всего используют кортеж.

Если в операторе `return` перечислить через запятую несколько значений, функция
вернёт кортеж из этих значений:

    return a, b, c

Для анализа этих значений можно использовать распаковку

    def divmod(a, b):
        return a // b, a % b

Функция `divmod(a, b)` выполняет деление с остатком: возвращает частное и остаток.

    >>> div, rem = divmod(30, 4)
    >>> div
    7
    >>> rem
    2

Срезы строк, списков и кортежей
-------------------------------
Ранее мы говорили, что операция индексирования `xs[i]` позволяет обратиться
к одному элементу строки, списка или кортежа. В случае списков, операция
индексирования может располагаться в левой части оператора присваивания:

    xs[5] = 6

поскольку список является изменяемым типом данных.

Однако, при помощи операции индексирования можно обращаться и целым участкам
последовательностей, т.е. списков, строк или кортежей. Это так называемый
синтаксис **срезов:**

    xs[‹start›:‹limit›:‹step›]

где

* `‹start›` — индекс первого элемента среза,
* `‹limit›` — индекс граничного элемента среза, т.е. участок от `‹start›`
  до `‹limit›` включает в себя `‹start›` и не включает в себя `‹limit›`.
  Пользуясь математическими обозначениями, границы можно записать как
  полуоткрытый интервал `[‹start›, ‹limit›)`.
* `‹step›` — шаг, с которым выбираются элементы.

Каждый из этих компонентов может отсутствовать, в этом случае подразумевается:

* отсутствует `‹start›` — подразумевается от начала последовательности,
* отсутствует `‹limit›` — до конца последовательности, т.е. до `len(xs)`,
* отсутствует `‹step›` — шаг равен 1, т.е. элементы перечисляются без
  пропусков.

Например:

              0  1  2  3   4   5   6   7
    >>> xs = [2, 3, 5, 7, 11, 13, 17, 19]
             -8 -7 -6 -5  -4  -3  -2  -1
    >>> len(xs)
    8
    >>> xs[3:6]
    [7, 11, 13]
    >>> xs[2:-2]
    [5, 7, 11, 13]
    >>> xs[:4]
    [2, 3, 5, 7]
    >>> xs[4:]
    [11, 13, 17, 19]
    >>> xs[3:6:2]
    [7, 11]
    >>> xs[::3]
    [2, 7, 17]

Шаг может быть отрицательным — в этом случае элементы перечисляются в обратном
порядке. В этом случае `‹start›` должен быть больше, чем `‹limit›`:

    >>> xs[::-3]
    [19, 11, 3]
    >>> xs[1:6:-2]
    []
    >>> xs[6:1:-2]
    [17, 11, 5]

На практике чаще всего используют отрицательный шаг `-1` для того, чтобы
перевернуть список, кортеж или строку:

    >>> xs[::-1]
    [19, 17, 13, 11, 7, 5, 3, 2]
    >>> s = 'hello'
    >>> s[::-1]
    'olleh'
    >>> "Madam, I'm Adam"[::-1]
    "mada m'I madaM"
    >>> "Eve"[::-1]
    'evE'

Списки являются изменяемой структурой данных, с ними можно использовать
присваивания срезам:

    >>> xs
    [2, 3, 5, 7, 11, 13, 17, 19]
    >>> xs[3:6]
    [7, 11, 13]
    >>> xs[3:6] = [33, 44, 55]
    >>> xs
    [2, 3, 5, 33, 44, 55, 17, 19]
    >>> xs[2:4] = [111, 222, 333]
    >>> xs
    [2, 3, 111, 222, 333, 44, 55, 17, 19]
    >>> xs[-4:-1] = []
    [2, 3, 111, 222, 333, 19]

А что означает срез `xs[:]`? Очевидно, это всё содержимое списка от начала
и до конца. Зачем оно нужно? На практике такой срез используется, чтобы
получить копию списка.

Дело в том, что список — ссылочный тип данных. Когда мы присваиваем список
другой переменной, то у нас копируется только ссылка — обе переменные
ссылаются на один и тот же список. Можно сказать, что у одного списка
получаются два равноправных псевдонима.

И если теперь поменять значение списка через одну переменную, мы это же
изменение увидим через другую:

    >>> xs = [2, 3, 5, 7, 11]
    >>> ys = xs                        # Здесь мы скопировали ссылку
    >>> ys
    [2, 3, 5, 7, 11]
    >>> xs[2] = 88
    >>> ys[2]
    88
    >>> xs
    [2, 3, 88, 7, 11]
    >>> ys
    [2, 3, 88, 7, 11]
    >>> ys.append(100500)
    >>> ys
    [2, 3, 88, 7, 11, 100500]
    >>> xs
    [2, 3, 88, 7, 11, 100500]

Переменные `xs` и `ys` в примере — два псевдонима для одного объека списка.
В этом примере в памяти компьютера находится один список, на который ссылаются
переменные `xs` и `ys`, можем видеть и менять его содержимое через любую из них.

    >>> xs = [2, 3, 5, 7, 11]
    >>> zs = xs[:]                     # Здесь мы сделали срез [:]!!!
    >>> zs
    [2, 3, 5, 7, 11]
    >>> xs[2] = 88
    >>> zs[2]
    5
    >>> xs
    [2, 3, 88, 7, 11]
    >>> zs
    [2, 3, 5, 7, 11]
    >>> zs.append(100500)
    >>> zs
    [2, 3, 5, 7, 11, 100500]
    >>> xs
    [2, 3, 88, 7, 11]

Во втором примере мы при помощи среза `xs[:]` создали новый список с тем же
содержимым. Т.е. в памяти компьютера образовалось два равных списка, на один
ссылается переменная `xs`, на другой — `zs`. Через переменную `xs` мы можем
видеть и менять содержимое первого списка, через `zs` — второго. Изменения
обоих списков независимы.

Срез `xs[:]` может использоваться для изменения содержимого всего списка.

    >>> xs = [2, 3, 5, 7]
    >>> ys = xs
    >>> ys = [11, 12, 13]
    >>> xs
    [2, 3, 5, 7]

Когда мы присвоили переменной `ys` новый список, мы просто в неё положили
ссылку на новый список. Содержимое списка `xs` мы не меняли.

    >>> xs = [2, 3, 5, 7]
    >>> ys = xs
    >>> ys[:] = [11, 12, 13]           # Присваиваем срезу ys[:]!!!
    >>> xs
    [11, 12, 13]

Тут мы поменяли содержимое списка, на который ссылаются две переменные `xs`
и `ys` через переменную `ys`. Соответственно, т.к. эти переменные — псевдонимы,
через `xs` видно изменение.


Ещё про ссылочные типы данных
-----------------------------
В Python все данные — ссылочные. Но для неизменяемых типов (`int`, `float`,
`str`, `tuple`) это не важно, т.к. для них копирование ссылки эквивалентно
копированию значения.

Для изменяемых типов данных (`list`, `dict`, `set`) о том, что данные ссылочные,
помнить нужно. Присваивание переменной не создаёт новый список (или словарь,
или множество), а просто копирует ссылку на объект, создаёт псевдоним.
Изменения, сделанные через один псевдоним, будут видны и через другой. Чтобы
создать новый объект и менять его независимо, нужно его явно скопировать.
Например, для списка при помощи среза `xs[:]`.

Частный случай присваивания — присваивания параметрам при вызове функции:

    def func(xs):
        xs[0] = 1

При вызове этой функции содержимое списка будет меняться:

    >>> ys = [5, 7, 9]
    >>> func(ys)
    >>> ys
    [1, 7, 9]

При вызове функции параметру `xs` была присвоена ссылка на тот же список,
что и в переменной `ys` — а значит, функция изменила чужой список.

    >>> zs = [5, 7, 9]
    >>> func(zs[:])
    >>> zs
    [5, 7, 9]

Тут мы хитрые, передали в функцию копию списка, функция поменяла содержимое
копии, исходный список остался неприкосновенным.


Словари (`dict`)
----------------
Ранее мы рассматривали последовательности — контейнеры, элементы в которых
сопоставлялись последовательным целым числам: от 0 до N−1 или (если ссылаться
справа налево) от −1 до −N. К элементам последовательности мы обращаемся
по номеру.

**Словарь** (`dict`) — контейнер, к элементам которого можно обращаться
по ключам, например, строкам. Словарь хранит внутри себя пары значений
в произвольном порядке. Первый элемент каждой пары называется **ключом,**
второй — **значением.** Каждому ключу сопоставляется ровно одно значение —
ключи повторяться не могут. А значения повторяться могут.

Словарь позволяет находить или изменять значение (второй компонент пары),
зная её ключ. Синтаксис тот же, что и при индексации массива:

    >>> exam_scores['Вася'] = 5
    >>> exam_scores['Маша']
    4

Т.е. в словаре `exam_scores` (экзаменационные оценки) с ключом `'Вася'` мы
связали значение `5`, ранее с другим ключом `'Маша'` было связано значение `4`.

Можно сказать, что ключ — это «имя» для некоторого значения.

Конструктор словаря — функция `dict()`. Без параметров создаёт пустой словарь,
её параметром может быть список пар.

    >>> dict()
    {}
    >>> dict( [('Вася', 5), ('Маша', 4), ('Коля', 4), ('Лена', 5)] )
    {'Вася':5, 'Маша':4, 'Коля':4, 'Лена':5}

Создать словарь можно, перечислив его содержимое в фигурных скобках. Содержимое
записывается как пары `‹ключ› : ‹значение›`, перечисленные через запятую. В каждой
паре ключ и значения разделяются двоеточием:

    >>> d = { 'Саша':3, 'Кеша':2 }
    >>> d
    {'Саша':3, 'Кеша':2}

Ключами словаря могут служить только неизменяемые значения:

* числа: `int`, `float`,
* строки `str`,
* кортежи (`tuple`) из других неизменяемых значений.

### Операции со словарями

Обращаться к элементам словаря можно при помощи операции индексации, примеры
на которую мы рассмотрели выше:

    >>> exam_scores['Вася'] = 5
    >>> exam_scores['Маша']
    4

Объединять значения двух словарей можно при помощи операции `|`: `d1 | d2`,
при этом значения из `d2` имеют приорирет, т.е. если в обоих словарях есть
одинаковые ключи, то значения для них берутся из второго словаря:

    >>> d1 = {'a' : 5, 'b' : 7, 'c' : 8 }
    >>> d2 = {'d' : 4, 'f' : 1, 'c' : 0 }
    >>> d12 = d1 | d2
    >>> d12
    {'a':5, 'b':7, 'c':0, 'd':4, 'f':1}
    >>> d2 | d1
    {'a':5, 'b':7, 'c':8, 'd':4, 'f':1}

Операция `del` позволяет удалить значение из словаря:

    >>> d1 = {'a' : 5, 'b' : 7, 'c' : 8 }
    >>> del d1['b']
    >>> d1
    {'a':5, 'c':8}

### Полезные методы словарей

**Метод `dict.get()`** извлекает значение из словаря:

    d.get(key)
    d.get(key, default)

Операция индексации при обращении к несуществующему ключу приводит к ошибке
(как и при выходе за границы списка).

    >>> d = {'a':5, 'b':8, 'c':10}
    >>> d['a']
    5
    >>> d['d']
    ‹СООБЩЕНИЕ ОБ ОШИБКЕ›

Метод `get` к ошибке не приводит. Если ключа не существует, то возвращается
значение по умолчанию `default`, если `default` не указан, то подразумевается
`None`:

    >>> d.get('d')
    >>> print(d.get('d'))
    None
    >>> d.get('d') == None
    True
    >>> d.get('a')
    5
    >>> d.get('a', 100500)
    5
    >>> d.get('d', 100500)
    100500

При помощи метода `get` можно представлять себе словарь как бесконечный,
при этом всем реально не существующим ключам `get` сопоставляет значение
по умолчанию.

Например, если мы посчитываем какие-то значения (например, слова), то можем
считать, что для несуществующих слов их количество равно нулю, вызывая
`words.get(word, 0)`.

**Пример.** Напишем функцию `dict_get`, имитирующую поведение метода `get`:

    def dict_get(d, key, default):
        d_ext = {key : default} | d
        return d_ext[key]

В словаре `d_ext` заведомо будет нужный ключ, т.к. он получен объединением
словаря `{key : default}` с исходным. При этом в операции объединения `|`
исходный словарь указан справа, поэтому если в нём есть искомое значение,
то оно перекроет значение `default` из словаря слева. Если нет, в `d_ext`
останется `default` для ключа `key`.


**Метод `items`** возвращает список (на самом деле, итератор, но о них позже)
с парами `(‹ключ›, ‹значение›)`.

    >>> d = {'a':5, 'b':8, 'c':10}
    >>> list(d.items())
    [('a', 5), ('b', 8), ('c', 10)]

Метод `items` удобно использовать в цикле `for` (об этом на следующей лекции).

**Метод `copy`** создаёт копию словаря (похож на срез `xs[:]` для списков).


Множество (`set`)
-----------------
Тип данных «множество» (`set`) хранит неупорядоченный набор значений без
повторений. Элементами множества могут быть только неизменяемые типы
данных (как и ключи в словаре): числа, строки, кортежи из чисел и строк.

В отличие от списка, данные во множестве неупорядочены — при переборе
его содержимого элементы будут просматриваться в произвольном порядке.
Т.е. как множество захочет расположить внутри себя элементы, так
и расположит, мы на это повлиять никак не можем.

Элементы во множестве не повторяются — если мы попробуем добавить
ко множеству элемент, который там присутствует, то множество просто
не изменится.

### Контструктор и литералы
Конструктор множества — `set`, может быть вызван без параметров,
тогда будет создано пустое множество, может получать на входе некоторый
другой контейнер (например, список или строку) — будет построено
множество из элементов этого контейнера.

    >>> empty = set()                  # создание пустого множества
    >>> empty
    set()
    >>> hello = set('hello')
    >>> hello                          # в реальности они могут быть
    { 'h', 'e', 'l', 'o' }             # показаны в любом порядке

Можно создать множество путём перечисления элементов в фигурных скобках:

    >>> primes = { 2, 3, 5, 7, 11 }
    >>> primes
    { 2, 3, 5, 7, 11 }

В Python фигурные скобки используются в двух ролях: для создания словарей
и создания множеств. Разница между ними в том, что при создании словарей
указываются ключи:

    >>> xs = { 'Вася': 5, 'Петя': 4 }
    >>> ys = { 'Вася', 'Петя' }

В переменной `xs` будет находиться словарь, в переменной `ys` будет
находиться множество. Поскольку мы отличаем создание словаря от создания
множества по содержимому фигурных скобок, то пустые фигурные скобки `{}`
могут трактоваться неоднозначно: и как пустой словарь, и как пустое
множество.

Поскольку на практике словари используются чаще множеств, разработчики
Python решили, что пустые фигурные скобки `{}` будут представлять пустой
словарь. А для создания пустого множества нужно вызывать конструктор `set()`
без параметров.

### Основные операции над множествами

Операция `in` (`not in`) проверяет входит ли (не входит ли) элемент
во множество:

    >>> primes = { 2, 3, 5, 7, 11 }
    >>> 5 in primes
    True
    >>> 6 in primes
    False
    >>> 6 not in primes
    True

Операция `|`, как и для словарей, строит объединение множеств:

    >>> xs = { 2, 4, 6, 8 }
    >>> ys = { 2, 3, 5, 7 }
    >>> xs | ys
    { 2, 3, 4, 5, 6, 7, 8 }

Операция `&` строит пересечение множеств:

    >>> xs & ys
    { 2 }

Операция `-` вычисляет разность множеств:

    >>> xs - ys
    { 3, 5, 7 }
    >>> ys - xs
    { 4, 6, 8 }

Для этих операций есть соответствующие сокращёные записи оператора
присваивания: `|=`, `&=`, `-=`.

### Некоторые методы множеств

Самый основной метод — метод `.add(x)`, добавляющий элемент во множество:

    >>> s = set()
    >>> s.add(2)
    >>> s.add(3)
    >>> s
    { 2, 3 }
    >>> s.add(2)
    >>> s
    { 2, 3 }

Метод `.remove(x)` удаляет элемент из множества. Если его вызвать
к отсутствующему элементу, получим ошибку. Для того, чтобы удалить элемент,
но при этом не получить ошибку, если он отсутствовал, нужно просто вычесть
множество из одного элемента:

    >>> s.remove(3)
    >>> s
    { 2 }
    >>> s.remove(3)
    ‹сообщение об ошибке KeyError›
    >>> s -= { 2 }
    >>> s
    set()
    >>> s -= { 2 }
    >>> s
    set()

### Пример применения множеств

Дан список элементов. Составить новый список, в котором отстутсвуют дубликаты,
причём порядок не важен. Для этого мы из списка делаем множество, а из него —
снова список:

    >>> xs = [ 3, 7, 8, 2, 3, 4 ]
    >>> ys = list(set(xs))
    >>> ys
    [ 3, 4, 2, 8, 7 ]

Дан список элементов. Проверить — есть ли в нём дубликаты?

    def has_repeated(xs):
        return len(xs) > len(set(xs))

Почему работает эта функция? Потому что если в списке будут дубликаты,
то множество, построенное из него, будет содержать меньше элементов,
чем в исходном списке.
