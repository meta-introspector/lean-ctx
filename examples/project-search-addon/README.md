# project-search addon (example)

Declares the `project-search-mcp` stdio MCP server (from
[ipld-car-ipc-shmem-linux](https://github.com/meta-introspector/ipld-car-ipc-shmem-linux))
as a lean-ctx addon. It exposes host-wide tantivy search over indexed project
trees as four gateway tools:

- `psearch_search` — query + optional comma-separated project scope
- `psearch_status` — per-project docs/files/index-size/age table
- `psearch_update` — incremental index refresh (never wipes; no force path)
- `psearch_list_projects` — registry with `[indexed]` flags

## Prerequisites

Build and install the server binary first — lean-ctx never installs it for you:

    cargo build --release --bin project-search-mcp
    cp target/release/project-search-mcp ~/.local/bin/

The server keeps its index cache under `PROJECT_SEARCH_CACHE`
(default `/mnt/data1/dasl-cache/projects`).

## Install

    lean-ctx addon add examples/project-search-addon/lean-ctx-addon.toml

`add` prints the exact command line and asks before wiring the server into the
global gateway (flipping `gateway.enabled` on if it was off).
