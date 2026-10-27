# Snapshot provenance and recovery

## What is preserved

`Protected.lua` remains at the repository root, byte-for-byte unchanged. It is
73,044 bytes and contains a `Protected_by_MoonSecV2` marker. That marker does not
establish authorship, project behavior, or the toolchain used to produce it.
The artifact was neither executed nor deobfuscated during this cleanup.

| Evidence | Recorded value |
| --- | --- |
| Configured Git origin | `https://github.com/leofratu/mdhub.git` |
| Original commit | `7918f3fd3d8c9159f5ae1b85ebc5b9767e02ae06` |
| Commit date | `2024-09-16 19:36:06 +0200` |
| Commit subject | `Main Lua` |
| Original Git blob | `5952ea19bbd2b2cf16d466da4c79c64fba100bc4` |
| SHA-256 | `0bd222f899e96cc93769b23ab9ed2e6198f1d0826afdf0cbb71c7ec3e090c5e0` |

The original commit message describes the script as encrypted. The configured
origin and commit metadata are local evidence, not independent verification of
the artifact's upstream provenance. No README, readable source, tests, dependency
manifest, or license file existed in the inspected commit. No runtime or
application capabilities can be established from that inventory.

## Search performed on 2026-10-27

- Inspected all local Git refs, commit history, trees, and reflogs. The checkout
  was not shallow; its history contained only the original commit above.
- Ran `git fsck --full --no-reflogs --unreachable`; it succeeded with no output,
  finding no unreachable objects that could supply missing source.
- Searched names under `/Users/main/Desktop`, `/Users/main/Documents`, and
  `/Users/main/Downloads`, walking directories up to five levels below each
  root. Looked for names containing `mdhub` or exactly matching `Protected.lua`,
  case-insensitively. Excluded hidden directories and dependency/cache folders
  (`node_modules`, `.venv`, `venv`, `.next`, `.cache`, `vendor`, `Library`, `.git`).
  The only matches were this checkout and its existing artifact; no traversal
  errors were reported.

This was a bounded local search, not proof that the original source no longer
exists. Files with unrelated names, deeper folders, remote services, backups,
and other machines were outside its scope. No remote fetch or upstream audit
was performed. The snapshot is unrecoverable from the materials inspected here;
the original implementation remains unknown.

## Recover the project

1. Ask the repository owner for the original readable Lua source, its revision,
   and any inputs or configuration used to create this artifact. Check owner
   backups, editor history, and original development folders when available.
2. Record where the recovered files came from and how the owner associates them
   with this snapshot. Confirm the intended runtime, dependencies, entry point,
   usage, and license rather than inferring them from obfuscated strings.
3. Add verified source alongside `Protected.lua`, retaining the artifact at its
   current path. Update the README with evidence-backed setup instructions and
   appropriate checks once the recovered implementation can be inspected.

## Check snapshot integrity

From the repository root:

```sh
shasum -a 256 Protected.lua
git diff 7918f3fd3d8c9159f5ae1b85ebc5b9767e02ae06 -- Protected.lua
```

The hash should match the SHA-256 above, and the diff should be empty. These
checks establish preservation only; they do not validate runtime behavior.
