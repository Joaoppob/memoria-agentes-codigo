---
topico: Idempotência e semântica de entrega "pelo menos uma vez" em sistemas distribuídos
fonte_primaria: "HELLAND, Pat. Idempotence Is Not a Medical Condition. Communications of the ACM, v. 55, n. 5, p. 56-65, mai. 2012. DOI: 10.1145/2160718.2160734."
autor: Pat Helland
ano: 2012
ponteiro_arquivo: biblioteca/distribuidos/helland-2012-idempotence.pdf
catalogado_por: Beatriz Colombo
data_catalogacao: 2026-05-28
projeto: Nortada
tags: [distribuidos, idempotencia, mensageria, fundamentos]
---

# Idempotence Is Not a Medical Condition (Helland, 2012)

## Por que esse documento está na biblioteca

Fonte fundamental por trás da entrada `wiki-exemplo.md`, sobre idempotência em webhooks do
Stripe. Beatriz catalogou este artigo antes de abrir a documentação do Stripe, porque queria
entender o princípio geral antes de aplicar a recomendação específica de um provedor. Diferente
da nota da wiki, que resume o que o Stripe recomenda pro Nortada, este é o documento primário: o
paper que formaliza por que qualquer sistema que promete entrega "pelo menos uma vez" empurra a
responsabilidade de deduplicação pro consumidor, não pro produtor.

## O que o documento estabelece

Helland argumenta que sistemas distribuídos raramente conseguem garantir entrega "exatamente uma
vez" fim a fim sem custo proibitivo de coordenação, então a alternativa prática é aceitar entrega
"pelo menos uma vez" e projetar o receptor pra tratar duplicata como caso normal, não exceção. O
ponto central do paper: idempotência não é propriedade natural de uma operação, é propriedade de
design que precisa ser construída deliberadamente, geralmente por meio de um identificador único
de operação que o receptor usa pra reconhecer repetição antes de aplicar qualquer efeito
colateral.

O paper também separa dois tipos de garantia que costumam ser confundidos: a garantia de
mensageria (o transporte entregou a mensagem) e a garantia de efeito (a operação que a mensagem
descreve foi aplicada uma única vez). A idempotência resolve a segunda, não a primeira, e as duas
exigem mecanismo próprio.

## Onde esse fundamento aparece no Nortada

O princípio de "identificador único checado antes do efeito colateral" é o que a nota
`wiki-exemplo.md` aplica ao caso concreto do Stripe, e o que a regra em
`configuracao/regras-projeto.md`, seção Webhook e idempotência, torna operacional pro
repositório. A distinção entre garantia de mensageria e garantia de efeito também explica por que
a correção descrita em `episodica/sessao-2026-06-12.md` precisou de instrução atômica, não só de
checagem prévia: duas queries separadas garantiam recebimento da mensagem, não garantiam efeito
único.
