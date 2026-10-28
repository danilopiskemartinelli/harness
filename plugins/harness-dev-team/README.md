# harness-dev-team

Plugin do harness Martinelli Dev Team. Versão 0.1.0 (experimental).

Esta versão traz o **grill**: perguntas até a spec ter critérios testáveis, com resposta de aprovação conceitual (decisão, motivo, o que invalidaria). Cobre as decisões D03 a D08 do roadmap.

## Uso

Dentro de um projeto com o plugin ativo:

- `/harness-dev-team:grill descoberta <nome>`: grill de descoberta, antes da spec.
- `/harness-dev-team:grill revisao <nome>`: grill de revisão, no portão.
- `/harness-dev-team:grill desvio <nome>`: grill de divergência (níveis 2 e 3).

O nível da pessoa (0 a 3) fica em `.harness/nivel`. Essa regra é provisória (decisão D30).

## Testes

`claude plugin eval .` roda a suíte em `evals/`. Cada decisão com imposição tem casos na suíte. Veja o `README.md` do repositório.
