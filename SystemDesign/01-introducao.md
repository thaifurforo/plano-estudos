# 📖 Introdução ao System Design

## 🎯 O Que é System Design?

**System Design** é a arte e ciência de projetar sistemas de software escaláveis, confiáveis e eficientes que resolvem problemas do mundo real.

### Definição
> System Design é o processo de definir a arquitetura, componentes, módulos, interfaces e dados de um sistema para satisfazer requisitos específicos.

## 🤔 Por Que System Design é Importante?

### 1. **Entrevistas Técnicas**
- Obrigatório para posições Senior+ em empresas tech
- Avalia pensamento arquitetural e tomada de decisões
- Diferencial entre níveis de senioridade

### 2. **Trabalho Diário**
- Tomar decisões arquiteturais informadas
- Comunicar design com time
- Evitar problemas de escalabilidade

### 3. **Crescimento Profissional**
- Transição de IC (Individual Contributor) para Tech Lead
- Arquiteto de Soluções
- Engineering Manager

## 🎨 Diferença: Coding vs System Design

| Aspecto | Coding Interview | System Design |
|---------|------------------|---------------|
| **Foco** | Algoritmos, DS | Arquitetura, Escalabilidade |
| **Escopo** | Função/classe | Sistema completo |
| **Resposta** | Uma solução ótima | Múltiplas soluções válidas |
| **Avaliação** | Corretude, eficiência | Trade-offs, raciocínio |
| **Tempo** | 30-45 min | 45-60 min |

## 🏗️ Componentes de um Bom Design

### 1. **Escalabilidade**
Capacidade de lidar com crescimento de carga

```
Escalabilidade = Performance sob carga crescente
```

### 2. **Confiabilidade**
Sistema continua funcionando mesmo com falhas

```
Confiabilidade = Uptime / (Uptime + Downtime)
Target: 99.9% (três noves) = 8.76h downtime/ano
```

### 3. **Disponibilidade**
Sistema está operacional e acessível

```
Disponibilidade ≠ Confiabilidade
Pode estar disponível mas retornando dados incorretos
```

### 4. **Eficiência**
Utilização ótima de recursos

- **Latência**: Tempo de resposta
- **Throughput**: Requisições por segundo

### 5. **Manutenibilidade**
Facilidade de manter e evoluir

- Código limpo
- Documentação
- Monitoramento

## 📊 Níveis de Design

### High-Level Design (HLD)
- Visão geral do sistema
- Componentes principais
- Fluxo de dados
- APIs externas

### Low-Level Design (LLD)
- Detalhes de implementação
- Classes e métodos
- Schemas de banco
- Algoritmos específicos

**Em entrevistas**: Foco em HLD, LLD apenas se solicitado

## 🎓 Conceitos Fundamentais

### CAP Theorem
Sistema distribuído pode ter apenas 2 de 3:

- **C**onsistency: Todos veem os mesmos dados
- **A**vailability: Sistema sempre responde
- **P**artition Tolerance: Funciona mesmo com falhas de rede

```
Escolhas comuns:
- CP: Bancos tradicionais (consistency > availability)
- AP: Redes sociais (availability > consistency)
```

### ACID vs BASE

**ACID** (Databases relacionais):
- **A**tomicity: Tudo ou nada
- **C**onsistency: Dados válidos
- **I**solation: Transações independentes
- **D**urability: Dados persistidos

**BASE** (NoSQL):
- **B**asically **A**vailable: Sempre responde
- **S**oft state: Estado pode mudar
- **E**ventually consistent: Eventualmente consistente

## 🔢 Estimativas de Capacidade

### Números que Todo Engenheiro Deve Saber

```
L1 cache reference:           0.5 ns
L2 cache reference:           7 ns
RAM access:                   100 ns
SSD random read:              150 μs
HDD seek:                     10 ms
Network packet CA->EU:        150 ms

1 MB = 1000 KB = 1,000,000 bytes
1 GB = 1000 MB
1 TB = 1000 GB
```

### Cálculos Rápidos

**Requisições por Segundo (RPS)**:
```
100M usuários ativos/dia
Cada usuário faz 10 requisições/dia
= 1B requisições/dia
= 1,000,000,000 / (24 * 3600)
≈ 11,574 RPS

Peak (2x média) ≈ 23,000 RPS
```

**Storage**:
```
1M usuários
Cada usuário = 1KB dados
= 1GB storage

Crescimento 20%/ano por 5 anos
= 1GB * (1.2^5)
≈ 2.5GB
```

## 🎯 O Que Entrevistadores Avaliam

### 1. **Pensamento Estruturado**
- Abordagem sistemática
- Não pula etapas
- Organização clara

### 2. **Comunicação**
- Explica decisões
- Pergunta quando incerto
- Ouve feedback

### 3. **Trade-offs**
- Identifica pros e cons
- Justifica escolhas
- Considera alternativas

### 4. **Conhecimento Técnico**
- Componentes de sistema
- Padrões de arquitetura
- Boas práticas

### 5. **Pragmatismo**
- Soluções práticas
- Não over-engineering
- Considera constraints

## 🚫 Erros Comuns

### ❌ Ir Direto para Detalhes
Não comece com "vou usar Kafka e Redis"
✅ Primeiro: requisitos, estimativas, high-level

### ❌ Solução Única
Não existe "a melhor solução"
✅ Discuta múltiplas abordagens e trade-offs

### ❌ Ignorar Requisitos
Não assuma, pergunte!
✅ Clarifique requisitos funcionais e não-funcionais

### ❌ Ficar em Silêncio
Entrevistador não sabe o que você está pensando
✅ Pense em voz alta, compartilhe raciocínio

### ❌ Não Discutir Falhas
Todo sistema pode falhar
✅ Discuta pontos de falha e mitigações

## 📚 Tópicos Essenciais

### Fundamentais
- [ ] Load Balancers
- [ ] Caching
- [ ] Databases (SQL vs NoSQL)
- [ ] Replication e Sharding
- [ ] Message Queues
- [ ] CDN

### Intermediários  
- [ ] Microservices
- [ ] API Gateway
- [ ] Service Discovery
- [ ] Consistent Hashing
- [ ] Rate Limiting
- [ ] Circuit Breaker

### Avançados
- [ ] Event Sourcing
- [ ] CQRS
- [ ] Saga Pattern
- [ ] Two-Phase Commit
- [ ] Vector Clocks
- [ ] Bloom Filters

## 🎯 Próximos Passos

1. Estude [Componentes Fundamentais](02-componentes-fundamentais.md)
2. Entenda [Conceitos de Escalabilidade](03-conceitos-escalabilidade.md)
3. Aprenda [Padrões de Arquitetura](04-padroes-arquitetura.md)
4. Pratique com [Estudos de Caso](05-estudos-caso.md)

---

## 💡 Citações Inspiradoras

> "Premature optimization is the root of all evil" - Donald Knuth

> "Make it work, make it right, make it fast" - Kent Beck

> "Simplicity is prerequisite for reliability" - Edsger Dijkstra

---

**Pronto para começar! 🚀**
