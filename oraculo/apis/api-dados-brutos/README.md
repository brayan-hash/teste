# API de Dados Brutos

> **Tipo:** API
> **Tecnologia:** Node.js

## Objetivo

Receber dados brutos em JSON interceptados da navegação no Instagram (via extensão Chrome) e gravá-los em uma **pasta global de dados brutos**. Também recebe e armazena cookies atualizados do navegador para uso pelo robô explorador (Selenium).

## Entradas

- **JSON de dados brutos** — Dados interceptados da navegação no Instagram pela extensão Chrome (perfis, postagens, comentários, feeds, etc.)
- **Cookies atualizados** — Cookie de sessão do Instagram do navegador do usuário, enviado pela extensão Chrome

## Saídas

- **Arquivos JSON salvos** em pasta global de dados brutos (um arquivo por payload recebido)
- **Cookie salvo** em local acessível pelo robô explorador para uso no Selenium/ChromeDriver

## Contexto

Esta é a porta de entrada de dados no sistema. A extensão Chrome intercepta as requisições que o Instagram faz durante a navegação normal do usuário e envia esses JSONs para esta API. Os dados ficam como arquivos físicos em uma pasta — ainda não são processados nem estruturados. O Serviço de Processamento de Dados monitora essa pasta e processa os dados posteriormente.

Além dos dados de navegação, a extensão também envia o cookie atualizado do Instagram. Esse cookie é reutilizado pelo Selenium na hora que o robô explorador vai acessar o Instagram automaticamente, evitando bloqueios.

## Dependências

- **Extensão Chrome** — É quem envia os dados para esta API
- **Serviço de Processamento de Dados** — Consome os arquivos gerados por esta API
- **Robô Explorador** — Consome o cookie salvo por esta API

## Regras Específicas

- Deve ter documentação Swagger
- Deve ter servidor MCP
- Logs constantes de recebimento e erros
- No MVP, armazenamento é local (pasta no servidor). Para escalar, pode migrar para serviço de ingestão de dados

## Observações

- No MVP, o armazenamento é local (arquivos físicos em pasta)
- Para mais clientes, seria necessário um sistema de ingestão de dados mais robusto
