# **Chapter 33: Retrieving and Modifying Data with GET and PATCH**

## **33.1 The Complete API Workflow: CRUD**

A full-featured API typically allows for four core operations, often abbreviated as **CRUD**:
*   **C**reate (``POST``)
*   **R**ead (``GET``)
*   **U**pdate (``PUT``/``PATCH``)
*   **D**elete (``DELETE``)

This chapter covers the "Read" and "Update" operations.

## **33.2 Retrieving Resources with GET**

After creating resources (like an order), you often need to retrieve them.

**Example: Get All Orders**
*   **Endpoint:** ``GET /orders``
*   **Purpose:** Fetches a list of all orders previously created by the authenticated client.
*   **Execution:** Duplicate a request (like the ``POST /orders`` request), change the method to ``GET``, and remove the request body. The authorization header remains necessary.
*   **Response:** Returns a ``200 OK`` status with a JSON array of order objects in the response body.

## **33.3 Updating Resources with PATCH**

The ``PATCH`` method is used to apply **partial modifications** to a resource. It updates only the fields provided in the request body, leaving all other fields unchanged.

**Example: Update an Order's Customer Name**
*   **Endpoint:** ``PATCH /orders/{orderId}``
*   **Purpose:** To modify a specific, existing order identified by its ``orderId``.
*   **Method:** ``PATCH``
*   **Path Variable:** The ``orderId`` of the order to update.
*   **Body:** A JSON object containing **only the field(s) you wish to change** (e.g., ``{"customerName": "Joe Doe"}``).
*   **Authorization:** Required.
*   **Response:** A successful update returns a ``204 No Content`` status. This means the request was understood and processed successfully, but the server has no additional information to send back in the response body. The update must be verified by a subsequent ``GET`` request.

## **33.4 Key Difference: POST vs. PATCH**

*   **``POST``:** Used to **create** a **new** resource. The request body typically contains all data needed to create the resource.
*   **``PATCH``:** Used to **update** an **existing** resource. The request body contains only the differential changes (the "patch") to apply.

## **33.5 Verification**

After a ``PATCH`` request returns ``204 No Content``, it is a best practice to call a ``GET`` request (e.g., ``GET /orders`` or ``GET /orders/{orderId}``) to confirm the changes were applied correctly.

***
### **Key Concepts**

*   **CRUD:** An acronym for the four basic functions of persistent storage: Create, Read, Update, Delete.
*   **PATCH:** An HTTP method used to apply partial updates to a resource.
*   **204 No Content:** A success status response code indicates that the request has succeeded, but that the client doesn't need to navigate away from its current page.

***
### **Key Takeaways**

*   Use ``GET`` on a collection endpoint (e.g., ``/orders``) to **retrieve a list** of resources.
*   Use ``PATCH`` on a specific resource endpoint (e.g., ``/orders/123``) to **update specific fields** of an existing resource.
*   A ``204 No Content`` response is a common and successful outcome for an update operation.
*   **Always verify** the results of an update operation by retrieving the resource afterward with a ``GET`` request.
*   ``PATCH`` is for partial updates; ``PUT`` (not covered here) is often used to replace an entire resource. The API documentation specifies which method to use.
