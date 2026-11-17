# Composio — a tomada universal

## O que é
Um serviço onde você **conecta cada app uma vez** (GitHub, Gmail, Google Drive, Instagram, Facebook, Threads, LinkedIn, Reddit, Stripe, Cloudflare, Supabase, Google Analytics, Canva...) e **todas as suas IAs** passam a usar essas conexões. Em vez de configurar chave por chave em cada ferramenta, você tem **um caminho só**.

**Por que importa para você:** menos configuração, menos chaves espalhadas (menos risco de vazar), e qualquer IA do seu time consegue agir nos seus apps com a sua autorização.

## Três formas de usar (a IA escolhe a melhor para o seu caso)
1. **CLI no computador** (a mais simples para IAs com terminal): comando `composio`.
2. **MCP:** para IAs que aceitam conectores MCP, adicione o Composio Connect: `https://connect.composio.dev/mcp`. (É um endereço de protocolo para clientes MCP: abrir no navegador devolve erro 401, e isso é esperado.)
3. **Plugin** para Claude Code e Codex (a própria CLI instala).

## Instalação (a IA faz; você aprova e autoriza no navegador)
```bash
# Mac/Linux. No Windows, siga o método indicado em docs.composio.dev.
# instalador oficial da Composio (leia a documentação antes de aprovar)
curl -fsSL https://composio.dev/install | sh
composio login          # abre o navegador para você entrar
composio whoami         # confere a conta (não mostra chaves)
composio link github    # conecta o GitHub (abre o navegador para autorizar)
composio search "publicar post no instagram"   # a IA acha a ferramenta certa
composio execute <ferramenta> ...              # roda a ferramenta
```
Cada `link` abre uma tela do próprio app pedindo a **sua autorização**. Você sempre pode revogar depois.

## Regras do ecossistema para o Composio
1. **Chave de API do Composio nunca vai ao chat, a commit ou a documento.** Fica só no campo do conector ou em arquivo local protegido.
2. **Toda chamada informa a conta usada** quando há mais de uma (por exemplo, duas contas de Instagram).
3. **Conexões são suas:** só você remove ou renomeia.
4. **Cobranças:** alguns conectores de raspagem/serviços de terceiros podem cobrar créditos. Só use com ordem sua.
5. **Cada IA só usa o que o papel dela exige.** Quem pesquisa não precisa de acesso ao seu banco de produção. Se puder, separe contas/organizações por finalidade.
6. **Limites de cada app valem por cima:** leitura de banco de produção só leitura; pagamento só em modo de teste até você liberar; DNS só leitura.

## Quais conectores ligar primeiro
| Se você quer... | Conecte |
|---|---|
| Guardar e publicar código | GitHub |
| Ler/enviar e-mail | Gmail |
| Guardar arquivos e filas de posts | Google Drive / Docs |
| Publicar nas redes | Instagram, Facebook (Página), Threads, LinkedIn, Reddit |
| Ler métricas de site | Google Analytics, Search Console |
| Banco, deploy, domínio | Supabase, Vercel, Cloudflare |
| Pagamentos | Stripe (comece em modo de teste) |

## Limites do plano gratuito
Há limite de chamadas por período. Sistemas que chamam muito (como o [Marquinhos](../MARQUINHOS/README.md)) devem **poupar chamadas** (ver como lá).
