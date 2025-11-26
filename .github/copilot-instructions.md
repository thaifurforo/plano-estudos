# Instruções Personalizadas do GitHub Copilot

## Contexto do Repositório
Este repositório contém planos de estudos estruturados para o crescimento de carreira em engenharia de software, focando no desenvolvimento de habilidades técnicas e comportamentais necessárias para atuar em nível sênior. O conteúdo é organizado usando MkDocs e publicado no GitHub Pages.

## Diretrizes de Desenvolvimento

### Idioma e Comunicação
- Todo o conteúdo deve ser escrito em português brasileiro (pt-BR)
- Mantenha um tom profissional e educacional
- Use exemplos práticos e aplicáveis ao mercado brasileiro

### Estrutura do Projeto
- **docs/**: Contém toda a documentação em Markdown
  - `index.md`: Página inicial do site
  - `leetcode/`: Plano de estudos de algoritmos e estruturas de dados
  - `system-design/`: Plano de estudos de design de sistemas
  - `soft-skills/`: Plano de estudos de habilidades comportamentais
- **mkdocs.yml**: Configuração do MkDocs (navegação, tema, plugins)
- **requirements.txt**: Dependências Python do projeto

### Convenções de Código e Conteúdo
1. **Arquivos Markdown**:
   - Use `index.md` como página principal de cada seção
   - Numere arquivos sequencialmente (ex: `01-introducao.md`, `02-componentes.md`)
   - Inclua emojis apropriados nos títulos para melhor visualização
   
2. **MkDocs**:
   - Sempre teste mudanças com `mkdocs serve` antes de commitar
   - Mantenha a estrutura de navegação (nav) sincronizada com os arquivos
   - Use o tema Material for MkDocs com suporte a modo claro/escuro
   
3. **Foco no Conteúdo**:
   - O objetivo é crescimento de carreira para nível sênior
   - Evite referências específicas a "preparação para entrevistas"
   - Enfatize desenvolvimento de habilidades aplicáveis no dia a dia

### Comandos Úteis
```bash
# Instalar dependências
pip install -r requirements.txt

# Servidor de desenvolvimento local
mkdocs serve

# Build do site
mkdocs build

# Deploy para GitHub Pages
mkdocs gh-deploy
```

### Áreas de Conhecimento
1. **Algoritmos e Estruturas de Dados**: 150 problemas essenciais do LeetCode organizados por padrões
2. **System Design**: Fundamentos de sistemas escaláveis, componentes e casos de estudo
3. **Soft Skills**: Comunicação, liderança, trabalho em equipe e gestão de tempo

## Instruções para o Copilot
Ao sugerir código ou conteúdo para este repositório:
- Priorize clareza e didática nas explicações
- Mantenha consistência com o estilo existente
- Use exemplos práticos relacionados ao mercado de trabalho brasileiro
- Considere o público-alvo: engenheiros de software buscando crescimento para nível sênior
- Ao modificar navegação, verifique que todos os links estão funcionais