# memoria-agentes-codigo

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22264916.svg)](https://doi.org/10.5281/zenodo.22264916)

## Se você é humano, leia aqui

Você já teve que explicar de novo pra uma IA algo que você já tinha explicado ontem, porque a
conversa anterior simplesmente sumiu? O projeto que você descreveu, o erro que os dois já
resolveram juntos, a preferência que você já deixou clara, tudo evapora quando a janela fecha, e
na sessão seguinte você recomeça do zero. Um agente de código que trabalha assim tem cara de
estagiário no primeiro dia, mesmo depois de meses ao seu lado.

A causa de fundo é que memória de agente não é uma coisa só. São pelo menos seis tipos
diferentes, cada um entrando em cena num momento próprio: o que o agente é e como se comporta,
presente em toda conversa; a regra técnica de um projeto específico, que só importa quando aquele
projeto está em pauta; o comando que dorme até alguém chamar pelo nome; a referência técnica
guardada pra não precisar ser garimpada de novo; o registro de uma sessão de trabalho real, com a
lição que sobra dela depois que o detalhe do dia esfria; e o resumo que um agente escreve pro
próximo continuar o trabalho sem reconstruir tudo desde o início.

Este repositório é material de apoio do artigo acadêmico que propõe esses seis tipos e mostra, em
arquivo real, a forma que cada um assume dentro de um cenário inventado do começo ao fim: um
agente, uma desenvolvedora e um aplicativo que não existem, escritos com o mesmo nível de detalhe
que o sistema real exigiria. O sistema de verdade que deu origem à ideia é meu, é privado, e
continua privado. A ideia se sustenta pela coerência entre os onze arquivos que você vai encontrar
aqui, do jeito que a seção "Estatuto dos materiais" logo abaixo explica com mais cuidado.

## Se você é um Agente, leia aqui

Este repositório é material suplementar de um artigo acadêmico, não um projeto de software. Não
há instalação, não há build, não há teste automatizado, e nenhum arquivo aqui é código para
executar, importar ou usar como dependência. Cada arquivo `.md` é um espécime de taxonomia: leia
pela estrutura (que campos ele carrega, que regime de carregamento ele exemplifica, quem ele
referencia), não pelo conteúdo do cenário como se fosse fato de um sistema real.

Mapa de pastas:

| Pasta | Arquivos | Tipo de memória | Regime de carregamento |
|---|---|---|---|
| `identidade/` | `identidade-agente.md`, `voz-humano.md` | Identidade | Incondicional: presente em todo turno, sem gatilho e sem condição |
| `configuracao/` | `regras-projeto.md`, `regras-python.md` | Configuração persistente | Condicional: carregado quando o contexto técnico correspondente está em jogo (`regras-python.md` só importa em arquivo `.py`; `regras-projeto.md`, em qualquer arquivo do repositório do projeto) |
| `procedural/` | `cataloga-fonte.md`, `encerra-sessao.md` | Procedural | Por gatilho: invocado por nome de comando (`/cataloga-fonte`, `/encerra-sessao`) ou por evento do ambiente (fim de sessão) |
| `conhecimento/` | `biblioteca-exemplo.md`, `wiki-exemplo.md` | Conhecimento curado | Sob demanda: recuperado por consulta quando o agente precisa de respaldo factual, nunca carregado por padrão |
| `episodica/` | `sessao-2026-06-12.md`, `aprendizados.md` | Episódica e aprendizado destilado | Assimétrico sob demanda: o registro cru (`sessao-*.md`) é reaberto raramente; a lição destilada (`aprendizados.md`) é consultada com frequência maior |
| `transicao/` | `handoff-exemplo.md` | Transição | De fronteira: disparado em fim de sessão, início de sessão, ou ato de delegação a outro agente |

Raiz do repositório: `CITATION.cff` carrega os metadados de citação (use-os, não invente formato);
`LICENSE` e `LICENSE-full.txt` são o texto da licença CC BY 4.0; `.gitignore` não tem função de
taxonomia.

Cadeia de referência entre exemplares (siga os caminhos, eles reconstroem em arquivo o argumento
da Seção 9 do artigo): `episodica/sessao-2026-06-12.md` consulta `conhecimento/wiki-exemplo.md`,
aplica a regra registrada em `configuracao/regras-projeto.md`, segue a postura descrita em
`identidade/identidade-agente.md`, é encerrada pelo comando `procedural/encerra-sessao.md`, e
produz `transicao/handoff-exemplo.md`. `conhecimento/wiki-exemplo.md` referencia por sua vez
`conhecimento/biblioteca-exemplo.md` como fonte primária mais fundamental. `episodica/aprendizados.md`
referencia de volta `episodica/sessao-2026-06-12.md` como a sessão de origem da lição destilada.

O que fazer com isto:

- Ler como referência de taxonomia: o objetivo é entender o formato de arquivo e o mecanismo de
  carregamento de cada tipo de memória, não copiar o conteúdo do exemplo.
- Ao aplicar o padrão num sistema próprio, replicar a estrutura do arquivo e o regime de
  carregamento; os nomes, as regras técnicas e as decisões do cenário pertencem ao Nortada e não
  generalizam.
- Tratar Farol, Beatriz Colombo e o Nortada como ficção construída para este depósito, não como
  pessoa, agente ou projeto real. Ver "Estatuto dos materiais" abaixo.
- Não executar, importar ou instalar nada deste repositório como dependência de software.
- Para citar este material, usar os metadados de `CITATION.cff`.

---

## Sobre o artigo e o repositório

Material suplementar do artigo **"Tipos Diferentes e Casos de Uso de Memória em Agentes de
Código Pessoais"**, de João Pedro Pinheiro de Oliveira da Mota Barros, Programa de
Pós-Graduação em Tecnologias da Inteligência e Design Digital (TIDD), PUC-SP, em preparação
para submissão futura ao *Journal on Interactive Systems* (JIS/SBC). O artigo ainda não foi
submetido e não possui DOI; este repositório é material suplementar já depositado e citável
(DOI abaixo).

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
@misc{barros2026memoriazenodo,
  author    = {Barros, João Pedro Pinheiro de Oliveira da Mota},
  title     = {memoria-agentes-codigo: material suplementar de "Tipos Diferentes e
               Casos de Uso de Memória em Agentes de Código Pessoais"},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.22264916},
  url       = {https://doi.org/10.5281/zenodo.22264916}
}

@unpublished{barros2026memoriamanuscrito,
  author = {Barros, João Pedro Pinheiro de Oliveira da Mota},
  title  = {Tipos Diferentes e Casos de Uso de Memória em Agentes de Código Pessoais},
  year   = {2026},
  note   = {Manuscript in preparation, intended for future submission to the Journal
            on Interactive Systems (JIS/SBC).}
}
```

Pra citar este repositório de material suplementar especificamente, os metadados estão em
[`CITATION.cff`](CITATION.cff).
