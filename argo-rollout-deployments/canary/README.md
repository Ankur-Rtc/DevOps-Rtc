# Argo Rollouts and Helm

Argo Rollouts will respond to changes in Rollout resources
regardless of the event source. If you package your manifest
with the Helm package manager you can perform Progressive Delivery deployments with Helm

1. Install the Argo Rollouts controller in your cluster: https://github.com/argoproj/argo-rollouts#installation
2. Install the `helm` executable locally: https://helm.sh/docs/intro/install/

## Deploying the initial version

To deploy the first version of your application:

```
git clone https://github.com/Ankur-Rtc/DevOps-Rtc.git
cd argo-rollout-deployments/
helm install example ./canary/
```

Your application will be deployed and exposed via the `example-helm-guestbook` service

## Perform the second deployment

To deploy the updated version using a Blue/Green strategy:

```
helm upgrade example ./canary/  --set image.tag=1.22
```

It will start the upgrade process and will follow the steps defined in strategy. This will promotes container image `nginx:latest` to `green` status and `Rollout` deletes old replica which runs `nginx:1.22`.
