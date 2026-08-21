# Google Keep

### Google Keep for Claude, ChatGPT and AI agents

Google Keep MCP, read and edit your notes, lists, labels and collaborators. Connect with your Google email + master token (there is no official API; we use the private Android-app API via a master token, like gkeepapi). Supports multiple Google accounts. Stateless server running on Cloudflare Workers; credentials live only in the platform WCA. By default it only manages notes tagged with the 'keep-mcp' label (pass unsafe=true to act on any note).

- 📊 **24 tools**
- ✏️ **Read and write**
- 💬 **Works with any MCP client**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Magic-link login (no password)**

[Portuguese version](README.md) · [Full docs (PT-BR)](docs/)

---

## One-click install

### Claude (Web and Desktop)

[➕ Open in Claude and connect](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

Manual: [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Add custom connector** → name `Google Keep`, URL `https://api.mcp.ai/p_keep`.

### Cursor

[➕ Install in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=keep&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9rZWVwIn0=)

### VS Code (Copilot Chat)

[➕ Install in VS Code](vscode:mcp/install?name=keep&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_keep%22%7D)

### Any other MCP-over-HTTP client

```
https://api.mcp.ai/p_keep
```

---

## 24 tools

| Tool | Description |
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

---

## Pricing

Free.

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_keep` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.
