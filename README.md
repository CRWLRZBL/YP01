# YP01
Штучки с змейкой

import math

# Ввод x и вычисление функции y(x)
x = float(input("Введите x: "))
if x < -10:
    y = math.pi * (x ** 2)
elif -10 <= x < -5:
    y = x ** 2
elif -5 <= x < 10:
    y = math.e * abs(x)
else:  # x >= 10
    y = 1 / math.sin(math.sqrt(x))
print("Значение функции y(x) = {:.3f}".format(y))

# Ввод трех чисел и вывод числа между двумя другими
a = float(input("Введите первое число: "))
b = float(input("Введите второе число: "))
c = float(input("Введите третье число: "))
median = a if (b < a < c) or (c < a < b) else (b if (a < b < c) or (c < b < a) else c)
print("Число, находящееся между двумя другими:", median)

# Определение количества дней в месяце
year = int(input("Введите год: "))
month = int(input("Введите номер месяца (1-12): "))
days_in_month = 31 if month in [1, 3, 5, 7, 8, 10, 12] else 30 if month in [4, 6, 9, 11] else (29 if (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0) else 28)
print("Количество дней в месяце:", days_in_month)

# Проверка возможности построить треугольник
side1 = float(input("Введите первую сторону: "))
side2 = float(input("Введите вторую сторону: "))
side3 = float(input("Введите третью сторону: "))

can_form_triangle = (side1 + side2 > side3) and (side1 + side3 > side2) and (side2 + side3 > side1)
if can_form_triangle:
    if side1 == side2 == side3:
        triangle_type = "равносторонний"
    elif side1**2 + side2**2 == side3**2 or side1**2 + side3**2 == side2**2 or side2**2 + side3**2 == side1**2:
        triangle_type = "прямоугольный"
    else:
        triangle_type = "равнобедренный"
    print("Треугольник можно построить, его тип:", triangle_type)
else:
    print("Треугольник нельзя построить.")

# Ввод двух чисел и битовой операции
num1 = int(input("Введите первое целое число: "))
num2 = int(input("Введите второе целое число: "))
operation = input("Введите битовую операцию (и, или, исключающее или, сдвиг влево, сдвиг вправо): ")

result = None
if operation == 'и':
    result = num1 & num2
elif operation == 'или':
    result = num1 | num2
elif operation == 'исключающее или':
    result = num1 ^ num2
elif operation == 'сдвиг влево':
    result = num1 << num2
elif operation == 'сдвиг вправо':
    result = num1 >> num2

print("Исходные числа: {} и {}".format(num1, num2))
print("Результат операции: {}".format(result))
print("Результат в двичном виде: {}".format(bin(result)[2:])) if result is not None else print("Неверная операция.")
