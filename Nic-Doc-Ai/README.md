# NIC Doc AI

Sistema de analise inteligente de documentos integrado ao Discord. O usuario envia um arquivo pelo comando `/ndoc`, escolhe o tipo de analise e recebe uma resposta estruturada gerada por IA.

## Objetivo

Automatizar a leitura de documentos tecnicos, funcionais e corporativos, reduzindo o tempo gasto em triagem manual e extraindo informacoes uteis para tecnologia, produto, processos e gestao.

## Funcionalidades

| Area | Recursos |
| --- | --- |
| Documentos | Leitura de PDF, DOCX e TXT; download automatico do anexo enviado no Discord. |
| Processamento | Extracao de texto pelo n8n e montagem de prompt conforme a acao escolhida. |
| IA | Envio do conteudo para a OpenAI e formatacao da resposta. |
| Discord | Atualizacao da resposta original no Discord apos o processamento. |

## Acoes do comando

| Acao | Resultado esperado |
| --- | --- |
| `resumo` | Gera um resumo objetivo do documento. |
| `requisitos` | Extrai requisitos funcionais e nao funcionais. |
| `negocio` | Identifica regras de negocio. |
| `pendencias` | Lista pendencias, riscos, duvidas e lacunas. |
| `tarefas` | Transforma o conteudo em tarefas praticas. |

## Fluxo

```txt
Discord /ndoc
    |
    v
Workflow n8n: Comando slash Nic Doc
    |
    v
Workflow n8n: NIC Doc AI - Workflow 2 Processar Corrigido
    |
    v
Download e extracao do arquivo
    |
    v
OpenAI
    |
    v
Resposta final no Discord
```

## Arquivos

| Arquivo | Funcao |
| --- | --- |
| `workflows n8n/Comando_slash_Nic_Doc.json` | Recebe o slash command `/ndoc` e encaminha os dados para processamento. |
| `workflows n8n/Processar.json` | Baixa o arquivo, extrai texto, chama a OpenAI e responde ao Discord. |

## Workflows

### Comando slash Nic Doc

| Item | Valor |
| --- | --- |
| Status no export | Ativo |
| Webhook | `discord-ndoc-path` |
| Nos principais | `Webhook`, `HTTP Request`, `Respond to Webhook` |

Responsabilidade: receber a interacao do Discord e iniciar o processamento assincrono.

### NIC Doc AI - Workflow 2 Processar Corrigido

| Item | Valor |
| --- | --- |
| Status no export | Ativo |
| Webhook | `ndoc-processar-prod` |
| Nos principais | `Webhook Processar /ndoc`, `Extrair Dados`, `Baixar Arquivo`, `Extract From File`, `Montar Prompt`, `OpenAI`, `Formatar Resposta`, `Responder Discord` |

Responsabilidade: executar a analise documental e atualizar a mensagem original do Discord.

## Integracoes

- Discord Slash Commands.
- n8n self-hosted.
- OpenAI API.
- Extrator de arquivos do n8n.

## Exemplo de uso

```txt
/ndoc acao:resumo arquivo:documento.pdf
/ndoc acao:requisitos arquivo:especificacao.docx
/ndoc acao:pendencias arquivo:relatorio.txt
```

## Manutencao

- Conferir limites de tamanho de arquivo antes de processar documentos grandes.
- Validar a credencial da OpenAI no n8n.
- Revisar prompts quando novas acoes forem adicionadas.
- Remover ou mascarar URLs e tokens antes de publicar os exports.
