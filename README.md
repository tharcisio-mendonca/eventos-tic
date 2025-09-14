# Dashboards

https://grafana.com/grafana/dashboards/315-kubernetes-cluster-monitoring-via-prometheus/

https://grafana.com/grafana/dashboards/8171-kubernetes-nodes/

# Comando para obter a senha do Grafana

```
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```