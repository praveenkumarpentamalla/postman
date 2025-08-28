# **Chapter 13: API Parameters: Limitations and Documentation**

## **13.1 The Constraint of Defined Parameters**

A common misconception is that any parameter can be added to a request to filter results in a desired way. In reality, an API will only process parameters that it has been explicitly programmed to understand. Adding arbitrary parameters not defined in the API's documentation will have no effect.

## **13.2 The Role of API Documentation**

The API documentation is the contract that defines all possible interactions. It explicitly lists:
*   Which **endpoints** are available.
*   Which **HTTP methods** (GET, POST, etc.) each endpoint accepts.
*   Which **query parameters** each endpoint supports.
*   What **values** are valid for each parameter.

**You cannot use a parameter that is not listed in the documentation.** The API's server-side code is only designed to look for and process the parameters specified in its documentation. All other parameters are silently ignored.

## **13.3 Practical Example: Unsupported Parameters**

In the grocery store API:
*   The `/products` endpoint documentation specifies supported parameters: `category`, `limit`, `page`.
*   Adding a parameter like `name=cabbage` is syntactically correct in the URL, but because the API's backend logic does not include code to handle a `name` parameter, it is disregarded.
*   The API processes the request using only the parameters it recognizes (e.g., `category=fresh%20produce`) and returns the full result set for that category, ignoring the `name` filter entirely.

## **13.4 Key Implication**

The filtering, sorting, and searching capabilities of an API are **determined solely by the server's implementation.** As a client, you are limited to the functionality the API provider has chosen to expose. You cannot create new filters on the fly; you can only use the ones that have been built.

***
### **Key Concepts**

*   **Server-Side Logic:** The code running on the API server that processes requests and determines how parameters are used to query the database and formulate a response.

***
### **Key Takeaways**

*   **An API will only respond to parameters defined in its documentation.** All other parameters are ignored.
*   **The API documentation is the ultimate authority** on what is possible with an API.
*   You cannot invent new parameters or functionality; you can only use the tools the API provider has made available.
*   If you need a specific filter (e.g., search by product name) that isn't available, you must request that feature from the API provider or filter the results manually on the client side after receiving the full response.
