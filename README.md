# pi-memory

Lean, local, SQLite-backed memory for [pi](https://pi.dev).

## What it does

- Stores concise user or project memories in `~/.pi/agent/memory/memory.sqlite`.
- Provides explicit save, search, list, update, and delete tools.
- Provides `/remember`, `/memories`, and `/forget` commands.
- Uses simple local ranking based on term overlap, tags, importance, recency, and confirmed use.
- Supports opt-in bounded automatic recall with `/memory-recall on`.
- Uses Node's built-in `node:sqlite`; no database server, vector database, or embedding service is required.

## Install

```text
pi install git:github.com/jephal/pi-memory@v0.0.1
```

Then reload Pi:

```text
/reload
```

## Usage

Explicitly save a memory:

```text
/remember I prefer TypeScript for new Pi extensions.
```

Search memories:

```text
/memories TypeScript Pi extensions
```

Delete a memory:

```text
/forget mem_1234567890abcdef
```

Automatic recall is disabled by default. Enable bounded user-memory recall with:

```text
/memory-recall on
```

Disable it again with:

```text
/memory-recall off
```

## Scopes and privacy

The `memory_save` tool accepts `user` and `project` scopes. `/remember` always creates a user-scoped memory. Project memories are not automatically recalled by the first version.

Memory writes are explicit. Do not save credentials, tokens, private keys, raw authentication files, or unrestricted transcripts. The database is local and should be treated as private user data.

## Design

The first version intentionally does not include FTS5, embeddings, a vector database, automatic conversation extraction, or a background service. The database adapter keeps those possibilities open for later without making them requirements.
