# Formato de Saída — Tabelas, Gráficos, Relatórios e Nomenclatura

## Destino dos Arquivos Gerados
- Todo arquivo gerado por análise ou processamento deve ser salvo exclusivamente em `processamento/` (artefatos intermediários) ou `saida/` (resultados finais) — nunca em `entrada/`.

## Conteúdo Esperado em `saida/`
- `analises/` — relatórios de desvio físico-financeiro, causas de atraso, divergências registradas.
- `planilhas/` — planilhas consolidadas (previsto x realizado, saldo físico, saldo financeiro).
- `curvas-s/` — Curva S consolidada e Curva S reprogramada (cenários conservador, moderado, acelerado).
- `relatorios-finais/` — relatório final consolidado do replanejamento.

## Nomenclatura Recomendada
Seguir o mesmo padrão de competência usado em `entrada/` (ver `docs/requirements.md`): `AAAA-MM_tipo-de-saida_descricao.ext`.

Exemplo: `2026-01_curva-s-reprogramada_cenario-moderado.xlsx`

## Requisitos Mínimos de Saída
- Tabelas e planilhas devem separar avanço físico e avanço financeiro (nunca combinados em uma única coluna de "avanço").
- Gráficos de Curva S devem apresentar previsto, realizado e reprogramado (quando houver) na mesma visualização, por cenário.
- O relatório final deve listar explicitamente: divergências encontradas, premissas/inferências assumidas, e dados sinalizados como ausentes ou inconsistentes.
