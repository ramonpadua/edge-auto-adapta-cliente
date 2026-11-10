# SPEC-1-004 — Cálculo faturável fail-closed, relatório comparativo e baseline

- **Fase**: F1 · **Capacidades**: C7 (parcial), C11 (v1), C13 (mínima) · **Risco**: obrigatório (dado pessoal, valor financeiro)
- **Ambiente**: Skip (GoSkip + SkipCloud) — regra geral do consultor (22/09/2026)
- **Degrau da solução**: entrega palpável da F1 — o **relatório comparativo ponto × planilha do cliente** (ID-02, valor visível na 1ª consultoria e argumento do rito/SLA) — e fecha a base de medição do ciclo (baseline + métrica), com o cálculo de faturáveis protegido por fail-closed.

## Contexto
- **Estado atual**: horas faturáveis calculadas à mão em planilha (H.T., H.E.1 75%, H.E.2 100%, noturno, sáb/dom/fer), com teto contratual em conflito e sem baseline medido.
- **Estado desejado**: motor de cálculo parametrizado por regra contratual, fail-closed sem teto provado; relatório comparativo por competência/planta/colaborador com divergências por origem; baseline coletado com protocolo de medição; governança mínima (dado real bloqueado, auditoria).

## Atores e permissões
- Financeiro: confere itens faturáveis, valida relatório, registra baseline.
- RH/Medição: contribui com dados de tempo de processo.
- Consultoria: registra protocolo de medição (janela/método).

## Dados
Regra contratual por cliente/planta/vigência (H.E.1 %, H.E.2 %, adicional noturno, sáb/dom/fer), teto (I-04), horas conciliadas (SPEC-1-003), itens faturáveis/não faturáveis/em conferência, tempos do baseline (I-02: conciliação, envio→aprovação, aprovação→pagamento), métrica por competência.

## Regras
1. **Fail-closed de teto**: sem teto provado, nenhum item sai como "faturável" — apenas "em conferência — teto não provado" (DH-04).
2. Faturáveis só com regra contratual aplicada e conferência registrada; rubricas (H.E.1/H.E.2/noturno/sáb/dom/fer) calculadas por parametrização, nunca por valor fixo universal (a regra VW não é universal).
3. **Meta numérica só após baseline** (DH-02) — nada de promessa antes de medido.
4. Política mínima: dado real (próprio/de terceiros) bloqueado até I-06; até lá, fixtures (CA-1-022 com prova negativa de recusa).
5. Toda alteração de valor/horas/previsão auditada (quem/quando/por quê).
6. Nenhuma superfície promete automação não provada (I-03): rótulos de "manual/integração" fiéis à realidade.

## Fluxo e passos
1. Aplicar regra contratual às horas conciliadas → itens faturáveis / não faturáveis / em conferência.
2. Gerar relatório comparativo ponto × planilha do cliente (por competência/planta/colaborador, divergências por origem).
3. Registrar tempos de processo → baseline + métrica por competência (protocolo de medição documentado).

## Exceções e rollback
- Regra contratual ausente → item "sem regra", não faturável.
- Baseline incompleto → registra parcial com ressalva; nunca estima.
- Relatório regenerável a qualquer momento a partir dos dados versionados (idempotente).

## Critérios de aceite (binários)
- **CA-1-018**: motor calcula H.E.1 (75%), H.E.2 (100%), noturno, sáb/dom/fer conforme regra parametrizada por cliente/planta/vigência; teste com 2 regras distintas mostra resultados distintos para as mesmas horas.
- **CA-1-019**: sem teto provado, todos os itens saem "em conferência — teto não provado"; com teto cadastrado (I-04), H.T. acima do teto é sinalizado e faturáveis exigem conferência registrada.
- **CA-1-020**: relatório comparativo ponto × planilha do cliente é gerado por competência/planta/colaborador, com divergências agrupadas por origem e exportável para apresentação ao cliente.
- **CA-1-021**: baseline é coletado com protocolo de medição (janela/método) registrado; métrica (tempo de conciliação, dias envio→aprovação, dias aprovação→pagamento) é registrada desde a primeira competência.
- **CA-1-022**: tentativa de usar dado real antes de I-06 é recusada com motivo (prova negativa); demonstrações e testes rodam em fixture sintético.
- **CA-1-023**: toda alteração de valor, horas ou previsão gera registro de auditoria (quem, quando, por quê) — verificado por consulta após edição.
- **CA-1-024**: nenhuma superfície exibe "integração ativa" sem I-03 provado; o fallback manual é visível e operável (rótulo fiel).

