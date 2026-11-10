# SPEC-1-001 — Cadastro operacional e competência mensal

- **Fase**: F1 (Módulo 1 — Extração e Conciliação) · **Capacidades**: C1, C2 · **Prioridade**: ≤3 calls
- **Ambiente**: Skip (GoSkip + SkipCloud) — regra geral do consultor (22/09/2026)
- **Degrau da solução**: primeiro degrau — sem cadastro único de clientes/contratos/plantas/regras e sem a competência mensal como container do ciclo, nenhuma conciliação é possível. Troca a navegação por pastas/planilhas por um cadastro consultável.

## Contexto

- **Estado atual**: controles dispersos em planilhas (SharePoint/Excel), regras contratuais em memória das responsáveis, teto de horas em conflito (187:30 × 183:30), entidade empregadora/faturamento não confirmada (EEP DATA MANAGEMENT × EDGE AUTO).
- **Estado desejado**: cadastro de cliente (com entidade), projeto/planta, regra de medição e **teto configurável** por cliente/projeto/planta/vigência (nenhum valor padrão); competência mensal com status único e lista de colaboradores/documentos esperados.

## Atores e permissões
- RH/Medição (Meire): cadastra operacional, abre competência, mantém lista de colaboradores.
- Financeiro (Renata): consulta; valida dados contratuais (teto, entidade).
- CEO/Liderança: consulta.
- Nenhuma alteração de cadastro sem registro de autoria (quem/quando/por quê).

## Dados
Cliente, entidade empregadora/faturamento, projeto/comprador, planta (Anchieta, Curitiba, Taubaté…), vigência da regra, teto de horas (nullable), colaborador (nome, PT, área), competência (período, status), documentos esperados.

## Regras
1. Contrato só é cadastrado com entidade confirmada (I-09) — sem confirmação, recusa explícita com motivo.
2. Teto é campo configurável; **nunca** fixado em 187:30 ou 183:30 por padrão (DH-04).
3. Sem teto, o cálculo de faturáveis retorna "em conferência — teto não provado" (fail-closed).
4. Competência tem status único entre: em preparação · aguardando documentos · em conciliação · com divergência · liberada internamente · enviada ao cliente · aguardando aprovação · aprovada · faturada · aguardando pagamento · paga · cancelada/refaturamento em análise.
5. Nenhuma competência avança para liberação com colaborador sem situação definida.

## Fluxo e passos
1. Cadastrar cliente/entidade (com I-09 embutido: "qual entidade emprega e qual fatura cada contrato?").
2. Cadastrar projeto/planta/regra/vigência/teto (I-04 embutido: "trazer a cláusula/planilha contratual com o teto por planta").
3. Abrir competência → lista de colaboradores + documentos esperados + marcos.
4. Manter status por transição auditada.

## Exceções e rollback
- Entidade não confirmada → cadastro de contrato bloqueado com motivo (não é gate do projeto: a task pergunta e segue em fixture).
- Teto divergente entre fontes → cadastra como "em disputa", cálculo fail-closed.
- Exclusão nunca física: cadastro inativado com histórico.

## Critérios de aceite (binários)
- **CA-1-001**: contrato só cadastra com entidade empregadora/faturamento confirmada; sem isso, recusa com motivo registrado.
- **CA-1-002**: teto de horas é configurável por cliente/projeto/planta/vigência, sem valor padrão; a tela de regra exibe a vigência.
- **CA-1-003**: com teto vazio, qualquer tentativa de calcular faturável retorna "em conferência — teto não provado" (nunca número).
- **CA-1-004**: abrir competência cria ciclo com status único, lista de colaboradores, documentos esperados e marcos; cada transição de status é auditada (quem/quando/por quê).
- **CA-1-005**: sistema recusa liberar competência com colaborador sem situação definida (conciliado / divergente justificado / excluído / pendente assumido), com bloqueio explícito em tela.

## TDD da SPEC
- **RED**: cenário "criar contrato sem entidade confirmada" → sistema aceita hoje (não existe sistema; controle é planilha). Prova: registro da tentativa em fixture mostra aceitação sem validação.
- **GREEN**: CA-1-001..005 verificados em fixture sintética (2 clientes, 3 plantas, 1 competência); prova: recusa com motivo (001), campo teto vazio salvo sem default (002), resposta "em conferência" (003), transição auditada (004), bloqueio de liberação (005).
- **REGRESSÃO**: reabrir/fechar competência e reeditar teto preservam histórico; nenhuma alteração destrutiva.

