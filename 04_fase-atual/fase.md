# Fase 1 — Tarefas e testes acompanhados

Execução liberada em 10/11/2026. Revisão baseada no código 5179d0b (v0.0.7), não em teste no ambiente do cliente. 9 tarefas; 0 encerradas nesta revisão. IDs, dependências, critérios e provas originais preservados. Dono da execução: Maestro. Bruno/time: teste e aceite.

## Como o Maestro deve conduzir

Explique em linguagem simples o que existe, o que esta tarefa acrescenta e por que isso ajuda. Execute uma tarefa por vez e apenas as lacunas do sistema existente. Não fale em código, API, coleção, migration ou fixture com o cliente: diga conexão, cadastro, histórico ou exemplo fictício, conforme o caso. Antes do teste, confira os nomes reais das telas e botões; o roteiro abaixo não autoriza inventar controles que ainda não existem. Avise “olha o Skip agora” e dê os cliques, o que preencher e o resultado esperado a cada passo. Só conclua com evidência e aprovação explícita. Não exija nova autorização do consultor por tarefa. Não refaça o sistema nem presuma aceite por existir uma tela.

Testes técnicos somente em ambiente próprio isolado com dados sintéticos. Não conectar ao banco do cliente, nem em homologação. Não usar dado real nem produção nos testes. A navegação e o teste humano são feitos pelo cliente em seu ambiente autorizado. Se faltar regra que o cliente controla, perguntar apenas o que destrava a tarefa. Preserve aceites e provas já registrados, inclusive eventual evidência da call de 27/10, sem inventar novo aceite.

## Tasks

| ID | Task | Dono | Prazo histórico | SPEC | Critérios | Depende de | Prova | Estado |
|---|---|---|---|---|---|---|---|---|
| 1f8bc7fb-f85a-4ed1-9abc-a9d6dc8afbd5 | Conferir e completar o cadastro de clientes, contratos e plantas | @Maestro | 05/10/2026 | SPEC-1-001 | CA-1-001, CA-1-002, CA-1-003 | nenhuma | Resultados do roteiro abaixo + aprovação explícita | Conferir versão atual; teste humano pendente |
| f924d4f2-d6e4-4685-802f-f44f199dbb30 | Organizar o mês de trabalho e conferir quem pode ser liberado | @Maestro | 06/10/2026 | SPEC-1-001 | CA-1-004, CA-1-005 | T1 | Resultados do roteiro abaixo + aprovação explícita | Pendente (T1) |
| 27f82800-9345-4527-bbfd-97a102d07691 | Definir quem pode criar contas e proteger o acesso | @Maestro | a combinar | SPEC-1-001 | CA-1-025 | T1, T2 | Resultados do roteiro abaixo + aprovação explícita | Pendente (T1, T2) |
| 85b69fe3-d278-41e3-b8cb-24177bc4d3e1 | Trazer os dados de ponto sem repetir registros | @Maestro | 07/10/2026 | SPEC-1-002 | CA-1-006, CA-1-008, CA-1-009, CA-1-011 | T1 | Resultados do roteiro abaixo + aprovação explícita | Pendente (T1) |
| cb389d03-1401-491f-82f6-e4ecd4dc9edf | Receber a planilha do cliente e avisar quando estiver fora do modelo | @Maestro | 08/10/2026 | SPEC-1-002 | CA-1-007, CA-1-010 | T1 | Resultados do roteiro abaixo + aprovação explícita | Pendente (T1) |
| 195a6547-bd37-442a-b22a-0dd541b44bfd | Comparar as horas e mostrar quem precisa de conferência | @Maestro | 09/10/2026 | SPEC-1-003 | CA-1-012, CA-1-016 | T3, T4 | Resultados do roteiro abaixo + aprovação explícita | Pendente (T3, T4) |
| f367ac8b-08f6-4e3e-a58e-22287bebb06a | Resolver diferenças com aprovação e histórico | @Maestro | 10/10/2026 | SPEC-1-003 | CA-1-013, CA-1-014, CA-1-015, CA-1-017 | T5 | Resultados do roteiro abaixo + aprovação explícita | Pendente (T5) |
| 630704b0-7141-45e2-9462-84d0737946dd | Conferir as horas que podem entrar na cobrança | @Maestro | 11/10/2026 | SPEC-1-004 | CA-1-018, CA-1-019, CA-1-022, CA-1-023, CA-1-024 | T5 | Resultados do roteiro abaixo + aprovação explícita | Pendente (T5) |
| 01e77682-eb47-41a0-ad2a-0a589c5abec0 | Gerar o relatório da conferência e medir o tempo de trabalho | @Maestro | 12/10/2026 | SPEC-1-004 | CA-1-020, CA-1-021 | T6, T7 | Resultados do roteiro abaixo + aprovação explícita | Pendente (T6, T7) |

