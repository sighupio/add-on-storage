<h1 align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/sighupio/distribution/refs/heads/main/docs/assets/white-logo.png">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/sighupio/distribution/refs/heads/main/docs/assets/black-logo.png">
  <img alt="Shows a black logo in light color mode and a white one in dark color mode." src="https://raw.githubusercontent.com/sighupio/distribution/refs/heads/main/docs/assets/white-logo.png">
</picture><br/>
  Storage Add-On Module
</h1>

![Release](https://img.shields.io/badge/Latest%20Release-v0.3.0-blue)
![License](https://img.shields.io/github/license/sighupio/add-on-storage?label=License)
![Slack](https://img.shields.io/badge/slack-@kubernetes/fury-yellow.svg?logo=slack&label=Slack)

<!-- <SD-DOCS> -->

**Storage Add-On Module** provides the Rook Kubernetes Operator for Ceph add-on
for [SIGHUP Distribution (SD)][sd-repo].

If you are new to SD please refer to the [official documentation][sd-docs] on how
to get started with SD.

## Overview

**Storage Add-On Module** uses the [Rook operator][rook-page] to install and manage
Ceph clusters in a Kubernetes environment.

All the components are deployed in the `rook-ceph` namespace of the cluster.

## Packages

The following packages are included in the Storage Add-On Module katalog:

| Package                                                                    | Version   | Description                                                                                     |
| -------------------------------------------------------------------------- | --------- | ----------------------------------------------------------------------------------------------- |
| [rook-operator](katalog/rook-operator)                                     | `v1.15.9` | Rook provides a way to run a highly available, durable Ceph storage in your Kubernetes cluster. |
| [rook-hostcluster](katalog/rook-hostcluster)                               | `NA`      | Rook CRDs to run a production ready Ceph cluster providing Block and File storage.              |
| [nfs-subdir-external-provisioner](katalog/nfs-subdir-external-provisioner) | `v4.0.2`  | Dynamic sub-dir volume provisioner on a remote NFS server.                                      |

Click on each package to see its full documentation.

## Compatibility

| Kubernetes Version |   Compatibility    | Notes           |
| ------------------ | :----------------: | --------------- |
| `1.29.x`           | :white_check_mark: | No known issues |
| `1.30.x`           | :white_check_mark: | No known issues |
| `1.31.x`           | :white_check_mark: | No known issues |

Check the [compatibility matrix][compatibility-matrix] for additional information
about previous releases of the modules.

The module is still in version `0.X.X` but can be used in production.

## Usage

### Prerequisites

| Tool                                  | Version    | Description                                                                                                                                               |
| ------------------------------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [furyctl][furyctl-repo]               | `>=0.29.0` | The recommended tool to download and manage SD modules and their packages. To learn more about `furyctl` read the [official documentation][furyctl-repo]. |
| [prometheus-opeator][fury-monitoring] | `>=2.0.1`  | prometheus-operator is needed by Rook in order to install the ServiceMonitor needed to monitor the Ceph cluster.                                          |

### Deployment

#### SIGHUP Distribution

In your `furyctl.yaml` specify the storage-add-on as a plugin:

```yaml
plugins:
  kustomize:
    - name: rook-operator
      folder: https://github.com/sighupio/add-on-storage/katalog/rook-operator?ref=v0.3.0
    - name: rook-hostcluster
      folder: https://github.com/sighupio/add-on-storage/katalog/rook-hostcluster?ref=v0.3.0
```

Then, use `furyctl apply` to deploy cheph in your cluster.

#### Legacy

1. List the packages you want to deploy and their version in a `Furyfile.yml`

   ```yaml
   bases:
     - name: ingress/cert-manager
       version: "v1.13.1"
     - name: monitoring/promtheus-operator
       version: "v2.0.1"
     - name: storage/rook-operator
       version: "v0.3.0"
     - name: storage/rook-hostcluster
       version: "v0.3.0"
   ```

   > [!INFO]
   > See `furyctl` [documentation][furyctl-repo] for additional details about `Furyfile.yml`
   > format.

2. Execute `furyctl vendor -H` (before v0.11.1), starting from fury v0.25.0 use
   `furyctl legacy vendor -H` to download the packages
3. Inspect the downloaded packages under `./vendor/katalog/storage`.
4. Define a `kustomization.yaml` that includes the `./vendor/katalog/storage` directory
   as resource.

   ```yaml
   resources:
     - ./vendor/katalog/ingress/cert-manager
     - ./vendor/katalog/monitoring/prometheus-operator
     - ./vendor/katalog/storage/rook-operator
     - ./vendor/katalog/storage/rook-hostcluster
   ```

5. To deploy the packages to your cluster, execute:

```bash
kustomize build . | kubectl apply -f - --server-side
```

<!-- Links -->

[rook-page]: https://rook.io
[sd-repo]: https://github.com/sighupio/distribution
[furyctl-repo]: https://github.com/sighupio/furyctl
[kustomize-repo]: https://github.com/kubernetes-sigs/kustomize
[sd-docs]: https://docs.kubernetesfury.com/docs/distribution/
[compatibility-matrix]: https://github.com/sighupio/fury-kubernetes-storage/blob/main/docs/COMPATIBILITY_MATRIX.md
[fury-ingress]: https://github.com/sighupio/fury-kubernetes-ingress/tree/main/katalog/cert-manager
[fury-monitoring]: https://github.com/sighupio/fury-kubernetes-monitoring/tree/main/katalog/prometheus-operator

<!-- </SD-DOCS> -->

<!-- <FOOTER> -->

## Contributing

Before contributing, please read first the [Contributing Guidelines](https://docs.kubernetesfury.com/docs/contribute/).

### Reporting Issues

In case you experience any problem with the module, please [open a new issue](https://github.com/sighupio/fury-kubernetes-storage/issues/new/choose).

## License

This module is open-source and it's released under the following [LICENSE](LICENSE)

<!-- </FOOTER> -->
