# Threat Model Report

## Executive Summary

| Field | Value |
|-------|-------|
| Repository | `mlieberman85/darnit-gittuf-demo` |
| Scan date | 2026-05-21 08:06:22 |
| Languages | go, yaml |
| Total findings | 88 |
| Critical | 0 |
| High | 0 |
| Medium | 88 |
| Low | 0 |

## Top Risks

_After reviewer triage on 2026-05-21, the 88 generator findings under the class "Unauthenticated cli command (cobra)" were collapsed into a single explanatory entry — see [CLI authentication scope](#cli-authentication-scope-reviewed) below. No critical or high-severity risks remain after triage._

## Unmitigated Findings

_None after triage. See [CLI authentication scope](#cli-authentication-scope-reviewed) for context on why the 88 generator findings were dismissed as not applicable._

## CLI authentication scope (reviewed)

The discovery pipeline emitted 88 MEDIUM findings of the same class — "Unauthenticated cli command (cobra)" — one per Cobra subcommand (`internal/cmd/**`, plus `docs/cli/main.go` and `docs/sandbox/main.go`). The heuristic flags any Cobra entry point that lacks an authentication step.

**Reviewer judgement: not applicable to this project's architecture.** gittuf is a local CLI; subcommands execute under the invoking user's OS account. There is no network listener, no API surface, and no remote caller — so there is no authentication boundary for these entry points to cross. The trust model is anchored in artefacts the CLI *produces* (signed RSL/policy metadata, signatures, attestations), not in authenticating the *invocation* of the CLI itself. Privilege at the process boundary is delegated to the operating system's user account, file permissions, and the surrounding shell environment.

Any actual trust-sensitive operation (signing policy, modifying root of trust, recording RSL entries) requires possession of the relevant signing key — that is the real access-control mechanism, and it lives in cryptographic key management, not in subcommand-level auth.

The per-finding detail files (`findings/go-entry-cobra_command_literal.md`, `findings/go-entry-cobra_new_func.md`) have been removed as part of this triage.

## Entry Points

### CLI Entry Points

#### Family: trust

**Source root**: `internal/cmd/trust/`
**Subcommands**: 31 (trust, set-repository-location, add-network-repository, init, remove-hook, enable-github-app-approvals, update-policy-threshold, make-controller, remove-policy-key, list-propagation-directives, add-policy-key, increment-version, add-root-key, remove-root-key, remove-global-rule, remove-propagation-directive, update-root-threshold, update-global-rule, inspect-root, add-github-app, update-hook, add-controller-repository, add-hook, remove-github-app, list-global-rules, add-global-rule, list-hooks, sign, disable-github-app-approvals, add-propagation-directive, update-propagation-directive)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| trust | `internal/cmd/trust/trust.go:46` | Tools for gittuf's root of trust |
| set-repository-location | `internal/cmd/trust/setrepositorylocation/setrepositorylocation.go:48` | Set repository location |
| add-network-repository | `internal/cmd/trust/addnetworkrepository/addnetworkrepository.go:77` |  |
| init | `internal/cmd/trust/init/init.go:47` | Initialize gittuf root of trust for repository |
| remove-hook | `internal/cmd/trust/removehook/removehook.go:84` |  |
| enable-github-app-approvals | `internal/cmd/trust/enablegithubappapprovals/enablegithubappapprovals.go:48` | Mark GitHub app approvals as trusted henceforth |
| update-policy-threshold | `internal/cmd/trust/updatepolicythreshold/updatepolicythreshold.go:48` | Update Policy threshold in the gittuf root of trust |
| make-controller | `internal/cmd/trust/makecontroller/makecontroller.go:40` |  |
| remove-policy-key | `internal/cmd/trust/removepolicykey/removepolicykey.go:50` | Remove Policy key from gittuf root of trust |
| list-propagation-directives | `internal/cmd/trust/listpropagationdirectives/listpropagationdirectives.go:52` | Lists propagation directives in the gittuf root of trust |
| add-policy-key | `internal/cmd/trust/addpolicykey/addpolicykey.go:53` | Add Policy key to gittuf root of trust |
| increment-version | `internal/cmd/trust/incrementversion/incrementversion.go:37` | Increment the integer version of the root metadata |
| add-root-key | `internal/cmd/trust/addrootkey/addrootkey.go:53` | Add Root key to gittuf root of trust |
| remove-root-key | `internal/cmd/trust/removerootkey/removerootkey.go:50` | Remove Root key from gittuf root of trust |
| remove-global-rule | `internal/cmd/trust/removeglobalrule/removeglobalrule.go:49` |  |
| remove-propagation-directive | `internal/cmd/trust/removepropagationdirective/removepropagationdirective.go:48` |  |
| update-root-threshold | `internal/cmd/trust/updaterootthreshold/updaterootthreshold.go:48` | Update Root threshold in the gittuf root of trust |
| update-global-rule | `internal/cmd/trust/updateglobalrule/updateglobalrule.go:94` |  |
| inspect-root | `internal/cmd/trust/inspectroot/inspectroot.go:47` | Inspect root metadata |
| add-github-app | `internal/cmd/trust/addgithubapp/addgithubapp.go:64` | Add GitHub app to gittuf root of trust |
| update-hook | `internal/cmd/trust/updatehook/updatehook.go:141` |  |
| add-controller-repository | `internal/cmd/trust/addcontrollerrepository/addcontrollerrepository.go:77` |  |
| add-hook | `internal/cmd/trust/addhook/addhook.go:141` |  |
| remove-github-app | `internal/cmd/trust/removegithubapp/removegithubapp.go:48` | Remove GitHub app from gittuf root of trust |
| list-global-rules | `internal/cmd/trust/listglobalrules/listglobalrules.go:73` | List global rules for the current state |
| add-global-rule | `internal/cmd/trust/addglobalrule/addglobalrule.go:96` |  |
| list-hooks | `internal/cmd/trust/listhooks/listhooks.go:69` | List gittuf hooks for the current policy state |
| sign | `internal/cmd/trust/sign/sign.go:39` | Sign root of trust |
| disable-github-app-approvals | `internal/cmd/trust/disablegithubappapprovals/disablegithubappapprovals.go:48` | Mark GitHub app approvals as untrusted henceforth |
| add-propagation-directive | `internal/cmd/trust/addpropagationdirective/addpropagationdirective.go:92` |  |
| update-propagation-directive | `internal/cmd/trust/updatepropagationdirective/updatepropagationdirective.go:94` |  |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: policy

**Source root**: `internal/cmd/policy/`
**Subcommands**: 15 (policy, init, remove-person, add-key, remove-key, add-person, remove-rule, increment-version, update-person, reorder-rules, list-principals, update-rule, add-rule, sign, list-rules)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| policy | `internal/cmd/policy/policy.go:31` | Tools to manage gittuf policies |
| init | `internal/cmd/policy/init/init.go:48` | Initialize policy file |
| remove-person | `internal/cmd/policy/removeperson/removeperson.go:57` | Remove a person from a policy file |
| add-key | `internal/cmd/policy/addkey/addkey.go:68` | Add a trusted key to a policy file |
| remove-key | `internal/cmd/policy/removekey/removekey.go:57` | Remove a key from a policy file |
| add-person | `internal/cmd/policy/addperson/addperson.go:122` | Add a trusted person to a policy file |
| remove-rule | `internal/cmd/policy/removerule/removerule.go:57` | Remove rule from a policy file |
| increment-version | `internal/cmd/policy/incrementversion/incrementversion.go:48` | Increment the integer version of the specified rule file metadata |
| update-person | `internal/cmd/policy/updateperson/updateperson.go:127` | Update a person in a policy file |
| reorder-rules | `internal/cmd/policy/reorderrules/reorderrules.go:51` | Reorder rules in the specified policy file |
| list-principals | `internal/cmd/policy/listprincipals/listprincipals.go:75` | List principals for the current policy in the specified rule file |
| update-rule | `internal/cmd/policy/updaterule/updaterule.go:103` | Update an existing rule in a policy file |
| add-rule | `internal/cmd/policy/addrule/addrule.go:103` | Add a new rule to a policy file |
| sign | `internal/cmd/policy/sign/sign.go:48` | Sign policy file |
| list-rules | `internal/cmd/policy/listrules/listrules.go:79` | List rules for the current state |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: rsl

**Source root**: `internal/cmd/rsl/`
**Subcommands**: 10 (rsl, propagate, record, annotate, skip-rewritten, log, remote, reconcile <remote>, pull <remote>, push <remote>)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| rsl | `internal/cmd/rsl/rsl.go:17` | Tools to manage the repository's reference state log |
| propagate | `internal/cmd/rsl/propagate/propagate.go:26` |  |
| record | `internal/cmd/rsl/record/record.go:74` | Record latest state of a Git reference (e.g., 'main') in the RSL |
| annotate | `internal/cmd/rsl/annotate/annotate.go:71` | Annotate prior RSL entries |
| skip-rewritten | `internal/cmd/rsl/skiprewritten/skiprewritten.go:26` | Creates an RSL annotation to skip RSL reference entries that point to commits that do not exist in the specified ref |
| log | `internal/cmd/rsl/log/log.go:38` | Display the repository's Reference State Log |
| remote | `internal/cmd/rsl/remote/remote.go:14` | Tools for managing remote RSLs |
| reconcile <remote> | `internal/cmd/rsl/remote/reconcile/reconcile.go:24` | Reconcile local RSL with remote RSL |
| pull <remote> | `internal/cmd/rsl/remote/pull/pull.go:25` | Pull RSL from the specified remote |
| push <remote> | `internal/cmd/rsl/remote/push/push.go:25` | Push RSL to the specified remote |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: attest

**Source root**: `internal/cmd/attest/`
**Subcommands**: 7 (attest, apply, github, pull-request, record-approval, dismiss-approval, authorize)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| attest | `internal/cmd/attest/attest.go:16` | Tools for attesting to code contributions |
| apply | `internal/cmd/attest/apply/apply.go:40` | Apply and push local attestations changes to remote repository |
| github | `internal/cmd/attest/github/github.go:15` | Tools to attest about GitHub actions and entities |
| pull-request | `internal/cmd/attest/github/pullrequest/pullrequest.go:99` | Record GitHub pull request information as an attestation |
| record-approval | `internal/cmd/attest/github/recordapproval/recordapproval.go:92` | Record GitHub pull request approval |
| dismiss-approval | `internal/cmd/attest/github/dismissapproval/dismissapproval.go:66` | Record dismissal of GitHub pull request approval |
| authorize | `internal/cmd/attest/authorize/authorize.go:69` | Add or revoke reference authorization |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: trustpolicy

**Source root**: `internal/cmd/trustpolicy/`
**Subcommands**: 6 (apply, discard, stage, remote, pull <remote>, push <remote>)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| apply | `internal/cmd/trustpolicy/apply/apply.go:40` | Validate and apply changes from policy-staging to policy |
| discard | `internal/cmd/trustpolicy/discard/discard.go:26` | Discard the currently staged changes to policy |
| stage | `internal/cmd/trustpolicy/stage/stage.go:40` | Stage and push local policy-staging changes to remote repository |
| remote | `internal/cmd/trustpolicy/remote/remote.go:13` | Tools for managing remote policies |
| pull <remote> | `internal/cmd/trustpolicy/remote/pull/pull.go:25` | Pull policy from the specified remote |
| push <remote> | `internal/cmd/trustpolicy/remote/push/push.go:25` | Push policy to the specified remote |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: dev

**Source root**: `internal/cmd/dev/`
**Subcommands**: 5 (dev, New(), New(), New(), rsl-record)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| dev | `internal/cmd/dev/dev.go:18` | Developer mode commands |
| New() | `internal/cmd/dev/dismissgithubapproval/dismissgithubapproval.go:27` |  |
| New() | `internal/cmd/dev/attestgithub/attestgithub.go:27` |  |
| New() | `internal/cmd/dev/addgithubapproval/addgithubapproval.go:27` |  |
| rsl-record | `internal/cmd/dev/rslrecordat/rslrecordat.go:65` |  |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: cache

**Source root**: `internal/cmd/cache/`
**Subcommands**: 3 (cache, init, delete)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| cache | `internal/cmd/cache/cache.go:13` | Manage gittuf's caching functionality |
| init | `internal/cmd/cache/init/init.go:26` | Initialize persistent cache |
| delete | `internal/cmd/cache/delete/delete.go:26` | Delete the local persistent cache |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: docs

**Source root**: `internal/cmd/docs/`
**Subcommands**: 2 (gendoc, gendoc)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| gendoc | `docs/cli/main.go:19` | Generate Markdown documentation for all commands in gittuf |
| gendoc | `docs/sandbox/main.go:22` | Generate sandbox docs |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: add-hooks

**Source root**: `internal/cmd/addhooks/`
**Subcommands**: 1 (add-hooks)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| add-hooks | `internal/cmd/addhooks/addhooks.go:49` | Add git hooks that automatically create and sync RSL |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: clone

**Source root**: `internal/cmd/clone/`
**Subcommands**: 1 (clone)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| clone | `internal/cmd/clone/clone.go:65` | Clone repository and its gittuf references |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: gittuf

**Source root**: `internal/cmd/root/`
**Subcommands**: 1 (gittuf)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| gittuf | `internal/cmd/root/root.go:104` | A security layer for Git repositories, powered by TUF |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: sync [remoteName]

**Source root**: `internal/cmd/sync/`
**Subcommands**: 1 (sync [remoteName])
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| sync [remoteName] | `internal/cmd/sync/sync.go:55` | Synchronize local references with remote references based on RSL |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: tui

**Source root**: `internal/cmd/tui/`
**Subcommands**: 1 (tui)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| tui | `internal/cmd/tui/tui.go:51` | Start the TUI for gittuf |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: verify-mergeable

**Source root**: `internal/cmd/verifymergeable/`
**Subcommands**: 1 (verify-mergeable)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| verify-mergeable | `internal/cmd/verifymergeable/verifymergeable.go:60` | Tools for verifying mergeability using gittuf policies |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: verify-network

**Source root**: `internal/cmd/verifynetwork/`
**Subcommands**: 1 (verify-network)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| verify-network | `internal/cmd/verifynetwork/verifynetwork.go:26` | Verify state of network repositories |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: verify-ref

**Source root**: `internal/cmd/verifyref/`
**Subcommands**: 1 (verify-ref)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| verify-ref | `internal/cmd/verifyref/verifyref.go:69` | Tools for verifying gittuf policies |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

#### Family: version

**Source root**: `internal/cmd/version/`
**Subcommands**: 1 (version)
**STRIDE categories**: Tampering
**Confidence**: heuristic — needs reviewer attention

| Subcommand | Location | Notes |
|---|---|---|
| version | `internal/cmd/version/version.go:34` | Version of gittuf |

_Refinement notes: This family was categorised by import-based heuristic; categories may need recategorisation per the project's threat model._

## Companion Artefacts

- [Data Flow Diagram](data-flow.md)
- [Raw Findings (JSON)](raw-findings.json)

## Recommendations Summary

### Immediate Actions (Critical / High)

No critical or high severity findings requiring immediate action.

### Short-term Actions (Medium)

1. **CLI subcommand authentication (88 findings, collapsed)** — Reviewer dismissed: this is a local CLI; subcommand entry points have no network/API authentication boundary. Trust is rooted in signed artefacts (RSL, policy metadata) and possession of signing keys, not in authenticating CLI invocations. See [CLI authentication scope](#cli-authentication-scope-reviewed).

## Verification Prompts

<!-- darnit:verification-prompt-block -->

**Triage status:** this summary was produced by the darnit tree-sitter discovery pipeline and has been triaged. On 2026-05-21 a reviewer collapsed the 88 generator findings ("Unauthenticated cli command (cobra)") into a single explanatory entry — see [CLI authentication scope](#cli-authentication-scope-reviewed) for the rationale. The per-finding detail files under `findings/` were removed as part of that triage.

The CLI Entry Points section's STRIDE categories were produced by an import-based heuristic and were not individually re-judged during this triage. If a future change adds a non-CLI entry point (e.g., a network listener), re-run the generator and re-triage.

<!-- /darnit:verification-prompt-block -->

## Limitations

- Scanned **286** in-scope files (go=267, yaml=19).
- Skipped **2** vendor/build directories and **141** files in unsupported languages.
- Opengrep taint analysis: not available.
  - Reason: opengrep/semgrep binary not installed on PATH
- Scanned **267** Go files; **91** imported `github.com/spf13/cobra`.
  - **3** cobra-importing file(s) matched no recognised pattern (builder-style or factory-returned-via-indirection construction); example: `internal/cmd/attest/persistent/persistent.go`. Surfaced commands may be incomplete.

- **68** additional candidate findings were trimmed to fit the finding cap.

*This is a threat-modeling aid, not an exhaustive vulnerability scan. Use Kusari Inspector or an equivalent SAST tool for deeper coverage.*