As datas acima são históricas. Recombinar os prazos com Bruno; não tratá-las como prazos novos. Ordem: 1 → 2 → 9 → 3 → 4 → 5 → 6 → 7 → 8; dependências formais preservadas, sem execução em paralelo. T8 exige T6 e T7. Fases seguintes não liberadas por esta revisão.

## Tarefa 1 — Conferir e completar o cadastro de clientes, contratos e plantas

<!-- id:1f8bc7fb-f85a-4ed1-9abc-a9d6dc8afbd5 -->

**O que já existe:** Já existe a página Contratos, com cadastro de cliente, contrato, empresas responsáveis, planta, período de validade e limite de horas. Também existem verificações para recusar contrato sem confirmação e para não calcular faturamento quando falta o limite.

**O que o Maestro vai conferir ou completar:** Não reconstruir essa página. Conferir a versão atual e corrigir somente o que faltar. Há um caminho alternativo de cadastro de cliente que pode salvar sem garantir o histórico da alteração. O resultado antigo do teste automático não comprova esta versão; antes de pedir o teste humano, demonstrar que um cadastro não fica sem histórico. Isso é correção do cadastro existente, não uma nova função.

**Por que importa:** Garantir que cada contrato tenha responsáveis definidos e que o sistema não invente um limite de horas nem apresente valores sem base.

**O que precisamos de vocês:** Perguntar quem é a empresa que emprega e quem emite a cobrança, quem confere esses dados e qual documento informa o limite por planta. Enquanto não houver resposta, usar exemplos fictícios; não transformar exemplo em regra real.

**Antes de começar:** Nenhuma; retomar a conferência do que já existe.

**Teste humano, acompanhado pelo Maestro:**
1. O Maestro explica o que já existe e o que foi corrigido. Diz 'olha o Skip agora' e indica os cliques exatos da página Contratos que conferiu na versão atual, sem pedir comandos ou termos técnicos ao Bruno.
2. Prepare com o Maestro dois clientes e três plantas fictícias, como previsto no teste. Com um cliente fictício, tente cadastrar contrato sem confirmar as empresas responsáveis. Esperado: o sistema recusa e explica o motivo. Depois confirme apenas os dados fictícios de teste e repita. Esperado: cadastro permitido, com registro de quem fez, quando e por quê.
3. Cadastre uma regra de uma planta fictícia com período definido e deixe o limite de horas em branco. Esperado: campo continua vazio, sem aparecer 187:30, 183:30 ou outro limite automaticamente.
4. Use a verificação de faturamento disponível nessa regra. O Maestro deve apontar o nome exato do botão existente antes do clique. Esperado: 'em conferência — teto não provado', sem número de horas faturáveis ou valor. Com limite fictício confirmado, não exigir cálculo completo: isso pertence à tarefa 7.
5. Confira o histórico do cadastro com ajuda do Maestro. Esperado: cada alteração permitida tem autor, data e motivo. O Maestro apresenta também a prova técnica, em ambiente isolado, de que falha no histórico não deixa um cadastro salvo sem rastro.
6. Envie prints ou descrição dos resultados e diga explicitamente se testou e aprovou. Se algo falhar, a tarefa permanece aberta e o Maestro corrige apenas esse ponto antes de repetir o teste.

**Quando parar e quando concluir:** Só concluir após conferir a versão atual, apresentar as provas e receber o aceite explícito de Bruno. Se o teste de 27/10 já foi registrado, localizar a evidência, preservar esse aceite e testar somente o que mudou; não exigir a repetição sem explicar a razão.

**Prova:** registrar o que foi tentado, o esperado, o resultado e print ou relato de cada passo; juntar a prova técnica separadamente. Só concluir com confirmação explícita de quem testou. O silêncio não é aprovação.

**Referência para o Maestro (não precisa ser explicada em termos técnicos ao cliente):** SPEC-1-001; CA-1-001, CA-1-002, CA-1-003. Estado: em conferência da implementação atual; teste humano pendente, aceite anterior não presumido.

