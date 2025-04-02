# YP01
Штучки с змейкой

# Класс Автор
class Author:
    def __init__(self, full_name: str, country: str):
        self.full_name = full_name
        self.country = country

    def display_info(self):
        """Выводит информацию об авторе."""
        print(f"Автор: {self.full_name}, Страна: {self.country}")

# Класс Книга
class Book:
    def __init__(self, title: str):
        self.title = title
        self._content = []  # Приватное поле содержание
        print(f"Книга '{self.title}' создана")

    def __del__(self):
        print(f"Книга '{self.title}' удалена")

    def add_work(self, work: str):
        """Добавляет произведение в содержание книги."""
        self._content.append(work)

    def get_work_count(self):
        """Возвращает количество произведений в книге."""
        return len(self._content)

    def display_info(self):
        """Выводит информацию о книге."""
        print(f"Книга: {self.title}")
        print("Содержание:")
        for idx, work in enumerate(self._content, start=1):
            print(f"{idx}) {work}")

# Класс КнигаАвтора, наследующий от Автор и Книга
class BookAuthor(Author, Book):
    def __init__(self, full_name: str, country: str, title: str):
        Author.__init__(self, full_name, country)
        Book.__init__(self, title)

    def display_full_info(self):
        """Выводит полную информацию об авторе и книге."""
        self.display_info()  # Информация об авторе
        Book.display_info(self)  # Информация о книге

# Основная программа
def main():
    authors = []
    n = int(input("Введите количество авторов: "))

    # Ввод данных от пользователя
    for _ in range(n):
        full_name = input("Введите ФИО автора: ")
        country = input("Введите страну автора: ")
        title = input("Введите название книги: ")
        
        # Создание экземпляра BookAuthor
        book_author = BookAuthor(full_name, country, title)
        
        # Ввод произведений книги
        while True:
            work = input("Введите название произведения (или 'exit' для выхода): ")
            if work.lower() == 'exit':
                break
            book_author.add_work(work)
        
        authors.append(book_author)
    
    # Вывод всех авторов
    print("\nСписок всех авторов:")
    for author in authors:
        author.display_info()

    # Вывод только русских авторов
    print("\nСписок русских авторов:")
    for author in authors:
        if author.country.lower() == "россия":
            author.display_info()

    # Вывод содержания книг
    print("\nСодержание книг:")
    for author in authors:
        author.display_full_info()

if __name__ == "__main__":
    main()


В этой версии кода добавлен вывод содержания книг в конце программы. После вывода информации обо всех авторах и только российских авторах, программа теперь также выводит полную информацию о каждом авторе вместе с его книгой и содержанием.


# Класс Автор
class Author:
    def __init__(self, full_name: str, country: str):
        self.full_name = full_name
        self.country = country

    def display_info(self):
        """Выводит информацию об авторе."""
        print(f"Автор: {self.full_name}, Страна: {self.country}")

# Класс Книга
class Book:
    def __init__(self, title: str):
        self.title = title
        self._content = []  # Приватное поле содержание
        print(f"Книга '{self.title}' создана")

    def __del__(self):
        print(f"Книга '{self.title}' удалена")

    def add_work(self, work: str):
        """Добавляет произведение в содержание книги."""
        self._content.append(work)

    def get_work_count(self):
        """Возвращает количество произведений в книге."""
        return len(self._content)

    def display_info(self):
        """Выводит информацию о книге."""
        print(f"Книга: {self.title}")
        print("Содержание:")
        for idx, work in enumerate(self._content, start=1):
            print(f"{idx}) {work}")

# Класс КнигаАвтора, наследующий от Автор и Книга
class BookAuthor(Author, Book):
    def __init__(self, full_name: str, country: str, title: str):
        Author.__init__(self, full_name, country)
        Book.__init__(self, title)

    def display_full_info(self):
        """Выводит полную информацию о авторе и книге."""
        self.display_info()  # Информация об авторе
        Book.display_info(self)  # Информация о книге

# Основная программа
def main():
    authors = []
    n = int(input("Введите количество авторов: "))

    # Ввод данных от пользователя
    for _ in range(n):
        full_name = input("Введите ФИО автора: ")
        country = input("Введите страну автора: ")
        title = input("Введите название книги: ")
        
        # Создание экземпляра BookAuthor
        book_author = BookAuthor(full_name, country, title)
        
        # Ввод произведений книги
        while True:
            work = input("Введите название произведения (или 'exit' для выхода): ")
            if work.lower() == 'exit':
                break
            book_author.add_work(work)
        
        authors.append(book_author)
    
    # Вывод всех авторов
    print("\nСписок всех авторов:")
    for author in authors:
        author.display_info()

    # Вывод только русских авторов
    print("\nСписок русских авторов:")
    for author in authors:
        if author.country.lower() == "россия":
            author.display_info()

if __name__ == "__main__":
    main()


В этой реализации класса BookAuthor добавлена возможность создания книги с произведениями. В основной программе пользователь может вводить произведения книги, а затем выводится информация обо всех авторах и только о русских авторах.

# Функция возведения числа a в степень x
def power(a: 'основание степени' = 2, x: 'показатель степени' = 1):
    """Возводит число a в степень x, по умолчанию a=2, x=1."""
    return a ** x

# Тестирование функции power
print(power())  # Ожидается 2
print(power(3))  # Ожидается 3
print(power(3, 2))  # Ожидается 9
print(power(4, 0))  # Ожидается 1


# Функция вычисления факториала
def factorial(n: 'целое неотрицательное число'):
    """Вычисляет факториал числа n рекурсивно. Возвращает -1 при некорректных данных."""
    if not isinstance(n, int) or n < 0:
        return -1
    if n == 0 or n == 1:
        return 1
    return n * factorial(n - 1)

