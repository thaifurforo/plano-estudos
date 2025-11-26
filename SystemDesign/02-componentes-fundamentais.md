# 🧱 Componentes Fundamentais de System Design

## 📚 Building Blocks Essenciais

Estes são os componentes que você usará repetidamente ao desenhar sistemas.

---

## 1. 🔀 Load Balancer

### O Que É
Distribui tráfego entre múltiplos servidores para:
- Evitar sobrecarga de um servidor
- Aumentar disponibilidade
- Melhorar throughput

### Tipos

#### Layer 4 (Transport)
- Opera em TCP/UDP
- Rápido e simples
- Baseado em IP/porta
- Exemplo: AWS NLB

#### Layer 7 (Application)
- Opera em HTTP/HTTPS
- Roteamento baseado em conteúdo
- SSL termination
- Exemplo: AWS ALB, NGINX

### Algoritmos de Distribuição

```python
# Round Robin
servers = ['s1', 's2', 's3']
current = 0

def get_server():
    global current
    server = servers[current]
    current = (current + 1) % len(servers)
    return server
```

**Outros algoritmos**:
- **Least Connections**: Servidor com menos conexões
- **Weighted Round Robin**: Peso por capacidade
- **IP Hash**: Mesmo cliente → mesmo servidor

### Quando Usar
✅ Múltiplos servidores idênticos
✅ Alta disponibilidade necessária  
✅ Tráfego distribuído geograficamente

---

## 2. 💾 Cache

### O Que É
Armazenamento temporário de dados frequentemente acessados para:
- Reduzir latência
- Diminuir carga no database
- Melhorar performance

### Tipos de Cache

#### Application Cache
- Dados em memória da aplicação
- Exemplo: Dicionários, HashMaps

#### Distributed Cache
- Compartilhado entre instâncias
- Exemplo: **Redis**, **Memcached**

#### CDN Cache
- Cache de conteúdo estático
- Exemplo: CloudFront, Cloudflare

### Estratégias de Cache

#### 1. Cache-Aside (Lazy Loading)
```python
def get_data(key):
    # Tenta cache primeiro
    data = cache.get(key)
    if data:
        return data
    
    # Cache miss: busca no DB
    data = database.get(key)
    cache.set(key, data, ttl=3600)
    return data
```

**Pros**: Apenas dados usados são cacheados
**Cons**: Cache miss tem 3x latência

#### 2. Write-Through
```python
def save_data(key, data):
    # Escreve no cache E database
    database.set(key, data)
    cache.set(key, data)
```

**Pros**: Cache sempre consistente
**Cons**: Latência de escrita maior

#### 3. Write-Back (Write-Behind)
```python
def save_data(key, data):
    # Escreve no cache
    cache.set(key, data)
    # Database escrita assíncrona
    queue.enqueue({'key': key, 'data': data})
```

**Pros**: Escrita rápida
**Cons**: Risco de perda de dados

### Eviction Policies

- **LRU** (Least Recently Used): Remove menos usado recentemente
- **LFU** (Least Frequently Used): Remove menos frequente
- **FIFO**: Remove mais antigo
- **TTL** (Time To Live): Expira após tempo

### Cache Invalidation

Problema difícil! Estratégias:
1. **TTL**: Expira automaticamente
2. **Event-based**: Invalida quando dado muda
3. **Version-based**: Incrementa versão

### Redis vs Memcached

| Feature | Redis | Memcached |
|---------|-------|-----------|
| Tipos de dados | Strings, Lists, Sets, Hashes | Apenas Strings |
| Persistência | Sim (RDB, AOF) | Não |
| Replicação | Sim | Não nativo |
| Uso de memória | Mais eficiente | Simples |
| Caso de uso | Cache + DS | Cache simples |

---

## 3. 🗄️ Databases

### SQL (Relacional)

**Quando usar**:
- Dados estruturados
- Relacionamentos complexos
- Transações ACID necessárias
- Queries complexas com JOINs

**Exemplos**: PostgreSQL, MySQL, Oracle

