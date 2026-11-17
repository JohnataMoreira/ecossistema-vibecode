# 10 · Stack para começar

Combinação que usamos hoje, com planos gratuitos para começar (limites mudam; confira nos sites):

| Peça | Para quê |
|---|---|
| **GitHub** | guarda o código, o histórico e roda a verificação automática (CI/Actions) |
| **Vercel** | coloca o site/app no ar (deploys automáticos, ambientes de teste) |
| **Supabase** | banco de dados, login de usuários, armazenamento de arquivos |
| **Resend** | envio de e-mails do seu sistema |
| **Cloudflare** | DNS, proteção, Workers (pequenos programas na borda) e redirecionadores |
| **Next.js / React** | o "motor" do site/app (a IA escreve; você não precisa dominar) |
| **Composio** | conecta tudo isso (e muito mais) às suas IAs |

## Cuidados que aprendemos
- **Cotas:** plataformas têm limite de minutos de build/execução. Commit de documentação não precisa disparar build (configure o projeto para ignorar). Ligue alertas de gasto e, se quiser travar o custo, o corte automático (cuidado: ele pode derrubar o site).
- **Ambientes:** crie sempre um de **teste** separado do de **produção**.
- **Segredos:** nas plataformas, em "Environment Variables"; nunca no código.
- **Banco:** ligue a segurança por linha (RLS) em toda tabela com dado de usuário e teste com usuário de verdade.
- **E-mail:** domínio "verificado" não prova que o e-mail chega; teste o envio de verdade.

## Ordem sugerida para o primeiro projeto
GitHub → projeto no Vercel ligado ao GitHub → projeto no Supabase (ambiente de teste) → e-mail com Resend → domínio próprio (quando for lançar; é decisão sua).
