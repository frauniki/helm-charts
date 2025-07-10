# frauniki's helm-charts repository

A collection of Helm charts for various Kubernetes applications and infrastructure components.

## Quick Start

```bash
# Add the repository
helm repo add frauniki https://frauniki.github.io/helm-charts/

# Update repository information
helm repo update

# Search for charts
helm search repo frauniki/

# Install a chart
helm install my-release frauniki/<chart-name>
```

## Available Charts

### Application Charts

| Chart | Version | Description |
|-------|---------|-------------|
| `generic-server` | 0.7.0 | A flexible chart for deploying generic server applications with full Kubernetes features support |
| `generic-batch` | - | Deploy batch jobs and cronjobs with comprehensive configuration options |
| `migration-job` | - | Execute database migrations and other one-time setup tasks |
| `mysql-console` | - | Deploy a MySQL console for database administration |

### Infrastructure & Operations

| Chart | Version | Description |
|-------|---------|-------------|
| `actions-runner` | 0.1.2 | Deploy GitHub Actions self-hosted runners on Kubernetes |
| `atlas-operator` | - | Operator for managing database schemas with Atlas |
| `atlas-migration` | - | Run Atlas database migrations |
| `unbound` | - | A caching DNS resolver suitable for use as an upstream DNS resolver |

### AWS & Cloud Native

| Chart | Version | Description |
|-------|---------|-------------|
| `karpenter-aws-provisoner` | 0.2.0 | AWS provisioner for Karpenter node autoscaling |

### Service Mesh & Networking

| Chart | Version | Description |
|-------|---------|-------------|
| `istio-resources` | - | Manage Istio service mesh resources (VirtualService, DestinationRule, ServiceEntry) |
| `thanos-querier` | - | Deploy Thanos Querier for global view of Prometheus metrics |

### Utilities

| Chart | Version | Description |
|-------|---------|-------------|
| `namespace` | - | Create and configure Kubernetes namespaces |
| `pluto` | - | Detect deprecated Kubernetes APIs in your cluster |

## Installation Examples

### Generic Server Application

```bash
# Install a basic web application
helm install my-app frauniki/generic-server \
  --set image.repository=myrepo/myapp \
  --set image.tag=v1.0.0 \
  --set service.port=8080

# Install with custom values file
helm install my-app frauniki/generic-server -f my-values.yaml
```

### GitHub Actions Runner

```bash
# Deploy a GitHub Actions runner
helm install github-runner frauniki/actions-runner \
  --set githubUrl=https://github.com/myorg/myrepo \
  --set runnerToken=YOUR_RUNNER_TOKEN
```

### Unbound DNS Resolver

```bash
# Deploy Unbound as a caching DNS resolver
helm install unbound frauniki/unbound \
  --set allowedIpRanges={"10.0.0.0/8"} \
  --set forwardZones[0].name="." \
  --set forwardZones[0].forwardIps={"8.8.8.8","8.8.4.4"}
```

## Chart Features

### Generic Server

The `generic-server` chart provides a comprehensive solution for deploying containerized applications with:

- **Deployment Management**: Configurable replicas, update strategies, and pod disruption budgets
- **Service Discovery**: ClusterIP, NodePort, and LoadBalancer service types
- **Ingress Support**: Configure ingress rules with TLS support
- **Auto-scaling**: Horizontal Pod Autoscaler (HPA) configuration
- **Configuration Management**: ConfigMaps and Secrets
- **Service Accounts**: RBAC and IAM integration
- **Observability**: Prometheus metrics and health checks
- **Sidecar Containers**: Support for additional containers

### Generic Batch

The `generic-batch` chart enables running batch workloads with:

- **Job Types**: One-time jobs or recurring CronJobs
- **Configuration**: Environment variables, ConfigMaps, and Secrets
- **Service Accounts**: For workload identity
- **Sidecar Support**: For logging, monitoring, or proxy containers

## Configuration

Each chart comes with a `values.yaml` file that contains default configuration values. You can override these values by:

1. **Command-line parameters**:
   ```bash
   helm install my-release frauniki/chart-name --set key=value
   ```

2. **Custom values file**:
   ```bash
   helm install my-release frauniki/chart-name -f custom-values.yaml
   ```

3. **Multiple values files**:
   ```bash
   helm install my-release frauniki/chart-name -f values-prod.yaml -f values-secrets.yaml
   ```

## Requirements

- Kubernetes 1.19+
- Helm 3.0+

Some charts may have additional requirements:
- `istio-resources`: Requires Istio service mesh
- `karpenter-aws-provisoner`: Requires Karpenter and AWS credentials
- `atlas-operator`: Requires Atlas CLI

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues on the [GitHub repository](https://github.com/frauniki/helm-charts).

## License

These charts are provided as-is under the MIT License.
