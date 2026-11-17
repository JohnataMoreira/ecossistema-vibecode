# 07 · Aprovação e deploy

## Os três portões (Gates)
| Gate | Quem | O que acontece |
|---|---|---|
| **Gate 1** | Orquestrador | Escreve a tarefa completa (contexto, arquivos, critérios, armadilhas, limite de tentativas). Sem Gate 1 não se começa. |
| **Gate 2** | Executor → Orquestrador | O executor entrega a **prova literal** (testes, git log, diff, CI). O orquestrador confere por amostragem na fonte, não confia no resumo. |
| **Gate 3** | Você | Você entende **sem contexto extra**? O checkpoint reflete hoje? A lição foi extraída? A próxima tarefa está definida? Só então aprova. |

## Do teste à produção
1. Executor integra na **staging** (ambiente de teste) quando CI e E2E de tela estiverem verdes.
2. O orquestrador confere o diff (se aparecer **deleção em massa** ou migration sumindo, é branch velho: recusar).
3. Auditoria cruzada se o risco for alto.
4. Se o usuário verá um fluxo novo, **você homologa** na staging (testa como usuário).
5. Deploy de produção, com **plano de volta** (rollback) anotado antes.
6. O orquestrador avisa o que mudou e como voltar atrás.

## Rollback (voltar atrás)
Antes de subir, anote: "se der errado, faço X". Em geral é reverter o último deploy na plataforma ou reverter o commit. Banco de dados é mais delicado: mudanças que só adicionam são fáceis de manter; as que apagam exigem backup e o seu "sim".

## Merge e limpeza
- Ao integrar, remova a worktree e o branch já integrado.
- Nunca integre automaticamente um conflito.
- Depois de qualquer envio, **olhe o CI**: envio que "passou" localmente pode falhar lá.

## Emergência
Sistema fora ou dado exposto: **contenha primeiro** (reverter, pausar, revogar chave) e avise você; investigue depois.
