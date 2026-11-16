# Documentation index

Integration records for DOOM Kernel on miatoll, oldest first. The `evidence/` tree holds
the captured build and validation logs those documents refer to.

## Records

| File | Content |
|---|---|
| [`integration/01-audit.md`](integration/01-audit.md) | Phase 1 — miatoll / VoltageOS 6.2 integration audit and baseline |
| [`integration/02-implementation.md`](integration/02-implementation.md) | Phase 2 — feature integration record |
| [`integration/03-runtime.md`](integration/03-runtime.md) | Runtime validation checklist |
| [`integration/04-build-and-download.md`](integration/04-build-and-download.md) | Build and download instructions |
| [`integration/05-final-pretest.md`](integration/05-final-pretest.md) | Final pre-test integration (2026-10-31) |

## Evidence

| Directory | Build |
|---|---|
| `integration/evidence/` (top level) | Baseline: toolchain audit, config dump, artifact list |
| `integration/evidence/phase2-before-kcal-revert/` | Superseded KCal-enabled build |
| `integration/evidence/phase2-no-kcal/` | First KCal-free build |
| `integration/evidence/phase3-final-pretest/` | Final pre-test build, SHA256SUMS and installer verification |

## Local notes

`docs/reports/` is for working notes and is not tracked.
