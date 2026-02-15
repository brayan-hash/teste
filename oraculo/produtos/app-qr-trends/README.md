# QR Trends

> **Tipo:** App / Produto
> **Tecnologia:** React (frontend)
> **Público-alvo:** Clientes QR Ofertas (supermercadistas)

## Objetivo

**Galeria de conteúdos de terceiros para inspiração** — sem curadoria humana. Mostra grupos de conteúdos similares (agrupados por embeddings) filtrados por segmento, para que o usuário tenha ideias de vídeos que pode produzir para seu negócio. Primeiro produto público do ecossistema Oráculo.

## Entradas

- **Segmento** — Filtro por área de atuação (ex: supermercado, varejo)
- **Público-alvo** — Filtro por tipo de público (ex: caçador de oferta)
- **Filtros de ordenação** — Mais recente, mais views, mais comentários, trends
- **Ação do usuário** — "Vou fazer" (marcar conteúdo para executar)
- **Link da postagem publicada** — Para monitoramento de desempenho
- **Feedback** — Se gostou, se trouxe resultado

## Saídas

- **Galeria de conteúdos** agrupados por similaridade (via embeddings de transcrições)
- **Detalhes de cada conteúdo** — Hook, CTA, texto, por que funciona, por que é engraçado/sério/agrega valor (vindos das análises dos agentes)
- **Métricas de desempenho** — Views, likes, comentários, scores
- **Transcrições traduzidas** — Conteúdos em outros idiomas traduzidos para português
- **Monitoramento de postagem** — Acompanhamento da postagem que o usuário publicou

## Contexto

### Como Funciona

1. O robô explorador visita perfis de supermercados e negócios relacionados
2. Transcrições de vídeos são feitas e embeddings criados
3. Conteúdos similares são agrupados automaticamente
4. O agente de análise de perfil classifica a ontologia de cada perfil (segmento, público-alvo)
5. Filtros por segmento mostram conteúdos relevantes para supermercados
6. O usuário navega pela galeria e se inspira

### Fluxo do Usuário

1. Entra na plataforma (filtrado para supermercados — primeiro para QR Ofertas)
2. Vê centenas de ideias de conteúdo, agrupadas por similaridade
3. Assiste os vídeos e vê as análises (hook, CTA, por que funciona)
4. Marca "vou fazer" se quiser executar a ideia
5. Ao marcar, já sabe: qual é o CTA, qual é o hook, qual é o texto
6. Pode compartilhar o link da postagem que publicou para monitoramento
7. O sistema monitora o desempenho e melhora as recomendações
8. Recebe pedido de feedback sobre o resultado

### Tradução
- Transcrições em outros idiomas são traduzidas para português
- Toda classificação e ontologia é em português
- Mesmo análises de conteúdos em inglês são feitas em português

### Modelo de Negócio
- Usuário do QR Ofertas já entra filtrado para supermercados
- Inicialmente pode ser gratuito para ver tudo
- Depois pode cobrar por pesquisa ou por funcionalidades avançadas
- Modelo exato ainda a definir

### Sem Curadoria Humana
- **Zero curadoria humana** — Tudo automatizado pelos agentes de IA e embeddings
- Só exploração de ideias com base nos dados coletados

## Dependências

- **API de Dados Sociais** — Dados dos perfis e postagens
- **API de Análise LLM** — Análises de conteúdo (hook, CTA, sentimento)
- **Agentes de Análise** — Classificação de perfis, análise estrutural de vídeos
- **API de Autenticação** — Login do usuário
- **API de Créditos/Produtos** — Controle de acesso e cobrança
- **API de Mídia** — Exibição de vídeos e imagens
- **API de Solicitações** — Para solicitar monitoramento de postagem publicada

### Backend necessário (que pode não existir ainda):
- **Banco de embeddings (vetores)** — Para agrupar conteúdos similares
- **Embeddings de transcrições** — Vetor de palavras para cada transcrição de vídeo
- **Serviço de tradução** — Para traduzir transcrições para português

## Regras Específicas

- **Sem curadoria humana** — Tudo automatizado
- **Respostas e classificações em português** — Mesmo para conteúdos em outros idiomas
- **Erros de console JS interceptados** e enviados para API de Logs
- **Construir no servidor remoto** com URL pública

## Observações

- Primeiro produto público do ecossistema — foco em QR Ofertas / supermercados
- A tradução de transcrições precisa ser validada (fazer na transcrição ou depois?)
- O agrupamento por embeddings precisa de uma API de pesquisa semântica no backend
- Precisa definir métricas de ordenação: mais recente? mais views? mais engagement?
