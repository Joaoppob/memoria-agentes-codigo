---
topico: Idempotência em webhooks de pagamento (Stripe)
fonte_primaria: "Stripe. Idempotent Requests. Stripe Docs, 2024. Disponível em: https://docs.stripe.com/api/idempotent_requests"
autor_organizacao: Stripe Inc.
ano: 2024
catalogado_por: Farol, via /cataloga-fonte
data_catalogacao: 2026-05-30
projeto: Nortada
tags: [pagamentos, webhooks, idempotencia, stripe]
---

# Idempotência em webhooks de pagamento (Stripe)

## Por que essa fonte foi catalogada

O Nortada recebe webhook do Stripe pra cada evento de cobrança (fatura paga, fatura falhou,
assinatura cancelada). O Stripe reenvia o mesmo evento quando não recebe 200 dentro do timeout
esperado, o que significa que qualquer endpoint de webhook vai, mais cedo ou mais tarde, receber
o mesmo evento mais de uma vez.

## O que a fonte estabelece

O Stripe recomenda gravar a chave de idempotência do evento (`event.id`, único por evento) antes
de processar qualquer efeito colateral, e checar essa chave no início do handler. Se a chave já
foi vista, o handler responde 200 sem reprocessar, mesmo que o processamento anterior não tenha
terminado: a resposta 200 confirma recebimento do evento, não confirma conclusão de todo o
efeito que aquele evento dispara.

A documentação também explica que o Stripe considera o evento como recebido pelo código HTTP da
resposta, não pelo corpo dela. Qualquer código fora da faixa 2xx dispara reenvio, com backoff
crescente, por até três dias.

## Aplicação no Nortada

A regra derivada dessa fonte entrou em `configuracao/regras-projeto.md`, seção Webhook e
idempotência: gravar a chave antes de processar, nunca depois. A ordem importa porque gravar
depois deixa uma janela de corrida em que dois webhooks concorrentes (reenvio rápido do Stripe)
passam pela checagem de duplicidade antes que o primeiro tenha terminado de gravar. Essa fonte
foi consultada de novo na sessão de 12 de junho de 2026, registrada em
`episodica/sessao-2026-06-12.md`, quando o bug de transação duplicada apareceu exatamente por
essa janela de corrida.

O princípio geral por trás dessa recomendação, entrega "pelo menos uma vez" com deduplicação a
cargo do receptor, está catalogado como documento primário em `biblioteca-exemplo.md`, mesmo
diretório: fonte mais fundamental, consultada por Beatriz antes de aplicar a recomendação
específica do Stripe.
