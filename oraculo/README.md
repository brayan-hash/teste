# Projeto Oráculo — Visão Geral do Ecossistema

## O que é

O Oráculo é um ecossistema de sistemas, APIs, serviços e aplicações projetado para **coletar, processar, analisar e extrair valor de conteúdos de redes sociais** — inicialmente focado no Instagram. O objetivo central é transformar dados brutos de perfis, postagens, comentários e mídias em inteligência acionável para marketing, branding e vendas.

## Ecossistema de Alto Nível

O projeto está inserido em um ecossistema maior com três sistemas principais:

| Sistema | Setor | Objetivo | Descrição |
|---------|-------|----------|-----------|
| **Oráculo** | Marketing | Vendas | Analisa conteúdos do Instagram, cria snippets de estrutura de postagem, economiza tráfego pago |
| **orgOS** | Gestão | Consistência | Sistema operacional da empresa — KPIs, OKRs, iniciativas, tarefas diárias |
| **KnowLedge** (Bubbles) | Estratégia | Ontologia/IA | Base de conhecimento que ouve, transcreve, extrai entidades e organiza informação |

## Estrutura de Pastas

```
oraculo/
├── ecossistema/           # Sistemas de alto nível (contexto estratégico)
│   ├── oraculo/           # Sistema Oráculo (Marketing/Vendas)
│   ├── orgos/             # orgOS - Sistema Operacional da Empresa
│   └── knowledge/         # KnowLedge (Bubbles) - Base de Conhecimento
│
├── apis/                  # Todas as APIs do sistema
│   ├── api-dados-brutos/  # Recebe JSONs do Instagram via extensão
│   ├── api-dados-sociais/ # CRUD padronizado + métricas virtuais
│   ├── api-solicitacoes/  # Gerencia ordens e tarefas
│   ├── api-eventos/       # Publica e consulta estados e eventos
│   ├── api-midia/         # Serve mídias publicamente
│   ├── api-analise-llm/   # Centraliza requisições de IA
│   ├── api-logs/          # Centraliza logs e erros
│   ├── api-autenticacao/  # Autenticação de usuários
│   └── api-creditos-produtos/ # Créditos, assinaturas e custos
│
├── servicos/              # Serviços backend (Node.js)
│   ├── servico-processamento-dados/  # Processa dados brutos
│   ├── servico-download/  # Download de mídias
│   └── robo-explorador/   # Selenium/ChromeDriver
│
├── extensoes/             # Extensões de navegador
│   └── extensao-chrome/   # Captura dados do Instagram
│
├── uis/                   # Interfaces de usuário internas
│   ├── monitor-dashboard/ # Dashboard de controle geral
│   └── agentes-analise/   # UI de criação e gestão de agentes
│
├── produtos/              # Produtos e Apps voltados ao usuário
│   ├── app-data-explorer/ # Explorador de dados
│   ├── app-qr-trends/     # Galeria de trends e inspiração
│   ├── app-qr-brand/      # Máquina de branding
│   └── app-semantic-explorer/ # Descoberta semântica de conteúdo
│
└── docs/                  # Documentação transversal
    └── regras-gerais.md   # Regras aplicáveis a todos os componentes
```

## Classificação dos Componentes

Cada componente do sistema é **exclusivamente** um dos seguintes tipos:

- **API** — Recebe e responde requisições HTTP, documentada no Swagger com servidor MCP
- **Serviço** — Processo Node.js que roda continuamente executando tarefas
- **UI** — Interface de usuário em React
- **Extensão** — Extensão de navegador (Chrome)
- **App/Produto** — Aplicação completa voltada ao usuário final

## Escopo Atual

- **MVP** para ~10 clientes
- **Provider inicial:** Instagram (sem TikTok/Google por enquanto)
- **Deploy:** Servidor remoto com URL pública para feedback em tempo real
- **Stack:** Node.js (backend), React (frontend), Firebase (auth), Solar (banco de dados)

## Referências

- [Regras Gerais](docs/regras-gerais.md) — Padrões obrigatórios para todos os componentes
