# slesty-jobs (PUBLIC)

Actions-only harness that runs Slesty batch downloads on free public
runners. **This repository intentionally contains no code, no queue,
and never stores any output.**

## What lives where

| Repo | Visibility | Contents |
|---|---|---|
| `ryyr-ry/slesty-jobs` (this) | public | this workflow only |
| `ryyr-ry/slesty-worker` | private | worker binary, driver script, `jobs/queue/job.json` |
| `ryyr-ry/slesty-vault` | private | the download zips (Releases) |
| `ryyr-ry/Slesty` | private | the downloader itself |

## Secrets (this repo)

| Secret | What it is |
|---|---|
| `SLESTY_RUNNER_TOKEN` | fine-grained PAT: Contents rw on slesty-worker + slesty-vault only |
| `SLESTY_CREDS` | the registered device credentials JSON for slesty |

## Usage

1. Edit `jobs/queue/job.json` in **slesty-worker** (what to download).
2. Run this workflow (Actions -> batch -> Run workflow).
3. Fetch the zips from **slesty-vault** Releases (`batch-<run>`).

The run log only ever shows counts: no artist names, no titles, no
ASINs.
