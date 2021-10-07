# blink-runner-deploy

How to deploy Blink Runner with kustomize

## Install kustomize

`brew install kustomize`

## Deploy new runner in prod

Navigate to (environment)[https://app.blinkops.com/runners] and add a new runner from UI.

From the "command for helm" instructions capture the following :
* apiid
* apikey

1. In `runner/overlays/prod/secrets.ymal` set both apiId and apikey with corresponding captured values.
2. open a terminal and navigate to this repository local path ./kustomize/runner and run the followning
   
   `kustomize build overlays/prod | kubectl apply -f -`

This will use values define in overlays/prod to ovveride default values defined in base and apply it to the cluster.

## Deploy new runner in dev

Navigate to dev environment and add a new runner from UI.

From the command for helm instructions capture the following :
* apiid
* apikey

1. In `runner/overlays/development/secrets.ymal` set both apiId and apikey with corresponding captured values.
2. open a terminal and navigate to this repository local path ./kustomize/runner and run the followning
   
   `kustomize build overlays/development | kubectl apply -f -`

This will use values define in overlays/development to ovveride default values defined in base and apply it to the cluster.

As an example the jon folder shows how to manage to create a new namespace and deploy the runner into.