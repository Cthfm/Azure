# Bicep File Structure

### **Bicep File Structure**

A Bicep file is composed of several key elements, each serving a distinct purpose in resource deployment:​

* **Metadata (`metadata`)**: Provides supplementary information about the Bicep file, such as descriptions or versioning details.​
* **Target Scope (`targetScope`)**: Defines the deployment scope, indicating whether the resources are deployed at the resource group, subscription, management group, or tenant level.​
* **Parameters (`param`)**: Allow customization of deployments by accepting input values during deployment.​
* **Variables (`var`)**: Store computed values or constants to simplify expressions within the Bicep file.​
* **Resources (`resource`)**: Declare the Azure resources to be deployed, specifying their types, properties, and configurations.​
* **Modules (`module`)**: Encapsulate reusable Bicep code, enabling modularization and better organization of complex deployments.​
* **Outputs (`output`)**: Define values to be returned after deployment, which can be used for subsequent operations or referenced in other deployments.​

### **Bicep Syntax Elements**

#### **Metadata**

The `metadata` keyword is used to add descriptive information to your Bicep file. This can include details like the purpose of the file or version information.​

```bicep
metadata description = 'Deploys a storage account and a web app'
```

#### **Target Scope**

The `targetScope` keyword specifies the level at which the deployment is executed. The default scope is `resourceGroup`. Other valid scopes include `subscription`, `managementGroup`, and `tenant`.​

```bicep
targetScope = 'resourceGroup'
```

#### **Parameters**

Parameters allow you to pass values into the Bicep file during deployment, making your templates more flexible and reusable.​

```bicep
@description('The prefix to use for the storage account name.')
@minLength(3)
@maxLength(11)
param storagePrefix string
```

In this example, the `storagePrefix` parameter is defined with a description and length constraints.​

#### **Variables**

Variables store values that are derived from parameters or computed expressions, simplifying complex expressions within your Bicep file.​

```bicep
var uniqueStorageName = '${storagePrefix}${uniqueString(resourceGroup().id)}'
```

Here, `uniqueStorageName` combines the `storagePrefix` parameter with a unique string based on the resource group ID.​

#### **Resources**

The `resource` keyword is used to declare Azure resources to be deployed. Each resource declaration includes a symbolic name, resource type with API version, and a set of properties.​

```bicep
resource storageAccount 'Microsoft.Storage/storageAccounts@2023-04-01' = {
  name: uniqueStorageName
  location: location
  sku: {
    name: storageSKU
  }
  kind: 'StorageV2'
  properties: {
    supportsHttpsTrafficOnly: true
  }
}
```

This example defines a storage account resource with specific configurations.​

#### **Modules**

Modules enable you to encapsulate and reuse Bicep code across different deployments, promoting modularity and maintainability.​

```bicep
bicepCopyEditmodule webModule './webApp.bicep' = {
  name: 'webDeploy'
  params: {
    skuName: 'S1'
    location: location
  }
}
```

In this snippet, the `webModule` module is invoked, passing parameters to configure its deployment.​

#### **Outputs**

Outputs define values that are returned after the deployment is complete, which can be useful for retrieving resource properties or passing information to other deployments.​

```bicep
output storageEndpoint object = storageAccount.properties.primaryEndpoints
```

This output returns the primary endpoints of the deployed storage account.​

### **Decorators**

Decorators in Bicep are annotations that provide additional information or constraints for parameters, variables, resources, modules, outputs, functions, and user-defined data types. They are prefixed with the `@` symbol and placed above the declaration they modify.​

Common decorators include:​

* `@description()`: Adds a description to the element.​
* `@minLength()`: Specifies the minimum length for strings or arrays.​
* `@maxLength()`: Specifies the maximum length for strings or arrays.​
* `@allowed()`: Defines an allowed set of values for a parameter.​
* `@secure()`: Marks a parameter as secure, ensuring its value isn't exposed in deployment outputs or logs.​

For a comprehensive list of decorators and their usage, refer to the [Bicep file structure and syntax documentation](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/file).



