# 💻 Templates de Código Python

## 🎯 Por Que Usar Templates?

Templates são **esqueletos de código reutilizáveis** que:
- Economizam tempo em entrevistas
- Reduzem erros comuns
- Servem como ponto de partida
- Facilitam customização para problemas específicos

---

## 1. 📊 Arrays & Hashing

### Hash Map - Two Sum Pattern
```python
def two_sum_pattern(arr, target):
    """
    Template para encontrar pares com soma específica
    Tempo: O(n), Espaço: O(n)
    """
    seen = {}  # {valor: índice}
    
    for i, num in enumerate(arr):
        complement = target - num
        
        if complement in seen:
            return [seen[complement], i]
        
        seen[num] = i
    
    return []

# Variação: Contar pares
def count_pairs(arr, target):
    seen = {}
    count = 0
    
    for num in arr:
        complement = target - num
        if complement in seen:
            count += seen[complement]
        seen[num] = seen.get(num, 0) + 1
    
    return count
```

### Frequency Counter
```python
from collections import Counter

def frequency_pattern(arr):
    """
    Template para problemas de frequência
    Tempo: O(n), Espaço: O(n)
    """
    freq = Counter(arr)
    
    # Ou manualmente:
    freq = {}
    for item in arr:
        freq[item] = freq.get(item, 0) + 1
    
    return freq

# Top K Frequent Elements
def top_k_frequent(nums, k):
    freq = Counter(nums)
    # Retorna k elementos mais frequentes
    return [num for num, _ in freq.most_common(k)]
```

### Prefix Sum
```python
def prefix_sum_pattern(arr):
    """
    Template para soma de prefixos
    Tempo: O(n), Espaço: O(n)
    """
    n = len(arr)
    prefix = [0] * (n + 1)
    
    for i in range(n):
        prefix[i + 1] = prefix[i] + arr[i]
    
    # Range sum de [left, right]
    def range_sum(left, right):
        return prefix[right + 1] - prefix[left]
    
    return prefix, range_sum
```

---

## 2. ↔️ Two Pointers

### Opposite Direction
```python
def two_pointers_opposite(arr):
    """
    Template para dois ponteiros em direções opostas
    Tempo: O(n), Espaço: O(1)
    """
    left = 0
    right = len(arr) - 1
    
    while left < right:
        # Processar arr[left] e arr[right]
        
        if condition_met:
            # Fazer algo
            left += 1
            right -= 1
        elif need_larger:
            left += 1
        else:
            right -= 1
    
    return result

# Exemplo: Two Sum II (sorted array)
def two_sum_sorted(numbers, target):
    left, right = 0, len(numbers) - 1
    
    while left < right:
        current_sum = numbers[left] + numbers[right]
        
        if current_sum == target:
            return [left + 1, right + 1]  # 1-indexed
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    
    return []
```

### Same Direction (Fast & Slow)
```python
def two_pointers_same_direction(arr):
    """
    Template para remover elementos in-place
    Tempo: O(n), Espaço: O(1)
    """
    slow = 0
    
    for fast in range(len(arr)):
        if should_keep(arr[fast]):
            arr[slow] = arr[fast]
            slow += 1
    
    return slow  # novo comprimento

# Exemplo: Remove Duplicates
def remove_duplicates(nums):
    if not nums:
        return 0
    
    slow = 1
    for fast in range(1, len(nums)):
        if nums[fast] != nums[fast - 1]:
            nums[slow] = nums[fast]
            slow += 1
    
    return slow
```

### Fast & Slow (Cycle Detection)
```python
def has_cycle(head):
    """
    Template para detecção de ciclo em linked list
    Tempo: O(n), Espaço: O(1)
    """
    if not head or not head.next:
        return False
    
    slow = head
    fast = head
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        
        if slow == fast:
            return True
    
    return False

# Encontrar início do ciclo
def detect_cycle(head):
    slow = fast = head
    
    # Detectar ciclo
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            break
    else:
        return None
    
    # Encontrar início
    slow = head
    while slow != fast:
        slow = slow.next
        fast = fast.next
    
    return slow
```

---

## 3. 🪟 Sliding Window

### Fixed Size Window
```python
def fixed_window(arr, k):
    """
    Template para janela de tamanho fixo
    Tempo: O(n), Espaço: O(1)
    """
    if len(arr) < k:
        return None
    
    # Calcular soma da primeira janela
    window_sum = sum(arr[:k])
    max_sum = window_sum
    
    # Deslizar janela
    for i in range(k, len(arr)):
        window_sum += arr[i] - arr[i - k]
        max_sum = max(max_sum, window_sum)
    
    return max_sum
```

