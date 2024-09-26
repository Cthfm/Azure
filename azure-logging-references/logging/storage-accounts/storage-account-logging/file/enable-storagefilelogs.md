# Enable StorageFileLogs

## Azure Portal

1. From the default portal page select Storage Accounts.
2. Select the specific Storage Account.
3. Click the Diagnostics settings under the Monitoring section in the left column.
4. Select the 'file' tab indented below the storage account.
5. Click '+ Add diagnostic setting'.
6. Select StorageRead, StorageWrite and StorageDelete options under the Logging section to enable Storage Logging for Blob service.
7. Select a destination for your logs to be sent to. From Azure CLI Use the below command to enable the Storage Logging for file service.&#x20;

&#x20;