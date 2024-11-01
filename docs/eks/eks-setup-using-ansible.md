J eto pala yung readme ko
# Automated EKS Cluster setup with Ansible Guide
 
This README demonstrates the deployment of a Private EKS Cluster with High Availability using Ansible and Amazon Cloudformation.
 
## Prerequisites
- **Ansible**: Make sure you have Ansible installed on your local machine.
- **AWS Access Key**: This is your AWS credentials which consists of Access Key ID and a Secret Access Key, that allow you to authenticate and interact with AWS services
- **Python**: Python is need in order to run Ansible. Make sure to install it.
 
## Installation
 
1. Clone the repository:
   ```bash
   git clone <repository_url>
   cd <repository_name>
   ```
2. Navigate to the ansible directory:
   ```bash
   cd ansible
   ```
## EKS Cluster Setup with Ansible
 
### To create the EKS cluster, execute the following Ansible playbook:
   ```bash
   ansible-playbook deploy_HAcluster.yml
   ```
 
### After the EKS cluster has been created, configure the cluster to join the Worker Nodes to the cluster:
   ```bash
   ansible-playbook -i inventory/inventory.ini configure_HAcluster.yml
   ```
 
### Finally, test the EKS cluster by deploying pods to the cluster:
   ```bash
   ansible-playbook -i inventory/inventory.ini test_HAcluster.yml
   ```
## AWS Templates
 
The aws/templates directory contains CloudFormation templates for setting up the necessary AWS resources:
- **bastion.yml**: Provisions a Bastion host for secure access.
- **eks.yml**:eks.yml: Creates the EKS cluster.
- **network.yml**:network.yml: Configures networking resources like VPC and subnets.
- **roles.yml**:roles.yml: Defines IAM roles for the EKS cluster.
 
## Testing
 
When the cluster has been created, you may test your setup. First is to ssh to your Bastion-Host and run the following command to verify if have access to the cluster and the Nodes are joined in your cluster:
  ```bash
   kubectl get node
   ```
 