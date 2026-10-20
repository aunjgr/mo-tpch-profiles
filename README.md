# MatrixOne / DuckDB TPC-H profiles

Downloadable profiling evidence for [matrixorigin/matrixone#30569](https://github.com/matrixorigin/matrixone/issues/30569).

## Completed targeted diagnosis

[Download release](https://github.com/aunjgr/mo-tpch-profiles/releases/tag/diagnosis-20261020) · [Starter bundle](https://github.com/aunjgr/mo-tpch-profiles/releases/download/diagnosis-20261020/tpch-30569-diagnosis-starter.tar.zst) · [Checksums](https://github.com/aunjgr/mo-tpch-profiles/releases/download/diagnosis-20261020/SHA256SUMS.txt)

The starter bundle covers 88 accepted diagnostic arms, including the twelve primary SF100 CPU cells for Q1/Q6/Q9/Q15/Q18/Q21 on both engines. It contains interactive CPU SVGs, weighted stacks, PMU counters, native plans/EXPLAIN output, Go-server heap/allocation profiles, matched controls, source snapshots and provenance.

Extract with `tar --zstd -xf tpch-30569-diagnosis-starter.tar.zst`, then read README.md and profile-index.csv. Open cpu-leaves.svg files in a browser. Go profiles can be opened with `go tool pprof -http=127.0.0.1:9090 FILE.pb.gz`.

## Expanded comparison

The all-query matrix is running independently of PR merge state. Its downloadable native/CPU/wait/allocation evidence, raw perf captures and exact executable/symbol support bundle will be added after measurements and offline analysis finish, then linked from the tracking issue.

## Exact versions and metric boundaries

- Native MO source: `873282742714436bff407dfcdbbe879147162bd3`.
- DuckDB 1.5.6 source: `069cc9f9b5be802405797faecc284961b07c70ef`.
- Query-worker source: `f881dfc604c11c29067ec5ccfcabbeeb357f40bc`.
- 8 physical application cores; 32 GiB primary total application cap; no application swap; MO aggregation threshold 2 GiB. Source/build/configuration identities and per-arm resource settings accompany the profiles.

CPU leaf samples are user-mode; common application CPU includes user and system time. Parallel operator elapsed-time sums are not process CPU. Go heap profiles cover their named Go process, not complete C++ or custom allocator totals. Optimized C++ callgraphs may be partial. Controlled query/cache variants are labeled separately. Excluded/failed captures are not presented as accepted measurements.

Generated tables, database images, ordinary query result captures and verbose service logs are not distributed here. This is engineering TPC-H workload evidence, not an audited TPC-H score.