### Variable Size Window
```python
def variable_window(s):
    """
    Template para janela de tamanho variável
    Tempo: O(n), Espaço: O(k)
    """
    char_set = set()
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        # Expandir janela
        while s[right] in char_set:
            # Contrair janela
            char_set.remove(s[left])
            left += 1
        
        # Adicionar novo elemento
        char_set.add(s[right])
        
        # Atualizar resultado
        max_length = max(max_length, right - left + 1)
    
    return max_length

# Com Hash Map (para contagem)
def variable_window_with_count(s, k):
    """
    Longest substring com no máximo k caracteres distintos
    """
    char_count = {}
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        # Adicionar char à direita
        char = s[right]
        char_count[char] = char_count.get(char, 0) + 1
        
        # Contrair se necessário
        while len(char_count) > k:
            left_char = s[left]
            char_count[left_char] -= 1
            if char_count[left_char] == 0:
                del char_count[left_char]
            left += 1
        
        # Atualizar máximo
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

---

## 4. 📚 Stack

### Basic Stack
```python
def stack_pattern():
    """
    Template básico de stack
    Tempo: O(n), Espaço: O(n)
    """
    stack = []
    
    # Push
    stack.append(item)
    
    # Pop
    if stack:
        top = stack.pop()
    
    # Peek
    if stack:
        top = stack[-1]
    
    # Empty
    is_empty = len(stack) == 0
```

### Valid Parentheses
```python
def is_valid(s):
    """
    Template para validar parênteses
    """
    stack = []
    mapping = {')': '(', '}': '{', ']': '['}
    
    for char in s:
        if char in mapping:
            # Closing bracket
            top = stack.pop() if stack else '#'
            if mapping[char] != top:
                return False
        else:
            # Opening bracket
            stack.append(char)
    
    return len(stack) == 0
```

### Monotonic Stack
```python
def monotonic_stack_increasing(arr):
    """
    Template para stack monótona crescente
    Útil para "next greater element"
    """
    stack = []  # armazena índices
    result = [-1] * len(arr)
    
    for i in range(len(arr)):
        # Manter stack crescente
        while stack and arr[stack[-1]] < arr[i]:
            idx = stack.pop()
            result[idx] = arr[i]
        
        stack.append(i)
    
    return result

def monotonic_stack_decreasing(arr):
    """
    Template para stack monótona decrescente
    Útil para "next smaller element"
    """
    stack = []
    result = [-1] * len(arr)
    
    for i in range(len(arr)):
        # Manter stack decrescente
        while stack and arr[stack[-1]] > arr[i]:
            idx = stack.pop()
            result[idx] = arr[i]
        
        stack.append(i)
    
    return result
```

---

## 5. 🔍 Binary Search

### Classic Binary Search
```python
def binary_search(arr, target):
    """
    Template clássico de binary search
    Tempo: O(log n), Espaço: O(1)
    """
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

### Find First Occurrence
```python
def find_first(arr, target):
    """
    Encontrar primeira ocorrência
    """
    left, right = 0, len(arr) - 1
    result = -1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if arr[mid] == target:
            result = mid
            right = mid - 1  # Continue buscando à esquerda
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return result
```

### Find Last Occurrence
```python
def find_last(arr, target):
    """
    Encontrar última ocorrência
    """
    left, right = 0, len(arr) - 1
    result = -1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if arr[mid] == target:
            result = mid
            left = mid + 1  # Continue buscando à direita
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return result
```

### Binary Search on Answer
```python
def binary_search_on_answer(arr, check_func):
    """
    Template para binary search na resposta
    Usado quando: "Minimize/Maximize X such that condition"
    """
    left, right = min_possible, max_possible
    result = -1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if check_func(mid):
            result = mid
            # Tentar melhorar (depende do problema)
            right = mid - 1  # ou left = mid + 1
        else:
            left = mid + 1  # ou right = mid - 1
    
    return result
```

---

## 6. 🔗 Linked List

### Reversal
```python
def reverse_list(head):
    """
    Template para reverter linked list
    Tempo: O(n), Espaço: O(1)
    """
    prev = None
    curr = head
    
    while curr:
        next_temp = curr.next
        curr.next = prev
        prev = curr
        curr = next_temp
    
    return prev

# Recursivo
def reverse_list_recursive(head):
    if not head or not head.next:
        return head
    
    new_head = reverse_list_recursive(head.next)
    head.next.next = head
    head.next = None
    
    return new_head
```

