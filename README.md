# goit-algo2-hw-02

**Design and Analysis of Algorithms. HW 2. Greedy algorithms and dynamic programming**

## Завдання 1. Оптимізація черги 3D-принтера в університетській лабораторії

Розробіть програму для оптимізації черги завдань 3D-друку з урахуванням пріоритетів та технічних обмежень принтера, використовуючи жадібний алгоритм.

**Опис завдання**

1. Використовуйте вхідні дані у вигляді списку завдань на друк, де кожне завдання містить: `ID`, `об'єм моделі`, `пріоритет` та `час друку`.

2. Реалізуйте основну функцію `optimize_printing`, яка буде:

- Враховувати пріоритети завдань.
- Групувати моделі для одночасного друку.
- Перевіряти обмеження об'єму та кількості.
- Розраховувати загальний час друку.
- Повертати оптимальний порядок друку.

3. Виведіть оптимальний порядок друку та загальний час виконання всіх завдань.

**Технічні умови**

1. Очікуваний формат виведення функції `optimize_printing`:

```
{
    "print_order": ["M1", "M2", "M3"],  # порядок друку завдань
    "total_time": 360  # загальний час у хвилинах
}
```

2. Формат вхідних даних для завдань:

```
print_jobs = [
    {
        "id": str,  # унікальний ідентифікатор
        "volume": float,  # об'єм в см³ (> 0)
        "priority": int,  # пріоритет (1, 2 або 3)
        "print_time": int  # час друку в хвилинах (> 0)
    }
]
```

3. Формат обмежень принтера:

```
printer_constraints = {
    "max_volume": float,  # максимальний об'єм для друку
    "max_items": int  # максимальна кількість моделей
}

4. Пріоритети завдань:

1 (найвищий) — Курсові/дипломні роботи
2 — Лабораторні роботи
3 (найнижчий) — Особисті проєкти

```

### Шаблон програми

```
from typing import List, Dict
from dataclasses import dataclass

@dataclass
class PrintJob:
    id: str
    volume: float
    priority: int
    print_time: int

@dataclass
class PrinterConstraints:
    max_volume: float
    max_items: int

def optimize_printing(print_jobs: List[Dict], constraints: Dict) -> Dict:
    """
    Оптимізує чергу 3D-друку згідно з пріоритетами та обмеженнями принтера

    Args:
        print_jobs: Список завдань на друк
        constraints: Обмеження принтера

    Returns:
        Dict з порядком друку та загальним часом
    """
    # Тут повинен бути ваш код

    return {
        "print_order": None,
        "total_time": None
    }
```

### Тестування

```
def test_printing_optimization():
    # Тест 1: Моделі однакового пріоритету
    test1_jobs = [
        {"id": "M1", "volume": 100, "priority": 1, "print_time": 120},
        {"id": "M2", "volume": 150, "priority": 1, "print_time": 90},
        {"id": "M3", "volume": 120, "priority": 1, "print_time": 150}
    ]

    # Тест 2: Моделі різних пріоритетів
    test2_jobs = [
        {"id": "M1", "volume": 100, "priority": 2, "print_time": 120},  # лабораторна
        {"id": "M2", "volume": 150, "priority": 1, "print_time": 90},  # дипломна
        {"id": "M3", "volume": 120, "priority": 3, "print_time": 150}  # особистий проєкт
    ]

    # Тест 3: Перевищення обмежень об'єму
    test3_jobs = [
        {"id": "M1", "volume": 250, "priority": 1, "print_time": 180},
        {"id": "M2", "volume": 200, "priority": 1, "print_time": 150},
        {"id": "M3", "volume": 180, "priority": 2, "print_time": 120}
    ]

    constraints = {
        "max_volume": 300,
        "max_items": 2
    }

    print("Тест 1 (однаковий пріоритет):")
    result1 = optimize_printing(test1_jobs, constraints)
    print(f"Порядок друку: {result1['print_order']}")
    print(f"Загальний час: {result1['total_time']} хвилин")

    print("\\nТест 2 (різні пріоритети):")
    result2 = optimize_printing(test2_jobs, constraints)
    print(f"Порядок друку: {result2['print_order']}")
    print(f"Загальний час: {result2['total_time']} хвилин")

    print("\\nТест 3 (перевищення обмежень):")
    result3 = optimize_printing(test3_jobs, constraints)
    print(f"Порядок друку: {result3['print_order']}")
    print(f"Загальний час: {result3['total_time']} хвилин")

if __name__ == "__main__":
    test_printing_optimization()

```

### Очікуваний результат:

```
Тест 1 (однаковий пріоритет):
Порядок друку: ['M1', 'M2', 'M3']
Загальний час: 270 хвилин

Тест 2 (різні пріоритети):
Порядок друку: ['M2', 'M1', 'M3']
Загальний час: 270 хвилин

Тест 3 (перевищення обмежень):
Порядок друку: ['M1', 'M2', 'M3']
Загальний час: 450 хвилин
```

## Завдання 2. Оптимальне розрізання стрижня для максимального прибутку (Rod Cutting Problem)

