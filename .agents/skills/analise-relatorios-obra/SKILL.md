---
name: analise-relatorios-obra
description: >
  Use esta skill sempre que o usuário pedir para analisar relatórios mensais de obra,
  consolidar avanço físico-financeiro, comparar previsto e realizado, identificar desvios
  da Curva S, diagnosticar atrasos, ou elaborar um replanejamento de tarefas, recursos ou
  desembolsos de uma obra. Aciona também quando o usuário mencionar "obra ativa", "Curva S",
  "desvio físico", "desvio financeiro", "replanejamento de obra", "cronograma reprogramado",
  "cenário conservador/moderado/acelerado" ou pedir para processar documentos da pasta
  `entrada/` de uma obra em `obras/<nome-da-obra>/`.
---

# Análise e Replanejamento de Relatórios de Obra

## Objetivo
Analisar os documentos oficiais de uma obra, consolidar os dados físico-financeiros mensais, comparar previsto e realizado, identificar desvios da Curva S e elaborar o replanejamento das tarefas, recursos e desembolsos dos meses restantes.

## Fonte Metodológica Obrigatória
Esta skill não duplica a metodologia — ela aponta para os documentos já existentes na raiz da plataforma, que devem ser lidos (carregados) conforme a etapa em execução:

- Contrato geral de requisitos → `docs/requirements.md`
- Fórmulas da Curva S (físico/financeiro) → `docs/metodologia/curva-s.md`
- Redistribuição de tarefas, dependências e cenários → `docs/metodologia/replanejamento.md`
- Mão de obra, materiais, equipamentos → `docs/metodologia/recursos.md`
- Saldo financeiro e redistribuição de desembolsos → `docs/metodologia/desembolsos.md`
- Fechamento, orçamento e inconsistências → `docs/metodologia/validacoes.md`
- Tabelas, gráficos, relatórios e nomenclatura → `docs/metodologia/formato-de-saida.md`

Nunca prosseguir com uma etapa sem ter lido o documento metodológico correspondente.

## Modos de Execução
A skill deve ser executada em um dos quatro modos abaixo. Se o usuário não especificar, o modo padrão é `inventario`.

- **`inventario`** — apenas Inventário dos arquivos e Validação documental (etapas 1 e 2). Não avança para extração sem aprovação.
- **`consolidacao`** — Inventário até Diagnóstico dos desvios (etapas 1 a 5), sem elaborar replanejamento. Pressupõe inventário já aprovado (ou aprovado nesta mesma execução, se solicitado).
- **`replanejamento`** — Análise de produtividade até Geração do relatório final (etapas 6 a 12), partindo de uma consolidação já aprovada pelo usuário. Não reextrai dados por conta própria — usa a consolidação fornecida/aprovada como entrada.
- **`completo`** — executa todas as 12 etapas em sequência. É o único modo em que a skill pode avançar de uma etapa para a seguinte sem que o usuário precise aprovar cada etapa individualmente — mas os três pontos obrigatórios de aprovação (ver seção seguinte) continuam sendo paradas obrigatórias, mesmo no modo `completo`.

Fora do modo `completo`, a skill nunca avança de uma etapa do fluxo de trabalho para a etapa seguinte sem aprovação explícita do usuário.

## Pontos Obrigatórios de Aprovação

### 1. Após o inventário documental
Apresentar e aguardar aprovação antes de prosseguir:
- arquivos encontrados;
- competências identificadas;
- revisões encontradas;
- duplicidades encontradas;
- lacunas (competências ou tipos de documento ausentes);
- fonte candidata da Curva S;
- último mês consolidado identificado.

### 2. Após a extração e consolidação
Apresentar e aguardar aprovação antes de iniciar o replanejamento:
- tabela dos dados extraídos;
- fonte de cada dado (ver "Rastreabilidade Obrigatória");
- divergências encontradas entre relatórios.

