# Pathways SRE – Capstone Project

## Infrastructure-as-Code: Deploy and Operate

## Learning Objectives
- Create automations for deploying infrastructure, platform, and application using an Infrastructure-as-Code approach.
- Learn how to configure alert rules and send notifications for critical incidents.
- Simulate operational activities and incidents by intentionally introducing failures, and write operations runbooks to resolve them.
- Write operations runbooks to resolve them.

## Case Description
Build automation that deploys infrastructure hosted in AWS using Infrastructure-as-Code. In the event of a catastrophic infrastructure outage, the automation must be able to rebuild a similarly configured infrastructure from the ground up by simply running it. Once the infrastructure is up, a highly available web app must be deployed on top, complete with monitoring and logging.

Runbooks must be written to resolve common incidents.

All related documentation must be in the given GitHub repository.

## Limitations
- KodeKloud’s AWS playground will be used to deploy the infrastructure. The playground will only be active for 3 hours and will be destroyed automatically after.
- Directly pushing or committing to the GitHub repository is not allowed. Pull requests with review, approval, and merging must be practiced for collaboration purposes.
- On the day of the defense, it is expected that the infrastructure will be freshly re-deployed using the created automation.

## Pre-requisites
### c/o Trainees:
  - Create GitHub accounts using OpsWerks email.
  - Send the list of GitHub accounts to the course admin.
### c/o Course Admins:
- Create a private GitHub repo and give write access to trainees.

## Solution Must-Haves
### Infra-as-code for deploying the infrastructure:
#### *Automation requirements*
  - Must cover the deployment of AWS infrastructure (creation of AWS objects) as well as configuration.
  - Must cover the deployment of a container orchestration platform on top of the infrastructure (Kubernetes).
  - Can be created with combinations of scripts, Jenkins pipelines, or Ansible playbooks.

#### *Infrastructure Requirements*
- A Kubernetes cluster must be deployed for running the web app.
- Splunk must be deployed as the logging solution.
- Prometheus must be deployed as the monitoring solution.
- AlertManager must be deployed as the alerting solution.

### Web App
#### *Deployment*
- The web app of your own choosing must be accessible on the internet via IP or hostname.
- A Jenkins pipeline must be in place for deploying an updated build of the app to the Kubernetes cluster.
#### *Operation*
- Web app logs must be stored in Splunk.
- Web app related telemetry must be scraped by Prometheus.
- Email notification must be in place for any infrastructure-related and web app-related alerts.

### *Version Control: Git and GitHub*
- The given GitHub repository is the main storage for all project info: from the automation codebase, infrastructure configurations, to documentation.
- To show that pull request practices were strictly followed, the main repository’s commit history must only consist of merged pull requests.

### *Ops Simulation*
#### Introduce failures in your infrastructure and application based on (but not limited to) the alerting rules required:
- *Infrastructure failures*
    - Down Kubernetes Control Plane / Worker node.
    - Down EC2 instances.
    - Entire infrastructure is compromised and needs to be rebuilt.
- *Application failures*
    - Web app is down.
    - Too many 4xx and 5xx HTTP errors.
- *Create respective runbooks to properly diagnose, address, and resolve these incidents.*

### Documentation
#### The following must be included:
- *Project documentation*
    - Description of the solution.
    - An architecture diagram of how the solution works, showing the technologies used in the solution stack.
- *Ops Runbook*
    - How to resolve common infra-related outages.
    - How to resolve common app-related outages.
    - Disaster recovery plan for rebuilding infrastructure using the automation.
