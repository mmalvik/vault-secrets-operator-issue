# Repro for vault secrets operator issue

## Steps

```shell
helm template .
```

This works fine.

Now update to vault-secrets-operator to `0.3.1` in `Chart.yaml`:

```yaml
dependencies:
  - name: vault
    version: 0.25.0
    repository: https://helm.releases.hashicorp.com
  - name: vault-secrets-operator 
    version: 0.3.1
    repository: https://helm.releases.hashicorp.com
```

And run update command:
```shell
helm dependency update
```

Now try to run template command again:
```shell
helm template .
```

Fails with error message.