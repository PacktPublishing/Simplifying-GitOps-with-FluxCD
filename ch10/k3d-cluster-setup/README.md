# Local Kubernetes Cluster Setup with K3d and Flux

This guide will walk you through setting up a local Kubernetes cluster with K3d and installing Flux using a Taskfile. The steps include installing K3d, creating a cluster, installing Flux, and configuring it with your GitHub repository.

## Prerequisites

- [Docker](https://www.docker.com/products/docker-desktop) must be installed and running.
- [Helm](https://helm.sh/docs/intro/install/) must be installed.
- [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl) must be installed.
- [flux cli](https://fluxcd.io/flux/installation/) must be installed
- [SOPS](https://github.com/getsops/sops/releases) must be installed.
- [AGE](https://github.com/FiloSottile/age?tab=readme-ov-file#installation) must be installed.


## Install Task

### macOS

1. Install Task using Homebrew:
    ```sh
    brew install go-task/tap/go-task
    ```

### Linux

1. Download and move the Task binary /usr/local/bin/ dir:
    ```sh
    sh -c "$(curl --location https://taskfile.dev/install.sh)" -- -d -b /usr/local/bin/
    ```

## Fork and clone the repository

Before running the setup, you need to fork the repository:

1. Go to [https://github.com/PacktPublishing/Simplifying-GitOps-with-FluxCD](https://github.com/PacktPublishing/Simplifying-GitOps-with-FluxCD) and fork the repository to your GitHub account.

2. Clone your GitHub repository and go to `./Simplifying-GitOps-with-FluxCD/ch10/k3d-cluster-setup` dir.
    ```sh
    git clone https://github.com/<your-github-username>/Simplifying-GitOps-with-FluxCD
    cd ./Simplifying-GitOps-with-FluxCD/ch10/k3d-cluster-setup
    ```

## Update the .env File

1. Before running the setup with `task setup`, you need to update the .env file with your details:
    ```sh
    GITHUB_USERNAME=your-github-username
    EMAIL=your-email@example.com
    AWS_ACCESS_KEY_ID=your-aws-access-key-id
    AWS_SECRET_ACCESS_KEY=your-aws-secret-access-key
    ```

## Run the Setup

1. Run the setup task to create and configure the local Kubernetes cluster:
    ```sh
    task setup
    ```

## Tasks Overview

The `setup` task will perform the following steps:

1. **Install K3d**: Installs K3d for managing the Kubernetes cluster.
2. **Create Cluster**: Creates a new Kubernetes cluster with K3d.
3. **Verify Cluster**: Verifies that the Kubernetes cluster is running.
4. **Switch Context**: Switches the context to the new K3d cluster.
5. **Install Flux Operator**: Installs the Flux operator using Helm.
6. **Generate SSH Key**: Generates an SSH key for Flux.
7. **Display Public Key**: Displays the public SSH key for you to add to your GitHub repository.
8. **Wait for Key Copy**: Waits for you to add the SSH key to your GitHub repository.
9. **Create Flux Secret**: Creates a Flux secret with the private SSH key.
10. **Generate AGE Key**: Generates an AGE key for encrypting secrets.
11. **Create SOPS Secret**: Creates a Kubernetes secret for SOPS with the AGE key.
12. **Update Flux Instance URL**: Updates the flux-instance.yaml file to replace "PacktPublishing" with your GitHub username.
13. **Push Flux Instance Update**: Commits and pushes the updated flux-instance.yaml file to your GitHub repository.
14. **Apply Flux Instance**: Deploys the Flux instance CRD.
15. **Create AWS Credentials File**: Create an AWS credentials file.
16. **Dry Run Create AWS Creds**: Creates a local AWS credentials YAML file.
17. **Encrypt AWS Creds**: Encrypts the AWS credentials file using SOSP and AGE.
18. **Push AWS Creds to Repo**: Push the encrypted AWS credentials file to your GitHub repository.
19. **Print Setup Complete**: Prints a message indicating the setup is complete.

## Author

`Georgi Lazarov`

#### Email: georgi@lazaroff.pro