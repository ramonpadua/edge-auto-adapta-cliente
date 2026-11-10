# Sistema EDGE AUTO — Acompanhamento RH e Financeiro

- Repositório do cliente: https://github.com/bperrotta89/Acompanhamento-RH-e-Financeiro
- Submódulo real: `07-sistemas/Acompanhamento-RH-e-Financeiro`.
- Branch de origem: `main`.
- Commit fixado em 10/11/2026: `5179d0b0a57eb0e7f4e8815661d3d64c4b22975d`.
- Versão declarada no package.json: `0.0.7`.
- Ramon informou que o cliente (Bruno Perrotta) construiu este sistema no Skip (React + Vite + TypeScript + PocketBase/Skip Cloud), com páginas de ponto, RH, financeiro e admin. Este repositório é o sistema deles; **consultar seu código antes de construir e reaproveitar a base**. Isso não comprova tarefas concluídas nem teste humano.
- Arquitetura vigente no plano Drive: Skip + Skip Cloud (org do Bruno). Não acessar banco para analisar o sistema.
- O repositório contém um `.env` com `VITE_POCKETBASE_URL` (URL do backend do Skip). É do cliente, não publicado por nós e não usado por nós.

## Inicialização

```bash
git submodule update --init --recursive
```

O submódulo fixa uma versão, fixa o commit `5179d0b`, não acompanha alterações automaticamente. Antes de avaliar atualidade, conferir o remoto sem trocar o ponteiro:

```bash
git -C 07-sistemas/Acompanhamento-RH-e-Financeiro fetch origin
git -C 07-sistemas/Acompanhamento-RH-e-Financeiro log --oneline HEAD..origin/main
```

Atualizar o ponteiro exige decisão explícita e novo commit no repositório de projeto. Acesso ao repo privado do projeto não concede acesso automático ao repo do cliente.

O restante da documentação operacional atual está no Drive: https://drive.google.com/drive/folders/1oLvJ98tzQIuRU78joQP7J7iB4QValiIg . No Google Drive a pasta `07-sistemas` contém a referência; o submódulo Git real fica no GitHub, não é uma cópia dos arquivos no Drive.

## Vínculo Git verificado
Submódulo publicado no repositório do projeto no commit 1628c2d. Clone novo com --recurse-submodules testado com sucesso. No Google Drive esta pasta contém a referência; o submódulo Git real fica no GitHub, não é uma cópia dos arquivos no Drive.
