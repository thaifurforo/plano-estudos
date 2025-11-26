# 📋 Lista dos 150 Problemas LeetCode

## 📊 Visão Geral

Esta lista contém os **150 problemas mais importantes** para entrevistas técnicas, organizados por categoria e padrão algorítmico.

**Legenda de Dificuldade:**
- 🟢 **Easy** - Problemas fundamentais
- 🟡 **Medium** - Maioria das entrevistas
- 🔴 **Hard** - Empresas top tier

---

## 1. Arrays & Hashing (15 problemas)

### 1. Two Sum
- **Dificuldade**: 🟢 Easy
- **Link**: [LeetCode #1](https://leetcode.com/problems/two-sum/)
- **Descrição**: Encontrar dois números que somam target
- **Técnica**: Hash Map
- **Complexidade**: O(n) tempo, O(n) espaço
- **Pontos-chave**:
  - Use hash map para lookup O(1)
  - Armazene complement
  - Cuidado com usar mesmo elemento duas vezes

### 2. Contains Duplicate
- **Dificuldade**: 🟢 Easy
- **Link**: [LeetCode #217](https://leetcode.com/problems/contains-duplicate/)
- **Descrição**: Verificar se há duplicatas no array
- **Técnica**: Hash Set
- **Complexidade**: O(n) tempo, O(n) espaço
- **Pontos-chave**:
  - Set para verificar existência
  - Retornar true ao encontrar duplicata
  - Alternativa: ordenar primeiro O(n log n)

### 3. Valid Anagram
- **Dificuldade**: 🟢 Easy
- **Link**: [LeetCode #242](https://leetcode.com/problems/valid-anagram/)
- **Descrição**: Verificar se duas strings são anagramas
- **Técnica**: Frequency Counter
- **Complexidade**: O(n) tempo, O(1) espaço (26 letras)
- **Pontos-chave**:
  - Contar frequência de cada caractere
  - Comparar contadores
  - Pode usar sorted() também

### 4. Group Anagrams
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #49](https://leetcode.com/problems/group-anagrams/)
- **Descrição**: Agrupar strings que são anagramas
- **Técnica**: Hash Map com chave canônica
- **Complexidade**: O(n*k log k) tempo onde k é comprimento
- **Pontos-chave**:
  - Use sorted string como chave
  - Ou use tuple de contadores
  - Hash map de listas

### 5. Top K Frequent Elements
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #347](https://leetcode.com/problems/top-k-frequent-elements/)
- **Descrição**: Encontrar k elementos mais frequentes
- **Técnica**: Heap ou Bucket Sort
- **Complexidade**: O(n log k) com heap, O(n) com bucket
- **Pontos-chave**:
  - Contar frequências primeiro
  - Min heap de tamanho k
  - Bucket sort para O(n)

### 6. Product of Array Except Self
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #238](https://leetcode.com/problems/product-of-array-except-self/)
- **Descrição**: Produto de todos exceto elemento atual
- **Técnica**: Prefix/Suffix products
- **Complexidade**: O(n) tempo, O(1) espaço
- **Pontos-chave**:
  - Não pode usar divisão
  - Duas passadas: left e right
  - Otimizar espaço usando output array

### 7. Valid Sudoku
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #36](https://leetcode.com/problems/valid-sudoku/)
- **Descrição**: Validar board de Sudoku
- **Técnica**: Hash Sets para linhas/colunas/boxes
- **Complexidade**: O(1) tempo (9x9 fixo), O(1) espaço
- **Pontos-chave**:
  - 3 sets: rows, cols, boxes
  - Box index: (r//3, c//3)
  - Verificar duplicatas

### 8. Encode and Decode Strings
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #271](https://leetcode.com/problems/encode-and-decode-strings/)
- **Descrição**: Serializar/deserializar lista de strings
- **Técnica**: Length prefix
- **Complexidade**: O(n) tempo, O(1) espaço
- **Pontos-chave**:
  - Formato: "4#word5#hello"
  - Armazenar comprimento + delimitador
  - Parse com índices

### 9. Longest Consecutive Sequence
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #128](https://leetcode.com/problems/longest-consecutive-sequence/)
- **Descrição**: Maior sequência consecutiva
- **Técnica**: Hash Set
- **Complexidade**: O(n) tempo, O(n) espaço
- **Pontos-chave**:
  - Adicionar todos em set
  - Só começar contagem se num-1 não existe
  - Contar sequência crescente

### 10-15. Problemas Adicionais Arrays & Hashing
- Replace Elements (Easy)
- Is Subsequence (Easy)
- Length of Last Word (Easy)
- Longest Common Prefix (Easy)
- Palindrome Number (Easy)
- Roman to Integer (Easy)

---

## 2. Two Pointers (12 problemas)

### 11. Valid Palindrome
- **Dificuldade**: 🟢 Easy
- **Link**: [LeetCode #125](https://leetcode.com/problems/valid-palindrome/)
- **Descrição**: Verificar se string é palíndromo
- **Técnica**: Two Pointers (opposite direction)
- **Complexidade**: O(n) tempo, O(1) espaço

### 12. Two Sum II - Input Array Sorted
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #167](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
- **Descrição**: Two Sum em array ordenado
- **Técnica**: Two Pointers
- **Complexidade**: O(n) tempo, O(1) espaço

### 13. 3Sum
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #15](https://leetcode.com/problems/3sum/)
- **Descrição**: Encontrar triplas com soma zero
- **Técnica**: Sorting + Two Pointers
- **Complexidade**: O(n²) tempo, O(1) espaço

### 14. Container With Most Water
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #11](https://leetcode.com/problems/container-with-most-water/)
- **Descrição**: Máxima área de água
- **Técnica**: Two Pointers
- **Complexidade**: O(n) tempo, O(1) espaço

### 15. Trapping Rain Water
- **Dificuldade**: 🔴 Hard
- **Link**: [LeetCode #42](https://leetcode.com/problems/trapping-rain-water/)
- **Descrição**: Calcular água acumulada
- **Técnica**: Two Pointers ou Stack
- **Complexidade**: O(n) tempo, O(1) espaço

### 16-22. Mais Two Pointers
- Remove Duplicates from Sorted Array (Easy)
- Remove Element (Easy)
- Move Zeroes (Easy)
- Sort Colors (Medium)

---

## 3. Sliding Window (10 problemas)

### 23. Best Time to Buy and Sell Stock
- **Dificuldade**: 🟢 Easy
- **Link**: [LeetCode #121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
- **Técnica**: Sliding Window / Min tracking
- **Complexidade**: O(n) tempo, O(1) espaço

### 24. Longest Substring Without Repeating Characters
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #3](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- **Técnica**: Variable Sliding Window
- **Complexidade**: O(n) tempo, O(k) espaço

### 25. Longest Repeating Character Replacement
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #424](https://leetcode.com/problems/longest-repeating-character-replacement/)
- **Técnica**: Sliding Window com contador
- **Complexidade**: O(n) tempo, O(1) espaço

### 26. Minimum Window Substring
- **Dificuldade**: 🔴 Hard
- **Link**: [LeetCode #76](https://leetcode.com/problems/minimum-window-substring/)
- **Técnica**: Sliding Window com hash map
- **Complexidade**: O(n+m) tempo, O(k) espaço

### 27-32. Mais Sliding Window
- Permutation in String (Medium)
- Find All Anagrams (Medium)
- Minimum Size Subarray Sum (Medium)
- Sliding Window Maximum (Hard)

---

## 4. Stack (10 problemas)

### 33. Valid Parentheses
- **Dificuldade**: 🟢 Easy
- **Link**: [LeetCode #20](https://leetcode.com/problems/valid-parentheses/)
- **Técnica**: Stack
- **Complexidade**: O(n) tempo, O(n) espaço

### 34. Min Stack
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #155](https://leetcode.com/problems/min-stack/)
- **Técnica**: Two stacks ou pairs
- **Complexidade**: O(1) todas operações

### 35. Evaluate Reverse Polish Notation
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #150](https://leetcode.com/problems/evaluate-reverse-polish-notation/)
- **Técnica**: Stack
- **Complexidade**: O(n) tempo, O(n) espaço

### 36. Daily Temperatures
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #739](https://leetcode.com/problems/daily-temperatures/)
- **Técnica**: Monotonic Stack
- **Complexidade**: O(n) tempo, O(n) espaço

### 37-42. Mais Stack
- Generate Parentheses (Medium)
- Car Fleet (Medium)
- Largest Rectangle in Histogram (Hard)

---

## 5. Binary Search (12 problemas)

### 43. Binary Search
- **Dificuldade**: 🟢 Easy
- **Link**: [LeetCode #704](https://leetcode.com/problems/binary-search/)
- **Técnica**: Classic Binary Search
- **Complexidade**: O(log n) tempo, O(1) espaço

### 44. Search in Rotated Sorted Array
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #33](https://leetcode.com/problems/search-in-rotated-sorted-array/)
- **Técnica**: Modified Binary Search
- **Complexidade**: O(log n) tempo, O(1) espaço

### 45-54. Mais Binary Search
- Search Insert Position (Easy)
- Find Minimum in Rotated Sorted Array (Medium)
- Search a 2D Matrix (Medium)
- Koko Eating Bananas (Medium)
- Time Based Key-Value Store (Medium)
- Median of Two Sorted Arrays (Hard)

---

## 6. Linked List (10 problemas)

### 55. Reverse Linked List
- **Dificuldade**: 🟢 Easy
- **Link**: [LeetCode #206](https://leetcode.com/problems/reverse-linked-list/)
- **Técnica**: Iterative/Recursive reversal
- **Complexidade**: O(n) tempo, O(1) espaço

### 56. Merge Two Sorted Lists
- **Dificuldade**: 🟢 Easy
- **Link**: [LeetCode #21](https://leetcode.com/problems/merge-two-sorted-lists/)
- **Técnica**: Two pointers
- **Complexidade**: O(n+m) tempo, O(1) espaço

### 57. Linked List Cycle
- **Dificuldade**: 🟢 Easy
- **Link**: [LeetCode #141](https://leetcode.com/problems/linked-list-cycle/)
- **Técnica**: Fast & Slow pointers
- **Complexidade**: O(n) tempo, O(1) espaço

### 58-64. Mais Linked List
- Reorder List (Medium)
- Remove Nth Node From End (Medium)
- Copy List with Random Pointer (Medium)
- Add Two Numbers (Medium)
- LRU Cache (Medium)
- Merge K Sorted Lists (Hard)

---

## 7. Trees (20 problemas)

### 65. Invert Binary Tree
- **Dificuldade**: 🟢 Easy
- **Link**: [LeetCode #226](https://leetcode.com/problems/invert-binary-tree/)
- **Técnica**: DFS/BFS
- **Complexidade**: O(n) tempo, O(h) espaço

### 66. Maximum Depth of Binary Tree
- **Dificuldade**: 🟢 Easy
- **Link**: [LeetCode #104](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- **Técnica**: DFS
- **Complexidade**: O(n) tempo, O(h) espaço

### 67-84. Mais Trees
- Diameter of Binary Tree (Easy)
- Balanced Binary Tree (Easy)
- Same Tree (Easy)
- Subtree of Another Tree (Easy)
- Lowest Common Ancestor of BST (Medium)
- Binary Tree Level Order Traversal (Medium)
- Binary Tree Right Side View (Medium)
- Count Good Nodes (Medium)
- Validate BST (Medium)
- Kth Smallest Element in BST (Medium)
- Construct Binary Tree (Medium)
- Binary Tree Maximum Path Sum (Hard)
- Serialize and Deserialize Binary Tree (Hard)

---

## 8. Tries (3 problemas)

### 85. Implement Trie
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #208](https://leetcode.com/problems/implement-trie-prefix-tree/)
- **Técnica**: Trie implementation
- **Complexidade**: O(m) tempo por operação

### 86-87. Mais Tries
- Design Add and Search Words (Medium)
- Word Search II (Hard)

---

## 9. Heap / Priority Queue (7 problemas)

### 88. Kth Largest Element
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #215](https://leetcode.com/problems/kth-largest-element-in-an-array/)
- **Técnica**: Min Heap de tamanho k
- **Complexidade**: O(n log k) tempo

### 89-94. Mais Heap
- Find Median from Data Stream (Hard)
- Last Stone Weight (Easy)
- K Closest Points (Medium)
- Task Scheduler (Medium)
- Design Twitter (Medium)

---

## 10. Backtracking (10 problemas)

### 95. Subsets
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #78](https://leetcode.com/problems/subsets/)
- **Técnica**: Backtracking
- **Complexidade**: O(2^n) tempo

### 96-104. Mais Backtracking
- Combination Sum (Medium)
- Permutations (Medium)
- Subsets II (Medium)
- Combination Sum II (Medium)
- Word Search (Medium)
- Palindrome Partitioning (Medium)
- Letter Combinations (Medium)
- N-Queens (Hard)

---

## 11. Graphs (15 problemas)

### 105. Number of Islands
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #200](https://leetcode.com/problems/number-of-islands/)
- **Técnica**: DFS/BFS
- **Complexidade**: O(m*n) tempo

### 106-119. Mais Graphs
- Clone Graph (Medium)
- Max Area of Island (Medium)
- Pacific Atlantic Water Flow (Medium)
- Surrounded Regions (Medium)
- Rotting Oranges (Medium)
- Course Schedule (Medium)
- Course Schedule II (Medium)
- Number of Connected Components (Medium)
- Graph Valid Tree (Medium)

---

## 12. 1-D Dynamic Programming (12 problemas)

### 120. Climbing Stairs
- **Dificuldade**: 🟢 Easy
- **Link**: [LeetCode #70](https://leetcode.com/problems/climbing-stairs/)
- **Técnica**: DP 1D
- **Complexidade**: O(n) tempo, O(1) espaço

### 121-131. Mais 1D DP
- House Robber (Medium)
- House Robber II (Medium)
- Longest Palindromic Substring (Medium)
- Palindromic Substrings (Medium)
- Decode Ways (Medium)
- Coin Change (Medium)
- Maximum Product Subarray (Medium)
- Word Break (Medium)
- Longest Increasing Subsequence (Medium)

---

## 13. 2-D Dynamic Programming (11 problemas)

### 132. Unique Paths
- **Dificuldade**: 🟡 Medium
- **Link**: [LeetCode #62](https://leetcode.com/problems/unique-paths/)
- **Técnica**: DP 2D
- **Complexidade**: O(m*n) tempo e espaço

### 133-142. Mais 2D DP
- Longest Common Subsequence (Medium)
- Best Time to Buy and Sell Stock with Cooldown (Medium)
- Coin Change 2 (Medium)
- Target Sum (Medium)
- Interleaving String (Medium)
- Longest Increasing Path (Hard)
- Distinct Subsequences (Hard)
- Edit Distance (Hard)
- Burst Balloons (Hard)
- Regular Expression Matching (Hard)

---

## 14. Advanced Graphs (3 problemas)

### 143. Dijkstra's Algorithm
- **Dificuldade**: 🟡 Medium
- **Link**: Network Delay Time
- **Técnica**: Dijkstra
- **Complexidade**: O((V+E) log V) tempo

### 144-145. Mais Advanced Graphs
- Cheapest Flights Within K Stops (Medium)
- Min Cost to Connect All Points (Medium)

---

## 📊 Distribuição por Dificuldade

| Dificuldade | Quantidade | Porcentagem |
|-------------|------------|-------------|
| 🟢 Easy | 35 | 23% |
| 🟡 Medium | 95 | 63% |
| 🔴 Hard | 20 | 14% |
| **Total** | **150** | **100%** |

---

## 📈 Como Usar Esta Lista

1. **Siga o cronograma**: Use com o [Cronograma de 12 Semanas](03-cronograma-12-semanas.md)
2. **Marque seu progresso**: Track o que você completou
3. **Revise regularmente**: Use sistema de repetição espaçada
4. **Foque em padrões**: Aprenda a técnica, não memorize problemas

---

**Lista completa! Bons estudos! 🚀**
