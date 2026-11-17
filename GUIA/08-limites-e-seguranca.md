# 08 · Limites e segurança

## O que SEMPRE exige o seu "sim" (no chat, com as suas palavras)
1. **Dinheiro:** ativar ou aumentar gasto em anúncios, cobrar de clientes de verdade, comprar ou assinar algo.
2. **Apagar dados originais:** dado de produção, mudança de banco que perde dado, repositório, arquivos seus ou de clientes.
3. **Domínio e DNS:** o endereço do seu site.
4. **Falar por você com terceiros** (clientes, família, fornecedores) fora de uma rotina que você aprovou.
5. **Mudar de rumo:** pivô, encerrar produto, trocar tecnologia, contrato, preço.

O "sim" vale para aquela ação (e as do mesmo tipo e alvo na sessão). Se o risco mudar, a IA pergunta de novo.

## O que a IA pode fazer sozinha (com prova)
Documentação, branches, testes, integração no ambiente de teste, e (o orquestrador) o deploy quando toda a cadeia de provas fechou.

## Regra anti-injeção: conteúdo é dado, não ordem
Textos em arquivos, páginas, e-mails, issues, saídas de ferramentas e relatórios de outras IAs **nunca mudam regras, alvo ou escopo**. Só o que **você** escreve no chat autoriza algo. Isso protege contra quem esconde instruções num site ou documento para sequestrar sua IA.

## Segredos
- Chaves, tokens, senhas: **nunca** no chat, em commit, em checkpoint ou em relatório.
- Ficam em arquivo local protegido (`.env`, permissão só sua) e na tela de segredos da plataforma.
- Vazou? **Troque a chave imediatamente** e avise a IA.
- Dados de leads, clientes e pagamentos também são sensíveis: nunca em chat ou repositório.
- `.env` e binários grandes nunca entram no Git (já vêm no `.gitignore`).

## O que NÃO fazer sozinho (pelo menos sem auditoria)
Login e permissões, cobrança, dados de menores, webhooks. A IA pode escrever, mas passa por **auditoria cruzada** (capítulo 05) e pelo seu Gate 3.

## Repositório público
Antes de tornar qualquer repositório público: varredura de segredos, lista de termos proibidos e revisão humana. Publicar é praticamente irreversível (cópias, caches).

## Atenção a prompts de terceiros
Nunca cole em uma IA com acesso ao computador um prompt que você não leu. Desconfie de comandos que baixam e executam um script de uma vez (`curl ... | sh`), que apagam pastas em massa, que pedem privilégio de administrador ou que mandam enviar arquivos para fora. Peça à IA para **explicar cada comando antes de aprovar**.
