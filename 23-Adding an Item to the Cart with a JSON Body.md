# **Chapter 23: Adding an Item to the Cart with a JSON Body**

## **23.1 Constructing a Valid POST Request**

To add an item to a cart, you must send a `POST` request with a correctly structured JSON body. The API documentation specifies the exact requirements.

**Request Components:**
*   **HTTP Method:** `POST`
*   **Endpoint:** `/cart/{cartId}/items` (The `{cartId}` is a path variable replaced with your actual cart ID)
*   **Body:** A JSON object containing the required parameters.

## **23.2 The JSON Request Body**

The API expects a specific JSON structure in the request body. The documentation provides an example:

```json
{
  "productId": 1234
}
```

*   **`productId` (Required):** The key must be exactly as specified. The value must be a valid numeric product ID that exists in the inventory.

## **23.3 Executing the Request in Postman**

**Step-by-Step Guide:**

1.  **Set the Method and URL:** Create a `POST` request to `{{baseURL}}/cart/{{cartId}}/items`. Ensure the `cartId` path variable is set to the ID you received from the `POST /cart` request.
2.  **Configure the Body:**
    *   Go to the **Body** tab.
    *   Select the **`raw`** option.
    *   From the format dropdown, select **`JSON`**.
3.  **Write the JSON:** Enter the valid JSON object. The easiest and most reliable method is to **copy the example directly from the API documentation** and then replace the example `productId` value with a real one from your "Get All Products" response.
4.  **Send the Request:** Click "Send".

## **23.4 Interpreting a Successful Response**

A successful add-to-cart request returns:
*   **Status Code:** `201 Created`, indicating a new resource (the cart item) was successfully created.
*   **Response Body:** A JSON object containing details about the newly added item, including a new `itemId` and the `productId`.

## **23.5 Verifying the Action**

To confirm the item was added, you can call a `GET` endpoint for the cart (e.g., `GET /cart/{cartId}/items`). The response should be a JSON array containing the item you just added, confirming the cart's state has changed.

## **23.6 The Critical Importance of Valid JSON**

Postman's JSON editor provides visual cues:
*   **Syntax Highlighting:** Colors different elements (keys, strings, numbers) for easier reading.
*   **Error Highlighting:** Invalid JSON (e.g., missing commas, single quotes instead of double quotes) will be underlined in red. **Sending invalid JSON will always result in a `400 Bad Request` error.**

**Best Practice:** Always copy the basic structure from the API documentation to avoid syntax errors, then modify the values.

***
### **Key Concepts**

*   **Request Body:** The section of an HTTP request used to send data to the server to create or update a resource.
*   **201 Created:** The HTTP status code indicating that a request has been fulfilled and has resulted in a new resource being created.

***
### **Key Takeaways**

*   Use a **`POST`** request with a **JSON body** to add items to a cart.
*   The **JSON structure must match the API documentation exactly**. Keys are case-sensitive.
*   **Always use a valid product ID** obtained from a `GET /products` request.
*   A successful response returns a **`201 Created`** status.
*   **Postman's JSON editor helps validate syntax** before sending. Red underlines indicate errors that must be fixed.
*   Verify the cart's contents after adding an item by calling a corresponding `GET` endpoint.
