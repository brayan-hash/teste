# Semantic Explorer

> **Tipo:** App / Produto
> **Tecnologia:** React (frontend)
> **Nível:** Corporativo

## Objetivo

**Descoberta semântica de conteúdo** por meio de pesquisa por entidades (5W2H: quem, o que, como, onde, por quê), com geração de **relatórios de nível corporativo**. O agente usa ferramentas de pesquisa no banco de dados, embeddings e keyword para encontrar postagens, comentários e padrões relevantes.

## Entradas

- **Pesquisas por entidades** — Quem mencionou o quê e quando (5W2H)
- **Queries semânticas** — Pesquisa livre que o agente interpreta e executa
- **Filtros** — Por tipo de conteúdo, data, perfil, segmento
- **Solicitação de pesquisa profunda** — O sistema roda por dias coletando mais dados

## Saídas

- **Lista de postagens relevantes** — Com contexto de por que são relevantes
- **Lista de comentários relevantes** — Com análise de conteúdo
- **Relatório corporativo** — Consolidação das descobertas em formato executivo
- **Insights** — Padrões identificados, tendências, oportunidades
- **Status da pesquisa** — O que já foi encontrado, o que ainda está sendo buscado

## Contexto

### Caso de Uso Exemplar
A Cimed quer encontrar **pessoas que publicaram sobre desodorante aerossol nas redes sociais** que não sejam do segmento de supermercados. O Semantic Explorer:

1. Recebe a query do usuário
2. O agente interpreta a pesquisa
3. Usa ferramentas: pesquisa semântica no banco, embeddings, keyword
4. Retorna o que já tem: "Do que temos até agora, são esses perfis e postagens"
5. Se quiser mais: "Se quiser uma pesquisa profunda, vamos ficar 10 dias rodando, coletando novas informações"
6. No final: relatório completo de **por que** as pessoas publicam sobre desodorante aerossol, com 1000 postagens analisadas ou um relatório enxuto consolidado

### Como Funciona a Pesquisa

1. **Extração de entidades** — Toda postagem/vídeo/comentário passa por extração 5W2H (quem, o que, como, onde, por quê)
2. **Pesquisa por entidades** — O usuário pesquisa por qualquer combinação de entidades
3. **Agente com ferramentas** — O agente usa:
   - Pesquisa por embeddings (semântica)
   - Pesquisa por word vectors
   - Pesquisa por keyword
   - **Inversão de visão** — Interpreta a pergunta e pesquisa com termos que estariam na resposta
4. **Processamento iterativo** — O agente pode fazer múltiplas buscas, refinar resultados, consolidar

### Relatórios
- **Nível corporativo** — Formatação executiva, insights acionáveis
- O agente pode analisar centenas/milhares de postagens e entregar um relatório enxuto
- Ou entregar a lista completa para análise manual

## Dependências

- **API de Dados Sociais** — Fonte de dados de perfis, postagens, comentários
- **API de Análise LLM** — Processamento de queries e geração de relatórios
- **Agentes de Análise** — Extração de entidades 5W2H, análise de conteúdo
- **API de Autenticação** — Login
- **API de Créditos/Produtos** — Controle de créditos (pesquisas consomem crédito)
- **API de Solicitações** — Para disparar pesquisas profundas (coleta de novos dados)

### Backend necessário:
- **API de pesquisa semântica** — Embeddings + word vectors + keyword
- **Banco de embeddings** — Vetores de transcrições, comentários, análises
- **Agentes de extração 5W2H** — Para todas as postagens e comentários
- Possivelmente **GraphRAG** para melhorar descoberta por entidades

## Regras Específicas

- **Pesquisa semântica: embeddings + word vectors + keyword (60/40)** — Obrigatório
- **Inversão de visão** nos agentes — Pesquisar pelas palavras da resposta
- **Respostas em português** — Sempre
- **Relatórios de nível corporativo** — Formatação profissional e insights acionáveis
- **Erros de console JS interceptados** e enviados para API de Logs

## Observações

- Produto de maior valor agregado — serve grandes empresas (ex: Cimed)
- GraphRAG pode ajudar muito neste caso de uso (mencionado na transcrição)
- O potencial é enorme: qualquer marca pode pesquisar qualquer tema nas redes sociais
- Precisa de volume grande de dados coletados para ser realmente útil
