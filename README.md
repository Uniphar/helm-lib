# helm-lib
DevOps Helm Library

## Including the DevOps library in your chart

Add the library chart under dependencies and choose the version you want (example below). Version number can include ~ or ^ to pick up latest PATCH and MINOR versions respectively.
Issue the following commands to add the repo that contains the library chart, update the repo, then update dependencies in your Helm chart:
```bash
helm repo add uniphar https://uniphar.github.io/helm-lib/
helm repo update
helm dependency update
```
```
In your chart's `Chart.yaml` file, add the following:
```yaml
- name: helm-lib
  version: ^0.1.0
  repository: https://github.com/Uniphar/helm-lib
```