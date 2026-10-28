# Base: Framework, Harness e Plugin

Equipe: Harness Martinelli Dev Team (IA Engineering)
Status: base aprovada. Stacks e padrões ficam fora do escopo por enquanto.

## 1. Escopo atual

1. As três camadas de definição.
2. O processo de grill.
3. O comportamento do plugin.

## 2. Modelo de desenvolvimento

- **DDD (Document-Driven Development):** os documentos são a memória do projeto. Se não está no documento, não existe.
- **SDD (Spec-Driven Development):** a spec diz o que construir.
- **TDD (Test-Driven Development):** o teste prova que a spec foi cumprida.
- **Testes de regressão:** provam que o que já funcionava continua funcionando.
- **Validação em 2 camadas:** camada 1 mecânica (máquina) e camada 2 conceitual (agente de review e humano). A camada 1 roda antes. A camada 2 prevalece se discordam.

## 3. As três camadas

| Camada | Definição | Cobre |
|---|---|---|
| Framework de desenvolvimento | Como pensamos e provamos. | Documentos, specs, testes |
| Framework agêntico | Quem faz o quê. | Liberdade do agente, portões |
| Harness | Em que o agente roda e com o quê. | Ferramentas, memória, isolamento |

## 4. Níveis

| Nível | Perfil | Plugin |
|---|---|---|
| 0 | Vibe coder. Programa sem conhecer estrutura, lógica ou algoritmo. | Impõe estrutura. Sem debate. |
| 1 | Dev júnior. | Informa o padrão. Sem debate. |
| 2 | Dev sênior. | Sugere quando há desvio. Espera o desvio vindo dele. |
| 3 | Líder do time. Também lê código de outros. | Sugere quando há desvio. Espera o desvio vindo dele. |

Desvio nos níveis 2 e 3: o plugin questiona, debate e faz o grill. Depois da resposta, ele segue. Ele não bloqueia.

## 5. Grill

- Dois usos: **descoberta** (antes da spec) e **revisão** (no portão).
- Na descoberta, o agente pergunta ao autor. Na revisão, pergunta ao revisor.
- Para o sênior: protege contra desatenção.
- Para o júnior: ajuda a construir.
- Toda resposta de aprovação é **conceitual**. Resposta vazia ou "siga" é recusada.

Formato de toda resposta de aprovação:

1. **Decisão:** o que foi decidido.
2. **Motivo:** por que.
3. **O que invalidaria:** quando a decisão mudaria.

"Não sei" é permitido. Vira pendência com dono.

Critério de parada: ver `grill-criterio-de-parada.md` (versão 0.4: fases, falha, grill na revisão, grill de divergência).

## 6. Revisão

- A revisão é por nível.
- O revisor escreve no documento de aprovação.
- Níveis 2 e 3: revisão do time em reuniões ágeis ou trocas.
- Níveis 2 e 3: sem hook impeditivo.
- Alertas do plugin: registrados para a reunião **e** visíveis na hora.

## 7. Agentes e memória

- **Agente code assistant:** implementa.
- **Agente de review:** contexto zerado. Sem memória do projeto.
- **Agente de testes:** escreve os testes a partir da spec. Contexto zerado.
- **Agente de PR:** escreve a descrição e os comentários do PR. Contexto zerado.
- Cada agente roda em sessão própria. Nenhum recebe o raciocínio de outro (decisão D29).
- O plugin impõe o isolamento. Ele não depende da disciplina das pessoas.
- Isonomia: o agente de review aplica o mesmo critério a todos os autores. O agente de review não recebe a descrição do PR.
- Os dois geram memórias no sistema atual.
- Hook online de memória coletiva.
- Toda memória coletiva nasce em um **repositório de memórias**.
- Uma pessoa **efetiva** a memória para ela ser válida.
- **Agente revisor de memórias:** só para os níveis 2 e 3.
- Revisões colegiadas de memórias e de documentos do projeto.

## 8. Premissas de qualidade

- Documentos, PRs e comentários usam linguagem clara. Padrão: ASD-STE100. O 80% menos verbosidade é meta de reescrita. A camada 1 verifica limites mecânicos. O corte nunca remove decisão, motivo ou o que invalidaria.
- O código é limpo e claro.
- Uma premissa não precisa de debate de valor. Precisa de definição verificável (decisões D26 e D27 no roadmap).

## 9. Em aberto

- Desvio de nível 2 ou 3: exceção pontual ou proposta de mudança do padrão?
- O code assistant lê todas as memórias coletivas ou só as efetivadas?
- Nível 0: ponto de entrada ou perfil permanente?
- Existe uma lista de proibidos sem exceção, com bloqueio mecânico?
- Quem impede o documento de ficar desatualizado?
- Grill: a regra de parada vale igual para descoberta e revisão? (ver seção 13 do documento do grill)

## 10. Roadmap de decisões

Ver `roadmap-de-decisoes.md`. Ele lista as decisões, a ordem e o estado. Ele guia as revisões futuras.

## 11. Próximas etapas

- Debater cada ponto sobre este documento.
- Depois: definir os padrões, com documentos de aceitável e não aceitável.
