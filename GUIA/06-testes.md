# 06 · Testes

## Os três níveis
1. **Testes de unidade/integração:** o código por dentro, rodam em segundos.
2. **CI (verificação automática):** o GitHub roda tudo a cada envio. Se ficar vermelho, não segue. O hook local **não** é o portão; o CI é. Depois de todo envio, confira os workflows antes de dizer "concluído".
3. **E2E (ponta a ponta):** um robô (Playwright) abre o site de verdade, clica e confere. É o teste que se parece com o seu usuário.

## Anti-castelo de areia
Se o usuário **usa a funcionalidade numa tela**, ela exige **teste E2E de tela no ambiente de teste (staging)**, nunca em produção. Antes de confiar no "verde", confirme que o deploy testado é o **código novo** (o endereço de teste aponta para a versão certa).

## Armadilhas reais de teste
- Teste que só olha o status HTTP não prova que o fluxo funciona; simule o clique.
- Mock (imitação) esconde regras de acesso do banco: teste com um usuário de verdade.
- Teste verde com tudo mockado é decoração.
- Parta de conta nova para testar cadastro; conta antiga esconde bug.
- Rode a **suíte completa** antes de enviar; PR rascunho roda o CI de graça.

## Como a IA deve provar (Gate 2)
Saída literal dos testes (não "passou"), `git log`, `git diff --stat`, `git status`, link do CI verde e, para telas, prints do teste E2E.

## Dê nomes aos critérios
Cada critério do Gate 1 (EARS) vira, no mínimo, um teste com o mesmo número. No fim, a prova mostra: critério 1 → teste X → passou.
