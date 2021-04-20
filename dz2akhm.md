```python
import numpy as np

X = np.stack([
    np.fromstring(row, dtype=int, sep=' ') 
    for row in input().split(';')
])

Y = np.stack([
    np.fromstring(row, dtype=int, sep=' ') 
    for row in input().split(';')
])

def solution(X, Y):
    n, m = X.shape
    
    for i in range(n):
        for j in range(m):
            for k in range(1, min(n - i, m - j) + 1):
                M = X[i:i+k, j:j+k]
                det = np.linalg.det(M)
                if np.isclose(det, Y[i, j]):
                    return True
    
    return False

print(solution(X, Y))

```
