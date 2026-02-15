# API de Eventos

> **Tipo:** API
> **Tecnologia:** Node.js
> **Banco de dados:** Próprio

## Objetivo

Publicar e consultar **eventos e estados** de tudo que acontece no sistema. Quando um download é feito, quando dá erro, quando uma postagem é visitada — tudo é registrado aqui. Essa API gerencia o **estado atual** de cada entidade (postagem, mídia, perfil) e o **histórico de eventos**.

## Entradas

- **Publicação de evento** — Qual entidade (postagem, mídia, perfil), qual evento (download concluído, download com erro, visita realizada, transcrição feita), timestamp, dados adicionais
- **Consulta de estado** — Qual o estado atual de uma entidade específica
- **Consulta de histórico** — Todos os eventos de uma entidade ao longo do tempo

## Saídas

- **Estado atual** de uma entidade (ex: postagem X tem download OK, transcrição pendente)
- **Histórico de eventos** de uma entidade (timeline completa)
- **Eventos por tipo** (ex: todos os downloads com erro)
- **Eventos em tempo real** para o Monitor/Dashboard

## Contexto

A API de Eventos funciona como um log de estado do sistema inteiro. Enquanto a API de Solicitações gerencia "o que precisa ser feito", a API de Eventos registra "o que aconteceu e em que estado as coisas estão".

Exemplos de eventos:
- `download.concluido` — Mídia da postagem X foi baixada com sucesso
- `download.erro` — Tentativa de download da postagem X falhou (link expirado)
- `visita.realizada` — Perfil Y foi visitado pelo robô explorador
- `transcricao.concluida` — Vídeo Z foi transcrito
- `analise.concluida` — Análise de hook da postagem X foi completada

Cada serviço, após executar sua tarefa, publica aqui o resultado. Isso permite que outros serviços consultem se os pré-requisitos deles estão atendidos.

## Dependências

- **API de Solicitações** — Trabalham juntas: solicitações definem "o que fazer", eventos registram "o que aconteceu"
- **Serviço de Download** — Publica eventos de download
- **Robô Explorador** — Publica eventos de visita/exploração
- **Serviço de Processamento** — Publica eventos de processamento
- **Monitor/Dashboard** — Consome eventos em tempo real
- **Todos os produtos** — Consultam estado das entidades

## Regras Específicas

- **Banco de dados próprio** — Eventos ficam separados dos dados sociais
- **Documentação Swagger + MCP**
- **Logs constantes**
- Estado deve ser claro e consultável para informar a UI

## Observações

- ❓ A relação entre API de Eventos e API de Solicitações precisa ser refinada — são complementares mas os limites entre elas precisam ser mais claros
- Eventos podem ser usados para disparar novos fluxos automaticamente (event-driven)
