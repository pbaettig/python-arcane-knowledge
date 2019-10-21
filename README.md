# python-arcane-knowledge
## Compare n variables
When you need to compare one set of variables with another one, for example when checking if two objects are identical in content.
```python
a = 1
b = 2
c = 3
A = 1
B = 2
C = 33

a == A and b == B and c == C
# -> False

(a,b,c) == (A,B,C)
# -> False
```

## DataClass (instead of namedtuple)
Python 3.7 has [DataClasses](https://docs.python.org/3/library/dataclasses.html) that work similar to `namedtuple` but are more flexible.

```python
from collections import namedtuple
Person = namedtuple('Person', ('first_name', 'last_name', 'drink_preference'))

p = Person('Max', 'Muster', 'beer')
```
Dataclasses behave more like proper classes, they allow methods for example.
```python
from dataclasses import dataclass

@dataclass
class Person:
  first_name: str
  last_name: str
  drink_preference: str

  def introduction(self) -> str:
    return f'Hello, my name is {self.first_name} {self.last_name} and I like to drink {self.drink_preference}'

p = Person('Max', 'Muster', 'beer')

print(p.introduction())
# -> Hello, my name is Max Muster and I like to drink beer
```
By default dataclasses objects are mutable.
```python
p = Person('Max', 'Muster', 'beer')

print(p.introduction())
# -> Hello, my name is Max Muster and I like to drink beer

p.first_name = 'Bob'
print(p.introduction())
# -> Hello, my name is Bob Muster and I like to drink beer
```
It is possible to make them immutable by adding `frozen=True` to the `dataclass decorator`
```python
@dataclass(frozen=True)
class Person:
  ...

p = Person('Max', 'Muster', 'beer')
# -> Hello, my name is Max Muster and I like to drink beer
p.first_name = 'Bob'
# -> Traceback (most recent call last):
# ->   File "<input>", line 1, in <module>
# ->     p.first_name = 'Parschgal'
# ->   File "<string>", line 3, in __setattr__
# -> dataclasses.FrozenInstanceError: cannot assign to field 'first_name'
```
