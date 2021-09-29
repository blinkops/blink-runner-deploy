# blink-runner-deploy

How to deploy Blink Runner with kustomize

## Install kustomize

`brew install kustomize`

## Deploy new runner in dev

Navigate to dev environment and add a new runner from UI.

From the instructions box to deploy with helm capture the follwoing :
* apiid
* apikey
* ctrl_url

1. In runner/overlays/configmap set the "ctrl_url"  from value captured.
2. In runner/overlays/development set both apiId and apikey with corresponding captured values.
3. if needed create a new namespace for your runner and switch to it with kubens
4. with a terminal go in this repository path /kustomize/runner and run the followning
   
   `kustomize build overlays/development | kubectl apply -f -`

This will use values define in overlays/development to ovveride default values defined in base and apply it to the cluster.

As an example the jon folder shows how to manage several environment with overlays. It also brings an overlay on deployment.yaml to chenage image tag for docker-runner