## Tarefa 2 — Organizar o mês de trabalho e conferir quem pode ser liberado

<!-- id:f924d4f2-d6e4-4685-802f-f44f199dbb30 -->

**O que já existe:** Existe o Painel RH, com registros de ponto e filtros. Essa tela pode ser aproveitada como entrada para o trabalho do mês, mas listar pontos não é o mesmo que organizar e liberar o mês de medição.

**O que o Maestro vai conferir ou completar:** Completar o controle do mês com lista de colaboradores, documentos esperados, etapas, marcos do mês (acontecimentos e datas que precisam ser acompanhados) e histórico das mudanças. Não substituir o Painel RH nem confundir o status de um ponto com o andamento do mês inteiro.

**Por que importa:** Mostrar o que falta conferir antes de liberar o fechamento, sem deixar alguém esquecido.

**O que precisamos de vocês:** Confirmar com Bruno/RH quais pessoas e documentos entram no mês de exemplo. Usar dez colaboradores fictícios para a demonstração; não importar pessoas reais.

**Antes de começar:** Tarefa(s) 1 testada(s) e aprovada(s).

**Teste humano, acompanhado pelo Maestro:**
1. O Maestro mostra onde o controle do mês foi acrescentado e explica: 'competência é o mês que estamos conferindo'. Depois diz 'olha o Skip agora' e informa o caminho real da tela.
2. Abra um mês de demonstração com dez colaboradores fictícios. Esperado: mês, lista de pessoas, documentos esperados, marcos do mês com suas datas e etapa atual visíveis. O Maestro explica como registrar e consultar esses acontecimentos sem inventar datas.
3. Deixe um colaborador sem situação definida e tente liberar o mês. Esperado: bloqueio claro mostrando quem ainda precisa de conferência.
4. Defina a situação de cada pessoa com uma opção permitida: conferido, divergência justificada, excluído com motivo ou pendência assumida por responsável. Esperado: o sistema deixa claro qual foi a escolha; não resolve sozinho.
5. Mude a etapa do mês e confira o histórico. Esperado: uma única etapa atual e registro de quem mudou, quando e por quê; mudança de etapa não apaga registros antigos.
6. Registre o resultado e confirme explicitamente se testou e aprovou. Se falhar, permaneça nesta tarefa.

**Quando parar e quando concluir:** Não começar antes do aceite da tarefa 1. Só concluir com prova do bloqueio, do histórico e teste aprovado; não antecipar aprovação do cliente nem faturamento automático.

**Prova:** registrar o que foi tentado, o esperado, o resultado e print ou relato de cada passo; juntar a prova técnica separadamente. Só concluir com confirmação explícita de quem testou. O silêncio não é aprovação.

**Referência para o Maestro (não precisa ser explicada em termos técnicos ao cliente):** SPEC-1-001; CA-1-004, CA-1-005. Estado: pendente das dependências e do teste humano.

## Tarefa 9 — Definir quem pode criar contas e proteger o acesso

<!-- id:27f82800-9345-4527-bbfd-97a102d07691 -->

**O que já existe:** Já existem login, cadastro público e página Usuários para administrar contas. O login ainda mostra 'Criar conta' e a rota de cadastro continua disponível.

**O que o Maestro vai conferir ou completar:** Aproveitar a página Usuários e as contas existentes. Remover a criação pública e permitir novas contas somente por pessoas autorizadas, com a proteção valendo também fora da tela e com histórico de criação.

**Por que importa:** Evitar que alguém crie acesso por conta própria, sem deixar o time atual sem entrar.

**O que precisamos de vocês:** Antes de mudar qualquer permissão, Bruno precisa dizer quais pessoas ou perfis podem criar contas. Não presumir que todos sejam administradores. O Maestro não pede senha nem chave no chat.

**Antes de começar:** Tarefa(s) 1, 2 testada(s) e aprovada(s).

