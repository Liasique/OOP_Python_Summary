# Основи ООП у Python 
---

## 1. Класи, поля, методи
```python
class Dog:
    def __init__(self, name):  # поле
        self.name = name

    def bark(self):  # метод
        print(f"{self.name} says Woof!")
```

---

## 2. Абстракція, Інкапсуляція, Наслідування, Поліморфізм
```python
# Абстракція — показуємо тільки важливе
class Animal:
    def make_sound(self):
        pass

# Наслідування
class Dog(Animal):
    def make_sound(self):
        print("Bark")

# Поліморфізм
def animal_sound(animal):
    animal.make_sound()

animal_sound(Dog())

# Інкапсуляція
class Person:
    def __init__(self):
        self.name = "Anna"       # public
        self._age = 25           # protected
        self.__ssn = "123-456"   # private
```

---

## 3. Рівні захисту
```python
obj = Person()
print(obj.name)     # ✅
print(obj._age)     # ⚠️ не рекомендується
# print(obj.__ssn)  # ❌ помилка
```

---

## 4. MRO — порядок пошуку методів
```python
class A: pass
class B(A): pass
class C(B): pass

print(C.mro())  # [C, B, A, object]
```

---

## 5. Типізація
```python
# Статична
def add(x: int, y: int) -> int:
    return x + y

# Качина: "Якщо щось поводиться як качка..."
class Duck:
    def quack(self):
        print("Quack!")

def make_it_quack(duck):
    duck.quack()
```

---

## 6. Класи-контейнери
```python
from collections import UserList, UserDict

class MyList(UserList):
    def append(self, item):
        print("Adding:", item)
        super().append(item)
```

---

## 7. dataclass
```python
from dataclasses import dataclass

@dataclass
class Product:
    name: str
    price: float

p = Product("Phone", 699.99)
print(p)
```

---

## 8. Enum
```python
from enum import Enum

class Status(Enum):
    ACTIVE = 1
    INACTIVE = 0

print(Status.ACTIVE)
```

---

## 9. Асоціація, агрегація, композиція
```python
# Асоціація
class Driver: ...
class Car:
    def drive(self, driver): pass

# Агрегація
class Engine: ...
class Car:
    def __init__(self, engine): self.engine = engine

# Композиція
class Battery: ...
class Phone:
    def __init__(self): self.battery = Battery()
```

---

## 10. Власні винятки
```python
class MyError(Exception): pass

def check(value):
    if value < 0:
        raise MyError("Negative not allowed")

try:
    check(-5)
except MyError as e:
    print("Error:", e)
```