# AGENTS.md

## Repository purpose

This repository stores Codex skills for Mosai-Sys. Current primary skill:

```text
.agents/skills/iota-infrastructure-move-l1-security
```

## Maintenance rules

- Keep all skill content in English.
- Keep `SKILL.md` concise, directive, and suitable for progressive disclosure.
- Put detailed guidance in `references/` rather than expanding `SKILL.md` unnecessarily.
- Do not add secrets, private keys, wallet exports, keystore contents, bearer tokens, or real credentials.
- Treat IOTA facts as source-sensitive. Verify current official IOTA docs and `github.com/iotaledger/iota` before changing protocol, CLI, SDK, network, or Move-framework guidance.
- Treat Sui as conceptual only unless a point is verified for IOTA.
- Treat community tooling as non-authoritative for IOTA protocol behavior.
- Preserve the mainnet safety gate in all IOTA-related skill updates.

## Checks before committing

```bash
bash -n .agents/skills/iota-infrastructure-move-l1-security/scripts/*.sh
bash .agents/skills/iota-infrastructure-move-l1-security/scripts/check_no_secret_patterns.sh .
```

If the secret-pattern scan flags files, review them locally without printing secret values.

## Review expectations

For changes to the IOTA skill, report:

- Files changed.
- Official sources checked.
- Commands run.
- Tests or syntax checks passed/failed.
- Security impact.
- Residual risks.
