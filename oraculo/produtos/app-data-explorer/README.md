# Data Explorer

> **Tipo:** App / Produto
> **Tecnologia:** React (frontend)
> **Autenticação:** Firebase (via API de Autenticação)

## Objetivo

Aplicação web de **exploração de dados** onde o usuário faz login e pode pesquisar perfis, entrar em perfis, ver postagens, comentários, análises e solicitar ações (downloads, indexações, análises). É a ferramenta principal para **validar que tudo no backend está funcionando** e visualizar os dados coletados.

## Entradas

- **Login do usuário** — Via Firebase
- **Pesquisas** — Por perfil, por palavra-chave, por postagem
- **Solicitações** — Download de vídeo, indexação de perfil, análise de postagem, revisita, etc.
- **Filtros** — Por tipo de conteúdo, métricas, data, etc.

## Saídas

- **Visualização de perfis** — Dados completos do perfil, postagens, métricas
- **Visualização de postagens** — Texto, mídias, comentários, threads de conversa
- **Análises** — Todas as análises feitas sobre a postagem/perfil (hook, sentimento, extração de marcas, etc.)
- **Status de solicitações** — O que foi pedido, em que estado está, cadeia de eventos
- **Exportação** — Botão de exportar análises e dados do perfil

## Contexto

Esta aplicação é um "super app" de exploração. Talvez não seja um produto público, mas é **essencial para validar** que todo o backend funciona. É onde a equipe interna vai:

1. Entrar, fazer login
2. Pesquisar um perfil (ex: Toguro)
3. Ver postagens do perfil com todas as métricas
4. Clicar em uma postagem e ver todos os detalhes
5. Ver comentários e threads de conversa
6. Ver todas as análises existentes sobre a postagem
7. Solicitar novas ações:
   - Download de vídeo/mídia
   - Mais comentários (definir nível de profundidade)
   - Indexação completa de postagem
   - Indexação completa de perfil (até N páginas)
   - Perfis relacionados
   - Pesquisa de perfis por palavra-chave
   - Visitar perfis com determinada palavra-chave
   - Transcrição de vídeo
   - Análise de conteúdo

### Ferramentas em cada postagem
Em cada postagem, o usuário tem acesso a **tools** (ferramentas):
- Solicitar mais comentários
- Solicitar indexação da postagem
- Solicitar indexação do perfil
- Solicitar perfis relacionados
- Solicitar download de mídia
- Solicitar análise
- Ver status das solicitações

### Exportação
Todo lugar com dados tem **botão de exportar**:
- Exportar análise individual
- Exportar dados do perfil
- Para visualizar a saída e validar o valor que está sendo agregado

## Dependências

- **API de Autenticação** — Login do usuário
- **API de Dados Sociais** — Consulta de perfis, postagens, comentários
- **API de Solicitações** — Criar e consultar solicitações
- **API de Eventos** — Ver status das solicitações
- **API de Mídia** — Exibir vídeos e imagens
- **API de Análise LLM** — Visualizar análises feitas
- **Agentes de Análise** — Consultar via MCP quais análises existem e seus formatos

## Regras Específicas

- **Login via Firebase** obrigatório
- **Exportação em todo lugar** — Botão de exportar em qualquer visualização de dados
- **Erros de console JS interceptados** e enviados para API de Logs
- **Construir no servidor remoto** — Com URL pública para enviar para pessoas e receber feedback
- A UI deve consultar o servidor MCP dos serviços para saber o que está sendo respondido e em que formato, e usar isso para renderizar as análises

## Observações

- Pode não ser um produto público — mais uma ferramenta interna de validação
- "É pra gente ver se tá funcionando: se a solicitação ocorre, se a extração ocorre, se a análise ocorre"
- Análises individuais são visíveis mas não agregam valor sozinhas (ex: ver hook de um vídeo do Toguro isoladamente)
