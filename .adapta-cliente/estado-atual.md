# Estado atual — Adapta Cliente

- task_id: 1f8bc7fb-f85a-4ed1-9abc-a9d6dc8afbd5
- champion: Bruno - Champion
- spec: 04_fase-atual/specs/spec-1-001-cadastro-e-competencia.md
- etapa: conferir_versao_atual_antes_do_teste_humano
- autorizacao_implementacao: confirmada — 2026-10-06T12:32-03:00; “pode usar eles como dados sintéticos, ou criar novos. Faça as alterações necessárias para garantir que construa o projeto”
- autorizacao_execucao_fase: liberada — 2026-11-10, consultor Ramon Pádua; uma task por vez, teste humano entre tasks
- teste_humano: pendente — Bruno valida CA-1-001/002/003 no preview atual (sistema evoluiu a v0.0.7)
- verificacao_automatica: passou — QA Skip v0.0.3 (`3219216`): setup, staticAnalysis, build, integrations e test passaram; migration 0005 aplicada; schema verificado. Observação: npm test é placeholder e não cobre comportamento.
- aprendizado: capturado:06_notas/aprendizado-continuo/AP-2026-10-06-1728-skip-migration-fixtures.md
- ultima_acao: execução da F1 liberada pelo consultor (10/11); submódulo `07-sistemas/Acompanhamento-RH-e-Financeiro` publicado (repo do cliente, commit 5179d0b, v0.0.7) — o sistema já tem ponto/RH/financeiro/admin; evoluir, nunca reconstruir
- proxima_acao: Maestro confere a versão atual da T1 e a garantia do histórico; corrige somente lacunas em ambiente isolado; depois conduz Bruno no teste humano e pede aceite explícito.
- atualizado_em: 2026-11-10T15:55:00-03:00

## Estado vigente — revisão das tarefas em 10/11/2026

Fase 1 LIBERADA pelo consultor Ramon neste chat. 9 tarefas, nenhuma encerrada nesta revisão. Maestro executa; Bruno/time fazem o teste e aprovam cada tarefa. Não exigir autorização do consultor por tarefa. Escopo novo ou mudança de fase volta ao consultor.

Foi conferido o remoto do sistema em 10/11: commit 5179d0b, v0.0.7, igual ao gitlink existente. Leitura de código, sem acesso ao banco, app ou produção. Contratos, Painel RH, ponto, Cobranças e Usuários devem ser aproveitados. Presença de tela não comprova competência mensal, importação, conciliação, motor faturável, relatório comparativo nem proteção completa de contas. A T1 precisa conferir/corrigir o caminho de cadastro com histórico opcional antes do aceite da versão atual; o QA v0.0.3 não comprova v0.0.7.

Todas as tarefas foram reescritas em linguagem simples: o que existe, o que falta, por que importa, informação necessária, teste humano em passos com resultado esperado, evidência e parada. IDs e critérios preservados. T9 visível ao cliente. A primeira retomada é só T1; conferir eventual aceite de 27/10 e preservar provas existentes. Não reiniciar cadastros nem reconstruir o app. Dados fictícios e testes técnicos isolados, sem banco do cliente. MarqPonto: credencial cadastrada não é integração ativa; não pedir valor da chave nem antecipar API/SharePoint/rotinas. Prazos anteriores permanecem como histórico, a recombinar com Bruno.