### Merge Two Lists
```python
def merge_two_lists(l1, l2):
    """
    Template para merge de duas listas ordenadas
    """
    dummy = ListNode(0)
    tail = dummy
    
    while l1 and l2:
        if l1.val < l2.val:
            tail.next = l1
            l1 = l1.next
        else:
            tail.next = l2
            l2 = l2.next
        tail = tail.next
    
    # Adicionar resto
    tail.next = l1 if l1 else l2
    
    return dummy.next
```

### Find Middle
```python
def find_middle(head):
    """
    Template para encontrar meio da lista
    """
    slow = fast = head
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    
    return slow
```

---

## 7. 🌳 Trees

### DFS Templates
```python
# Preorder
def preorder(root):
    if not root:
        return
    result.append(root.val)      # Process
    preorder(root.left)           # Left
    preorder(root.right)          # Right

# Inorder (sorted for BST)
def inorder(root):
    if not root:
        return
    inorder(root.left)            # Left
    result.append(root.val)       # Process
    inorder(root.right)           # Right

# Postorder
def postorder(root):
    if not root:
        return
    postorder(root.left)          # Left
    postorder(root.right)         # Right
    result.append(root.val)       # Process
```

### BFS Template
```python
from collections import deque

def level_order(root):
    """
    Template para BFS (level order traversal)
    """
    if not root:
        return []
    
    result = []
    queue = deque([root])
    
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

### Tree Path Template
```python
def has_path_sum(root, target_sum):
    """
    Template para problemas de path
    """
    if not root:
        return False
    
    # Leaf node
    if not root.left and not root.right:
        return target_sum == root.val
    
    # Recursive case
    remaining = target_sum - root.val
    return (has_path_sum(root.left, remaining) or 
            has_path_sum(root.right, remaining))

# All paths
def all_paths(root, target_sum):
    result = []
    
    def dfs(node, current_sum, path):
        if not node:
            return
        
        path.append(node.val)
        current_sum += node.val
        
        # Leaf node
        if not node.left and not node.right:
            if current_sum == target_sum:
                result.append(path[:])
        
        # Recursive
        dfs(node.left, current_sum, path)
        dfs(node.right, current_sum, path)
        
        # Backtrack
        path.pop()
    
    dfs(root, 0, [])
    return result
```

---

## 8. 🔄 Backtracking

### General Template
```python
def backtrack_template(options):
    """
    Template geral para backtracking
    """
    result = []
    
    def backtrack(path, remaining_options):
        # Base case
        if is_solution(path):
            result.append(path[:])  # Importante: copiar!
            return
        
        # Recursive case
        for option in remaining_options:
            # Prune (optional)
            if not is_valid(option):
                continue
            
            # Choose
            path.append(option)
            
            # Explore
            backtrack(path, get_next_options(option))
            
            # Unchoose
            path.pop()
    
    backtrack([], options)
    return result
```

### Subsets
```python
def subsets(nums):
    """
    Template para gerar todos os subsets
    """
    result = []
    
    def backtrack(start, path):
        # Cada path é uma solução válida
        result.append(path[:])
        
        for i in range(start, len(nums)):
            path.append(nums[i])
            backtrack(i + 1, path)
            path.pop()
    
    backtrack(0, [])
    return result
```

### Permutations
```python
def permutations(nums):
    """
    Template para gerar todas as permutações
    """
    result = []
    
    def backtrack(path):
        if len(path) == len(nums):
            result.append(path[:])
            return
        
        for num in nums:
            if num in path:
                continue
            
            path.append(num)
            backtrack(path)
            path.pop()
    
    backtrack([])
    return result

# Mais eficiente com visited set
def permutations_optimized(nums):
    result = []
    visited = set()
    
    def backtrack(path):
        if len(path) == len(nums):
            result.append(path[:])
            return
        
        for i, num in enumerate(nums):
            if i in visited:
                continue
            
            visited.add(i)
            path.append(num)
            backtrack(path)
            path.pop()
            visited.remove(i)
    
    backtrack([])
    return result
```

### Combinations
```python
def combinations(n, k):
    """
    Template para combinações
    """
    result = []
    
    def backtrack(start, path):
        if len(path) == k:
            result.append(path[:])
            return
        
        for i in range(start, n + 1):
            path.append(i)
            backtrack(i + 1, path)
            path.pop()
    
    backtrack(1, [])
    return result
```

---

## 9. 🕸️ Graphs

### DFS Template
```python
def dfs_recursive(graph, node, visited):
    """
    Template DFS recursivo
    """
    if node in visited:
        return
    
    visited.add(node)
    # Process node
    
    for neighbor in graph[node]:
        dfs_recursive(graph, neighbor, visited)

