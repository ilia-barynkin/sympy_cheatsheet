# 📘 SymPy как черновик: шпаргалка

Минималистичный набор команд для символьных выкладок, проверки и фиксации контекста.

---

## 🔧 Инициализация

```python
from sympy import *
init_printing(use_unicode=True)  # Для красивого вывода в терминале
````

Объявление символов:

```python
x, y, z = symbols('x y z', real=True)
a, b, c = symbols('a b c')
```

---

## 🧮 Алгебра

| Задача                        | Команда           |
| ----------------------------- | ----------------- |
| Раскрыть скобки               | `expand(expr)`    |
| Свернуть в множители          | `factor(expr)`    |
| Упростить выражение           | `simplify(expr)`  |
| Привести к общему знаменателю | `together(expr)`  |
| Разделить дроби               | `apart(expr)`     |
| Подставить значения           | `expr.subs(x, 2)` |

---

## 🧷 Работа с уравнениями

```python
solve(x**2 - 4, x)             # => [-2, 2]
solve([x + y - 2, x - y], (x, y))  # => {x: 1, y: 1}
```

Система линейных уравнений:

```python
linsolve([Eq(a + b, 2), Eq(a - b, 0)], (a, b))
```

---

## 📐 Дифференцирование и интегрирование

```python
diff(sin(x)*x**2, x)           # производная
integrate(sin(x)*x, x)         # интеграл
```

---

## 🧠 Работа с выражениями

```python
expr = 1 + m / 2**23
expr.subs(m, 10)
```

Многострочные выражения:

```python
expr = (a + b)**3
expand(expr)
```

---

## 🧾 LaTeX / Markdown

```python
latex(expr)     # строка в LaTeX для вставки в md/pdf
```

Пример вставки:

```markdown
$$
\left(a + b\right)^3 = a^3 + 3a^2b + 3ab^2 + b^3
$$
```

---

## 🧰 Полезные конструкции

| Конструкция                 | Назначение            |
| --------------------------- | --------------------- |
| `Rational(1, 3)`            | Точная дробь 1/3      |
| `S('1/3')`                  | То же, но из строки   |
| `oo`, `-oo`                 | Бесконечности         |
| `Eq(x, y)`                  | Равенство `x == y`    |
| `Piecewise(...)`            | Частичная функция     |
| `Symbol('m', integer=True)` | Символ с ограничением |

---
## Функции 
В `sympy` определять функции можно двумя основными способами:

---

### ✅ **1. Символьная функция `Function` (абстрактная, без тела)**

Если ты хочешь просто задать обозначение **f(x)** без определения выражения:

```python
from sympy import symbols, Function

x = symbols('x')
f = Function('f')(x)

print(f.diff(x))  # f'(x)
```

Такую функцию можно использовать в уравнениях и дифференцировании, но у неё **нет тела** — просто имя.

---

### ✅ **2. Определённая функция (через `Eq`, `Lambda` или обычное выражение)**

Если ты хочешь задать **функцию с телом**, используй:

#### 🔹 Через выражение:

```python
from sympy import symbols, sin

x = symbols('x')
f = sin(x)**2 + x

print(f.diff(x))  # производная от sin(x)**2 + x
```

#### 🔹 Через `Lambda`:

```python
from sympy import symbols, Lambda

x = symbols('x')
f = Lambda(x, x**2 + 1)

print(f(x))         # x**2 + 1
print(f(x).diff(x)) # производная
```

---

### 🧠 Пример с подстановкой:

```python
from sympy import symbols, sin

x = symbols('x')
f = sin(x)

f_at_3 = f.subs(x, 3)
print(f_at_3.evalf())  # приближённое значение
```

---
