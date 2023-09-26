# GitHub Actions pipeline template

### GitHub Action: Docker Build, GCP registry push and Kustomize step

This GitHub Action module automates the process of building a Docker image an a application, pushing it to aGCP registry and running Kustomize steps for Kubernetes deployment.

## Inputs

- **app-name:** 'The app name'
- **app-registry:** 'The app GCP registry'
- **gcp-registry-project-id:** 'GCP Registry account project ID'
- **gcp-registry-service-account:** 'GCP service account JSON to push images to registry'
- **github-actor:** 'The commit author'
- **github-deploy-ssh-key:** 'The github deploy SSH key to clone K8S manifests'
- **github-package-url:** 'The github package URL to download application packages'
- **github-token:** 'The github token to download the application packages and create th GitOps PR from sandbox branch to master'
- **java-version:** 'Java version'
- **k8s-manifest-repo-name:** 'The name of K8S manifests repository'
- **k8s-manifest-repo-ssh:** 'The SSH of K8S manifests repository'


**OBS.:** All inputs are **required**

## Outputs

There are no outputs for this action

## Example usage

```yaml
    on: [push]

    permissions:
      id-token: write      # This is required for aws oidc connection
      contents: read       # This is required for actions/checkout
      pull-requests: write # This is required for gh bot to comment PR

    jobs:
      go_pipeline:
        runs-on: ubuntu-latest
        name: Go lang pipeline
        steps:
          - uses: actions/checkout@v3
            uses: makevalue-tech/github-actions-pipeline-template@main
            with:
              app-name: '<The app name>'
              app-registry: '<The app GCP registry>'
              gcp-registry-project-id: '<GCP Registry account project ID>'
              gcp-registry-service-account: '<GCP service account JSON to push images to registry>'
              github-actor: '<The commit author>'
              github-deploy-ssh-key: '<The github deploy SSH key to clone K8S manifests>'
              github-package-url: '<The github package URL to download application packages>'
              github-token: '<The github token to download the application packages and create th GitOps PR from sandbox branch to master>'
              java-distribution: 'Java distribution name'
              java-version: '<Java version eg. 17>'
              k8s-manifest-repo-name: '<The name of K8S manifests repository>'
              k8s-manifest-repo-ssh: '<The SSH of K8S manifests repository>'
```

## How to send updates?
If you wants to update or make changes in module code you should use the **develop** branch of this repository, you can test your module changes passing the `@develop` in module calling. Ex.:

```yaml
    on: [push]

    permissions:
      id-token: write # This is required for aws oidc connection
      contents: read # This is required for actions/checkout
      pull-requests: write # This is required for gh bot to comment PR

    jobs:
      go_pipeline:
        runs-on: ubuntu-latest
        name: Go lang pipeline
        steps:
          - uses: actions/checkout@v3
            uses: makevalue-tech/github-actions-pipeline-template@develop
            with:
              app-name: '<The app name>'
              app-registry: '<The app GCP registry>'
              gcp-registry-project-id: '<GCP Registry account project ID>'
              gcp-registry-service-account: '<GCP service account JSON to push images to registry>'
              github-actor: '<The commit author>'
              github-deploy-ssh-key: '<The github deploy SSH key to clone K8S manifests>'
              github-package-url: '<The github package URL to download application packages>'
              github-token: '<The github token to download the application packages and create th GitOps PR from sandbox branch to master>'
              java-distribution: 'Java distribution name'
              java-version: '<Java version eg. 17>'
              k8s-manifest-repo-name: '<The name of K8S manifests repository>'
              k8s-manifest-repo-ssh: '<The SSH of K8S manifests repository>'
```
After execute all tests you can open a pull request to the main branch.