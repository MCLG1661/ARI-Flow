# Arquitetura do ARI Flow

## Visão Arquitetural

O ARI Flow utiliza uma arquitetura orientada a eventos para automatizar a triagem e o atendimento de mensagens recebidas por e-mail.

O Make atua como camada de orquestração, conectando Gmail, Google Gemini e Google Drive em um fluxo condicional controlado.

## Componentes

### Gmail — Entrada

Responsável pelo monitoramento da caixa de entrada e captura de novas mensagens que serão processadas pelo fluxo.

### Google Gemini — Classificação

Analisa o assunto e o conteúdo da mensagem e determina se o e-mail está relacionado ao domínio de Oracle Cloud Applications.

A classificação funciona como mecanismo de decisão para o roteamento do processo.

### Router — Orquestração Condicional

O Router separa o processamento em dois caminhos:

- dúvida relacionada a Oracle Cloud Applications;
- mensagem fora do escopo definido.

Essa separação impede que mensagens fora do domínio sejam respondidas automaticamente pela IA.

## Fluxo Oracle

Quando uma mensagem é classificada como dúvida Oracle:

1. o Google Drive disponibiliza a base de conhecimento;
2. o Google Gemini utiliza o contexto fornecido para gerar a resposta;
3. o Gmail envia a resposta ao remetente;
4. a mensagem processada é organizada automaticamente.

## Fluxo Fora do Escopo

Quando uma mensagem não pertence ao domínio Oracle, nenhuma resposta automática é gerada.

A mensagem é separada para tratamento humano, implementando uma estratégia de **Human-in-the-Loop**.

## Knowledge Grounding

A geração de respostas utiliza uma base de conhecimento armazenada no Google Drive.

Essa abordagem fornece contexto documental ao modelo e reduz a dependência exclusiva do conhecimento geral do LLM.

> O ARI Flow utiliza knowledge grounding baseado em documentação. A implementação atual não utiliza uma arquitetura RAG completa com embeddings, vector database e recuperação semântica de chunks.

## Orquestração

O Make é responsável por:

- execução do workflow;
- integração entre serviços;
- roteamento condicional;
- transferência de dados entre módulos;
- execução periódica da automação.

O cenário está configurado para verificar novas mensagens em intervalos regulares.

## Human-in-the-Loop

O ARI Flow mantém intervenção humana nos casos em que a mensagem não pertence ao domínio definido para a automação.

Em vez de solicitar ao modelo que responda sobre assuntos desconhecidos, essas mensagens são separadas para análise humana.

## Princípios da Solução

A arquitetura foi construída considerando:

- separação entre classificação e geração;
- respostas contextualizadas por uma base de conhecimento;
- tratamento humano para situações fora do escopo;
- redução de respostas não fundamentadas;
- modularidade;
- rastreabilidade do fluxo;
- possibilidade de evolução da automação.
