# Rook Operator

<!-- <SD-DOCS> -->

Rook provides a way to run a highly available, durable Ceph storage in your Kubernetes
cluster. See [Rook website][rook-website] for more details about the project.

## Requirements

- Kubernetes >= `1.26.0`

> cert-manager is nedeed to let Rook setup a Validating Webhook to assess that Rook
> CRDs are correctly configured.

## Image repository and tag

- Rook Operator image: `registry.sighup.io/fury/rook/ceph:v1.15.9`
- Ceph image: `registry.sighup.io/fury/ceph/ceph:v17.2.5`

## Deployment

You can deploy the Rook operator with the following command:

```bash
kustomize build . | kubectl apply -f - --server-side
```

<!-- Links -->

[rook-website]: https://rook.io/

<!-- </SD-DOCS> -->
