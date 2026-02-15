# API de Dados Sociais

> **Tipo:** API
> **Tecnologia:** Node.js
> **Banco de dados:** Solar

## Objetivo

Servir como a **camada padronizada de acesso aos dados** de redes sociais. Toda leitura e escrita de dados no banco passa por esta API. Ela garante que os dados são gravados de forma padronizada, gerencia métricas virtuais pré-calculadas e mantém histórico de todas as informações.

## Entradas

- **Dados de perfis** — Criação, atualização de perfis do Instagram (nome, bio, seguidores, etc.)
- **Dados de postagens** — Informações de postagens (texto, tipo, métricas de engajamento)
- **Dados de comentários** — Comentários e threads de conversa
- **Dados de mídias** — Referência a mídias locais (caminho público da API de Mídia)
- **Consultas** — Pesquisas por palavra-chave, filtros por perfil, postagem, comentários

## Saídas

- **Dados padronizados** — Perfis, postagens, comentários em formato consistente
- **Métricas virtuais** — Scores e métricas pré-calculadas (views/comentários, views/compartilhamentos, engagement rate relativo a seguidores, etc.)
- **Histórico** — Snapshots de dados ao longo do tempo (seguidores, views, métricas)
- **Resultados de consulta** — Perfis por palavra-chave, comentários por postagem, etc.

## Contexto

Esta API é o coração dos dados do sistema. Todos os dados que forem gravados no Solar passam por aqui e seguem um padrão. Ela não recebe dados brutos diretamente — é o Serviço de Processamento que transforma dados brutos e envia para cá.

### Métricas Virtuais
Toda vez que uma postagem é atualizada, as métricas virtuais são recalculadas:
- Views ÷ comentários
- Views ÷ compartilhamentos
- Views ÷ reenvios
- Comentários ÷ seguidores do perfil
- Score médio baseado em comentários (mais = melhor)
- Score médio baseado em views (mais = melhor)
- Score médio baseado em salvamentos (mais = melhor)
- Proporção de engajamento relativa ao número de seguidores

### Histórico
- Toda atualização de dados gera um registro de histórico
- ID composto: ID do elemento + data (para ter múltiplas versões ao longo do tempo)
- Informação mais recente fica na postagem para facilitar indexação
- Histórico fica em collections separadas no Solar (sem necessidade de indexação pesada)
- Permite gerar gráficos de evolução (ex: quantas horas leva para uma postagem chegar a X views)

## Dependências

- **Serviço de Processamento de Dados** — Envia dados processados para esta API
- **Serviço de Download** — Atualiza referência de mídia local na postagem
- **Agentes de Análise** — Consultam dados via esta API (ferramenta dos agentes)
- **Todos os produtos (Data Explorer, QR Trends, QR Brand, Semantic Explorer)** — Consultam dados daqui

## Regras Específicas

- **Swagger + MCP obrigatórios** — O MCP expõe a API e todas as entradas/saídas esperadas, incluindo a estrutura de dados
- **Esquema de dados claro** — Nomes dos campos definidos e documentados no MCP para que agentes de IA possam consumir
- **Métricas virtuais sempre atualizadas** — Toda atualização de postagem recalcula as métricas
- **Histórico obrigatório** — Nunca sobrescrever dados; sempre criar registro histórico
- Dados do Instagram ficam separados (são dados de redes sociais/externos, não dados internos do sistema)

## Observações

- No futuro, se houver TikTok, cada provider teria sua própria camada de dados brutos, mas os dados estruturados convergiriam nesta API
- A modelagem por provider (Instagram, TikTok, etc.) adiciona complexidade ao sistema inteiro — descartada para o MVP
- Aba de visualização de estruturas de dados prevista no Monitor/Dashboard
