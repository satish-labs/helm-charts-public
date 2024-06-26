# Crossplane Module Chart

## TL;DR

## Introduction

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+

## Using the Chart

## Parameters

### Global parameters

| Name                               | Description                                                                                                              | Value                            |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | -------------------------------- |
| `global.chartNameOverride`         | Overrides the chart name.                                                                                                | `""`                             |
| `global.releaseNameOverride`       | Overrides the release name.                                                                                              | `crossplane`                     |
| `global.tags`                      | Define common tags for all IAC and app resources generated by this chart.                                                | `{}`                             |
| `global.labels`                    | Define common labels for all IAC and app resources generated by this chart.                                              | `{}`                             |
| `global.annotations`               | Define common annotations for all IAC and app resources generated by this chart.                                         | `{}`                             |
| `global.awsAccountId`              | Default aws account id for crossplane aws provider resources. Quotes are important, value must be a string.              | `0123456789`                     |
| `global.awsMgmtAccountId`          | Default aws account id of the main crossplane management instance. Quotes are important, value must be a string.         | `00000000000`                    |
| `global.awsRegion`                 | Default aws region for crossplane aws provider resources.                                                                | `us-east-2`                      |
| `global.eksHash`                   | Default EKS cluster hash for relevant crossplane resources such as IAM Role.                                             | `XXXXX`                          |
| `global.providerConfigRef.name`    | Default crossplane provider all resources generated for crossplane.                                                      | `crossplane-provider-config-aws` |
| `global.awsProviderVersion`        | Crossplane official AWS provider version: https://marketplace.upbound.io/providers/upbound/provider-aws/                 | `v0.47.1`                        |
| `global.kubernetesProviderVersion` | Crossplane Kubernetes provider version: https://marketplace.upbound.io/providers/crossplane-contrib/provider-kubernetes/ | `v0.11.0`                        |
| `global.crossplaneIAMRole`         | Crossplane AWS IAM role with administrative permissions to create cloud resources                                        | `crossplane-provider-aws`        |
| `global.crossplaneNamespace`       | Crossplane namespace                                                                                                     | `infra-crossplane`               |

### Crossplane configurations

| Name                       | Description                                | Value   |
| -------------------------- | ------------------------------------------ | ------- |
| `ControllerConfig.enabled` | Toggle for enabling or disabling template. | `false` |
| `ProviderConfig.enabled`   | Toggle for enabling or disabling template. | `false` |
| `StoreConfig.enabled`      | Toggle for enabling or disabling template. | `false` |
| `Provider.enabled`         | Toggle for enabling or disabling template. | `false` |

### Dependency: crossplane upstream helm chart parameters.

| Name                 | Description                                                | Value   |
| -------------------- | ---------------------------------------------------------- | ------- |
| `crossplane.enabled` | Toggle for enabling or disabling upstream chart templates. | `false` |

### Dependency: prometheus-service-discovery upstream helm chart parameters for creating serviceMonitors and podMonitors.

| Name                                   | Description                                                | Value   |
| -------------------------------------- | ---------------------------------------------------------- | ------- |
| `prometheus-service-discovery.enabled` | Toggle for enabling or disabling upstream chart templates. | `false` |

### Dependency: crossplane-aws-iam upstream helm chart parameters for creating and self managing crossplane IAM role

| Name                                                                                              | Description                                                | Value                                                        |
| ------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| `crossplane-aws-iam.enabled`                                                                      | Toggle for enabling or disabling upstream chart templates. | `false`                                                      |
| `crossplane-aws-iam.Role.items.provider-aws.annotations.crossplane.io/external-name`              | AWS resource name to import if exists.                     | `crossplane-provider-aws`                                    |
| `crossplane-aws-iam.Role.items.provider-aws.deletionPolicy`                                       | Deletion policy for the role.                              | `Orphan`                                                     |
| `crossplane-aws-iam.RolePolicyAttachment.items.provider-aws-adminaccess.deletionPolicy`           | Deletion policy for the role.                              | `Orphan`                                                     |
| `crossplane-aws-iam.RolePolicyAttachment.items.provider-aws-adminaccess.forProvider.policyArn`    | Default administratorAccess Policy resource ARN name.      | `arn:aws:iam::aws:policy/AdministratorAccess`                |
| `crossplane-aws-iam.RolePolicyAttachment.items.provider-aws-adminaccess.forProvider.roleRef.name` | Reference to the Role resource created by this helm chart. | `{{ include "common-gitops.names.release" . }}-provider-aws` |


## Configuration and installation details


## Troubleshooting


## Notable changes
