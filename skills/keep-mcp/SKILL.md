---
name: keep-mcp
description: Skill da REST API do Google Keep na MCP.AI: 24 endpoints em /api/keep. MCP do Google Keep, leia e edite suas notas, listas, labels e colaboradores. Conecta com email + master token do Google (não há API oficial; usamos a API privada do app Android via master token, como o gkeepapi). Suporta múltiplas contas Google. Servidor stateless rodando em Cloudflare Workers; credenciais ficam só na WCA da plataforma. Por padrão só gere notas marcadas com a label 'keep-mcp' (passe unsafe=true pra agir sobre qualquer nota). Autentique com workspace API key (sk_live) gerada em app.mcp.ai/settings/api-keys. Use quando o usuário pedir algo coberto pelos endpoints.
---

# Google Keep — REST API skill

Você tem acesso à **Google Keep** REST API na MCP.AI.

> MCP do Google Keep, leia e edite suas notas, listas, labels e colaboradores. Conecta com email + master token do Google (não há API oficial; usamos a API privada do app Android via master token, como o gkeepapi). Suporta múltiplas contas Google. Servidor stateless rodando em Cloudflare Workers; credenciais ficam só na WCA da plataforma. Por padrão só gere notas marcadas com a label 'keep-mcp' (passe unsafe=true pra agir sobre qualquer nota).

## Base URL

```
https://api.mcp.ai/api/keep
```

Todo endpoint é um **POST** na Base URL + o path abaixo. Os parâmetros vão no corpo JSON.

## Autenticação

Inclua em toda request:

```
Authorization: Bearer sk_live_...
Content-Type: application/json
```

> Gere sua chave em **https://app.mcp.ai/settings/api-keys** (workspace API key `sk_live_…`, não expira, revogável). Uma única chave serve pra todos os seus MCPs.

## Formato de resposta

```json
{ "ok": true, "tool": "<tool_id>", "result": <payload> }
```

## Exemplo cURL

