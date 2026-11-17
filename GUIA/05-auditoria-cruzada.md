# 05 · Auditoria cruzada

## Por quê
Um modelo revisando o próprio trabalho concorda consigo mesmo. Um modelo **de outra família** (por exemplo, quem escreveu foi Gemini e quem audita é GPT) pega falhas que o primeiro não vê.

## Quando auditar (risco alto)
Qualquer mudança que toque: **login e permissões**, **regras de acesso do banco (RLS)**, **pagamentos**, **dados de crianças ou dados pessoais sensíveis**, **webhooks**, **segredos**.

## Como pedir
1. Escreva o pedido de auditoria (modelo em `MODELOS/SYSTEM_PROMPT_AUDITOR.md`): o que mudou, onde, quais riscos você teme.
2. O auditor lê **o código e a branch**, não o resumo do executor.
3. Devolve um laudo com severidade: **bloqueante / importante / menor**, cada item com arquivo, linha e como reproduzir.
4. O executor corrige no **mesmo branch**; o auditor reconfere o que mudou.
5. O orquestrador decide com evidência. Em segurança, **o auditor segura até haver prova em contrário**.

## O que o auditor sempre procura
- **Falha silenciosa:** código que responde "sucesso" sem fazer o trabalho.
- **Teste que não testa:** passa mesmo se o código estiver quebrado.
- **Segredo no código** ou valor padrão inseguro.
- **Verificação ausente:** a regra existe no papel, mas ninguém a chama.
- **Isolamento entre usuários:** um usuário vendo dado de outro.
- **Relatório que não bate com o git** (o executor "entregou" algo que não existe).

## Regra de ouro
Auditoria não é burocracia: é o que separa "funciona na minha máquina" de "é seguro para pessoas reais".
