# 🎨 Padrões de Algoritmos - Guia Completo

## 🎯 O Que São Padrões Algorítmicos?

Padrões são **técnicas reutilizáveis** que se aplicam a múltiplos problemas. Reconhecer padrões é a chave para resolver problemas eficientemente em entrevistas.

---

## 1. 📊 Arrays & Hashing

### Quando Usar
- Precisa buscar/verificar existência em O(1)
- Contar frequência de elementos
- Agrupar elementos similares
- Encontrar pares/triplas com soma específica

### Técnicas Principais

#### Hash Map para Lookup
```
Problema: Encontrar complemento
Técnica: Armazenar elementos vistos em hash map
```

#### Frequency Counter
```
Problema: Contar ocorrências
Técnica: map[elemento] = contador
```

#### Grouping
```
Problema: Agrupar anagramas
Técnica: Usar chave canônica (sorted string)
```

### Complexidade Típica
- **Tempo**: O(n)
- **Espaço**: O(n)

### Problemas Exemplo
- Two Sum
- Group Anagrams
- Top K Frequent Elements

---

## 2. ↔️ Two Pointers

### Quando Usar
- Array/string está **ordenado**
- Precisa encontrar **pares** com propriedade
- Remover elementos **in-place**
- Comparar elementos de **duas pontas**

### Variações

#### Opposite Direction (←  →)
```python
left = 0
right = len(arr) - 1
while left < right:
    # Processar
    if condição:
        left += 1
    else:
        right -= 1
```

**Uso**: Two Sum II, Container With Most Water

#### Same Direction (→ →)
```python
slow = 0
for fast in range(len(arr)):
    if condição:
        arr[slow] = arr[fast]
        slow += 1
```

**Uso**: Remove Duplicates, Move Zeroes

#### Fast & Slow (🐇 🐢)
```python
slow = head
fast = head
while fast and fast.next:
    slow = slow.next
    fast = fast.next.next
```

**Uso**: Cycle detection, Find middle

### Complexidade Típica
- **Tempo**: O(n)
- **Espaço**: O(1)

---

## 3. 🪟 Sliding Window

### Quando Usar
- Problema envolve **subarray/substring contíguo**
- Palavras-chave: "maximum/minimum sum/length"
- Precisa otimizar de O(n²) para O(n)

### Variações

#### Fixed Size Window
```python
window_size = k
window_sum = sum(arr[:k])
max_sum = window_sum

for i in range(k, len(arr)):
    window_sum += arr[i] - arr[i-k]
    max_sum = max(max_sum, window_sum)
```

**Uso**: Maximum Average Subarray

#### Variable Size Window
```python
left = 0
for right in range(len(arr)):
    # Adicionar arr[right] à janela
    
    while condição_violada:
        # Remover arr[left] da janela
        left += 1
    
    # Atualizar resultado
```

**Uso**: Longest Substring Without Repeating Characters

### Complexidade Típica
- **Tempo**: O(n)
- **Espaço**: O(1) ou O(k) para hash map

---

## 4. 📚 Stack

### Quando Usar
- Precisa de **LIFO** (Last In First Out)
- Problema envolve **parênteses/brackets**
- Precisa do **próximo maior/menor** elemento
- Avaliar **expressões**

### Padrões

#### Valid Parentheses
```python
stack = []
for char in s:
    if char in '({[':
        stack.append(char)
    else:
        if not stack or not matches(stack.pop(), char):
            return False
return len(stack) == 0
```

#### Monotonic Stack
```python
stack = []  # indices
result = [-1] * len(arr)

for i in range(len(arr)):
    while stack and arr[stack[-1]] < arr[i]:
        result[stack.pop()] = arr[i]
    stack.append(i)
```

**Uso**: Next Greater Element, Daily Temperatures

### Complexidade Típica
- **Tempo**: O(n)
- **Espaço**: O(n)

---

## 5. 🔍 Binary Search

### Quando Usar
- Array está **ordenado**
- Precisa buscar em **O(log n)**
- Problema de **"find first/last"**
- Search space é **monotônico**

### Template Padrão
```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1
```

### Variações

#### Find First Occurrence
```python
while left < right:
    mid = left + (right - left) // 2
    if arr[mid] < target:
        left = mid + 1
    else:
        right = mid
```

#### Find Last Occurrence
```python
while left < right:
    mid = left + (right - left) // 2 + 1
    if arr[mid] > target:
        right = mid - 1
    else:
        left = mid
```

### Complexidade Típica
- **Tempo**: O(log n)
- **Espaço**: O(1)

---

## 6. 🔗 Linked List

### Quando Usar
- Problema envolve **nós sequenciais**
- Precisa de **inserção/remoção O(1)**
- **Não precisa** de acesso aleatório

