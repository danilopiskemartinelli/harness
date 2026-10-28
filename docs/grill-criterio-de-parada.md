# Grill: fases e critério de parada

Versão: 0.4 (grill de divergência)
Camada: framework agêntico
Usado por: plugin (níveis 0 a 3), agente code assistant, agente de review
Fonte: `base-framework-harness-plugin.md`

## 1. Objetivo

Definir as fases do grill e quando ele termina. O grill não pode durar sem fim. O grill não pode terminar cedo.

## 2. Definições

- **Comportamento:** o que o sistema faz, visto por quem o usa.
- **Critério de aceite testável:** uma frase que um teste pode provar verdadeira ou falsa.
- **Pergunta de falha:** pergunta sobre o que acontece quando o comportamento falha.
- **Pendência:** dúvida aberta com dono e prazo.
- **Resposta aceita:** resposta com decisão, motivo e o que invalidaria.

## 3. Fases

### Fase 1: entender o objetivo

| Faça | Não faça |
|---|---|
| Registrar o objetivo em uma frase com resultado observável: "O advogado recebe um aviso antes do prazo vencer." | Aceitar objetivo vago: "melhorar a gestão de prazos." |
| Perguntar quem usa e o que muda para essa pessoa. | Perguntar como implementar. Isso vem depois. |

### Fase 2: atacar os comportamentos

| Faça | Não faça |
|---|---|
| Fazer uma pergunta por comportamento. | Juntar três perguntas em uma. |
| Exigir um critério testável: "3 dias úteis antes do prazo". | Aceitar "o aviso deve ser claro". |
| Fazer ao menos uma pergunta de falha por comportamento. | Cobrir só o caminho feliz. |

### Fase 3: fechar as pendências

| Faça | Não faça |
|---|---|
| Registrar dono e prazo. | Registrar "alguém vê depois." |
| Marcar só o comportamento afetado como bloqueado. | Bloquear a spec inteira sem motivo. |

## 4. Regra de parada

O grill termina quando as três condições são verdadeiras:

1. Cada comportamento tem um critério de aceite testável.
2. Cada comportamento tem ao menos uma pergunta de falha respondida, ou virada em pendência.
3. Cada dúvida aberta é uma pendência com dono e prazo.

O grill continua se uma das três é falsa.

## 5. Regras de resposta

| Resposta | O agente |
|---|---|
| Vazia ("siga", "ok") | Recusa. Repete a pergunta. |
| Fluente, mas sem decisão, motivo e invalidação | Recusa. Pede a parte que falta. |
| Completa | Aceita. Registra no documento. |
| "Não sei" | Aceita. Cria pendência com dono e prazo. |

## 6. Efeito da pendência

- A pendência bloqueia **só o comportamento afetado**.
- Os outros comportamentos seguem para teste e implementação.
- O comportamento afetado não passa no portão até a pendência fechar.

## 7. Saída

O documento da spec contém:

- o objetivo em uma frase;
- a lista de comportamentos;
- um critério de aceite testável por comportamento;
- as respostas aceitas (decisão, motivo, invalidação);
- a lista de pendências (dono, prazo).

## 8. Comportamento por nível

| Nível | Grill |
|---|---|
| 0 | Pergunta só sobre comportamento visível. Sem debate. |
| 1 | Pergunta e espera a resposta. Aponta a lacuna depois. Sem debate. |
| 2 e 3 | Curto e adversarial. Debate desvio, depois segue. |

A regra de parada é a mesma para todos os níveis.

## 9. Grill na revisão

Na revisão, o agente pergunta ao **revisor**. O revisor é quem aprova.

Regra do "não sei": se o revisor responde "não sei", a pergunta vira pendência **para o autor**. A lacuna volta a quem pode fechá-la.

Registro obrigatório: o revisor escreve no documento de aprovação o que verificou e o que deixou de fora.

| Faça | Não faça |
|---|---|
| Perguntar ao revisor. | Repetir ao autor as perguntas da descoberta. |
| Exigir que o revisor escreva o que verificou e o que deixou de fora. | Aceitar "revisei, ok". |
| Atacar só o que costuma escapar: borda, impacto em outro módulo, documento desatualizado. | Reabrir decisões que o autor já justificou. |
| Transformar "não sei" em pendência para o autor. | Deixar o "não sei" do revisor sem dono. |

Exemplo: um sênior revisa a spec do júnior sobre o aviso de prazo.

| Pergunta | Resposta | Resultado |
|---|---|---|
| Existe teste para um prazo que cai na segunda-feira? | "Sim, o teste 4." | Aceita. |
| Qual dado o teste 4 usa? | "Ok." | Recusada. |
| (repetida) | "Dado sintético. Mudaria se o teste precisasse de feriado local." | Aceita. |
| A integração com o e-mail tem teste? | "Não sei." | Pendência para o autor: dono o júnior, prazo sexta. |

