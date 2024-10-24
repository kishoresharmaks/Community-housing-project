# API Documentation Guidelines

## 1. API Names
API names should be descriptive and reflect the purpose of the API. It's best to follow a clear and consistent naming pattern.

**Examples:**
- `GetUserDetails`: Retrieves user information
- `CreateOrder`: Creates a new order in the system
- `UpdateProfile`: Updates user profile information

## 2. API Endpoints
API endpoints represent the URLs to access the resources. They should follow standard practices such as RESTful conventions.

**Format:**  
`[HTTP Method] /[baseURL]/[resource]/[optional-id]`

**Examples:**
- `GET /api/v1/users/{id}` – Retrieves a user by ID
- `POST /api/v1/orders` – Creates a new order
- `PUT /api/v1/users/{id}` – Updates a user's details
- `DELETE /api/v1/products/{id}` – Deletes a product by ID

## 3. API Naming Conventions
- **Use nouns for resources:** API endpoints should represent objects or resources (e.g., `/users`, `/orders`)
- **Use HTTP verbs for actions:**
  - `GET` for retrieving data
  - `POST` for creating data
  - `PUT` or `PATCH` for updating data
  - `DELETE` for removing data
- **Use plural nouns for collections:** e.g., `/users` instead of `/user`
- **Avoid using verbs in URLs:** e.g., use `/users` instead of `/getUsers`

## 4. Request Payload
The request payload refers to the data sent by the client to the API, typically for POST, PUT, or PATCH operations. Document the required fields, data types, and any validation rules.

**Example: POST /api/v1/orders**
```json
{
  "customerId": "12345",      // required, string
  "orderDate": "2024-10-20",  // required, string (YYYY-MM-DD)
  "items": [                  // required, array of objects
    {
      "productId": "A987",    // required, string
      "quantity": 2           // required, integer
    }
  ]
}
```

## 5. Response Payload
The response payload refers to the data returned by the API after processing a request. Typically, responses should include standard HTTP status codes and relevant data.

**Example: Response (200 OK)**
```json
{
  "orderId": "67890",
  "customerId": "12345",
  "orderDate": "2024-10-20",
  "status": "confirmed",
  "items": [
    {
      "productId": "A987",
      "quantity": 2,
      "price": 19.99
    }
  ],
  "totalAmount": 39.98
}
```

**Response (404 Not Found)**
```json
{
  "error": "Order not found",
  "status": 404
}
```

## 6. HTTP Status Codes
Always document standard HTTP status codes to describe the success or failure of an API request:

- **200 OK**: The request was successful
- **201 Created**: A new resource has been created
- **400 Bad Request**: The request payload is invalid or missing required fields
- **401 Unauthorized**: Authentication is required
- **404 Not Found**: The requested resource could not be found
- **500 Internal Server Error**: A server-side error occurred
