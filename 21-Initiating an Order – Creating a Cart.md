# **Chapter 21: Initiating an Order – Creating a Cart**

## **21.1 The Order Process Workflow**

Placing an order is a multi-step process governed by business logic. The first step is to create a **shopping cart**, which will hold the items you intend to purchase. The API documentation outlines the required steps and data.

## **21.2 The HTTP POST Method**

Until now, we have only used the **GET** method to retrieve (or "read") data. To create new resources on the server (like a cart or an order), we use the **POST** method.

*   **GET:** Used to **retrieve** information from the server. (Safe, idempotent).
*   **POST:** Used to **create** a new resource on the server. (Not idempotent – multiple identical requests will create multiple resources).

## **21.3 Creating a New Cart**

The endpoint to create a new cart is `POST /cart`.

**Key Characteristics of this Request:**
*   **HTTP Method:** `POST`
*   **Parameters:** This specific endpoint requires **no parameters**. There are no query parameters, path variables, or a request body to configure.
*   **Action:** It simply instructs the API to generate a new, empty cart.

**Executing the Request in Postman:**
1.  Create a new request or duplicate an existing one.
2.  Change the HTTP method from `GET` to `POST`.
3.  Set the URL to `{{baseURL}}/cart`.
4.  Ensure the **Body** tab is set to "none".
5.  Send the request.

## **21.4 Interpreting the Response**

A successful `POST /cart` request returns:
*   **Status Code:** `201 Created`. This is the standard HTTP response for a successful resource creation, which is more specific than a generic `200 OK`.
*   **Response Body:** A JSON object containing the newly created `cartId`. This ID is a unique identifier that **must be used in all subsequent requests** to add items to this specific cart or to place an order from it.

## **21.5 The Nature of POST Requests**

A critical property of `POST` is that it is **not idempotent**. This means:
*   Each time you send the `POST /cart` request, the server will create a **brand new cart** with a **new unique ID**.
*   Sending the same request five times will result in five different carts being created.
*   This differs from `GET` requests, which can be called repeatedly without changing the server's state.

***
### **Key Concepts**

*   **POST:** An HTTP method used to submit data to the server to create a new resource.
*   **201 Created:** The HTTP status code indicating that a request has been fulfilled and has resulted in a new resource being created.
*   **Idempotent:** The property of an operation whereby it can be applied multiple times without changing the result beyond the initial application. `GET` is idempotent; `POST` is not.
*   **cartId:** A unique identifier returned by the API after creating a cart. It is essential for all future operations on that cart.

***
### **Key Takeaways**

*   The first step in placing an order is to **create a cart** using a `POST` request to the `/cart` endpoint.
*   The `POST` method is used for **actions that change state** on the server (e.g., creating, updating, deleting).
*   A successful creation returns a **201 status code** and a **`cartId`** in the response body.
*   **`POST` requests are not idempotent;** repeating them creates multiple resources.
*   The **`cartId` is temporary and must be saved** immediately, as it is required for the next steps of adding items and placing the order.
