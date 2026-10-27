# changelog — Projeto EDGE AUTO

## 2026-10-27
- 2026-10-27 · [consultor] · EMENDA DOCUMENTAL (sem implementação de app): task 9 "Configurar acesso e gestão de contas de usuários" criada na Fase 1, leva 2 (inserida após a task 2; depende de T1 e T2 aceitas), vinculada à SPEC-1-001 com o critério **CA-1-025 (emenda)** — CA-1-006 já pertence à SPEC-1-002 e não é reutilizado. Prazo a combinar na liberação (não fixado). Escopo do pedido: retirar botão "Criar conta" do login e passar a criação de contas para a página de gestão administrativa restrita, com controle no servidor (além de ocultar a UI), auditoria e contas existentes preservadas. Pergunta obrigatória a Bruno (I-11): quais pessoas e perfis poderão criar contas — a política de acesso não é definida antes da resposta, sem presumir administradores. Projeções sincronizadas: fase.md, SPEC-1-001, STATUS, changelog, README da fase; Jornada (fase_1.md), 00-Tasks_Gerais, matriz de rastreabilidade, STATUS e changelog no Plano (Drive); espelho da SPEC no repositório adapta-cliente.

## 2026-10-06
- 2026-10-06 · [champion] · DEBUG task 1f8bc7fb-f85a-4ed1-9abc-a9d6dc8afbd5: QA v0.0.2 falhou em hook/staticAnalysis por marcador de patch e fixtures incompatíveis com os validadores → causa raiz corrigida com substituição limpa do hook e migration aditiva 0005 (sem mudar IDs de clientes/cobranças) → QA v0.0.3 passou setup, staticAnalysis, build, integrations e test; 0005 aplicada; preview redireciona para login, então falta teste humano autenticado de Bruno; app não publicado. Detalhes em `06_notas/debug/debug-2026-10-06-task1-fixtures.md`.

## 2026-09-30
- Workspace operacional criado (handoff validado) com a Fase 1: 4 SPECs, 8 tasks em 6 levas, champion Bruno e prazos 05/10→12/10/2026.
- Regras de ouro registradas: dado real só após política; fail-closed de teto e layout; decisão humana preservada em ponto/divergência/liberação/NFS-e/call off.

## 2026-09-17
- Kickoff Adapta Native (Bruno/CEO, Renata/Financeiro, Meire/RH, Alexandra/Vendas). Ciclo 1 definido: conciliação de ponto + régua de cobrança.
