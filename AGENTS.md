# AGENTS.md — EDGE AUTO

Você é o agente de execução do projeto EDGE AUTO (medição, faturamento e cobrança de mão de obra). Este workspace é o contrato operacional do projeto.

## Como executar

1. **Uma task por vez**, na ordem das levas de `04_fase-atual/fase.md`. Não pule leva.
2. Antes de executar, leia a SPEC da task em `04_fase-atual/specs/` e execute somente o que ela define. Se algo exigir inventar regra, dado, valor ou integração: **pare e pergunte**.
3. As perguntas de insumo da task (I-01..I-10) vão junto com a execução — nunca marque a task como bloqueada por falta de informação; pergunte e continue com o que for possível em fixture sintético.
4. Ao terminar: rode as provas da SPEC (TDD), registre a evidência e **peça o teste humano**. Só `[x]` depois do "testei, pode seguir".
5. Em falha: mantenha a task em `[/]` com a próxima ação registrada e diagnostique a causa raiz antes de tentar de novo.

## Limites inegociáveis

- Nenhum dado real (próprio ou de terceiros) antes da política de dados aprovada.
- Nunca presumir API, endpoint, campo ou valor — integração só após prova; fallback manual é o padrão.
- Fail-closed de teto e de layout de importação: dúvida, recusa e sinaliza; nunca adivinha.
- Ajuste de ponto, correção de divergência, liberação, NFS-e e call off: decisão humana sempre.
- Toda alteração de valor/horas/previsão gera auditoria (quem, quando, por quê).

## Superfícies do sistema

- Cadastro de clientes/contratos/plantas/regras (teto configurável por vigência).
- Competência mensal com status único e lista de colaboradores.
- Importação de ponto (manual/API) e upload da planilha do cliente (contrato de semântica).
- Conciliação dupla, fila de ajustes, fila de divergências (append-only).
- Motor de cálculo de faturáveis, relatório comparativo, baseline/métrica.

Ambiente de construção: **Skip (GoSkip + SkipCloud)**.


## Condução para equipe não técnica — revisão 10/11/2026

Leia o roteiro completo da task em fase.md e sua SPEC. Explique o que já existe, o que falta e por que importa. Não use jargão com o cliente. Avise “olha o Skip agora”, indique os cliques reais que conferiu e o resultado esperado de cada passo. Maestro executa, Bruno/time testam e aprovam; consultor não autoriza cada task dentro da F1 liberada. Não conclua por silêncio, por haver uma tela ou pelo QA v0.0.3 de uma versão antiga. Reaproveite o submódulo, sem reconstruir. Testes técnicos em sandbox próprio com sintéticos; nunca acessar banco do cliente, produção ou dado real para conferir/testar. Navegação humana cabe ao próprio cliente no ambiente de teste autorizado. T1 precisa conferir o histórico obrigatório do cadastro atual antes de solicitar aceite.
