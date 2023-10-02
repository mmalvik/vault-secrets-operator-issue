# Repro for vault secrets operator issue

## Steps

```shell
helm template .
```

This works fine.

Now update to vault-secrets-operator from `0.1.0` to `0.3.1` in `Chart.yaml`:

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

Fails with error message:
```shell
Error: template: secrets-operator-issue/charts/vault/templates/tests/server-test.yaml:17:6: executing "secrets-operator-issue/charts/vault/templates/tests/server-test.yaml" at <include "imagePullSecrets" .>: error calling include: template: secrets-operator-issue/charts/vault-secrets-operator/templates/_helpers.tpl:140:15: executing "imagePullSecrets" at <.Values.controller.imagePullSecrets>: nil pointer evaluating interface {}.imagePullSecrets
```