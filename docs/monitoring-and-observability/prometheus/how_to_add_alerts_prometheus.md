## Adding Alerts with Extra Volumes

You can also set up alerts by using `extraVolumes` and `extraVolumeMounts`. This allows you to create a ConfigMap for your alert rules and mount it into the Prometheus pod without modifying the main `values.yaml`.

### Steps to Configure Alerts

1. **Create a ConfigMap for Alerts**

   First, create a ConfigMap containing your alert rules. Here’s an example of how to create a ConfigMap named `prometheus-alerts`:

   ```yaml
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: prometheus-alerts
     namespace: <your-namespace>
   data:
     alerts.yml: |
       groups:
       - name: example_alerts
         rules:
         - alert: HighCPUUsage
           expr: sum(rate(container_cpu_usage_seconds_total[5m])) by (instance) > 0.8
           for: 5m
           labels:
             severity: warning
           annotations:
             summary: "High CPU Usage Detected"
             description: "CPU usage is above 80% for more than 5 minutes."
      ```

Save this as alerts-configmap.yaml, and create it with:

```bash
kubectl apply -f alerts-configmap.yaml
```
2. ***Create a Separate Values File for Alerts***
Create another values file named alerts-values.yaml. Here’s an example configuration to specify the extra volumes and mounts:

```yaml
extraVolumes:
  - name: alerts
    configMap:
      name: prometheus-alerts

extraVolumeMounts:
  - name: alerts
    mountPath: /etc/prometheus/alerts
    readOnly: true
```

3. ***Deploy or Update Prometheus***
To deploy Prometheus with the alert configuration, use the following command, ensuring you pass both the main values.yaml and the alerts-values.yaml:

```bash
helm install prometheus prometheus-community/prometheus -f values.yaml -f alerts-values.yaml -n <your-namespace>
```

If you are updating an existing deployment, use:

```bash
helm upgrade prometheus prometheus-community/prometheus -f values.yaml -f alerts-values.yaml -n <your-namespace>
```

4. Verify the Deployment
After deployment, check that Prometheus is running and that the alerts are configured correctly. You can view the logs of the Prometheus pod to ensure that the alerts were loaded:

```bash
kubectl logs <prometheus-pod-name> -n <your-namespace>
```

5. Access the Prometheus UI
To access the Prometheus UI, you can port-forward as before:

```bash
kubectl port-forward svc/prometheus-server -n <your-namespace> 9090:80
```

Visit http://localhost:9090 to view the alerts under the "Alerts" tab.

## Additional Notes
Ensure your alert rules are correctly formatted in the ConfigMap. For details on alert rule configuration, refer to the Prometheus alerting documentation.
You can create multiple ConfigMaps for different sets of alerts and mount them similarly by adjusting the extraVolumes and extraVolumeMounts in additional values files.

## Conclusion

You have successfully configured alerts for your Prometheus setup by using a separate values file for extraVolumes and extraVolumeMounts. This setup allows for greater flexibility and management of alert rules through ConfigMaps.

Feel free to make any further adjustments or ask if you need more modifications!
