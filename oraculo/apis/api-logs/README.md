# API de Logs

> **Tipo:** API
> **Tecnologia:** Node.js

## Objetivo

**Centralizar logs e erros de todos os serviços, APIs e UIs** do sistema. Tudo que acontece de relevante — especialmente erros — é enviado para cá. Os logs ficam salvos em arquivo TXT para que agentes de IA possam consultá-los e entender o que está acontecendo no sistema.

## Entradas

- **Logs de serviços/APIs** — Nome do serviço, tipo de log (info, warning, error), mensagem, stack trace, timestamp
- **Erros de UI (React)** — Interceptação de `console.log`, `console.error` e exceções JavaScript das aplicações frontend
- **Logs do robô explorador** — Status de navegação, erros de Selenium
- **Logs de qualquer componente** do sistema

## Saídas

- **Arquivos TXT** com logs organizados por serviço/data
- **Dados consultáveis** para o Monitor/Dashboard exibir em tempo real
- **Informação para agentes de IA** diagnosticarem problemas

## Contexto

Todos os componentes do sistema enviam seus logs para cá. Isso inclui:
- APIs reportando erros de requisição
- Serviços reportando falhas de processamento
- UIs React com todo `console.*` interceptado e enviado automaticamente
- Robô explorador reportando problemas de navegação

Os logs são salvos em TXT para que o agente de IA possa ler e entender o que está acontecendo, inclusive sugerir correções.

## Dependências

- **Todos os componentes** — Enviam logs para esta API
- **Monitor/Dashboard** — Exibe os logs em tempo real
- **Agentes de IA** — Podem consultar logs para diagnóstico

## Regras Específicas

- **Todo serviço DEVE enviar logs** — É obrigatório, não opcional
- **Erros claros e rastreáveis** — Deve ser possível entender como consertar a partir do log
- **Interceptar console JS** — Tudo que for por console do JavaScript nas UIs React é interceptado e enviado
- **Documentação Swagger + MCP**
- Estado atual, o que está fazendo, que erro está dando — tudo deve estar nos logs

## Observações

- Os logs em TXT são o formato inicial (MVP). Futuramente pode evoluir para algo mais robusto
- A interceptação de console JS nas UIs é fundamental para debugar problemas de frontend em produção
