# Deploying Kind Clusters on AWS

This repository provides Bash scripts to install dependencies and set up Kubernetes clusters in different AWS environments using **Amazon Linux 2**.

## Scripts Overview

- **kind_on_t3-medium.sh**:  
    - Installs dependencies and deploys a Kind-based Kubernetes cluster on AWS.  
    - Runs with **1 control plane and 2 worker nodes** using `t3.medium` instances.  
    - **Minimum Requirements**: `t3.medium` (2 vCPUs, 4 GB RAM).  

- **kind_on_free-tier.sh**:  
    - Installs dependencies and deploys a Kind-based Kubernetes cluster on AWS.  
    - Runs **only a control plane** on a `t2.micro` instance.  
    - **Suitable for AWS free tier** (1 vCPU, 1 GB RAM, best for lightweight workloads).  

## Prerequisites

Before running the scripts, ensure the following on your **Amazon Linux 2** EC2 instance:

- Git is installed
- Scripts have execution permissions

## Usage Instructions

### Deploying a Multi-Node Kind Cluster

The `kind_on_t3-medium.sh` script sets up a Kubernetes cluster with **1 control plane and 2 worker nodes** on AWS (`t3.medium` instances).

> **Note:** Ensure your instance has at least `t3.medium` configuration (2 vCPUs, 4 GB RAM) before running this script.

1. SSH into the EC2 instance and switch to the root user:
    ```bash
    sudo -i
    ```
2. Install Git:
    ```bash
    sudo yum install git -y
    ```
3. Clone the repository:
    ```bash
    git clone https://github.com/sivakumaranrg/k8s_arena.git
    cd k8s_arena/kind_cluster-ec2
    ```
4. Grant execution permissions to the script:
    ```bash
    chmod +x kind_on_t3-medium.sh
    ```
5. Run the script:
    ```bash
    ./kind_on_t3-medium.sh
    ```
6. Verify cluster deployment:
    ```bash
    kubectl get nodes
    ```
    Expected output:
    ```
    NAME                 STATUS   ROLES    AGE   VERSION
    kind-control-plane   Ready    master   1m    v1.21.1
    kind-worker          Ready    <none>   1m    v1.21.1
    kind-worker2         Ready    <none>   1m    v1.21.1
    ```

### Deploying a Control-Plane-Only Cluster (Free Tier)

The `kind_on_free-tier.sh` script sets up a Kubernetes cluster with **only a control plane** on AWS (`t2.micro` instance).

> **Note:** This instance type has 1 vCPU and 1 GB RAM, making it suitable for lightweight workloads only.

1. SSH into the EC2 instance and switch to the root user:
    ```bash
    sudo -i
    ```
2. Install Git:
    ```bash
    sudo yum install git -y
    ```
3. Clone the repository:
    ```bash
    git clone https://github.com/sivakumaranrg/k8s_arena.git
    cd k8s_arena/kind_cluster-ec2
    ```
4. Grant execution permissions to the script:
    ```bash
    chmod +x kind_on_free-tier.sh
    ```
5. Run the script:
    ```bash
    ./kind_on_free-tier.sh
    ```
6. Verify cluster deployment:
    ```bash
    kubectl get nodes
    ```
    Expected output:
    ```
    NAME                 STATUS   ROLES    AGE   VERSION
    kind-control-plane   Ready    master   1m    v1.21.1
    ```

## Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request for improvements.

### Reporting Issues

If you encounter any issues, please report them on the [GitHub Issues](https://github.com/sivakumaranrg/k8s_arena/issues) page.

## License

This project is licensed under the MIT License.
