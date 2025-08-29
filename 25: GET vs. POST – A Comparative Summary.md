# **Chapter 25: GET vs. POST – A Comparative Summary**

## **25.1 Core Semantic Difference**

The fundamental difference between `GET` and `POST` lies in their intended purpose, as defined by the HTTP standard:

*   **GET:** Used to **retrieve** (or "read") data from the server. It should not change the state of the server.
*   **POST:** Used to **create** new resources (or sometimes to update them) on the server. It is used for actions that change the server's state.

## **25.2 Key Differences at a Glance**

| Feature | **GET** | **POST** |
| :--- | :--- | :--- |
| **Purpose** | Retrieve data (Read) | Create data (Create) |
| **Side Effects** | **None (Idempotent).** Repeated identical requests have the same effect as a single request. | **Has side effects (Not Idempotent).** Each identical request creates a new, separate resource. |
| **Request Body** | Typically **never has a body.** All data is sent via the URL (query parameters/path variables). | **Almost always has a body** (e.g., JSON, XML) containing the data to be created. |
| **Data Visibility** | Parameters are visible in the URL. | Data is hidden in the request body, offering more privacy for sensitive information. |
| **Use Case** | Fetching a list of products, getting details of a single product, viewing cart contents. | Creating a new cart, adding an item to a cart, placing an order. |

## **25.3 Practical Implications**

*   **Idempotency:** Calling `GET /products` ten times will return the same product list ten times without creating anything new. Calling `POST /cart` ten times will create ten separate, empty carts.
*   **Data Transmission:** With `GET`, you filter what you *get* using **query parameters** in the URL. With `POST`, you specify what you want to *create* using a **request body**.
*   **The Rule of Documentation:** **You do not choose between `GET` and `POST`.** The API documentation for each endpoint explicitly states which HTTP method to use. Using the wrong method (e.g., sending a `GET` to a endpoint documented for `POST`) will either fail or not perform the intended action.

## **25.4 Analogy**

*   **GET** is like **reading** a menu. You can look at it as many times as you want; it doesn't change the kitchen's state.
*   **POST** is like **submitting** your order to the kitchen. Each time you submit an order slip, the kitchen prepares a new meal, changing its state.

***
### **Key Concepts**

*   **Idempotent:** An operation that can be performed multiple times without changing the result beyond the initial application. `GET` requests are idempotent.
*   **Side Effect:** A change of state on the server (e.g., creating a new record in a database). `POST` requests are designed to cause side effects.

***
### **Key Takeaways**

*   Use **GET** for **reading** data. Use **POST** for **creating** data.
*   **GET requests are safe and idempotent;** repeating them is harmless.
*   **POST requests are not idempotent;** repeating them will create duplicate resources.
*   **GET uses the URL for data;** **POST uses the request body.**
*   **Always follow the API documentation** to determine the correct HTTP method for each endpoint.
