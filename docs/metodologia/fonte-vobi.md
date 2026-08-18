# Fonte VOBI — Mecânica de Cálculo do Cronograma

Aplica-se sempre que uma obra usa o **VOBI** como sistema de planejamento/orçamento e os
documentos de `entrada/cronogramas/` dessa obra forem exportações ou capturas do VOBI
(planejamento, Curva S, Físico-Financeiro). Baseado em auditoria somente-leitura (interceptação
passiva da própria aplicação, nenhuma requisição extra disparada, nenhum dado alterado).

## Telas e sua relação real
- **Orçamento** e **Planejamento** são o mesmo registro (mesmo item), não duas tabelas ligadas: os campos de data de planejamento (`Início`, `Fim`, duração) vivem dentro do próprio item de orçamento.
- **Curva S** e **Físico-Financeiro** são **irmãos**, não pai e filho — vêm do mesmo relatório/endpoint de cálculo. A Curva S apenas agrega o resultado e desenha o gráfico; não existe um "cálculo da Curva S" separado do "cálculo do Físico-Financeiro".
- **Medições** alimentam o Realizado físico (%). **Financeiro/custos lançados** alimenta o Realizado (R$). Não confundir os dois — R$ realizado (custo lançado) e R$ medido (medição) são grandezas diferentes e não devem ser conciliados como se fossem a mesma coisa.

## Fórmula do previsto
```
valorPrevisto(grupo, mês) = valorTotal(grupo) × diasCorridosDoGrupoNoMês ÷ diasTotais(grupo)
```
- Distribuição **linear por dia corrido** — sábados, domingos e feriados contam igual; não é por dia útil, não é por medição, não é ponderada, não tem rampa nem curva em "S" dentro da própria atividade.
- `diasTotais(grupo)` = dias corridos inclusivos entre a data de início e a data de fim do grupo.

## Regra crítica: só o nível hierárquico mais alto do orçamento governa o relatório
- Apenas as datas do **nível 1** (os grupos-raiz do orçamento, ex. as grandes disciplinas/etapas) entram no cálculo do previsto da Curva S e do Físico-Financeiro.
- Datas de subníveis e de itens (folhas) **não têm efeito no relatório** — existem apenas para o Gantt visual. Alterá-las dá uma falsa sensação de replanejamento.
- O nível 1 **não é um agregador automático** das datas dos filhos — são campos independentes, editáveis diretamente nele. Podem divergir do mín/máx real dos descendentes sem gerar erro ou aviso.
- Ao ler um cronograma exportado do VOBI, verificar sempre as datas do nível 1, não a data aparente do primeiro/último item.

## Recálculo retroativo — risco central para o replanejamento
- O previsto é **recalculado do zero a cada leitura**, a partir das datas atuais do nível 1. Não existe snapshot mensal congelado do previsto.
- Alterar `Início` ou `Fim` de um grupo cuja janela inclua meses **já fechados/publicados** reescreve o previsto desses meses (a mudança altera `diasTotais(grupo)`, o que altera a taxa diária, que multiplica todos os meses da atividade, inclusive os passados).
- O **realizado** não sofre esse risco: vem das medições, ancorado na data de cada medição, e não é recalculado pelo planejamento.

## Teste de segurança antes de editar uma data de nível 1
```
É seguro alterar as datas de um grupo se, e somente se:
   data de início atual >= data de corte da análise   E   nova data de início >= data de corte da análise
```
Se o início atual for anterior à data de corte, qualquer alteração (início ou fim) altera o
passado — não existe meio-termo.

## Classificação das atividades por risco de recálculo retroativo
Antes de propor remanejamento, classificar cada grupo de nível 1 conforme sua janela em relação à data de corte:
- **Classe A — Histórico fechado:** janela inteiramente anterior à data de corte. Não tocar.
- **Classe B — Atravessa o corte:** começa antes da data de corte e termina depois. Qualquer edição reescreve meses já publicados — exige decisão explícita do gestor (congelar, aceitar/documentar o recálculo, ou compensar ajustando outros grupos para preservar o acumulado publicado).
- **Classe C — Futura:** começa na data de corte ou depois. É o espaço seguro de remanejamento — atrasar o início ou prorrogar o fim dessas atividades não tem efeito retroativo, desde que o novo fim não ultrapasse o prazo final da obra.

## Origem de cada série do relatório
| Série | Origem |
|---|---|
| Previsto (período e acumulado) | Datas de nível 1 × valor total do grupo, conforme fórmula acima |
| Realizado físico (%) | Medições, pela data de cada medição |
| Realizado financeiro (R$) | Custos/despesas lançados no financeiro — não é o valor medido |
| Desempenho | Realizado ÷ Previsto do mesmo período |

## Armadilhas conhecidas ao usar exportações do VOBI como fonte
- A linha "Previsto acumulado" (e, por vezes, "Realizado acumulado (%)") de uma Curva S do VOBI pode **não ser a soma aritmética correta** das linhas mensais — sempre validar o acumulado somando os valores absolutos mês a mês em vez de confiar na linha pronta (ver `curva-s.md`).
- A "Duração" exibida costuma ser em dias úteis, mas o cálculo do previsto usa dias corridos — nunca estimar impacto financeiro a partir da coluna de duração.
- A numeração de meses ("Mês 1", "Mês 2"...) pode diferir entre telas quando uma delas inclui um mês adicional com realizado anterior ao previsto.
- Um grupo de nível 1 pode ter medição registrada **antes** da sua data de início prevista — sinal de que o planejamento não reflete a execução real e precisa de revisão, não de conciliação silenciosa.
- Itens/subníveis sem nenhuma data de planejamento não afetam o relatório (só o nível 1 conta), mas indicam planejamento incompleto e devem ser sinalizados.

## Procedimento seguro para remanejamento de datas no VOBI
Executar apenas após aprovação explícita, item a item:
1. Registrar (congelar) a Curva S, o Físico-Financeiro, a lista de medições e as datas de nível 1 atuais — sem isso não há "antes × depois".
2. Criar uma nova linha de base no VOBI antes de qualquer edição (ação de escrita — exige autorização expressa).
3. Definir a meta do(s) mês(es) a ajustar e converter em valor absoluto.
4. Aplicar o teste de segurança a cada grupo candidato — priorizar Classe C; tratar Classe B como decisão consciente do gestor.
5. Simular fora do VOBI com a fórmula acima antes de editar, conferindo que a soma dos meses bate com o valor total do grupo/obra e que os meses já publicados permanecem idênticos (quando essa for a meta).
6. Editar apenas Início/Fim do nível 1, um grupo por vez, conferindo o Físico-Financeiro após cada edição.
7. Conferir se o reagendamento automático moveu subníveis ou outros grupos por causa de predecessoras.
8. Registrar um relatório de alterações: grupo, data anterior, data nova, dias antes/depois, delta por mês, delta acumulado, e confirmação de que nenhum mês histórico foi afetado.

## Regra absoluta
- Nunca alterar quantidade, unidade, preço unitário, BDI ou valor total de um item ao editar
  o cronograma — essas edições mudam o peso financeiro do item, que é proibido no escopo de
  replanejamento (só a plataforma de orçamento pode alterá-los, mediante decisão separada do
  cliente/gestor).
