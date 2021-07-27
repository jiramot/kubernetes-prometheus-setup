# Prometheus
* [doc](https://artifacthub.io/packages/helm/prometheus-community/prometheus#configuration)

## Add helm repo
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add kube-state-metrics https://kubernetes.github.io/kube-state-metrics
helm repo update
```

## Setting up config
```
helm show values prometheus-community/prometheus
```
## Install prometheus chart
```
helm install prometheus prometheus-community/prometheus --create-namespace -n monitoring-system
```
## Install grafana
```
helm repo add grafana https://grafana.github.io/helm-charts
helm install grafana grafana/grafana -n monitoring-system
```
## Install metric server on minikube
https://www.educative.io/courses/advanced-kubernetes-techniques/qVYQ5g9pwAk
```
minikube addons enable metrics-server
kubectl -n kube-system rollout status deployment metrics-server
```
## Install prometheus adapter
```
helm install prometheus-adapter prometheus-community/prometheus-adapter -n monitoring-system --values helm-value-prometheus-adapter.yaml
```
```
kubectl -n prometheus  get --raw /apis/custom.metrics.k8s.io/v1beta1
kubectl -n prometheus get --raw "/apis/custom.metrics.k8s.io/v1beta1" | jq .  |grep "pods/"
kubectl -n prometheus  get --raw /apis/custom.metrics.k8s.io/v1beta1/namespaces/infinitaskt/pods/*/jvm_threads_live_threads_per_second
```

https://www.section.io/blog/horizontal-pod-autoscaling-custom-metrics/
```
helm install kube-state-metrics prometheus-community/kube-state-metrics -n monitoring-system

```