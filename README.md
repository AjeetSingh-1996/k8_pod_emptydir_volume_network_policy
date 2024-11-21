# Multi-Container Kubernetes Pod with NetworkPolicy

This repository demonstrates how to deploy a **multi-container Pod** in Kubernetes with a **NetworkPolicy** to control ingress and egress traffic. The project includes an example configuration with two containers (Nginx and Busybox) running in the same Pod, and a policy to restrict network access to and from the Pod based on labels.

## Key Features

- **Multi-container Pod**: Runs multiple containers (e.g., Nginx and Firefox) in a single Kubernetes Pod.
- **NetworkPolicy**: Defines ingress and egress rules to control which Pods can communicate with each other.
- **Shared Volume**: Uses a shared `emptyDir` volume between containers to allow data sharing.
- **Custom Labels**: Applies labels to the Pod and uses them in the NetworkPolicy to define access rules.

## Prerequisites

To use this repository, you will need:

- A running Kubernetes cluster (you can use Minikube, Kind, or any cloud provider).
- **kubectl** installed and configured to interact with your cluster.

## Files

- **pod.yaml**: The Kubernetes configuration for deploying the multi-container Pod.
- **network-policy.yaml**: The Kubernetes configuration for the NetworkPolicy.

## How to Use

1. Clone the repository:

    ```bash
    git clone https://github.com/your-username/multi-container-k8s.git
    cd multi-container-k8s
    ```

2. Apply the Pod configuration:

    ```bash
    kubectl apply -f pod.yaml
    ```

3. Apply the NetworkPolicy configuration:

    ```bash
    kubectl apply -f network-policy.yaml
    ```

4. Verify that the Pod and NetworkPolicy are successfully created:

    ```bash
    kubectl get pods
    kubectl get networkpolicy
    ```

## Explanation of the Configuration

### Pod (pod.yaml)

The `Pod` configuration defines two containers:

- **Container 1 (nginx)**: Uses the `nginx:latest` image to serve web content on port 80.
- **Container 2 (busybox)**: Uses the `firefox` image and runs a `sleep` command for background tasks.

The two containers share an `emptyDir` volume, which allows them to exchange data.

### NetworkPolicy (network-policy.yaml)

The `NetworkPolicy` restricts network communication to and from the Pod. Specifically:

- **Ingress Traffic**: Only Pods with the label `app: allowed-app` can send traffic to this Pod on port 80.
- **Egress Traffic**: This Pod can only send traffic to Pods with the label `app: allowed-app` on port 80.

This ensures that only authorized Pods can communicate with the deployed Pod.

## Customizing the Configuration

You can modify the YAML files to:

- Change container images or add more containers to the Pod.
- Adjust the NetworkPolicy rules to allow or deny traffic to/from other Pods or external IPs.
- Add more volumes or environment variables as required.

## License

(Optional, if applicable)

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

Feel free to contribute by creating pull requests or opening issues if you have suggestions or encounter any bugs.
