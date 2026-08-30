---
kind: fixed
summary: Load the base .env file before mode resolution so it can select the mode/custom env file
---

`resolveContext` used to resolve `dev`/`prod` mode and pick the mode-specific
env file *before* loading the base `.env` file, so a mode key
(`PRISMA_TOOLS_ENV`/`PRISMA_ENV`) or `PRISMA_ENV_FILE` set only in `.env` was
silently ignored — the wrong mode-specific file could load instead of the one
`.env` asked for. `.env` is now loaded first, so it can select the mode and
the mode-specific/custom env file as documented. Precedence is unchanged
otherwise: an explicit `--prod`/`--dev` flag and any variable already present
in the real process environment still win over anything in `.env`, and the
mode-specific file still overrides the base file for ordinary variables.
