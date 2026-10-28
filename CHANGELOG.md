# Changelog

Formato: versão, data, decisões do roadmap (`docs/roadmap-de-decisoes.md`).

## harness-dev-team 0.1.0 (2026-10-27)

Decisões: D03, D04, D05, D06, D07, D08.

- Skill `grill` com 3 modos: descoberta, revisão, desvio.
- Resposta de aprovação com 3 partes: decisão, motivo, o que invalidaria.
- "Não sei" vira pendência com dono e prazo.
- Regra de parada com 3 condições (critério testável, pergunta de falha, pendências com dono).
- Comportamento por nível (0 a 3).
- Suíte `evals/` com 12 casos.

Limitações conhecidas:

- O nível vem de `.harness/nivel` ou da própria pessoa. Regra provisória (D30).
- Sem agentes isolados e sem hooks. Eles entram nas versões 0.2.0 e 0.3.0.
- A suíte de evals tem turno único. Conversas completas são testadas por roteiro manual.
