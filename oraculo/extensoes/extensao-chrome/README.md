# Extensão Chrome

> **Tipo:** Extensão de Navegador
> **Plataforma:** Google Chrome

## Objetivo

**Interceptar dados da navegação no Instagram** e enviá-los para a API de Dados Brutos. Também **salvar o cookie atualizado** do Instagram para que o robô explorador (Selenium) possa reutilizá-lo sem ser bloqueado.

## Entradas

- **Navegação no Instagram** — Interceptação automática de requisições HTTP que o Instagram faz durante a navegação normal do usuário (perfis, feeds, postagens, comentários, etc.)
- **Cookie de sessão** — Captura automática do cookie de autenticação do Instagram

## Saídas

- **JSONs de dados brutos** — Enviados para a API de Dados Brutos (payloads interceptados das requisições do Instagram)
- **Cookie atualizado** — Enviado para a API de Dados Brutos e salvo para uso pelo robô explorador

## Contexto

A extensão é o **ponto de captura primário** de dados do sistema. Ela funciona em dois cenários:

### 1. Navegação manual do usuário
O usuário navega normalmente pelo Instagram no Chrome. A extensão intercepta silenciosamente os dados que o Instagram retorna (perfis, postagens, comentários, feeds) e envia para a API de Dados Brutos.

### 2. Dentro do ChromeDriver (Robô Explorador)
Quando o robô explorador abre o ChromeDriver, a extensão está instalada nele. Enquanto o Selenium navega automaticamente, a extensão captura os dados da mesma forma.

### Fluxo
1. Usuário navega no Instagram (manualmente ou via Selenium)
2. Instagram faz requisições HTTP para carregar dados
3. Extensão intercepta as respostas dessas requisições
4. Extrai o JSON do payload
5. Envia para a API de Dados Brutos
6. Também captura e envia o cookie atualizado periodicamente

### Cookie
Antes de usar o Selenium, o usuário abre o Chrome normal, acessa o Instagram um pouco, e isso salva o cookie. Na hora que o Selenium abre, reutiliza esse cookie — evitando bloqueios de conta.

## Dependências

- **API de Dados Brutos** — Recebe os JSONs interceptados e os cookies
- **Robô Explorador** — Usa o cookie salvo e roda com a extensão instalada no ChromeDriver

## Regras Específicas

- Interceptação deve ser silenciosa e não afetar a navegação do usuário
- Enviar cookie atualizado periodicamente
- Logs de interceptação enviados para API de Logs (quantidade de payloads capturados, erros)

## Observações

- Esta é a **única forma de captura de dados** do Instagram — tanto manual quanto automatizada
- A extensão é o complemento essencial dos dados brutos
- No MVP, funciona apenas com Instagram. Para TikTok ou outros, seria outra extensão ou adaptação
