# Lições completas — tudo o que o erro nos ensinou

> **Para a IA:** leia este documento **inteiro** antes de trabalhar com o usuário. Ele condensa mais de 200 lições aprendidas construindo produtos reais com IAs. Cada lição tem **Regra** (o que fazer) e **Por quê** (o que aconteceu ou o risco). Use-as para escrever Gate 1 melhores (seção "Armadilhas"), para conferir entregas e para evitar repetir erros caros.
> **Para a pessoa:** você não precisa decorar nada. Mas ler os temas 1 e 2 já muda a forma como você dirige IAs.
> Os exemplos foram anonimizados. Se você descobrir lições novas, conte nas Discussions: as melhores entram aqui.

---

## TEMA 1 — Confiança em relatório de IA: confira, nunca presuma

1. **Relatório de executor não é prova.** *Regra:* confira na fonte (git, CI, ambiente vivo). *Por quê:* já recebemos relatório afirmando deploy que não existia, relatório de Lighthouse fabricado, "8 entregas de alta qualidade" que não se sustentaram na medição e foto de terceiro publicada como se fosse da pessoa.
2. **Saída reconstruída não vale.** *Regra:* exija a saída literal do comando, não um resumo "reescrito". *Por quê:* resumos escondem falhas.
3. **Gate 2 que não bate com o git é falha grave.** *Regra:* `git log`, `git diff --stat` e `git status` sempre na prova; compare com o que foi dito.
4. **Passar nos critérios numéricos não prova qualidade.** *Regra:* quando o resultado é visual, olhe a tela de verdade (e a tela inicial, não só a interna). *Por quê:* um entregável passou em todos os critérios e estava feio.
5. **"Tudo verde" cego.** *Regra:* medir em vez de crer: crie um teste de aceitação que **mede** o resultado (por exemplo, % do roteiro realmente presente no vídeo). *Por quê:* relatório escrito antes das correções continuou afirmando sucesso.
6. **Concluir "ausente" por busca truncada.** *Regra:* ao afirmar que algo não existe, busque no repositório inteiro e leia até o fim. *Por quê:* `grep` com saída cortada levou a alarme falso.
7. **Checkpoint é cumulativo.** *Regra:* leia até o fim antes de afirmar estado; confira também o BACKLOG.
8. **Auditoria "não confie só na documentação".** *Regra:* cruze documento × código × produção ao vivo × painel. *Por quê:* a doc dizia uma coisa e o sistema fazia outra.
9. **Avalie ferramenta de IA pela pior saída, não pela melhor promessa.** Vídeos de demonstração mostram o melhor caso.
10. **Decisão "resolvida" só de boca não existe.** *Regra:* escreva no checkpoint ou na decisão arquitetural na mesma sessão.

## TEMA 2 — Testes e CI: o que é prova de verdade

11. **O hook local não é o portão; a CI é.** *Regra:* depois de todo envio, confira os workflows antes de declarar "concluído". *Por quê:* a CI ficou vermelha por dias com tudo "passando" localmente.
12. **Gate 2 sem a suíte completa e sem CI não é prova.** Rode tudo; PR rascunho roda a CI de graça.
13. **Teste só de status ou JSON não prova fluxo de clique.** Se o produto é "clicar no link", simule o clique.
14. **Mock esconde regra de acesso do banco.** Teste com usuário real; um mock devolveu sucesso onde a regra real bloquearia.
15. **Teste de tela com cadastro:** parta de conta nova de verdade e espere o que o formulário preenche sozinho.
16. **Anti-castelo de areia:** funcionalidade de tela exige E2E na staging, nunca em produção; confirme que o deploy testado é o novo (endereço aponta para o commit certo).
17. **Bug "só no navegador X":** reproduza no motor real antes de corrigir; o componente suspeito pode ser inocente.
18. **Conserto que liga um caminho que nunca rodou:** confira o que ele vai **produzir** antes de ligar.
19. **Critério de teste para uma tela que nenhuma tarefa criou:** confirme que o destino existe na linha principal antes de escrever o critério.
20. **Medir antes de propor otimização.** Número vence palpite.

## TEMA 3 — Segurança e banco de dados