**Teste humano, acompanhado pelo Maestro:**
1. Depois de Bruno definir quem pode criar contas, o Maestro explica a regra em uma frase, mostra o que mudou e diz 'olha o Skip agora'. Não prosseguir com a regra indefinida.
2. Abra a tela de login sem entrar. Esperado: não existe botão 'Criar conta'. Tente também o endereço antigo de cadastro indicado pelo Maestro. Esperado: não conseguir criar conta por esse caminho.
3. Entre com uma conta já existente e autorizada. Esperado: o acesso continua funcionando. O próprio usuário digita sua senha, sem enviá-la ao Maestro.
4. Na página Usuários, a pessoa autorizada cria uma conta fictícia de teste. Esperado: criação permitida e registro de quem criou e quando.
5. Com uma conta sem permissão, tente a mesma ação. Esperado: criação recusada. O Maestro apresenta também a prova técnica em ambiente isolado de que chamar a operação fora da tela não burla a proteção.
6. Confira que as contas existentes continuam preservadas, registre os resultados e confirme explicitamente se testou e aprovou.

**Quando parar e quando concluir:** Só começar após os aceites das tarefas 1 e 2 e a resposta de Bruno sobre quem cria contas. Não apagar contas, trocar senhas ou ampliar permissões por conveniência.

**Prova:** registrar o que foi tentado, o esperado, o resultado e print ou relato de cada passo; juntar a prova técnica separadamente. Só concluir com confirmação explícita de quem testou. O silêncio não é aprovação.

**Referência para o Maestro (não precisa ser explicada em termos técnicos ao cliente):** SPEC-1-001; CA-1-025. Estado: pendente das dependências e do teste humano.

## Tarefa 3 — Trazer os dados de ponto sem repetir registros

<!-- id:85b69fe3-d278-41e3-b8cb-24177bc4d3e1 -->

**O que já existe:** Já existem Registrar Ponto, Meus Pontos, Painel RH e o cálculo básico do tempo entre entrada e saída. Isso não comprova importação dos arquivos do MarqPonto nem conexão com ele.

**O que o Maestro vai conferir ou completar:** Acrescentar a entrada controlada dos dados de ponto, aproveitando as telas e serviços existentes quando compatíveis. Guardar a origem da carga e impedir que o mesmo arquivo gere registros repetidos.

**Por que importa:** Evitar redigitação e duplicidade sem perder a possibilidade de saber de onde vieram as horas.

**O que precisamos de vocês:** A credencial do MarqPonto foi informada como cadastrada no Skip Cloud. Não pedir a chave novamente nem expor seu valor no chat. Quando a conexão for avaliada, pedir somente o nome cadastrado, o ambiente onde está e a documentação necessária. Credencial salva não é conexão funcionando: sem prova de viabilidade e autorização, demonstrar a entrada manual prevista, com arquivo fictício e rótulo de entrada manual.

**Antes de começar:** Tarefa(s) 1 testada(s) e aprovada(s).

**Teste humano, acompanhado pelo Maestro:**
1. O Maestro explica se a entrada demonstrada é por arquivo ou por uma conexão comprovada. Para o caminho por arquivo, diz 'olha o Skip agora' e mostra os cliques reais para escolher o arquivo de exemplo.
2. Envie um arquivo fictício de ponto preparado pelo Maestro. Esperado: dados carregados com origem, data e responsável visíveis; se houver rejeição, o motivo deve aparecer.
3. Confira algumas linhas com o arquivo original: pessoa fictícia, data, horas, unidades e sinais. Esperado: nenhum valor alterado ou arredondado sem a regra prevista.
4. Envie exatamente o mesmo arquivo uma segunda vez. Esperado: nenhum registro novo duplicado e mensagem explicando que aquela carga já foi recebida.
5. Abra o registro da importação. Esperado: origem, arquivo, identificação da carga, data e responsável. Entrada por arquivo deve aparecer como manual, nunca como integração ativa.
6. Registre os resultados e confirme explicitamente se testou e aprovou. Uma credencial cadastrada ou uma tela de ponto funcionando, sozinhas, não aprovam esta tarefa.

**Quando parar e quando concluir:** Não começar antes do aceite da tarefa 1. Sem conexão provada, manter o caminho manual; não criar promessa de sincronização, disparo automático ou integração SharePoint.

**Prova:** registrar o que foi tentado, o esperado, o resultado e print ou relato de cada passo; juntar a prova técnica separadamente. Só concluir com confirmação explícita de quem testou. O silêncio não é aprovação.

**Referência para o Maestro (não precisa ser explicada em termos técnicos ao cliente):** SPEC-1-002; CA-1-006, CA-1-008, CA-1-009, CA-1-011. Estado: pendente das dependências e do teste humano.

