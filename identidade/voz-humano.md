# Beatriz Colombo, voz e valores

Escrito por Beatriz, pra Farol e pra qualquer agente que venha a trabalhar no Nortada depois
dele. Descreve quem ela é, não o que o projeto é.

## Quem é Beatriz

Desenvolvedora solo. Passou seis anos numa fintech de médio porte em São Paulo, saiu no fim de
2024 pra tocar o Nortada sozinha, porque queria decidir o roadmap sem passar por comitê de
priorização. O Nortada é o único produto que mantém: aplicativo de controle financeiro pra
freelancer, com foco em separar dinheiro de imposto do dinheiro que pode gastar. Cerca de 900
usuários pagantes em junho de 2026, crescimento devagar e sustentado por indicação, sem
investimento externo.

## Valores que orientam decisão de projeto

- Prefere errar rápido e barato a planejar até não sobrar dúvida. Uma feature nova entra como
  experimento pequeno, com métrica definida antes de escrever a primeira linha.
- Prioriza dado de uso real sobre opinião própria de produto. Se o dado contradiz o que ela
  achava que ia funcionar, o dado ganha.
- Dinheiro de usuário é a linha que não se cruza. Nenhuma decisão de performance, de custo de
  infraestrutura ou de prazo justifica risco em cálculo financeiro ou em dado sensível.
- Prefere admitir que uma decisão anterior estava errada e reverter a defender a decisão por
  ter sido dela.

## Tom com o agente

Direta, sem formalidade. Corrige o agente na hora quando ele erra a instrução, sem rodeio, e
espera o mesmo tipo de correção de volta quando ela pede algo que não faz sentido técnico. Não
gosta de explicação didática de conceito que já domina: se pede pra implementar um índice
composto no Postgres, não precisa da definição de índice composto, precisa da implementação.

## Restrição de tom e de conteúdo

- Dado financeiro de usuário (valor de transação, valor agregado, saldo) nunca aparece em log,
  em print de tela compartilhado, em mensagem de commit ou em qualquer texto que saia do
  ambiente de produção controlado.
- Nome completo de usuário não aparece em nota de sessão nem em issue pública. Referência a
  usuário em texto interno usa o identificador interno (ID numérico), nunca o nome.

## Contexto que importa pro trabalho

Beatriz trabalha sozinha, então revisão de código é ela mesma revisando o próprio pull request
num segundo momento, não um par revisando em tempo real. Por isso a suíte de teste carrega peso
maior do que carregaria numa equipe com revisão cruzada: é o único freio automático que existe
antes do merge.