### 3. Antes do replanejamento
Confirmar explicitamente com o usuário:
- data de corte da análise;
- orçamento vigente;
- prazo contratual;
- Curva S oficial (fonte);
- último mês fechado;
- aditivos confirmados;
- cenário(s) solicitado(s).

## Rastreabilidade Obrigatória
Todo dado relevante extraído deve registrar, quando possível:
- arquivo de origem;
- competência;
- página do PDF;
- planilha e célula;
- seção ou tabela;
- nível de confiança: alto, médio ou baixo.

Para dados calculados ou derivados, registrar adicionalmente:
- fórmula utilizada;
- valores de entrada;
- origem de cada valor de entrada;
- regra metodológica aplicada;
- resultado do cálculo;
- nível de confiança.

Um valor calculado não precisa existir diretamente em um documento, mas todos os seus dados de origem devem ser rastreáveis.

Nenhum percentual, valor ou data deve aparecer no relatório final sem que sua origem possa ser rastreada.

## Tratamento de Versões e Revisões
Quando houver arquivos `_revNN`:
- considerar a maior revisão somente quando pertencer claramente à mesma família documental (mesma competência e mesmo tipo de documento);
- não descartar automaticamente arquivos anteriores — mantê-los referenciados como histórico;
- registrar explicitamente qual revisão foi usada e por quê;
- quando houver conflito ou dúvida sobre qual revisão é a fonte oficial, perguntar ao usuário antes de escolher.

## Nomenclatura dos Arquivos de Saída
Arquivos gerados em `saida/` (e, quando aplicável, em `processamento/`) devem seguir, quando aplicável:

`AAAA-MM_nome-da-obra_tipo_cenario_revNN.ext`

Exemplos:
- `2026-06_reserva-park_consolidacao_rev01.xlsx`
- `2026-06_reserva-park_curva-s_acelerado_rev01.xlsx`
- `2026-06_reserva-park_relatorio-final_acelerado_rev01.pdf`

## Regras Obrigatórias
1. Antes de qualquer análise, identificar explicitamente a obra ativa. Se não estiver clara, perguntar ao usuário.
2. Trabalhar exclusivamente dentro de `obras/<obra-ativa>/`.
3. Ler primeiro `obras/<obra-ativa>/AGENTS.md` e os documentos em `obras/<obra-ativa>/docs/` antes de iniciar qualquer análise.
4. Nunca utilizar, comparar ou referenciar dados de outra obra.
5. Nunca alterar, renomear, mover ou sobrescrever arquivos existentes em `entrada/`.
6. Organizar os documentos por competência mensal (`AAAA-MM`).
7. Tratar versões e revisões conforme a seção "Tratamento de Versões e Revisões".
8. Consolidar previsto, realizado e acumulado — físico e financeiro, sempre separadamente.
9. Calcular os desvios da Curva S conforme `docs/metodologia/curva-s.md`.
10. Identificar atividades atrasadas, suas dependências técnicas e causas do atraso.
11. Redistribuir apenas o saldo ainda não realizado — nunca alterar meses já encerrados.
12. Redistribuir tarefas, equipes, materiais, equipamentos e desembolsos de forma compatível entre si.
13. Criar os três cenários (conservador, moderado, acelerado) quando a execução envolver replanejamento.
14. Preservar integralmente os meses encerrados.
15. Garantir que a Curva S física reprogramada termine em exatamente 100%.
16. Não inventar dados ausentes (percentuais, valores, datas, produtividades, tarefas, recursos).
17. Sinalizar inconsistências, divergências e dados ausentes antes de elaborar o replanejamento.
18. Registrar a rastreabilidade de todo dado relevante extraído, conforme "Rastreabilidade Obrigatória".
19. Salvar todo arquivo intermediário em `processamento/`.
20. Salvar todo resultado final em `saida/`, seguindo "Nomenclatura dos Arquivos de Saída".
21. Nunca sobrescrever arquivos existentes em `processamento/` ou `saida/`. Antes de gerar um arquivo, verificar se já existe arquivo com o mesmo nome; quando já existir, incrementar automaticamente a revisão (`_rev01`, `_rev02`, `_rev03`, ...). Nunca substituir silenciosamente uma análise, planilha, Curva S ou relatório anterior.
22. Se qualquer documento metodológico obrigatório não existir, estiver vazio ou não puder ser lido, interromper a etapa correspondente, informar exatamente qual arquivo está ausente ou inacessível, e nunca improvisar uma regra metodológica para substituí-lo.
23. Nunca alterar automaticamente `docs/requirements.md`, `docs/metodologia/*.md` ou o `AGENTS.md` da raiz — qualquer mudança na metodologia geral deve ser proposta separadamente e depender de aprovação expressa.
24. Atualizar `obras/<obra-ativa>/docs/roadmap.md` e `obras/<obra-ativa>/docs/state.md` apenas conforme a seção "Atualização de roadmap.md e state.md".

