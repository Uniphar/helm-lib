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

Inside your templates folder, create a `csi.yaml` file and add the following:
```yaml
{{- include "helm-lib.csi" (list . "<yourchart>.csi") -}}
{{- define "<yourchart>.csi" -}}
    #override here if needed
{{- end -}}
```

The Csi file will expect a values.yaml file in your chart's root folder. This file should contain the following:
```yaml

serviceAccount:
  name: <service account name>
  clientId: Azure AD Client ID / App ID / Service Principal, etc..
  tenantId: Azure Tenant ID

CSI:
  VolumeName: <volume name>
  ProviderClassName: <provider class name>
  kvName: <keyvault name>

kvSecrets:
  cosmosConnectionString:
    kvName: <keyvault name>
    k8Name: <k8s secret name>
    envName: <environment variable name>

```