## dding Dashboards with Extra Volumes in Grafana

You can set up Grafana dashboards using extraVolumes and extraVolumeMounts. This allows you to create a ConfigMap for your dashboards and mount it into the Grafana pod without modifying the main values.yaml.

## Steps to Configure Dashboards
1. Create a ConfigMap for Dashboards
First, create a ConfigMap containing your Grafana dashboards. Here’s an example of how to create a ConfigMap named grafana-dashboards:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: grafana-dashboards
  namespace: <your-namespace>
data:
  example-dashboard.json: |
    {
      "annotations": {
        "list": []
      },
      "panels": [
        {
          "datasource": "Prometheus",
          "type": "graph",
          "title": "CPU Usage",
          "targets": [
            {
              "expr": "sum(rate(container_cpu_usage_seconds_total[5m])) by (instance)",
              "format": "time_series"
            }
          ]
        }
      ],
      "schemaVersion": 16,
      "version": 1
    }
```

2. Save this as dashboards-configmap.yaml and create it with:
```bash
kubectl apply -f dashboards-configmap.yaml
```

3. Create a Separate Values File for Dashboards
Create another values file named dashboards-values.yaml. Here’s an example configuration to specify the extra volumes and mounts:

```yaml
extraVolumes:
  - name: dashboards
    configMap:
      name: grafana-dashboards

extraVolumeMounts:
  - name: dashboards
    mountPath: /var/lib/grafana/dashboards
    readOnly: true
```

4. Deploy or Update Grafana
To deploy Grafana with the dashboard configuration, use the following command, ensuring you pass both the main values.yaml and the dashboards-values.yaml:

```bash
helm install grafana grafana/grafana -f values.yaml -f dashboards-values.yaml -n <your-namespace>
```

If you are updating an existing deployment, use:
```bash
helm upgrade grafana grafana/grafana -f values.yaml -f dashboards-values.yaml -n <your-namespace>
```

5. Verify the Deployment
After deployment, check that Grafana is running and that the dashboards are configured correctly. You can view the logs of the Grafana pod to ensure that the dashboards were loaded:

```bash
kubectl logs <grafana-pod-name> -n <your-namespace>
```

6. Access the Grafana UI
To access the Grafana UI, you can port-forward as follows:

```bash
kubectl port-forward svc/grafana -n <your-namespace> 3000:80
```

Visit http://localhost:3000 to view the dashboards.

## Additional Notes

Ensure your dashboard JSON is correctly formatted in the ConfigMap. For details on dashboard configuration, refer to the Grafana documentation.

You can create multiple ConfigMaps for different sets of dashboards and mount them similarly by adjusting the extraVolumes and extraVolumeMounts in additional values files.

## Conclusion

You have successfully configured dashboards for your Grafana setup by using a separate values file for extraVolumes and extraVolumeMounts. This setup allows for greater flexibility and management of dashboards through ConfigMaps.

Feel free to ask if you need any more modifications or additional information!