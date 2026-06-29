# Checklist de commit

Use esta lista antes de commitar alteracoes neste repositorio.

## Organizacao

- [ ] Conferir se cada projeto tem `README.md` atualizado.
- [ ] Confirmar se novos exports n8n estao na pasta do projeto correto.
- [ ] Evitar arquivos soltos na raiz, exceto `README.md` e itens de configuracao do repositorio.
- [ ] Guardar referencias antigas em `docs/archive/` quando ainda forem uteis.

## Seguranca

- [ ] Revisar exports JSON em busca de tokens, webhooks sensiveis, segredos e credenciais.
- [ ] Rotacionar webhooks ou tokens que tenham sido versionados por engano.
- [ ] Remover dados pessoais ou operacionais que nao precisam estar no historico Git.
- [ ] Confirmar que credenciais do n8n, Google, Discord e OpenAI nao foram expostas em texto puro.

## Validacao

- [ ] Rodar `git status --short`.
- [ ] Revisar `git diff --stat`.
- [ ] Abrir os READMEs alterados e verificar se os caminhos citados existem.
- [ ] Validar se os JSONs continuam parseaveis.

## Sugestao de commit

```txt
docs: organiza documentacao das automacoes NIC
```
