# API de Análise LLM

> **Tipo:** API
> **Tecnologia:** Node.js

## Objetivo

**Centralizar todas as requisições aos modelos de IA** do sistema. Toda chamada a OpenAI ou outro provider de LLM passa por esta API, que implementa **cache/idempotência** para nunca executar a mesma análise duas vezes, e retorna o **custo** de cada requisição.

## Entradas

- **Modelo** — Qual modelo de IA usar (ex: GPT-4, etc.)
- **Parâmetros do modelo** — Temperature, max_tokens, etc.
- **Prompt** — O prompt completo da requisição
- **Conteúdo** — O texto/dados a serem analisados (transcrição, comentários, legenda, etc.)
- **JSON Schema de resposta** — Estrutura esperada da resposta (obrigatório)

## Saídas

- **Resposta estruturada** em JSON Schema (conforme definido na entrada)
- **Custo da requisição** — Quanto custou em tokens/dinheiro
- **Flag de cache** — Se a resposta veio de cache ou foi uma nova execução
- **Metadata** — Modelo usado, tempo de execução, tokens consumidos

## Contexto

Esta API não define **o que** analisar — isso é responsabilidade dos Agentes de Análise. Ela é puramente uma camada de execução e cache. Quem estrutura a análise, determina o formato da resposta e decide qual modelo usar é o agente que faz a solicitação.

### Cache e Idempotência
- Se a mesma combinação de modelo + parâmetros + prompt + conteúdo já foi executada, retorna do cache
- Isso economiza custos significativos, especialmente durante desenvolvimento e testes
- Mesmo vindo de cache, o crédito do cliente pode ser cobrado (decisão de negócio)

### JSON Schema Obrigatório
Todas as solicitações para IA são retornadas com base em JSON Schema:
- Não são respostas abertas
- São respostas com intervalo de valores definidos
- Estrutura clara: hook, conteúdo, call-to-action, sentimento, etc.
- Se um campo não se aplica (ex: não tem CTA), o campo indica "não presente"

## Dependências

- **Agentes de Análise** — São os consumidores principais desta API
- **API de Créditos/Produtos** — Para registrar custo de cada execução
- **Providers de LLM** — OpenAI, Anthropic, etc.

## Regras Específicas

- **Cache/idempotência obrigatória** — Nunca executar o mesmo trabalho duas vezes
- **Retornar custo sempre** — Quanto custou + se veio de cache
- **Todas as respostas em JSON Schema** — Nunca respostas abertas/livres
- **Respostas em português** — Mesmo analisando conteúdo em outro idioma
- **Documentação Swagger + MCP**

## Observações

- Conversas abertas sobre conteúdo (em produtos futuros) também serão estruturadas, mas essa decisão ainda precisa ser validada
- O versionamento dos schemas de resposta é controlado nos Agentes de Análise, não aqui
