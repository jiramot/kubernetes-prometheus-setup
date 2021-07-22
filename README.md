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
helm inspect values prometheus-community/prometheus
helm show values prometheus-community/prometheus
```
## Install prometheus chart
```
helm install [name] prometheus-community/prometheus
```
```
helm install prometheus prometheus-community/prometheus --create-namespace -n prometheus
```
## Delete prometheus chart
```
helm delete [name]
```
```
helm delete prometheus -n prometheus
```

## Install grafana
```
helm repo add grafana https://grafana.github.io/helm-charts
helm install grafana grafana/grafana -n prometheus
helm show values grafana/grafana
```
## Instal metric server on minikube
https://www.educative.io/courses/advanced-kubernetes-techniques/qVYQ5g9pwAk
```
minikube addons enable metrics-server
kubectl -n kube-system rollout status deployment metrics-server
```
## Install prometheus adapter
https://artifacthub.io/packages/helm/prometheus-community/prometheus-adapter
https://github.com/kubernetes-sigs/prometheus-adapter
```
helm install prometheus-adapter prometheus-community/prometheus-adapter -n prometheus --values helm-value-prometheus-adapter.yaml
```
```
kubectl -n prometheus  get --raw /apis/custom.metrics.k8s.io/v1beta1
kubectl -n prometheus get --raw "/apis/custom.metrics.k8s.io/v1beta1" | jq .  |grep "pods/"
kubectl -n prometheus  get --raw /apis/custom.metrics.k8s.io/v1beta1/namespaces/infinitaskt/pods/*/jvm_threads_live_threads_per_second
```

https://www.section.io/blog/horizontal-pod-autoscaling-custom-metrics/
```
helm install kube-state-metrics prometheus-community/kube-state-metrics -n prometheus

```