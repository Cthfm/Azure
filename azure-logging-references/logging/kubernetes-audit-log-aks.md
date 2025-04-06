# Kubernetes Audit Log (AKS)

## What Are Kubernetes Audit Logs?

Kubernetes Audit Logs track all requests made to the Kubernetes API Server. They record what happened, when it happened, who made the request, and what the outcome was. Think of them as a security camera watching everything that hits your Kubernetes API.

***

### Structure of a Kubernetes Audit Log Event

Each audit log event is a JSON object with several standard fields.

Here’s the main structure:

```json
{
  "kind": "Event",
  "apiVersion": "audit.k8s.io/v1",
  "level": "RequestResponse",
  "timestamp": "2025-04-05T10:20:30Z",
  "auditID": "abc123-456def-789ghi",
  "stage": "ResponseComplete",
  "requestURI": "/api/v1/namespaces/default/pods",
  "verb": "create",
  "user": {
    "username": "system:serviceaccount:default:myserviceaccount",
    "groups": ["system:serviceaccounts", "system:authenticated"]
  },
  "sourceIPs": ["10.0.0.1"],
  "userAgent": "kubectl/v1.26.0 (linux/amd64)",
  "objectRef": {
    "resource": "pods",
    "namespace": "default",
    "name": "my-pod"
  },
  "responseStatus": {
    "metadata": {},
    "code": 201
  },
  "requestObject": { },
  "responseObject": { },
  "annotations": {
    "authorization.k8s.io/decision": "allow",
    "authorization.k8s.io/reason": "RBAC: allowed by RoleBinding"
  }
}
```

***

### Key Fields You Should Know

| Field              | What It Means                                                                           |
| ------------------ | --------------------------------------------------------------------------------------- |
| **kind**           | Always `Event` for audit logs                                                           |
| **apiVersion**     | Audit log schema version (e.g., `audit.k8s.io/v1`)                                      |
| **level**          | Level of detail: `Metadata`, `Request`, `RequestResponse`                               |
| **timestamp**      | When the request happened                                                               |
| **auditID**        | Unique ID for tracking this event                                                       |
| **stage**          | Stage of the request: `RequestReceived`, `ResponseStarted`, `ResponseComplete`, `Panic` |
| **requestURI**     | API endpoint that was called                                                            |
| **verb**           | Action performed: `get`, `list`, `create`, `delete`, `patch`, etc.                      |
| **user**           | Identity of the user or service account making the request                              |
| **sourceIPs**      | IP addresses of the client                                                              |
| **userAgent**      | Client info (kubectl, dashboard, app, etc.)                                             |
| **objectRef**      | Which object (e.g., Pod, Service) was accessed                                          |
| **responseStatus** | Status code (e.g., `200 OK`, `201 Created`, `403 Forbidden`)                            |
| **requestObject**  | The full object sent in the request (optional based on `level`)                         |
| **responseObject** | The full object returned in the response (optional based on `level`)                    |
| **annotations**    | Extra info like why the request was allowed or denied (e.g., RBAC decision)             |

### Understanding Level

The level field controls how much detail the audit log has:

| Level               | What is Captured                            |
| ------------------- | ------------------------------------------- |
| **Metadata**        | Only metadata about the request (no body)   |
| **Request**         | Metadata + request body                     |
| **RequestResponse** | Metadata + request body + response body     |
| **None**            | No logging at all (usually not recommended) |

***

### Understanding Stage

The stage tells you how far the request got:

| Stage                | Meaning                       |
| -------------------- | ----------------------------- |
| **RequestReceived**  | API Server got the request    |
| **ResponseStarted**  | Started sending the response  |
| **ResponseComplete** | Finished sending the response |
| **Panic**            | Server crashed while handling |

***

### Example Scenarios You Can Detect in Audit Logs

| Scenario                          | What to Look For                                                      |
| --------------------------------- | --------------------------------------------------------------------- |
| Unauthorized Access Attempt       | `responseStatus.code = 403`                                           |
| Successful Pod Deletion           | `verb = delete` and `resource = pods` and `responseStatus.code = 200` |
| Creating a Secret                 | `verb = create` and `resource = secrets`                              |
| Changing Roles or RoleBindings    | `resource = roles` or `rolebindings`                                  |
| Access from Suspicious IP         | Unrecognized `sourceIPs`                                              |
| Excessive API Calls (Brute Force) | Repeated `requestURI` hits in a short time                            |

***

### Kubernetes Audit Policies

You control what gets logged using an Audit Policy.

A **policy** tells Kubernetes:

* Which users/resources to log
* What level (Metadata, Request, etc.)
* What stages (RequestReceived, ResponseComplete, etc.)

You define the audit policy in YAML format and pass it to the API Server using the `--audit-policy-file` flag.

Example of a simple policy:

```yaml
yamlCopyEditapiVersion: audit.k8s.io/v1
kind: Policy
rules:
- level: RequestResponse
  verbs: ["create", "update", "delete"]
  resources:
  - group: ""
    resources: ["pods", "services"]
```

This policy logs all create, update, and delete actions on pods and services with full request and response data.

### Common Verbs&#x20;

| Verb            | Meaning                               | Example Use Case                  | Threat Hunting Tip                                                         |
| --------------- | ------------------------------------- | --------------------------------- | -------------------------------------------------------------------------- |
| **get**         | Read a single resource                | `kubectl get pod mypod`           | Very common. Look for `get` on `secrets` by unusual users.                 |
| **list**        | Read multiple resources               | `kubectl get pods`                | Normal in day-to-day operations.                                           |
| **watch**       | Watch for changes                     | Used by apps/controllers.         | Attackers might watch pods/nodes for recon.                                |
| **create**      | Create a new resource                 | `kubectl create deployment myapp` | 🚩 Critical to monitor — who’s creating new deployments/pods/roles?        |
| **delete**      | Delete a resource                     | `kubectl delete pod mypod`        | 🚩 Unexpected deletes can be destructive or hide attacks.                  |
| **update**      | Update a resource                     | `kubectl edit deployment myapp`   | 🚩 Watch updates to sensitive resources like RBAC or Secrets.              |
| **patch**       | Partial update of a resource          | `kubectl patch deployment myapp`  | 🚩 Sometimes used by attackers to escalate privileges quietly.             |
| **proxy**       | Access services through API server    | `kubectl proxy`                   | 🚩 Watch proxy use — it could mean someone is tunneling into your cluster. |
| **bind**        | Bind a role to a user/service account | Rare outside of RBAC setup        | 🚩 Unauthorized `bind` could mean RBAC abuse.                              |
| **impersonate** | Act as another user/service account   | Service Meshes sometimes do this  | 🚩 Rare — watch carefully for impersonations.                              |

***

### In Summary

| Concept         | Key Point                                                         |
| --------------- | ----------------------------------------------------------------- |
| Audit Log Event | JSON object describing one API request                            |
| Key Fields      | `timestamp`, `user`, `verb`, `objectRef`, `responseStatus`, etc.  |
| Levels          | `Metadata`, `Request`, `RequestResponse`                          |
| Stages          | `RequestReceived`, `ResponseStarted`, `ResponseComplete`, `Panic` |
| Policy          | Defines what is logged and at what detail level                   |
| Use Cases       | Monitor security, investigate incidents, detect threats           |
