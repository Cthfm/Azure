# Graph API Requests

## **How Microsoft Graph API Requests Work**

Every Graph API call has a basic structure:

```
cssCopyEdithttps://graph.microsoft.com/{version}/{resource}?[query_parameters]
```

| Part                 | Example                       | Description                                    |
| -------------------- | ----------------------------- | ---------------------------------------------- |
| **Base URL**         | `https://graph.microsoft.com` | Always the same.                               |
| **Version**          | `v1.0` or `beta`              | v1.0 = stable; beta = in development.          |
| **Resource**         | `/users`, `/me`, `/groups`    | The Microsoft 365 resource you want to access. |
| **Query Parameters** | `$filter`, `$select`, etc.    | Control what data you get back.                |

Example:

```http
GET https://graph.microsoft.com/v1.0/users
```

***

## **Important HTTP Methods**

| Method     | Purpose              | Example                       |
| ---------- | -------------------- | ----------------------------- |
| **GET**    | Read data            | Fetch user profiles.          |
| **POST**   | Create new data      | Create a new user.            |
| **PATCH**  | Update existing data | Update a user’s phone number. |
| **DELETE** | Remove data          | Delete a user or group.       |

These methods map directly to **CRUD** operations (Create, Read, Update, Delete).

***

## **Common Request Example: Get My Profile**

```http
GET https://graph.microsoft.com/v1.0/me
Authorization: Bearer {access_token}
```

✅ This will return a JSON object with your user details.

***

## **Understanding Query Parameters**

You can make your API requests smarter and faster using OData query parameters.

Here are the most important ones:

***

&#x20;1\. `$select` → Only Get Specific Fields

By default, Graph returns **all fields** for a resource.\
You can use `$select` to **limit** the fields you get back.

Example: Get only displayName and mail for a user.

```http
GET https://graph.microsoft.com/v1.0/me?$select=displayName,mail
```

***

#### 2. `$filter` → Only Get Items Matching a Condition

Use `$filter` to **retrieve only matching records**.

Example: Get users where department = "Sales".

```http
GET https://graph.microsoft.com/v1.0/users?$filter=department eq 'Sales'
```

***

#### 3. `$orderby` → Sort the Results

Sort your results by a field.

Example: Order users by displayName alphabetically.

```http
GET https://graph.microsoft.com/v1.0/users?$orderby=displayName
```

***

#### 🎯 4. `$expand` → Bring in Related Data

Pull related data into one query.

Example: Get a user and their manager details:

```http
httpCopyEditGET https://graph.microsoft.com/v1.0/me?$expand=manager
```

***

## **Combining Query Options**

You can combine multiple options!

Example: Get users in the Sales department, selecting only displayName and mail, ordered by name:

```http
GET https://graph.microsoft.com/v1.0/users?$filter=department eq 'Sales'&$select=displayName,mail&$orderby=displayName
```

***

## **Common Pitfalls**

| Mistake                                        | Problem                                    | Solution                                             |
| ---------------------------------------------- | ------------------------------------------ | ---------------------------------------------------- |
| Forgetting `$` before `select`, `filter`, etc. | API returns an error.                      | Always prefix options with `$`.                      |
| Typos in field names                           | API returns `Invalid filter clause` error. | Double-check field names in the Graph documentation. |
| Not setting correct permissions                | API returns `403 Forbidden`.               | Make sure your app has the right Graph permissions.  |
