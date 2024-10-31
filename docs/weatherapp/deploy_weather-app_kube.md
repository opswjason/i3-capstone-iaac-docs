## Weather App Helm Chart

This section provides instructions on how to deploy the Weather App using a Helm chart. The Weather App is a simple application that provides weather data based on user input.

## Prerequisites

1. Kubernetes cluster up and running.
2. Helm installed on your local machine.
3. Access to the Docker registry where the weather app image is stored.

## Deployment Steps

1. Add the Helm Chart Repository
If you have not already added the repository for the Weather App, do so by running:

```bash
helm repo add weather-app-repo <repository-url>
helm repo update
```

2. Configure the Values
Before deploying the Helm chart, you need to configure a few important variables. You can create a values.yaml file to specify these settings. Below are the variables you need to configure:

```yaml
docker:
  registry64: "<your-docker-registry-url>"  # URL of the Docker registry where the weather app image is stored.

apikey: "<your-api-key>"  # API key for accessing weather data.

metrics:
  user: "<your-metrics-username>"  # Username for Basic Auth for the "/metrics" endpoint.
  password: "<your-metrics-password>"  # Password for Basic Auth for the "/metrics" endpoint.
```

Make sure to replace the placeholder values with your actual configuration.

3. Install the Helm Chart
To deploy the Weather App using your customized values.yaml, run the following command:

```bash
helm install weather-app weather-app-repo/weather-app -f values.yaml
```

4. Verify the Deployment
After installation, you can check the status of your deployment:

```bash
kubectl get all -l app=weather-app
```

5. Access the Weather App
Depending on your Kubernetes setup, you may need to expose the service to access the Weather App. You can use kubectl port-forward or configure an Ingress resource.

6. Update the Deployment
If you need to update any configurations or the Docker image, modify your values.yaml file and run:

```bash
helm upgrade weather-app weather-app-repo/weather-app -f values.yaml
```

7. Uninstall the Helm Chart
To uninstall the Weather App, run:

```bash
helm uninstall weather-app
```

## Conclusion

You have successfully deployed the Weather App using the Helm chart. Make sure to monitor the application and adjust the configurations as needed. For any issues, consult the logs or reach out for support.

Happy weather forecasting! 🌤️