def dfs_iterative(graph, start):
    """
    Template DFS iterativo
    """
    visited = set()
    stack = [start]
    
    while stack:
        node = stack.pop()
        
        if node in visited:
            continue
        
        visited.add(node)
        # Process node
        
        for neighbor in graph[node]:
            if neighbor not in visited:
                stack.append(neighbor)
    
    return visited
```

### BFS Template
```python
from collections import deque

def bfs(graph, start):
    """
    Template BFS
    """
    visited = set([start])
    queue = deque([start])
    
    while queue:
        node = queue.popleft()
        # Process node
        
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
    
    return visited
```

### Union Find Template
```python
class UnionFind:
    """
    Template para Union Find (Disjoint Set)
    """
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n
        self.count = n  # número de componentes
    
    def find(self, x):
        """Find com path compression"""
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]
    
    def union(self, x, y):
        """Union por rank"""
        px, py = self.find(x), self.find(y)
        
        if px == py:
            return False
        
        if self.rank[px] < self.rank[py]:
            px, py = py, px
        
        self.parent[py] = px
        if self.rank[px] == self.rank[py]:
            self.rank[px] += 1
        
        self.count -= 1
        return True
    
    def connected(self, x, y):
        """Verifica se x e y estão conectados"""
        return self.find(x) == self.find(y)
```

---

## 10. 🎯 Dynamic Programming

### 1D DP Template
```python
def dp_1d(n):
    """
    Template para DP 1D
    """
    # Definir array DP
    dp = [0] * (n + 1)
    
    # Base case
    dp[0] = base_value
    dp[1] = base_value
    
    # Fill array
    for i in range(2, n + 1):
        dp[i] = function(dp[i-1], dp[i-2], ...)
    
    return dp[n]

# Space optimized
def dp_1d_optimized(n):
    """
    Otimização de espaço quando só precisa dos últimos k valores
    """
    prev2 = base_value
    prev1 = base_value
    
    for i in range(2, n + 1):
        curr = function(prev1, prev2)
        prev2 = prev1
        prev1 = curr
    
    return prev1
```

### 2D DP Template
```python
def dp_2d(m, n):
    """
    Template para DP 2D
    """
    # Criar tabela
    dp = [[0] * n for _ in range(m)]
    
    # Base cases
    for i in range(m):
        dp[i][0] = base_value
    for j in range(n):
        dp[0][j] = base_value
    
    # Fill table
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = function(dp[i-1][j], dp[i][j-1], ...)
    
    return dp[m-1][n-1]
```

### Memoization Template
```python
def memoization_template(n):
    """
    Template para top-down DP com memoization
    """
    memo = {}
    
    def dp(state):
        # Base case
        if base_condition(state):
            return base_value
        
        # Check memo
        if state in memo:
            return memo[state]
        
        # Compute
        result = function(dp(next_state1), dp(next_state2), ...)
        
        # Store in memo
        memo[state] = result
        return result
    
    return dp(n)

# Com decorator
from functools import lru_cache

@lru_cache(maxsize=None)
def dp_with_cache(n):
    if n <= 1:
        return n
    return dp_with_cache(n-1) + dp_with_cache(n-2)
```

---

## 📝 Como Usar os Templates

### Passos para Aplicar

1. **Identificar o padrão** do problema
2. **Escolher o template** apropriado
3. **Customizar** para o problema específico:
   - Ajustar condições
   - Modificar processamento
   - Adaptar estruturas de dados
4. **Testar** com exemplos

### Exemplo de Customização

```python
# Template genérico de sliding window
def sliding_window_template(arr):
    left = 0
    for right in range(len(arr)):
        # [CUSTOMIZAR] Adicionar arr[right]
        
        while condition_violated:
            # [CUSTOMIZAR] Remover arr[left]
            left += 1
        
        # [CUSTOMIZAR] Atualizar resultado

# Aplicação específica: Longest substring sem repetição
def length_of_longest_substring(s):
    char_set = set()  # [CUSTOMIZAR] Estrutura
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        while s[right] in char_set:  # [CUSTOMIZAR] Condição
            char_set.remove(s[left])
            left += 1
        
        char_set.add(s[right])
        max_length = max(max_length, right - left + 1)  # [CUSTOMIZAR] Resultado
    
    return max_length
```

---

## 🎓 Dicas de Uso

1. **Não decore cegamente** - Entenda o porquê
2. **Pratique customizar** os templates
3. **Anote suas próprias versões** que fazem mais sentido
4. **Teste edge cases** sempre
5. **Discuta complexidade** de tempo e espaço

---

**Templates são ferramentas, não respostas prontas. Use-os com sabedoria! 🚀**
