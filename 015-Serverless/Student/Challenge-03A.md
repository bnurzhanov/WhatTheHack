# Challenge 03 Accelerator - Create Resources

[< Previous Challenge](./Challenge-02.md) - **[Home](../README.md)** - [Next Challenge >](./Challenge-04.md)

## Introduction

As per the diagram below, the TollBooth application is composed of multiple Azure "Platform As A Service" (aka PaaS) services including:
- Azure Functions
- Cosmos DB
- Azure Event Grid
- Azure Blob Storage
- Azure Key Vault
- Azure Computer Vision API (aka "Azure AI Vision Service" as of 2024)

![The Solution diagram is described in the text following this diagram.](../images/preferred-solution.png 'Solution diagram')

The TollBooth application's Azure Function source code is just one piece of the overall solution. That code depends on each of these services being deployed and configured properly.

If your coach has directed you to this page, give them a HUGE "Thank you"!  The Azure PaaS resources that will support the TollBooth application have already been pre-deployed for you to a lab environment.

Normally, you must provision these resources in Azure yourself before you can start developing the solution. 

## Description

In this challenge, you will explore the resources that have been pre-deployed in your Azure environment.  Don't worry, we still left a few tasks for you to figure out.

Each of the Azure PaaS services have secrets that the Azure Function application code needs to access those services. The *easy* thing would be to just put those secrets in the source code so the functions can access each service. However, the *easy* way is rarely the **CORRECT** way to do things.

**NOTE:** Placing secrets in plain-text code files could result in your company or organization being in the news headlines for all the wrong reasons.

It is a best practice to store secrets in a key management service like [Azure Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/general/basic-concepts), and then have the application request those secret values from Key Vault on demand as needed. This solution has multiple benefits, including:
- The secrets are not placed in plain text code files where they can be compromised (by committing them to a Git repository)
- The application developer does not need to know or see the secret values
- The secrets can be managed by an operations team independently of application developers

The secrets for each of the services have already been stored in the Azure Key Vault for you. By default, you will NOT have access to view the secrets (even though you are the owner of your Azure subscription and the resources deployed in it).

Your challenges are to:
- Figure out how to grant yourself access to view the secrets in the Key Vault
- The Azure Functions each have an managed identity that have already been granted access to the Key Vault for you. Figure out where that permission is set.
- Validate each of secrets listed in the table below is populated with a value

    |                          |                                                                                                                                                             |
    | ------------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------: |
    | **Secret Name**      |                                                                          **Value**                                                                          |
    | `computerVisionApiKey`     |                                                                   Computer Vision API key                                                                   |
    | `eventGridTopicKey`        |                                                                 Event Grid Topic access key                                                                 |
    | `cosmosDBAuthorizationKey` |                                                                    Cosmos DB Primary Key                                                                    |
    | `cosmosDBConnectionString` |                                                                    Cosmos DB Primary Connection String                                                                 |
    | `blobStorageConnection`    |                                                               Blob storage connection string                                                                |

**HINT:** Understand the Azure RBAC (Role Based Access Control) role "KeyVault Administrator", which is more privileged than the "KeyVault Secrets User" role that the functions will use.

## Success Criteria

1. Validate that you have 13 resources in your resource group in the same region (This includes the 2 storage accounts associated to your function apps). 
2. Ensure you have permissions to read/write the Key Vault Secrets using the Portal
3. Demonstrate to your coach that you understand how/where the Azure Function Apps have been granted access to the Key Vault.

## Learning Resources

- [Creating a storage account (blob hot tier)](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account?toc=%2fazure%2fstorage%2fblobs%2ftoc.json%23create-a-storage-account)
- [Creating a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal)
- [Concepts in Event Grid](https://docs.microsoft.com/azure/event-grid/concepts)
- [Creating an Azure Cosmos DB account](https://docs.microsoft.com/azure/cosmos-db/manage-account)
- [Key Vault Secret Identifiers](https://docs.microsoft.com/azure/key-vault/about-keys-secrets-and-certificates)
- [Configure Azure Functions and KeyVault to work together](https://docs.microsoft.com/azure/app-service/app-service-key-vault-references?tabs=azure-cli#granting-your-app-access-to-key-vault)
- [Key Vault roles for RBAC](https://learn.microsoft.com/en-us/azure/key-vault/general/rbac-guide?tabs=azure-cli#azure-built-in-roles-for-key-vault-data-plane-operations)