## Tarefa 4 — Receber a planilha do cliente e avisar quando estiver fora do modelo

<!-- id:cb389d03-1401-491f-82f6-e4ecd4dc9edf -->

**O que já existe:** Há cadastro de contratos e clientes que pode identificar a quem pertence o arquivo. Não foi localizada uma entrada da planilha do cliente com a validação prevista.

**O que o Maestro vai conferir ou completar:** Acrescentar o envio da planilha e a comparação das colunas e significados com o modelo combinado. Reaproveitar os cadastros, sem criar outra base de clientes.

**Por que importa:** Evitar comparar horas ou valores errados porque uma planilha veio com colunas ou significados diferentes.

**O que precisamos de vocês:** Confirmar o cliente piloto e o modelo de planilha. Se o modelo real já estiver no contexto, usar o que foi entregue, sem cobrar de novo. Até a liberação de dados reais, testar com cópia fictícia de mesma estrutura.

**Antes de começar:** Tarefa(s) 1 testada(s) e aprovada(s).

**Teste humano, acompanhado pelo Maestro:**
1. O Maestro apresenta o modelo de teste e explica em palavras simples o que cada coluna significa. Depois diz 'olha o Skip agora' e indica os cliques reais para enviar a planilha.
2. Selecione o contrato fictício e envie a planilha fictícia no modelo correto. Esperado: a entrada é aceita e identificada para aquele contrato.
3. Envie outra versão com uma coluna obrigatória faltando ou com significado diferente. Esperado: rejeição explicada e nenhuma linha dessa versão importada.
4. Confira o aviso da rejeição. Esperado: mostrar o que precisa corrigir, sem tentar adivinhar ou transformar uma coluna em outra por semelhança do nome.
5. Volte à versão válida e confira os valores carregados. Esperado: origem preservada, sem misturar o arquivo rejeitado com o aceito.
6. Registre os resultados e confirme explicitamente se testou e aprovou.

**Quando parar e quando concluir:** Não começar antes do aceite da tarefa 1. Sem modelo aprovado, mostrar somente demonstração fictícia e explicar que a comparação real ainda depende desse modelo.

**Prova:** registrar o que foi tentado, o esperado, o resultado e print ou relato de cada passo; juntar a prova técnica separadamente. Só concluir com confirmação explícita de quem testou. O silêncio não é aprovação.

**Referência para o Maestro (não precisa ser explicada em termos técnicos ao cliente):** SPEC-1-002; CA-1-007, CA-1-010. Estado: pendente das dependências e do teste humano.

## Tarefa 5 — Comparar as horas e mostrar quem precisa de conferência

<!-- id:195a6547-bd37-442a-b22a-0dd541b44bfd -->

**O que já existe:** O Painel RH já lista pontos e permite filtros. Isso ajuda na navegação, mas não faz as duas comparações de medição previstas no projeto.

**O que o Maestro vai conferir ou completar:** Acrescentar a conferência por colaborador, aproveitando o Painel RH: uma comparação dos dados internos com o contrato e outra com a planilha do cliente. Não confundir atraso de entrada com divergência de medição.

**Por que importa:** Encontrar rapidamente quem está de acordo, quem tem diferença e quem ainda não tem informação suficiente.

**O que precisamos de vocês:** Usar o modelo e as regras já confirmados. Se houver vídeos do processo no contexto, consultá-los antes de perguntar; pedir apenas a dúvida que ainda altera a comparação.

**Antes de começar:** Tarefa(s) 3, 4 testada(s) e aprovada(s).

**Teste humano, acompanhado pelo Maestro:**
1. O Maestro explica os dois lados da conferência, mostra as telas acrescentadas e diz 'olha o Skip agora'. Deve indicar os cliques reais, sem pedir que Bruno interprete nomes de campos técnicos.
2. Abra o mês fictício com dez pessoas: quatro sem diferença, três com diferença, duas pendentes e uma sem informação correspondente. Esperado: os dez casos aparecem com situação e valores visíveis.
3. Abra uma pessoa sem diferença e outra com diferença. Esperado: ver lado a lado os números que justificam cada situação.
4. Confira separadamente a comparação interna com o contrato e a comparação com a planilha do cliente. Esperado: valores e regras de uma não são usados como se fossem da outra.
5. Retire uma informação do exemplo preparado para esse teste. Esperado: pendência explicada, nunca um resultado inventado para preencher a falta.
6. Registre os resultados e confirme explicitamente se testou e aprovou.