Розробіть програму для знаходження оптимального способу розрізання стрижня, щоб отримати максимальний прибуток. Необхідно реалізувати два підходи: через рекурсію з мемоізацією та через табуляцію.

**Опис завдання**

1. На вхід подається довжина стрижня та масив цін, де `price[i]` — це ціна стрижня довжини `i+1`.
2. Потрібно визначити, як розрізати стрижень, щоб отримати максимальний прибуток.
3. Реалізувати обидва підходи динамічного програмування.
4. Вивести оптимальний спосіб розрізання та максимальний прибуток.

**Технічні умови**

1. Формат вхідних даних:

```
length = 5 # довжина стрижня
prices = [2, 5, 7, 8, 10] # ціни для довжин 1, 2, 3, 4, 5
```

2. Обмеження:

- Довжина стрижня > 0.
- Всі ціни > 0.
- Масив цін не може бути порожнім.
- Довжина масиву цін повинна відповідати довжині стрижня.

### Очікуваний формат виведення

```
{
    "max_profit": 12, # максимальний прибуток
    "cuts": [2, 2, 1], # список довжин частин
    "number_of_cuts": 2 # кількість розрізів
}
```

### Шаблон програми:

```
from typing import List, Dict

def rod_cutting_memo(length: int, prices: List[int]) -> Dict:
    """
    Знаходить оптимальний спосіб розрізання через мемоізацію

    Args:
        length: довжина стрижня
        prices: список цін, де prices[i] — ціна стрижня довжини i+1

    Returns:
        Dict з максимальним прибутком та списком розрізів
    """

		# Тут повинен бути ваш код

    return {
        "max_profit": None,
        "cuts": None,
        "number_of_cuts": None
    }

def rod_cutting_table(length: int, prices: List[int]) -> Dict:
    """
    Знаходить оптимальний спосіб розрізання через табуляцію

    Args:
        length: довжина стрижня
        prices: список цін, де prices[i] — ціна стрижня довжини i+1

    Returns:
        Dict з максимальним прибутком та списком розрізів
    """

    # Тут повинен бути ваш код

    return {
        "max_profit": None,
        "cuts": None,
        "number_of_cuts": None
    }

def run_tests():
    """Функція для запуску всіх тестів"""
    test_cases = [
        # Тест 1: Базовий випадок
        {
            "length": 5,
            "prices": [2, 5, 7, 8, 10],
            "name": "Базовий випадок"
        },
        # Тест 2: Оптимально не різати
        {
            "length": 3,
            "prices": [1, 3, 8],
            "name": "Оптимально не різати"
        },
        # Тест 3: Всі розрізи по 1
        {
            "length": 4,
            "prices": [3, 5, 6, 7],
            "name": "Рівномірні розрізи"
        }
    ]

    for test in test_cases:
        print(f"\\nТест: {test['name']}")
        print(f"Довжина стрижня: {test['length']}")
        print(f"Ціни: {test['prices']}")

        # Тестуємо мемоізацію
        memo_result = rod_cutting_memo(test['length'], test['prices'])
        print("\\nРезультат мемоізації:")
        print(f"Максимальний прибуток: {memo_result['max_profit']}")
        print(f"Розрізи: {memo_result['cuts']}")
        print(f"Кількість розрізів: {memo_result['number_of_cuts']}")

        # Тестуємо табуляцію
        table_result = rod_cutting_table(test['length'], test['prices'])
        print("\\nРезультат табуляції:")
        print(f"Максимальний прибуток: {table_result['max_profit']}")
        print(f"Розрізи: {table_result['cuts']}")
        print(f"Кількість розрізів: {table_result['number_of_cuts']}")

        print("\\nПеревірка пройшла успішно!")

if __name__ == "__main__":
    run_tests()
```

### Очікуваний результат:

```
Тест: Базовий випадок
Довжина стрижня: 5
Ціни: [2, 5, 7, 8, 10]

Результат мемоізації:
Максимальний прибуток: 12
Розрізи: [1, 2, 2]
Кількість розрізів: 2

Результат табуляції:
Максимальний прибуток: 12
Розрізи: [2, 2, 1]
Кількість розрізів: 2

Перевірка пройшла успішно!

Тест: Оптимально не різати
Довжина стрижня: 3
Ціни: [1, 3, 8]

Результат мемоізації:
Максимальний прибуток: 8
Розрізи: [3]
Кількість розрізів: 0

Результат табуляції:
Максимальний прибуток: 8
Розрізи: [3]
Кількість розрізів: 0

Перевірка пройшла успішно!

Тест: Рівномірні розрізи
Довжина стрижня: 4
Ціни: [3, 5, 6, 7]

Результат мемоізації:
Максимальний прибуток: 12
Розрізи: [1, 1, 1, 1]
Кількість розрізів: 3

Результат табуляції:
Максимальний прибуток: 12
Розрізи: [1, 1, 1, 1]
Кількість розрізів: 3

Перевірка пройшла успішно!
```
