# Guardrails: Forbidden Actions (STRICT)

- ❌ **NO DESTRUCTIVE COMMANDS**: Never execute `rm -rf /`, `git reset --hard`, or force pushes (`git push --force`) without explicit human confirmation.
- ❌ **NO ENV TAMPERING**: Never modify `.env` or configuration secrets files.
- ❌ **NO UNAPPROVED DEPENDENCIES**: Do not add major libraries or frameworks without prior approval.
