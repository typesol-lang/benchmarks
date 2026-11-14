# Changelog

Versions follow the organization's [versioning policy](https://github.com/typesol-lang/.github/blob/main/VERSIONING.md).
Results change with the compiler and the toolchain; each run records both in `results.json` (`toolchain`). This file
lists changes to the benchmarks themselves: programs, scenarios, methodology and tooling.

## Unreleased

- Measured with `@typesol/cli` 0.48.0: `results.json` and `results/0.48.0.json`. Every figure is the same as 0.47.0's
  (0.48.0 builds every program measured here to the same binary; the compiler version and the runtime header's hash
  recorded changed).
- Measured with `@typesol/cli` 0.47.0: `results.json` and `results/0.47.0.json`. Every figure is the same as 0.46.0's
  (0.47.0 builds every program to the same binary; only the compiler version recorded changed).
- Measured with `@typesol/cli` 0.46.0: `results.json` and `results/0.46.0.json`. Every figure is the same as 0.45.0's
  (0.46.0 builds every program to the same binary; only the compiler version recorded changed).
- Measured with `@typesol/cli` 0.45.0: `results.json` and `results/0.45.0.json`. Every figure is the same as 0.44.1's
  (the counter, vault and escrow programs and the official examples measured build to the same binaries; only the
  compiler version and the toolchain record changed).
- Measured with `@typesol/cli` 0.44.1: `results.json` and `results/0.44.1.json`. Every figure is the same as 0.44.0's
  (only the compiler version recorded changed).
- Measured with `@typesol/cli` 0.44.0: `results.json` and `results/0.44.0.json`. counter, vault and escrow are as
  with 0.43.0. Seven of the official examples move by at most 22 CU either way (helper parameters are passed by
  pointer now): account-data 2,165 → 2,153, create-account 4,056 → 4,074, favorites 6,536 → 6,514, transfer-tokens
  8,372 → 8,390, create-token 41,096 → 41,110, and three more by 1 to 3 CU.
- Measured with `@typesol/cli` 0.43.0: `results.json` and `results/0.43.0.json`. Every figure is the same as 0.42.0's
  except favorites (`set_favorites (create)` 6,555 → 6,536 CU, binary 23.5 → 23.4 KB).
- Measured with `@typesol/cli` 0.42.0: `results.json` and `results/0.42.0.json`. Every figure is the same as 0.41.0's
  (only the compiler and runtime versions recorded changed).
- Measured with `@typesol/cli` 0.41.0: `results.json` and `results/0.41.0.json`. Every figure is the same as 0.40.0's
  (only the compiler and runtime versions recorded changed).
- Measured with `@typesol/cli` 0.40.0: `results.json` and `results/0.40.0.json`. Every figure is the same as 0.39.0's
  (only the compiler and runtime versions recorded changed).
- Measured with `@typesol/cli` 0.39.0: `results.json` and `results/0.39.0.json`. Within a few compute units and
  0.1 KB of 0.38.0 on every program.
- Moved to github.com/typesol-lang (the compiler is cloned from typesol-lang/typesol); Dependabot no longer opens
  weekly pull requests.
- The program-examples ports are read from `showcase/program-examples/` of the TypeSOL sources when it exists
  (TypeSOL moved them there after 0.38.0), else from `test/ports/`; Token Metadata from `test/programs/` either way.
- Measured with `@typesol/cli` 0.38.0 (was 0.25.0): `results.json` and `results/0.38.0.json`, with the toolchain each
  build used. The TypeSOL program on mainnet is still the 0.25.0 build (`results/mainnet-escrow.json`).
- Mainnet: a second escrow run on 2026-10-29, after the TypeSOL program was upgraded in place to 0.25.0 (the others
  unchanged). `results/mainnet-escrow.json` holds every run; the one before the upgrade is also in
  `results/mainnet-escrow-2026-10-27.json`.

- The mainnet run's result moved to `results/mainnet-escrow.json`.
- The Anchor twins are found at `test/anchor-twins` in TypeSOL checkouts after 0.25.0, and at `bench/anchor` before.

- `results/<version>.json`: the results of every released compiler measured (0.24.0, 0.24.1, 0.25.0, 0.38.0 so far), written by
  `scripts/archive.ts` and checked in CI.
- Dependabot for the npm tooling and GitHub Actions (not `@typesol/cli` or the measured Rust crates).

## 0.2.0 — 2026-10-29

- Measured with `@typesol/cli` 0.25.0: the escrow port checks its mints' token program as Anchor's
  `mint::token_program` does (make_offer +23 CU, take_offer +9), and refusals return Anchor's error codes in 12 of the
  14 hostile calls.
- `official.ts` records the error each refused hostile call returned (`probeErrors`): Anchor and TypeSOL as
  `Custom(<code>)`, native and Pinocchio as the runtime's error.
- `toolchain.typesolBuild`: the clang, SBPF version and runtime header hash the TypeSOL programs were built with.
- CI fails when a run's numbers differ from the committed `results.json` (`scripts/compare.ts`), with the
  differences in the job summary.

## 0.1.1 — 2026-10-28

- Measured with `@typesol/cli` 0.24.1 (smaller TypeSOL programs, the same results; the other implementations are
  unchanged).

## 0.1.0 — 2026-10-28

First public version.

- `run.ts`: counter, vault and escrow in TypeSOL, Anchor, native Rust and Pinocchio, with identical final state
  required before any number is reported.
- `official.ts`: the official solana-developers/program-examples (de09019) in Anchor, native and Pinocchio, unmodified,
  next to TypeSOL ports of the Anchor versions.
- The TypeSOL side is pinned: the compiler from npm (`@typesol/cli`, exact version in `package.json`) and its programs
  from the TypeSOL repository at that version's tag (`scripts/setup.sh`); `TYPESOL_REPO` measures a checkout instead.
- `results.json` records the toolchain (TypeSOL, Anchor, Pinocchio and solana-program versions, cargo-build-sbf and
  platform-tools, Node).
- `mainnet-escrow.ts`: the official escrow on mainnet-beta (RPC and keys from the environment).
