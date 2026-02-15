# Robô Explorador

> **Tipo:** Serviço
> **Tecnologia:** Node.js + Selenium/ChromeDriver

## Objetivo

Automatizar a **navegação no Instagram** usando Selenium e ChromeDriver para visitar perfis, navegar postagens, abrir carrosséis, ler comentários, acessar stories e explorar perfis relacionados. Ele não salva dados diretamente — é a extensão Chrome (rodando dentro do ChromeDriver) que captura os dados durante a navegação.

## Entradas

- **Solicitações de exploração** — Consultadas na API de Solicitações (visitar perfil, navegar postagens, etc.)
- **Cookie do Instagram** — Salvo pela extensão Chrome (via API de Dados Brutos) para autenticar a sessão do Selenium

## Saídas

- **Dados capturados pela extensão** — A extensão Chrome, rodando dentro do ChromeDriver, intercepta os dados e envia para a API de Dados Brutos (o robô não salva diretamente)
- **Eventos publicados** na API de Eventos (visita realizada, exploração concluída, erro)
- **Solicitações marcadas como executadas** na API de Solicitações

## Contexto

O robô usa Selenium com ChromeDriver e reutiliza o cookie do Instagram do usuário para evitar bloqueios. Ele executa **fluxos de acesso** definidos:

### Fluxos Disponíveis

| Fluxo | Descrição |
|-------|-----------|
| **Visita completa de perfil** | Abre o perfil, faz scroll até N páginas ou até acabar as postagens |
| **Visita de postagem** | Abre uma postagem específica para capturar dados atualizados |
| **Navegação de carrosséis** | Abre postagem e navega todas as imagens do carrossel |
| **Comentários** | Clica em "mais comentários" até profundidade definida |
| **Threads de comentários** | Abre respostas de comentários para ver conversas completas |
| **Stories** | Abre e navega os stories de um perfil |
| **Perfis relacionados** | Clica em perfis relacionados/sugeridos |
| **Revisita de postagem** | Re-visita uma postagem para atualizar dados (ex: link de mídia expirado) |

### Funcionamento
1. O serviço inicia e abre o ChromeDriver com o cookie salvo
2. **O navegador fica aberto** — nunca fecha entre tarefas
3. Monitora a API de Solicitações buscando tarefas pendentes
4. Apareceu tarefa → executa o fluxo correspondente
5. Terminou → marca como executado, publica evento, vai para a próxima
6. Se não tem tarefa → aguarda

### Importante
- Os fluxos **não são encadeáveis entre si** — cada fluxo é independente
- "Ele tem fluxo de acesso: visita de perfil completa é essa, visita de postagem é essa. Terminou."
- Isso evita quebras e simplifica o controle

## Dependências

- **API de Solicitações** — Fonte das tarefas de exploração
- **API de Eventos** — Publicação de eventos de execução
- **API de Dados Brutos** — Onde a extensão Chrome (dentro do ChromeDriver) envia os dados capturados
- **Extensão Chrome** — Roda dentro do ChromeDriver capturando dados
- **API de Logs** — Recebe logs de navegação e erros

## Regras Específicas

- **Navegador fica aberto** — Nunca fechar e reabrir o navegador entre tarefas
- **Fluxos não encadeáveis** — Cada fluxo é independente e completo
- **Usar cookie salvo** — Sempre reutilizar o cookie do Instagram para evitar bloqueios
- **Logs constantes** — O que está visitando, estado da navegação, erros
- Marca solicitações como executadas e publica eventos

## Observações

- Para o MVP, 1 instância do robô é suficiente
- Para escalar, seriam necessários múltiplos robôs com múltiplos cookies/contas
- O robô não salva dados — quem salva é a extensão Chrome rodando dentro do ChromeDriver
