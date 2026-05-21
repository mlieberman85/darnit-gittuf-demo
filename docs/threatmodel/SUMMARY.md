# Threat Model Report

## Executive Summary

| Field | Value |
|-------|-------|
| Repository | `mlieberman85/darnit-gittuf-demo` |
| Scan date | 2026-05-20 22:47:04 |
| Languages | go, yaml |
| Total findings | 88 |
| Critical | 0 |
| High | 0 |
| Medium | 88 |
| Low | 0 |

## Top Risks

| Class | STRIDE | Instances | Severity | Mitigation |
|-------|--------|-----------|----------|------------|
| [Unauthenticated cli command (cobra): verify-network](findings/go-entry-cobra_command_literal.md) | Spoofing | 85 | MEDIUM | 0/85 |
| [Unauthenticated cli command (cobra): New()](findings/go-entry-cobra_new_func.md) | Spoofing | 3 | MEDIUM | 0/3 |

## Unmitigated Findings

| Class | Instances | Max Severity | Detail |
|-------|-----------|--------------|--------|
| Unauthenticated cli command (cobra): verify-network | 85 | MEDIUM | [go-entry-cobra_command_literal.md](findings/go-entry-cobra_command_literal.md) |
| Unauthenticated cli command (cobra): New() | 3 | MEDIUM | [go-entry-cobra_new_func.md](findings/go-entry-cobra_new_func.md) |

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

