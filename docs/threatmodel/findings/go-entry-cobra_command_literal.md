# Unauthenticated cli command (cobra): verify-network

**STRIDE category:** Spoofing
**Rule ID:** `go.entry.cobra_command_literal`
**Max severity:** MEDIUM

## Mitigation

No specific guidance available.

*All 85 instances are unmitigated (no sidecar entries recorded).*

## Representative Examples

<details>
<summary><code>internal/cmd/verifynetwork/verifynetwork.go:26</code></summary>

```
      16 | 	repo, err := gittuf.LoadRepository(".")
      17 | 	if err != nil {
      18 | 		return err
      19 | 	}
      20 | 
      21 | 	return repo.VerifyNetwork(cmd.Context())
      22 | }
      23 | 
      24 | func New() *cobra.Command {
      25 | 	o := &options{}
>>>   26 | 	cmd := &cobra.Command{
      27 | 		Use:               "verify-network",
      28 | 		Short:             "Verify state of network repositories",
      29 | 		Long:              "The 'verify-network' command verifies the state of network repositories configured in the repository's root of trust. It is used to check the integrity and consistency of network repositories against the expected trust configuration.",
      30 | 		RunE:              o.Run,
      31 | 		DisableAutoGenTag: true,
      32 | 	}
      33 | 	o.AddFlags(cmd)
      34 | 
      35 | 	return cmd
      36 | }
```

*No authentication decorator was found on this endpoint. If the endpoint handles sensitive actions, it may be accessible to unauthenticated callers. Verify whether authentication is enforced at a different layer (middleware, reverse proxy, MCP client credential check).*

</details>

<details>
<summary><code>internal/cmd/cache/cache.go:13</code></summary>

```
       3 | 
       4 | package cache
       5 | 
       6 | import (
       7 | 	"github.com/gittuf/gittuf/internal/cmd/cache/delete"
       8 | 	i "github.com/gittuf/gittuf/internal/cmd/cache/init"
       9 | 	"github.com/spf13/cobra"
      10 | )
      11 | 
      12 | func New() *cobra.Command {
>>>   13 | 	cmd := &cobra.Command{
      14 | 		Use:               "cache",
      15 | 		Short:             "Manage gittuf's caching functionality",
      16 | 		Long:              `The 'cache' command group contains subcommands to manage gittuf's local persistent cache. This cache helps improve performance by storing metadata locally. The cache is local-only and is not synchronized with remote repositories.`,
      17 | 		DisableAutoGenTag: true,
      18 | 	}
      19 | 
      20 | 	cmd.AddCommand(i.New())
      21 | 	cmd.AddCommand(delete.New())
      22 | 
      23 | 	return cmd
```

*No authentication decorator was found on this endpoint. If the endpoint handles sensitive actions, it may be accessible to unauthenticated callers. Verify whether authentication is enforced at a different layer (middleware, reverse proxy, MCP client credential check).*

</details>

<details>
<summary><code>internal/cmd/cache/init/init.go:26</code></summary>

```
      16 | 	repo, err := gittuf.LoadRepository(".")
      17 | 	if err != nil {
      18 | 		return err
      19 | 	}
      20 | 
      21 | 	return repo.PopulateCache()
      22 | }
      23 | 
      24 | func New() *cobra.Command {
      25 | 	o := &options{}
>>>   26 | 	cmd := &cobra.Command{
      27 | 		Use:   "init",
      28 | 		Short: "Initialize persistent cache",
      29 | 		Long:  `The 'init' command initializes the local persistent cache for a gittuf repository, intended to improve performance of gittuf operations. This cache is local-only and is not synchronized with the remote.`,
      30 | 		RunE:  o.Run,
      31 | 	}
      32 | 	o.AddFlags(cmd)
      33 | 
      34 | 	return cmd
      35 | }
