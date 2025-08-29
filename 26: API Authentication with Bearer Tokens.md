# **Chapter 26: API Authentication with Bearer Tokens**

## **26.1 The Need for Authentication**

Many API endpoints, especially those that create, modify, or delete data, require **authentication** to identify the client making the request. This ensures security and accountability. Without proper authentication, requests will be rejected with a **401 Unauthorized** error.

## **26.2 The Registration Process**

To obtain access to protected endpoints, you must first register your client with the API to get a credential.

1.  **Find the Registration Endpoint:** The API documentation provides a `POST /api-clients` endpoint for registration.
2.  **Construct the Request:**
    *   **Method:** `POST`
    *   **Body:** A JSON object containing a `clientName` and `clientEmail`. These values identify your application (e.g., "Postman-Test"), not an end-user.
3.  **Interpret the Response:** A successful registration returns a **`201 Created`** status and a JSON response containing a unique **`accessToken`**. This token is your temporary password for all subsequent authenticated requests.

## **26.3 Storing the Access Token**

The access token is sensitive and should be stored securely and reused.
*   **Best Practice:** Save the token as a **collection variable** (e.g., `accessToken`).
*   **Set the Initial Value:** To a placeholder like `"your_access_token_here"` for sharing.
*   **Set the Current Value:** To your actual, private token. This value is not shared when exporting the collection.

## **26.4 Applying Authentication: The Authorization Header**

The standard method for sending an access token is via the **`Authorization`** HTTP header.

*   **Header Format:** `Authorization: Bearer <your_access_token>`
*   **`Bearer`:** This is a keyword indicating the type of authentication being used.
*   **`<your_access_token>`:** The actual token value obtained during registration.

## **26.5 Configuring Authentication in Postman**

Postman provides a dedicated interface to manage authentication, which automatically handles header creation.

**Using the Authorization Tab:**
1.  Navigate to the **Authorization** tab of your request.
2.  Set the **Type** to **"Bearer Token"**.
3.  In the **Token** field, reference your stored variable using the `{{accessToken}}` syntax. This is preferable to hardcoding the token value.
4.  Postman will automatically add the correctly formatted `Authorization` header to the request when it is sent.

## **26.6 Manual Header Configuration (Alternative)**

You can achieve the same result manually by:
1.  Going to the **Headers** tab.
2.  Adding a new key: `Authorization`.
3.  Setting its value to: `Bearer {{accessToken}}`.

## **26.7 Verifying the Request**

Use the **Postman Console** to inspect the raw HTTP request. You should see the `Authorization` header with the `Bearer` prefix and your token value, confirming it was sent correctly.

## **26.8 Outcome**

Once the `Authorization` header is correctly set, the `401 Unauthorized` error should be resolved. The request will then be processed based on its other parameters (e.g., body, path variables), potentially returning new errors (e.g., `400 Bad Request`) that need to be addressed separately.

***
### **Key Concepts**

*   **Authentication:** The process of verifying the identity of a client making an API request.
*   **Access Token:** A string that serves as a credential to access protected API resources. It is obtained through a registration or login process.
*   **Authorization Header:** An HTTP header used to transmit credentials (like an access token) to the server.
*   **Bearer Token:** A common type of authentication where the client simply presents ("bears") the token for access.

***
### **Key Takeaways**

*   Protected API endpoints require an **access token** passed in the **`Authorization: Bearer`** header.
*   **Register your client** using the `POST /api-clients` endpoint to obtain an access token.
*   **Store the access token in a collection variable** for security and reusability.
*   Use Postman's **Authorization tab** (Type: Bearer Token) to easily configure authentication by referencing your variable (`{{accessToken}}`).
*   Always verify the header is being sent correctly using the **Postman Console**.