## Instruções para o Ethos
- Superfícies: cadastro de cliente/contrato/regra; tela de competência; lista de colaboradores; trilha de auditoria.
- Dados de demonstração: fixtures sintéticos (nada real até I-06); nomes fictícios; teto vazio ou fictício.
- Insumos embutidos na task (perguntas junto com a execução): I-01 (aceite do núcleo — Bruno/Ricardo), I-04 (teto — Renata/contrato), I-09 (entidade — Bruno/Financeiro), I-10 (champion/RACI — liderança).
- **Ponto de parada**: se I-09 não vier, mantém cadastro de contrato bloqueado com motivo e segue com fixture; se I-04 não vier, teto vazio + fail-closed. Nunca inventar valor, entidade ou regra.

## Checklist de aceite
- [ ] CA-1-001..005 provados em fixture
- [ ] Auditoria de transições visível
- [ ] Nenhum dado real presente
- [ ] Teste humano do RH/Medição registrado

## Tasks vinculadas

| ID | Tarefa | Critérios | Dependências |
|---|---|---|---|
| 1f8bc7fb-f85a-4ed1-9abc-a9d6dc8afbd5 | Conferir e completar o cadastro de clientes, contratos e plantas | CA-1-001, CA-1-002, CA-1-003 | nenhuma |
| f924d4f2-d6e4-4685-802f-f44f199dbb30 | Organizar o mês de trabalho e conferir quem pode ser liberado | CA-1-004, CA-1-005 | T1 |
| 27f82800-9345-4527-bbfd-97a102d07691 | Definir quem pode criar contas e proteger o acesso | CA-1-025 | T1, T2 |

## Emendas
- **E-2710-01 (27/10/2026, pedido do consultor Ramon Pádua)**: criação de contas sai do login público e passa para a página de gestão administrativa restrita. Botão "Criar conta" removido do login; criação de contas fica na página administrativa, restrita por controle no servidor (além de ocultar a UI) e com registro de auditoria (quem criou/quando). Contas existentes preservadas sem alteração. Emenda documental em 27/10: naquela data houve apenas publicação documental, sem implementação. Com a F1 liberada em 10/11, a T9 agora inclui a implementação da proteção descrita — sempre após T1 e T2 aceitas e com a resposta do Bruno (I-11) sobre quem cria contas.
- **Pergunta obrigatória (I-11, a responder por Bruno ANTES de definir a permissão): quais pessoas e perfis poderão criar contas — a política de acesso não é definida enquanto essa resposta não existir; não presumir que todos serão administradores.** A permissão de criação de contas não é definida antes dessa resposta; até lá a página administrativa fica restrita ao perfil já existente que o Bruno indicar, sem ampliar acesso.
- **CA-1-025 (emenda)**: login não exibe botão "Criar conta"; criação de contas só ocorre na página de gestão administrativa restrita, com permissão verificada no servidor e auditoria (quem/quando); contas existentes permanecem válidas. Teste humano: permitido (exercer a prova no preview).
- **Prova negativa (emenda)**: tentativa de criar conta fora da página restrita (ou sem permissão no servidor) é recusada; contas existentes continuam autenticando.
- **Dependência**: a task 9 é inserida na Jornada após a task 2 e só começa com as tasks 1 e 2 concluídas e aceitas (T1 e T2).
- **Prazo**: a combinar com o Bruno na liberação (não fixado nesta emenda).
- **Critérios CA-1-001..005 e provas da SPEC permanecem inalterados; CA-1-006 continua pertencendo à SPEC-1-002 (importação de ponto).**


## Orientação de execução — revisão de 10/11/2026

Esta revisão não altera critérios, fórmulas, limites ou o resultado contratado. O código do sistema disponível foi lido no commit 5179d0b, v0.0.7; não foi testado no ambiente do cliente. O estado e o teste humano não se presumem por existir código. Ler os roteiros correspondentes em `04_fase-atual/fase.md` (ou `00-Tasks_Gerais.md` no Plano). Reaproveitar a base, conferir a versão atual e corrigir apenas lacunas. Maestro executa; Bruno/time testam e aprovam. Explicar o que existe, o que falta, por que importa e cada clique com resultado esperado; avisar “olha o Skip agora”. Sem jargão nas interações. Não concluir sem evidência e aceite explícito. Uma tarefa por vez dentro da F1 liberada, sem autorização do consultor por tarefa. Testes técnicos em ambiente próprio isolado e dados fictícios; não acessar banco do cliente nem usar produção. Não alterar campos sensíveis, permissões ou valores por suposição.

Na T1, conferir a regressão possível em `src/services/registry.ts`: o cadastro alternativo tenta gravar histórico separadamente e ignora sua falha; `0006_allow_clients_create.js` abre gravação direta. A regra já existente de autoria obrigatória deve continuar verdadeira. O QA v0.0.3 não prova a versão 0.0.7. Sem garantia de histórico, corrigir a lacuna e testar em sandbox antes do teste humano. Não apagar ou desfazer registros existentes para provar o teste. A T9 reaproveita Usuários e mantém a dependência T1+T2; a definição de quem cria contas continua sendo do Bruno (I-11).
