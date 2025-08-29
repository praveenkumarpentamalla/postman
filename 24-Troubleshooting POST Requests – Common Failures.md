# **Chapter 24: Troubleshooting POST Requests – Common Failures**

## **24.1 Overview of Common Failure Points**

`POST` requests are more complex than `GET` requests because they involve sending data. This introduces multiple potential points of failure. This chapter catalogs common errors and their solutions.

## **24.2 Common Error #1: Unresolved Variables**

*   **Symptom:** The request fails because the `{{baseURL}}` (or other variables) appear in red or are not replaced.
*   **Cause:** The request is not saved to the collection that contains the variable definitions.
*   **Solution:** Save the request to the correct collection to inherit its variables.

## **24.3 Common Error #2: Invalid or Missing Path Variable**

*   **Symptom:** Error message like "No cart with ID: {cartId}".
*   **Cause:** The path variable (e.g., `cartId`) is empty or contains an invalid/expired value.
*   **Solution:** Ensure the path variable's **Value** field is populated with a current, valid identifier obtained from a previous API call (e.g., the `cartId` from `POST /cart`).

## **24.4 Common Error #3: Incorrect HTTP Method**

*   **Symptom:** The request appears to succeed (e.g., returns `200 OK`) but the intended action does not occur (e.g., no item is added to the cart).
*   **Cause:** Using `GET` instead of `POST`. `GET` requests are for retrieving data and ignore the request body entirely. The server processes them as a read operation, not a create operation.
*   **Solution:** **Always double-check that the HTTP method is set to `POST`** (or the method specified in the documentation) for actions that create or modify data.

## **24.5 Common Error #4: Missing Content-Type Header**

*   **Symptom:** Error message like "Invalid or missing product ID" even though the JSON body looks correct.
*   **Cause:** The **Body** format is set to `Text` instead of `JSON`. This means the request lacks the `Content-Type: application/json` header, so the server doesn't know how to interpret the body's content.
*   **Solution:** In the **Body** tab, always select **`JSON`** from the format dropdown after choosing `raw`. This automatically sets the correct `Content-Type` header.

## **24.6 Common Error #5: Invalid JSON Body Structure**

*   **Symptom:** `400 Bad Request` errors related to the request body.
*   **Cause:**
    *   **Invalid Product ID:** The `productId` value in the JSON does not correspond to an actual product in the system.
    *   **Invalid JSON Syntax:** The body contains JSON syntax errors (missing commas, trailing commas, single quotes instead of double quotes).
    *   **Incorrect Data Structure:** Trying to send an array of items when the API endpoint only accepts a single object (e.g., `[{"productId": 1}, {"productId": 2}]` instead of `{"productId": 1}`).
*   **Solution:**
    *   Use **valid product IDs** from a `GET /products` call.
    *   **Copy the exact JSON structure** from the API documentation example to avoid syntax errors.
    *   Use Postman's **JSON editor and "Beautify"** function to validate and format your JSON.
    *   **Never assume functionality;** only send data structures explicitly described in the API documentation.

## **24.7 The Golden Rule of API Testing**

**You cannot invent functionality.** The API's capabilities are strictly defined by its documentation. If the documentation for `POST /cart/{cartId}/items` shows an example with a single JSON object, you cannot send an array and expect it to work, even if it is valid JSON. The server-side logic is only built to handle the documented use case.

***
### **Key Concepts**

*   **Content-Type Header:** An HTTP header that tells the server what kind of data is in the request body. For JSON, it must be `application/json`.
*   **Idempotent:** An operation that can be repeated without changing the result. `GET` is idempotent; `POST` is not.

***
### **Key Takeaways**

*   **Save requests to collections** to ensure variables are resolved.
*   **Always use `POST`** (not `GET`) for requests that create data.
*   **Always set the Body format to `JSON`** to ensure the `Content-Type` header is set correctly.
*   **Use valid, existing IDs** for path variables and in the JSON body.
*   **Follow the API documentation exactly** for the JSON body structure. Do not deviate from the provided examples.
*   **The server's logic is limited to its documentation.** Unsupported actions, even if syntactically correct, will fail.
