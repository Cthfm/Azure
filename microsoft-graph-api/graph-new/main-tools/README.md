# Main Tools

## **Main Tools You Should Know**

| Tool                     | Purpose                                    | Best For                                                   |
| ------------------------ | ------------------------------------------ | ---------------------------------------------------------- |
| **Graph Explorer**       | Web-based testing tool                     | Quick testing without setup.                               |
| **Postman**              | API client for testing and automating APIs | More advanced manual testing.                              |
| **PowerShell**           | Scripting with Graph                       | Admin automation.                                          |
| **Microsoft Graph SDKs** | Code libraries for different languages     | Building real applications (Python, C#, PowerShell, etc.). |

***

### 1. **Graph Explorer**

Graph Explorer is the quickest way to test Graph API without writing any code.

#### How to Use:

1. Go to 👉 [https://developer.microsoft.com/en-us/graph/graph-explorer](https://developer.microsoft.com/en-us/graph/graph-explorer)
2. Click **Sign In**.
3.  Run a query like:

    ```
    GET https://graph.microsoft.com/v1.0/me
    ```

#### Features:

* Pre-built sample queries.
* Shows API response instantly.
* Automatically handles authentication.

***

### 2. **Postman**

Postman is a popular tool for working with APIs.\
It gives you more control over headers, body data, and authentication.

#### Setting Up Postman for Graph:

1. Download and Install Postman → https://www.postman.com/downloads/
2. Create a New Request:
   * Method: `GET`
   * URL: `https://graph.microsoft.com/v1.0/me`
   *   Headers:

       ```http
       Authorization: Bearer {access_token}
       ```

#### Bonus:

* Microsoft provides a Microsoft Graph Postman Collection to help you get started faster!
  * [Microsoft Graph Postman Collection](https://learn.microsoft.com/en-us/graph/use-postman)

***

### 3. **PowerShell**

You can also interact with Graph API using PowerShell, which is great for scripting automation.

There now one major module:

| Module            | Description                                          |
| ----------------- | ---------------------------------------------------- |
| `Microsoft.Graph` | New official Graph SDK for PowerShell (recommended). |

#### Install the Microsoft Graph PowerShell Module:

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
```

#### Example: Connect and Query

```powershell
Connect-MgGraph -Scopes "User.Read.All"
Get-MgUser 
```

{% hint style="warning" %}
Tip: The first time you run it; it will open a login window for permissions!
{% endhint %}

***

### 4. **Microsoft Graph SDKs**

If you're building applications or automated scripts, using an SDK saves you a ton of work.

| Language           | SDK                                          |
| ------------------ | -------------------------------------------- |
| C#                 | `Microsoft.Graph` NuGet Package              |
| Python             | `msgraph-core` and `azure-identity` packages |
| JavaScript/Node.js | `@microsoft/microsoft-graph-client`          |

#### Example: Python SDK

Install the libraries:

```bash
pip install msgraph-core azure-identity
```

Example code:

```python
from azure.identity import ClientSecretCredential
from msgraph_core import GraphClient

tenant_id = 'your-tenant-id'
client_id = 'your-client-id'
client_secret = 'your-client-secret'

credential = ClientSecretCredential(tenant_id, client_id, client_secret)
client = GraphClient(credential)

response = client.get('/me')
print(response.json())
```

### &#x20;**Summary**

* **Graph Explorer** is the easiest place to get started quickly.
* **Postman** gives you complete control for testing APIs.
* **PowerShell** lets you automate admin tasks with scripts.
* **SDKs** make it easy to integrate Microsoft Graph into real apps.
