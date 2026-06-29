# Mapa dos workflows

Este documento resume os exports n8n versionados neste repositorio. Use como indice tecnico para localizar rapidamente o fluxo correto antes de alterar, importar ou revisar uma automacao.

## Visao geral

| Projeto | Workflow | Export | Status |
| --- | --- | --- | --- |
| Gestao de Capacidade Operacional | Discord slash update | `Gestao_de_capacidade_Operacional/codigos workflows n8n/Discord_slash_update.json` | Ativo |
| Gestao de Capacidade Operacional | Discord update -> Apps Script -> Discord | `Gestao_de_capacidade_Operacional/codigos workflows n8n/Discord_update_ AppsScrip.json` | Ativo |
| NIC Doc AI | Comando slash Nic Doc | `Nic-Doc-Ai/workflows n8n/Comando_slash_Nic_Doc.json` | Ativo |
| NIC Doc AI | NIC Doc AI - Workflow 2 Processar Corrigido | `Nic-Doc-Ai/workflows n8n/Processar.json` | Ativo |
| NIC Agenda AI | Comando slash Nic Agenda | `Nic_Agenda_Ai/n8n/Comando_slash_Nic_Agenda.json` | Ativo |
| NIC Agenda AI | Processar slash Nic Agenda | `Nic_Agenda_Ai/n8n/Processar_slash_Nic_Agenda.json` | Ativo |

## Endpoints e chamadas externas

| Workflow | Webhook interno | Chamadas externas observadas |
| --- | --- | --- |
| Discord slash update | `discord-update-path` | Chama o webhook de processamento `update-discord-prod-4185644X`. |
| Discord update -> Apps Script -> Discord | `update-discord-prod-4185644X` | Chama Google Apps Script e webhook de mensagem do Discord. |
| Comando slash Nic Doc | `discord-ndoc-path` | Encaminha para `ndoc-processar-prod`. |
| NIC Doc AI - Workflow 2 Processar Corrigido | `ndoc-processar-prod` | Baixa arquivo do Discord, chama OpenAI e atualiza mensagem original no Discord. |
| Comando slash Nic Agenda | `discord-agenda-slash` | Encaminha para `processar-agenda`. |
| Processar slash Nic Agenda | `processar-agenda` | Consulta, cria, exclui e sincroniza eventos via Google Calendar; atualiza mensagem original no Discord. |

## Gestao de Capacidade Operacional

Fluxo voltado ao comando `/update`. O primeiro workflow recebe a interacao do Discord e o segundo executa a integracao com Google Apps Script, formatando a mensagem final para publicacao.

Pontos de atencao:

- validar se o endpoint do Apps Script continua ativo;
- revisar webhooks de Discord antes de expor o repositorio;
- manter os dois workflows sincronizados, pois o primeiro depende do webhook do segundo.

## NIC Doc AI

Fluxo voltado ao comando `/ndoc`. O primeiro workflow atua como gateway do Discord e o segundo faz o processamento pesado: download do anexo, extracao de texto, prompt, chamada de IA e resposta final.

Pontos de atencao:

- revisar limites de arquivo e tamanho de texto;
- validar a credencial da OpenAI;
- testar cada acao (`resumo`, `requisitos`, `negocio`, `pendencias`, `tarefas`) apos qualquer ajuste no prompt.

## NIC Agenda AI

Fluxo voltado ao comando `/agenda`. O primeiro workflow recebe a interacao e o segundo interpreta a acao solicitada, roteando para consulta, criacao, exclusao ou sincronizacao de eventos.

Pontos de atencao:

- validar credenciais OAuth2 do Google Calendar;
- revisar IDs de agendas usadas na sincronizacao;
- testar exclusao em ambiente controlado antes de usar em agenda real;
- manter o formato de data e hora consistente com o esperado pelo workflow.

## Checklist de importacao no n8n

1. Importar o JSON no ambiente correto.
2. Reassociar credenciais que nao sao exportadas com seguranca pelo n8n.
3. Conferir URLs de webhooks entre workflows dependentes.
4. Ativar o workflow somente depois de testar em modo manual.
5. Executar um comando real no Discord e validar a resposta final.
