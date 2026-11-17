# 03 · Como um projeto nasce

## O caminho
1. **Ideia.** Você conta o que quer em linguagem normal.
2. **Conversa de clareza.** O orquestrador pergunta: quem usa, que problema resolve, qual o mínimo que já vale a pena (o MVP).
3. **Decisão registrada.** O que ficou decidido vai para `.agents/DECISOES_ARQUITETURAIS.md` (data, decisão, motivo). Decisão escrita não se perde e não é "reinventada" na próxima conversa.
4. **Pasta do projeto.** `~/Projetos/<projeto>/` com `git init`, `CHECKPOINT.md` e `.agents/BACKLOG.md` próprios.
5. **Backlog.** Tarefas pequenas, uma por vez, em `.agents/BACKLOG.md`, cada uma com linha `**Status:**`.
6. **Gate 1.** A primeira tarefa é escrita completa em `.agents/propostas/G1_<ID>.md` (modelo em `MODELOS/G1.md`).
7. **Execução → Gate 2 → Auditoria → Teste → Gate 3 → Produção.** Capítulos 04 a 07.

## O Gate 1 (a tarefa bem escrita)
Uma tarefa ruim gera retrabalho. Uma tarefa boa contém:
- **Contexto:** por que existe.
- **Arquivos de entrada e de saída:** o que ler e o que criar/alterar.
- **Critérios de aceite** no formato EARS: `QUANDO <situação>, O SISTEMA DEVE <resultado>`; também `NÃO DEVE` para o que nunca pode acontecer.
- **Armadilhas:** erros conhecidos que o executor deve evitar (vêm das lições).
- **Máximo de iterações** (padrão 3) e **quando parar**.
- **Prova exigida:** o que o executor precisa mostrar.

## Regras de escopo
- Cresceu? Entregue o núcleo e registre o resto no backlog. Não inche a tarefa.
- Uma conversa = um objetivo.
- Antes de propor algo, procure se já foi tentado e descartado (lista de "obsoletos" em `docs/OBSOLETOS.md`).

## Exemplo mínimo de tarefa
```
G1 — T-001 — Página inicial com formulário de e-mail
Contexto: capturar interessados antes do lançamento.
Saída: app/page.tsx, app/api/lead/route.ts
Critérios:
 1. QUANDO o visitante enviar um e-mail válido, O SISTEMA DEVE gravar no banco e mostrar "recebido".
 2. QUANDO o e-mail for inválido, O SISTEMA DEVE mostrar o erro e NÃO gravar.
 3. O SISTEMA NÃO DEVE exibir chave de API em nenhum arquivo do navegador.
Armadilhas: rota que responde "ok" sem gravar (falha silenciosa).
Prova: saída dos testes, git diff --stat, CI verde.
```
