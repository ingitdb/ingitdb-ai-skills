---
name: ingitdb-record
description: Create, read, update, and delete records in an inGitDB collection. Use for SQL-style INSERT, SELECT, UPDATE, and DELETE against `map[string]any` collections, locally or against a remote Git repo.
---

# inGitDB record CRUD

Wraps the four record-level commands in the `ingitdb` CLI: `insert`, `select`, `update`, `delete`. All four target `map[string]any` collections (i.e., collections whose `record_file.type` is `map[string]any`).

## Pre-flight check

```bash
command -v ingitdb >/dev/null 2>&1
```

On miss, invoke the `ingitdb-install` skill and stop until `ingitdb version` succeeds.

## ID format

Record IDs follow `<collection-id>/<record-key>`. Collection IDs allow alphanumeric and `.`; `/` separates the collection from the record key.

Example: `geo.nations/ie` → collection `geo.nations`, record key `ie`.

**Encoded keys.** A collection whose definition sets `record_file.key_encoding: tilde-v1` stores each key under an encoded file name: `a/b` is the file `a~2Fb.yaml`, `CON` is `~43ON.yaml`, `..` is `~2E~2E.yaml`. Always use, and show the user, the real key (`a/b`), never the file name; the tools encode and decode it. One exception: in a `select --from` subcollection path, a parent of such a collection is written as its file name (`--from=spaces/a~2Fb/notes` for the parent `a/b`; `--from=spaces/~43ON/notes` for `CON`), and the real key there is an error. Writes fail for a key that differs from an existing one only in letter case (`Ab` beside `ab`), and for a key whose file name would exceed 255 bytes. Pass that error on as it is: its remedy is to keep the collection in one file.

## Local vs. remote

Every record command accepts `--path <dir>` (local clone) **or** `--remote <host/owner/repo[@ref]>` (no clone, via REST API). Public repos need no token for reads; writes always require one (via `GITHUB_TOKEN` env var or `--token` flag).

## Pick a verb

| You need to… | Read |
|---|---|
| Insert a new record | [references/insert.md](references/insert.md) |
| Select records (by ID or by `--where` filter) | [references/select.md](references/select.md) |
| Update fields of an existing record | [references/update.md](references/update.md) |
| Delete a record (by ID or by `--where` filter) | [references/delete.md](references/delete.md) |
