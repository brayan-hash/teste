# API de Créditos, Produtos e Tarefas

> **Tipo:** API
> **Tecnologia:** Node.js

## Objetivo

Controlar **assinaturas**, **créditos** e **custo por tarefa** de cada usuário. Define quais são os produtos disponíveis, quanto de crédito cada ação consome, e gerencia o saldo do usuário.

## Entradas

- **ID do usuário** — Para consultar/debitar créditos
- **Tipo de ação/tarefa** — Para calcular custo (download, transcrição, análise, etc.)
- **Registro de assinatura** — Quando o usuário assina um produto
- **Definição de produto** — Nome, preço, créditos incluídos
- **Definição de custo por tarefa** — Quanto cada tipo de tarefa custa em créditos

## Saídas

- **Saldo atual** do usuário em créditos
- **Custo da ação** — Quanto uma tarefa específica vai custar
- **Validação de crédito** — Se o usuário tem crédito suficiente para executar a ação
- **Histórico de consumo** — O que o usuário gastou e quando
- **Produtos e planos** disponíveis

## Contexto

Cada tarefa no sistema (download, transcrição, análise, visita de perfil, etc.) tem um custo em créditos. Antes de executar qualquer solicitação, o sistema verifica se o usuário tem crédito suficiente. O custo de cada execução é registrado independentemente de ter sido processado do cache ou não (decisão de negócio).

### Estrutura
- **Produtos** — Planos de assinatura com créditos incluídos
- **Créditos** — Saldo do usuário, consumido a cada tarefa
- **Tarefas** — Catálogo de todas as tarefas possíveis com seu custo em créditos

Cada tarefa documentada na API de Solicitações deve ter seu custo correspondente definido aqui.

## Dependências

- **API de Autenticação** — Para identificar o usuário
- **API de Solicitações** — Verifica crédito antes de criar solicitação
- **API de Análise LLM** — Reporta custo de execução de IA
- **Todos os produtos** — Consomem créditos

## Regras Específicas

- **Documentação Swagger + MCP**
- Cada tarefa deve ter seu custo documentado
- Gasto de crédito registrado por tarefa, independente de cache

## Observações

- O modelo de negócio (cobrar por pesquisa, gratuito com limite, assinatura) ainda está sendo definido
- Para o MVP, pode ser simplificado (sem cobrança real), mas a estrutura deve existir
