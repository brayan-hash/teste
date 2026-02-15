# Serviço de Download

> **Tipo:** Serviço
> **Tecnologia:** Node.js (processo contínuo)

## Objetivo

Executar **downloads de mídias** (vídeos MP4, imagens, fotos de perfil, thumbnails) com base nas solicitações da API de Solicitações. Salva os arquivos em uma pasta global acessível pela API de Mídia e atualiza o estado no sistema.

## Entradas

- **Solicitações de download** — Consultadas na API de Solicitações (tipo: download de mídia)
- **URLs de mídia** — Links do Instagram para os arquivos a serem baixados
- **Dados da postagem** — ID da postagem, tipo de mídia, metadados

## Saídas

- **Arquivos de mídia baixados** — Salvos na pasta global de downloads (acessível pela API de Mídia)
- **Atualização na API de Dados Sociais** — A postagem agora tem referência à mídia local (caminho público)
- **Eventos publicados** na API de Eventos (download concluído, download com erro)
- **Novas solicitações** em caso de erro (ex: link expirado → solicitar revisita da postagem)

## Contexto

Este serviço monitora a API de Solicitações buscando tarefas de download pendentes. Para cada tarefa:

1. Consulta a solicitação na API de Solicitações
2. Tenta fazer o download do arquivo
3. Se sucesso:
   - Salva na pasta de mídias (acessível pela API de Mídia)
   - Atualiza a API de Dados Sociais com o caminho público da mídia
   - Publica evento de sucesso na API de Eventos
   - Marca solicitação como concluída
4. Se erro (ex: link expirado):
   - Publica evento de erro na API de Eventos
   - Cria nova solicitação para o Robô Explorador revisitar a postagem
   - Essa nova solicitação tem um callback: quando a revisita completar, gerar novo download
   - Marca solicitação original com status de erro + referência à cadeia de recuperação

### Separação de Responsabilidades
- Este serviço **faz o download** dos arquivos
- A **API de Mídia** serve esses arquivos publicamente
- São coisas separadas: "o negócio faz download, o outro entrega — são papéis diferentes"

## Dependências

- **API de Solicitações** — Fonte das tarefas de download
- **API de Eventos** — Publicação de eventos de sucesso/erro
- **API de Dados Sociais** — Atualização da referência de mídia na postagem
- **API de Mídia** — Serve publicamente os arquivos baixados por este serviço
- **Robô Explorador** — Chamado via nova solicitação quando link expira
- **API de Logs** — Recebe logs do serviço

## Regras Específicas

- **Logs constantes** — Estado do download, progresso, erros claros
- Se link expirou, criar nova solicitação de revisita (não falhar silenciosamente)
- Após download, sempre atualizar API de Dados Sociais com caminho público da mídia
- No MVP, 1 instância é suficiente

## Observações

- O serviço não fecha e abre — fica rodando continuamente processando a fila
- Para escalar, seria necessário múltiplas instâncias com gestão de fila
