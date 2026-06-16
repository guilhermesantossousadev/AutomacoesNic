# 🤖 NIC Agenda Bot

Sistema corporativo de automação de agendas desenvolvido para a NIC Labs.

O projeto integra Discord, Google Calendar, Cloudflare Workers e n8n para permitir consultas, criação, exclusão e sincronização de eventos através de Slash Commands.

---

# 📋 Visão Geral

O objetivo do projeto é centralizar o gerenciamento de agendas corporativas através do Discord.

Os usuários podem executar comandos diretamente no servidor e o sistema consulta ou manipula eventos no Google Calendar sem necessidade de acessar a interface do Google.

---

# 🚀 Funcionalidades

## Consultar Agenda

Comandos disponíveis:

/agenda acao:hoje

/agenda acao:amanha

/agenda acao:semana

/agenda acao:dia

---

## Criar Evento

Exemplo:

/agenda acao:criar titulo:Reunião Cliente data:17/06/2026 hora:14:00 email:cliente@email.com

Funcionalidades:

* Cria evento no Google Calendar
* Adiciona convidado automaticamente
* Define duração padrão de 1 hora
* Envia convite por e-mail

---

## Excluir Evento

Exemplo:

/agenda acao:excluir titulo:Reunião Cliente

Funcionalidades:

* Localiza evento pelo título
* Remove evento da agenda

---

## Sincronizar Agendas

Exemplo:

/agenda acao:sincronizar

Funcionalidades:

* Consulta agendas compartilhadas
* Identifica eventos ainda não copiados
* Replica eventos para agenda central
* Evita duplicação

---

# 🏗 Arquitetura

Discord
↓
Cloudflare Worker
↓
Workflow 01 (Recepção do Slash Command)
↓
Workflow 02 (Processamento)
↓
Google Calendar

---

# 🔧 Tecnologias Utilizadas

Discord Developer Portal

Discord Slash Commands

Cloudflare Workers

n8n Self Hosted

Google Calendar API

Google OAuth2

JavaScript

---

# 📁 Estrutura do Projeto

/workflows
├── workflow_01_comando_slash.json
├── workflow_02_processar_agenda.json

/cloudflare-worker
├── worker.js
├── wrangler.toml

/docs
├── instalacao.md
├── troubleshooting.md
├── arquitetura.md

README.md

---

# ⚙️ Workflow 01

Responsável por:

* Receber requisição do Cloudflare Worker
* Validar chave de segurança
* Extrair parâmetros do Slash Command
* Encaminhar para Workflow 02

Webhook:

/webhook/discord-agenda-slash

Campos recebidos:

applicationId

token

guildId

channelId

usuario

userId

acao

titulo

data

hora

email

---

# ⚙️ Workflow 02

Responsável por:

* Interpretar comando
* Consultar agenda
* Criar evento
* Excluir evento
* Sincronizar agendas
* Retornar resposta ao Discord

Comandos suportados:

hoje

amanha

semana

dia

criar

excluir

sincronizar

---

# ☁️ Cloudflare Worker

Responsável por:

* Validar assinatura do Discord
* Responder PING (type 1)
* Responder ACK imediato (type 5)
* Encaminhar payload para o n8n

Variáveis:

DISCORD_PUBLIC_KEY

N8N_WEBHOOK_URL

NIC_SECRET

---

# 🔐 Segurança

Toda comunicação entre Cloudflare Worker e n8n utiliza:

Header:

x-nic-automation-secret

Valor:

Nic_labsautomationsecret145885454548547

O Workflow 01 valida a chave antes de processar qualquer requisição.

---

# 📅 Google Calendar

Credencial:

Google Calendar OAuth2 API

Permissões necessárias:

https://www.googleapis.com/auth/calendar

https://www.googleapis.com/auth/calendar.events

---

# 🧪 Testes

Consultar agenda:

/agenda acao:hoje

Criar evento:

/agenda acao:criar titulo:Teste data:17/06/2026 hora:14:00 email:teste@email.com

Excluir evento:

/agenda acao:excluir titulo:Teste

Sincronizar:

/agenda acao:sincronizar

---

# 🚨 Troubleshooting

## Interactions Endpoint URL não pôde ser verificada

Verificar:

* Worker online
* Public Key correta
* Resposta ao Discord type 1

---

## redirect_uri_mismatch

Verificar:

Google Cloud Console

Authorized Redirect URIs

A URL deve ser exatamente igual à exibida pelo n8n.

---

## Invalid Webhook Token

O token de interação expirou.

Necessário responder ao Discord em até 15 minutos.

---

## Missing Access

Verificar permissões do bot:

View Channels

Send Messages

Use Application Commands

---

## Invalid Form Body

Verificar parâmetros enviados ao Discord.

Campos obrigatórios:

titulo

data

hora

email

---

# 📦 Backup

Sempre exportar:

Workflow 01

Workflow 02

Cloudflare Worker

Credenciais OAuth

Comandos Slash

Antes de qualquer alteração em produção.

---

# 👨‍💻 Autor

Guilherme Santos

Estagiário de Infraestrutura e Gerência de TI

NIC Labs

Projeto desenvolvido para automação corporativa de agendas utilizando Discord, Google Calendar, Cloudflare Workers e n8n.