1. **Unauthenticated cli command (cobra): verify-network** — `internal/cmd/verifynetwork/verifynetwork.go:26`
2. **Unauthenticated cli command (cobra): cache** — `internal/cmd/cache/cache.go:13`
3. **Unauthenticated cli command (cobra): init** — `internal/cmd/cache/init/init.go:26`
4. **Unauthenticated cli command (cobra): delete** — `internal/cmd/cache/delete/delete.go:26`
5. **Unauthenticated cli command (cobra): verify-mergeable** — `internal/cmd/verifymergeable/verifymergeable.go:60`
6. **Unauthenticated cli command (cobra): tui** — `internal/cmd/tui/tui.go:51`
7. **Unauthenticated cli command (cobra): attest** — `internal/cmd/attest/attest.go:16`
8. **Unauthenticated cli command (cobra): apply** — `internal/cmd/attest/apply/apply.go:40`
9. **Unauthenticated cli command (cobra): github** — `internal/cmd/attest/github/github.go:15`
10. **Unauthenticated cli command (cobra): pull-request** — `internal/cmd/attest/github/pullrequest/pullrequest.go:99`
11. **Unauthenticated cli command (cobra): record-approval** — `internal/cmd/attest/github/recordapproval/recordapproval.go:92`
12. **Unauthenticated cli command (cobra): dismiss-approval** — `internal/cmd/attest/github/dismissapproval/dismissapproval.go:66`
13. **Unauthenticated cli command (cobra): authorize** — `internal/cmd/attest/authorize/authorize.go:69`
14. **Unauthenticated cli command (cobra): clone** — `internal/cmd/clone/clone.go:65`
15. **Unauthenticated cli command (cobra): version** — `internal/cmd/version/version.go:34`
16. **Unauthenticated cli command (cobra): gittuf** — `internal/cmd/root/root.go:104`
17. **Unauthenticated cli command (cobra): dev** — `internal/cmd/dev/dev.go:18`
18. **Unauthenticated cli command (cobra): rsl-record** — `internal/cmd/dev/rslrecordat/rslrecordat.go:65`
19. **Unauthenticated cli command (cobra): verify-ref** — `internal/cmd/verifyref/verifyref.go:69`
20. **Unauthenticated cli command (cobra): trust** — `internal/cmd/trust/trust.go:46`
21. **Unauthenticated cli command (cobra): set-repository-location** — `internal/cmd/trust/setrepositorylocation/setrepositorylocation.go:48`
22. **Unauthenticated cli command (cobra): add-network-repository** — `internal/cmd/trust/addnetworkrepository/addnetworkrepository.go:77`
23. **Unauthenticated cli command (cobra): init** — `internal/cmd/trust/init/init.go:47`
24. **Unauthenticated cli command (cobra): remove-hook** — `internal/cmd/trust/removehook/removehook.go:84`
25. **Unauthenticated cli command (cobra): enable-github-app-approvals** — `internal/cmd/trust/enablegithubappapprovals/enablegithubappapprovals.go:48`
26. **Unauthenticated cli command (cobra): update-policy-threshold** — `internal/cmd/trust/updatepolicythreshold/updatepolicythreshold.go:48`
27. **Unauthenticated cli command (cobra): make-controller** — `internal/cmd/trust/makecontroller/makecontroller.go:40`
28. **Unauthenticated cli command (cobra): remove-policy-key** — `internal/cmd/trust/removepolicykey/removepolicykey.go:50`
29. **Unauthenticated cli command (cobra): list-propagation-directives** — `internal/cmd/trust/listpropagationdirectives/listpropagationdirectives.go:52`
30. **Unauthenticated cli command (cobra): add-policy-key** — `internal/cmd/trust/addpolicykey/addpolicykey.go:53`
31. **Unauthenticated cli command (cobra): increment-version** — `internal/cmd/trust/incrementversion/incrementversion.go:37`
32. **Unauthenticated cli command (cobra): add-root-key** — `internal/cmd/trust/addrootkey/addrootkey.go:53`
33. **Unauthenticated cli command (cobra): remove-root-key** — `internal/cmd/trust/removerootkey/removerootkey.go:50`
34. **Unauthenticated cli command (cobra): remove-global-rule** — `internal/cmd/trust/removeglobalrule/removeglobalrule.go:49`
35. **Unauthenticated cli command (cobra): remove-propagation-directive** — `internal/cmd/trust/removepropagationdirective/removepropagationdirective.go:48`
36. **Unauthenticated cli command (cobra): update-root-threshold** — `internal/cmd/trust/updaterootthreshold/updaterootthreshold.go:48`
37. **Unauthenticated cli command (cobra): update-global-rule** — `internal/cmd/trust/updateglobalrule/updateglobalrule.go:94`
38. **Unauthenticated cli command (cobra): inspect-root** — `internal/cmd/trust/inspectroot/inspectroot.go:47`
39. **Unauthenticated cli command (cobra): add-github-app** — `internal/cmd/trust/addgithubapp/addgithubapp.go:64`
40. **Unauthenticated cli command (cobra): update-hook** — `internal/cmd/trust/updatehook/updatehook.go:141`
41. **Unauthenticated cli command (cobra): add-controller-repository** — `internal/cmd/trust/addcontrollerrepository/addcontrollerrepository.go:77`
42. **Unauthenticated cli command (cobra): add-hook** — `internal/cmd/trust/addhook/addhook.go:141`
43. **Unauthenticated cli command (cobra): remove-github-app** — `internal/cmd/trust/removegithubapp/removegithubapp.go:48`
44. **Unauthenticated cli command (cobra): list-global-rules** — `internal/cmd/trust/listglobalrules/listglobalrules.go:73`
45. **Unauthenticated cli command (cobra): add-global-rule** — `internal/cmd/trust/addglobalrule/addglobalrule.go:96`
46. **Unauthenticated cli command (cobra): list-hooks** — `internal/cmd/trust/listhooks/listhooks.go:69`
47. **Unauthenticated cli command (cobra): sign** — `internal/cmd/trust/sign/sign.go:39`
48. **Unauthenticated cli command (cobra): disable-github-app-approvals** — `internal/cmd/trust/disablegithubappapprovals/disablegithubappapprovals.go:48`
49. **Unauthenticated cli command (cobra): add-propagation-directive** — `internal/cmd/trust/addpropagationdirective/addpropagationdirective.go:92`
50. **Unauthenticated cli command (cobra): update-propagation-directive** — `internal/cmd/trust/updatepropagationdirective/updatepropagationdirective.go:94`
51. **Unauthenticated cli command (cobra): apply** — `internal/cmd/trustpolicy/apply/apply.go:40`
52. **Unauthenticated cli command (cobra): discard** — `internal/cmd/trustpolicy/discard/discard.go:26`
53. **Unauthenticated cli command (cobra): stage** — `internal/cmd/trustpolicy/stage/stage.go:40`
54. **Unauthenticated cli command (cobra): remote** — `internal/cmd/trustpolicy/remote/remote.go:13`
55. **Unauthenticated cli command (cobra): pull <remote>** — `internal/cmd/trustpolicy/remote/pull/pull.go:25`
56. **Unauthenticated cli command (cobra): push <remote>** — `internal/cmd/trustpolicy/remote/push/push.go:25`
57. **Unauthenticated cli command (cobra): sync [remoteName]** — `internal/cmd/sync/sync.go:55`
58. **Unauthenticated cli command (cobra): rsl** — `internal/cmd/rsl/rsl.go:17`
59. **Unauthenticated cli command (cobra): propagate** — `internal/cmd/rsl/propagate/propagate.go:26`
60. **Unauthenticated cli command (cobra): record** — `internal/cmd/rsl/record/record.go:74`
61. **Unauthenticated cli command (cobra): annotate** — `internal/cmd/rsl/annotate/annotate.go:71`
62. **Unauthenticated cli command (cobra): skip-rewritten** — `internal/cmd/rsl/skiprewritten/skiprewritten.go:26`
63. **Unauthenticated cli command (cobra): log** — `internal/cmd/rsl/log/log.go:38`
64. **Unauthenticated cli command (cobra): remote** — `internal/cmd/rsl/remote/remote.go:14`
65. **Unauthenticated cli command (cobra): reconcile <remote>** — `internal/cmd/rsl/remote/reconcile/reconcile.go:24`
66. **Unauthenticated cli command (cobra): pull <remote>** — `internal/cmd/rsl/remote/pull/pull.go:25`
67. **Unauthenticated cli command (cobra): push <remote>** — `internal/cmd/rsl/remote/push/push.go:25`
68. **Unauthenticated cli command (cobra): add-hooks** — `internal/cmd/addhooks/addhooks.go:49`
69. **Unauthenticated cli command (cobra): policy** — `internal/cmd/policy/policy.go:31`
70. **Unauthenticated cli command (cobra): init** — `internal/cmd/policy/init/init.go:48`
71. **Unauthenticated cli command (cobra): remove-person** — `internal/cmd/policy/removeperson/removeperson.go:57`
72. **Unauthenticated cli command (cobra): add-key** — `internal/cmd/policy/addkey/addkey.go:68`
73. **Unauthenticated cli command (cobra): remove-key** — `internal/cmd/policy/removekey/removekey.go:57`
74. **Unauthenticated cli command (cobra): add-person** — `internal/cmd/policy/addperson/addperson.go:122`
75. **Unauthenticated cli command (cobra): remove-rule** — `internal/cmd/policy/removerule/removerule.go:57`
76. **Unauthenticated cli command (cobra): increment-version** — `internal/cmd/policy/incrementversion/incrementversion.go:48`
77. **Unauthenticated cli command (cobra): update-person** — `internal/cmd/policy/updateperson/updateperson.go:127`
78. **Unauthenticated cli command (cobra): reorder-rules** — `internal/cmd/policy/reorderrules/reorderrules.go:51`
79. **Unauthenticated cli command (cobra): list-principals** — `internal/cmd/policy/listprincipals/listprincipals.go:75`
80. **Unauthenticated cli command (cobra): update-rule** — `internal/cmd/policy/updaterule/updaterule.go:103`
81. **Unauthenticated cli command (cobra): add-rule** — `internal/cmd/policy/addrule/addrule.go:103`
82. **Unauthenticated cli command (cobra): sign** — `internal/cmd/policy/sign/sign.go:48`
83. **Unauthenticated cli command (cobra): list-rules** — `internal/cmd/policy/listrules/listrules.go:79`
84. **Unauthenticated cli command (cobra): gendoc** — `docs/cli/main.go:19`
85. **Unauthenticated cli command (cobra): gendoc** — `docs/sandbox/main.go:22`
86. **Unauthenticated cli command (cobra): New()** — `internal/cmd/dev/dismissgithubapproval/dismissgithubapproval.go:27`
87. **Unauthenticated cli command (cobra): New()** — `internal/cmd/dev/attestgithub/attestgithub.go:27`
88. **Unauthenticated cli command (cobra): New()** — `internal/cmd/dev/addgithubapproval/addgithubapproval.go:27`

