# Enable Queue Logging

## Instructions to Enabling Queue Logging

From Azure Portal

1. Go to Storage Accounts.
2. Select the specific Storage Account.
3. Click the Diagnostics settings under the Monitoring section in the left column.
4. Select the queue tab indented below the storage account.
5. Click + Add diagnostic setting.
6. Select StorageRead, StorageWrite and StorageDelete options under the Logs section to enable Storage Logging for Queue service.
7. Select a destination for your logs to be sent to. From Azure CLI Use the below command to enable the Storage Logging for Queue service.&#x20;

