# Analise-relatorios-obras

Plataforma reutilizável para análise e replanejamento de relatórios mensais de obras. Cada obra é mantida isolada dentro de `obras/`.

## Stack
- [PREENCHER: linguagem/framework principal]
- [PREENCHER: fonte de dados/planilhas]
- [PREENCHER: infra/deploy, se houver]

## Contexto da Plataforma
- Visão e propósito → `docs/project.md`
- Requisitos e regras de negócio gerais → `docs/requirements.md`
- Metodologia detalhada → `docs/metodologia/` (Curva S, replanejamento, recursos, desembolsos, validações, formato de saída)
- Histórico e roadmap da plataforma → `docs/roadmap.md`
- Estado da sessão atual → `docs/state.md`

## Obras Ativas
- `obras/reserva-park/` → ver `obras/reserva-park/CLAUDE.md`

## Templates
- Nova obra → `templates/obra-template/`

## Regras Absolutas
- Nunca misturar dados entre obras diferentes.
- Regras gerais ficam na raiz; dados e regras específicas ficam dentro de cada obra em `obras/<nome-da-obra>/`.
- Não versionar documentos confidenciais de clientes nem arquivos gerados (ver `.gitignore`).
- Toda nova obra deve ser criada a partir de `templates/obra-template/`.
- Este arquivo permanece curto (roteador apenas) — nunca adicionar dados de obra específica aqui.
- Antes de qualquer análise, identificar explicitamente qual é a obra ativa.
- Trabalhar exclusivamente dentro de `obras/<obra-ativa>/`.
- Nunca pesquisar, comparar ou utilizar arquivos de outra obra sem solicitação expressa.
- Caso a obra ativa não esteja clara, perguntar qual obra deverá ser analisada.
- Nunca alterar, renomear, mover ou sobrescrever documentos da pasta `entrada/`.
- Todo arquivo gerado deve ser salvo exclusivamente em `processamento/` ou `saida/`.
- Não considerar inferências como fatos.
- Não inventar percentuais, valores, datas, produtividades, tarefas ou recursos ausentes.
- Sempre registrar divergências encontradas entre relatórios antes de realizar o replanejamento.

## Fluxo de Trabalho
1. Identifique a obra ativa e leia `docs/state.md` (plataforma) e o `CLAUDE.md` da obra antes de qualquer ação.
2. Ao concluir uma task, atualize o `roadmap.md` correspondente (plataforma ou obra).
3. Ao encerrar sessão, atualize o `state.md` correspondente com checkpoint.
