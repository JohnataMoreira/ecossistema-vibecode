# 04 · Como o código é construído

## Princípios
- **Pasta separada por executor.** Cada tarefa roda em um *branch* (linha de trabalho) e, se possível, numa *worktree* (cópia de trabalho). Assim dois executores não se atropelam e o trabalho principal fica intacto.
- **Parte da base atual.** O executor sempre começa do que está mais recente (`git fetch` + atualizar). Branch velho traz de volta coisas já removidas.
- **Pequeno e frequente.** Commits claros ("feat: formulário de e-mail"), nunca um commit gigante.
- **Sem atalhos.** Proibido: pular verificações (`--no-verify`), forçar envio (`force-push`), reescrever histórico publicado, resolver conflito às cegas.
- **Sem gambiarra.** Nada de `TODO: arrumar depois`. Velocidade que gera retrabalho é dívida com juros.

## O ciclo de uma tarefa
1. Executor lê o Gate 1.
2. Cria branch/worktree próprio.
3. Escreve o código **e os testes**.
4. Roda tudo: testes, verificação de tipos, lint, build.
5. Faz commit(s).
6. Abre o pedido de integração (Pull Request) e espera a **CI** (verificação automática no GitHub).
7. Entrega o **relatório com prova** (Gate 2): saída literal, não resumo.

## Banco de dados
- Mudanças que **só adicionam** (criar tabela/coluna) são de risco menor e rodam primeiro no ambiente de teste.
- Mudanças que **apagam ou perdem dado** exigem o seu "sim" (capítulo 08).
- Toda mudança de banco vive em arquivo versionado (migration), nunca feita "no clique" sem registro.

## Ambientes
- **Local:** o computador do executor.
- **Staging (teste):** cópia da produção para testar de verdade, sem risco aos usuários.
- **Produção:** o que os usuários usam. Só chega lá depois dos Gates.

## Disco e máquina
Builds e testes pesados consomem disco e memória. Meça antes de limpar, rode um por vez e não deixe o disco ficar abaixo de ~15 GB livres.
