# ARI Flow — Agente Inteligente para Automação de E-mails

---

## Visão Geral

O ARI Flow é uma automação inteligente desenvolvida para realizar triagem,
classificação e resposta automatizada de e-mails relacionados a Oracle Cloud
Applications.

A solução combina automação de processos e Inteligência Artificial Generativa
para identificar a intenção da mensagem, consultar uma base de conhecimento,
gerar uma resposta contextualizada e encaminhar situações fora do escopo para
tratamento humano.

---

## Problema de Negócio

Equipes que recebem grande volume de solicitações por e-mail precisam dedicar
tempo à leitura, classificação e resposta de perguntas recorrentes.

O ARI Flow foi desenvolvido para automatizar parte desse processo sem permitir
que a IA responda indiscriminadamente a mensagens fora de seu domínio de
conhecimento.

---

## Arquitetura

Gmail → Gemini → Router

### Dúvida Oracle
Google Drive → Gemini → Gmail → Organização da mensagem

### Fora do escopo
Gmail → Tratamento humano

---

## Como o fluxo funciona

1. O Gmail monitora novas mensagens.
2. O Gemini analisa o assunto e o conteúdo.
3. A mensagem é classificada como relacionada ou não a Oracle Cloud Applications.
4. O Router direciona a execução.
5. Para dúvidas Oracle, a automação consulta a base de conhecimento armazenada
   no Google Drive.
6. O Gemini gera uma resposta contextualizada.
7. O Gmail envia a resposta ao remetente.
8. Mensagens processadas são organizadas automaticamente.
9. Mensagens fora do escopo são separadas para análise humana.

---

## Tecnologias

- Make
- Google Gemini
- Gmail
- Google Drive
- IA Generativa
- Automação de Processos
- Prompt Engineering

---

## Human-in-the-Loop

O ARI Flow utiliza uma estratégia de human-in-the-loop.

Quando uma mensagem não pertence ao domínio de conhecimento definido, a IA não
gera uma resposta automática. A mensagem é encaminhada para tratamento humano.

Essa abordagem reduz o risco de respostas inadequadas e mantém supervisão humana
nos casos fora do escopo da automação.

---

## Segurança

Este repositório não contém:

- API Keys
- credenciais de acesso
- tokens
- dados pessoais
- e-mails reais de usuários

As integrações são realizadas por conexões autenticadas diretamente nas
plataformas utilizadas.

---

🙏 Agradecimentos
Este projeto foi desenvolvido a partir dos conhecimentos e desafios propostos na Imersão ONE — Agentes de IA para Negócios, promovida pela Oracle Next Education (ONE) em parceria com a Alura.

Meu agradecimento a **Amanda Gelembauskas (Latam Head of Oracle Next Education)**, aos instrutores, **Christian Velasco (Diretor da Alura Latam)**, **Eric Oliveira (Supervisor de conteúdo na Alura Latam)** e **Leon Kulikoswki (Senior Solution Engineering Manager na Oracle)**, aos especialistas e às equipes da **Oracle** e da **Alura** pela iniciativa, pelo conteúdo compartilhado e pela oportunidade de explorar, na prática, a aplicação de agentes de Inteligência Artificial em problemas reais de negócio.

Durante essa jornada, o **ARI NEWS** e o **DealCraft AI** representaram as primeiras aplicações práticas desenvolvidas a partir dos exercícios da Imersão, explorando o uso de agentes de IA na coleta, organização e transformação e automação.

A evolução desse aprendizado levou ao desenvolvimento do **ARI FLOW**, um projeto independente voltado à automação inteligente de triagem e atendimento por e-mail. A solução amplia a aplicação dos conceitos trabalhados durante a Imersão ao integrar classificação de mensagens com IA generativa, roteamento condicional, consulta a uma base de conhecimento estruturada, geração contextualizada de respostas e automação do fluxo de e-mails. O projeto também incorpora uma estratégia de Human-in-the-Loop, direcionando mensagens fora do escopo para tratamento humano e reduzindo o risco de respostas inadequadas ou não fundamentadas. A arquitetura integra Make, Google Gemini, Gmail e Google Drive, transformando um processo operacional recorrente em um fluxo automatizado, controlado e escalável.

Mais do que concluir exercícios isolados, o objetivo foi transformar o aprendizado em projetos funcionais, documentados, testáveis e replicáveis, demonstrando uma evolução prática na aplicação de Inteligência Artificial, automação, dados e regras de negócio a problemas reais.

---

👤 Autor
Marcus Corrêa Lopes Guedes

Profissional com atuação multidisciplinar em Marketing, Gestão, Inteligência Artificial, Data Analytics, Projetos e Transformação Digital, desenvolvendo soluções que conectam estratégia de negócios, tecnologia e dados.

LinkedIn: Marcus Corrêa Lopes Guedes

GitHub: MCLG1661

---

## Status do Projeto

✅ Classificação automática de e-mails  
✅ Roteamento condicional  
✅ Consulta à base de conhecimento  
✅ Geração de respostas com IA  
✅ Envio automático de respostas  
✅ Tratamento de mensagens fora do escopo  
✅ Human-in-the-loop  
✅ Execução automatizada