### Padrões

#### Reversal
```python
def reverse(head):
    prev = None
    curr = head
    while curr:
        next_temp = curr.next
        curr.next = prev
        prev = curr
        curr = next_temp
    return prev
```

#### Fast & Slow Pointers
```python
def find_middle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow
```

#### Dummy Node
```python
dummy = ListNode(0)
dummy.next = head
# Facilita edge cases
```

### Complexidade Típica
- **Tempo**: O(n)
- **Espaço**: O(1) iterativo, O(n) recursivo

---

## 7. 🌳 Trees

### Quando Usar
- Estrutura **hierárquica**
- Precisa de **travessia**
- Problema envolve **paths** ou **levels**

### Padrões

#### DFS - Preorder
```python
def preorder(root):
    if not root:
        return
    process(root)        # Root
    preorder(root.left)  # Left
    preorder(root.right) # Right
```

#### DFS - Inorder (BST)
```python
def inorder(root):
    if not root:
        return
    inorder(root.left)   # Left
    process(root)        # Root (sorted!)
    inorder(root.right)  # Right
```

#### DFS - Postorder
```python
def postorder(root):
    if not root:
        return
    postorder(root.left)  # Left
    postorder(root.right) # Right
    process(root)         # Root
```

#### BFS - Level Order
```python
from collections import deque

def level_order(root):
    if not root:
        return []
    
    queue = deque([root])
    result = []
    
    while queue:
        level_size = len(queue)
        level = []
        
        for _ in range(level_size):
            node = queue.popleft()
            level.append(node.val)
            
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        
        result.append(level)
    
    return result
```

### Complexidade Típica
- **Tempo**: O(n)
- **Espaço**: O(h) para DFS, O(w) para BFS

---

## 8. 🔤 Tries (Prefix Trees)

### Quando Usar
- Problema envolve **prefixos** de strings
- Precisa de **autocomplete**
- **Word search** em grid

### Template
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True
    
    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end
```

### Complexidade Típica
- **Tempo**: O(m) onde m = comprimento da palavra
- **Espaço**: O(n*m) onde n = número de palavras

---

## 9. 🏔️ Heap / Priority Queue

### Quando Usar
- Precisa do **K maior/menor**
- **Merge K sorted** lists/arrays
- **Median** dinâmico
- **Task scheduling**

### Padrões

#### Top K Elements
```python
import heapq

def top_k(nums, k):
    # Min heap de tamanho k
    heap = []
    for num in nums:
        heapq.heappush(heap, num)
        if len(heap) > k:
            heapq.heappop(heap)
    return heap
```

#### K-way Merge
```python
def merge_k_sorted(lists):
    heap = []
    # Adicionar primeiro elemento de cada lista
    for i, lst in enumerate(lists):
        if lst:
            heapq.heappush(heap, (lst[0], i, 0))
    
    result = []
    while heap:
        val, list_idx, elem_idx = heapq.heappop(heap)
        result.append(val)
        
        # Adicionar próximo elemento da mesma lista
        if elem_idx + 1 < len(lists[list_idx]):
            next_val = lists[list_idx][elem_idx + 1]
            heapq.heappush(heap, (next_val, list_idx, elem_idx + 1))
    
    return result
```

### Complexidade Típica
- **Tempo**: O(n log k)
- **Espaço**: O(k)

---

## 10. 🔄 Backtracking

### Quando Usar
- Precisa **explorar todas possibilidades**
- Palavras-chave: "all possible", "generate"
- **Combinações, Permutações, Subsets**

### Template Geral
```python
def backtrack(path, options):
    # Base case
    if is_solution(path):
        result.append(path[:])
        return
    
    # Recursive case
    for option in options:
        # Choose
        path.append(option)
        
        # Explore
        backtrack(path, next_options)
        
        # Unchoose (backtrack)
        path.pop()
```

### Padrões Específicos

#### Subsets
```python
def subsets(nums):
    result = []
    
    def backtrack(start, path):
        result.append(path[:])
        for i in range(start, len(nums)):
            path.append(nums[i])
            backtrack(i + 1, path)
            path.pop()
    
    backtrack(0, [])
    return result
```

#### Permutations
```python
def permutations(nums):
    result = []
    
    def backtrack(path):
        if len(path) == len(nums):
            result.append(path[:])
            return
        
        for num in nums:
            if num not in path:
                path.append(num)
                backtrack(path)
                path.pop()
    
    backtrack([])
    return result
