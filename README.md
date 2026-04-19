# Codex Skills - IOTA L1 (Move) - by Mosai-Sys

This repository stores Codex skills for Mosai-Sys workflows.

The first included skill is a security-first IOTA infrastructure and Move L1 skill for Codex:

```text
.agents/skills/iota-infrastructure-move-l1-security
```

## IOTA Infrastructure + Move L1 Security Skill

The IOTA skill helps Codex work safely with IOTA infrastructure and IOTA Move smart contracts on Layer 1.

It is intended for high-risk engineering tasks where code can affect real assets, including:

- IOTA Move L1 packages, modules, objects, capabilities, shared objects, dynamic fields, coins, NFTs, events, package upgrades, and Move tests.
- IOTA CLI operations across localnet, devnet, testnet, and mainnet.
- Package publish and upgrade workflows.
- Programmable Transaction Blocks.
- TypeScript SDK, Rust SDK, dApp Kit, GraphQL, JSON-RPC, wallet integration, and indexer usage.
- Security review, threat modeling, and deployment manifests.
- Source verification against official IOTA documentation and `github.com/iotaledger/iota`.
- Optional iotatools.dev On-Chain Apps integration through an isolated community-tooling adapter.

## Security model

The skill assumes that implementation mistakes can cause irreversible asset loss.

Core rules enforced by the skill:

- Use localnet or testnet by default.
- Do not perform state-changing mainnet actions without explicit current-task approval.
- Do not read, print, log, copy, or commit secrets, mnemonics, private keys, wallet exports, keystore contents, bearer tokens, or cloud credentials.
- Verify CLI version, active environment, RPC URL, chain identifier, active address, package IDs, object IDs, gas budget, and expected object changes before transaction work.
- Enforce value protection in Move, not in the frontend.
- Treat Sui documentation and examples as conceptual only unless verified against IOTA.
- Treat community tooling as untrusted until the exact branch, commit, package IDs, object IDs, and runtime behavior are verified.

## Installation

This repository is already laid out for repository-local Codex skills:

```text
.agents/skills/iota-infrastructure-move-l1-security/
```

To use the skill from another repository, copy the skill directory:

```bash
mkdir -p /path/to/target-repo/.agents/skills
cp -R .agents/skills/iota-infrastructure-move-l1-security /path/to/target-repo/.agents/skills/
```

To install it globally for the current user:

```bash
mkdir -p "$HOME/.agents/skills"
cp -R .agents/skills/iota-infrastructure-move-l1-security "$HOME/.agents/skills/"
```

## Invocation

Use this in Codex:

```text
$iota-infrastructure-move-l1-security
```

Example:

```text
Use the $iota-infrastructure-move-l1-security skill.

Review the Move package in ./move/escrow for capability safety, shared object invariants, package upgrade risk, and unauthorized public entry points. Do not perform any state-changing operation. Run build and tests if available. Findings first.
```

## Skill structure

```text
.agents/skills/iota-infrastructure-move-l1-security/
  SKILL.md
  README.md
  agents/
    openai.yaml
  references/
    codex_operating_model.md
    iota_authoritative_sources.md
    iota_cli_sdk_graphql.md
    iota_github_verification.md
    iota_move_l1_security.md
    iotatools_onchain_apps_adapter.md
    revision_decision_record.md
    security_checklist.md
  examples/
    codex_prompt.template.md
    deployment_manifest.template.yaml
    move_audit_report.template.md
  scripts/
    check_no_secret_patterns.sh
    collect_iota_context.sh
    run_iota_move_checks.sh
```

## Why the skill is structured this way

Version 4 uses one focused `SKILL.md` plus task-specific reference files. This structure was selected over a minimal patch and over multiple separate skills because it gives Codex a short activation surface while preserving detailed safety guidance for the exact task being performed.

See:

```text
.agents/skills/iota-infrastructure-move-l1-security/references/revision_decision_record.md
```

## Helper scripts

Collect non-secret IOTA context:

```bash
bash .agents/skills/iota-infrastructure-move-l1-security/scripts/collect_iota_context.sh
```

Run IOTA Move build and tests for a package:

```bash
bash .agents/skills/iota-infrastructure-move-l1-security/scripts/run_iota_move_checks.sh ./path/to/move/package
```

Scan for common secret-pattern mistakes without printing matching secret lines:

```bash
bash .agents/skills/iota-infrastructure-move-l1-security/scripts/check_no_secret_patterns.sh .
```

## Maintenance

When updating this repository:

1. Keep all skill content in English.
2. Keep `SKILL.md` concise and directive.
3. Put detailed operational guidance in `references/`.
4. Keep helper scripts deterministic and non-secret-reading.
5. Re-check official IOTA documentation and `github.com/iotaledger/iota` before changing IOTA facts.
6. Re-check official OpenAI Codex skill guidance before changing skill architecture.
7. Run shell syntax checks before committing script changes:

```bash
bash -n .agents/skills/iota-infrastructure-move-l1-security/scripts/*.sh
```

## Official sources to re-check

- IOTA developer docs: `https://docs.iota.org/developer/getting-started`
- IOTA CLI docs: `https://docs.iota.org/developer/references/cli`
- IOTA network overview: `https://docs.iota.org/developer/network-overview`
- IOTA package upgrades: `https://docs.iota.org/developer/iota-101/move-overview/package-upgrades`
- IOTA source repository: `https://github.com/iotaledger/iota`
- Codex skills docs: `https://developers.openai.com/codex/skills`
- Codex prompting guide: `https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide`

## Limitations

This repository does not provide a formal security audit guarantee. The skill improves Codex behavior, but it does not replace expert review, formal verification, staged deployment, multisig operations, monitoring, or incident response planning.
