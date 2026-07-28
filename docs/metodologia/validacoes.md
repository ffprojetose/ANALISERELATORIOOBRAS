# Validações — Fechamento, Orçamento, Datas, Inconsistências e Alertas

## Validações Obrigatórias de Fechamento
- O avanço físico final do replanejamento deve fechar em exatamente 100%.
- O financeiro final deve ser compatível com o orçamento vigente da obra.
- Os meses já realizados/encerrados não podem ser alterados retroativamente.

## Sinalização de Dados
- Dados ausentes, divergentes ou inconsistentes entre relatórios devem ser sinalizados explicitamente antes de qualquer replanejamento — nunca presumidos ou preenchidos automaticamente.
- Não considerar inferências como fatos; toda inferência deve ser identificada claramente como tal no resultado apresentado.
- Não inventar percentuais, valores, datas, produtividades, tarefas ou recursos ausentes.

## Versões e Duplicidade de Arquivos
- Ao encontrar mais de um arquivo de `entrada/` para a mesma competência e tipo (ver padrão de nomenclatura em `docs/requirements.md`), considerar a revisão mais alta (`_revNN`) como válida.
- Informar explicitamente qual arquivo foi considerado quando houver duplicidade ou revisão.

## Divergências entre Relatórios
- Antes de realizar o replanejamento, registrar todas as divergências encontradas entre os relatórios mensais analisados (ex. valores conflitantes entre cronograma e medição para a mesma competência).
