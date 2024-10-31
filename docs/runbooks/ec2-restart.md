# Operation Runbook: Restart EC2 Instance

## Purpose
This runbook details the steps required to restart an EC2 instance in the AWS environment.

## Pre-requisites
- AWS IAM user with sufficient permissions to stop and start EC2 instances.
- AWS CLI installed and configured with appropriate credentials.

## Steps

### Identify the EC2 Instance
1. Log in to the AWS Management Console.
2. Navigate to the **EC2 Dashboard**.
3. Identify the instance to be restarted. Note its **Instance ID** and **Instance State**.

### Check Instance Status
1. Ensure the instance is in a state that can be restarted (e.g., it should be in the running state).

### Stop the EC2 Instance
1. Use AWS CLI to stop the instance:
   ```shell
   aws ec2 stop-instances --instance-ids i-1234567890abcdef0
