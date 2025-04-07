# mosquitto-helm-chart

This repository contains a Helm chart for deploying the Mosquitto MQTT broker on Kubernetes. Helm is a package manager for Kubernetes that simplifies the deployment and management of applications.

## Features

- Deploys the Mosquitto MQTT broker as a Kubernetes deployment.
- Configurable settings for persistence, service type, and resource limits.
- Includes a ConfigMap for customizing the Mosquitto configuration.
- Supports persistent volume claims (PVC) for data storage.

## Prerequisites

- Kubernetes cluster (v1.19+ recommended)
- Helm (v3.0+ recommended)

## Installation

1. Add the repository (if applicable):
   ```bash
   helm repo add mosquitto-helm-chart <repository-url>
   ```

2. Install the chart:
   ```bash
   helm install my-mosquitto ./mosquitto-helm-chart
   ```
   Replace `my-mosquitto` with your desired release name.

3. Verify the installation:
   ```bash
   kubectl get all -l app.kubernetes.io/name=mosquitto
   ```

## Configuration

The chart can be customized using the `values.yaml` file. Below are some of the configurable parameters:

| Parameter              | Description                                | Default |
|------------------------|--------------------------------------------|---------|
| `replicaCount`         | Number of replicas                        | `1`     |
| `image.repository`     | Mosquitto image repository                | `eclipse-mosquitto` |
| `image.tag`            | Mosquitto image tag                       | `latest`|
| `service.type`         | Kubernetes service type                   | `ClusterIP` |
| `persistence.enabled`  | Enable persistent storage                 | `false` |
| `persistence.size`     | Size of the persistent volume             | `1Gi`   |
| `resources.limits.cpu` | CPU resource limits                       | `100m`  |
| `resources.limits.memory` | Memory resource limits                  | `128Mi` |

To override these values, create a custom `values.yaml` file and pass it during installation:
```bash
helm install my-mosquitto ./mosquitto-helm-chart -f custom-values.yaml
```

## Files

- `Chart.yaml`: Contains metadata about the Helm chart.
- `values.yaml`: Default configuration values for the chart.
- `templates/`: Directory containing Kubernetes resource templates.
  - `configmap.yaml`: ConfigMap for Mosquitto configuration.
  - `deployment.yaml`: Deployment resource for Mosquitto.
  - `pvc.yaml`: PersistentVolumeClaim for data storage.
  - `service.yaml`: Service resource for exposing Mosquitto.

## Uninstallation

To uninstall the chart:
```bash
helm uninstall my-mosquitto
```
This will remove all resources associated with the release.

## License

This project is licensed under the terms of the MIT License. See the `LICENSE` file for details.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any improvements or bug fixes.

## References

- [Mosquitto Documentation](https://mosquitto.org/documentation/)
- [Helm Documentation](https://helm.sh/docs/)