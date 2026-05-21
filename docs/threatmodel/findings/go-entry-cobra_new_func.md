# Unauthenticated cli command (cobra): New()

**STRIDE category:** Spoofing
**Rule ID:** `go.entry.cobra_new_func`
**Max severity:** MEDIUM

## Mitigation

No specific guidance available.

*All 3 instances are unmitigated (no sidecar entries recorded).*

## Representative Examples

<details>
<summary><code>internal/cmd/dev/dismissgithubapproval/dismissgithubapproval.go:27</code></summary>

```
      17 | 	cmd.Flags().StringVarP(
      18 | 		&o.signingKey,
      19 | 		"signing-key",
      20 | 		"k",
      21 | 		"",
      22 | 		"specify key to sign attestation with",
      23 | 	)
      24 | 	cmd.MarkFlagRequired("signing-key") //nolint:errcheck
      25 | }
      26 | 
>>>   27 | func New() *cobra.Command {
      28 | 	o := &options{}
      29 | 	cmd := dismissapproval.New(&persistent.Options{SigningKey: o.signingKey, WithRSLEntry: true})
      30 | 	o.AddFlags(cmd)
      31 | 	cmd.Deprecated = "switch to \"gittuf attest github dismiss-approval\""
      32 | 	return cmd
      33 | }
```

*No authentication decorator was found on this endpoint. If the endpoint handles sensitive actions, it may be accessible to unauthenticated callers. Verify whether authentication is enforced at a different layer (middleware, reverse proxy, MCP client credential check).*

</details>

<details>
<summary><code>internal/cmd/dev/attestgithub/attestgithub.go:27</code></summary>

```
      17 | 	cmd.Flags().StringVarP(
      18 | 		&o.signingKey,
      19 | 		"signing-key",
      20 | 		"k",
      21 | 		"",
      22 | 		"specify key to sign attestation with",
      23 | 	)
      24 | 	cmd.MarkFlagRequired("signing-key") //nolint:errcheck
      25 | }
      26 | 
>>>   27 | func New() *cobra.Command {
      28 | 	o := &options{}
      29 | 	cmd := pullrequest.New(&persistent.Options{SigningKey: o.signingKey, WithRSLEntry: true})
      30 | 	o.AddFlags(cmd)
      31 | 	cmd.Deprecated = "switch to \"gittuf attest github pull-request\""
      32 | 	return cmd
      33 | }
```

*No authentication decorator was found on this endpoint. If the endpoint handles sensitive actions, it may be accessible to unauthenticated callers. Verify whether authentication is enforced at a different layer (middleware, reverse proxy, MCP client credential check).*

</details>

<details>
<summary><code>internal/cmd/dev/addgithubapproval/addgithubapproval.go:27</code></summary>

```
      17 | 	cmd.Flags().StringVarP(
      18 | 		&o.signingKey,
      19 | 		"signing-key",
      20 | 		"k",
      21 | 		"",
      22 | 		"specify key to sign attestation with",
      23 | 	)
      24 | 	cmd.MarkFlagRequired("signing-key") //nolint:errcheck
      25 | }
      26 | 
>>>   27 | func New() *cobra.Command {
      28 | 	o := &options{}
      29 | 	cmd := recordapproval.New(&persistent.Options{SigningKey: o.signingKey, WithRSLEntry: true})
      30 | 	o.AddFlags(cmd)
      31 | 	cmd.Deprecated = "switch to \"gittuf attest github record-approval\""
      32 | 	return cmd
      33 | }
```

*No authentication decorator was found on this endpoint. If the endpoint handles sensitive actions, it may be accessible to unauthenticated callers. Verify whether authentication is enforced at a different layer (middleware, reverse proxy, MCP client credential check).*

</details>

## All Instances

| # | File | Line | Severity | Confidence | Status |
|---|------|------|----------|------------|--------|
| 1 | `internal/cmd/dev/dismissgithubapproval/dismissgithubapproval.go` | 27 | MEDIUM | 0.85 | Unmitigated |
| 2 | `internal/cmd/dev/attestgithub/attestgithub.go` | 27 | MEDIUM | 0.85 | Unmitigated |
| 3 | `internal/cmd/dev/addgithubapproval/addgithubapproval.go` | 27 | MEDIUM | 0.85 | Unmitigated |

*3 instances total.*

