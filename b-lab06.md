Лабораторная работа № 6. Работа в консоли ОС
============================================

Список `sys.argv`
-----------------
Для доступа к параметрам командной строки в программах на Python используется
список `sys.argv`, доступный из библиотечного модуля `sys`. Для подключения
модуля нужно добавить строчку

```python
import sys
```

в начало программы.

Нулевым элементом списка `sys.argv[0]` является имя самой программы, остальные
элементы — параметры командной строки, указанные после имени программы.

Пример. Пусть у нас имеется следующая программа `example.py`:

```python
import sys

print(sys.argv)
```
Тогда при запуске из консоли получим:
```
C:\Users\Mazdaywik>python example.py one two three
['example.py', 'one', 'two', 'three']
```
Список `sys.argv` нам сегодня потребуется при выполнении лабораторной работы.


Задание на лабораторную (4 балла)
---------------------------------

Нужно будет выполнить следующие действия и в конце занятия продемонстрировать
окно консоли с процессом работы.

1.  Откройте окно консоли.
2.  Перейдите в папку, в которой Вы будете работать.
    * Если работаете на университетском компьютере, перейдите в папку `D:\TEMP`:
      ```
      C:\Users\User>D:
      D:\>cd D:\TEMP
      D:\TEMP>
      ```
    * Если работаете на личном ноутбуке, перейдите в папку рабочего стола `Desktop`.
      На Windows:
      ```
      C:\Users\‹ваше имя›>cd Desktop
      C:\Users\Desktop>
      ```
      На macOS:
      ```
      [‹ваше имя›@‹имя компьютера›:~]$ cd Desktop
      [‹ваше имя›@‹имя компьютера›:~/Desktop]$
      ```
      Файлы, значки которых отображаются на рабочем столе, на самом деле лежат
      в папке `Desktop`. И наоборот, если создать файл в папке `Desktop`, то его
      значок отобразится на рабочем столе.
3.  Используя командную строку, в выбранной папке (`D:\TEMP` или `Desktop`)
    создайте папку `lab6`.
4.  Перейдите в папку `lab6`.
5.  Используя командную строку, создайте текстовый файл `example.txt`
    с произвольным текстом на английском языке. Например, таким:
    ```
    To be, or not to be, that is the question;
    Whether 'tis nobler in the mind to suffer
    The Slings and Arrows of outrageous Fortune
    Or to take arms against a sea of troubles,
    And by opposing, end them.
    ```
    На Windows используйте `copy con example.txt`, на macOS — `cat > example.txt`.
6.  Скопируйте файл `example.txt` в файл `copy.txt`.
7.  Выведите на экран подробное содержимое папки (`dir` или `ls`)
8.  Удалите файл `copy.txt`.
9.  Откройте Python, создайте в папке `lab6` файл `show_file.py` со следующим содержимым:
    ```python
    import sys

    def show_file(filename):
        with open(filename) as f:
            for line in f:
                print(line, end='')

    if len(sys.argv) > 1:
        show_file(sys.argv[1])
    else:
        print('No filename')
    ```
10. Выполните в командной строке следующие команды:
    ```
    D:\TEMP\lab6>python show_file.py
    …
    D:\TEMP\lab6>python show_file.py example.txt
    …
    D:\TEMP\lab6>python show_file.py show_file.py
    ```
    (На macOS вместо `python` следует использовать `python3`.)
11. Скопируйте файл `show_file.py` в `num_file.py`.
12. Откройте файл `num_file.py` в среде IDLE (File → Open…), добавьте в программу
    нумерацию строк (см. [Лабораторную работу № 3](b-lab03.md), функцию
    `num_lines(filename)`).
13. Выполните следующие команды:
    ```
    D:\TEMP\lab6>python num_file.py
    …
    D:\TEMP\lab6>python num_file.py example.txt
    …
    D:\TEMP\lab6>python num_file.py show_file.py
    …
    D:\TEMP\lab6>python num_file.py num_file.py
    ```
