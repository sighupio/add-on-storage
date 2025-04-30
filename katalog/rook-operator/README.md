# Rook Operator

<!-- <SD-DOCS> -->

Rook provides a way to run a highly available, durable Ceph storage in your Kubernetes
cluster. See [Rook website][rook-website] for more details about the project.

## Requirements

- Kubernetes >= `1.28.0`
- Kustomize >= `v3.5.3`
- [cert-manager][cert-manager]

> cert-manager is nedeed to let Rook setup a Validating Webhook to asses that Rook
> CRDs are correctly configured.

## Image repository and tag

- Rook Operator image: `registry.sighup.io/fury/rook/ceph:v1.17.0`
- Ceph image: `registry.sighup.io/fury/ceph/ceph:v19.2.2`

## Deployment

You can deploy the Rook operator with the following command:

```bash
kubectl apply --server-side -k .
```

<!-- Links -->

[rook-website]: https://rook.io/
[cert-manager]: https://github.com/sighupio/fury-kubernetes-ingress/tree/main/katalog/cert-manager

<!-- </SD-DOCS> -->
