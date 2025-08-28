# **Chapter 12: Filtering Data with Query Parameters**

## **12.1 The Purpose of Query Parameters**

APIs often return large datasets. **Query parameters** are a standard HTTP feature that allows clients to filter, sort, and paginate these results directly within the request URL. They are used to refine the data returned by an endpoint without changing the endpoint itself.

## **12.2 Anatomy of a Query Parameter**

Query parameters are appended to the end of a URL after a question mark (`?`). The syntax is:
`?key=value`

*   **Key:** The name of the parameter (e.g., `category`).
*   **Value:** The specific value for that parameter (e.g., `dairy`).
*   **Example:** `https://api.example.com/products?category=dairy`

Multiple parameters are separated by an ampersand (`&`):
`?key1=value1&key2=value2`

## **12.3 Adding Parameters in Postman**

Postman provides a dedicated interface under the **"Params"** tab to manage query parameters easily.

1.  **Navigate to the Params Tab:** Located next to the "Headers" tab in the request composer.
2.  **Add a Parameter:** Enter the **Key** (parameter name) and its corresponding **Value**.
3.  **Observe the URL:** As you type, Postman automatically constructs and displays the full URL with the parameters in the address bar. Parameters can be temporarily disabled using the checkbox next to them without deleting them.

## **12.4 Common Errors and Best Practices**

### **Case Sensitivity**
Computers treat `category` and `Category` as two completely different keys. **Query parameters are case-sensitive.** Always use the exact parameter names and values as specified in the API documentation.

### **Handling Invalid Parameters**
*   **Invalid Value:** If you provide a value the API doesn't recognize (e.g., `category=milk` when only `dairy` is valid), the server will typically return a **400 Bad Request** error with a message explaining the valid options.
*   **Invalid Key:** If you provide a parameter key the API doesn't expect (e.g., `categry=dairy`), the API will usually **ignore it silently** and process the request as if the parameter wasn't there, as most query parameters are optional.

### **Interpreting Responses**
*   **Empty Response:** A successful request (200 OK) with an empty array `[]` in the response body is a valid response. It means the query was understood, but no resources match the given criteria (e.g., `category=x` returns no products).
*   **Always Consult Documentation:** The available parameters, their required/optional status, and their accepted values are **always defined in the API documentation.** Postman is merely the tool for sending them.

## **12.5 How It Works: Client vs. Server**

It is crucial to understand the division of labor:
*   **Postman's Role:** A client tool that helps you **construct and send** the HTTP request with the correct parameters.
*   **The API's Role:** The server **receives** the request, **processes** the query parameters, **filters** the data in its database, and **returns** the matching results. The filtering logic is entirely implemented on the server side.

***
### **Key Concepts**

*   **Query Parameter:** A key-value pair appended to a URL after a `?` used to modify the response from an API endpoint.
*   **400 Bad Request:** An HTTP status code indicating the server could not understand the request due to invalid client input (e.g., an invalid parameter value).
*   **Case Sensitivity:** The property of a system where uppercase and lowercase letters are treated as distinct characters (e.g., `A` ≠ `a`).

***
### **Key Takeaways**

*   Use **query parameters** to filter and customize the data returned by an API endpoint.
*   **Always copy-paste parameter names and values** from the API documentation to avoid case-sensitivity errors.
*   A **400 status code** usually means you provided an invalid parameter value. Check the response body for details.
*   An **empty list `[]` with a 200 status** is a successful response indicating zero results matched your filter.
*   **Postman constructs the request; the API performs the filtering.** Understanding this separation is key to effective debugging.
