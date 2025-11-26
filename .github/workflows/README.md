# GitHub Actions Workflows

Este diretório contém os workflows do GitHub Actions para deploy e preview do site MkDocs.

## Workflows Disponíveis

### 1. Deploy MkDocs to GitHub Pages (`deploy-docs.yml`)

**Trigger**: 
- Push para a branch `main`
- Pull Request mergeado para `main`
- Execução manual (workflow_dispatch)

**Função**:
- Faz o build do site MkDocs
- Faz o deploy para o GitHub Pages na raiz do site
- Preserva o diretório `preview/` que contém os previews de PRs

**URL Final**: `https://thaifurforo.github.io/plano-estudos/`

### 2. Preview Deploy (`preview-deploy.yml`)

**Trigger**:
- Abertura de Pull Request para `main`
- Atualização de Pull Request (novos commits)
- Reabertura de Pull Request
- Fechamento de Pull Request

**Função**:

#### Quando PR é aberto/atualizado:
- Faz o build do site MkDocs com configuração específica para preview
- Cria uma pasta de preview em `gh-pages` branch: `preview/<nome-da-branch>/`
- Adiciona um comentário no PR com a URL do preview
- Atualiza o comentário se já existir

#### Quando PR é fechado/mergeado:
- Remove a pasta de preview correspondente
- Adiciona um comentário no PR confirmando a limpeza

**URL do Preview**: `https://thaifurforo.github.io/plano-estudos/preview/<nome-da-branch>/`

## Como Funciona

### Estrutura do GitHub Pages

```
gh-pages branch
├── index.html              (site principal - branch main)
├── assets/
├── leetcode/
├── system-design/
├── soft-skills/
└── preview/                (previews de PRs)
    ├── feature-branch-1/   (preview da feature-branch-1)
    ├── bugfix-issue-123/   (preview da bugfix-issue-123)
    └── ...
```

### Fluxo de Trabalho

1. **Desenvolvendo em uma branch**:
   - Crie uma branch a partir de `main`
   - Faça suas alterações
   - Abra um Pull Request para `main`
   - O workflow `preview-deploy.yml` será executado automaticamente
   - Um comentário será adicionado ao PR com o link do preview

2. **Atualizando o PR**:
   - Faça novos commits na branch
   - O preview será atualizado automaticamente
   - O comentário no PR será atualizado com a mesma URL

3. **Mergeando o PR**:
   - Ao fazer merge para `main`:
     - O workflow `preview-deploy.yml` remove o preview
     - O workflow `deploy-docs.yml` faz deploy do site principal
   - O site principal será atualizado com as alterações

4. **Fechando PR sem merge**:
   - O preview será removido automaticamente
   - Um comentário confirmará a limpeza

## ⚠️ Configuração Necessária no Repositório

### Passo 1: Permissões do GitHub Actions

O repositório precisa ter as seguintes configurações:

1. **Settings > Actions > General**:
   - Workflow permissions: "Read and write permissions"
   - Allow GitHub Actions to create and approve pull requests: ✓

### Passo 2: Configurar GitHub Pages (CRÍTICO)

**Esta é a configuração mais importante!** Sem ela, os deploys não funcionarão.

1. Acesse: **Settings > Pages**
2. Em **"Build and deployment"**:
   - **Source**: Selecione **"Deploy from a branch"**
   - **Branch**: Selecione **`gh-pages`** e **`/ (root)`**
   - Clique em **"Save"**

### Secrets Necessários

Nenhum secret adicional é necessário. Os workflows usam o `GITHUB_TOKEN` padrão.

### Verificação

Após configurar:
1. Faça um push na branch `main`
2. O workflow deve executar e criar/atualizar a branch `gh-pages`
3. Após alguns minutos, o site deve estar disponível em:
   - https://thaifurforo.github.io/plano-estudos/

📖 **Para instruções detalhadas, veja:** [GITHUB_PAGES_SETUP.md](../../GITHUB_PAGES_SETUP.md)

## Testando Localmente

Para testar o build antes de fazer push:

```bash
# Instalar dependências
pip install -r requirements.txt

# Build local
mkdocs build

# Servidor local
mkdocs serve
```

## Troubleshooting

### Preview não está acessível

1. Verifique se o workflow foi executado com sucesso
2. Verifique se o GitHub Pages está habilitado
3. Aguarde alguns minutos - o GitHub Pages pode levar até 10 minutos para atualizar

### Preview não foi removido

1. Verifique os logs do workflow `cleanup-preview`
2. Execute manualmente: vá para Actions > Preview Deploy > Run workflow

### Site principal não atualizou

1. Verifique se o push foi para a branch `main`
2. Verifique os logs do workflow `deploy-docs.yml`
3. Limpe o cache do navegador

## Manutenção

### Limpeza Manual de Previews

Se necessário limpar previews manualmente:

```bash
# Clone o repositório
git clone https://github.com/thaifurforo/plano-estudos.git
cd plano-estudos

# Checkout gh-pages
git checkout gh-pages

# Remover preview específico
rm -rf preview/<nome-da-branch>

# Commit e push
git add preview
git commit -m "Remove preview for <nome-da-branch>"
git push origin gh-pages
```

### Atualizar Workflows

Ao modificar os workflows:
1. Teste em uma branch separada
2. Verifique os logs de execução
3. Faça merge apenas após confirmar funcionamento