```sql
-- Schema estruturado
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE,
    created_at TIMESTAMP
);

CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    total DECIMAL(10,2)
);
```

### NoSQL

#### Document Store
**MongoDB, CouchDB**

```json
{
  "_id": "user123",
  "email": "user@example.com",
  "profile": {
    "name": "João",
    "age": 30
  },
  "orders": [
    {"id": "order1", "total": 99.99}
  ]
}
```

**Quando usar**:
- Schema flexível
- Dados hierárquicos
- Desenvolvimento rápido

#### Key-Value Store
**Redis, DynamoDB, Riak**

```python
# Simples: chave → valor
set("user:123", "João")
get("user:123")  # "João"
```

**Quando usar**:
- Acesso simples por chave
- Cache
- Session storage

#### Column-Family Store
**Cassandra, HBase**

```
RowKey: user123
Columns:
  name: "João"
  email: "user@example.com"
  age: 30
```

**Quando usar**:
- Writes massivos
- Time-series data
- Analytics

#### Graph Database
**Neo4j, Amazon Neptune**

```cypher
// Relacionamentos são first-class
CREATE (u:User {name: 'João'})
CREATE (f:User {name: 'Maria'})
CREATE (u)-[:FOLLOWS]->(f)
```

**Quando usar**:
- Relacionamentos complexos
- Social networks
- Recommendations

### SQL vs NoSQL

| Critério | SQL | NoSQL |
|----------|-----|-------|
| Schema | Fixo | Flexível |
| Escalabilidade | Vertical (difícil) | Horizontal (fácil) |
| Transações | ACID | BASE |
| Queries | SQL (poderoso) | Limitado |
| Consistência | Forte | Eventual |

---

## 4. 🌐 CDN (Content Delivery Network)

### O Que É
Rede distribuída de servidores que entrega conteúdo baseado em localização geográfica.

### Como Funciona

```
User (Brasil) → CDN Edge (São Paulo) → Origin Server (US)
                ↓ Cache hit
                Retorna conteúdo local (low latency)
```

### Benefícios
- **Latência**: Serve de servidor próximo
- **Disponibilidade**: Redundância global
- **Custo**: Reduz bandwidth do origin
- **Segurança**: DDoS protection

### Quando Usar
✅ Conteúdo estático (imagens, videos, CSS, JS)
✅ Audiência global
✅ High traffic

**Exemplos**: CloudFront, Cloudflare, Akamai

---

## 5. 📬 Message Queue

### O Que É
Sistema de mensagens assíncronas que desacopla produtores e consumidores.

### Padrões

#### 1. Point-to-Point (Queue)
```
Producer → Queue → Consumer
```
- Uma mensagem = um consumidor
- Exemplo: Task processing

#### 2. Publish-Subscribe (Topic)
```
Publisher → Topic → Subscriber 1
                   → Subscriber 2
                   → Subscriber 3
```
- Uma mensagem = múltiplos consumidores
- Exemplo: Event broadcasting

### Tecnologias

#### RabbitMQ
- Full-featured
- Protocol: AMQP
- Garantias de entrega

#### Apache Kafka
- High-throughput
- Log-based
- Stream processing
- Retenção de mensagens

#### AWS SQS
- Managed service
- Simples e escalável
- Pay per use

### Quando Usar
✅ Processamento assíncrono
✅ Desacoplar serviços
✅ Load leveling (suavizar picos)
✅ Garantir entrega de mensagens

### Exemplo

```python
# Producer
queue.send({
    'type': 'email',
    'to': 'user@example.com',
    'subject': 'Welcome!'
})

# Consumer
def process_message(msg):
    if msg['type'] == 'email':
        send_email(msg['to'], msg['subject'])
    queue.ack(msg)  # Confirma processamento
```

---

## 6. 🔐 API Gateway

### O Que É
Ponto de entrada único para APIs que oferece:
- Roteamento
- Autenticação
- Rate limiting
- Monitoring
- Response caching

### Responsabilidades

