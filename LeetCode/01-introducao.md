# 📖 Introdução ao Plano de Estudos LeetCode

## 🎯 Por Que LeetCode?

LeetCode é a plataforma mais utilizada para preparação de entrevistas técnicas em empresas de tecnologia. Dominar algoritmos e estruturas de dados é essencial para:

- ✅ Passar em entrevistas técnicas de FAANG e outras empresas top
- ✅ Desenvolver pensamento lógico e analítico
- ✅ Melhorar habilidades de resolução de problemas
- ✅ Aprender a otimizar código (tempo e espaço)
- ✅ Construir confiança para entrevistas ao vivo

## 🎓 Metodologia de Estudo

### 1. Abordagem Baseada em Padrões

Em vez de resolver problemas aleatoriamente, este plano foca em **padrões algorítmicos**:

- **Padrão**: Técnica ou estrutura que se aplica a múltiplos problemas
- **Exemplo**: Two Pointers, Sliding Window, DFS, BFS, DP, etc.
- **Benefício**: Ao reconhecer o padrão, você resolve o problema mais rápido

### 2. Framework de Resolução

Use este framework para todo problema:

#### Passo 1: Entender o Problema (5 minutos)
- Leia o problema 2-3 vezes
- Identifique inputs e outputs
- Pergunte sobre edge cases
- Faça exemplos manualmente

```python
# Exemplo: Two Sum
# Input: nums = [2,7,11,15], target = 9
# Output: [0,1]
# Por quê? nums[0] + nums[1] = 2 + 7 = 9

# Edge cases:
# - Array vazio? Não (constraints: 2 <= nums.length)
# - Números negativos? Sim
# - Múltiplas soluções? Não (exactly one solution)
# - Usar mesmo elemento duas vezes? Não
```

#### Passo 2: Pensar em Voz Alta (10 minutos)
- Descreva sua abordagem antes de codificar
- Discuta diferentes soluções (brute force → otimizada)
- Analise complexidade de cada abordagem

```
Abordagem 1 (Brute Force):
- Dois loops aninhados
- Testar todas as combinações
- Tempo: O(n²), Espaço: O(1)

Abordagem 2 (Hash Map):
- Um loop com hash map
- Verificar se complement existe
- Tempo: O(n), Espaço: O(n)
```

#### Passo 3: Codificar (15-20 minutos)
- Escreva código limpo e comentado
- Use nomes de variáveis descritivos
- Teste com exemplos durante a codificação

#### Passo 4: Testar (5-10 minutos)
- Teste casos normais
- Teste edge cases
- Faça dry run manual

#### Passo 5: Otimizar (5 minutos)
- Pode melhorar tempo ou espaço?
- Existe solução mais elegante?
- Discuta trade-offs

### 3. Análise de Complexidade

**SEMPRE** analise a complexidade da sua solução:

#### Tempo (Time Complexity)
- **O(1)**: Constante - acesso direto
- **O(log n)**: Logarítmico - binary search
- **O(n)**: Linear - percorrer array uma vez
- **O(n log n)**: Linearítmico - sorting
- **O(n²)**: Quadrático - dois loops aninhados
- **O(2ⁿ)**: Exponencial - subsets, combinações

#### Espaço (Space Complexity)
- Considere memória adicional usada
- Stack de recursão conta!
- In-place vs. extra space

```python
# Exemplo: Análise de complexidade

def two_sum(nums, target):
    """
    Tempo: O(n) - percorremos array uma vez
    Espaço: O(n) - hash map pode armazenar n elementos
    """
    seen = {}  # O(n) espaço
    for i, num in enumerate(nums):  # O(n) tempo
        complement = target - num
        if complement in seen:  # O(1) tempo
            return [seen[complement], i]
        seen[num] = i
    return []
```

## 📝 Como Abordar Cada Problema

### ✅ Etapas Recomendadas

1. **Leia o problema** sem olhar a solução
2. **Tente resolver** sozinho por 30-45 minutos
3. **Se travou**, leia apenas os hints
4. **Ainda travado?** Veja a abordagem (não o código)
5. **Implemente** a solução você mesmo
6. **Compare** com solução oficial
7. **Anote** o padrão e insights
8. **Revise** após 1 dia, 3 dias, 1 semana

### ❌ Erros Comuns a Evitar

- ❌ Ir direto para o código sem planejar
- ❌ Não testar edge cases
- ❌ Não analisar complexidade
- ❌ Copiar código sem entender
- ❌ Não praticar explicar em voz alta
- ❌ Pular problemas "fáceis"
- ❌ Não revisar problemas resolvidos

## 🎨 Padrões de Reconhecimento

Aprenda a identificar padrões pelos sinais:

