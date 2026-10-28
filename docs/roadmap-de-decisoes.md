# Roadmap de decisões

Equipe: Harness Martinelli Dev Team (IA Engineering)
Origem: mapa mental do harness (artefato "Harness Martinelli Dev Team")
Atualizado: 2026-10-27
Documentos ligados: `base-framework-harness-plugin.md`, `grill-criterio-de-parada.md`

## 1. Como usar este documento

- Cada linha é uma decisão. Cada decisão tem um ID fixo.
- Estados: **Decidido**, **Em debate**, **A decidir**.
- Cada decisão tomada entra no registro (seção 4) com decisão, motivo e o que invalidaria.
- Em toda revisão colegiada, percorra o registro. Reabra a decisão se o que a invalidaria aconteceu.
- Debata uma decisão por vez. Traga um exemplo. Registre o Faça e o Não faça.
- Ao decidir, atualize o mapa mental e este documento.

## 2. Ordem

1. **Fundação:** modelo, níveis e grill.
2. **Garantias:** testes, validação, review, documentos, memória.
3. **Plugin:** mecânica por nível e rituais.
4. **Harness:** padrões, infra, skills, MCPs, evals.

Regra de ordem: uma decisão só começa quando as dependências dela estão decididas.
Stacks e padrões ficam na etapa 4. Estão fora do escopo agora.

## 3. Decisões

### Etapa 1: Fundação

| ID | Decisão | Ramo do mapa | Depende de | Estado |
|---|---|---|---|---|
| D01 | Três camadas: framework de desenvolvimento, framework agêntico, harness. | Raiz | - | Decidido |
| D02 | DDD é Document-Driven. SDD é spec. TDD é teste. | Modelo misto | D01 | Decidido |
| D03 | Níveis 0 a 3 e o que o plugin faz em cada um. | Agente de Code Review | D01 | Decidido |
| D04 | Formato de toda resposta de aprovação: decisão, motivo, o que invalidaria. | Padrão Documental | D03 | Decidido |
| D05 | Grill: regra de parada. | Método | D04 | Decidido (v0.1) |
| D06 | Grill: três fases e regra de falha. | Método | D05 | Decidido |
| D07 | Grill na revisão: pergunta ao revisor. | Método | D05 | Decidido |
| D08 | Grill de divergência: debate sem bloqueio. "Urgente" abre pendência de recuperação. | Método | D05 | Decidido |

### Etapa 2: Garantias

| ID | Decisão | Ramo do mapa | Depende de | Estado |
|---|---|---|---|---|
| D09 | Validação em 2 camadas: mecânica e conceitual. A camada 2 prevalece se discordam. | Modelo misto | D02 | Decidido |
| D10 | TDD: testes congelados. Quem escreve, quem aprova, quem pode alterar. | Modelo misto | D09 | **Em debate (próxima)** |
| D11 | Testes de regressão: quando rodam e quem os mantém. | Modelo misto | D10 | A decidir |
| D12 | Agente de review: o que ele recebe, o que ele nunca recebe. | Agente de Code Review | D09, D29 | A decidir |
| D13 | Padrão documental: estrutura, documento de aprovação, como evitar documento velho. | Padrão Documental | D04 | A decidir |
| D14 | Memória coletiva: repositório, efetivação, validade, quem lê o quê. | Devops / Memória | D13 | A decidir |
| D15 | Lista de proibidos: existe bloqueio mecânico para todos os níveis? | Segurança | D03 | A decidir |
| D26 | Linguagem clara (ASD-STE100, meta de 80% menos verbosidade) em documentos, PRs e comentários: regras, medida, quem verifica. | Premissas de qualidade | D09, D13 | Decidido |
| D27 | Código limpo e claro: critérios verificáveis e quem verifica. | Premissas de qualidade | D09 | A decidir |
| D28 | Linguagem clara: valores dos limites mecânicos e lista de palavras de enchimento. | Premissas de qualidade | D26 | A decidir |
| D29 | Isolamento de agentes por função: code assistant, testes, PR e review. Sessão própria, contexto zerado, entrada mínima. O plugin impõe o isolamento. Isonomia: mesmo critério para todos os autores. | Agente de Code Review | D09 | Decidido (conceito) |

### Etapa 3: Plugin

