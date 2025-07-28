# API Endpoint Specification: [Endpoint Name]

## 1. Endpoint
*Specify the HTTP method and the full URL path.*

-   **Method:** `POST`
-   **Path:** `/api/v1/users`

## 2. Description
*A clear description of what this endpoint does.*

**Example:** "Creates a new user in the system."

## 3. Request
*Detail the parts of the incoming request.*

### 3.1. Headers (if applicable)
| Header          | Type     | Description                        |
| :-------------- | :------- | :--------------------------------- |
| `Authorization` | `String` | Bearer token for authentication.   |
| `Content-Type`  | `String` | Must be `application/json`.        |

### 3.2. Path Parameters (if applicable)
*N/A*

### 3.3. Query Parameters (if applicable)
*N/A*

### 3.4. Request Body
*Provide a description and a JSON schema or example of the request body.*

**Description:** An object containing the new user's information.
**Schema:**
```json
{
  "type": "object",
  "properties": {
    "email": {
      "type": "string",
      "format": "email",
      "description": "The user's unique email address."
    },
    "name": {
      "type": "string",
      "description": "The user's full name."
    },
    "password": {
      "type": "string",
      "minLength": 8,
      "description": "The user's password."
    }
  },
  "required": ["email", "name", "password"]
}
