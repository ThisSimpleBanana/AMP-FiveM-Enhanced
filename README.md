# FiveM for GTA V Enhanced - AMP template (experimental)

Linux-only community AMP template based on [CubeCoders AMPTemplates](https://github.com/CubeCoders/AMPTemplates). It is not an official AMP or Cfx.re release.

## Add to AMP
In ADS > Configuration > Instance Deployment > Configuration Repositories, add `ThisSimpleBanana/AMP-FiveM-Enhanced:main` and fetch the repository. Create a **new** instance using **FiveM - GTA V Enhanced (Manual Install)**.

## Manual server installation
This template intentionally has **no update stages**. The legacy FiveM update process must not overwrite Enhanced binaries. Stop the instance, download the official **Enhanced / Linux** archive at https://docs.fivem.net/docs/server-download/?platform=enhanced&os=linux and extract it to the new instance's `fivem/server-enhanced/` directory (so `fivem/server-enhanced/run.sh` and `fivem/server-enhanced/alpine/` exist). Set file ownership to the AMP user and ensure executable permissions on the musl loader and any required files. Never place license keys or secrets in this repository.

AMP is configured to launch `cfx-server` with txAdmin v9 on TCP port 40121. Game traffic defaults to TCP/UDP 30121; actual game port must also be configured in txAdmin/server.cfg. These defaults **cannot be shared** with another server listening on the same IP.

## Important limitations
- This is **experimental and not yet end-to-end tested in AMP**. In particular confirm that AMP passes `TXHOST_TXA_PORT` to the child process; if not, adapt instance-level startup/environment configuration.
- txAdmin v9 manages the initial game configuration; no server.cfg is passed on the first start.
- Docker's default seccomp policy may block `io_uring` syscalls used by Enhanced. Prefer a separate container / narrowly scoped profile, and avoid exposing txAdmin publicly.
- Do not deploy into an existing legacy FiveM instance or run its legacy updater.
- The template deliberately uses empty AMP game configuration/meta mappings to avoid imposing obsolete FiveM Legacy configuration options.

The original AMP FiveM template is maintained at https://github.com/CubeCoders/AMPTemplates.
