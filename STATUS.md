# STATUS — Projeto EDGE AUTO (Medição, Faturamento e Cobrança)

**Etapa atual:** Fase 1 — **execução LIBERADA em 10/11 pelo consultor Ramon Pádua** · task 1 implementada (QA v0.0.3) aguardando teste humano do Bruno no preview atual · sistema do cliente já evoluiu a v0.0.7 (submódulo `07-sistemas/Acompanhamento-RH-e-Financeiro`) — evoluir o que existe, nunca reconstruir
**Champion:** Bruno (CEO) · **Construção:** Skip (GoSkip + SkipCloud)

| Etapa | Estado |
|---|---|
| Kickoff e corte do escopo | Concluídos (17/09–30/09) |
| Escopo do ciclo 1 (conciliação + cobrança) | Aprovado |
| SPECs da Fase 1 | 4 SPECs · 24 critérios de aceite + CA-1-025 (emenda 27/10) · com TDD e provas negativas |
| Tasks da Fase 1 | 9 tasks em 6 levas · responsável: Bruno |
| Task 1 — cadastro clientes/contratos/plantas/tetos | Código no preview; QA v0.0.3 passou; migration 0005 aplicada; aguardando teste humano |
| Execução confirmada | 0 tasks fechadas; teste funcional da task 1 pendente |

## Próxima ação

1. Bruno entra no preview autenticado e valida as provas de CA-1-001/002/003 (contrato sem entidade recusado; teto sem default; cálculo com teto vazio retorna "em conferência"). Passo a passo no comando de retomada.
2. Só depois da aprovação explícita do teste humano, concluir a task 1 e atualizar o avanço da fase.
3. Em seguida: task 2 (competência) e, após T1+T2 aceitas, task 9 (gestão de contas, CA-1-025) — a política de contas depende da resposta do Bruno sobre pessoas/perfis (I-11), pergunta obrigatória.

## Limites

- App não publicado em produção.
- `npm test` do projeto é um placeholder sem casos automatizados reais.
- Dados de trabalho devem continuar sintéticos até aprovação da política de dados.
- O sistema do cliente (repo próprio, v0.0.7) já tem páginas de ponto, RH, financeiro e admin — consultar o submódulo `07-sistemas/Acompanhamento-RH-e-Financeiro` antes de construir; evoluir, nunca reconstruir.
