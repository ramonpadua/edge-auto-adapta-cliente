# SPEC-1-002 — Extração de ponto, upload da planilha do cliente e contrato de semântica de dados

- **Fase**: F1 · **Capacidades**: C3, C4 · **Risco**: obrigatório (API externa, input externo, dado pessoal)
- **Ambiente**: Skip (GoSkip + SkipCloud) — regra geral do consultor (22/09/2026)
- **Degrau da solução**: alimenta os dois lados da comparação (ponto × planilha do cliente) com integridade; elimina a transcrição manual de espelhos PDF e previne o maior risco técnico do Módulo 1 — a quebra por semântica divergente (06:03: "não consegue fazer parametrização de semelhança automática").

## Contexto
- **Estado atual**: RH consulta colaborador por colaborador no Marque Ponto/MarqPonto, gera espelho PDF e transcreve em planilha; financeiro recebe reportes por e-mail; planilha do cliente chega por e-mail em formato livre.
- **Estado desejado**: entrada de ponto por API/export **se provada** (I-03), senão importação manual/lista controlada com a mesma trilha; upload da planilha do cliente validado contra **contrato de semântica de dados** por cliente (mapeamento campo a campo, fail-closed).

## Atores e permissões
- RH/Medição: executa importações/upload; não edita dado importado (só versão nova com motivo).
- Financeiro: consulta e valida.
- Somente operadores autenticados importam; toda importação registra operador.

## Dados
Fonte (API/manual/upload), arquivo (hash, data, operador), linhas importadas (colaborador, H.T., H.E.1, H.E.2, noturno, sáb/dom/fer, HT CONTRATO), campos da planilha do cliente, contrato de semântica (mapa campo→campo por cliente, formatos, unidades).

## Contrato de integração (Marque Ponto/MarqPonto)
- API/export em lote **somente após prova real** (I-03: disponibilidade + formato de saída). Nenhum endpoint, campo ou credencial é presumido.
- Sem prova: modo manual (importação de arquivo/lista controlada) com origem "manual" e mesma auditoria. A superfície nunca alega "integração ativa" sem prova.

## Regras
1. **Fail-closed de layout**: arquivo com layout/colunas divergentes do contrato é rejeitado com relatório de divergência — nada é preenchido por inferência ou semelhança.
2. **Idempotência**: reimportar o mesmo arquivo (hash idêntico) não duplica registros.
3. **Fidelidade**: valores, unidades, casas decimais e operadores são preservados como recebidos; normalização exige regra homologada no contrato.
4. Até I-07 (planilha modelo), a comparação usa fixture sintético; variante não-modelo é sinalizada, não convertida.
5. Importação proibida com dado real antes de I-06 (política) — recusa explícita.

## Fluxo e passos
1. Registrar contrato de semântica do cliente (mapa campo→campo, formatos).
2. Importar ponto (API se provada; senão manual) → validação → carga.
3. Upload da planilha do cliente → validação de layout → carga.
4. Gerar registro de origem (fonte, hash, data, operador) para cada carga.

## Exceções e rollback
- Layout divergente → rejeição + relatório; nada carrega.
- Upload repetido → idempotente, sem duplicidade.
- Carga corrompida → reversão por lote (registro inativado com motivo), nunca edição silenciosa.

## Critérios de aceite (binários)
- **CA-1-006**: entrada de ponto via API/export só ocorre com I-03 provado; caso contrário o modo manual é usado e registra origem "manual" com a mesma trilha de auditoria.
- **CA-1-007**: upload da planilha do cliente é validado contra o contrato de semântica (campo→campo); layout divergente é rejeitado com relatório de divergência e zero linhas carregadas.
- **CA-1-008**: reimportação do mesmo arquivo (hash idêntico) não gera duplicidade (teste com 2 cargas idênticas).
- **CA-1-009**: valores, unidades, casas decimais e operadores são preservados byte a byte do arquivo de origem; nenhum valor é normalizado silenciosamente.
- **CA-1-010**: planilha modelo (I-07) aceita; variante de layout não-modelo sinalizada como "fora do contrato" e não convertida; sem I-07, a validação roda em fixture sintético.
- **CA-1-011**: toda importação gera registro auditável (fonte, arquivo/hash, data, operador, total de linhas aceitas/rejeitadas).