21. **Webhook com segredo padrão fixo é brecha esperando ativação.** Sem segredo configurado, recuse; valide sempre a assinatura.
22. **Valor inicial "sucesso" em fluxo de pagamento é fraude garantida.** O estado inicial é "não pago".
23. **Valide cota antes de inserir** em operações com vários usuários/famílias.
24. **Reação/curtida em dado compartilhado = operação atômica no banco**, não ler-e-gravar no código.
25. **Valide pertencimento e posse antes de qualquer ação em recurso de grupo.**
26. **Estruturas de resposta em árvore precisam de limite de profundidade no servidor.**
27. **Rota "stub" que responde sucesso é pior que erro.** O formulário diz "enviado", o Pixel conta conversão e o lead some; e o SDK de e-mail pode não lançar erro.
28. **Rota que lê dado de OUTRO usuário com a sessão do usuário falha por causa da regra de acesso.** Use o cliente com o privilégio correto, **depois** de validar quem pergunta.
29. **Fluxo de aceite lido com a sessão do convidado:** a regra devolve `null` e o código "funciona" criando duplicata.
30. **Convite "ativo" sem olhar a validade trava o reconvite para sempre.**
31. **Funções com duas sobrecargas e parâmetros padrão quebram toda chamada via API do banco.**
32. **Gate de segurança que depende de um valor gravado na criação:** audite quem **escolhe** o valor, não só quem o lê.
33. **Executor sem acesso ao cofre inventa fallback com segredo no código.** Valide decodificando o valor, não só o formato.
34. **Parâmetro aceito não é parâmetro aplicado:** configuração criada por API se verifica lendo o objeto de volta.
35. **Job de IA nunca escreve em campo que o usuário escreve.** Tabela da IA vazia em produção é sintoma.
36. **Callbacks de autenticação:** sanitize destinos de retorno; URLs de retorno de rotas filhas exigem curinga `/**`; o campo de Client ID web não aceita ID de outra plataforma quando há segredo.
37. **Logout seletivo exige verificação de autenticação dentro do componente da página**, não só no guarda geral.
38. **Cadastro "sem atrito" que ainda dispara e-mail de confirmação sequestra o fluxo de convite.**
39. **Formulário que pede o que o sistema já sabe trava o usuário.** E todo botão "compartilhar" deve levar ao **mesmo** caminho de entrada.
40. **Documento societário/fiscal:** confira campo a campo contra a intenção declarada; nunca aceite por inferência.

## TEMA 4 — Infraestrutura, custos e plataformas

41. **CI sem filtro de caminhos queima minutos em commit de documentação.** Ignore docs no build.
42. **Corte automático de gasto com pausa da produção** derrubou site, páginas e painel de uma vez. Se ligar o corte, saiba o efeito; mantenha o que tem webhook de alto volume em lugar sem cold start (ex.: Workers).
43. **Push na linha principal vira deploy de produção** (até de documentação). Suíte completa antes de empurrar.
44. **Build "Standard" cobra por minuto:** configure "Ignored Build Step" por projeto.
45. **Deploy só de branch principal no projeto de produção;** staging recebe o resto.
46. **Migration no diretório errado fica invisível** e se disfarça de "falta de conector".
47. **`node_modules`, `.env` e binários commitados incham o repositório e vazam segredos.** `.gitignore` desde o primeiro commit.
48. **E-mail:** "Verified" no provedor não prova DKIM saudável (um registro TXT órfão duplicado deu falha); bloqueio de envio enquanto "pending"; devolução vira supressão silenciosa.
49. **Token de API:** o nome do template não diz o que ele pode; teste as permissões por chamada.
50. **Plataforma de anúncios muda a API:** confira a documentação oficial antes de especificar.
51. **Agendador gratuito do GitHub é "melhor esforço"** e ficou dias sem disparar. Use gatilhos independentes (Worker, cron externo) e um vigia.
52. **Trava de concorrência vive no lugar errado:** o `flock` num diretório temporário local não evita duplicata entre máquinas. Releia o estado **no último instante** antes de publicar; cuidado para não confundir "ler estado" com "enviar estado".
53. **Duas rodadas sobrepostas publicaram o mesmo post duas vezes** (e a reconciliação por busca na mídia não pega *stories*).
54. **Validador e gerador precisam concordar sobre onde ficam os dados** (hashtags numa coluna × na legenda): 15 posts ficaram travados e ninguém viu porque os stories passavam.
55. **HTML renderizado em navegador headless não enxerga caminho de disco em `url(...)`:** a tela do celular saiu **preta** em peças publicadas. Embuta a imagem como data URI e teste o resultado (verificação automática de tela preta).
56. **Rate limit e cobrança de conectores:** meça quantas chamadas uma rodada gasta; planos gratuitos têm teto. Poupe chamadas com uma "guarda".
57. **Integrações da Meta:** "Permitir acesso a mensagens" desligado = silêncio total (sem webhook, sem erro). A escolha do tipo de login do app é irreversível. A API não apaga mídia publicada; o Facebook pode recusar exclusão por falta de permissão.
58. **Uma private reply por comentário, dentro de 7 dias;** trate a reentrega de webhook com chave única; o servidor deve responder 200 em menos de 1 s e processar depois.