Registro do revisor: "Verifiquei os testes 1 a 4. Não verifiquei a integração com o e-mail."

## 10. Grill de divergência (níveis 2 e 3)

O plugin debate o desvio e depois segue. Ele não bloqueia.

Regras:

- O plugin pergunta o risco e o escopo antes de aceitar o desvio.
- A resposta tem decisão, motivo e o que invalidaria.
- Se o desvio contradiz uma decisão registrada, o plugin cita essa decisão.
- O plugin registra a decisão no documento.
- "Urgente" é aceito. A resposta deve dizer **o que foi pulado** e **quando será recuperado**.
- O motivo "urgente" abre uma **pendência de recuperação** com dono e prazo.

| Faça | Não faça |
|---|---|
| Perguntar o risco e o escopo antes de aceitar o desvio. | Bloquear o desvio. |
| Exigir decisão, motivo e o que invalidaria. | Aceitar "é urgente" como motivo completo. |
| Registrar a decisão no documento. | Seguir sem registro. |
| Citar a decisão anterior quando o desvio a contradiz. | Debater como se o sênior não conhecesse o padrão. |
| Abrir pendência de recuperação para o passo pulado. | Deixar o passo pulado sem dono e prazo. |

Exemplo 1: desvio de baixo risco.

| Pergunta | Resposta | Resultado |
|---|---|---|
| Qual comportamento o ajuste afeta e qual é o risco? | "O texto do aviso. Sem risco de dado." | Aceita. |
| O ajuste muda a regra de contagem? | "Só o texto. Muda se alguém mexer no cálculo junto." | Aceita. |
| (plugin) | Registra: descoberta pulada neste ajuste. Pendência de recuperação: dono o sênior, prazo definido. Segue. | Registrado. |

Exemplo 2: desvio que contradiz uma decisão.

| Pergunta | Resposta | Resultado |
|---|---|---|
| (sênior) "Quero mudar a contagem para dias corridos. Sem grill." | | |
| A contagem em dias úteis é uma decisão registrada. Qual motivo invalida essa decisão? | A resposta precisa trazer decisão, motivo e o que invalidaria. | O plugin espera a resposta. |

## 11. Exemplo (descoberta)

Funcionalidade: avisar o advogado quando um prazo está perto de vencer.
Nível: 1. Uso: descoberta.

| Fase | Pergunta | Resposta | Resultado |
|---|---|---|---|
| 1 | Que problema isso resolve? | "Advogados perdem prazo por esquecimento. O aviso evita perder." | Aceita. Objetivo registrado. |
| 2 | Quando o aviso chega? | "3 dias antes." | Aceita. Comportamento 1. |
| 2 | Dias corridos ou úteis? | "Siga." | Recusada. |
| 2 | (repetida) | "Dias úteis. Prazo processual conta só dia útil. Muda se o tribunal contar de outra forma." | Aceita. Comportamento 2. |
| 2 | Se o e-mail não for entregue? | "Tenta de novo em 1 hora. Falhando duas vezes, avisa o líder. Muda se o líder não for o responsável pelo prazo." | Aceita. Falha do comportamento 1. |
| 2 | Se o prazo não tem data? | "Não envia aviso. Mostra erro ao cadastrar. Muda se o tribunal publicar prazo sem data." | Aceita. Falha do comportamento 2. |
| 3 | Feriado local conta como dia útil? | "Não sei." | Pendência: dono Maria, prazo sexta. |

Verificação:

| Comportamento | Critério testável | Pergunta de falha | Situação |
|---|---|---|---|
| 1. Aviso 3 dias antes | Sim | Sim | Pronto |
| 2. Contagem em dias úteis | Sim | Sim | Pronto |
| 3. Feriado local | Não | Não | Pendência, dono Maria |

Resultado: o grill termina. Os comportamentos 1 e 2 seguem. O comportamento 3 espera a Maria.

## 12. O que impede o fim do grill

- Um comportamento sem critério testável. Exemplo: "o aviso deve ser claro".
- Um comportamento sem pergunta de falha.
- Uma dúvida sem dono.
- Uma dúvida sem prazo.

## 13. Revisar no futuro

- Qual é a regra de parada do grill na revisão? A regra atual (seção 4) foi escrita para a descoberta.
- O revisor pode se sentir avaliado pelo agente e responder para agradar? Medir.
- Desvio de nível 2 ou 3: é exceção deste projeto ou proposta de mudar o padrão? O plugin classifica ao fim do grill?
- "Urgente" vira o caminho normal? Medir a taxa de pendências de recuperação abertas e fechadas.
- A pendência deve bloquear a spec inteira em casos de risco alto?
- A pendência vencida deve gerar alerta? Para quem?
- A falha precisa de fase própria se o time achar que ela some na Fase 2?
