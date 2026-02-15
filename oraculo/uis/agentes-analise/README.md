# Agentes de Análise

> **Tipo:** UI + Backend
> **Tecnologia:** React (frontend) + Node.js (backend)
> **Banco de dados:** Próprio

## Objetivo

**Criar, gerenciar e versionar agentes de análise** que executam tarefas de IA sobre os dados do sistema. Cada agente tem um nome, descrição, parâmetros de entrada, JSON Schema de resposta e ferramentas disponíveis. É aqui que se define **o que** cada análise faz e **como** ela responde.

## Entradas

- **Definição de agente** — Nome, descrição do que entrega, modelo de IA a usar
- **Parâmetros de entrada** — Quais dados o agente precisa (ex: ID da postagem, ID do perfil)
- **JSON Schema de resposta** — Estrutura exata do que o agente deve retornar
- **Ferramentas do agente** — Quais APIs o agente pode consultar (ex: API de Dados Sociais)
- **Consulta de dados** — Como o agente busca os dados que precisa (qual core do Solar, quais parâmetros)

## Saídas

- **Agentes configurados** e salvos no banco de dados, prontos para execução
- **Versionamento** — V1, V2, V3... de cada agente (mudou o schema = nova versão)
- **Resultados de análise** — Respostas estruturadas em JSON, salvas vinculadas à entidade analisada (postagem, perfil, etc.)
- **Metadata de execução** — Custo, modelo usado, versão do agente, timestamp

## Contexto

Esta UI é onde se **projetam** os agentes de análise. Ela não executa as chamadas de IA diretamente — para isso, os agentes usam a API de Análise LLM. Mas é aqui que se define:

### Exemplos de Agentes

| Agente | Analisa | Resposta |
|--------|---------|----------|
| **Análise Estrutural de Short-form** | Transcrição de vídeo | Hook, conteúdo, CTA, estrutura narrativa |
| **Análise de Sentimento** | Comentários / legenda | Score de sentimento, classificação |
| **Extração de Marcas** | Transcrição / comentários | Lista de marcas, empresas, influencers, pessoas |
| **Análise de Thumbnail** | Imagem da thumbnail | Qualidade para atrair clique, elementos visuais |
| **Transcrição de Vídeo** | Arquivo MP4 | Texto transcrito + idioma detectado |
| **Extração de Entidades (5W2H)** | Transcrição / texto | Quem, o que, como, onde, por quê |
| **Análise de Perfil** | Dados do perfil | Segmento, público-alvo, ontologia do perfil |

### Versionamento
- Se o JSON Schema de resposta muda, o agente vira uma **nova versão** (V2, V3...)
- O agente mantém o mesmo nome mas é uma versão nova
- Versões anteriores ficam salvas para comparação e compatibilidade

### Ferramentas dos Agentes
Os agentes podem ter ferramentas ativas:
- **Consultar API de Dados Sociais** — Buscar dados de perfis, postagens, comentários
- **Consultar análises anteriores** — Ver o que já foi analisado sobre a entidade
- **Pesquisa semântica** — Buscar conteúdos similares por embeddings
- Agentes podem adicionar informações extras na saída se acharem necessário

### Análise de Análises
É possível criar agentes que analisam os **resultados de outros agentes**:
- Pegar análises de comentários + análise da legenda + análise da thumbnail + estatísticas
- Passar tudo para um "super agente" que faz uma análise consolidada
- Ex: "Isso é uma boa postagem que deve ranquear ou não?"

### Agente Assistente
Na própria UI, existe um agente que **ajuda a criar novos agentes**:
- "Eu quero descobrir tal informação"
- O agente consulta o que existe no banco, quais análises existem
- Sugere como montar um agente para descobrir aquilo

## Dependências

- **API de Análise LLM** — Executa as chamadas de IA definidas pelos agentes
- **API de Dados Sociais** — Ferramenta consultada pelos agentes
- **API de Solicitações** — Para disparar execução de agentes
- **API de Eventos** — Para registrar análises concluídas
- **API de Créditos/Produtos** — Custo de cada execução de agente

## Regras Específicas

- **Versionamento obrigatório** — Mudou o schema = nova versão do agente
- **Todas as respostas em JSON Schema** — Nunca respostas abertas
- **Respostas em português** — Mesmo analisando conteúdo em outro idioma
- **Amarrar agentes a tipos de dados** — Definir quais agentes atuam sobre quais tipos de dados
- **Tradução** — Transcrições em outros idiomas devem ser traduzidas para português
- **Erros de console JS interceptados** e enviados para API de Logs

## Observações

- ❓ Precisa discutir com a IA como estruturar este componente (é uma UI mas precisa de API — como organizar?)
- A tradução de transcrições para português precisa ser validada no escopo do projeto
- O agente de transcrição pode ter problema ao retornar JSON (precisa validar)
- Agentes com ferramentas de pesquisa no banco devem registrar **o que usaram e por quê** na saída
