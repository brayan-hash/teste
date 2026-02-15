# API de Mídia

> **Tipo:** API
> **Tecnologia:** Node.js

## Objetivo

Tornar **publicamente acessíveis** as mídias baixadas pelo sistema (vídeos MP4, imagens, fotos de perfil, thumbnails). É um servidor de arquivos estáticos que disponibiliza URLs públicas para cada mídia, desacoplado do serviço que faz o download.

## Entradas

- **Arquivos de mídia** — Vídeos (MP4), imagens (JPG/PNG), fotos de perfil, thumbnails, depositados na pasta de downloads pelo Serviço de Download

## Saídas

- **URLs públicas** de acesso direto a cada arquivo de mídia (ex: `https://servidor/midia/{id}.mp4`)
- Caminho público é salvo na API de Dados Sociais, vinculado à postagem correspondente

## Contexto

O Serviço de Download baixa os arquivos e os coloca em uma pasta global. A API de Mídia simplesmente serve esses arquivos publicamente. São duas coisas separadas mas ligadas — cada uma faz seu papel:
- **Serviço de Download** → executa o download
- **API de Mídia** → disponibiliza o arquivo baixado

Após o download, o Serviço de Download:
1. Salva o arquivo na pasta de mídia
2. Atualiza a API de Dados Sociais com o caminho público da mídia
3. Publica na API de Eventos que o download foi concluído

## Dependências

- **Serviço de Download** — Deposita os arquivos que esta API serve
- **API de Dados Sociais** — Recebe o caminho público da mídia para vincular à postagem
- **Todos os produtos** — Usam as URLs públicas para exibir mídias

## Regras Específicas

- **Documentação Swagger + MCP**
- **Não concentrar atribuições** — Esta API apenas serve arquivos, não faz download
- No MVP, armazenamento é local. Futuramente pode usar S3 ou outro serviço de armazenamento

## Observações

- O armazenamento não precisa ser local necessariamente — pode ser S3 ou qualquer serviço de armazenamento na nuvem
- A separação entre download e servir mídia permite trocar o backend de armazenamento sem afetar o serviço de download
