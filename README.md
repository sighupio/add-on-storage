<h1>
    <img src="https://github.com/sighupio/fury-distribution/blob/main/docs/assets/fury-epta-white.png?raw=true" align="left" width="90" style="margin-right: 15px"/>
    Kubernetes Fury Storage
</h1>

![Release](https://img.shields.io/badge/Latest%20Release-v0.1.0-blue)
![License](https://img.shields.io/github/license/sighupio/fury-kubernetes-logging?label=License)
![Slack](https://img.shields.io/badge/slack-@kubernetes/fury-yellow.svg?logo=slack&label=Slack)

<!-- <KFD-DOCS> -->

**Kubernetes Fury Storage** provides the Rook Kubernetes Operator for Ceph add-on for [Kubernetes Fury Distribution (KFD)][kfd-repo].

If you are new to KFD please refer to the [official documentation][kfd-docs] on how to get started with KFD.

## Overview

**Kubernetes Fury Storage** uses the [Rook operator][rook-page] to install and manage Ceph clusters in a Kubernetes environment.

All the components are deployed in the `rook-ceph` namespace in the cluster.

## Packages

The following packages are included in the Fury Kubernetes Storage katalog:

| Package                                      | Version   | Description                                                                                                                                          |
|----------------------------------------------|-----------|-------------------------------------------------------------------------------------------------|
| [rook-operator](katalog/rook-operator)       | `v1.10.5` | Rook provides a way to run a highly available, durable Ceph storage in your Kubernetes cluster. |
| [rook-hostcluster](katalog/rook-hostcluster) | `NA`      | Rook CRDs to run a production ready Ceph cluster providing Block and File storage.              |                                                                                                 |

Click on each package to see its full documentation.

## Compatibility

| Kubernetes Version |   Compatibility    | Notes                                               |
|--------------------|:------------------:|-----------------------------------------------------|
| `1.22.x`           | :white_check_mark: | No known issues                                     |
| `1.23.x`           | :white_check_mark: | No known issues                                     |
| `1.24.x`           | :white_check_mark: | No known issues                                     |

Check the [compatibility matrix][compatibility-matrix] for additional information about previous releases of the modules.

The module is still in version `0.X.X` but can be used in production.

## Usage

### Prerequisites

| Tool                        | Version    | Description                                                                                                                                                    |
|-----------------------------|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [furyctl][furyctl-repo]     | `>=0.6.0`  | The recommended tool to download and manage KFD modules and their packages. To learn more about `furyctl` read the [official documentation][furyctl-repo].     |
| [kustomize][kustomize-repo] | `3.5.3`  | Packages are customized using `kustomize`. To learn how to create your customization layer with `kustomize`, please refer to the [repository][kustomize-repo]. |
| [cert-manager][fury-ingress]| `>=1.13.1` | cert-manager is needed by Rook in order to install a Validating Webhook to asses that Rook CRs are correctly configured.                                        |

### Deployment

1. List the packages you want to deploy and their version in a `Furyfile.yml`

```yaml
bases:
  - name: ingress/cert-manager
    version: "v1.13.0"
  - name: storage/rook-operator
    version: "v0.1.0"
  - name: storage/rook-hostcluster
    version: "v0.1.0"
```

> See `furyctl` [documentation][furyctl-repo] for additional details about `Furyfile.yml` format.

2. Execute `furyctl vendor -H` to download the packages

3. Inspect the download packages under `./vendor/katalog/storage`.

4. Define a `kustomization.yaml` that includes the `./vendor/katalog/storage` directory as resource.

```yaml
resources:
  - ./vendor/katalog/ingress/cert-manager
  - ./vendor/katalog/storage/rook-operator
  - ./vendor/katalog/storage/rook-hostcluster
```

5. To deploy the packages to your cluster, execute:

```bash
kustomize build . | kubectl apply -f -
```

<!-- Links -->

[rook-page]: https://rook.io
[kfd-repo]: https://github.com/sighupio/fury-distribution
[furyctl-repo]: https://github.com/sighupio/furyctl
[kustomize-repo]: https://github.com/kubernetes-sigs/kustomize
[kfd-docs]: https://docs.kubernetesfury.com/docs/distribution/
[compatibility-matrix]: https://github.com/sighupio/fury-kubernetes-storage/blob/main/docs/COMPATIBILITY_MATRIX.md
[fury-ingress]: https://github.com/sighupio/fury-kubernetes-ingress/tree/main/katalog/cert-manager

<!-- </KFD-DOCS> -->

<!-- <FOOTER> -->

## Contributing

Before contributing, please read first the [Contributing Guidelines](docs/CONTRIBUTING.md).

### Reporting Issues

In case you experience any problem with the module, please [open a new issue](https://github.com/sighupio/fury-kubernetes-storage/issues/new/choose).

## License

This module is open-source and it's released under the following [LICENSE](LICENSE)

<!-- </FOOTER> -->
