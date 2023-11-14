## Prerequisites
curl -s https://fluxcd.io/install.sh | sudo bash

git clone https://tirom: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@github.com/tirom/flux2-kustomize-helm-example.git

export GITHUB_TOKEN=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
export GITHUB_USER=tirom
export GITHUB_REPO=flux2-kustomize-helm-example

flux check --pre

Set the kubectl context to your staging cluster and bootstrap Flux:
flux bootstrap github \
    --context=staging \
    --owner=${GITHUB_USER} \
    --repository=${GITHUB_REPO} \
    --branch=main \
    --personal \
    --path=clusters/staging