# Тестирование функции factorial
print(factorial(5))  # Ожидается 120
print(factorial(-1))  # Ожидается -1
print(factorial("строка"))  # Ожидается -1


# Функция для вычисления статистики
def statistics(*args: 'числа'):
    """Выводит сумму, среднее, максимум, минимум и количество чисел."""
    if len(args) == 0:
        return 'Нет данных для анализа.'
    
    total = sum(args)
    average = total / len(args)
    maximum = max(args)
    minimum = min(args)
    count = len(args)
    
    print(f"Сумма: {total}, Среднее: {average}, Максимум: {maximum}, Минимум: {minimum}, Количество: {count}")

# Тестирование функции statistics
statistics(1, 2, 3, 4, 5)  # Ожидается 15, 3.0, 5, 1, 5
statistics()  # Ожидается 'Нет данных для анализа.'


# Функция для изменения значений списка
def multiply_list(lst: 'список чисел', multiplier: 'множитель' = -1):
    """Изменяет значения списка путем умножения каждого элемента на multiplier."""
    for i in range(len(lst)):
        lst[i] *= multiplier
    return lst

# Тестирование функции multiply_list
my_list = [1, 2, 3]
print(multiply_list(my_list))  # Ожидается [-1, -2, -3]
print(multiply_list(my_list, 2))  # Ожидается [-2, -4, -6]


# Лямбда-функция для вычисления значения y
linear_function = lambda a, x, b: a * x + b

# Тестирование лямбда-функции
print(linear_function(2, 3, 1))  # Ожидается 7
print(linear_function(1, 5, 0))  # Ожидается 5

#PR2

# Модуль с необходимыми функциями

# Функция приветствия
def hello(name: 'имя пользователя' = None):
    """Выводит приветствие. Если передано имя, выводит 'Hello, имя'."""
    if name:
        return f"Hello, {name}"
    return "Hello, World"

# Функция арифметики
def arithmetic(a: 'число', b: 'число', operation: 'операция'):
    """Выполняет арифметическую операцию над двумя числами."""
    if operation == "+":
        return a + b
    elif operation == "-":
        return a - b
    elif operation == "*":
        return a * b
    elif operation == "/":
        return a / b if b != 0 else 'Ошибка: деление на ноль'
    return "Неизвестная операция"

# Функция для вычисления свойств квадрата
def square(side: 'длина стороны квадрата'):
    """Возвращает периметр, площадь и диагональ квадрата."""
    perimeter = 4 * side
    area = side ** 2
    diagonal = (side ** 2 + side ** 2) ** 0.5
    return perimeter, area, diagonal

# Функция для определения времени года
def season(month: 'номер месяца от 1 до 12'):
    """Возвращает время года для данного месяца."""
    if month in [12, 1, 2]:
        return "Зима"
    elif month in [3, 4, 5]:
        return "Весна"
    elif month in [6, 7, 8]:
        return "Лето"
    elif month in [9, 10, 11]:
        return "Осень"
    return "Неверный месяц"

# Функция для вычисления суммы вклада
def bank(a: 'сумма вклада', years: 'количество лет'):
    """Возвращает сумму на счету через years лет с 10% годовых."""
    total = a * ((1 + 0.1) ** years)
    return total

# Примеры использования функций
if __name__ == "__main__":
    print(hello("Alice"))  # Ожидается "Hello, Alice"
    print(arithmetic(10, 5, "+"))  # Ожидается 15
    print(square(4))  # Ожидается (16, 16, 5.656854249492381)
    print(season(4))  # Ожидается "Весна"
    print(bank(1000, 5))  # Ожидается 1610.51


#PR3

# Класс Автор
class Author:
    def __init__(self, full_name: str, country: str):
        self.full_name = full_name
        self.country = country

    def display_info(self):
        """Выводит информацию об авторе."""
        print(f"Автор: {self.full_name}, Страна: {self.country}")

# Класс Книга
class Book:
    def __init__(self, title: str):
        self.title = title
        self._content = []  # Приватное поле содержание
        print(f"Книга '{self.title}' создана")

    def __del__(self):
        print(f"Книга '{self.title}' удалена")

    def add_work(self, work: str):
        """Добавляет произведение в содержание книги."""
        self._content.append(work)

    def get_work_count(self):
        """Возвращает количество произведений в книге."""
        return len(self._content)

    def display_info(self):
        """Выводит информацию о книге."""
        print(f"Книга: {self.title}")
        print("Содержание:")
        for idx, work in enumerate(self._content, start=1):
            print(f"{idx}) {work}")

# Класс КнигаАвтора, наследующий от Автор и Книга
class BookAuthor(Author, Book):
    def __init__(self, full_name: str, country: str, title: str):
        Author.__init__(self, full_name, country)
        Book.__init__(self, title)

    def display_full_info(self):
        """Выводит полную информацию о авторе и книге."""
        self.display_info()  # Информация об авторе
        self.display_info()  # Информация о книге

# Основная программа
def main():
    authors = []
    n = int(input("Введите количество авторов: "))

    # Ввод данных от пользователя
    for _ in range(n):
        full_name = input("Введите ФИО автора: ")
        country = input("Введите страну автора: ")
        authors.append(Author(full_name, country))
    
    # Вывод всех авторов
    print("\nСписок всех авторов:")
    for author in authors:
        author.display_info()

    # Вывод только русских авторов
    print("\nСписок русских авторов:")
    for author in authors:
        if author.country.lower() == "россия":
            author.display_info()

if __name__ == "__main__":
    main()


Этот код включает в себя реализацию классов Author, Book и BookAuthor. Основная программа позволяет пользователю вводить информацию об авторах и выводить информацию о них и о русских авторах. Класс Book реализует дополнительные методы для работы с содержимым книги.