| ID | Decisão | Ramo do mapa | Depende de | Estado |
|---|---|---|---|---|
| D16 | Mecânica por nível: impõe, informa, sugere. Alertas na hora e para a reunião. | Agente de Code Review | D03, D08, D15 | A decidir |
| D17 | Nível 0: ponto de entrada ou perfil permanente. Critério para subir de nível. | Agente de Code Review | D16 | A decidir |
| D18 | Rituais: reuniões ágeis, trocas, revisão colegiada, revisão cega do líder. | Devops / Rotina | D12, D14 | A decidir |
| D19 | Desvio de nível 2 ou 3: exceção do projeto ou proposta de mudar o padrão. | Método | D08, D13 | A decidir |
| D30 | Entrega do plugin: marketplace privado, instalação gerenciada pela organização e teste de viabilidade (spike) do isolamento. | Agente de Code Review | D12, D16 | A decidir |

### Etapa 4: Harness

| ID | Decisão | Ramo do mapa | Depende de | Estado |
|---|---|---|---|---|
| D20 | Padrões: aceitável, desvio com grill, proibido. Stack entra aqui. | Skills e Repos | D15, D19 | A decidir |
| D21 | Skills: uma por função, com dono, versão e critério de entrada. | Skills e Repos | D20 | A decidir |
| D22 | MCPs e bancos de dados: somente leitura, anonimizador no caminho. | MCPS | D15, D20 | A decidir |
| D23 | Infra: Coolify, isolamento, segurança, controle de memória, HD e swap, imagens fantasmas do Docker. | Infra | D15, D20 | A decidir |
| D24 | Devops: rotina e cards. | Devops | D18 | A decidir |
| D25 | Evals: testes pré-estabelecidos (binário e qualitativo) para medir o harness. | Treinamento de Modelos | D11, D21 | A decidir |

## 4. Registro de decisões

Formato fixo: decisão, motivo, o que invalidaria. A coluna "O que invalidaria" é rascunho. A equipe confirma na revisão.

| ID | Decisão | Motivo | O que invalidaria (rascunho) |
|---|---|---|---|
| D01 | Três camadas separadas. | Separar método de ferramenta. Trocar uma ferramenta não muda o método. | Se as camadas mudarem sempre juntas. |
| D02 | DDD é Document-Driven. | Documento é a memória do projeto. O agente começa lendo e termina atualizando. | Se o documento envelhecer mais rápido do que o time o atualiza. |
| D03 | Níveis 0 a 3. Plugin impõe (0), informa (1), sugere (2 e 3). | A estrutura sai do plugin e vai para a pessoa conforme o nível sobe. | Se a taxa de desvio por ponto do padrão for alta em todos os níveis. |
| D04 | Resposta de aprovação com três partes. "Não sei" vira pendência. | Resposta vazia ou "siga" não prova entendimento. | Se respostas com o formato correto passarem com erro de conteúdo. |
| D05 | Grill termina com critério testável, pergunta de falha e pendências com dono. | Grill sem critério dura sem fim ou termina cedo. | Se lacunas passarem mesmo com a regra cumprida. |
| D06 | Três fases: objetivo, comportamentos, pendências. Falha dentro da Fase 2. | Uma pergunta de falha por comportamento evita cobrir só o caminho feliz. | Se a falha sumir na prática. Então, crie fase própria. |
| D07 | Na revisão, o agente pergunta ao revisor. "Não sei" vira pendência para o autor. | O revisor é quem aprova. A lacuna volta a quem pode fechá-la. | Se o revisor responder para agradar o agente. |
| D08 | Desvio de nível 2 ou 3: debate e segue. "Urgente" abre pendência de recuperação. | Bloquear faz o sênior desligar o plugin. Aceitar sem registro faz o desvio virar norma. | Se a taxa de pendências de recuperação abertas e não fechadas subir. |
| D09 | Duas camadas de validação. Camada 1 mecânica (máquina). Camada 2 conceitual (agente de review e humano). Camada 1 roda antes. A camada 2 prevalece. | Teste errado passa sem esforço. Passar nos testes não prova que a spec está certa. | Se a camada 2 recusar com frequência sem critério claro. |
| D26 | O 80% é meta de reescrita. A camada 1 verifica limites mecânicos (tamanho da frase, lista de enchimento). O corte nunca remove decisão, motivo ou o que invalidaria. | O 80% só se mede contra um texto verboso. Em documento novo não há comparação. Corte forçado pode apagar o motivo. | Se os limites mecânicos aprovarem texto confuso ou barrarem texto claro. |
| D29 | Agentes isolados por função (code assistant, testes, PR, review). Cada um em sessão própria, com contexto zerado e entrada mínima. Nenhum recebe o raciocínio de outro. O plugin impõe o isolamento. Isonomia: o review aplica o mesmo critério a todos os autores. | Quem escreve não revisa. O agente que escreve o teste, a descrição ou o parecer não herda o viés de quem implementou. O isolamento imposto pelo plugin não depende da disciplina das pessoas. | Se o custo de sessões separadas superar o ganho medido em erros evitados. |

