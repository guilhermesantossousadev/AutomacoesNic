# Gestao de Capacidade Operacional

Automacao corporativa para consulta e distribuicao de informacoes sobre escalas de trabalho, ausencias e atualizacoes operacionais da NIC Labs.

O projeto usa workflows n8n para receber o comando `/update` no Discord, acionar uma rotina de processamento via Google Apps Script e enviar o resultado para canais de comunicacao internos.

## Objetivo

Reduzir consultas manuais em planilhas e centralizar a publicacao de informacoes operacionais atualizadas, como:

- escala do dia;
- ausentes hoje;
- ausentes amanha;
- proximas ausencias;
- retornos previstos;
- mensagens formatadas para canais internos.

## Funcionalidades

| Area | Recursos |
| --- | --- |
| Escalas | Consulta da escala diaria, agrupamento por colaborador, horarios de entrada e saida, area de atuacao. |
| Ausencias | Ausentes hoje, ausentes amanha, proximas ausencias e retornos previstos. |
| Discord | Slash command `/update`, resposta imediata ao usuario e integracao com n8n via webhook. |
| Automacao | Execucao manual, execucao agendada e integracao com Google Workspace. |

## Fluxo

```txt
Discord /update
    |
    v
Workflow n8n: Discord slash update
    |
    v
Workflow n8n: Discord update -> Apps Script -> Discord
    |
    v
Google Apps Script
    |
    v
Google Sheets
    |
    v
Mensagem final no Discord/Google Chat
```

## Arquivos

| Arquivo | Funcao |
| --- | --- |
| `codigos workflows n8n/Discord_slash_update.json` | Recebe o slash command `/update`, prepara a resposta inicial e encaminha o processamento. |
| `codigos workflows n8n/Discord_update_ AppsScrip.json` | Chama o Apps Script, formata o retorno e envia a mensagem final. |

## Workflows

### Discord slash update

| Item | Valor |
| --- | --- |
| Status no export | Ativo |
| Webhook | `discord-update-path` |
| Nos principais | `Webhook`, `Code in JavaScript`, `HTTP Request`, `Respond to Webhook` |

Responsabilidade: receber o comando do Discord, responder rapidamente e encaminhar para o workflow de processamento.

### Discord update -> Apps Script -> Discord

| Item | Valor |
| --- | --- |
| Status no export | Ativo |
| Webhook | `update-discord-prod-4185644X` |
| Nos principais | `Chamar Apps Script1`, `Formatar Discord Embed1`, `Webhook`, `If`, `Enviar para Discord1` |

Responsabilidade: executar a rotina operacional, montar embed/mensagem e publicar o resultado.

## Integracoes

- Discord Slash Commands.
- n8n self-hosted.
- Google Apps Script.
- Google Sheets.
- Google Chat ou webhook de mensagem.

## Operacao

Comando principal:

```txt
/update
```

O comando dispara a atualizacao manual das informacoes operacionais. A execucao agendada, quando utilizada, deve ser controlada no n8n ou no ambiente de automacao configurado.

## Manutencao

- Exportar os workflows antes de qualquer alteracao em producao.
- Revisar webhooks e credenciais antes de publicar o repositorio.
- Validar se o Apps Script ainda esta publicado e acessivel.
- Conferir se as planilhas esperadas mantem o mesmo formato de colunas.
