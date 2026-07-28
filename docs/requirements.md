# Requisitos Gerais da Plataforma

Este documento é o contrato geral de requisitos da plataforma. O detalhamento técnico de cada etapa está modularizado em `docs/metodologia/`:

- Curva S (fórmulas físicas e financeiras) → `docs/metodologia/curva-s.md`
- Replanejamento (tarefas, dependências, cenários) → `docs/metodologia/replanejamento.md`
- Recursos (mão de obra, materiais, equipamentos) → `docs/metodologia/recursos.md`
- Desembolsos (saldo financeiro, redistribuição mensal) → `docs/metodologia/desembolsos.md`
- Validações (fechamento, orçamento, inconsistências) → `docs/metodologia/validacoes.md`
- Formato de saída (tabelas, gráficos, relatórios) → `docs/metodologia/formato-de-saida.md`

## Requisitos Funcionais

- Leitura de múltiplos relatórios mensais.
- Organização dos documentos por competência (mês/ano).
- Identificação do último mês consolidado.
- Consolidação do avanço físico previsto e realizado.
- Consolidação do avanço financeiro previsto e realizado.
- Cálculo do desvio físico em pontos percentuais.
- Cálculo do atraso relativo.
- Cálculo do saldo físico da obra.
- Cálculo do saldo financeiro.
- Identificação das atividades atrasadas.
- Análise das causas dos desvios.
- Respeito às predecessoras e dependências técnicas.
- Redistribuição das tarefas pendentes.
- Redistribuição de mão de obra, materiais e equipamentos.
- Redistribuição dos desembolsos.
- Criação da Curva S reprogramada.
- Criação dos cenários conservador, moderado e acelerado.
- Preservação integral dos meses já realizados.
- Fechamento do avanço físico final em exatamente 100%.
- Compatibilidade do financeiro final com o orçamento vigente.
- Sinalização de dados ausentes, divergentes ou inconsistentes.
- Geração de tabelas, planilhas, gráficos e relatório final.

## Regras de Negócio Críticas

- Percentuais acumulados não devem ser somados.
- Avanço físico e avanço financeiro devem ser analisados separadamente.
- Desembolso menor não deve ser classificado automaticamente como economia.
- Uma atividade pode ter peso físico diferente do seu peso financeiro.
- O replanejamento deve começar no valor real acumulado do último mês consolidado.
- Não alterar retroativamente os resultados dos meses encerrados.
- Não concentrar artificialmente todo o saldo no último mês.
- Avaliar a produtividade histórica antes de afirmar que o prazo original pode ser mantido.
- Quando o prazo for inviável, propor nova previsão de término.
- Toda inferência deve ser identificada claramente.

## Padrão de Nomenclatura dos Arquivos de Entrada

Todos os documentos em `entrada/` devem seguir o padrão `AAAA-MM_tipo_descricao.ext`.

Exemplos:
- `2026-01_relatorio-mensal.pdf`
- `2026-01_cronograma-fisico-financeiro.xlsx`
- `2026-01_medicao.xlsx`
- `2026-01_ata-reuniao.pdf`

Quando houver revisão do mesmo documento: `AAAA-MM_tipo_descricao_rev01.ext`.

Ao identificar arquivos com o mesmo `AAAA-MM_tipo_descricao` em revisões diferentes, a revisão mais alta deve ser considerada a válida, e o arquivo efetivamente utilizado deve ser informado explicitamente na análise (ver `docs/metodologia/validacoes.md`).

## Integrações Externas
- [PREENCHER: ex. fontes de planilhas, sistemas de gestão de obras]

## Validações Obrigatórias
- Nenhum dado de uma obra pode ser referenciado ou processado junto com o de outra obra.
- Nenhum documento confidencial de cliente pode ser versionado (ver `.gitignore`).
- Ver também `docs/metodologia/validacoes.md` para as validações específicas de fechamento e consistência.

*Atualizado sempre que um requisito muda ou é descoberto.*