## 5. Próxima decisão: D10

TDD: testes congelados.

Perguntas para o debate:

1. Quem escreve os testes?
2. Quem aprova os testes?
3. O que significa "congelado"?
4. Quem pode alterar um teste congelado, e como?
5. O que o plugin faz em cada nível quando um teste congelado muda?

Decidido até agora em D10:

- Quem aprova o teste congelado: **níveis 2 e 3**. Quem escreve o teste não o aprova.
- Quem escreve o teste: **agente de testes** com contexto zerado, em sessão própria (D29). Uma pessoa escreve só se o agente não consegue, e o teste segue o mesmo caminho de aprovação.
- Mudança de teste congelado, dois caminhos:
  - A spec **não muda**: o nível 2 ou 3 corrige o teste direto. Ele registra decisão, motivo e o que invalidaria.
  - A spec **muda**: o pedido volta ao grill. O novo teste é aprovado por nível 2 ou 3 e congelado de novo.
- Níveis 0 e 1 só abrem o pedido de mudança. Eles não editam o teste.

Proposto, ainda sem confirmação:

- Níveis 0 e 1: o agente não edita teste congelado. Níveis 2 e 3: alerta na hora e registro para a reunião.

Decidido até agora em D12 (princípios de D29):

- O agente de PR escreve a descrição e os comentários só a partir do diff e da spec.
- O agente de review **não** recebe a descrição do PR.
- Isonomia: o agente de review aplica o mesmo critério a todos os autores.
- O plugin impõe o isolamento. Ele não depende da disciplina das pessoas.
- Quem desenvolve não trabalha para o validador.
- O agente de review usa um modelo diferente do code assistant.

Proposto em D12, ainda sem confirmação:

- O agente de review não recebe o autor nem o nível dele.
- Só a revisão iniciada pelo plugin vale no portão. Revisão manual não conta.
- O code assistant recebe o contrato (spec e testes). Ele não recebe os critérios internos do review.

Teste de viabilidade (spike) proposto para D30:

1. A entrada do review é montada por script do plugin, não pelo prompt do code assistant.
2. O modelo de cada agente vale mesmo se alguém definir a variável de ambiente de modelo global.
3. O plugin sabe o nível da pessoa ou do projeto.
4. O portão sabe que a revisão veio do plugin.

## 6. Teste de cada decisão

Regra: toda decisão com imposição ganha testes antes de entrar no plugin.

1. Casos na suíte `evals/` do plugin (automático, `claude plugin eval`).
2. Um roteiro no projeto de teste (manual, conversa completa).
3. Uma linha no registro de testes, com versão do plugin e resultado.

A versão do plugin só sobe com a suíte aprovada. Falha vira entrada no Learning. Depois, a equipe decide: corrige o plugin ou revisa a decisão.

Testes da v0.1.0:

| Decisão | Casos automáticos (evals) | Roteiros manuais |
|---|---|---|
| D03 | d03-nivel1-nao-debate-desvio, d03-nivel0-so-comportamento-visivel | R02 |
| D04 | d04-recusa-resposta-vazia, d04-resposta-sem-motivo, d04-nao-sei-vira-pendencia | R01, R06 |
| D05 | d05-recusa-criterio-nao-testavel | R01, R07 |
| D06 | d06-recusa-objetivo-vago, d06-exige-pergunta-de-falha | R01 |
| D07 | d07-revisao-recusa-revisei-ok, d07-nao-sei-do-revisor-vai-ao-autor | R03 |
| D08 | d08-urgente-exige-o-que-foi-pulado, d08-urgente-completo-abre-pendencia | R04, R05 |
