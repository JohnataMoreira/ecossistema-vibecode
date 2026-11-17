# 09 · Memória e sessões

A IA não lembra da conversa de ontem. **O QG lembra.**

## Os arquivos da memória
| Arquivo | O que guarda |
|---|---|
| `AGENTS.md` | Regras gerais para qualquer IA que abrir o projeto |
| `CHECKPOINT.md` | **Onde paramos:** o que foi feito, o que falta, o que depende de você. O mais recente em cima |
| `.agents/BACKLOG.md` | Fila de tarefas abertas, cada uma com `**Status:**` |
| `.agents/DECISOES_ARQUITETURAIS.md` | Decisões (data, o que, por quê). Pesam mais que qualquer tarefa |
| `.agents/LESSONS_LEARNED.md` | Lições. Já vem carregado com as nossas |
| `DOC_MAP.md` | A bússola: qual arquivo é o **dono** de cada assunto |
| `.agents/propostas/` | Os Gates 1 (tarefas) |
| `.agents/historico/` | O que foi concluído (mover para cá, nunca apagar) |

## Precedência (quando dois textos discordam)
1. System prompt do orquestrador → 2. documento dono (via DOC_MAP) → 3. checkpoint e backlog. A "memória automática" de uma ferramenta **não é fonte de verdade**.

## Tetos e rotação
CHECKPOINT ~200 linhas, BACKLOG ~400. Passou? Mova o bloco antigo para `.agents/historico/` (mover, nunca apagar).

## Rotina de sessão
- **Início ("bom dia"):** a IA atualiza o repositório, lê o checkpoint, e diz em 3 linhas: estado, pendência mais alta, próxima ação. E começa.
- **Durante:** atualiza o checkpoint a cada marco. Com o limite de uso da conta perto, **os checkpoints vêm primeiro**.
- **Fim ("finaliza"):** checkpoint do projeto e do QG, commit com mensagem clara, envio ao GitHub. Se o envio falhou, a sessão **continua aberta**.
- **Regra:** o que não está no checkpoint **não existe** para a próxima conversa.

## Trocando de conta ou de IA sem perder o fio
Como tudo está em arquivos no Git, qualquer conta ou IA que abra o QG lê o `CHECKPOINT.md` e continua do ponto. Antes de trocar, garanta que o checkpoint e o envio estão feitos.

## Não declare "concluído" só pelo checkpoint
Leia o BACKLOG. O checkpoint resume; o backlog é a fila real.
