# CrossInk nightlies

Unofficial, untested firmware builds of [uxjulia/CrossInk](https://github.com/uxjulia/CrossInk), compiled once a day from the tip of its `development` branch.

**[Download a build from the Releases page](../../releases)**

Each release is one nightly. It lists one firmware file per supported board, so you can download any single build with one click:

| file | board |
| --- | --- |
| `firmware-x3-x4-nightly-<date>-<commit>.bin` | Xteink X3 and X4 |
| `firmware-sticky-nightly-<date>-<commit>.bin` | Seeed Sticky |
| `firmware-x4-pro-nightly-<date>-<commit>.bin` | Xteink X4 Pro |
| `firmware-x4-classic-nightly-<date>-<commit>.bin` | Xteink X4 Classic |

Flashing instructions are in the [CrossInk user guide](https://github.com/uxjulia/CrossInk/blob/development/docs/user-guide.md).

## What you are getting

- Built from upstream `development` exactly as it is, no local patches, in the same plain configuration upstream uses for its release candidates.
- Nobody has flashed these on any device before they are published. Expect rough edges, and keep a copy of a release you trust.
- The on-device version reads like a local development build (for example `1.6.1-dev+development`). The exact upstream commit is in the file name and in the release notes.
- The check runs daily at 06:23 UTC (02:23 US Eastern). A nightly is only published when `development` has moved since the previous one. Releases older than 30 days are removed automatically.
- If one board fails to build, the others are still published and the release notes say which file is missing.

This project is not affiliated with the CrossInk maintainers. Please report problems with a nightly here, not upstream, unless you can reproduce them on an official release or release candidate.

## How it works

[`.github/workflows/nightly.yml`](.github/workflows/nightly.yml) runs on a daily schedule and on demand. It resolves the current head of upstream `development`, compares it with the commit recorded in the latest nightly, and if they differ it checks out upstream at that commit, builds the four board environments with the same pinned toolchain as upstream's own CI, and publishes a pre-release with the firmware files and the list of upstream commits since the previous nightly.

Nothing is pushed to this repository by the workflow except release tags.
