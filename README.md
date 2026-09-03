# memoria-agentes-codigo

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22264916.svg)](https://doi.org/10.5281/zenodo.22264916)

Material suplementar do artigo **"Tipos Diferentes e Casos de Uso de Memória em Agentes de
Código Pessoais"**, de João Pedro Pinheiro de Oliveira da Mota Barros, Programa de
Pós-Graduação em Tecnologias da Inteligência e Design Digital (TIDD), PUC-SP, submetido ao
*Journal on Interactive Systems* (JIS/SBC). O DOI do artigo será atribuído na publicação.

Este repositório está arquivado no Zenodo com identificador persistente:
**[10.5281/zenodo.22264916](https://doi.org/10.5281/zenodo.22264916)** — DOI conceitual, que
aponta sempre para a versão mais recente. A versão v1.0.0 tem o DOI
[10.5281/zenodo.22264917](https://doi.org/10.5281/zenodo.22264917).

O artigo propõe seis tipos de memória para Agentes de Código pessoais, diferenciados pelo regime
em que cada um é carregado no contexto do agente: quando entra, sob qual condição, e por quanto
tempo permanece disponível. Este repositório instancia cada um dos seis tipos com um exemplar
concreto, escrito para acompanhar a submissão.

## As seis camadas

| Diretório | Tipo de memória | Regime de carregamento | Seção do artigo |
|---|---|---|---|
| `identidade/` | Identidade | Incondicional: presente em todo turno, sem gatilho | Seção 3 |
| `configuracao/` | Configuração persistente | Condicional: ativa quando o contexto técnico correspondente está em jogo | Seção 4 |
| `procedural/` | Procedural | Por gatilho: invocada por nome (comando) ou por evento do ambiente | Seção 5 |
| `conhecimento/` | Conhecimento curado | Sob demanda: recuperada por consulta quando o agente precisa de respaldo factual | Seção 6 |
| `episodica/` | Episódica e aprendizado destilado | Assimétrico sob demanda: registro cru raro, lição destilada com frequência maior | Seção 7 |
| `transicao/` | Transição | De fronteira: disparada em fim de sessão, início de sessão, ou ato de delegação | Seção 8 |

A síntese dos quatro regimes (incondicional, condicional, por gatilho, de fronteira) e da
composição entre os seis tipos está na Seção 9 do artigo.

## O universo dos exemplares

Cada arquivo deste repositório pertence ao mesmo cenário fictício, pra que a leitura de um
arquivo ilumine o próximo em vez de exigir onze contextos diferentes. O agente se chama Farol. A
desenvolvedora que ele serve é Beatriz Colombo, que mantém sozinha o Nortada, um aplicativo de
controle financeiro pra freelancer, escrito em Python com FastAPI, SQLAlchemy e PostgreSQL.

Os onze arquivos citam uns aos outros: a sessão de trabalho registrada em `episodica/` consulta
o par catalogado em `conhecimento/`, aplica a regra escrita em `configuracao/`, respeita a
postura descrita em `identidade/`, é fechada por um comando descrito em `procedural/`, e produz
o artefato que está em `transicao/`. É a mesma cadeia de dependência que a Seção 9 do artigo
descreve em prosa, aqui realizada em arquivo.

## Estatuto dos materiais

Os onze arquivos deste repositório são instâncias sintéticas, escritas para este depósito. O
sistema pessoal que deu origem à taxonomia proposta no artigo é privado, contém material do
autor e de terceiros, e não será publicado. O que se oferece aqui é um artefato construído com o
mesmo nível de detalhe técnico que o sistema real exigiria: um agente, uma desenvolvedora e um
projeto inventados até o fim, com nomes, datas, decisões e erros concretos, coerentes entre os
onze arquivos. Essa coerência interna, não a autenticidade da origem, é o que sustenta a
utilidade do material: o suficiente para que o leitor reconstrua o raciocínio de cada camada e
implemente o padrão em sistema próprio, sem depender de acesso ao sistema que não está aqui.

## Como usar

Pra adotar o padrão num sistema próprio:

1. Leia o artigo, Seções 3 a 9, pra entender o regime de carregamento de cada tipo e o porquê
   dele.
2. Leia o exemplar correspondente neste repositório pra ver a forma concreta que esse regime
   assume num arquivo real.
3. Adapte a forma, não o conteúdo. Os nomes, o projeto e as regras técnicas aqui pertencem ao
   Nortada. O que se generaliza é o formato do arquivo e o mecanismo de carregamento, não o
   conteúdo do exemplo.
4. Comece pela identidade, contrato base sobre o qual as outras camadas se assentam, e adicione
   as demais conforme a situação de uso concreta exigir. Nenhum sistema real precisa das seis
   camadas desde o primeiro dia.

## Licença

Este repositório é distribuído sob **Creative Commons Attribution 4.0 International (CC BY
4.0)**. Uso, adaptação e redistribuição são livres, com atribuição. Texto da licença em
[`LICENSE`](LICENSE) (com o legalcode completo em [`LICENSE-full.txt`](LICENSE-full.txt)) e na
página oficial: <https://creativecommons.org/licenses/by/4.0/>.

## Como citar

```bibtex
@article{barros2026memoria,
  author  = {Barros, João Pedro Pinheiro de Oliveira da Mota},
  title   = {Tipos Diferentes e Casos de Uso de Memória em Agentes de Código Pessoais},
  journal = {Journal on Interactive Systems},
  year    = {2026},
  volume  = {[a definir]},
  number  = {[a definir]},
  pages   = {[a definir]},
  doi     = {[a definir]}
}
```

Pra citar este repositório de material suplementar especificamente, os metadados estão em
[`CITATION.cff`](CITATION.cff).
