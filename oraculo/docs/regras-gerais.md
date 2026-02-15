# Regras Gerais do Projeto Oráculo

Estas regras se aplicam a **todos os componentes** do sistema (APIs, Serviços, UIs, Extensões e Produtos), salvo exceções explícitas.

---

## 1. Documentação e MCP

### 1.1 Toda API deve ter documentação Swagger
> *"A regra é toda API tem que tá documentada no Swagger e tem que ter um MCP pra gente saber o que ela faz."*

- Toda API deve ter documentação completa no Swagger
- A documentação deve incluir: endpoints, parâmetros, tipos, exemplos de resposta

### 1.2 Toda API deve ter um servidor MCP
- O MCP expõe a documentação do Swagger para que agentes de IA possam consumir
- Deve expor todas as entradas e saídas esperadas
- Isso permite que a IA saiba o que cada API faz e como interagir com ela

---

## 2. Classificação de Componentes

### 2.1 Cada componente é exclusivamente um tipo
> *"Cada pasta de coisa ou ela é um serviço, ou ela é uma API, ou ela é uma UI."*

| Tipo | Descrição |
|------|-----------|
| **API** | Recebe e responde requisições HTTP |
| **Serviço** | Processo Node.js que roda continuamente |
| **UI** | Interface de usuário em React |
| **Extensão** | Extensão de navegador |
| **App/Produto** | Aplicação completa voltada ao usuário final |

### 2.2 Papel claro de entrada e saída
> *"Vamos tentar todos os serviços ter um papel claro de entrada de dados e saídas, pra ela não concentrar várias atribuições."*

- Cada componente faz **uma coisa** bem feita
- Não misturar responsabilidades (ex: download e servir mídia são coisas separadas)
- Entradas e saídas devem ser claramente documentadas

---

## 3. Logs e Monitoramento

### 3.1 Todo serviço deve ter logs constantes
> *"Todo serviço tem que ter logs constante de como que ele tá fazendo, o que que ele tá fazendo, que estado que ele tá e que erro que tá dando, erros claros rastreáveis."*

- Logs de estado: o que está fazendo agora
- Logs de erro: claro, rastreável, com informação suficiente para consertar
- Logs enviados para a API de Logs

### 3.2 Erros de UI interceptados
> *"Tudo que for por console do JavaScript é interceptado, enviado pra API de logs."*

- Toda UI React deve interceptar `console.log`, `console.error` e exceções
- Tudo enviado automaticamente para a API de Logs
- Para debugar problemas de frontend em produção

---

## 4. Respostas de IA

### 4.1 Todas as respostas em JSON Schema
> *"Todas as solicitações pra IA são retornadas com base em um JSON schema, não são respostas abertas, são respostas com intervalo de valores."*

- Nunca respostas abertas/livres
- Sempre JSON Schema com campos definidos
- Intervalo de valores pré-definido quando possível
- Se um campo não se aplica (ex: não tem CTA), indicar "não presente"

### 4.2 Respostas sempre em português
> *"Toda ontologia, classificação de perfil tem que ser em português. Mesmo ele analisa o conteúdo em inglês e passa pro português."*

- Mesmo analisando conteúdo em outro idioma
- Classificações, ontologias, respostas de agentes — tudo em português
- Orientar os agentes explicitamente para isso nos prompts

---

## 5. Autenticação e Segurança

### 5.1 ID do usuário em tudo
> *"O ID do usuário é carregado em todas as solicitações."*

- Toda solicitação carrega o ID do usuário
- Todo evento registra quem gerou
- Para saber quem pediu o quê e controlar créditos

### 5.2 Login via Firebase
- Todos os produtos usam Firebase para autenticação
- Suportado pela API de Autenticação centralizada

### 5.3 APIs internas protegidas
- Todas as APIs são internas
- A API de Autenticação é o gateway
- Ninguém deve acessar APIs internas diretamente sem autenticação

---

## 6. Pesquisa Semântica

### 6.1 Mistura obrigatória: embeddings + word vectors + keyword
> *"Pesquisas de RAG tem que ser mistura entre embeddings e word vectors e palavra-chave, não pode ser uma coisa ou outra porque a gente aumenta a precisão. Peso 60/40."*

