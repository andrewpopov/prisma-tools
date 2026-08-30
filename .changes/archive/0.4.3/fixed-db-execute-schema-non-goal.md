---
kind: fixed
summary: Document that db execute is excluded from schema auto-appending, matching migrate diff
---

README used to describe schema-arg auto-appending as covering "schema-aware
Prisma commands" and documented only `migrate diff` as an exception, but
`shouldAppendSchemaArg` also excluded `db execute` without saying so. The code
was right and stays unchanged: `db execute`'s datasource flags are not stable
across the Prisma versions this package might run under (Prisma 7 removed
`--schema`/`--url` from `db execute` in favor of `prisma.config.ts`), and this
package does not detect the installed Prisma version, so auto-appending
`--schema` there would work on some installs and break on others. README now
lists `db execute` alongside `migrate diff` as a documented non-goal.
