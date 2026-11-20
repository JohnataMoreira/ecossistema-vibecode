# 02 · As IAs e seus papéis

> Papéis são fixos; ferramentas são exemplos de hoje. Use as que você tem. Comece com **uma** (o orquestrador) e vá somando.

## 🧭 Estrategista / Orquestrador — Claude (Desktop ou Claude Code)
- **Faz:** conversa com você, decide arquitetura, escreve a tarefa (Gate 1), despacha, **confere** o que os executores entregam (Gate 2 e 3), cuida de deploy, coordena a memória.
- **Use quando:** decisão que afeta vários projetos; qualquer coisa que dependa das conexões do Composio; revisar entregas.
- **Não use para:** escrever milhares de linhas de código com a tarefa já pronta (delegue).

## 🛠️ Executor — Antigravity (Gemini), Codex (GPT) ou qualquer IA que escreva código
- **Fazem:** escrevem o código **numa pasta/branch próprios**, rodam testes, entregam com **prova literal**, atualizam a memória.
- **Como acionar:** você abre o arquivo de tarefa (Gate 1) e diz "execute `<arquivo>`". O Codex funciona melhor numa conversa nova com um objetivo verificável.
- **Regra de ouro:** dois executores **nunca** mexem no mesmo arquivo ao mesmo tempo.

## 🔍 Auditor de outra família — Codex (exemplo) ou qualquer IA de família diferente do executor

> **Regra:** o auditor de uma tarefa nunca é da mesma família do executor dela. Se o Codex executou, audita Claude ou Gemini; se o Antigravity executou, audita Codex ou Claude.
- **Faz:** revisa o que **outro modelo** escreveu, procurando brechas (segurança, regras de acesso, pagamento, dados de menores) e testes que não testam nada. Também escreve e roda os **testes de tela (E2E)**.
- **Por que outra família:** modelos da mesma família tendem a errar do mesmo jeito. Um de fora enxerga o ponto cego.

## 🌐 Pesquisa pesada e execução visual — Manus
- **Faz:** pesquisa de mercado, benchmarks, tarefas dentro de sites e painéis (navegador), publicação e respostas em redes por tarefa combinada, e também código em par com os executores.
- **Cuidado:** plataformas podem detectar automação em painéis; se pedirem verificação, pare e avise você.

## 📚 Pesquisa/copy com o seu contexto — Gemini + NotebookLM (e Spark)
- **Faz:** debate ideias e escreve texto **sabendo do seu projeto** (você alimenta com documentos). O Spark roda pesquisas em segundo plano dentro do ecossistema Google.
- **Nunca:** mexe em produção nem é fonte técnica final.

## 🔌 Composio — a tomada universal
Todas as conexões (GitHub, Gmail, Drive, Instagram, Stripe, Cloudflare...) em um só lugar. Veja `COMPOSIO/README.md`.

## Tabela de decisão
| Tarefa | Quem |
|---|---|
| Decidir, planejar, escrever a tarefa | Orquestrador |
| Construir código com a tarefa pronta | Executor (A ou B) |
| Auditar e testar telas | Auditor (família diferente do executor) |
| Pesquisar mercado, operar painéis | Manus |
| Debater ideia/copy com contexto | Gemini + NotebookLM |
| Publicar nas redes, ler dados de apps | Composio (por qualquer IA autorizada) |

## Como montar o seu time aos poucos
- **Nível 1:** só o Orquestrador + memória + Gates.
- **Nível 2:** + um segundo modelo como executor/auditor.
- **Nível 3:** + pesquisa/visual e Carteiro.
O prompt-mestre configura apenas o que você tem hoje.

## Cenários: com quais IAs você conta?
Papéis são fixos; as marcas são escolha sua. Na configuração, a sua IA pergunta quais você usa e explica os cenários:
- **A · Uma IA só.** Ela orquestra e executa. Para auditar, abra uma **conversa nova** com o prompt do auditor, exija testes e prova literal, e leia o laudo você mesmo. É uma auditoria mais fraca (mesma família erra do mesmo jeito): diga isso no `docs/ECOSSISTEMA.md` e adicione uma segunda IA quando puder.
- **B · Duas IAs de famílias diferentes.** Uma executa, a outra audita, e vocês alternam. Já entrega o ganho principal. Funciona com qualquer par (por exemplo, Claude + Codex, Claude + Gemini ou Codex + Antigravity).
- **C · Três ou mais.** Orquestrador, um ou mais executores (em pastas/branches separados) e um auditor de outra família. Some pesquisa e navegador quando precisar.
Sem Codex, sem Antigravity, sem Manus: o kit funciona do mesmo jeito. Só o papel precisa ser preenchido.
