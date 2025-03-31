# YP01
Штучки с змейкой

import random

# Генерация случайного числа и проверка на простоту
random_number = random.randint(1, 1000)
is_prime = True

if random_number < 2:
    is_prime = False
else:
    for i in range(2, int(random_number ** 0.5) + 1):
        if random_number % i == 0:
            is_prime = False
            break

print("Случайное число:", random_number)
print("Является ли число простым:", "Да" if is_prime else "Нет")

# Угадывание числа от 1 до 10
secret_number = random.randint(1, 10)
while True:
    guess = int(input("Угадайте число от 1 до 10: "))
    if guess == secret_number:
        print("Молодец! Вы угадали.")
        break
    elif guess < secret_number:
        print("Ваше число меньше загаданного.")
    else:
        print("Ваше число больше загаданного.")

# Перевод температуры Цельсия в Фаренгейт
print("Температура (°C) и её перевод в Фаренгейт (°F):")
for celsius in range(100, -1, -10):
    fahrenheit = celsius * 1.8 + 32
    print("{:.1f} °C = {:.1f} °F".format(celsius, fahrenheit))

# Запрос суммы покупки и внесенной суммы
while True:
    purchase_amount = float(input("Введите сумму покупки: "))
    if purchase_amount <= 0:
        print("Сумма покупки должна быть больше 0. Попробуйте снова.")
        continue
    break

while True:
    paid_amount = float(input("Введите внесенную сумму: "))
    if paid_amount < purchase_amount:
        print("Недостающая сумма:", purchase_amount - paid_amount)
        continue
    break

if paid_amount == purchase_amount:
    print("Спасибо!")
else:
    change = paid_amount - purchase_amount
    print("Возьмите сдачу:", change)

# Вывод значений функции y(x) = ax + b
N = int(input("Введите количество значений N: "))
a = float(input("Введите a: "))
b = float(input("Введите b: "))
x1 = float(input("Введите x1: "))
x2 = float(input("Введите x2: "))

step = (x2 - x1) / (N - 1) if x1 < x2 else (x1 - x2) / (N - 1)

x_values = [x1 + i * step for i in range(N)]
if x1 > x2:
    x_values.reverse()

for x in x_values:
    y = a * x + b
    print("y({:.2f}) = {} * {:.2f} + {} = {:.3f}".format(x, a, x, b, y))
