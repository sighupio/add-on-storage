# Compatibility Matrix

## Tested Kubernetes versions

| Module Version / Kubernetes Version | 1.25.X             | 1.26.X             | 1.27.X             | 1.28.X             | 1.29.X             | 1.30.X             | 1.31.X             | 1.32.X             | 1.33.X             |
| ----------------------------------- | ------------------ | ------------------ | ------------------ | ------------------ | ------------------ | ------------------ | ------------------ | ------------------ | ------------------ |
| v0.1.0                              | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| v0.2.0                              | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| v0.3.0                              | :x:                | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| v0.3.1                              | :x:                | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| v0.4.0                              | :x:                | :x:                | :x:                | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |

## Rook Operator compatibility against Ceph cluster versions

| Module Version / Ceph Cluster Version | >= 16.2.0          | >= 17.2.0          | >= 18.2.0          | >= 19.2.0          |
| ------------------------------------- | ------------------ | ------------------ | ------------------ | ------------------ |
| v0.1.0                                | :white_check_mark: | :white_check_mark: | :x:                | :x:                |
| v0.2.0                                | :white_check_mark: | :white_check_mark: | :x:                | :x:                |
| v0.3.0                                | :x:                | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| v0.3.1                                | :x:                | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| v0.4.0                                | :x:                | :x:                | :white_check_mark: | :white_check_mark: |

- :white_check_mark: Compatible
- :warning: Has issues
- :x: Incompatible
