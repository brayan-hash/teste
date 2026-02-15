# API de Solicitações

> **Tipo:** API
> **Tecnologia:** Node.js

## Objetivo

Receber e gerenciar **ordens de execução** de tarefas no sistema. Qualquer ação que precisa ser executada por um serviço (download, visita de perfil, transcrição, análise, etc.) passa por esta API. Ela gerencia **requisitos**, **callbacks**, **cadeia de solicitações pai/filho** e o **estado de execução** de cada tarefa.

## Entradas

- **Nova solicitação** — Tipo de tarefa, serviço executor, parâmetros necessários, requisitos para execução, callback em caso de erro
- **Atualização de status** — Serviço reportando que executou, que falhou, que precisa de pré-requisito
- **Consulta de fila** — O que tem pendente para executar, por serviço
- **Consulta de cadeia** — Histórico completo de uma solicitação original e todas as sub-solicitações geradas

## Saídas

- **Solicitação criada** com ID, status, requisitos, serviço responsável
- **Fila de tarefas** por serviço (o que precisa ser executado, em que ordem)
- **Status detalhado** — Pendente, em execução, concluído, com erro, aguardando requisito
- **Cadeia de eventos** — Da solicitação original até a última sub-solicitação, rastreável
- **Requisitos pendentes** — O que falta para uma solicitação poder ser executada

## Contexto

Esta API é o orquestrador de tarefas do sistema. Quando o usuário (ou outro serviço) precisa que algo aconteça, ele cria uma solicitação aqui. Exemplos:
- "Quero que o robô visite o perfil X e faça um screen completo"
- "Quero que o vídeo Y seja transcrito"
- "Quero que a postagem Z seja re-visitada porque os dados ficaram desatualizados"

### Cadeia de Solicitações
Toda solicitação tem um **pai**:
- Se o usuário criou, o pai é o ID do usuário
- Se foi gerada por outra solicitação (callback), o pai é a solicitação original
- Isso permite rastrear toda a cadeia de eventos que aconteceu a partir de uma solicitação

### Requisitos e Callbacks
- Cada solicitação declara seus **requisitos** (ex: para transcrever, precisa ter o vídeo baixado)
- Se um requisito não é atendido, a solicitação fica em espera
- Em caso de erro, o **callback** pode gerar uma nova solicitação (ex: download falhou → solicitar revisita da postagem → quando revisita completar, gerar novo download)

### Fluxo Exemplo
1. Usuário solicita download do vídeo
2. Serviço de download tenta baixar → link expirado
3. Callback gera solicitação: revisitar postagem
4. Robô explorador visita a postagem → dados atualizados
5. Callback da revisita gera nova solicitação: tentar download novamente
6. Download completo → solicitação original marcada como concluída

## Dependências

- **API de Eventos** — Publica eventos de execução e status
- **Serviço de Download** — Consome solicitações de download
- **Robô Explorador** — Consome solicitações de visita/exploração
- **Agentes de Análise** — Consome solicitações de análise/transcrição
- **API de Créditos/Produtos** — Verifica se o usuário tem crédito antes de executar
- **Todos os produtos** — Criam solicitações via interface

## Regras Específicas

- **Toda solicitação tem um pai** — Para rastreabilidade completa da cadeia
- **Callbacks em caso de erro** — Possibilidade de encadear ações automaticamente
- **Requisitos declarados** — Cada tarefa declara o que precisa estar pronto para ser executada
- **Status claro e detalhado** — Para informar na UI o que está acontecendo (gerenciar a ansiedade do usuário)
- **Documentação Swagger + MCP**
- Deve ser claro: quantos na fila, qual está executando, o que precisa ser feito

## Observações

- ❓ A relação entre API de Solicitações e API de Eventos precisa ser melhor definida — quando algo é um "evento" vs. quando é uma "solicitação"?
- Criar novos fluxos de serviço de forma dinâmica para não precisar codar todas as cadeias de eventos
