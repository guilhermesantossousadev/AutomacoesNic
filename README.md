# Automacoes NIC Labs

Repositorio de backup e documentacao das automacoes desenvolvidas para apoio operacional da NIC Labs.

Este repositorio reune exports de workflows n8n, documentacao tecnica e referencias de integracoes usadas em bots e automacoes corporativas. Ele nao deve ser tratado como ambiente de producao; a finalidade principal e preservar os projetos, facilitar manutencoes futuras e deixar o historico pronto para versionamento.

## Projetos

| Projeto | Descricao | Principais integracoes |
| --- | --- | --- |
| `Gestao_de_capacidade_Operacional` | Automacao de escalas, ausencias e atualizacoes operacionais via Discord e Google Chat. | Discord, n8n, Google Apps Script, Google Sheets, Google Chat |
| `Nic-Doc-Ai` | Analise inteligente de documentos enviados pelo Discord usando IA. | Discord, n8n, OpenAI, processamento de PDF/DOCX/TXT |
| `Nic_Agenda_Ai` | Consulta, criacao, exclusao e sincronizacao de eventos de agenda pelo Discord. | Discord, n8n, Google Calendar |

## Estrutura

```txt
.
|-- Gestao_de_capacidade_Operacional/
|   |-- README.md
|   `-- codigos workflows n8n/
|-- Nic-Doc-Ai/
|   |-- README.md
|   `-- workflows n8n/
|-- Nic_Agenda_Ai/
|   |-- README.md
|   `-- n8n/
|-- docs/
|   |-- WORKFLOWS.md
|   |-- COMMIT_CHECKLIST.md
|   `-- archive/
`-- README.md
```

## Documentacao complementar

- [Mapa dos workflows](docs/WORKFLOWS.md): lista os exports n8n, responsabilidades, endpoints e principais nos.
- [Checklist de commit](docs/COMMIT_CHECKLIST.md): roteiro rapido antes de versionar novas alteracoes.
- READMEs individuais: cada projeto possui sua propria documentacao com objetivo, fluxo, arquivos e pontos de atencao.

## Cuidados antes de publicar

Os exports podem conter URLs internas, webhooks, identificadores de servicos ou referencias operacionais. Antes de publicar em repositorios publicos, revise os JSONs e rotacione qualquer token, webhook ou segredo que tenha sido exportado junto com os workflows.

## Autor

Guilherme Santos

Estagiario de Infraestrutura e TI - NIC Labs
