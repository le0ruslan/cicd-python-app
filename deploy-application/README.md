# CI/CD for Python App

## Project Description
This repository implements the deployment of the application [devops-sample-django-app](https://github.com/simbirsoft/devops-sample-django-app) using Kind and Helm. The CI/CD process is carried out using GitLab Runner, with two separate pipelines for the frontend and backend.

## Installing Kind

To install Kind, follow the official instructions from the [kind](https://kind.sigs.k8s.io/docs/user/quick-start/#installing-from-release-binaries) website:

1. Download the Kind binary file (for AMD64 / x86_64 architecture):

   ```sh
   [ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.26.0/kind-linux-amd64
   ```

2. Make the file executable:

   ```sh
   chmod +x ./kind
   ```

3. Move the Kind binary to the `/usr/local/bin/kind` directory:

   ```sh
   sudo mv ./kind /usr/local/bin/kind
   ```

4. Check the Kind version:

   ```sh
   kind --version
   ```

5. Install the [cloud provider](https://github.com/kubernetes-sigs/cloud-provider-kind/tree/main) for Kind, which is required for Ingress functionality:

   ```sh
   go install sigs.k8s.io/cloud-provider-kind@latest
   ```

## Deploying the Application

1. Create a Kind cluster:

   ```sh
   sudo kind create cluster --config kind-cluster.yaml
   ```

2. Install and start GitLab Runner:

   ```sh
   sudo helm repo add gitlab https://charts.gitlab.io
   sudo helm repo update
   sudo helm upgrade gitlab-runner gitlab/gitlab-runner -f .deploy/gitlab-runner/gitlab-runner.yaml -n gitlab-runner --install --create-namespace
   ```

3. Navigate to the `backend` repository, make the necessary changes, and commit them.

4. Navigate to the `frontend` repository, make the necessary changes, and commit them.

5. The pipelines will automatically start in GitLab.

## Verifying the Deployment

* Navigate to the directory containing the Kind cloud provider installed in step 5 of the "Installing Kind" section and start it:

   ```sh
   ./cloud-provider-kind
   ```

* In another terminal, obtain the external IP address assigned by Ingress:

   ```sh
   sudo kubectl get svc frontend-service -n workshop2025 -o jsonpath='{.status.loadBalancer.ingress[0].ip}'
   ```

* Open a browser and go to the following URL to view the application interface:

   ```
   http://{external-ip}/
   ```

