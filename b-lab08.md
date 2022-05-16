Лабораторная работа № 8. Написание консольных утилит
====================================================

Задача 1. Команда `echo` (1 балл)
---------------------------------
Команда `echo` в unix-подобных ОС печатает аргументы командной строки,
разделяя их пробелами.

Требуется написать программу `echo.py`, которая своим поведением повторяет
действие встроенной команды `echo`.

```
$ python echo.py Hello, World!
Hello, World!
```

Задача 2. Команда `sort` (2 балла)
----------------------------------
Команда `sort` в unix-подобных ОС принимает несколько имён файлов, объединяет
их содержимое, сортирует строки в алфавитном порядке и выводит результат
на стандартный вывод.

Если имена файлов не заданы, читается стандартный ввод.

Требуется написать программу `sort.py`, которая имитирует работу встроенной
программы `sort`.

Задача 3. Программа `decimate.py` (2 балла)
-------------------------------------------
В обработке сигналов **децимацией** называется прореживание отсчётов
цифрового сигнала — передача на выход каждого N-го отсчёта.

Требуется написать программу `decimate.py`, которая принимает в командной
строке число N и имена входных файлов, и отправляет на выход только N-е
строки каждого из файлов.

Допустим, входной файл `to be.txt` содержит следующий текст:

```
To be, or not to be, that is the question;
Whether 'tis nobler in the mind to suffer
The Slings and Arrows of outrageous Fortune
Or to take arms against a sea of troubles,
And by opposing, end them. To die, to sleep;
No more; and by a sleep to say we end
The heart-ache and the thousand natural shocks
That flesh is heir to - 'tis a consummation
Devoutly to be wish'd. To die, to sleep;
To sleep, perchance to dream. Ay, there's the rub,
For in that sleep of death what dreams may come,
When we have shuffled off this mortal coil,
Must give us pause.
```

Тогда программа `decimate.py` должна работать вот так:

```
$ python decimate.py 3 "to be.txt"
To be, or not to be, that is the question;
Or to take arms against a sea of troubles,
The heart-ache and the thousand natural shocks
To sleep, perchance to dream. Ay, there's the rub,
Must give us pause.
$ python decimate.py 5 "to be.txt"
To be, or not to be, that is the question;
No more; and by a sleep to say we end
For in that sleep of death what dreams may come,
$ python decimate.py 2 "to be.txt"
To be, or not to be, that is the question;
The Slings and Arrows of outrageous Fortune
And by opposing, end them. To die, to sleep;
The heart-ache and the thousand natural shocks
Devoutly to be wish'd. To die, to sleep;
For in that sleep of death what dreams may come,
Must give us pause.
```

Программа должна придерживаться соглашения для unix-утилит: на входе может
быть несколько файлов, если имена файлов не указаны, то должен читаться
стандартный ввод.