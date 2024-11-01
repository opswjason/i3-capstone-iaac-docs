# Weather App

In this project we will be using a simple application which we will refer to as "Weather App", an application that provides real-time weather information based on the city/location the user inputs. 

This project utilizes the OpenWeatherMap API to fetch weather data and presents it in a user-friendly interface.

<!-- ## Table of Contents

- [Installation](#installation)
- [Obtaining an API Key](#obtaining-an-api-key)
- [Running with Docker](#running-with-docker) -->

## Obtaining an API Key

1. Go to the OpenWeatherMap website.
2. Sign up for a free account if you don’t have one.
3. After logging in, navigate to the API section and generate an API key.

## Running with Docker

To run the application using Docker, you can pass your API key as an environment variable:

1. Build the Docker image:
```bash
    docker build -t weather-app .
```
2. Run the Docker container, replacing your_api_key_here with your actual API key, and set your_metric_user_here and your_metric_password_here with your actual username and password.

    This configuration allows Prometheus or exporters to access the metrics URL:
```bash
    docker run -d \
        -e API_KEY=your_api_key_here \
        -e METRIC_USER=your_metric_user_here\
        -e METRIC_PASSWORD=your_metric_password_here\
        -p 3000:3000 weather-app
```
3. Open your browser and go to http://localhost:8080 to access the app.

## Health Check

The web application includes a health check endpoint to monitor its status. This is useful for ensuring that the application is running smoothly and can help with automated monitoring systems.

### Endpoint

- **URL:** `/health`
- **Method:** GET

### Response

When you send a GET request to the `/health` endpoint, the application will respond with a JSON object containing the current health status. 

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