# Object Types chart
Here you can find a reference implementation of Object Types deployment in the Kubernetes cluster via [Helm](https://helm.sh/).
This Helm chart installs Object Types API and is dependent on [PostgreSQL](https://github.com/bitnami/charts/tree/master/bitnami/postgresql) subchart.

:warning: The default settings are unsafe and should be used only for development purposes. Configure proper secrets, enable persistence, add certificates before using in production.

## Installation

Install the Helm chart with following commands:

```bash
cd deployment/helm/objecttypes
helm install objecttypes .
```

Use Kubernetes CLI to monitor the status of deployment:
```bash
kubectl get pods
```

If ingress is not configured you can use `port-forward` to check the status of application:
```bash
export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=objecttypes,app.kubernetes.io/instance=objecttypes" -o jsonpath="{.items[0].metadata.name}")
export CONTAINER_PORT=$(kubectl get pod --namespace default $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")
echo "Visit http://127.0.0.1:8080 to use your application"
kubectl --namespace default port-forward $POD_NAME 8080:$CONTAINER_PORT
```