## Verification Prompts

<!-- darnit:verification-prompt-block -->

**For the calling agent (Claude via MCP):** this summary was produced by the darnit tree-sitter discovery pipeline. Before committing, follow these steps:

1. Open each detail file under `findings/` and review the representative code snippets.
2. For each finding class, ask: does the code at these locations plausibly exhibit the described threat? If not, remove the detail file and its entry from this summary.
3. Refine narrative with project-specific details where helpful.
4. Preserve this `darnit:verification-prompt-block` section — it marks the draft as having gone through review.

**For the CLI Entry Points section:** this section was produced by an import-based heuristic, not a STRIDE analysis. Open each family's representative file. For each STRIDE category listed: does the file's actual behaviour match? If not, replace the category and remove this paragraph's note. If the family was over- or under-grouped (subcommands missing, or unrelated commands lumped together), restructure the table and edit the `family_key` identifier in `raw-findings.json` to match.

<!-- /darnit:verification-prompt-block -->

## Limitations

- Scanned **286** in-scope files (go=267, yaml=19).
- Skipped **2** vendor/build directories and **145** files in unsupported languages.
- Opengrep taint analysis: not available.
  - Reason: opengrep/semgrep binary not installed on PATH
- Scanned **267** Go files; **91** imported `github.com/spf13/cobra`.
  - **3** cobra-importing file(s) matched no recognised pattern (builder-style or factory-returned-via-indirection construction); example: `internal/cmd/attest/persistent/persistent.go`. Surfaced commands may be incomplete.

- **68** additional candidate findings were trimmed to fit the finding cap.

*This is a threat-modeling aid, not an exhaustive vulnerability scan. Use Kusari Inspector or an equivalent SAST tool for deeper coverage.*

