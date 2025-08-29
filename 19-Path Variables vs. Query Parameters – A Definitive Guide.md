# **Chapter 19: Path Variables vs. Query Parameters – A Definitive Guide**

## **19.1 Core Conceptual Difference**

While both path variables and query parameters are used to pass information in a URL, they serve fundamentally different purposes and are not interchangeable.

*   **Path Variables:** Used to **identify a specific resource or a hierarchy of resources**. They are part of the endpoint path itself and are **mandatory** for the endpoint to function. They define *what* you are accessing.
*   **Query Parameters:** Used to **modify, filter, or provide optional instructions** for the request. They are appended after a `?` and are typically **optional**. They define *how* you want the resource presented.

## **19.2 Visual Identification in a URL**

Deconstructing a complex URL makes the distinction clear:
`https://api.example.com/users/{username}/orders/{orderId}?platform=desktop&lang=en`

*   **Base URL:** `https://api.example.com`
*   **Path Variables (Mandatory, identify the resource):**
    *   `{username}` (e.g., `jane-doe`) – Identifies a specific user.
    *   `{orderId}` (e.g., `28032`) – Identifies a specific order belonging to that user.
*   **Query Parameters (Optional, modify the request):**
    *   `?platform=desktop` – Instructs the API to format the response for a desktop view.
    *   `&lang=en` – Requests the response content in English.

**Key Signifiers:**
*   **Path Variables** appear **before** the `?`.
*   **Query Parameters** appear **after** the `?`.
*   Multiple query parameters are separated by an **ampersand (`&`)**.

## **19.3 The "Directory" Analogy**

Think of the URL path as a filesystem directory structure:
*   `/users/jane-doe/orders/28032`
*   This path means: "Navigate into the `users` directory, then into the `jane-doe` sub-directory, then into her `orders` sub-directory, and finally access the resource named `28032`."
*   Path variables are the names of these specific, variable sub-directories and files. You cannot remove them without changing the resource you are trying to access.

## **19.4 The Most Important Rule: Follow the Documentation**

**You do not get to choose whether to use a path variable or a query parameter.** This decision is made by the API designer and is **immutably defined in the API documentation**.

*   The documentation will explicitly state if a parameter is **"in path"** (a path variable) or **"in query"** (a query parameter).
*   **You must use the exact type and key** specified. Using a path variable as a query parameter (or vice versa) will **always fail** because the server is only looking for the information in one specific place.

## **19.5 Combining Path Variables and Query Parameters**

A single request can—and often does—use both. The rule remains: use each for its intended purpose.
*   **Path Variables** pinpoint the exact resource.
*   **Query Parameters** refine how that resource is returned.

**Example:** `GET /products/4643?label=true`
*   **Path Variable `4643`:** Gets the specific product with ID 4643.
*   **Query Parameter `label=true`:** Adds an optional instruction to include the product label in the response.

## **19.6 Summary: Key Differences**

| Feature | Path Variable | Query Parameter |
| :--- | :--- | :--- |
| **Purpose** | Identify a specific resource | Filter, sort, paginate, or provide options |
| **Placement** | In the URL path | After the `?` in the URL |
| **Mandatory?** | Almost always **Yes** | Often **Optional** |
| **Syntax** | `/resource/{id}` | `?key=value&key2=value2` |
| **Flexibility** | Fixed by API design; cannot change | You can add supported options |

***
### **Key Concepts**

*   **Endpoint Path:** The part of the URL that comes after the base URL and before the `?`, defining the resource being accessed.
*   **Ampersand (`&`):** The character used to separate multiple query parameters in a URL.

***
### **Key Takeaways**

*   **Path variables identify *which* resource.** **Query parameters specify *how* to return it.**
*   **Path variables are before the `?`; query parameters are after it.**
*   **You must use the parameter type (path vs. query) specified in the API documentation.** There is no flexibility.
*   The **Postman UI separates them into different tabs** because they are fundamentally different concepts, even though both use a key-value format.
*   A single request can successfully use both path variables and query parameters together.