## TDD da SPEC
- **RED**: cenário "upload de planilha com coluna extra/renomeada" → hoje o processo humano aceita e transcreve à mão (sem validação). Prova: fixture de layout divergente carregada sem recusa no fluxo atual documentado.
- **GREEN**: CA-1-006..011 em fixtures sintéticos (planilha modelo 20 linhas + variante divergente + arquivo repetido); prova: recusa com relatório (007), idempotência (008), fidelidade byte a byte (009), registro de origem (011).
- **REGRESSÃO**: cargas sucessivas de meses distintos não se misturam; rollback de lote preserva trilha; sem I-03, nenhuma superfície exibe "API ativa".

## Instruções para o Ethos
- Superfícies: tela/rota de importação de ponto; upload de planilha do cliente; editor de contrato de semântica; relatório de divergência de layout; trilha de importações.
- Fixtures sintéticos: arquivo de ponto modelo, planilha modelo do cliente, variante divergente, duplicado idêntico.
- Insumos embutidos na task: I-03 (API do Marque Ponto — Lucas Machado, "API disponível? formato de saída?"), I-07 (cliente piloto + planilha modelo — Navaar/Lucas com o cliente).
- **Ponto de parada**: se I-03 for negativa, F1 inteira opera no modo manual (previsto no escopo; §10.4 vira urgente e vai ao consultor). Se I-07 não vier, contrato de semântica fica com o fixture e a comparação real espera. Nunca presumir endpoint, campo ou formato.

## Checklist de aceite
- [ ] CA-1-006..011 provados em fixture
- [ ] Prova negativa de fail-closed registrada
- [ ] Zero "integração ativa" sem I-03
- [ ] Teste humano do RH/Medição registrado

## Tasks vinculadas

| ID | Tarefa | Critérios | Dependências |
|---|---|---|---|
| 85b69fe3-d278-41e3-b8cb-24177bc4d3e1 | Trazer os dados de ponto sem repetir registros | CA-1-006, CA-1-008, CA-1-009, CA-1-011 | T1 |
| cb389d03-1401-491f-82f6-e4ecd4dc9edf | Receber a planilha do cliente e avisar quando estiver fora do modelo | CA-1-007, CA-1-010 | T1 |

## Emendas
(nenhuma)


## Orientação de execução — revisão de 10/11/2026

Esta revisão não altera critérios, fórmulas, limites ou o resultado contratado. O código do sistema disponível foi lido no commit 5179d0b, v0.0.7; não foi testado no ambiente do cliente. O estado e o teste humano não se presumem por existir código. Ler os roteiros correspondentes em `04_fase-atual/fase.md` (ou `00-Tasks_Gerais.md` no Plano). Reaproveitar a base, conferir a versão atual e corrigir apenas lacunas. Maestro executa; Bruno/time testam e aprovam. Explicar o que existe, o que falta, por que importa e cada clique com resultado esperado; avisar “olha o Skip agora”. Sem jargão nas interações. Não concluir sem evidência e aceite explícito. Uma tarefa por vez dentro da F1 liberada, sem autorização do consultor por tarefa. Testes técnicos em ambiente próprio isolado e dados fictícios; não acessar banco do cliente nem usar produção. Não alterar campos sensíveis, permissões ou valores por suposição.

Credencial MarqPonto informada como cadastrada em 03/11 não prova conexão. Não cobrar novamente seu valor. Confirmar apenas nome exato/ambiente e viabilidade documentada quando necessário; sem conexão provada, manter o caminho manual previsto e seu rótulo fiel. Gatilho manual de API e eventual antecipação da integração não estão aprovados por esta revisão editorial; não inventar endpoint nem ativar rotina. SharePoint não é integração assumida.
