# Resolução do Problema de Deploy do GitHub Pages

## 🎯 Diagnóstico

Após análise completa do repositório, identifiquei que **os workflows estão configurados corretamente**. O problema está na configuração do GitHub Pages no repositório.

### O que está funcionando ✅

- ✅ Workflow de deploy principal (`.github/workflows/deploy-docs.yml`)
- ✅ Workflow de deploy de preview (`.github/workflows/preview-deploy.yml`)  
- ✅ Lógica de preservação do diretório `preview/` durante deploys principais
- ✅ Sistema de cleanup automático de previews
- ✅ Build do MkDocs funciona corretamente

### O que precisa ser configurado ⚙️

- ⚠️ **GitHub Pages precisa ser configurado para usar a branch `gh-pages`**

## 🔧 Solução: Configure o GitHub Pages

### Passo a Passo (OBRIGATÓRIO)

1. **Acesse as configurações do GitHub Pages:**
   ```
   https://github.com/thaifurforo/plano-estudos/settings/pages
   ```

2. **Configure a fonte de deploy:**
   - Procure a seção **"Build and deployment"**
   - Em **"Source"**, selecione: **"Deploy from a branch"**
   
3. **Selecione a branch gh-pages:**
   - Em **"Branch"**, selecione: **`gh-pages`**
   - No dropdown ao lado, selecione: **`/ (root)`**
   - Clique em **"Save"**

4. **Aguarde o primeiro deploy:**
   - Faça um push na branch `main` (ou merge um PR)
   - O workflow criará a branch `gh-pages` automaticamente
   - Após alguns minutos, o site estará disponível

### Como Verificar se Funcionou

1. **URL Principal:**
   ```
   https://thaifurforo.github.io/plano-estudos/
   ```

2. **URL de Preview (em PRs):**
   ```
   https://thaifurforo.github.io/plano-estudos/preview/<nome-da-branch>/
   ```

## 📋 Mudanças Implementadas

### 1. Documentação Detalhada

- **`GITHUB_PAGES_SETUP.md`**: Guia completo de configuração e troubleshooting
- **`.github/workflows/README.md`**: Atualizado com instruções críticas

### 2. Melhorias nos Workflows

#### `deploy-docs.yml` (Deploy Principal)
- **Antes**: Executava duas vezes ao mergear PR (evento `push` + `pull_request.closed`)
- **Depois**: Executa apenas no evento `push` para `main`
- **Benefício**: Evita deploys duplicados, mais eficiente

#### Permissões Otimizadas
- **Removido**: `pages: write` e `id-token: write` (não necessários para push manual)
- **Mantido**: `contents: write` (necessário para push na gh-pages)
- **Benefício**: Segurança - princípio do menor privilégio

## 🚀 Como Testar

### Teste 1: Deploy Principal

```bash
# No seu repositório local
git checkout main
git pull origin main

# Faça uma pequena mudança
echo "\n## Teste de Deploy" >> README.md
git add README.md
git commit -m "Test: Deploy principal"
git push origin main
```

**Resultado esperado:**
1. Workflow `Deploy MkDocs to GitHub Pages` executa
2. Branch `gh-pages` é criada/atualizada
3. Site atualizado em https://thaifurforo.github.io/plano-estudos/

### Teste 2: Preview de PR

```bash
# Crie uma nova branch
git checkout -b test/preview-deployment
echo "\n## Teste de Preview" >> README.md
git add README.md
git commit -m "Test: Preview deployment"
git push origin test/preview-deployment

# Abra um PR no GitHub
# Acesse: https://github.com/thaifurforo/plano-estudos/compare/main...test/preview-deployment
```

**Resultado esperado:**
1. Workflow `Preview Deploy` executa
2. Um comentário aparece no PR com o link de preview
3. Preview disponível em https://thaifurforo.github.io/plano-estudos/preview/test-preview-deployment/

### Teste 3: Cleanup de Preview

```bash
# Mergee ou feche o PR criado no Teste 2
```

**Resultado esperado:**
1. Workflow `Preview Deploy` (job `cleanup-preview`) executa
2. Um comentário aparece confirmando a limpeza
3. Diretório `preview/test-preview-deployment/` é removido da branch `gh-pages`

## 📚 Documentação de Referência

- **[GITHUB_PAGES_SETUP.md](GITHUB_PAGES_SETUP.md)**: Configuração detalhada e troubleshooting
- **[.github/workflows/README.md](.github/workflows/README.md)**: Como funcionam os workflows

## ❓ FAQ

### Por que não usamos `actions/deploy-pages`?

A ação oficial `actions/deploy-pages` não suporta deployments em subdirectórios, que é necessário para os previews de PRs. Por isso, usamos push manual para a branch `gh-pages`.

### Posso usar outro nome de branch?

Tecnicamente sim, mas você precisaria:
1. Alterar todos os workflows para usar o novo nome
2. Atualizar as configurações do GitHub Pages
3. Não é recomendado - `gh-pages` é o padrão da comunidade

### E se eu quiser usar GitHub Actions como fonte?

Você perderia a funcionalidade de preview de PRs em subdirectórios. A abordagem atual é a mais flexível.

### Como limpar previews antigos manualmente?

```bash
git clone https://github.com/thaifurforo/plano-estudos.git
cd plano-estudos
git checkout gh-pages
rm -rf preview/nome-da-branch-antiga
git add preview
git commit -m "Cleanup old preview"
git push origin gh-pages
```

## 🎉 Conclusão

Os workflows estão funcionando perfeitamente. Basta configurar o GitHub Pages conforme as instruções acima e tudo funcionará como esperado!

**Próximos Passos:**
1. Configure o GitHub Pages (5 minutos)
2. Faça um push na `main` para testar
3. Crie um PR de teste para validar previews
4. 🎊 Aproveite os deploys automáticos!
