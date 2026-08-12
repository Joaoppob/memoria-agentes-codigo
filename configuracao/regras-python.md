# Regras de Python, Nortada

Escopo: qualquer arquivo `.py` no repositório do Nortada. Regra de linguagem, não de projeto:
vale mesmo se um dia o Nortada ganhar um segundo repositório Python.

## Versão e ambiente

- Python 3.12. Sem suporte a 3.11 ou anterior; a matriz de integração contínua roda só 3.12.
- Gerenciador de pacote: `uv`. Não existe `requirements.txt` no repositório desde a migração de
  março de 2026; toda dependência entra por `pyproject.toml` mais `uv.lock`, e o lock file é
  versionado.

## Formatação e lint

- `ruff format` roda em pre-commit. Formatação não é assunto de debate individual: quem
  discordar de uma escolha de formatação abre issue, não reformata na mão por cima.
- `ruff check` com o conjunto de regras `E, F, I, UP, B, SIM` habilitado. Falha de lint bloqueia
  merge na esteira de integração contínua.

## Import

- Import absoluto sempre. Nunca `from . import x` dentro de `src/nortada/`.
- Ordem: biblioteca padrão, depois pacote de terceiro, depois módulo interno `nortada.*`, cada
  grupo separado por linha em branco. A regra `I` do `ruff` garante essa ordem automaticamente;
  não reordenar import na mão.

## Tipagem

- `mypy --strict` roda na integração contínua, sem exceção por módulo.
- `Any` só é aceito na borda com biblioteca de terceiro sem stub disponível, e vem sempre
  acompanhado de comentário no formato `# tipo real: <o que o tipo correto seria>`.
- Função pública sem anotação de tipo completa não passa em revisão de código.

## O que nunca fazer

- Nunca `except Exception` genérico sem relançar a exceção ou registrar log estruturado com o
  contexto do erro. Captura ampla sem tratamento específico esconde bug, não produz resiliência.
- Nunca argumento default mutável (`def f(x, cache={})`). Usar `None` como default e inicializar
  o valor dentro do corpo da função.
- Nunca `print()` em código de produção. Log estruturado via `structlog`, com o nível apropriado
  ao evento (`debug`, `info`, `warning`, `error`).
- Nunca dado sensível (token de cartão, e-mail completo, valor de transação) em mensagem de log,
  em nenhum nível, nem em `debug`.

## Testes

- `pytest`, cobertura mínima de 80% em `src/nortada/core/` e em `src/nortada/api/`.
- Módulo que integra com o Stripe usa `respx` pra simular chamada HTTP. Chamada real ao Stripe
  em teste automatizado é proibida, mesmo em ambiente de teste do próprio provedor.