## TDD da SPEC
- **RED**: cenário "calcular faturáveis sem teto cadastrado" → hoje a planilha calcula mesmo sem teto confiável (187:30 × 183:30 em disputa). Prova: folha de cálculo produz número sem validade contratual.
- **GREEN**: CA-1-018..024 em fixtures (2 regras distintas, teto vazio/preenchido, relatório com divergências, baseline parcial); prova: fail-closed (019), regras distintas (018), relatório exportável (020), protocolo registrado (021), recusa de dado real (022), auditoria (023), rótulo fiel (024).
- **REGRESSÃO**: regenerar relatório é idempotente; editar valor mantém auditoria; mudar regra contratual não altera competências já encerradas.

## Instruções para o Ethos
- Superfícies: motor de cálculo; regras contratuais parametrizadas; gerador/exportador do relatório comparativo; registro de baseline/métrica; trilha de auditoria.
- Fixtures: 2 regras contratuais sintéticas, teto vazio e teto fictício, tempos de baseline fictícios.
- Insumos embutidos na task: I-02 (baseline 3 meses — Renata/Meire: "quanto tempo leva a conciliação e quantos dias entre envio, aprovação e pagamento?"), I-04 (cláusula do teto — Renata/contrato VW).
- **Ponto de parada**: sem I-04, teto vazio + fail-closed (não é bloqueio de task — a pergunta vai junto). Sem I-02, baseline nasce coletando a partir da primeira competência executada, com ressalva explícita. Nunca inventar teto, fórmula contratual ou número de baseline.

## Checklist de aceite
- [ ] CA-1-018..024 provados em fixture
- [ ] Prova negativa de fail-closed (019) e de dado real (022) registradas
- [ ] Relatório comparativo exportável demostrado (entrega palpável da F1)
- [ ] Teste humano do Financeiro registrado

## Tasks vinculadas

| ID | Tarefa | Critérios | Dependências |
|---|---|---|---|
| 630704b0-7141-45e2-9462-84d0737946dd | Conferir as horas que podem entrar na cobrança | CA-1-018, CA-1-019, CA-1-022, CA-1-023, CA-1-024 | T5 |
| 01e77682-eb47-41a0-ad2a-0a589c5abec0 | Gerar o relatório da conferência e medir o tempo de trabalho | CA-1-020, CA-1-021 | T6, T7 |

## Emendas
(nenhuma)


## Orientação de execução — revisão de 10/11/2026

Esta revisão não altera critérios, fórmulas, limites ou o resultado contratado. O código do sistema disponível foi lido no commit 5179d0b, v0.0.7; não foi testado no ambiente do cliente. O estado e o teste humano não se presumem por existir código. Ler os roteiros correspondentes em `04_fase-atual/fase.md` (ou `00-Tasks_Gerais.md` no Plano). Reaproveitar a base, conferir a versão atual e corrigir apenas lacunas. Maestro executa; Bruno/time testam e aprovam. Explicar o que existe, o que falta, por que importa e cada clique com resultado esperado; avisar “olha o Skip agora”. Sem jargão nas interações. Não concluir sem evidência e aceite explícito. Uma tarefa por vez dentro da F1 liberada, sem autorização do consultor por tarefa. Testes técnicos em ambiente próprio isolado e dados fictícios; não acessar banco do cliente nem usar produção. Não alterar campos sensíveis, permissões ou valores por suposição.

`time_records_compute.js` calcula tempo de presença; `registry_contract_rules_check.js` verifica teto e declara que o cálculo completo pertence à task correspondente. Não usar esses resultados nem o CSV de Cobranças como prova de motor faturável ou de relatório comparativo prontos.
