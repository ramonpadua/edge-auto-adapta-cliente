# SPEC-1-003 — Conciliação dupla, fila de ajustes de ponto e divergências

- **Fase**: F1 · **Capacidades**: C5, C6 · **Risco**: obrigatório (dado pessoal, decisão humana preservada)
- **Ambiente**: Skip (GoSkip + SkipCloud) — regra geral do consultor (22/09/2026)
- **Degrau da solução**: é o coração da F1 — substitui a conferência manual linha a linha (espelho PDF × reporte × planilha) por comparação automática com exceções; elimina o trabalho de transcrição e confronto descrito no as-is (02:43–04:05 da `[REUNIÃO MACHADO]`).

## Contexto
- **Estado atual**: financeiro recebe reporte semanal por e-mail e confronta manualmente com espelhos e planilha; correções ficam em versões de arquivo sem motivo.
- **Estado desejado**: cada colaborador com status **conciliado / divergente / pendente** nas duas comparações (interna: ponto × reporte × contrato; externa: ponto × planilha do cliente); ajustes de ponto decididos por humano com contexto; divergências com origem, responsável e prazo; histórico por versão.

## Atores e permissões
- RH/Medição: decide ajustes de ponto (aprova/recusa) — **o sistema nunca decide**.
- Financeiro/Interface VW: trata divergências, registra correção/justificativa.
- Consultoria: parametriza contrato de semântica (com o cliente).

## Dados
Marcações diárias (4/dia + justificativas), ajustes pendentes, H.T./H.E.1/H.E.2/noturno/sáb/dom, HT CONTRATO, reporte semanal, planilha do cliente (carga da SPEC-1-002), status por colaborador, motivo de divergência, versões de correção.

## Regras
1. **Decisão humana intransponível**: aprovação/recusa de ajuste de ponto é sempre humana; o sistema apresenta contexto e registra a decisão (prova negativa obrigatória).
2. Divergência só fecha com origem identificada (ponto · reporte · regra contratual · documento faltante · pedido do cliente · outro validado).
3. Comparação interna e externa nunca misturam semânticas: cada uma usa seu contrato (contrato × contrato de semântica do cliente).
4. Sem reporte → status "pendente — reporte ausente" + entrada na fila de pendências com responsável.
5. Toda correção gera nova versão com motivo, responsável e data (append-only); nada é sobrescrito.
6. Dado real bloqueado até I-06; demonstrações em fixture.

## Fluxo e passos
1. Para cada colaborador da competência: executar comparação interna e externa.
2. Atribuir status por comparação e consolidar situação do colaborador.
3. Ajustes pendentes → fila humana com contexto (marcações, justificativa, histórico).
4. Divergências → fila com origem, responsável, prazo; correção → nova versão auditada.

## Exceções e rollback
- Colaborador sem planilha do cliente → status "sem contrapartida do cliente", não "conciliado".
- Correção errada → nova versão corrige; a anterior permanece na trilha.
- Queda no meio da conciliação → estado por colaborador é idempotente; retomada não recalcula o que já foi decidido.

## Critérios de aceite (binários)
- **CA-1-012**: para cada colaborador, o sistema exibe status conciliado/divergente/pendente nas duas comparações (interna e planilha do cliente), com os valores comparados visíveis.
- **CA-1-013**: nenhuma divergência fecha sem origem identificada; o formulário de correção exige origem (enumeração acima) e a recusa sem origem é testada.
- **CA-1-014**: o sistema **nunca** aprova ou recusa ajuste de ponto automaticamente — prova negativa: cenário com ajuste pendente e timeout sem humano mantém o ajuste pendente.
- **CA-1-015**: toda correção de divergência gera nova versão com motivo, responsável e data; versões anteriores preservadas (append-only verificado por consulta).
- **CA-1-016**: comparação interna usa HT × HT CONTRATO e a externa usa o contrato de semântica do cliente; coluna cruzada não é usada entre comparações (teste de isolamento).
- **CA-1-017**: colaborador sem reporte semanal fica "pendente — reporte ausente" e aparece na fila de pendências com responsável nomeado.

## TDD da SPEC
- **RED**: cenário "ajuste pendente sem decisão humana por 24h" → hoje o processo depende de olhar o MarqPonto; sem sistema, não há fila. Prova: registro mostra ajuste sem tratamento estruturado.
- **GREEN**: CA-1-012..017 em fixtures (10 colaboradores: 4 conciliados, 3 divergentes, 2 pendentes, 1 sem contrapartida); prova: status corretos (012), recusa sem origem (013), ajuste mantido pendente (014), versões preservadas (015), isolamento de semânticas (016), fila de pendências (017).
- **REGRESSÃO**: reprocessar a mesma competência não altera decisões já registradas; decisões humanas preservadas após reimportação.

## Instruções para o Ethos
- Superfícies: motor de comparação; painel de status por colaborador; fila de ajustes; fila de divergências; histórico de versões.
- Fixtures: 10 colaboradores sintéticos com os 4 cenários acima; reportes e planilhas sintéticas.
- Insumos embutidos na task: I-08 (1–2 vídeos curtos dos processos faltantes — Meire/Renata; "envie um vídeo de cada processo antes de detalharmos as automações").
- **Ponto de parada**: se I-08 não vier, o desenho avança no declarado (escopo §3/§7) e ajusta depois; nunca modelar processo não demonstrado como fato. Sem I-07, a comparação externa roda contra fixture.

## Checklist de aceite
- [ ] CA-1-012..017 provados em fixture
- [ ] Prova negativa de não-decisão (014) registrada
- [ ] Append-only verificado
- [ ] Teste humano do RH/Medição e do Financeiro registrado

## Tasks vinculadas

| ID | Tarefa | Critérios | Dependências |
|---|---|---|---|
| 195a6547-bd37-442a-b22a-0dd541b44bfd | Comparar as horas e mostrar quem precisa de conferência | CA-1-012, CA-1-016 | T3, T4 |
| f367ac8b-08f6-4e3e-a58e-22287bebb06a | Resolver diferenças com aprovação e histórico | CA-1-013, CA-1-014, CA-1-015, CA-1-017 | T5 |

## Emendas
(nenhuma)


## Orientação de execução — revisão de 10/11/2026

Esta revisão não altera critérios, fórmulas, limites ou o resultado contratado. O código do sistema disponível foi lido no commit 5179d0b, v0.0.7; não foi testado no ambiente do cliente. O estado e o teste humano não se presumem por existir código. Ler os roteiros correspondentes em `04_fase-atual/fase.md` (ou `00-Tasks_Gerais.md` no Plano). Reaproveitar a base, conferir a versão atual e corrigir apenas lacunas. Maestro executa; Bruno/time testam e aprovam. Explicar o que existe, o que falta, por que importa e cada clique com resultado esperado; avisar “olha o Skip agora”. Sem jargão nas interações. Não concluir sem evidência e aceite explícito. Uma tarefa por vez dentro da F1 liberada, sem autorização do consultor por tarefa. Testes técnicos em ambiente próprio isolado e dados fictícios; não acessar banco do cliente nem usar produção. Não alterar campos sensíveis, permissões ou valores por suposição.
