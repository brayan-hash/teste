# QR Brand

> **Tipo:** App / Produto
> **Tecnologia:** React (frontend)
> **Status:** Ferramenta interna inicialmente — produto público no futuro

## Objetivo

**Máquina de branding e criação de conteúdo** que funde conteúdos virais de terceiros com a identidade da marca, o ICP e os valores do cliente para gerar scripts e ideias de conteúdo originais. Pesquisa semântica avançada com embeddings, word vectors e keyword para encontrar inspiração e detectar gaps de mercado.

## Entradas

- **Dados da marca (brandbook via áudio)** — O usuário fala sobre sua marca, valores, quem é, quem é o cliente, qual o ICP, qual a área de atuação, quais valores entrega. O sistema transcreve, faz perguntas e monta o brandbook
- **ICP (Ideal Customer Profile)** — Perfil do cliente ideal definido pelo usuário
- **Perfis de interesse** — Classificados como: ICP, concorrentes ou influencers
- **Pesquisas** — Por palavra-chave, por semântica, por embeddings
- **Conteúdos selecionados** — Conteúdos de terceiros que o usuário gostou/achou interessante

## Saídas

- **Brandbook estruturado** — Gerado a partir do áudio do usuário + perguntas da IA
- **Scripts/ideias de conteúdo** — Fusão de conteúdo viral + marca + ICP + valores
- **Análise de perfil vs. marca** — Se o perfil do Instagram está de acordo com o brandbook
- **Gaps de mercado** — Oportunidades identificadas pela análise de concorrentes e ICPs
- **Relatórios** — Análise de concorrência, aspirações do ICP, oportunidades
- **Sugestões de conteúdo** — Ideias que atendem o ICP, respeitam a marca e têm potencial viral

## Contexto

### Fluxo Principal

#### 1. Definição da Marca
O usuário entra em uma área e **fala tudo sobre sua marca**: quem é, quem é o cliente, qual o ICP, quais valores entrega, o que não gosta (ex: clickbait). O sistema:
- Transcreve o áudio
- Faz perguntas para aprofundar
- Gera um brandbook estruturado
- Analisa o perfil do Instagram e compara com a marca

#### 2. Pesquisa de Conteúdo
O usuário pesquisa conteúdos por:
- **Palavra-chave**
- **Semântica** (embeddings)
- **Perfis similares, concorrentes, influencers**

#### 3. Fusão de Conteúdo
Seleciona conteúdos que gostou e o sistema:
- Cruza com a marca e o ICP
- Monta uma ideia original que atende os objetivos
- Respeita os valores da marca (ex: sem clickbait se é um valor da marca)
- Gera um script com hook, conteúdo e CTA adaptados

#### Exemplo
- Conteúdo viral: "Cara jogando basquete faz 10 cestas — será que eu acerto?"
- Marca: Supermercado / QR Ofertas
- Fusão: "Será que eu consigo pagar esses 10 boletos fazendo uma ação de marketing seguindo esse script?"
- Adaptação: atende o ICP (supermercadista), respeita a marca, tem hook viral

### Exploração de Perfis

| Tipo | Uso |
|------|-----|
| **ICP** | Entender aspirações, perguntas, dores do cliente ideal |
| **Concorrentes** | Ver o que estão fazendo, quais perguntas recebem, gaps |
| **Influencers** | Encontrar influencers relevantes para a marca |

### Descoberta de Gaps
- Ver quais perguntas ICPs fazem nos perfis dos concorrentes
- Descobrir quais dúvidas o mercado tem que ninguém responde
- Por semântica, encontrar mais pessoas do ICP ou mais concorrentes desconhecidos

### Pesquisa Semântica Avançada
- **Mistura obrigatória**: embeddings + word vectors + keyword
- **Peso ~60/40** (semântica vs. keyword)
- O agente decide como usar os resultados
- **Inversão de visão**: interpretar a pergunta e pesquisar com as palavras que estariam na **resposta**, não na pergunta
- Possibilidade de incluir/remover pessoas de grupos para melhorar precisão

## Dependências

- **API de Dados Sociais** — Dados de perfis, postagens, comentários
- **API de Análise LLM** — Execução de análises e fusão de conteúdo
- **Agentes de Análise** — Análise de marca, ICP, concorrência
- **API de Autenticação** — Login
- **API de Créditos/Produtos** — Controle de créditos
- **API de Mídia** — Exibição de mídias

### Backend necessário:
- **API de pesquisa semântica** — Embeddings + word vectors + keyword
- **Banco de embeddings** — Vetores de transcrições e análises
- **Agentes de branding** — Especialistas em marca, ICP, fusão de conteúdo
- Tudo atendido pelo backend via APIs

## Regras Específicas

- **Pesquisa semântica: embeddings + word vectors + keyword (60/40)** — Obrigatório, nunca só um
- **Inversão de visão** nos agentes — Pesquisar pelas palavras da resposta, não da pergunta
- **Respostas em português** — Sempre
- **Análise respeita valores da marca** — Se clickbait é contra os valores, o hook não pode ter clickbait
- **Erros de console JS interceptados** e enviados para API de Logs
- Possibilidade de incluir/remover entidades de grupos para refinar precisão

## Observações

- Inicialmente ferramenta interna (para a própria empresa)
- Depois pode virar produto público para qualquer marca
- Quanto mais conteúdo coletado, melhor a pesquisa e as fusões
- Precisa de recursos de backend que podem não existir ainda — listar e criar conforme necessário