- Nunca usar apenas um método de pesquisa
- Combinar: embeddings (semântica), word vectors e keyword (literal)
- Peso aproximado: 60% semântica / 40% keyword (ajustável)
- O agente decide como usar os resultados

### 6.2 Inversão de visão
> *"Agentes orientados a fazer inversão de visão: interpretar a pergunta e pesquisar com as palavras que estariam na resposta, não na pergunta."*

- Quando alguém faz uma pergunta, os termos da resposta são diferentes dos da pergunta
- O agente deve interpretar a pergunta, pensar em quais termos estariam na resposta
- Pesquisar com esses termos, não com os termos da pergunta
- Isso gera uma pesquisa funcional muito mais precisa
- Aplicável a todos os produtos que usam pesquisa semântica

---

## 7. Dados e Métricas

### 7.1 Métricas virtuais pré-calculadas
> *"Toda vez que receber dados do Instagram, tem que criar as métricas virtuais já pré-calculadas."*

- Métricas que não vêm do Instagram — são calculadas por nós
- Atualizadas automaticamente quando uma postagem é atualizada
- Exemplos: views/comentários, views/compartilhamentos, engagement/seguidores

### 7.2 Histórico obrigatório
> *"A gente tem que ter histórico. O ID tem que compor o ID do elemento mais a data pra ser único."*

- Nunca sobrescrever dados — sempre criar registro histórico
- ID composto: ID do elemento + data
- Informação mais recente na entidade principal (para facilitar indexação)
- Histórico em collections separadas

### 7.3 Exportação em todo lugar
> *"Tem que ter um botãozinho de exportar análise, exportar dados do perfil."*

- Todo lugar com dados deve ter opção de exportar
- Para validar o valor que está sendo agregado
- Exportar análises, perfis, métricas

---

## 8. Escopo do MVP

### 8.1 Limitações do MVP
- **~10 clientes** — Sem gestão de fila complexa, 1 instância de cada serviço
- **Instagram apenas** — Sem TikTok, Google ou outros providers
- **Armazenamento local** — Sem S3 ou cloud storage (exceto onde necessário)
- **1 robô explorador** — Sem paralelismo
- **Sem curadoria humana** — Tudo automatizado

### 8.2 Deploy
> *"Vamos construir tudo isso já no servidor remoto, pra ver em tempo real, ter a URL, poder mandar pras pessoas."*

- **Servidor remoto** com URL pública
- Para poder enviar link e receber feedback em tempo real
- Stack: Node.js (backend), React (frontend), Firebase (auth), Solar (banco de dados)

---

## 9. Versionamento de Agentes

### 9.1 Mudou o schema = nova versão
> *"Se eu mudar essa estrutura de resposta, ela vira um agente V2, V3, mesmo nome mas versão nova."*

- Cada agente de análise tem versão (V1, V2, V3...)
- Se o JSON Schema de resposta muda, é uma nova versão
- Versões anteriores ficam salvas
- O nome do agente permanece o mesmo

---

## 10. Créditos e Custos

### 10.1 Toda tarefa tem custo
- Cada tipo de tarefa (download, transcrição, análise, visita, etc.) tem custo em créditos
- Custo documentado no catálogo de tarefas
- Verificar crédito antes de executar
- Registrar gasto independente de cache

---

## Regras Específicas por Componente

Além destas regras gerais, cada componente pode ter regras específicas documentadas no seu próprio README.md. Consulte:

- [API de Dados Sociais](../apis/api-dados-sociais/README.md) — Métricas virtuais, histórico, esquema MCP
- [API de Solicitações](../apis/api-solicitacoes/README.md) — Cadeia pai/filho, callbacks, requisitos
- [API de Análise LLM](../apis/api-analise-llm/README.md) — Cache/idempotência, custo
- [Agentes de Análise](../uis/agentes-analise/README.md) — Versionamento, ferramentas, tipos de dados
- [Robô Explorador](../servicos/robo-explorador/README.md) — Navegador aberto, fluxos não encadeáveis
- [KnowLedge](../ecossistema/knowledge/README.md) — Modelo bom, não duplicar entidades, sinônimos
