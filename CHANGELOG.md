# Changelog

All notable changes to the public skill package. Internal pl-cmp forks (`jakes-pr-review`, parity `/design-review`) may carry extra policy; port generic improvements here.

## [1.0.1] - 2026-11-15

### Fixed

- README badges: use shields.io until `www.skills.sh/b/...` install counter indexes for new repos

## [1.0.0] - 2026-03-21

### Added

- `bar-raiser-pr-review` — review, test-backed fix loop, full-diff re-review, merge gate
- `pr-round-reviewer` — read-only bar-raiser round + G-1–G-7 checklist
- `design-review` — dual-lens design doc orchestration
- `design-round-reviewer` — product or implementation read-only pass
- `test-first` — behavior-driven test-first protocol

### Notes

- Extracted and generalized from production agent workflows (Amazon-style PR loop, independent reviewer isolation).