# Desembolsos — Saldo Financeiro, Contratos, Compras e Medições

## Escopo
- Saldo financeiro remanescente: Orçamento vigente − Desembolso acumulado realizado.
- Base de referência: contratos, medições e compras registrados em `entrada/contratos/`, `entrada/medicoes/` e `entrada/orcamentos/`.

## Regras
- Desembolso menor que o previsto não deve ser classificado automaticamente como economia — verificar se corresponde a atraso físico equivalente antes de qualquer conclusão.
- O financeiro final do replanejamento deve ser compatível com o orçamento vigente da obra (ver `validacoes.md`).
- A nova distribuição mensal dos desembolsos deve acompanhar a curva física reprogramada (`curva-s.md`) e a redistribuição de tarefas (`replanejamento.md`) — não deve ser definida isoladamente.
- Não concentrar artificialmente todo o desembolso remanescente no último mês.
