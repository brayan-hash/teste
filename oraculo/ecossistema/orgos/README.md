# orgOS — Sistema Operacional da Empresa

> **Tipo:** Sistema
> **Setor:** Gestão
> **Nome:** orgOS

## Objetivo

Trazer **consistência** e **previsibilidade** para a gestão da empresa. O orgOS torna a empresa transparente do ponto de vista de gestão, inclusive para investidores, garantindo que iniciativas sejam executadas, medidas e acompanhadas.

## Entradas

- KPIs definidos por setor e líder
- OKRs da empresa e das equipes
- Iniciativas e ideias novas
- Tarefas diárias dos líderes
- Números e métricas de cada área

## Saídas

- Dashboards de acompanhamento de KPIs e OKRs
- Status de iniciativas (em execução, testando, medindo resultado)
- Relatório de consistência e previsibilidade
- Visão transparente da gestão para investidores
- Tarefas diárias organizadas por líder

## Contexto

O orgOS resolve o problema de: "eu pus alguém pra fazer alguma coisa e a pessoa continua fazendo? Eu determinei uma iniciativa e ela vai acontecer?". Quando surge uma ideia, ela vai pro orgOS e fica lá até alguém executar, testar e medir o resultado. Todos os líderes lançam seus números lá diariamente.

## Dependências

- **KnowLedge (Bubbles)** — Comunicação de entidades/objetos via MCP. O orgOS envia para o Bubbles quais entidades, KPIs e objetos ele tem, para que o Bubbles possa criar objetos úteis internamente
- **Oráculo** — KPIs de marketing e vendas que alimentam o orgOS

## Observações

- O orgOS precisa ter uma forma de comunicar seus objetos e entidades para outros sistemas via servidor MCP
- Ainda não será desenvolvido no MVP inicial do Oráculo — é um sistema paralelo
