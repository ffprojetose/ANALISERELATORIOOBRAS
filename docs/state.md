# Estado da Sessão — Plataforma

**Última atualização:** 2026-07-27

## Task em Andamento
Estruturação inicial da plataforma (índice modular), definição da metodologia geral (`docs/requirements.md` + `docs/metodologia/`) e criação da primeira obra (`reserva-park`) a partir do template.

## Arquivos Modificados
- `CLAUDE.md` — criado como roteador raiz, com regras absolutas de isolamento por obra.
- `docs/project.md`, `docs/requirements.md`, `docs/roadmap.md`, `docs/state.md` — criados.
- `docs/metodologia/` — criada (`curva-s.md`, `replanejamento.md`, `recursos.md`, `desembolsos.md`, `validacoes.md`, `formato-de-saida.md`).
- `.gitignore` — criado para proteger documentos confidenciais, arquivos gerados e arquivos de sistema/ambiente.
- `templates/obra-template/` — estrutura de pastas e documentação genérica criadas.
- `obras/reserva-park/` — estrutura de pastas criada, espelhando o template, ainda sem dados preenchidos.

## Decisões Tomadas (ainda não documentadas)
- Nomes de pastas em kebab-case sem acento.
- Estrutura de dados por obra organizada em três estágios: `entrada/`, `processamento/`, `saida/`.
- Metodologia técnica modularizada em `docs/metodologia/` para não sobrecarregar `docs/requirements.md`.

## Próximo Passo
Aguardar os documentos oficiais da Reserva Park em `obras/reserva-park/entrada/` para preencher os campos `[PREENCHER]` de `obras/reserva-park/CLAUDE.md` e `docs/project.md`.
