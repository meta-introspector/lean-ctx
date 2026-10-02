# shmem addon (example)

Declares the `shmem-mcp` stdio MCP server (from
[ipld-car-ipc-shmem-linux](https://github.com/meta-introspector/ipld-car-ipc-shmem-linux))
as a lean-ctx addon: a **read-only** window onto the CAR-page shared-memory
ring buffer via its Unix socket (`IPLD_CAR_SOCKET_NAME`, default
`@ipld_car_shmem`). Gateway tools:

- `shmem_stats` — slots/used/CIDs/blocks/compaction state
- `shmem_car_search`, `shmem_car_list` — CAR page metadata
- `shmem_blocks_query` — path-prefix query with server-side pagination
- `shmem_blocks_search` — full-text block search (descriptions, optional paths)

Put/rm/compact/shutdown/warm are intentionally **not** exposed.

## Prerequisites

    cargo build --release --bin shmem-mcp
    cp target/release/shmem-mcp ~/.local/bin/
    # and the ipld-car-ipc-shmem-linux server must be running

## Install

    lean-ctx addon add examples/shmem-addon/lean-ctx-addon.toml
