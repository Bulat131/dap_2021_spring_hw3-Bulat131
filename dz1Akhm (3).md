```python
import numpy as np

a = np.fromstring(input(), dtype=int, sep=' ')
n = len(a)

b = np.zeros(2 * n - 1)
b[:n] = np.flip(a)
b[n - 1:] = a

A = np.zeros((n, n), dtype=int)
for i in range(len(a)):
    A[i,:] = b[n-1-i : 2*n-1-i]
    
A[1::2, :] = A[1::2, ::-1]

print(A)
```


```python

```
