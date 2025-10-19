Create namespace

kubectl create namespace monitoring


Add Helm repositories

helm repo add grafana https://grafana.github.io/helm-charts
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update


Deploy Prometheus + Grafana

helm install monitoring prometheus-community/kube-prometheus-stack \
  --version 72.6.2 \
  --namespace monitoring \
  --values helm/prometheus-values.yaml \
  --wait

Deploy Tempo

  helm install tempo grafana/tempo \
  --version 1.21.1 \
  --namespace monitoring \
  --values helm/tempo-values.yaml \
  --wait

Deploy Alloy

  helm install alloy grafana/alloy \
  --version 1.0.3 \
  --namespace monitoring \
  --values helm/alloy-values.yaml \
  --wait

Deploy trace generator

   kubectl apply -f trace-generator.yaml


Check the logs to see if traces are being sent

   kubectl logs -n monitoring deployment/k6-trace-generator

port-forward
   kubectl port-forward -n monitoring svc/monitoring-kube-prometheus-grafana 3000:80