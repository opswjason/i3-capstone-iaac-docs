# Prometheus Pod Configuration

This guide will help you configure your Prometheus pod by passing a custom `prometheus.yml` configuration file using a values file.

## Overview

In this setup, we will use a Helm chart to deploy Prometheus. The main configuration for Prometheus is specified in a values file, where the configuration keys are nested under the `config` key. All keys under `config` will be treated as part of the `prometheus.yml` file.

## Prerequisites

- Helm installed and configured
- Kubernetes cluster set up
- Access to the Kubernetes namespace where Prometheus will be deployed

## Steps to Configure Prometheus

1. **Create Your Values File**

   Create a yaml file. This file will contain the configuration settings for Prometheus. Here’s an example of how to structure it:

   ```yaml
   config:
     global:
       scrape_interval: 15s
       evaluation_interval: 15s
     scrape_configs:
       - job_name: 'kubernetes'
         kubernetes_sd_configs:
           - role: pod

In this example, we define global settings and a scrape configuration for Kubernetes.


## Additional Notes

You can extend the configuration in values.yaml by adding more keys under the config section as needed for your specific use case.
For more complex configurations, refer to the Prometheus documentation for a complete list of available options.

## Conclusion

You have successfully configured a Prometheus pod by passing a custom prometheus.yml file through a values file. You can now monitor your applications and services effectively.
For further customization and deployment options, consult the Helm chart documentation or the Prometheus official docs.

Feel free to modify the examples and instructions to fit your specific use case!
