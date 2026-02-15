# Serviço de Processamento de Dados Brutos

> **Tipo:** Serviço
> **Tecnologia:** Node.js (processo contínuo)

## Objetivo

**Monitorar a pasta de dados brutos** e processar automaticamente cada novo arquivo JSON que aparece. Transforma dados brutos do Instagram em dados estruturados e os envia para a API de Dados Sociais.

## Entradas

- **Arquivos JSON na pasta de dados brutos** — Depositados pela API de Dados Brutos (vindos da extensão Chrome)
- Cada arquivo contém dados brutos de perfis, postagens, comentários, feeds, etc.

## Saídas

- **Dados processados** enviados para a API de Dados Sociais (perfis, postagens, comentários em formato padronizado)
- **Eventos publicados** na API de Eventos (processamento concluído, erro de processamento)
- **Logs** enviados para a API de Logs

## Contexto

Este serviço é um processo Node.js que **roda continuamente**, monitorando a pasta de dados brutos. Quando aparece um novo arquivo que ainda não foi processado, ele:

1. Lê o arquivo JSON bruto
2. Identifica o tipo de dado (perfil, postagem, comentário, feed)
3. Extrai e estrutura os campos relevantes
4. Envia para a API de Dados Sociais no formato padronizado
5. Marca o arquivo como processado

### Funcionamento
- É **1 serviço só** rodando continuamente (MVP)
- Não precisa de gestão de fila nem nada — apareceu arquivo, processa
- Monitora a pasta fisicamente (polling ou file watcher)
- Para mais clientes, precisaria de mais instâncias rodando em paralelo

### UI de Mapeamento de Dados
Este serviço acompanha uma **UI de mapeamento** que mostra:
- A estrutura dos JSONs brutos que estão chegando
- Quais campos existem nos dados brutos
- O que está sendo extraído e enviado para a API de Dados Sociais
- Se o Instagram mudou o formato dos dados (para detectar perda de informação)

Essa UI é fundamental para garantir coerência entre o que vem do Instagram e o que é injetado no banco de dados.

## Dependências

- **API de Dados Brutos** — Deposita os arquivos que este serviço monitora
- **API de Dados Sociais** — Recebe os dados processados
- **API de Eventos** — Recebe publicação de eventos de processamento
- **API de Logs** — Recebe logs do serviço

## Regras Específicas

- **Logs constantes** — Estado do processamento, o que está fazendo, erros claros
- Deve detectar se dados estão sendo perdidos (campos que existiam e sumiram)
- No MVP, 1 instância é suficiente (~10 clientes)

## Observações

- A UI de mapeamento pode ficar dentro do Monitor/Dashboard ou ser uma aba dedicada
- Se o Instagram mudar o formato dos dados, este serviço precisa ser atualizado