**Quando parar e quando concluir:** Só começar depois dos aceites das tarefas 3 e 4. A tela mostrar registros de ponto não basta: provar as duas comparações sem decidir divergências automaticamente.

**Prova:** registrar o que foi tentado, o esperado, o resultado e print ou relato de cada passo; juntar a prova técnica separadamente. Só concluir com confirmação explícita de quem testou. O silêncio não é aprovação.

**Referência para o Maestro (não precisa ser explicada em termos técnicos ao cliente):** SPEC-1-003; CA-1-012, CA-1-016. Estado: pendente das dependências e do teste humano.

## Tarefa 6 — Resolver diferenças com aprovação e histórico

<!-- id:f367ac8b-08f6-4e3e-a58e-22287bebb06a -->

**O que já existe:** O Painel RH já tem ações sobre justificativas e pontos. Essas ações devem ser aproveitadas quando compatíveis, mas editar ou apagar um registro não comprova o histórico completo exigido para a medição.

**O que o Maestro vai conferir ou completar:** Completar a fila de diferenças com decisão humana, motivo, origem e versões anteriores preservadas. Não apagar ou sobrescrever o dado original para fazer o número parecer correto.

**Por que importa:** Permitir correções sem perder a prova do que aconteceu e de quem decidiu.

**O que precisamos de vocês:** Perguntar quem pode decidir cada tipo de ajuste se isso ainda não estiver documentado. Não assumir que qualquer pessoa pode aprovar.

**Antes de começar:** Tarefa(s) 5 testada(s) e aprovada(s).

**Teste humano, acompanhado pelo Maestro:**
1. O Maestro mostra uma diferença fictícia que veio da tarefa 5, explica a decisão que cabe à pessoa e diz 'olha o Skip agora', indicando o caminho real da tela.
2. Tente resolver a diferença sem informar de onde veio a correção. Esperado: recusa com motivo claro.
3. Deixe uma solicitação sem aprovação. Esperado: continua pendente; o Maestro apresenta também a prova de que esperar 24 horas não aprova sozinho, sem exigir que Bruno aguarde um dia para testar.
4. Aprove uma correção fictícia com motivo. Esperado: nova versão com quem decidiu, quando e por quê; versão anterior permanece consultável.
5. Abra um caso sem reporte. Esperado: 'pendente — reporte ausente', com responsável visível, sem preenchimento inventado.
6. Registre os resultados e confirme explicitamente se testou e aprovou.

**Quando parar e quando concluir:** Só começar depois do aceite da tarefa 5. Não usar exclusão como correção; sem decisão humana, manter pendente.

**Prova:** registrar o que foi tentado, o esperado, o resultado e print ou relato de cada passo; juntar a prova técnica separadamente. Só concluir com confirmação explícita de quem testou. O silêncio não é aprovação.

**Referência para o Maestro (não precisa ser explicada em termos técnicos ao cliente):** SPEC-1-003; CA-1-013, CA-1-014, CA-1-015, CA-1-017. Estado: pendente das dependências e do teste humano.

## Tarefa 7 — Conferir as horas que podem entrar na cobrança

<!-- id:630704b0-7141-45e2-9462-84d0737946dd -->

**O que já existe:** Já existe verificação do limite do contrato, cálculo básico entre entrada e saída e uma página Cobranças. O cálculo de presença e os valores lançados em Cobranças não são o cálculo contratual de horas faturáveis.

**O que o Maestro vai conferir ou completar:** Completar o cálculo a partir das horas conferidas e das regras de cada contrato. Reaproveitar cadastros e proteção de limite; não aplicar percentuais universais nem criar outra tela de cobranças sem necessidade.

**Por que importa:** Evitar cobrar horas sem regra comprovada ou usar a regra de um cliente para outro.

**O que precisamos de vocês:** Financeiro informa a regra e o documento do limite. Sem confirmação, manter o caso em conferência. Até a política de dados estar aprovada, usar exemplos fictícios; nenhum dado real de empregado ou cliente.

**Antes de começar:** Tarefa(s) 5 testada(s) e aprovada(s).