## Etapas do Fluxo de Trabalho
1. **Inventário dos arquivos** — listar tudo o que existe em `entrada/`, organizado por competência e tipo.
2. **Validação documental** — checar nomenclatura, identificar duplicidades/revisões. → **Ponto de aprovação 1.**
3. **Extração dos dados** — extrair previsto/realizado físico e financeiro de cada documento aprovado, com rastreabilidade.
4. **Consolidação histórica** — montar a série mensal acumulada até o último mês consolidado.
5. **Diagnóstico dos desvios** — calcular desvios e saldos conforme `docs/metodologia/curva-s.md`. → **Ponto de aprovação 2.**
6. **Análise da produtividade** — avaliar o ritmo histórico real de execução (`docs/metodologia/replanejamento.md`). → **Ponto de aprovação 3** antes de seguir para o replanejamento.
7. **Replanejamento** — redistribuir tarefas pendentes respeitando dependências (`docs/metodologia/replanejamento.md`).
8. **Redistribuição de recursos** — mão de obra, materiais, equipamentos, frentes simultâneas (`docs/metodologia/recursos.md`).
9. **Redistribuição dos desembolsos** — nova distribuição mensal do saldo financeiro (`docs/metodologia/desembolsos.md`).
10. **Geração da nova Curva S** — curva reprogramada com os cenários solicitados.
11. **Validação dos totais** — fechamento em 100% físico e compatibilidade com o orçamento vigente (`docs/metodologia/validacoes.md`).
12. **Geração do relatório final** — tabelas, planilhas, gráficos e relatório, salvos em `saida/` conforme `docs/metodologia/formato-de-saida.md` e "Nomenclatura dos Arquivos de Saída".

## Estrutura de Pastas Envolvida
Dentro de `obras/<obra-ativa>/`:
- `entrada/` — leitura apenas, nunca escrita.
- `processamento/` — artefatos intermediários gerados durante a análise.
- `saida/` — resultados finais (análises, planilhas, curvas S, relatórios finais).

## Atualização de roadmap.md e state.md
Os arquivos atualizados por esta skill são sempre os da obra ativa, nunca os da raiz:
- `obras/<obra-ativa>/docs/roadmap.md`
- `obras/<obra-ativa>/docs/state.md`

Nunca atualizar por engano os arquivos gerais da plataforma:
- `docs/roadmap.md`
- `docs/state.md`

Regras de atualização:
- Atualizar `obras/<obra-ativa>/docs/roadmap.md` e `obras/<obra-ativa>/docs/state.md` somente após uma etapa efetivamente concluída **e aprovada** pelo usuário, e depois que os arquivos gerados nessa etapa tiverem sido validados.
- Nunca atualizar esses arquivos após uma simples leitura, uma tentativa cancelada ou uma execução incompleta.
- A atualização do `roadmap.md` deve apenas somar ao Consolidado — nunca apagar o histórico já registrado.
- O `state.md` deve refletir o checkpoint real: etapa concluída, arquivos gerados, decisões tomadas e o próximo passo.
