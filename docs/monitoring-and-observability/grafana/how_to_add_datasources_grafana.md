## Adding Data Sources with Extra Volumes for Grafana

You can set up data sources in Grafana using extraVolumes and extraVolumeMounts. This allows you to create a ConfigMap for your data sources and mount it into the Grafana pod without modifying the main values.yaml.

## Steps to Configure Data Sources
1. Create a ConfigMap for Data Sources
First, create a ConfigMap containing your data source configurations. Here’s an example of how to create a ConfigMap named grafana-datasources:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: grafana-datasources
  namespace: <your-namespace>
data:
  datasource.yml: |
    apiVersion: 1
    datasources:
      - name: Prometheus
        type: prometheus
        access: proxy
        url: http://prometheus-server.<your-namespace>:9090
        jsonData:
          tlsSkipVerify: true
```

2. Save this as datasources-configmap.yaml, and create it with:
```bash
kubectl apply -f datasources-configmap.yaml
```

3. Create a Separate Values File for Data Sources
Create another values file named datasources-values.yaml. Here’s an example configuration to specify the extra volumes and mounts:

```yaml
extraVolumes:
  - name: datasources
    configMap:
      name: grafana-datasources

extraVolumeMounts:
  - name: datasources
    mountPath: /etc/grafana/provisioning/datasources
    readOnly: true
```

4. Deploy or Update Grafana
To deploy Grafana with the data source configuration, use the following command, ensuring you pass both the main values.yaml and the datasources-values.yaml:

```bash
helm install grafana grafana/grafana -f values.yaml -f datasources-values.yaml -n <your-namespace>
```

If you are updating an existing deployment, use:

```bash
helm upgrade grafana grafana/grafana -f values.yaml -f datasources-values.yaml -n <your-namespace>
```

5. Verify the Deployment
After deployment, check that Grafana is running and that the data sources are configured correctly. You can view the logs of the Grafana pod to ensure that the data sources were loaded:

```bash
kubectl logs <grafana-pod-name> -n <your-namespace>
```

5. Access the Grafana UI
To access the Grafana UI, you can port-forward as before:

```bash
kubectl port-forward svc/grafana -n <your-namespace> 3000:80
```

Visit http://localhost:3000 to view and manage your data sources under the "Data Sources" section.

## Additional Notes

Ensure your data source configurations are correctly formatted in the ConfigMap. For more details on creating and configuring data sources, refer to the Grafana documentation. You can create multiple ConfigMaps for different data sources and mount them similarly by adjusting the extraVolumes and extraVolumeMounts in additional values files.

## Conclusion

You have successfully configured data sources for your Grafana setup by using a separate values file for extraVolumes and extraVolumeMounts. This setup allows for greater flexibility and management of data source configurations through ConfigMaps.

Feel free to make any further adjustments or ask if you need more modifications!
