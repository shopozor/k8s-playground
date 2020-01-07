## Flux setup

Follow the instructions provided in the [documentation](https://github.com/fluxcd/helm-operator-get-started), up to the following differences:

* download the fluxctl from the [releases](https://github.com/fluxcd/flux/releases)

* run 
```
helm upgrade -i flux fluxcd/flux --wait --namespace fluxcd --set git.url=git@github.com:shopozor/dev-cluster-configuration
```
instead of the command given in the doc