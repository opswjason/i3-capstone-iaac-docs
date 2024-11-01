
# Velero Backup for EKS

## Purpose

This runbook details the steps required to perform backups using Velero.

## Prerequisites

-   Velero installed and configured in your EKS cluster.
    
-   AWS CLI installed and configured with appropriate credentials.
    
-   BackupStorageLocation and VolumeSnapshotLocation resources configured in Velero.
    

## Steps

**1. Identify Backup Storage Location**

-   Ensure that a BackupStorageLocation is configured for AWS S3 or your desired storage provider (Azure, GCP etc).
    
-   Verify the configuration using:
    

    
    ```
    velero backup-location get
    
    ```
    

**2. Identify Volume Snapshot Location**

-   Ensure that a VolumeSnapshotLocation is configured for your desired snapshot provider.
    
-   Verify the configuration using:
    
    ```
    velero snapshot-location get
    
    ```

**3. Create a Backup**

-   Create a backup using the Velero CLI:
    
    ```
    velero backup create <backup-name> --include-namespaces=<namespace> --wait
    
    ```
    
-   Replace `<backup-name>`  with your desired backup name and `<namespace>`  with the namespace you want to back up.
    

**4. Monitor Backup Progress**

-   Monitor the progress of the backup using:
    
    ```
    velero backup describe <backup-name>
    
    ```

**5. Verify Backup Completion**

-   Once the backup is complete, verify the status using:
    
    ```
    velero backup describe <backup-name>
    
    ```
    
-   Check the status of the backup and ensure it is marked as `Completed`.
    

**6. Schedule Backups (Optional)**

-   If you want to schedule regular backups, create a schedule using:
    

    ```
    velero schedule create <schedule-name> --schedule=<cron-expression> --include-namespaces=<namespace>
    
    ```
    
-   Replace `<schedule-name>`  with your desired schedule name, `<cron-expression>`  with the appropriate cron expression, and `<namespace>`  with the namespace to back up.
    

**7. Restore from Backup**

-   To restore from a backup, use the Velero CLI:
    

    
    ```
    velero restore create <restore-name> --from-backup=<backup-name> --wait
    
    ```
    
-   Replace `<restore-name>`  with your desired restore name and `<backup-name>`  with the name of the backup to restore from.
    

**8. Verify Restore Completion**

-   Monitor the progress of the restore using:
    

    
    ```
    velero restore describe <restore-name>
    
    ```
    
-   Check the status of the restore and ensure it is marked as `Completed`.
    
## Post-conditions

-   The backup should be successfully created and stored in the configured storage location.
    
-   The restore should be successfully completed, and the data should be available in the specified namespace.
    

## Troubleshooting

-   If backups fail, check the Velero logs for errors using:
    
   
    ```
    kubectl logs -n velero <velero-pod-name>
    
    ```
    
-   Ensure that the BackupStorageLocation and VolumeSnapshotLocation resources are correctly configured.
    
-   Verify that the storage provider credentials are valid and have the necessary permissions.