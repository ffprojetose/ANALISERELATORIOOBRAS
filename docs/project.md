# North Star — Plataforma de Análise e Replanejamento de Obras

## Objetivo
Analisar relatórios mensais de múltiplas obras, comparar o previsto com o realizado, identificar desvios da Curva S e elaborar replanejamentos tecnicamente viáveis.

## Problema que Resolve
A consolidação manual de relatórios mensais dificulta a identificação precisa dos desvios físico-financeiros, das causas dos atrasos e dos impactos sobre tarefas, equipes, materiais e desembolsos futuros.

## Para Quem
Arquitetos, engenheiros, construtoras, gestores e profissionais responsáveis pelo planejamento e controle de obras.

## Metodologia Geral (aplicada a toda obra)
Cada obra segue o mesmo fluxo de dados, em três estágios:

1. **`entrada/`** — documentos brutos recebidos do cliente/obra, organizados por tipo: `relatorios-mensais/`, `cronogramas/`, `medicoes/`, `orcamentos/`, `contratos/`, `atas/`.
2. **`processamento/`** — scripts, notebooks e artefatos intermediários usados para transformar os dados de entrada.
3. **`saida/`** — resultados gerados pela análise: `analises/`, `planilhas/`, `curvas-s/`, `relatorios-finais/`.

O detalhamento técnico de cada etapa está em `docs/metodologia/`.

## Decisões Arquiteturais
- Cada obra vive em `obras/<nome-da-obra>/` com estrutura própria (`docs/`, `entrada/`, `processamento/`, `saida/`) — isolamento total entre obras.
- Novas obras são criadas a partir de `templates/obra-template/`, que deve permanecer genérico.
- Skills reutilizáveis ficam em `.claude/skills/` e podem ser aplicadas a qualquer obra.

## O que este Projeto NÃO É
- Não é um repositório de dados brutos/confidenciais versionados (ver `.gitignore`).
- Não é uma ferramenta específica para uma única obra — a raiz permanece genérica.
