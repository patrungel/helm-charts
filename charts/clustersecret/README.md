# clustersecret

A Helm Chart for [ClusterSecret](https://github.com/zakkg3/ClusterSecret)

![Version: 0.2.0](https://img.shields.io/badge/Version-0.2.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.0.9](https://img.shields.io/badge/AppVersion-0.0.9-informational?style=flat-square)

ClusterSecret Operator provides inter-namespace (or cluster-wide) secrets

**Homepage:** <https://github.com/patrungel/clustersecret-helm>

## Introduction

This chart introduces ClusterSecret custom resource, creates a deployment to run the ClusterSecret operator and optionally creates a number of ClusterSecret-s.

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| patrungel | <patrungel@gmail.com> |  |

## Source Code

* <https://github.com/zakkg3/ClusterSecret>
* <https://github.com/patrungel/helm-charts>

## Requirements

Kubernetes: `>= 1.16.0-0`

## Required Configuration

No configuration is required, the defaults are sufficient to run the operator. It is however recommended to specify `resources` matching your cluster.

### Specifying environment

Using command line:

```helm
helm -f values.yaml install --name test patrungel/clustersecret
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | affinity spec for clustersecret deployment |
| clusterSecrets | list | `[]` | Optional clustersecret entities to be managed as part of release For a given clustersecret name and data are the only required fields For details refer to https://github.com/zakkg3/ClusterSecret/tree/master/yaml/Object_example Example: clusterSecrets: - name: global-regcred  labels:    owner: ops  annotations:    rotate: never  matchNamespace:  - workers  - ".*-dev"  avoidNamespaces:  - default  - kube-system  type: "kubernetes.io/dockerconfigjson"  data:    .dockerconfigjson: ZHVtbXk= - name: db-creds  matchNamespace:  - ".*-dev"  data:    user: ZHVtbXk=    password: ZHVtbXk= |
| extraArgs | list | `[]` | Additional clustersecret container arguments Example: extraArgs: - --verbose |
| extraVars | object | `{}` | Optional environment variables as key-value pairs Example: extraVars:   LANG: en_US.utf8 |
| fullnameOverride | string | `""` | Set to override the release name |
| image.pullPolicy | string | `"IfNotPresent"` | Image pullPolicy to use |
| image.repository | string | `"flag5/clustersecret"` | Image repository to use |
| image.tag | string | `nil` | Image tag to use (defaults to appVersion of the chart) |
| nameOverride | string | `""` | Set to override the chart name part of the release name |
| nodeSelector | object | `{}` | nodeSelector spec for clustersecret deployment |
| podAnnotations | object | `{}` | Annotations for clustersecret deployment |
| podExtraLabels | object | `{}` | Additional labels for clustersecret deployment |
| priorityClassName | string | `""` | priorityClassName for clustersecret deployment |
| rbac.create | bool | `true` | If true create and use RBAC resources |
| replicaCount | int | `1` | Number of pod replicas in clustersecret deployment |
| resources | object | `{}` | Pod resources for clustersecret deployment Example: resources:   limits:     cpu: 50m     memory: 200Mi   requests:     cpu: 50m     memory: 200Mi |
| securityContext | object | `{}` | Pod security context for clustersecret deployment Example: securityContext:   runAsUser: 1000 |
| serviceAccount.annotations | object | `{}` | Service account annotations. Ignored if serviceAccount.create is false. |
| serviceAccount.create | bool | `true` | If true create a ServiceAccount |
| serviceAccount.imagePullSecretNames | list | `[]` | List of imagePullSecret names to use with the service account. Ignored if serviceAccount.create is false. |
| serviceAccount.name | string | `""` | The name of the ServiceAccount to use. If not set and create is true, a name is generated using the fullname template. |
| strategy | object | `{"type":"Recreate"}` | strategy spec for clustersecret deployment |
| tolerations | list | `[]` | tolerations spec for clustersecret deployment |

Please refer to [values.yaml](./values.yaml) for detailed examples.