**Teste humano, acompanhado pelo Maestro:**
1. O Maestro mostra duas regras fictícias de contrato, explica a conta esperada em uma tabela simples e diz 'olha o Skip agora', apontando os cliques reais.
2. Use as mesmas horas de exemplo nos dois contratos com regras diferentes. Esperado: resultados diferentes conforme as regras, incluindo hora extra 1, hora extra 2, adicional noturno, sábado, domingo e feriado conforme cada regra de exemplo, sem copiar uma porcentagem fixa para todos.
3. Deixe o limite sem comprovação. Esperado: 'em conferência — teto não provado', sem itens marcados como prontos para cobrar.
4. Use limite fictício confirmado e horas acima dele. Esperado: aviso do excesso e necessidade de conferência humana, nunca liberação automática.
5. O Maestro demonstra em ambiente isolado a recusa de uso real antes da política. Bruno confere o aviso com exemplo fictício marcado para esse teste; não inserir dado real para provar o bloqueio.
6. Altere um valor fictício com motivo e consulte o histórico. Esperado: autor, data e motivo, preservando o que foi alterado. Confira também se entradas manuais estão identificadas como manuais.
7. Registre os resultados e confirme explicitamente se testou e aprovou.

**Quando parar e quando concluir:** Só começar após o aceite da tarefa 5. Sem regra ou limite provado, não liberar cálculo real. Não converter hoursWorked ou um valor em Cobranças em prova de faturamento correto.

**Prova:** registrar o que foi tentado, o esperado, o resultado e print ou relato de cada passo; juntar a prova técnica separadamente. Só concluir com confirmação explícita de quem testou. O silêncio não é aprovação.

**Referência para o Maestro (não precisa ser explicada em termos técnicos ao cliente):** SPEC-1-004; CA-1-018, CA-1-019, CA-1-022, CA-1-023, CA-1-024. Estado: pendente das dependências e do teste humano.

## Tarefa 8 — Gerar o relatório da conferência e medir o tempo de trabalho

<!-- id:01e77682-eb47-41a0-ad2a-0a589c5abec0 -->

**O que já existe:** A página Cobranças já tem uma exportação de sua própria lista. Essa exportação pode inspirar o reaproveitamento da interface, mas não é o relatório comparativo de ponto e planilha do cliente.

**O que o Maestro vai conferir ou completar:** Completar o relatório por mês, planta e pessoa, mostrando os dois lados, diferenças e origem; acrescentar o registro de tempo de trabalho com método e período de medição.

**Por que importa:** Ter uma entrega que o time consegue conferir e apresentar, além de medir se o processo ficou mais rápido sem inventar ganho.

**O que precisamos de vocês:** Perguntar quanto tempo o processo leva hoje e em qual período foi medido. Se não houver histórico, começar a registrar da primeira medição válida; simulação fica identificada como simulação, nunca como ganho real.

**Antes de começar:** Tarefa(s) 6, 7 testada(s) e aprovada(s).

**Teste humano, acompanhado pelo Maestro:**
1. O Maestro apresenta um mês fictício já conferido, explica o conteúdo do relatório e diz 'olha o Skip agora', apontando os cliques reais para gerar.
2. Gere o relatório e filtre por planta e pessoa. Esperado: números dos dois lados, diferenças e origens coerentes com as telas anteriores.
3. Exporte e abra o arquivo. Esperado: os mesmos dados e filtros, leitura compreensível e identificação do mês. A lista financeira de Cobranças sozinha não atende a este teste.
4. Gere novamente sem alterar os dados. Esperado: mesmo conteúdo, sem duplicar lançamentos nem alterar o fechamento.
5. Registre o período e o modo de medir o tempo de conciliação e os intervalos envio-aprovação e aprovação-pagamento. Esperado: campo sem medição fica sem número e com ressalva, não recebe estimativa automática.
6. Registre os resultados e confirme explicitamente se testou e aprovou. Medição fictícia serve para testar a tela, não para declarar economia real.

**Quando parar e quando concluir:** Só começar após os aceites das tarefas 6 e 7. Não encerrar a fase nem abrir a fase 2 automaticamente; apresentar evidências para a transição.

**Prova:** registrar o que foi tentado, o esperado, o resultado e print ou relato de cada passo; juntar a prova técnica separadamente. Só concluir com confirmação explícita de quem testou. O silêncio não é aprovação.

**Referência para o Maestro (não precisa ser explicada em termos técnicos ao cliente):** SPEC-1-004; CA-1-020, CA-1-021. Estado: pendente das dependências e do teste humano.

