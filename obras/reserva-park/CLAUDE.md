# Reserva Park

[PREENCHER: 1-2 frases de identificação da obra]

## Dados Gerais
- Cliente: [PREENCHER]
- Localização: [PREENCHER]
- Contrato/Nº: [PREENCHER]
- Início: [PREENCHER] | Previsão de término: [PREENCHER]
- Data de corte da análise: [PREENCHER]
- Prazo original: [PREENCHER]
- Orçamento vigente: [PREENCHER]
- Fonte oficial da Curva S: [PREENCHER]
- Último relatório consolidado: [PREENCHER]
- Responsável pela validação dos dados: [PREENCHER]

## Contexto desta Obra
- Visão e propósito → `docs/project.md`
- Requisitos e regras de negócio específicas → `docs/requirements.md`
- Histórico e roadmap desta obra → `docs/roadmap.md`
- Estado da sessão atual → `docs/state.md`

## Estrutura de Dados
- Documentos recebidos → `entrada/` (relatórios mensais, cronogramas, medições, orçamentos, contratos, atas)
- Scripts e artefatos intermediários → `processamento/`
- Resultados gerados → `saida/` (análises, planilhas, curvas S, relatórios finais)

## Regras Absolutas
- Dados desta obra nunca devem ser referenciados junto com os de outra obra.
- Documentos de `entrada/` e resultados de `saida/` não são versionados (ver `.gitignore` da raiz).
- Este arquivo permanece curto (roteador apenas) — detalhes vão para `docs/`.
- Nunca alterar, renomear, mover ou sobrescrever documentos de `entrada/`.
- Todo arquivo gerado deve ser salvo exclusivamente em `processamento/` ou `saida/`.

## Fluxo de Trabalho
1. Leia `docs/state.md` desta obra antes de qualquer ação.
2. Ao concluir uma task, atualize `docs/roadmap.md` (mova para Consolidado).
3. Ao encerrar sessão, atualize `docs/state.md` com checkpoint.
