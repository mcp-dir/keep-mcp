# Google Keep

### Google Keep para Claude, ChatGPT e agentes de IA

MCP do Google Keep, leia e edite suas notas, listas, labels e colaboradores. Conecta com email + master token do Google (não há API oficial; usamos a API privada do app Android via master token, como o gkeepapi). Suporta múltiplas contas Google. Servidor stateless rodando em Cloudflare Workers; credenciais ficam só na WCA da plataforma. Por padrão só gere notas marcadas com a label 'keep-mcp' (passe unsafe=true pra agir sobre qualquer nota).

- 📊 **24 ferramentas**
- ✏️ **Leitura e escrita**
- 💬 **Funciona com qualquer cliente MCP**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Login via magic-link (sem senha)**

[English version](README.en.md) · [Documentação completa](docs/) · [Skill pra agentes](skills/)

---

## Instalar em 1 clique

### Claude (Web e Desktop)

A Anthropic unificou a instalação de MCPs em `claude.ai/customize/connectors`. **O mesmo link serve pra Claude Web e Claude Desktop** (basta estar logado):

[➕ Abrir no Claude e conectar](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (se o deeplink não abrir): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Adicionar conector personalizado** → cole **Nome** `Google Keep` e **URL** `https://api.mcp.ai/p_keep`.

### Cursor

[➕ Instalar Google Keep no Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=keep&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9rZWVwIn0=)

### VS Code (Copilot Chat)

[➕ Instalar Google Keep no VS Code](vscode:mcp/install?name=keep&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_keep%22%7D)

### ChatGPT, Manus, OpenClaw e mais 40+ clientes

Funciona em qualquer cliente MCP que suporte **MCP over HTTP**. A URL do servidor é sempre:

```
https://api.mcp.ai/p_keep
```

Detalhes por cliente: [INSTALL.md](INSTALL.md).

---

## Exemplos de uso

```
Liste minhas notas do Google Keep
Crie uma nota no Keep: 'Comprar pão e leite'
Crie uma checklist de compras com ovos, café e arroz
```

---

## 24 ferramentas disponíveis

| Tool | Descrição |
|---|---|
| `keep_list_accounts` | Lista as contas Google Keep vinculadas a este install (id/email, label). |
| `keep_find` | Busca notas no Google Keep. Filtros opcionais: query (título/texto), labels, colors, pinned, archived, trashed (default false). |
| `keep_get_note` | Retorna uma nota (ou lista) do Google Keep pelo id. |
| `keep_create_note` | Cria uma nota de texto no Google Keep. |
| `keep_create_list` | Cria uma checklist no Google Keep. |
| `keep_update_note` | Atualiza título e/ou texto de uma nota. |
| `keep_pin_note` | Fixa ou desafixa uma nota (`pinned`, default true). |
| `keep_archive_note` | Arquiva ou desarquiva uma nota (`archived`, default true). |
| `keep_set_note_color` | Define a cor de uma nota. Uma de: DEFAULT, RED, ORANGE, YELLOW, GREEN, TEAL, BLUE, CERULEAN, PURPLE, PINK, BROWN, GRAY. Bulk support: accepts note_ids for batched execution. |
| `keep_trash_note` | Move uma nota pra lixeira. Bulk support: accepts note_ids for batched execution. |
| `keep_restore_note` | Restaura uma nota da lixeira. Bulk support: accepts note_ids for batched execution. |
| `keep_delete_note` | Apaga uma nota permanentemente (não dá pra desfazer). |
| `keep_add_list_item` | Adiciona um item a uma checklist. |
| `keep_update_list_item` | Atualiza texto e/ou estado (checked) de um item de checklist (por item_id). |
| `keep_delete_list_item` | Remove um item de checklist por item_id. |
| `keep_list_labels` | Lista todas as labels da conta. |
| `keep_create_label` | Cria uma nova label. |
| `keep_delete_label` | Apaga uma label pelo nome. |
| `keep_add_label_to_note` | Anexa uma label (por nome, criada se não existir) a uma nota. |
| `keep_remove_label_from_note` | Remove uma label (por nome) de uma nota. |
| `keep_list_note_collaborators` | Lista os colaboradores (emails) com quem a nota é compartilhada. |
| `keep_add_note_collaborator` | Compartilha uma nota com um colaborador (por email). |
| `keep_remove_note_collaborator` | Remove um colaborador (por email) de uma nota. |
| `keep_list_note_media` | Lista os blobs de mídia (imagens/áudio/desenhos) de uma nota, com links. |

Detalhe de cada tool: [docs/ferramentas.md](docs/ferramentas.md)

---

## Preços

Grátis.

---

## Privacidade & LGPD

- **Sub-processadores**: o LLM host que você escolher (Claude, ChatGPT, Cursor, agente próprio). Lista completa em [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Os dados retornados pelas tools são enviados ao **LLM host que você escolher**, sub-processador fora do nosso controle. Recomendamos planos com opt-out de treinamento.

---

## Perguntas frequentes

**O servidor é open source?**
O servidor é proprietário (hosted). Este repositório é o wrapper público com manifestos, docs e skills — tudo MIT.

**Posso usar com agente próprio (não Claude/Cursor)?**
Sim — qualquer cliente que suporte MCP over HTTP. URL: `https://api.mcp.ai/p_keep`.


---

## Suporte

- 📧 [keep@mcp.ai](mailto:keep@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/keep-mcp/issues)
- 📄 [docs/](docs/)

---

## Licença

MIT — veja [LICENSE](LICENSE). O servidor MCP em `api.mcp.ai/p_keep` é proprietário (hosted); este repositório (manifestos, docs, skills) é MIT.