```

*No authentication decorator was found on this endpoint. If the endpoint handles sensitive actions, it may be accessible to unauthenticated callers. Verify whether authentication is enforced at a different layer (middleware, reverse proxy, MCP client credential check).*

</details>

## All Instances

| # | File | Line | Severity | Confidence | Status |
|---|------|------|----------|------------|--------|
| 1 | `internal/cmd/verifynetwork/verifynetwork.go` | 26 | MEDIUM | 0.85 | Unmitigated |
| 2 | `internal/cmd/cache/cache.go` | 13 | MEDIUM | 0.85 | Unmitigated |
| 3 | `internal/cmd/cache/init/init.go` | 26 | MEDIUM | 0.85 | Unmitigated |
| 4 | `internal/cmd/cache/delete/delete.go` | 26 | MEDIUM | 0.85 | Unmitigated |
| 5 | `internal/cmd/verifymergeable/verifymergeable.go` | 60 | MEDIUM | 0.85 | Unmitigated |
| 6 | `internal/cmd/tui/tui.go` | 51 | MEDIUM | 0.85 | Unmitigated |
| 7 | `internal/cmd/attest/attest.go` | 16 | MEDIUM | 0.85 | Unmitigated |
| 8 | `internal/cmd/attest/apply/apply.go` | 40 | MEDIUM | 0.85 | Unmitigated |
| 9 | `internal/cmd/attest/github/github.go` | 15 | MEDIUM | 0.85 | Unmitigated |
| 10 | `internal/cmd/attest/github/pullrequest/pullrequest.go` | 99 | MEDIUM | 0.85 | Unmitigated |
| 11 | `internal/cmd/attest/github/recordapproval/recordapproval.go` | 92 | MEDIUM | 0.85 | Unmitigated |
| 12 | `internal/cmd/attest/github/dismissapproval/dismissapproval.go` | 66 | MEDIUM | 0.85 | Unmitigated |
| 13 | `internal/cmd/attest/authorize/authorize.go` | 69 | MEDIUM | 0.85 | Unmitigated |
| 14 | `internal/cmd/clone/clone.go` | 65 | MEDIUM | 0.85 | Unmitigated |
| 15 | `internal/cmd/version/version.go` | 34 | MEDIUM | 0.85 | Unmitigated |
| 16 | `internal/cmd/root/root.go` | 104 | MEDIUM | 0.85 | Unmitigated |
| 17 | `internal/cmd/dev/dev.go` | 18 | MEDIUM | 0.85 | Unmitigated |
| 18 | `internal/cmd/dev/rslrecordat/rslrecordat.go` | 65 | MEDIUM | 0.85 | Unmitigated |
| 19 | `internal/cmd/verifyref/verifyref.go` | 69 | MEDIUM | 0.85 | Unmitigated |
| 20 | `internal/cmd/trust/trust.go` | 46 | MEDIUM | 0.85 | Unmitigated |
| 21 | `internal/cmd/trust/setrepositorylocation/setrepositorylocation.go` | 48 | MEDIUM | 0.85 | Unmitigated |
| 22 | `internal/cmd/trust/addnetworkrepository/addnetworkrepository.go` | 77 | MEDIUM | 0.85 | Unmitigated |
| 23 | `internal/cmd/trust/init/init.go` | 47 | MEDIUM | 0.85 | Unmitigated |
| 24 | `internal/cmd/trust/removehook/removehook.go` | 84 | MEDIUM | 0.85 | Unmitigated |
| 25 | `internal/cmd/trust/enablegithubappapprovals/enablegithubappapprovals.go` | 48 | MEDIUM | 0.85 | Unmitigated |
| 26 | `internal/cmd/trust/updatepolicythreshold/updatepolicythreshold.go` | 48 | MEDIUM | 0.85 | Unmitigated |
| 27 | `internal/cmd/trust/makecontroller/makecontroller.go` | 40 | MEDIUM | 0.85 | Unmitigated |
| 28 | `internal/cmd/trust/removepolicykey/removepolicykey.go` | 50 | MEDIUM | 0.85 | Unmitigated |
| 29 | `internal/cmd/trust/listpropagationdirectives/listpropagationdirectives.go` | 52 | MEDIUM | 0.85 | Unmitigated |
| 30 | `internal/cmd/trust/addpolicykey/addpolicykey.go` | 53 | MEDIUM | 0.85 | Unmitigated |
| 31 | `internal/cmd/trust/incrementversion/incrementversion.go` | 37 | MEDIUM | 0.85 | Unmitigated |
| 32 | `internal/cmd/trust/addrootkey/addrootkey.go` | 53 | MEDIUM | 0.85 | Unmitigated |
| 33 | `internal/cmd/trust/removerootkey/removerootkey.go` | 50 | MEDIUM | 0.85 | Unmitigated |
| 34 | `internal/cmd/trust/removeglobalrule/removeglobalrule.go` | 49 | MEDIUM | 0.85 | Unmitigated |
| 35 | `internal/cmd/trust/removepropagationdirective/removepropagationdirective.go` | 48 | MEDIUM | 0.85 | Unmitigated |
| 36 | `internal/cmd/trust/updaterootthreshold/updaterootthreshold.go` | 48 | MEDIUM | 0.85 | Unmitigated |
| 37 | `internal/cmd/trust/updateglobalrule/updateglobalrule.go` | 94 | MEDIUM | 0.85 | Unmitigated |
| 38 | `internal/cmd/trust/inspectroot/inspectroot.go` | 47 | MEDIUM | 0.85 | Unmitigated |
| 39 | `internal/cmd/trust/addgithubapp/addgithubapp.go` | 64 | MEDIUM | 0.85 | Unmitigated |
| 40 | `internal/cmd/trust/updatehook/updatehook.go` | 141 | MEDIUM | 0.85 | Unmitigated |
| 41 | `internal/cmd/trust/addcontrollerrepository/addcontrollerrepository.go` | 77 | MEDIUM | 0.85 | Unmitigated |
| 42 | `internal/cmd/trust/addhook/addhook.go` | 141 | MEDIUM | 0.85 | Unmitigated |
| 43 | `internal/cmd/trust/removegithubapp/removegithubapp.go` | 48 | MEDIUM | 0.85 | Unmitigated |
| 44 | `internal/cmd/trust/listglobalrules/listglobalrules.go` | 73 | MEDIUM | 0.85 | Unmitigated |
| 45 | `internal/cmd/trust/addglobalrule/addglobalrule.go` | 96 | MEDIUM | 0.85 | Unmitigated |
| 46 | `internal/cmd/trust/listhooks/listhooks.go` | 69 | MEDIUM | 0.85 | Unmitigated |
| 47 | `internal/cmd/trust/sign/sign.go` | 39 | MEDIUM | 0.85 | Unmitigated |
| 48 | `internal/cmd/trust/disablegithubappapprovals/disablegithubappapprovals.go` | 48 | MEDIUM | 0.85 | Unmitigated |
| 49 | `internal/cmd/trust/addpropagationdirective/addpropagationdirective.go` | 92 | MEDIUM | 0.85 | Unmitigated |
| 50 | `internal/cmd/trust/updatepropagationdirective/updatepropagationdirective.go` | 94 | MEDIUM | 0.85 | Unmitigated |
| 51 | `internal/cmd/trustpolicy/apply/apply.go` | 40 | MEDIUM | 0.85 | Unmitigated |
| 52 | `internal/cmd/trustpolicy/discard/discard.go` | 26 | MEDIUM | 0.85 | Unmitigated |
| 53 | `internal/cmd/trustpolicy/stage/stage.go` | 40 | MEDIUM | 0.85 | Unmitigated |
| 54 | `internal/cmd/trustpolicy/remote/remote.go` | 13 | MEDIUM | 0.85 | Unmitigated |
| 55 | `internal/cmd/trustpolicy/remote/pull/pull.go` | 25 | MEDIUM | 0.85 | Unmitigated |
| 56 | `internal/cmd/trustpolicy/remote/push/push.go` | 25 | MEDIUM | 0.85 | Unmitigated |
| 57 | `internal/cmd/sync/sync.go` | 55 | MEDIUM | 0.85 | Unmitigated |
| 58 | `internal/cmd/rsl/rsl.go` | 17 | MEDIUM | 0.85 | Unmitigated |
| 59 | `internal/cmd/rsl/propagate/propagate.go` | 26 | MEDIUM | 0.85 | Unmitigated |
| 60 | `internal/cmd/rsl/record/record.go` | 74 | MEDIUM | 0.85 | Unmitigated |
| 61 | `internal/cmd/rsl/annotate/annotate.go` | 71 | MEDIUM | 0.85 | Unmitigated |
| 62 | `internal/cmd/rsl/skiprewritten/skiprewritten.go` | 26 | MEDIUM | 0.85 | Unmitigated |
| 63 | `internal/cmd/rsl/log/log.go` | 38 | MEDIUM | 0.85 | Unmitigated |
| 64 | `internal/cmd/rsl/remote/remote.go` | 14 | MEDIUM | 0.85 | Unmitigated |
| 65 | `internal/cmd/rsl/remote/reconcile/reconcile.go` | 24 | MEDIUM | 0.85 | Unmitigated |
| 66 | `internal/cmd/rsl/remote/pull/pull.go` | 25 | MEDIUM | 0.85 | Unmitigated |
| 67 | `internal/cmd/rsl/remote/push/push.go` | 25 | MEDIUM | 0.85 | Unmitigated |
| 68 | `internal/cmd/addhooks/addhooks.go` | 49 | MEDIUM | 0.85 | Unmitigated |
| 69 | `internal/cmd/policy/policy.go` | 31 | MEDIUM | 0.85 | Unmitigated |
| 70 | `internal/cmd/policy/init/init.go` | 48 | MEDIUM | 0.85 | Unmitigated |
| 71 | `internal/cmd/policy/removeperson/removeperson.go` | 57 | MEDIUM | 0.85 | Unmitigated |
| 72 | `internal/cmd/policy/addkey/addkey.go` | 68 | MEDIUM | 0.85 | Unmitigated |
| 73 | `internal/cmd/policy/removekey/removekey.go` | 57 | MEDIUM | 0.85 | Unmitigated |
| 74 | `internal/cmd/policy/addperson/addperson.go` | 122 | MEDIUM | 0.85 | Unmitigated |
| 75 | `internal/cmd/policy/removerule/removerule.go` | 57 | MEDIUM | 0.85 | Unmitigated |
| 76 | `internal/cmd/policy/incrementversion/incrementversion.go` | 48 | MEDIUM | 0.85 | Unmitigated |
| 77 | `internal/cmd/policy/updateperson/updateperson.go` | 127 | MEDIUM | 0.85 | Unmitigated |
| 78 | `internal/cmd/policy/reorderrules/reorderrules.go` | 51 | MEDIUM | 0.85 | Unmitigated |
| 79 | `internal/cmd/policy/listprincipals/listprincipals.go` | 75 | MEDIUM | 0.85 | Unmitigated |
| 80 | `internal/cmd/policy/updaterule/updaterule.go` | 103 | MEDIUM | 0.85 | Unmitigated |
| 81 | `internal/cmd/policy/addrule/addrule.go` | 103 | MEDIUM | 0.85 | Unmitigated |
| 82 | `internal/cmd/policy/sign/sign.go` | 48 | MEDIUM | 0.85 | Unmitigated |
| 83 | `internal/cmd/policy/listrules/listrules.go` | 79 | MEDIUM | 0.85 | Unmitigated |
| 84 | `docs/cli/main.go` | 19 | MEDIUM | 0.85 | Unmitigated |
| 85 | `docs/sandbox/main.go` | 22 | MEDIUM | 0.85 | Unmitigated |

*85 instances total.*

