# Segurança, Governança e Limitações do ARI Flow

## Visão Geral

O ARI Flow foi desenvolvido considerando que automações baseadas em Inteligência Artificial devem operar dentro de um domínio claramente definido e manter mecanismos de controle para situações que exigem intervenção humana.

A solução combina automação, IA generativa, grounding documental e Human-in-the-Loop para reduzir o risco de respostas inadequadas ou fora do escopo.

## Segurança das Credenciais

Credenciais e informações sensíveis não são armazenadas neste repositório.

O projeto não publica:

- API Keys;
- tokens de autenticação;
- senhas;
- credenciais do Gmail;
- credenciais do Google Drive;
- credenciais do Google Gemini;
- dados pessoais de usuários;
- conteúdo de e-mails reais.

As conexões utilizadas pelo workflow são autenticadas e administradas diretamente nas plataformas responsáveis pelas integrações.

## Controle de Escopo

O ARI Flow possui uma etapa específica de classificação antes da geração de qualquer resposta automática.

O modelo verifica se a mensagem pertence ao domínio definido para a solução: dúvidas relacionadas a Oracle Cloud Applications.

Somente mensagens classificadas dentro desse escopo seguem para a etapa de geração automática.

## Human-in-the-Loop

Mensagens classificadas como fora do escopo não recebem resposta automática.

Essas mensagens são separadas para tratamento humano.

Esse mecanismo permite que a automação seja utilizada para tarefas previsíveis sem eliminar a supervisão humana nos casos que exigem análise adicional.

## Grounding da Resposta

As respostas do fluxo Oracle utilizam uma base de conhecimento armazenada no Google Drive.

A documentação funciona como contexto para a geração da resposta, reduzindo a dependência exclusiva do conhecimento geral do modelo.

A implementação atual utiliza knowledge grounding documental.

Não se trata de uma arquitetura RAG completa com embeddings, vector database e recuperação semântica de chunks.

## Limitações Conhecidas

### Dependência de serviços externos

O funcionamento do ARI Flow depende da disponibilidade dos serviços utilizados:

- Make;
- Gmail;
- Google Drive;
- Google Gemini.

Indisponibilidade, alteração de API, expiração de autorização ou mudanças nos serviços podem afetar a execução do workflow.

### Rate Limits e Quotas

APIs de modelos generativos possuem limites de utilização definidos pelo provedor.

Durante os testes do projeto foi observado um erro HTTP `429` relacionado ao limite de requisições do Google Gemini.

O cenário voltou a funcionar após a disponibilidade de quota.

Em uma implementação de produção, o consumo da API deve ser monitorado e dimensionado de acordo com o volume esperado de mensagens.

### Duas chamadas de IA

Na arquitetura atual, mensagens relacionadas ao domínio Oracle podem utilizar duas etapas com IA:

1. classificação da mensagem;
2. geração da resposta.

Essa separação aumenta o controle e a rastreabilidade do processo, mas também aumenta o número de chamadas ao modelo.

Uma evolução futura pode avaliar estratégias para otimização desse consumo sem comprometer a segurança do roteamento.

### Qualidade da Base de Conhecimento

A qualidade da resposta depende da qualidade, atualização e abrangência da documentação utilizada como contexto.

Uma base desatualizada ou incompleta pode limitar a capacidade do agente de produzir respostas adequadas.

### Respostas Geradas por IA

Mesmo com grounding documental, modelos generativos não devem ser considerados fontes infalíveis.

Para cenários críticos, recomenda-se implementar mecanismos adicionais de validação, observabilidade e aprovação humana.

## Guardrails Implementados

A versão atual utiliza como mecanismos de controle:

- classificação antes da geração;
- domínio de conhecimento delimitado;
- roteamento condicional;
- base documental como contexto;
- Human-in-the-Loop para mensagens fora do escopo;
- ausência de credenciais no repositório;
- organização das mensagens após processamento.

## Possíveis Evoluções

O projeto pode evoluir com:

- observabilidade e logs estruturados;
- tratamento automático de erros;
- política de retry e backoff para falhas temporárias;
- controle de custos e consumo de tokens;
- métricas de classificação e atendimento;
- registro de auditoria;
- validação de confiança antes do envio;
- aprovação humana para categorias sensíveis;
- utilização de embeddings e busca vetorial;
- arquitetura RAG para bases maiores;
- otimização do número de chamadas ao modelo.

## Considerações Finais

O objetivo do ARI Flow não é substituir indiscriminadamente a análise humana, mas automatizar etapas repetitivas dentro de um domínio controlado.

A combinação de automação, IA generativa, grounding documental e Human-in-the-Loop permite aumentar a eficiência operacional mantendo mecanismos de controle e supervisão.
