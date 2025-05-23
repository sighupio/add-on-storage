# `rook-operator` Package Maintenance

To prepare a new release of this package:

1. Get the current upstream release

   ```bash
   export ROOK_RELEASE=v1.17.2
   wget -c https://raw.githubusercontent.com/rook/rook/${ROOK_RELEASE}/deploy/examples/common.yaml \
     https://raw.githubusercontent.com/rook/rook/${ROOK_RELEASE}/deploy/examples/crds.yaml \
     https://raw.githubusercontent.com/rook/rook/${ROOK_RELEASE}/deploy/examples/operator.yaml
   ```

   Replace `ROOK_RELEASE` with the current upstream release.

2. Check the differences introduced by pulling the upstream release and any new
   file in `kustomization.yaml`
3. Update the `kustomization.yaml` file with the new image versions.
4. Update `rook-ceph-operator-config-csi-images.yml` with the correct images, refer
   to the [docs](https://rook.io/docs/rook/v1.17/Storage-Configuration/Ceph-CSI/custom-images/)
5. Sync the new images to our registry in the [container-image-sync repository](https://github.com/sighupio/fury-distribution-container-image-sync/blob/main/modules/storage/images.yml).