```
Client → API Gateway → Microservice A
                     → Microservice B
                     → Microservice C
```

**Funcionalidades**:
1. **Authentication**: JWT, OAuth
2. **Rate Limiting**: Prevenir abuso
3. **Load Balancing**: Distribuir tráfego
4. **Request/Response Transformation**
5. **Logging & Monitoring**
6. **API Versioning**

### Quando Usar
✅ Arquitetura de microservices
✅ Múltiplos clientes (web, mobile, IoT)
✅ Necessidade de autenticação centralizada

**Exemplos**: AWS API Gateway, Kong, Apigee

---

## 7. 🔍 Search Engine

### Elasticsearch

Motor de busca distribuído para:
- Full-text search
- Analytics
- Logging (ELK stack)

**Quando usar**:
- Busca textual complexa
- Autocompletion
- Faceted search
- Log aggregation

```json
// Indexar documento
PUT /products/_doc/1
{
  "name": "iPhone 15",
  "category": "electronics",
  "price": 999
}

// Buscar
GET /products/_search
{
  "query": {
    "match": {
      "name": "iphone"
    }
  }
}
```

---

## 8. 📊 Monitoring & Observability

### Métricas (Metrics)
Dados numéricos sobre sistema:
- CPU, RAM, Disk
- Request rate, latency
- Error rate

**Tools**: Prometheus, Grafana, CloudWatch

### Logs
Registros de eventos:
- Application logs
- Access logs
- Error logs

**Tools**: ELK Stack (Elasticsearch, Logstash, Kibana)

### Traces
Rastreamento de requisições:
- Distributed tracing
- Performance bottlenecks

**Tools**: Jaeger, Zipkin, AWS X-Ray

---

## 9. 🔐 Autenticação & Autorização

### Session-Based
```
1. Login → Server cria session → Session ID em cookie
2. Requests incluem cookie
3. Server valida session
```

**Pros**: Simples, pode revogar
**Cons**: Stateful, não escala bem

### Token-Based (JWT)
```
1. Login → Server gera JWT
2. Client envia JWT em header
3. Server valida JWT (stateless)
```

**Pros**: Stateless, escala bem
**Cons**: Difícil revogar

```json
// JWT payload
{
  "sub": "user123",
  "name": "João",
  "exp": 1735689600
}
```

### OAuth 2.0
Delegação de autorização:
- Login com Google, Facebook
- Third-party API access

---

## 10. 🛡️ Security

### HTTPS/TLS
- Encryption em trânsito
- Certificados SSL/TLS

### Rate Limiting
```python
# Token bucket algorithm
class RateLimiter:
    def __init__(self, rate, capacity):
        self.rate = rate  # tokens/sec
        self.capacity = capacity
        self.tokens = capacity
        self.last_update = time.time()
    
    def allow_request(self):
        now = time.time()
        # Adiciona tokens baseado no tempo
        elapsed = now - self.last_update
        self.tokens = min(self.capacity, 
                         self.tokens + elapsed * self.rate)
        self.last_update = now
        
        if self.tokens >= 1:
            self.tokens -= 1
            return True
        return False
```

### DDoS Protection
- CDN (Cloudflare)
- WAF (Web Application Firewall)
- Auto-scaling

---

## 📚 Resumo dos Componentes

| Componente | Propósito | Exemplos |
|------------|-----------|----------|
| Load Balancer | Distribuir tráfego | NGINX, AWS ALB |
| Cache | Melhorar performance | Redis, Memcached |
| Database | Persistir dados | PostgreSQL, MongoDB |
| CDN | Entregar conteúdo | CloudFront, Cloudflare |
| Message Queue | Comunicação assíncrona | Kafka, RabbitMQ |
| API Gateway | Entrada de APIs | Kong, AWS API Gateway |
| Search | Busca textual | Elasticsearch |
| Monitoring | Observabilidade | Prometheus, ELK |

---

**Domine estes componentes e você terá as ferramentas para desenhar qualquer sistema! 🚀**
