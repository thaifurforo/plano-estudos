# Configuração do GitHub Pages

## ⚠️ Configuração Necessária no Repositório

Para que os workflows de deploy funcionem corretamente, é necessário configurar o GitHub Pages nas configurações do repositório.

### Passo a Passo

1. **Acesse as configurações do repositório:**
   - Vá para https://github.com/thaifurforo/plano-estudos/settings/pages

2. **Configure a fonte de deploy:**
   - Em **"Build and deployment"** → **"Source"**
   - Selecione: **"Deploy from a branch"**
   
3. **Selecione a branch gh-pages:**
   - Em **"Branch"**
   - Selecione: **`gh-pages`**
   - Selecione: **`/ (root)`**
   - Clique em **"Save"**

### Como Funciona

#### Deploy Principal (Main Branch)
- **Trigger**: Push para `main` ou merge de PR
- **Workflow**: `.github/workflows/deploy-docs.yml`
- **Destino**: Raiz do GitHub Pages
- **URL**: https://thaifurforo.github.io/plano-estudos/

Quando você faz push ou merge na branch `main`:
1. O workflow builda o site com MkDocs
2. Faz checkout da branch `gh-pages`
3. Preserva o diretório `preview/` (se existir)
4. Substitui todo o conteúdo da raiz com o novo build
5. Faz push para `gh-pages`
6. GitHub Pages automaticamente publica o site

#### Deploy de Preview (Pull Requests)
- **Trigger**: Abertura, atualização ou fechamento de PR
- **Workflow**: `.github/workflows/preview-deploy.yml`
- **Destino**: `/preview/<nome-da-branch>/`
- **URL**: https://thaifurforo.github.io/plano-estudos/preview/<nome-da-branch>/

Quando você abre ou atualiza um PR:
1. O workflow builda o site com MkDocs configurado para o caminho de preview
2. Faz checkout da branch `gh-pages`
3. Cria/atualiza o diretório `preview/<nome-da-branch>/`
4. Faz push para `gh-pages`
5. Comenta no PR com o link do preview

Quando você fecha ou mergea o PR:
1. O workflow de cleanup remove o diretório `preview/<nome-da-branch>/`
2. Comenta no PR confirmando a limpeza

### Estrutura da Branch gh-pages

```
gh-pages/
├── .nojekyll           # Impede que GitHub Pages use Jekyll
├── index.html          # Site principal (da branch main)
├── assets/
├── leetcode/
├── system-design/
├── soft-skills/
└── preview/            # Previews de PRs
    ├── feature-xyz/    # Preview do PR da branch feature-xyz
    ├── bugfix-123/     # Preview do PR da branch bugfix-123
    └── ...
```

### Verificação

Após configurar, você pode verificar se está funcionando:

1. **Verifique se a branch gh-pages existe:**
   ```bash
   git fetch origin
   git branch -r | grep gh-pages
   ```

2. **Faça um commit na main para trigger do deploy:**
   - O workflow deve executar automaticamente
   - Verifique em: https://github.com/thaifurforo/plano-estudos/actions

3. **Acesse o site após alguns minutos:**
   - URL principal: https://thaifurforo.github.io/plano-estudos/

4. **Crie um PR de teste:**
   - Abra um PR de qualquer branch
   - O workflow deve comentar com o link de preview
   - URL: https://thaifurforo.github.io/plano-estudos/preview/<nome-da-branch>/

### Troubleshooting

#### Erro: "Pages build and deployment"
- **Problema**: GitHub Pages está tentando buildar como Jekyll
- **Solução**: O arquivo `.nojekyll` deve estar presente na raiz da branch gh-pages
  - Os workflows já criam este arquivo automaticamente

#### Site mostra 404
- **Causas possíveis**:
  1. GitHub Pages não está configurado corretamente (veja Passo a Passo acima)
  2. A branch gh-pages ainda não foi criada pelo primeiro deploy
  3. O deploy está em andamento (aguarde alguns minutos)
  
- **Soluções**:
  1. Verifique a configuração em Settings → Pages
  2. Faça um push na main para trigger o primeiro deploy
  3. Aguarde até 10 minutos para propagação

#### Preview não funciona
- **Problema**: Link de preview retorna 404
- **Causas possíveis**:
  1. O workflow ainda não terminou de executar
  2. O arquivo `.nojekyll` está faltando
  3. O caminho do `site_url` no MkDocs não foi configurado corretamente
  
- **Soluções**:
  1. Verifique os logs do workflow em Actions
  2. Verifique se `.nojekyll` existe na branch gh-pages
  3. O workflow configura automaticamente o `site_url` - não precisa alterar manualmente

#### Conflitos na branch gh-pages
- **Problema**: Push falha com conflito
- **Causa**: Múltiplos workflows tentando fazer push simultaneamente
- **Solução**: O workflow já usa `--force-with-lease` para lidar com isso
  - Se ainda houver problemas, aguarde o workflow anterior terminar

### Permissões Necessárias

Os workflows já estão configurados com as permissões corretas:

```yaml
permissions:
  contents: write      # Necessário para push na branch gh-pages
  pages: write         # Necessário para GitHub Pages
  id-token: write      # Necessário para autenticação
  pull-requests: write # Necessário para comentar em PRs (preview)
```

### Segurança

Os workflows implementam várias medidas de segurança:

1. **Sanitização de nomes de branches**: Previne command injection
2. **Validação de inputs**: Todos os inputs são validados antes de uso
3. **Uso de environment variables**: Evita injeção de código
4. **Force-with-lease**: Previne sobrescrita acidental
5. **Quoted expansions**: Protege contra word splitting

### Contato

Se encontrar problemas não listados aqui, abra uma issue em:
https://github.com/thaifurforo/plano-estudos/issues