## TEMA 5 — Seu computador e suas ferramentas

59. **IA em ambiente isolado grava arquivos no lugar errado.** Confira que o arquivo existe no **seu** computador, no caminho real.
60. **Til (`~`) entre aspas não expande** e cria uma pasta literal chamada "~".
61. **Processo e segredos:** não liste processos com argumentos; o ambiente dos executores pode conter segredos. E nunca leia o cofre com `grep` (o filtro de ocultação falha no formato que você não previu).
62. **Ferramenta de terminal que estoura o tempo:** confira o estado real antes de repetir o comando.
63. **Disco do Mac:** o espaço "livre" cai por *snapshots* locais do Time Machine, não só por arquivos. Meça antes de limpar. Com 16 GB de memória, build/E2E pesado só com disco e memória folgados, e um por vez. Mantenha o disco acima de ~15 GB livres.
64. **Execução sem supervisão ("headless")** costuma negar comandos compostos. Prefira acionar o executor pelo aplicativo, com a tarefa em arquivo.
65. **Horário nos registros:** sempre o de Brasília (ou o seu fuso), sempre com a mesma convenção.
66. **Commit em pasta compartilhada com executor ativo** gera confusão: cada executor, uma worktree.
67. **Memória automática de ferramentas** exige regra de precedência explícita: a fonte é o arquivo versionado.
68. **Skill/ferramenta de tracking aplicada sem cruzar com as decisões e a política do projeto** produziu medição indevida. Cruze com `DECISOES_ARQUITETURAIS.md`.

## TEMA 6 — Processo e memória

69. **O estado vivo de um runbook mora em uma seção só;** "decisões" não carregam números que envelhecem.
70. **Documento tem dono.** Duas cópias da mesma verdade divergem.
71. **Rotacione em vez de apagar:** mover para `historico/`.
72. **Sessão que fecha com "GO de push pendente" perde trabalho.** Fechar = commit + envio.
73. **Prepare o despacho em arquivo e peça uma linha:** "execute `<arquivo>`". Evita ambiguidade e permite trocar de conta sem perder o fio.
74. **Tarefa grande demais não entrega.** Núcleo primeiro; o resto no backlog.
75. **Limite de iterações** (padrão 3) evita loop infinito de retrabalho.
76. **Auditor de outra família:** um erro bloqueante (validação não chamada na rota) passou despercebido ao modelo que o escreveu e ao conferente de amostragem.

## TEMA 7 — Conteúdo, redes e anúncios

77. **Peça de produto com tela de app precisa de print real** e do aviso de "família fictícia" quando os dados são de demonstração.
78. **Nunca publique foto de terceiro como sendo da pessoa.**
79. **Campanha de "engajamento" otimizada para clique não mede conversa:** só ligue com a meta e a rota conferidas.
80. **Teste de medição (CAPI):** prove o servidor direto antes de pedir teste manual e confira os destinos das variáveis antes do E2E.
81. **Imagem de teste fica fora do repositório.**
82. **Crescimento esperado:** se seguidores e engajamento não crescem mês a mês, o método precisa de revisão.
83. **Humano aprova o que fala por ele.** Posts só saem com status aprovado; rascunho nunca publica.

## TEMA 8 — Como decidir quando há risco

84. **Decisão irreversível entra primeiro na fila do "sim":** tipo de login de app, apagar dado, domínio, repositório público.
85. **Desconfie de benchmark e de "ferramenta mágica".** Registre o veredito (adotar / não adotar / só ideia) e o motivo em `OBSOLETOS.md` para não reavaliar do zero.
86. **Contenha primeiro, investigue depois** em emergência.

---

## Como usar este documento
- **Ao escrever um Gate 1:** copie 2 a 5 lições relevantes para "Armadilhas".
- **Ao conferir um Gate 2:** percorra os temas 1 e 2.
- **Ao tocar segurança ou banco:** tema 3 inteiro.
- **Ao encontrar algo novo:** registre uma lição nova no `LESSONS_LEARNED.md` do QG (Regra + Por quê + data) e, se for útil para todos, conte nas Discussions.
