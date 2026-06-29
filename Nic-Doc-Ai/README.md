# NIC Doc AI

Sistema de análise inteligente de documentos integrado ao Discord, desenvolvido para automatizar a leitura, interpretação e extração de informações relevantes através de Inteligência Artificial.

O sistema utiliza **Discord Slash Commands**, **n8n** e **OpenAI**, permitindo que usuários enviem documentos diretamente pelo Discord e recebam análises estruturadas em segundos.

---

# Objetivo

O NIC Doc AI foi criado para reduzir o tempo gasto na leitura de documentos técnicos, funcionais e corporativos.

Através de IA, o sistema transforma documentos em informações úteis para equipes de:

* Tecnologia
* Produto
* Negócios
* Processos
* Gestão de Projetos

---

# Arquitetura

```txt
Usuário
   │
   ▼
Discord
   │
   ▼
Slash Command (/ndoc)
   │
   ▼
Workflow 1 (Discord Gateway)
   │
   ├── Resposta imediata ao usuário
   │
   ▼
Workflow 2 (Processamento)
   │
   ├── Validação de segurança
   ├── Download do documento
   ├── Extração de texto
   ├── OpenAI
   └── Resposta final
   │
   ▼
Discord
```

---

# Stack

## Plataforma

* Discord Developer Portal
* Discord Slash Commands
* n8n Self Hosted

## Inteligência Artificial

* OpenAI API
* GPT-4.1 Mini

## Processamento de Arquivos

* Extract From File (n8n)
* PDF
* DOCX
* TXT

---

# Funcionalidades

## Processamento de Documentos

* Leitura de arquivos PDF
* Leitura de arquivos DOCX
* Leitura de arquivos TXT
* Download automático de anexos
* Extração automática de texto
* Controle de tamanho de documentos

## Inteligência Artificial

### Resumo Executivo

```txt
/ndoc
ação: resumo
```

Gera um resumo objetivo do documento.

---

### Requisitos

```txt
/ndoc
ação: requisitos
```

Extrai:

* Requisitos Funcionais
* Requisitos Não Funcionais

---

### Regras de Negócio

```txt
/ndoc
ação: negocio
```

Identifica regras de negócio presentes no documento.

---

### Pendências

```txt
/ndoc
ação: pendencias
```

Localiza:

* Pendências
* Riscos
* Dúvidas
* Informações faltantes

---

### Tarefas

```txt
/ndoc
ação: tarefas
```

Transforma o conteúdo em uma lista prática de tarefas.

---

# Fluxo dos Workflows

## Workflow 1 - Discord Slash Command

Responsável por:

* Receber interações do Discord
* Validar endpoint
* Responder imediatamente ao usuário
* Encaminhar dados para o Workflow 2

Webhook:

```txt
discord-ndoc-path
```

---

## Workflow 2 - Processamento

Responsável por:

* Validar segurança
* Baixar documentos
* Extrair texto
* Chamar OpenAI
* Atualizar resposta original no Discord

Webhook:

```txt
ndoc-processar-prod
```

---

# Segurança

A comunicação entre workflows utiliza:

```txt
X-NIC-Automation-Secret
```

Validação obrigatória:

```txt
Nic_labsautomationsecret145885454548547
```

Fluxos sem autenticação válida são descartados.

---

# Estrutura dos Comandos

## Slash Command

```txt
/ndoc
```

Parâmetros:

### ação

Opções disponíveis:

```txt
resumo
requisitos
negocio
pendencias
tarefas
```

### arquivo

Tipos suportados:

```txt
PDF
DOCX
TXT
```

---

# Exemplo de Uso

Resumo:

```txt
/ndoc
ação: resumo
arquivo: documento.pdf
```

---

Extração de Requisitos:

```txt
/ndoc
ação: requisitos
arquivo: documento.docx
```

---

Identificação de Pendências:

```txt
/ndoc
ação: pendencias
arquivo: documento.pdf
```

---

# Roadmap

## Versão Atual

* [x] Discord Slash Commands
* [x] n8n Self Hosted
* [x] OpenAI
* [x] PDF
* [x] DOCX
* [x] TXT
* [x] Segurança entre workflows
* [x] Processamento assíncrono

## Próximas Versões

* [ ] Histórico de análises
* [ ] Banco de dados SQLite
* [ ] Exportação Markdown
* [ ] Exportação PDF
* [ ] Respostas em Embed
* [ ] Logs de utilização
* [ ] Dashboard Administrativo
* [ ] Múltiplos idiomas
* [ ] Cache de documentos

---

# Ambiente

Servidor n8n:

```txt
https://n8n-infra.nic-labs.com
```

Discord:

```txt
NIC Doc AI
```

---

# Autor

**Guilherme Santos**

Estagiário de Infraestrutura e Gerência de TI

NIC Labs

Projeto desenvolvido utilizando Discord, n8n e Inteligência Artificial para automação de análise documental.
