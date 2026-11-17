# DOC_MAP — {{NOME_DO_QG}}
# A bússola: onde vive cada verdade. Se o assunto já tem dono, EDITE o dono; nunca crie um segundo arquivo.

| Verdade | Arquivo DONO | Teto |
|---|---|---|
| Estado e resumo recente | `CHECKPOINT.md` | ~200 linhas |
| Fila de tarefas abertas | `.agents/BACKLOG.md` | ~400 linhas |
| Decisões e invariantes | `.agents/DECISOES_ARQUITETURAIS.md` | — |
| Lições aprendidas | `.agents/LESSONS_LEARNED.md` | — |
| Quem é quem e fronteiras das IAs | `docs/ECOSSISTEMA.md` | — |
| Regras do orquestrador | `docs/SYSTEM_PROMPT_ORQUESTRADOR.md` | — |
| Regras do executor | `docs/SYSTEM_PROMPT_EXECUTOR.md` | — |
| Regras do auditor | `docs/SYSTEM_PROMPT_AUDITOR.md` | — |
| Regras gerais para qualquer IA | `AGENTS.md` | — |
| Ideias descartadas ("não tente de novo") | `docs/OBSOLETOS.md` | — |
| Tarefas escritas (Gate 1) | `.agents/propostas/` | — |
| Concluído (arquivo morto) | `.agents/historico/` | — |

**Rotação:** concluiu no Gate 3 = **mover** o bloco para `.agents/historico/`. "Nunca apagar" = mover.
**Formato:** toda tarefa do BACKLOG tem linha `**Status:**` (PENDENTE / EM ANDAMENTO / ✅ CONCLUÍDA / 🚫 CANCELADA).
