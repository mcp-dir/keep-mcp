# Ferramentas

Google Keep expõe 24 ferramentas.

### 1. `keep_list_accounts`
**Input**: `account` (opcional)

Lista as contas Google Keep vinculadas a este install (id/email, label).

### 2. `keep_find`
**Input**: `query` (opcional), `labels` (opcional), `colors` (opcional), `pinned` (opcional), `archived` (opcional), `trashed` (opcional), `limit` (opcional), `account` (opcional)

Busca notas no Google Keep. Filtros opcionais: query (título/texto), labels, colors, pinned, archived, trashed (default false).

### 3. `keep_get_note`
**Input**: `note_id`, `account` (opcional), `note_ids` (opcional)

Retorna uma nota (ou lista) do Google Keep pelo id.

### 4. `keep_create_note`
**Input**: `title` (opcional), `text` (opcional), `account` (opcional)

Cria uma nota de texto no Google Keep.

### 5. `keep_create_list`
**Input**: `title` (opcional), `items` (opcional), `account` (opcional)

Cria uma checklist no Google Keep.

### 6. `keep_update_note`
**Input**: `note_id`, `title` (opcional), `text` (opcional), `unsafe` (opcional), `account` (opcional), `note_ids` (opcional)

Atualiza título e/ou texto de uma nota.

### 7. `keep_pin_note`
**Input**: `note_id`, `pinned` (opcional), `unsafe` (opcional), `account` (opcional), `note_ids` (opcional)

Fixa ou desafixa uma nota (`pinned`, default true).

### 8. `keep_archive_note`
**Input**: `note_id`, `archived` (opcional), `unsafe` (opcional), `account` (opcional), `note_ids` (opcional)

Arquiva ou desarquiva uma nota (`archived`, default true).

### 9. `keep_set_note_color`
**Input**: `note_id`, `color`, `unsafe` (opcional), `account` (opcional), `note_ids` (opcional)

Define a cor de uma nota. Uma de: DEFAULT, RED, ORANGE, YELLOW, GREEN, TEAL, BLUE, CERULEAN, PURPLE, PINK, BROWN, GRAY. Bulk support: accepts note_ids for batched execution.

### 10. `keep_trash_note`
**Input**: `note_id`, `unsafe` (opcional), `account` (opcional), `note_ids` (opcional)

Move uma nota pra lixeira. Bulk support: accepts note_ids for batched execution.

### 11. `keep_restore_note`
**Input**: `note_id`, `unsafe` (opcional), `account` (opcional), `note_ids` (opcional)

Restaura uma nota da lixeira. Bulk support: accepts note_ids for batched execution.

### 12. `keep_delete_note`
**Input**: `note_id`, `unsafe` (opcional), `account` (opcional), `note_ids` (opcional)

Apaga uma nota permanentemente (não dá pra desfazer).

### 13. `keep_add_list_item`
**Input**: `note_id`, `text`, `checked` (opcional), `unsafe` (opcional), `account` (opcional), `note_ids` (opcional)

Adiciona um item a uma checklist.

### 14. `keep_update_list_item`
**Input**: `item_id`, `text` (opcional), `checked` (opcional), `unsafe` (opcional), `account` (opcional), `item_ids` (opcional)

Atualiza texto e/ou estado (checked) de um item de checklist (por item_id).

### 15. `keep_delete_list_item`
**Input**: `item_id`, `unsafe` (opcional), `account` (opcional), `item_ids` (opcional)

Remove um item de checklist por item_id.

### 16. `keep_list_labels`
**Input**: `account` (opcional)

Lista todas as labels da conta.

### 17. `keep_create_label`
**Input**: `name`, `account` (opcional)

Cria uma nova label.

### 18. `keep_delete_label`
**Input**: `name`, `account` (opcional)

Apaga uma label pelo nome.

### 19. `keep_add_label_to_note`
**Input**: `note_id`, `label`, `unsafe` (opcional), `account` (opcional), `note_ids` (opcional)

Anexa uma label (por nome, criada se não existir) a uma nota.

### 20. `keep_remove_label_from_note`
**Input**: `note_id`, `label`, `unsafe` (opcional), `account` (opcional), `note_ids` (opcional)

Remove uma label (por nome) de uma nota.

### 21. `keep_list_note_collaborators`
**Input**: `note_id`, `account` (opcional), `note_ids` (opcional)

Lista os colaboradores (emails) com quem a nota é compartilhada.

### 22. `keep_add_note_collaborator`
**Input**: `note_id`, `email`, `unsafe` (opcional), `account` (opcional), `note_ids` (opcional)

Compartilha uma nota com um colaborador (por email).

### 23. `keep_remove_note_collaborator`
**Input**: `note_id`, `email`, `unsafe` (opcional), `account` (opcional), `note_ids` (opcional)

Remove um colaborador (por email) de uma nota.

### 24. `keep_list_note_media`
**Input**: `note_id`, `account` (opcional), `note_ids` (opcional)

Lista os blobs de mídia (imagens/áudio/desenhos) de uma nota, com links.

## Prompts de exemplo

```
Liste minhas notas do Google Keep
Crie uma nota no Keep: 'Comprar pão e leite'
Crie uma checklist de compras com ovos, café e arroz
```
