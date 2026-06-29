# NIC Agenda AI

Automacao de agenda corporativa integrada ao Discord e ao Google Calendar. O projeto permite consultar, criar, excluir e sincronizar eventos por meio de Slash Commands.

## Objetivo

Centralizar operacoes de agenda diretamente no Discord, evitando consultas manuais no Google Calendar para tarefas simples do dia a dia.

## Funcionalidades

| Funcionalidade | Descricao |
| --- | --- |
| Consulta do dia | Lista eventos previstos para hoje. |
| Consulta de amanha | Lista eventos previstos para o proximo dia. |
| Consulta semanal | Lista eventos dentro da janela semanal configurada. |
| Consulta por data | Busca eventos de um dia especifico. |
| Criacao de evento | Cria evento com titulo, data, hora e convidado. |
| Exclusao de evento | Localiza e remove evento pelo titulo. |
| Sincronizacao | Copia eventos novos de agendas compartilhadas para uma agenda central. |

## Comando principal

```txt
/agenda
```

Acoes suportadas pelo workflow:

```txt
hoje
amanha
semana
dia
criar
excluir
sincronizar
```

## Fluxo

```txt
Discord /agenda
    |
    v
Workflow n8n: Comando slash Nic Agenda
    |
    v
Workflow n8n: Processar slash Nic Agenda
    |
    v
Google Calendar
    |
    v
Resposta final no Discord
```

## Arquivos

| Arquivo | Funcao |
| --- | --- |
| `n8n/Comando_slash_Nic_Agenda.json` | Recebe o slash command `/agenda` e encaminha a interacao para processamento. |
| `n8n/Processar_slash_Nic_Agenda.json` | Interpreta a acao, consulta ou altera eventos no Google Calendar e responde ao Discord. |

## Workflows

### Comando slash Nic Agenda

| Item | Valor |
| --- | --- |
| Status no export | Ativo |
| Webhook | `discord-agenda-slash` |
| Nos principais | `Webhook1`, `If`, `HTTP Request1` |

Responsabilidade: receber a interacao, validar o fluxo inicial e encaminhar para o processamento da agenda.

### Processar slash Nic Agenda

| Item | Valor |
| --- | --- |
| Status no export | Ativo |
| Webhook | `processar-agenda` |
| Nos principais | `Webhook Discord`, `Interpretar Comando`, `Switch Acao`, `Preparar Evento`, `Buscar Eventos`, `Criar Evento Google Agenda`, `Deletar Evento`, `Listar Agendas Para Sincronizar`, `Responder ...` |

Responsabilidade: executar a acao solicitada no Google Calendar e atualizar a resposta no Discord.

## Exemplos de uso

```txt
/agenda acao:hoje
/agenda acao:amanha
/agenda acao:semana
/agenda acao:dia data:17/06/2026
/agenda acao:criar titulo:Reuniao Cliente data:17/06/2026 hora:14:00 email:cliente@email.com
/agenda acao:excluir titulo:Reuniao Cliente
/agenda acao:sincronizar
```

## Integracoes

- Discord Slash Commands.
- n8n self-hosted.
- Google Calendar API.
- Google OAuth2.

## Manutencao

- Conferir permissoes da credencial do Google Calendar.
- Validar nomes e IDs das agendas usadas na sincronizacao.
- Testar criacao e exclusao em uma agenda controlada antes de alterar producao.
- Revisar webhooks e segredos antes de publicar os exports.
