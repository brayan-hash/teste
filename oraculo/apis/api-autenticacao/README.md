# API de Autenticação

> **Tipo:** API
> **Tecnologia:** Node.js
> **Auth Provider:** Firebase

## Objetivo

**Autenticar usuários** do sistema e garantir que o **ID do usuário** seja carregado em todas as solicitações, eventos e operações. Todas as outras APIs internas são protegidas — esta API é o gateway de autenticação.

## Entradas

- **Credenciais do usuário** — Login via Firebase (email/senha, Google, etc.)
- **Token de sessão** — Para validação de requisições subsequentes

## Saídas

- **Token de autenticação** — JWT ou token Firebase para uso nas demais APIs
- **ID do usuário** — Identificador único propagado em todas as operações
- **Dados do perfil** — Nome, email, permissões do usuário

## Contexto

Esta API foi pensada desde o início para evitar o problema de "construir a plataforma inteira e depois tentar inserir o usuário, quebrando tudo". O ID do usuário é carregado em **todas** as solicitações, **todos** os eventos, **todas** as operações — para saber quem pediu o quê e se tem crédito.

Todas as APIs são internas. Esta API fica no meio, autenticando o usuário, e a comunicação com as APIs internas é protegida para ninguém hackear e usar os dados de graça.

### Fluxo
1. Usuário faz login via Firebase (no produto/app)
2. API de Autenticação valida e gera token
3. Token é usado em todas as requisições subsequentes
4. Cada API interna valida o token antes de processar

## Dependências

- **Firebase** — Provider de autenticação
- **API de Créditos/Produtos** — Para verificar se o usuário tem crédito/assinatura
- **Todas as APIs internas** — Protegidas por esta camada de autenticação
- **Todos os produtos** — Usam esta API para login

## Regras Específicas

- **ID do usuário em tudo** — Todas as solicitações e eventos devem carregar o ID do usuário
- **Suporte a Firebase** obrigatório
- **Documentação Swagger + MCP**
- Proteger todas as APIs internas contra acesso não autorizado

## Observações

- A implementação completa de segurança (proteção de APIs internas) é mais para a fase de produto público, não necessariamente no MVP interno
