# Fluxo Funcional do ARI Flow

## Objetivo

O ARI Flow automatiza a triagem de e-mails e o atendimento de dúvidas relacionadas a Oracle Cloud Applications, mantendo intervenção humana para mensagens fora do escopo definido.

## Fluxo Principal

### 1. Recebimento do e-mail

O Gmail monitora a caixa de entrada em busca de novas mensagens elegíveis para processamento.

O cenário é executado automaticamente em intervalos de 15 minutos.

### 2. Classificação com IA

O conteúdo da mensagem é enviado ao Google Gemini.

O modelo analisa o assunto e o corpo do e-mail para determinar se a mensagem contém uma dúvida relacionada a Oracle Cloud Applications, incluindo contextos como:

- HCM;
- ERP;
- SCM;
- CX;
- Financials;
- Supply Chain.

A saída dessa etapa é utilizada para determinar a próxima rota do workflow.

### 3. Roteamento

O Router do Make divide o processamento em dois caminhos:

- Dúvida Oracle;
- Fora do escopo.

---

## Rota 1 — Dúvida Oracle

Quando a mensagem é identificada como uma dúvida relacionada a Oracle Cloud Applications, o fluxo segue para processamento automatizado.

### 4. Consulta à base de conhecimento

O Google Drive disponibiliza a base documental utilizada pelo agente.

A base fornece contexto específico sobre Oracle Cloud Applications para a etapa de geração da resposta.

### 5. Geração da resposta

O Google Gemini recebe o contexto necessário e gera uma resposta relacionada à dúvida apresentada pelo remetente.

A base de conhecimento funciona como mecanismo de grounding para reduzir respostas não fundamentadas.

### 6. Envio ao remetente

O Gmail envia a resposta gerada para o endereço de e-mail que originou a solicitação.

O assunto original é preservado com o prefixo `RE:`.

### 7. Organização da mensagem

Após o processamento, a mensagem original é movimentada para evitar que permaneça no fluxo normal da caixa de entrada.

---

## Rota 2 — Fora do Escopo

Quando o e-mail não contém uma dúvida relacionada a Oracle Cloud Applications, o ARI Flow não gera uma resposta automática.

A mensagem é separada e destacada para tratamento humano.

Essa decisão implementa o princípio de Human-in-the-Loop e evita que a IA responda sobre assuntos para os quais o fluxo não foi projetado.

---

## Regras de Decisão

| Situação | Ação |
|---|---|
| Dúvida relacionada a Oracle Cloud Applications | Consultar base, gerar resposta e enviar ao remetente |
| Mensagem fora do escopo | Encaminhar para tratamento humano |

## Resultado Operacional

O fluxo permite automatizar tarefas repetitivas de:

- leitura inicial;
- classificação;
- roteamento;
- consulta de conhecimento;
- geração de respostas;
- envio de e-mails;
- organização das mensagens.

Ao mesmo tempo, preserva supervisão humana para situações que não pertencem ao domínio definido para a automação.
