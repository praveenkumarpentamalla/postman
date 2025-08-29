# **Chapter 36: Replacing Resources with PUT**

## **36.1 Beyond PATCH: Complete Replacement**

While `PATCH` is used for partial updates, the `PUT` method is used for **complete replacement** of a resource. `PUT` requests require the client to send the entire representation of the resource, effectively replacing whatever currently exists at the target URL.

## **36.2 PUT vs. PATCH: A Practical Distinction**

*   **`PATCH /cart/{cartId}/items/{itemId}`:** "Please change **only** the `quantity` of this specific item to 2." (Partial Update)
*   **`PUT /cart/{cartId}/items/{itemId}`:** "Here is the **complete new definition** for this specific item. Replace whatever is there with this new data." (Complete Replacement)

## **36.3 Constructing a PUT Request**

**Scenario:** Replacing a cart item (e.g., spinach) with a different product (e.g., coffee).

**Step-by-Step Guide:**

1.  **Identify the Target:** You need the `cartId` and the specific `itemId` of the item you want to replace.
2.  **Build the Request:**
    *   **Method:** `PUT`
    *   **URL:** `{{baseURL}}/cart/{{cartId}}/items/{{itemId}}`
    *   **Body:** A JSON object containing the **complete new state** of the item. According to the API documentation, this must include the new `productId` and can optionally include a new `quantity`. The entire existing item will be replaced by this new data.
        ```json
        {
          "productId": 4640,
          "quantity": 1
        }
        ```
3.  **Send the Request:** A successful `PUT` request typically returns a `204 No Content` status, indicating the resource was successfully replaced.

## **36.4 Outcome and Verification**

After the `PUT` request, the specified cart item is completely overwritten. The `itemId` remains the same (as it identifies the *slot* in the cart), but the `productId` and any other attributes are updated to the new values provided in the request body.

Verification via a subsequent `GET /cart/{cartId}/items` request will confirm the change: the item will show the new product details.

## **36.5 Key Consideration: Idempotency**

Like `GET`, `PUT` is **idempotent**. Making multiple identical `PUT` requests has the same effect as making a single one. This is because `PUT` sets the resource to a specific state; repeating the same "set" operation doesn't change the outcome.

***
### **Key Concepts**

*   **PUT:** An HTTP method used to replace the entire state of a resource at a specific URL with the representation provided in the request body.
*   **Idempotent:** The property of an operation whereby it can be applied multiple times without changing the result beyond the initial application. `PUT` is idempotent.

***
### **Key Takeaways**

*   Use `PUT` when you need to **completely replace** a resource, not just modify part of it.
*   The `PUT` request body must contain the **full representation** of the resource as you want it to exist after the operation.
*   `PUT` is **idempotent**, making it safe to retry if needed.
*   The target resource is identified by the URL (including path variables like `cartId` and `itemId`).
*   Always **verify** the result of a `PUT` operation with a subsequent `GET` request.
