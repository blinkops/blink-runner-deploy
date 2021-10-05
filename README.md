# blink-runner-deploy

How to deploy Blink Runner with kustomize

## Install kustomize

`brew install kustomize`

## Deploy new runner in dev

Navigate to dev environment and add a new runner from UI.

From the instructions box to deploy with helm capture the following :
* apiid
* apikey
* ctrl_url

1. In runner/overlays/configmap.yaml set the "ctrl_url"  from value captured.
2. In runner/overlays/development.ymal set both apiId and apikey with corresponding captured values.
3. if needed create a new namespace for your runner and switch to it
4. open a terminal and navigate to this repository local path /kustomize/runner and run the followning
   
   `kustomize build overlays/development | kubectl apply -f -`

This will use values define in overlays/development to ovveride default values defined in base and apply it to the cluster.

As an example the jon folder shows how to manage several environment with overlays. It also brings an overlay on deployment.yaml to change image tag for docker-runner