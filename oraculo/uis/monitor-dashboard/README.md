# Monitor / Dashboard

> **Tipo:** UI
> **Tecnologia:** React

## Objetivo

**Dashboard de controle geral** do sistema inteiro. Permite ligar/desligar serviços, ver logs em tempo real, monitorar filas de solicitações, acompanhar eventos e visualizar a saúde de cada componente. É o centro de comando do Oráculo.

## Entradas

- **Status de todos os serviços/APIs** — Ligado, desligado, com erro, processando
- **Logs em tempo real** — Da API de Logs
- **Filas de solicitações** — Da API de Solicitações
- **Eventos em tempo real** — Da API de Eventos
- **Estruturas de dados** — Da API de Dados Sociais (esquema do banco)

## Saídas

- **Interface visual** com:
  - Card para cada serviço/API com botão de ligar/desligar e logs
  - Visualização de filas e serviços pendentes
  - Eventos acontecendo em tempo real
  - Logs de erro com detalhes para diagnóstico
  - Força reinício e liberação de porta de serviços
- **Aba de banco de dados** — Visualização das estruturas de dados do Solar
- **Visão tipo Flow** — Interface parecida com N8N/Node-RED mostrando claramente:
  - Quais são as entradas que cada componente espera
  - Quais são as saídas
  - O que cada um monitora
  - Conexões entre componentes

## Contexto

Este é o "painel de controle" do Oráculo. Tudo que acontece no sistema é visível aqui. No início do projeto, é chamado de "orquestrador", mas na prática é um **monitor** — ele não orquestra nada, apenas observa e permite controle manual.

### Funcionalidades Principais

| Funcionalidade | Descrição |
|----------------|-----------|
| **Cards de serviços** | Um card para cada serviço/API com status, botão ligar/desligar, logs |
| **Logs em tempo real** | Stream de logs de todos os componentes |
| **Filas** | Solicitações pendentes, em execução, concluídas |
| **Eventos** | Timeline de eventos do sistema |
| **Força reinício** | Reiniciar serviço com problema |
| **Libera porta** | Liberar porta ocupada por serviço travado |
| **Banco de dados** | Aba para ver estruturas de dados do Solar |
| **Visão Flow** | Diagrama visual dos componentes e suas conexões (tipo N8N) |

### UIs dentro do Dashboard
O Dashboard pode agregar visualizações de outros componentes:
- UI de mapeamento de dados (do Serviço de Processamento)
- Estruturas de dados (do banco Solar)
- Estado das solicitações e eventos

## Dependências

- **API de Logs** — Fonte de logs em tempo real
- **API de Solicitações** — Fonte de filas e tarefas
- **API de Eventos** — Fonte de eventos em tempo real
- **API de Dados Sociais** — Estrutura do banco de dados
- **Todos os serviços** — Status de ligar/desligar

## Regras Específicas

- **Interface tipo Flow (N8N)** — Visualização clara de componentes, entradas, saídas e conexões
- **Tempo real** — Logs e eventos atualizados em tempo real
- **Controle completo** — Ligar, desligar, reiniciar, liberar porta
- **Erros de console JS interceptados** e enviados para API de Logs
- **Aba de banco de dados** para ver estruturas de dados

## Observações

- No começo é só o monitor. Com o tempo, agrega mais funcionalidades (UIs de outros componentes)
- A visão Flow é para facilitar o entendimento do sistema como um todo, especialmente para novos membros
