---
name: encerra-sessao
description: Fecha a sessão de trabalho corrente e gera o artefato de handoff para retomada em janela nova ou por outro agente.
trigger: /encerra-sessao
scope: qualquer sessão de trabalho no repositório do Nortada
output: transicao/handoff-<AAAA-MM-DD>.md
requires:
  - episodica/sessao-<AAAA-MM-DD>.md do dia corrente, existente ou gerada nesta chamada
---

# /encerra-sessao

## Quando usar

Ao final de qualquer sessão de trabalho com Farol, antes de fechar o editor. Também dispara
quando Beatriz precisa interromper no meio de uma tarefa e sabe que vai retomar em outra janela,
mesmo que a sessão não tenha chegado ao fim natural.

## O que o comando faz

1. Lê o registro de sessão do dia (`episodica/sessao-<AAAA-MM-DD>.md`). Se ainda não existe,
   monta um resumo a partir do histórico de comandos e diffs da sessão corrente antes de seguir.
2. Extrai da sessão quatro blocos: decisões tomadas, estado em curso (o que está pela metade),
   próximos passos concretos, dependências ainda abertas (o que bloqueia o próximo passo e de
   quem depende resolver).
3. Escreve `transicao/handoff-<AAAA-MM-DD>.md` com os quatro blocos, mais um ponteiro de volta
   pro registro de sessão que deu origem ao handoff.
4. Se algum teste está falhando no momento do fechamento, o handoff registra qual teste, com o
   caminho do arquivo, e por que ele falha, sem omitir.

## Campos obrigatórios do artefato gerado

- `origem`: caminho do log de sessão que gerou o handoff.
- `decisoes`: lista do que foi decidido e não está em aberto pra rediscussão.
- `estado_em_curso`: o que está pela metade, com caminho de arquivo e branch.
- `proximos_passos`: lista ordenada; o primeiro item é o próximo passo literal, não uma
  categoria de próximo passo.
- `dependencias_abertas`: o que bloqueia o avanço, e de quem ou de que evento depende resolver.

## O que este comando nunca faz

- Nunca fecha a sessão sem escrever o handoff, mesmo quando a sessão foi curta ou não produziu
  código novo.
- Nunca declara "tudo resolvido" quando há teste falhando ou resultado de integração contínua
  ainda não confirmado; isso vai pro campo `dependencias_abertas`, não fica de fora do artefato.
