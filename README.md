# Martinelli Harness: marketplace de plugins

Marketplace privado do harness de IA Engineering. Ele lista o plugin `harness-dev-team`.

Documentos de referência em `docs/`: base do framework, grill e roadmap de decisões.

## 1. Rodar agora, em pasta local

Dentro desta pasta:

```bash
claude plugin validate .
claude plugin marketplace add ./martinelli-harness-marketplace
claude plugin install harness-dev-team@martinelli-harness
```

Para testar sem instalar, em uma sessão só:

```bash
claude --plugin-dir ./plugins/harness-dev-team
```

Depois de editar um arquivo do plugin, rode `/reload-plugins` na sessão. Na pasta local, a edição vale sem mudar a versão.

## 2. Publicar no GitHub (repositório privado)

```bash
git remote add origin git@github.com:SUA-ORG/martinelli-harness-marketplace.git
git push -u origin main --tags
```

Cada pessoa precisa de acesso de leitura ao repositório e de credencial salva no `git`.

Quem usa registra o marketplace uma vez:

```bash
claude plugin marketplace add SUA-ORG/martinelli-harness-marketplace
claude plugin install harness-dev-team@martinelli-harness
```

Para ativar só em um projeto, rode no projeto: `claude plugin marketplace add SUA-ORG/martinelli-harness-marketplace --scope project` e faça commit do `.claude/settings.json`.

## 3. Ciclo de release

1. Mude o código do plugin.
2. Rode `claude plugin validate .` e `claude plugin eval .` em `plugins/harness-dev-team`.
3. Suba o campo `version` **só** em `plugins/harness-dev-team/.claude-plugin/plugin.json`. Não repita a versão na entrada do marketplace.
4. Adicione a entrada no `CHANGELOG.md`, com os IDs das decisões.
5. Commit, tag e push. Tag: `harness-dev-team--vX.Y.Z`.
6. Quem usa atualiza: `/plugin marketplace update martinelli-harness`, depois `claude plugin update harness-dev-team@martinelli-harness`.

Se você não mudar o `version`, quem usa uma cópia do GitHub não recebe as mudanças. A atualização automática vem desligada. Cada pessoa liga em `/plugin`, na aba Marketplaces. Um administrador também pode ligar nas configurações gerenciadas.

## 4. Testes

Em `plugins/harness-dev-team`:

```bash
claude plugin eval . --ablation none --runs 1 --case d04-recusa-resposta-vazia   # rápido e barato
claude plugin eval . --no-publish --max-cost-usd 10                                # suíte completa
```

Cada caso roda 3 vezes com o plugin e 3 sem ele. A diferença (Δ) mostra o que o plugin acrescenta. Cada execução é uma chamada real de modelo e conta no seu plano. Exige Claude Code v2.1.269 ou mais novo.

O plano completo está no projeto de teste (`docs/plano-de-testes.md`).

## 5. Para a organização inteira

Fica para a decisão D30. Há duas rotas na documentação oficial: configurações gerenciadas (`extraKnownMarketplaces` e `enabledPlugins`) e **Organization settings > Plugins & skills** no claude.ai, nos planos Team e Enterprise. A segunda lê um repositório privado pela conexão da organização com o GitHub.
