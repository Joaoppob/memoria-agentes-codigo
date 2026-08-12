# Aprendizados, Nortada

Arquivo append-only. Cada entrada é uma lição destilada de uma sessão registrada em
`episodica/`, com link de volta pra sessão de origem. Entrada não é editada depois de escrita:
correção de uma lição vira entrada nova, que referencia a antiga em vez de substituí-la.

---

## 2026-06-12, idempotência não se resolve em duas queries

**Origem:** `episodica/sessao-2026-06-12.md`

Checar se uma chave existe e gravar essa chave em duas operações separadas não é idempotente sob
concorrência, mesmo quando o teste sequencial passa sem problema. A janela entre a checagem e a
gravação é onde o bug mora, e ela existe mesmo que as duas queries rodem com poucos
milissegundos de diferença. A cura não é lock explícito nem retry com espera: é resolver
checagem e gravação como uma única operação atômica, do tipo `INSERT ... ON CONFLICT DO NOTHING`
no Postgres, ou o equivalente do banco em uso.

**Onde isso se aplica de novo:** qualquer endpoint que recebe evento externo com garantia de
"pelo menos uma vez" (webhook de provedor de pagamento, fila com reentrega, callback de
terceiro). Antes de aceitar "checar e depois gravar" como suficiente, a pergunta certa é se as
duas operações cabem numa transação atômica só.
