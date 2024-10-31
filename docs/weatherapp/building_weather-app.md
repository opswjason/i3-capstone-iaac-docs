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
