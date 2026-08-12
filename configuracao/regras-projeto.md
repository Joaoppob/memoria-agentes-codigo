# Regras de projeto, Nortada

Escopo: convenções que só fazem sentido dentro do repositório do Nortada, além das regras
gerais de Python descritas em `regras-python.md`.

## Estrutura de pastas

```
src/nortada/
  api/       rotas FastAPI, um arquivo por recurso
  core/      regra de negócio, sem dependência de FastAPI
  db/        modelos SQLAlchemy, sessão, migrações Alembic
  workers/   tarefas assíncronas (fila de e-mail, reconciliação com o Stripe)
```

A dependência entre pastas corre numa direção só: `api` chama `core`, `core` não importa nada
de `api`. Se um dia `core` precisar saber de algo da camada HTTP, o design está errado, não a
regra.

## Nomenclatura de arquivo

Todo arquivo do repositório em kebab-case, com uma exceção inescapável: módulo Python usa
snake_case, porque é o único formato que o próprio interpretador aceita como identificador de
import. Arquivo de infraestrutura, de documentação e de migração fica em kebab-case sem
exceção. O repositório começou em camelCase nos primeiros três meses; Beatriz reescreveu tudo
numa tarde de janeiro de 2026 porque a mistura de convenção custava mais atenção por semana do
que a padronização custou naquela tarde.

## Migração de banco

- Toda migração Alembic recebe nome `<timestamp>_<descricao-curta-kebab>.py`, gerado por
  `alembic revision --autogenerate -m "descricao"`.
- Migração já aplicada em produção nunca é editada. Erro numa migração aplicada vira migração
  corretiva nova.
- Coluna de valor monetário é sempre `Integer`, armazenando centavos. Nunca `Float`; `Numeric`
  só entra com justificativa escrita no corpo da migração sobre por que o caso foge da regra.

## Webhook e idempotência

Todo endpoint de webhook (hoje, só o do Stripe) grava a chave de idempotência do evento antes de
processar qualquer efeito colateral (criar transação, disparar e-mail de confirmação). Se a
chave já existe, o endpoint responde 200 sem reprocessar. Checagem e gravação da chave em duas
queries separadas está proibida: as duas operações entram numa única instrução atômica
(`INSERT ... ON CONFLICT DO NOTHING`, ou equivalente). Essa regra é resultado direto da sessão
de 12 de junho de 2026, registrada em `episodica/sessao-2026-06-12.md`.

## Commit e branch

- Conventional Commits (`feat:`, `fix:`, `chore:`, `refactor:`) em toda mensagem.
- Branch nomeada `<tipo>/<descricao-kebab>`, nunca algo como `beatriz/wip`.
- O Nortada é produto solo, mas todo pull request passa pela mesma esteira de integração
  contínua antes do merge, mesmo sendo Beatriz quem aprova. Não existe push direto pra `main`.

## Fuso horário

Todo timestamp gravado em UTC no banco. Conversão pro fuso do usuário acontece só na camada de
apresentação: a API já serializa em ISO 8601 com offset, e o front-end resolve a exibição local.
