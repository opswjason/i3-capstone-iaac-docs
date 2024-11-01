# Restart EC2 Instance

## Purpose

This runbook details the steps required to restart an EC2 instance in the AWS environment.

## Pre-requisites

-   AWS IAM user with sufficient permissions to stop and start EC2 instances.
-   AWS CLI installed and configured with appropriate credentials.

## Steps

Identify the EC2 Instance

-   Log in to the AWS Management Console.
-   Navigate to the EC2 Dashboard.
-   Identify the instance to be restarted. Note its Instance ID and Instance State.

Check Instance Status

-   Ensure the instance is in a state that can be restarted (e.g., it should be in the running state).

Stop the EC2 Instance

-   Use AWS CLI to stop the instance:  
      
    aws ec2 stop-instances --instance-ids <instance-id>
-   for the instance to reach the "stopped" state.

Start the EC2 Instance

-   Use AWS CLI to start the instance:  
      
    aws ec2 start-instances --instance-ids <instance-id>
-   for the instance to reach the "running" state.

Verify the Instance State

-   Ensure the instance is back to the "running" state.
-   Check that all services are up and running on the instance.

Notifications

-   Notify the relevant team members or stakeholders that the EC2 instance has been restarted.

## Post-conditions

-   The EC2 instance should be in the running state.
-   Services hosted on the instance should be operational.

## Troubleshooting

-   If the instance does not stop or start as expected, check for AWS service issues or IAM permission issues.
-   Review instance logs and metrics in the AWS Management Console for any errors or unusual activity.