```bash
curl -X POST https://api.mcp.ai/api/keep/add/label/to/note \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{"note_id":"...","label":"..."}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/keep/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (24)

#### `keep_add_label_to_note`

Anexa uma label (por nome, criada se não existir) a uma nota. _(POST /api/keep/add/label/to/note)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `label` | string | Sim |  |
| `unsafe` | boolean | Não | Por padrão só notas com a label 'keep-mcp' podem ser editadas. unsafe=true libera qualquer nota. |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

#### `keep_add_list_item`

Adiciona um item a uma checklist. _(POST /api/keep/add/list/item)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `text` | string | Sim |  |
| `checked` | boolean | Não |  |
| `unsafe` | boolean | Não | Por padrão só notas com a label 'keep-mcp' podem ser editadas. unsafe=true libera qualquer nota. |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

#### `keep_add_note_collaborator`

Compartilha uma nota com um colaborador (por email). _(POST /api/keep/add/note/collaborator)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `email` | string | Sim |  |
| `unsafe` | boolean | Não | Por padrão só notas com a label 'keep-mcp' podem ser editadas. unsafe=true libera qualquer nota. |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

#### `keep_archive_note`

Arquiva ou desarquiva uma nota (`archived`, default true). _(POST /api/keep/archive/note)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `archived` | boolean | Não |  |
| `unsafe` | boolean | Não | Por padrão só notas com a label 'keep-mcp' podem ser editadas. unsafe=true libera qualquer nota. |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

#### `keep_create_label`

Cria uma nova label. _(POST /api/keep/create/label)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `name` | string | Sim |  |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |

#### `keep_create_list`

Cria uma checklist no Google Keep. _(POST /api/keep/create/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `title` | string | Não |  |
| `items` | object[] | Não |  |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |

#### `keep_create_note`

Cria uma nota de texto no Google Keep. _(POST /api/keep/create/note)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `title` | string | Não |  |
| `text` | string | Não |  |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |

#### `keep_delete_label`

Apaga uma label pelo nome. _(POST /api/keep/delete/label)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `name` | string | Sim |  |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |

#### `keep_delete_list_item`

Remove um item de checklist por item_id. _(POST /api/keep/delete/list/item)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `item_id` | string | Sim |  |
| `unsafe` | boolean | Não | Por padrão só notas com a label 'keep-mcp' podem ser editadas. unsafe=true libera qualquer nota. |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `item_ids` | string[] | Não | Bulk mode: multiple values for item_id |

#### `keep_delete_note`

Apaga uma nota permanentemente (não dá pra desfazer). _(POST /api/keep/delete/note)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `unsafe` | boolean | Não | Por padrão só notas com a label 'keep-mcp' podem ser editadas. unsafe=true libera qualquer nota. |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

#### `keep_find`

Busca notas no Google Keep. Filtros opcionais: query (título/texto), labels, colors, pinned, archived, trashed (default false). _(POST /api/keep/find)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `query` | string | Não |  |
| `labels` | string[] | Não |  |
| `colors` | string[] | Não |  |
| `pinned` | boolean | Não |  |
| `archived` | boolean | Não |  |
| `trashed` | boolean | Não |  |
| `limit` | integer | Não |  |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |

#### `keep_get_note`

Retorna uma nota (ou lista) do Google Keep pelo id. _(POST /api/keep/get/note)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

#### `keep_list_accounts`

Lista as contas Google Keep vinculadas a este install (id/email, label). _(POST /api/keep/list/accounts)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |

#### `keep_list_labels`

Lista todas as labels da conta. _(POST /api/keep/list/labels)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |

#### `keep_list_note_collaborators`

Lista os colaboradores (emails) com quem a nota é compartilhada. _(POST /api/keep/list/note/collaborators)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

#### `keep_list_note_media`

Lista os blobs de mídia (imagens/áudio/desenhos) de uma nota, com links. _(POST /api/keep/list/note/media)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

#### `keep_pin_note`

Fixa ou desafixa uma nota (`pinned`, default true). _(POST /api/keep/pin/note)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `pinned` | boolean | Não |  |
| `unsafe` | boolean | Não | Por padrão só notas com a label 'keep-mcp' podem ser editadas. unsafe=true libera qualquer nota. |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

#### `keep_remove_label_from_note`

Remove uma label (por nome) de uma nota. _(POST /api/keep/remove/label/from/note)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `label` | string | Sim |  |
| `unsafe` | boolean | Não | Por padrão só notas com a label 'keep-mcp' podem ser editadas. unsafe=true libera qualquer nota. |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

#### `keep_remove_note_collaborator`

Remove um colaborador (por email) de uma nota. _(POST /api/keep/remove/note/collaborator)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `email` | string | Sim |  |
| `unsafe` | boolean | Não | Por padrão só notas com a label 'keep-mcp' podem ser editadas. unsafe=true libera qualquer nota. |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

#### `keep_restore_note`

Restaura uma nota da lixeira. _(POST /api/keep/restore/note)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `unsafe` | boolean | Não | Por padrão só notas com a label 'keep-mcp' podem ser editadas. unsafe=true libera qualquer nota. |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

#### `keep_set_note_color`

Define a cor de uma nota. Uma de: DEFAULT, RED, ORANGE, YELLOW, GREEN, TEAL, BLUE, CERULEAN, PURPLE, PINK, BROWN, GRAY. _(POST /api/keep/set/note/color)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `color` | string | Sim |  (DEFAULT, RED, ORANGE, YELLOW, GREEN, TEAL, BLUE, CERULEAN, PURPLE, PINK, BROWN, GRAY) |
| `unsafe` | boolean | Não | Por padrão só notas com a label 'keep-mcp' podem ser editadas. unsafe=true libera qualquer nota. |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

#### `keep_trash_note`

Move uma nota pra lixeira. _(POST /api/keep/trash/note)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `unsafe` | boolean | Não | Por padrão só notas com a label 'keep-mcp' podem ser editadas. unsafe=true libera qualquer nota. |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

#### `keep_update_list_item`

Atualiza texto e/ou estado (checked) de um item de checklist (por item_id). _(POST /api/keep/update/list/item)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `item_id` | string | Sim |  |
| `text` | string | Não |  |
| `checked` | boolean | Não |  |
| `unsafe` | boolean | Não | Por padrão só notas com a label 'keep-mcp' podem ser editadas. unsafe=true libera qualquer nota. |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `item_ids` | string[] | Não | Bulk mode: multiple values for item_id |

#### `keep_update_note`

Atualiza título e/ou texto de uma nota. _(POST /api/keep/update/note)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `note_id` | string | Sim |  |
| `title` | string | Não |  |
| `text` | string | Não |  |
| `unsafe` | boolean | Não | Por padrão só notas com a label 'keep-mcp' podem ser editadas. unsafe=true libera qualquer nota. |
| `account` | string | Não | Quando múltiplas contas Google Keep estão vinculadas, passe o `email`. Omita se houver apenas uma. Use keep_list_accounts pra descobrir. |
| `note_ids` | string[] | Não | Bulk mode: multiple values for note_id |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_keep` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
