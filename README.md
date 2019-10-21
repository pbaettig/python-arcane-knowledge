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
