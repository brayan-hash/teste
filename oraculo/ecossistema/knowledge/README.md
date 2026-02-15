# KnowLedge (Bubbles) — Base de Conhecimento

> **Tipo:** Sistema
> **Setor:** Estratégia
> **Nome:** KnowLedge

## Objetivo

Ouvir tudo o que o gestor fala, separar em **classes ontológicas** e **entidades**, organizar e tornar essa informação consultável com visualizações por pessoa, setor, área e tema.

## Entradas

- Áudio/transcrição de reuniões e conversas do gestor
- Blocos de texto (10.000-20.000 palavras por processamento inicial)
- Entidades já existentes no sistema (para não duplicar)
- Objetos e entidades de outros sistemas (via MCP do orgOS, por exemplo)

## Saídas

- Mini-artigos estruturados a cada ~500 palavras (com correções de transcrição)
- Entidades extraídas com base na ontologia do sistema (pessoas, empresas, setores, cargos, modelos de negócio, objetivos)
- Relações entre entidades (quem trabalha onde, quem presta serviço a quem)
- Sinônimos resolvidos (ex: "QR" → "QR Ofertas")
- Visualizações por pessoa (ex: tudo sobre a Katiane), por setor (ex: ações de marketing), por tema
- Perguntas, respostas, afirmações organizadas

## Contexto

O KnowLedge funciona assim:
1. Recebe um bloco grande de texto
2. Separa em blocos menores (~500 palavras) com novo processamento a cada bloco
3. A cada processamento, extrai entidades com base na ontologia definida
4. Olha para entidades do passado para não duplicar e relaciona sinônimos
5. Relaciona todas as entidades entre si dentro do contexto
6. Resolve ambiguidades analisando contexto (ex: "QR" pode ser "QR Ofertas" ou "QRG" dependendo do contexto da conversa)

### Ontologia definida:
- Setores da empresa
- Cargos
- Pessoas
- Modelos de negócio
- Objetivos
- KPIs (importados do orgOS)
- Perguntas e respostas
- Afirmações

## Dependências

- **orgOS** — Recebe entidades e objetos do orgOS via MCP para criar referências cruzadas
- **Oráculo** — Pode compartilhar entidades extraídas de conteúdos sociais

## Regras Específicas

- **Modelo de IA bom (não vagabundo)** — Precisa ser um modelo de alta qualidade para resolver ambiguidades e tirar dúvidas contextuais. Custa caro, mas é necessário
- **Não duplicar entidades** — Sempre olhar para o passado antes de criar nova entidade. Usar sinônimos para resolver duplicatas
- **Comunicação entre sistemas via MCP** — O orgOS manda seus objetos/entidades para o Bubbles poder criar objetos internos úteis

## Observações

- Ainda não será desenvolvido no MVP inicial do Oráculo — é um sistema paralelo
- Precisa definir melhor: como estruturar perguntas vs. respostas vs. afirmações
- Precisa definir: como criar visualizações dinâmicas por entidade/tema
