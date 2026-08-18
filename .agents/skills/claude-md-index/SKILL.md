---
name: Codex-md-index
description: >
  Estrutura o AGENTS.md de um projeto como um Índice Modular em vez de um monolito de contexto.
  Use esta skill sempre que o usuário mencionar AGENTS.md, contexto de projeto para Codex,
  escalabilidade de contexto em projetos de IA, "o Codex está esquecendo coisas entre sessões",
  "meu AGENTS.md está ficando gigante", ou quiser organizar documentação de projeto para agentes
  de IA. Também acione quando o usuário pedir para estruturar, criar ou refatorar arquivos de
  contexto para Codex, Cursor, ou qualquer agente LLM que use arquivos Markdown como memória.
  Esta skill deve ser ativada agressivamente -- qualquer menção a contexto de sessão, estado de
  projeto, ou documentação modular para agentes de IA é suficiente para acionar.
---

# AGENTS.md como Índice Modular

## Conceito Central

O erro mais comum em projetos que escalam: usar o `AGENTS.md` como um manual monolítico que cresce
indefinidamente. Isso degrada a qualidade do contexto, aumenta o custo de tokens e faz o agente
perder foco.

**A solução:** tratar o `AGENTS.md` como um **roteador de informações** -- um índice leve que aponta
para arquivos especializados. O agente lê o índice e navega apenas para o que precisa.

---

## Estrutura de Arquivos

```
projeto/
├── AGENTS.md           ← Índice principal (roteador)
├── docs/
│   ├── project.md      ← Visão, propósito, North Star
│   ├── requirements.md ← Requisitos e lógica de negócio
│   ├── roadmap.md      ← Histórico consolidado + próximos passos
│   └── state.md        ← Estado atual da sessão
```

---

## Papel de Cada Arquivo

### `AGENTS.md` -- O Roteador
- Identidade do projeto em 3-5 linhas
- Stack técnico resumido
- Links explícitos para os demais arquivos com descrição de quando usar cada um
- Regras absolutas de comportamento do agente (nunca deletar dados, padrões de código, etc.)
- **Deve ser curto.** Se passar de 80 linhas, algo deve ser movido para um arquivo filho.

### `docs/project.md` -- North Star
- Objetivo do produto/sistema em linguagem clara
- Problema que resolve e para quem
- Decisões arquiteturais de alto nível já tomadas
- O que o projeto **não** é (evita desvios de escopo)

### `docs/requirements.md` -- Contratos
- Requisitos funcionais estruturados (pode usar user stories, AC, ou formato livre)
- Regras de negócio críticas com exemplos
- Integrações externas e seus contratos
- Validações obrigatórias
- **Atualizado sempre que um requisito muda ou é descoberto**

### `docs/roadmap.md` -- Memória Histórica
- Seção `## Consolidado`: o que foi implementado e está estável
- Seção `## Em andamento`: features/tasks na sprint atual
- Seção `## Backlog`: próximos passos priorizados
- **Nunca apagar o consolidado** -- é a memória do projeto

### `docs/state.md` -- Checkpoint de Sessão
- Qual task estava em andamento quando a sessão foi encerrada
- Arquivos modificados na última sessão
- Decisões tomadas que ainda não estão em requirements.md
- Próximo passo imediato ao retomar
- **Sobrescrito a cada encerramento de sessão**

---

## Template: `AGENTS.md` (Índice)

```markdown
# [Nome do Projeto]

[1-2 frases: o que é e qual problema resolve]

## Stack
- [tecnologia principal]
- [banco de dados]
- [infra/deploy]

## Contexto do Projeto
- Visão e propósito → `docs/project.md`
- Requisitos e regras de negócio → `docs/requirements.md`
- Histórico e roadmap → `docs/roadmap.md`
- Estado da sessão atual → `docs/state.md`

## Regras Absolutas
- [regra crítica 1, ex: nunca sobrescrever .env sem confirmação]
- [regra crítica 2, ex: sempre rodar testes antes de commitar]
- [padrão de código/arquitetura obrigatório]

## Fluxo de Trabalho
1. Leia `docs/state.md` antes de qualquer ação
2. Ao concluir uma task, atualize `docs/roadmap.md` (mova para Consolidado)
3. Ao encerrar sessão, atualize `docs/state.md` com checkpoint
```

---

## Template: `docs/state.md` (Checkpoint)

```markdown
# Estado da Sessão

**Última atualização:** [data/hora]

## Task em Andamento
[descrição da task que estava sendo executada]

## Arquivos Modificados
- `src/...` -- [o que foi feito]
- `docs/...` -- [o que foi atualizado]

## Decisões Tomadas (ainda não documentadas)
- [decisão 1]
- [decisão 2]

## Próximo Passo
[instrução direta para o agente ao retomar]
```

---

## Quando Refatorar um AGENTS.md Existente

Se o usuário tem um `AGENTS.md` monolítico, siga esta ordem:

1. **Leia o arquivo completo** e identifique blocos de conteúdo por categoria
2. **Extraia para os arquivos filhos** respeitando as responsabilidades acima
3. **Reduza o AGENTS.md** para apenas o índice + regras absolutas
4. **Atualize os links** no índice apontando para os novos arquivos
5. **Confirme com o usuário** a estrutura antes de finalizar

---

## Sinais de que a Estrutura Está Degradando

- `AGENTS.md` passou de 100 linhas
- O agente está "esquecendo" contexto entre sessões
- Requisitos e estado estão misturados no mesmo arquivo
- O roadmap não tem seção de histórico consolidado
- `state.md` não existe ou nunca é atualizado

---

## Princípios de Manutenção

- **Imutabilidade do histórico:** seção `Consolidado` do roadmap nunca é deletada, apenas cresce
- **state.md é volátil:** único arquivo que pode ser sobrescrito completamente
- **requirements.md é contrato:** mudanças devem ser explícitas, com data se necessário
- **AGENTS.md é estável:** raramente muda; reflete a identidade permanente do projeto
