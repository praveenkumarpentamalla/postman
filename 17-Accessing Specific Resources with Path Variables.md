# **Chapter 17: Accessing Specific Resources with Path Variables**

## **17.1 Beyond Lists: Retrieving a Single Resource**

APIs often provide two ways to access data: a list of resources (e.g., `/products`) and a way to access a single, specific resource. To get detailed information about one specific item, you must use its unique identifier in the API request.

## **17.2 Path Variables vs. Query Parameters**

This introduces a new concept: the **path variable** (or path parameter).

*   **Query Parameter:** Appended to the URL after a `?` (e.g., `?category=dairy`). Used for **filtering, sorting, or optional** instructions on a collection endpoint.
*   **Path Variable:** Embedded **directly into the URL path** itself (e.g., `/products/4643`). Used to **identify a specific, unique resource** from a collection.

**Visual Difference:**
*   Path Variable URL: `https://api.example.com/products/4643`
*   Query Parameter URL: `https://api.example.com/products?category=dairy`

## **17.3 Constructing a Request with a Path Variable**

**Step-by-Step Guide:**

1.  **Find the Endpoint:** The API documentation specifies the endpoint for retrieving a single product: `/products/{productId}`. The curly braces `{}` indicate a placeholder for a path variable.
2.  **Duplicate a Request:** A efficient way to start is to duplicate an existing request (e.g., "Get All Products") and modify it.
3.  **Update the URL:** Replace the endpoint path with the one from the documentation. Postman will automatically detect the `{productId}` syntax and create a **"Path Variables"** section in the Params tab.
4.  **Provide the Value:** Obtain a valid product `id` from the response of the "Get All Products" request. Enter this numeric ID as the value for the `productId` path variable in the designated panel.
5.  **Send the Request:** Execute the request. A successful call (200 OK) will return a detailed JSON object for that single product, containing more fields (e.g., `price`, `inStock`, `manufacturer`) than the list view.

## **17.4 How Path Variables Work**

*   The `{productId}` notation in the URL is a **placeholder** for Postman's UI. When the request is sent, Postman replaces this placeholder with the value you provided, forming the final URL (e.g., `/products/4643`).
*   The path variable name itself (`productId`) is **not sent to the server**; only its value becomes part of the path.
*   This is functionally identical to manually typing `/products/4643` in the URL bar, but the Path Variables panel provides a more manageable and error-proof interface.

## **17.5 Error Handling: 404 Not Found**

If you provide an ID for a resource that does not exist (e.g., `/products/5000`), the API will return a **404 Not Found** status code. This is the standard HTTP response for a request aimed at a resource that the server cannot locate.

## **17.6 Common Mistake: Using the Wrong Parameter Type**

A common error is trying to use a path variable as a query parameter. For example, sending a request to `/products?productId=4643` will **not** work. The server for the `/products` endpoint is not designed to handle a `productId` query parameter; it expects the ID to be part of the path itself at the `/products/{id}` endpoint.

***
### **Key Concepts**

*   **Path Variable (Path Parameter):** A variable whose value is set directly in the URL path of an endpoint to identify a specific resource.
*   **404 Not Found:** An HTTP status code indicating that the server could not find the resource requested by the client.
*   **Resource Identifier:** A unique value (usually an ID or a slug) that pinpoints a single resource within a collection.

***
### **Key Takeaways**

*   Use **path variables** to retrieve details about a **single, specific resource**.
*   Use **query parameters** to **filter or modify** a list of resources.
*   **Path variables are part of the endpoint path**; query parameters are appended after a `?`.
*   Postman's **Path Variables** panel provides a user-friendly way to manage values that need to be inserted into the URL path.
*   A **404 error** means the specific resource with the provided identifier does not exist on the server.
*   Always use the **endpoint and parameter type** specified in the API documentation.
