# slesty-jobs (PUBLIC)

Actions-only harness that runs Slesty batch downloads on free public
runners. **This repository intentionally contains no code, no queue,
and never stores any output.**

## What lives where

| Repo | Visibility | Contents |
|---|---|---|
| `ryyr-ry/slesty-jobs` (this) | public | this workflow only |
| `ryyr-ry/slesty-worker` | private | worker binary, Rust packer, driver script, `jobs/queue/job.json` |
| `ryyr-ry/slesty-vault` | private | the download zips (Releases) + per-batch result logs (`logs/`) |
| `ryyr-ry/Slesty` | private | the downloader itself |

## Secrets (this repo)

| Secret | What it is |
|---|---|
| `SLESTY_RUNNER_TOKEN` | fine-grained PAT: Contents rw on slesty-worker + slesty-vault ONLY |
| `SLESTY_CREDS` | the registered device credentials JSON for slesty |

## Usage

1. The queue is curated in **slesty-worker** `jobs/queue/job.json`
   (what to download - full-catalog hand curation per artist).
2. Run this workflow (**Actions → batch → Run workflow**). Inputs:
   - `label` (**required**): human-readable release name, e.g.
     `Imagine Dragons - complete (81 tracks, 24bit UHD FLAC)`
   - `description`: shown on the release notes
   - `parallel`: slesty processes in flight (default 8; use 2 for
     large batches - throttling)
   - `max_minutes`: hard stop (default 180)
3. Fetch the zips from **slesty-vault** Releases - each `volN.zip` is
   a standalone valid zip that opens on a phone.
4. Audit the run without downloading anything: **slesty-vault**
   `logs/batch-N.log` lists every track as OK/SKIP/FAIL (+error).

The run log only ever shows counts: no artist names, no titles, no
ASINs. Downloads go straight to the private vault release; nothing is
ever uploaded here.
