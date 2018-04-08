This repository contains docker images for a selected set of minecraft modpacks found on https://minecraft.curseforge.com/modpacks. All images bundle a specific version of a pack with OpenJDK and are set up to simply start the server.  
This repo also contains a helm chart template to install those images on a kubernetes cluster.

## Docker

The image stores world data in `/var/lib/minecraft`. So this is where you want to mount a persistent data volume. The image also allows to set min and max heap for the JVM through the environment parameters `JVM_MIN_HEAP` and `JVM_MAX_HEAP`. They default to 2g and 6g.

## Kubernetes

The `modpack-server-chart` directory contains a helm chart that can be used to deploy a modpack server image on a kubernetes cluster. The deployment has no frontend so port-forwarding to the pod running the server is required. Alternatively you can manually create a `NodePort` service. Check `modpack-server-chart/values.yaml` to configure the deployment (modpack, version, etc.).

Make sure you have helm installed and set up correctly.  
```
cd modpack-server-chart
helm template . | kubectl -n YOUR_NAMESPACE_HERE apply -f -

kubectl -n YOUR_NAMESPACE_HERE port-forward THE_POD_NAME_HERE 25565
```


