---
name: cataloga-fonte
description: Cataloga uma fonte técnica externa consultada durante o desenvolvimento do Nortada como entrada de wiki, com metadados.
trigger: /cataloga-fonte
scope: material de referência técnica externa (documentação oficial, RFC, post técnico, issue de biblioteca)
output: conhecimento/wiki-<topico-kebab>.md
---

# /cataloga-fonte

## Quando usar

Quando Beatriz ou Farol consultam uma fonte externa pra resolver um problema técnico concreto, e
a fonte tem chance real de precisar ser consultada de novo no futuro. Não é pra qualquer busca
pontual: é pra fonte que vira referência estável do projeto.

## O que o comando faz

1. Pede o ponteiro da fonte primária (URL, DOI ou referência bibliográfica completa) e o tópico
   em uma frase curta.
2. Gera a entrada em `conhecimento/wiki-<topico-kebab>.md` com os metadados obrigatórios: autor
   ou organização responsável, ano, tópico, ponteiro pra fonte primária, data de catalogação,
   quem catalogou.
3. Resume a fonte em até três parágrafos, com foco no que é operacionalmente relevante pro
   Nortada, não num resumo genérico do documento inteiro.
4. Se a entrada nova substitui ou atualiza uma catalogação anterior sobre o mesmo tópico, a
   entrada nova referencia a antiga em vez de duplicar o conteúdo.

## O que este comando nunca faz

- Nunca cataloga uma fonte sem ponteiro verificável pra origem primária.
- Nunca resume uma fonte que ninguém leu até o fim. Se o resumo vem de segunda mão (resumo de
  outro resumo, por exemplo), o campo `fonte_secundaria` marca isso de forma explícita na
  entrada.
