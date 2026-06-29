# 🤖 NIC Bot Escalas

Sistema corporativo de automação para gestão de escalas de trabalho e ausências da NIC Labs, integrado ao Discord, n8n, Google Apps Script, Google Sheets, e Google Chat.

---

# 📋 Visão Geral

O NIC Bot Escalas centraliza a consulta e distribuição de informações sobre escalas de trabalho e ausências dos colaboradores.

Através do comando `/update` no Discord, gestores e equipes autorizadas podem disparar uma atualização em tempo real, que consulta as planilhas corporativas, processa os dados e publica relatórios automaticamente nos canais de comunicação da empresa.

---

# 🏗️ Arquitetura da Solução

```txt
Usuário
   │
   ▼
Discord (/update)
   │
   ▼
Workflow Discord Slash Command (n8n)
   │
   ├── Resposta imediata ao Discord
   │
   ▼
Workflow Principal (n8n)
   │
   ▼
Google Apps Script
   │
   ▼
Google Sheets
   │
   ▼
Processamento de Dados
   │
   ├── Relatório de Escalas
   └── Relatório de Ausências
   │
   ▼
Google Chat
```

---

# 🚀 Funcionalidades

## Escalas

* Consulta automática da escala diária
* Agrupamento por colaborador
* Exibição de horários de entrada e saída
* Identificação da área de atuação
* Atualização automática programada

## Ausências

* Ausentes hoje
* Ausentes amanhã
* Próximas ausências
* Retorno hoje
* Retorno amanhã
* Tratamento de ausências parciais e dia inteiro

## Discord

* Slash Command `/update`
* Resposta imediata ao usuário
* Integração com n8n via Webhook

## Automação

* Execução manual
* Execução agendada
* Controle de alterações para evitar mensagens duplicadas
* Integração com Google Workspace

---

# 🛠️ Tecnologias Utilizadas

## Backend

* Node.js
* Discord.js

## Automação

* n8n

## Google Workspace

* Google Apps Script
* Google Sheets
* Google Chat

## Infraestrutura

* Docker
* GitHub
* Linux Server
* Kubernetes (planejado)

---

# 📂 Estrutura do Projeto

```txt
nicbotescalas/

├── n8n/
│   ├── Discord Slash Command.json
│   └── Workflow Principal.json
│
├── apps-script/
│   └── bot_unificado_google_chat.gs
│
└── README.md
```

# 💬 Comandos Disponíveis

## Atualização Manual

```txt
/update
```

Executa:

* Atualização da escala do dia
* Atualização das ausências
* Envio dos relatórios para o Google Chat

---

# 📊 Relatórios Gerados

## Escala de Trabalho

```txt
📋 Escala de Trabalho

Alvaro Neto
Infraestrutura
07:45 às 14:00

Lorena Maielo
Gestão
09:00 às 16:00
```

## Relatório de Ausências

```txt
🏖️ Relatório de Ausências

Ausentes Hoje
Retornando Hoje
Ausentes Amanhã
Próximas Ausências
Retornando Amanhã
```

## Recomendações

* Utilizar segredo compartilhado entre Discord e n8n
* Restringir execução por cargo
* Restringir execução por canal
* Rotacionar tokens periodicamente
* Utilizar variáveis de ambiente

---

# 📦 Deploy

O projeto pode ser executado em:

* Servidor Linux
* Docker
* n8n Self Hosted

---

# 💾 Backup

Recomenda-se backup periódico de:

* Workflows n8n
* Código Apps Script
* Variáveis de ambiente
* Repositório GitHub
* Configurações do Discord Developer Portal

---

# 📈 Benefícios

* Eliminação de consultas manuais
* Atualização em tempo real
* Centralização da comunicação
* Redução de erros operacionais
* Escalabilidade corporativa
* Fácil manutenção

---

# 👨‍💻 Autor

Guilherme Santos

Estagiário de Infraestrutura e Gerência de TI – NIC Labs

GitHub:
https://github.com/guilhermesantossousadev