### Arrays & Hashing
- 🔍 "Find/Count/Check if exists"
- 🔍 "Frequency of elements"
- 🔍 "Group anagrams"

### Two Pointers
- 🔍 "Array/string is sorted"
- 🔍 "Find pair with sum X"
- 🔍 "Remove duplicates"

### Sliding Window
- 🔍 "Contiguous subarray/substring"
- 🔍 "Maximum/minimum in window"
- 🔍 "Longest substring with K distinct"

### Stack
- 🔍 "Valid parentheses"
- 🔍 "Next greater/smaller element"
- 🔍 "Expression evaluation"

### Binary Search
- 🔍 "Sorted array"
- 🔍 "Find in O(log n)"
- 🔍 "Rotated sorted array"

### Trees
- 🔍 "Binary tree/BST"
- 🔍 "Traverse tree"
- 🔍 "Path from root to leaf"

### Graphs
- 🔍 "Connected components"
- 🔍 "Shortest path"
- 🔍 "Cycle detection"

### Dynamic Programming
- 🔍 "Maximum/minimum/count ways"
- 🔍 "Optimal substructure"
- 🔍 "Overlapping subproblems"

## 📊 Sistema de Revisão Espaçada

Use o sistema de **repetição espaçada** para memorização efetiva:

```
Dia 0: Resolve o problema
Dia 1: Revisa (sem olhar solução)
Dia 3: Revisa novamente
Dia 7: Última revisão
Dia 14: Revisão final (opcional)
```

### 🗂️ Categorizando Problemas

Após resolver cada problema, categorize:

- ✅ **Verde**: Resolveu facilmente (< 20 min)
- 🟡 **Amarelo**: Resolveu com dificuldade (20-45 min)
- 🔴 **Vermelho**: Não conseguiu resolver (precisa revisar)

Foque tempo extra em problemas vermelhos e amarelos.

## 🔧 Ferramentas e Setup

### Editor de Código
- Use IDE com syntax highlighting
- Configure shortcuts para eficiência
- Pratique codificar sem autocomplete

### LeetCode Features
- ✅ Use o Playground para testar
- ✅ Leia as discussões após resolver
- ✅ Compare sua solução com top solutions
- ✅ Use Custom Testcase para edge cases

### Caderno de Notas
Mantenha um caderno (físico ou digital) com:
- Padrões identificados
- Templates de código
- Erros comuns
- Insights importantes

## 🎯 Metas de Desempenho

### Por Dificuldade
- **Easy**: Resolver em 10-15 minutos
- **Medium**: Resolver em 25-35 minutos
- **Hard**: Resolver em 40-50 minutos

### Por Fase
- **Semanas 1-4**: Aprender padrões (tempo não importa)
- **Semanas 5-8**: Consolidar (começar a cronometrar)
- **Semanas 9-12**: Dominar (resolver no tempo ideal)

## 💬 Prática de Comunicação

Durante entrevistas, você precisa **verbalizar seu raciocínio**. Pratique:

1. **Reformular** o problema com suas palavras
2. **Propor** abordagens (brute force primeiro)
3. **Discutir** trade-offs de cada solução
4. **Explicar** enquanto codifica
5. **Testar** e corrigir bugs em voz alta

### Exemplo de Verbalização

```
"Ok, então eu preciso encontrar dois números que somam o target.
Uma abordagem seria testar todas as combinações, mas isso seria O(n²).
Uma solução melhor seria usar um hash map para armazenar números já vistos.
Enquanto percorro o array, verifico se o complemento (target - num) 
já foi visto. Se sim, retorno os índices. Se não, adiciono o número 
atual ao hash map. Isso me dá O(n) tempo e O(n) espaço."
```

## 📚 Recursos Complementares

- **[NeetCode.io](https://neetcode.io/)**: Vídeos explicando problemas
- **[Visualgo](https://visualgo.net/)**: Visualizações de algoritmos
- **[LeetCode Patterns](https://seanprashad.com/leetcode-patterns/)**: Lista organizada
- **[Tech Interview Handbook](https://www.techinterviewhandbook.org/)**: Guia completo

## 🚀 Começando

Agora que você entende a metodologia, está pronto para começar!

1. Vá para a [Lista dos 150 Problemas](02-lista-150-problemas.md)
2. Comece com a categoria **Arrays & Hashing**
3. Siga o [Cronograma de 12 Semanas](03-cronograma-12-semanas.md)
4. Use os [Templates de Código](05-templates-codigo.md) como referência

---

**Lembre-se**: A jornada é mais importante que o destino. Foque em aprender profundamente, não apenas resolver problemas superficialmente. 🌟

**Boa sorte! 💪🚀**
