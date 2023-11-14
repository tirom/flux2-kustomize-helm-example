## Prerequisites
curl -s https://fluxcd.io/install.sh | sudo bash

git clone https://tirom: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@github.com/tirom/flux2-kustomize-helm-example.git

export GITHUB_TOKEN=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
export GITHUB_USER=tirom
export GITHUB_REPO=flux2-kustomize-helm-example
export GITHUB_REPO=https://github.com/tirom/flux2-kustomize-helm-example.git
export GITHUB_REPO=https://tirom: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@github.com/tirom/flux2-kustomize-helm-example.git

flux check --pre

Set the kubectl context to your staging cluster and bootstrap Flux:
flux bootstrap github \
    --context=docker-desktop \
    --owner=${GITHUB_USER} \
    --repository=${GITHUB_REPO} \
    --branch=main \
    --personal \
    --path=clusters/staging

► connecting to github.com
► cloning branch "main" from Git repository "https://github.com/tirom/flux2-kustomize-helm-example.git"
✔ cloned repository
► generating component manifests
✔ generated component manifests
✔ committed sync manifests to "main" ("b600a36a38daa87e57f6e70a07df63dff7deaaad")
► pushing component manifests to "https://github.com/tirom/flux2-kustomize-helm-example.git"
► installing components in "flux-system" namespace
✔ installed components
✔ reconciled components
► determining if source secret "flux-system/flux-system" exists
► generating source secret
✔ public key: ecdsa-sha2-nistp384 AAAAE2VjZHNhLXNoYTItbmlzdHAzODQAAAAIbmlzdHAzODQAAABhBMwPPDk8GLWxj5OvC9WvkGliL9jTlIkG8Z0ISP70L5eLOdG3Skezj5UjFZYcUdqZg9Zill/AoJErIaPx2sqKIiqZ8H1rZUJCsGSxuioKgeLxTUHA005UoD4a5KOnZcbuvA==
✔ configured deploy key "flux-system-main-flux-system-./clusters/staging" for "https://github.com/tirom/flux2-kustomize-helm-example"► applying source secret "flux-system/flux-system"
✔ reconciled source secret
► generating sync manifests
✔ generated sync manifests
✔ committed sync manifests to "main" ("8abe3cc45c9bd977db74f23203137e87aad49932")
► pushing sync manifests to "https://github.com/tirom/flux2-kustomize-helm-example.git"
► applying sync manifests
✔ reconciled sync configuration
◎ waiting for Kustomization "flux-system/flux-system" to be reconciled
✔ Kustomization reconciled successfully
► confirming components are healthy
✔ helm-controller: deployment ready
✔ kustomize-controller: deployment ready
✔ notification-controller: deployment ready
✔ source-controller: deployment ready
✔ all components are healthy

kubectl get Kustomization -n flux-system
kubectl get po -n flux-system
kubectl get po -n cert-manager
kubectl get po -n ingress-nginx

kubectl describe Kustomization apps -n flux-system