```

### Complexidade Típica
- **Tempo**: O(2ⁿ) para subsets, O(n!) para permutations
- **Espaço**: O(n) para stack de recursão

---

## 11. 🕸️ Graphs

### Quando Usar
- Problema envolve **nós e conexões**
- Precisa encontrar **caminhos**
- **Connected components**
- **Cycle detection**

### Representações

#### Adjacency List
```python
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D'],
    'C': ['A', 'D'],
    'D': ['B', 'C']
}
```

#### Adjacency Matrix
```python
graph = [
    [0, 1, 1, 0],
    [1, 0, 0, 1],
    [1, 0, 0, 1],
    [0, 1, 1, 0]
]
```

### Padrões

#### DFS (Recursivo)
```python
def dfs(node, visited):
    if node in visited:
        return
    
    visited.add(node)
    
    for neighbor in graph[node]:
        dfs(neighbor, visited)
```

#### BFS (Iterativo)
```python
from collections import deque

def bfs(start):
    visited = set([start])
    queue = deque([start])
    
    while queue:
        node = queue.popleft()
        
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

#### Union Find
```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n
    
    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]
    
    def union(self, x, y):
        px, py = self.find(x), self.find(y)
        if px == py:
            return False
        if self.rank[px] < self.rank[py]:
            px, py = py, px
        self.parent[py] = px
        if self.rank[px] == self.rank[py]:
            self.rank[px] += 1
        return True
```

### Complexidade Típica
- **Tempo**: O(V + E)
- **Espaço**: O(V)

---

## 12. 🎯 Dynamic Programming

### Quando Usar
- Problema tem **optimal substructure**
- Problema tem **overlapping subproblems**
- Palavras-chave: "maximum/minimum", "count ways"

### Abordagens

#### Top-Down (Memoization)
```python
def fib(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    
    memo[n] = fib(n-1, memo) + fib(n-2, memo)
    return memo[n]
```

#### Bottom-Up (Tabulation)
```python
def fib(n):
    if n <= 1:
        return n
    
    dp = [0] * (n + 1)
    dp[1] = 1
    
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    
    return dp[n]
```

### Padrões Comuns

#### 1D DP
- House Robber
- Climbing Stairs
- Decode Ways

#### 2D DP
- Longest Common Subsequence
- Edit Distance
- Unique Paths

### Complexidade Típica
- **Tempo**: O(n) para 1D, O(n*m) para 2D
- **Espaço**: O(n) ou O(n*m), otimizável

---

## 🎓 Como Reconhecer Padrões

### Perguntas a Fazer

1. **Estrutura de dados?**
   - Array → Two Pointers, Sliding Window
   - Tree → DFS, BFS
   - Graph → DFS, BFS, Union Find

2. **Está ordenado?**
   - Sim → Binary Search, Two Pointers
   - Não → Hash Map, Sorting

3. **Precisa de todas as soluções?**
   - Sim → Backtracking
   - Não → Greedy, DP

4. **Tem optimal substructure?**
   - Sim → DP
   - Não → Outros padrões

5. **Precisa do K maior/menor?**
   - Sim → Heap

### Fluxograma de Decisão

```
Array/String?
├─ Buscar elemento
│  ├─ Ordenado? → Binary Search
│  └─ Não ordenado → Hash Map
├─ Subarray contíguo? → Sliding Window
├─ Pares com propriedade? → Two Pointers
└─ Parentheses? → Stack

Tree?
├─ Por nível? → BFS
├─ Path/recursivo? → DFS
└─ Prefix? → Trie

Graph?
├─ Shortest path? → BFS
├─ Connected? → DFS/Union Find
└─ All paths? → Backtracking

Otimização?
├─ Overlapping subproblems? → DP
├─ Choice doesn't affect future? → Greedy
└─ Try all? → Backtracking
```

---

## 📚 Resumo dos Padrões

| Padrão | Tempo | Espaço | Sinais |
|--------|-------|---------|--------|
| Hash Map | O(n) | O(n) | Lookup, frequency |
| Two Pointers | O(n) | O(1) | Sorted, pairs |
| Sliding Window | O(n) | O(1) | Contiguous, substring |
| Stack | O(n) | O(n) | LIFO, parentheses |
| Binary Search | O(log n) | O(1) | Sorted, search |
| Linked List | O(n) | O(1) | Sequential access |
| Tree DFS | O(n) | O(h) | Recursive, paths |
| Tree BFS | O(n) | O(w) | Level-order |
| Trie | O(m) | O(n*m) | Prefix, autocomplete |
| Heap | O(n log k) | O(k) | Top K, median |
| Backtracking | O(2ⁿ) | O(n) | All solutions |
| Graph DFS/BFS | O(V+E) | O(V) | Connected, cycles |
| DP | O(n²) | O(n²) | Optimal, overlapping |

---

**Domine os padrões, não memorize problemas! 🎯**
