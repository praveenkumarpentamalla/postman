# **Chapter 35: Updating Resources with PATCH – A Practical Example**

## **35.1 The Scenario: Modifying an Existing Cart Item**

A common use case is needing to change the quantity of an item already in a cart. Simply trying to `POST` the same item again results in a `400 Bad Request` error because the item already exists. The correct approach is to **update** the existing item.

## **35.2 The PATCH Method for Partial Updates**

The `PATCH` HTTP method is designed specifically for making partial updates to a resource. Instead of sending the entire resource again, you send only the field(s) you want to change.

**Endpoint Structure:** `PATCH /cart/{cartId}/items/{itemId}`

This endpoint requires two path variables:
1.  **`cartId`:** The ID of the cart containing the item.
2.  **`itemId`:** The unique ID of the specific item within the cart you want to modify. This `itemId` is different from the `productId` and is typically returned in the response when you first add the item to the cart.

## **35.3 Constructing the PATCH Request**

**Step-by-Step Guide:**

1.  **Identify the Item:** First, call `GET /cart/{cartId}/items` to find the `itemId` of the product you wish to update.
2.  **Build the Request:**
    *   **Method:** `PATCH`
    *   **URL:** `{{baseURL}}/cart/{{cartId}}/items/{{itemId}}` (Using variables for `cartId` and `itemId`)
    *   **Body:** A JSON object containing the field to update. In this case, only `quantity` is needed: `{"quantity": 2}`. Note that numbers in JSON are **not** enclosed in quotes.
3.  **Send the Request:** A successful update will return a `204 No Content` status, indicating the change was applied but no data is returned.

## **35.4 Verification**

After a `PATCH` request, it is essential to verify the change was made correctly by calling a `GET` request to retrieve the cart items again. The response should show the updated quantity for the specified item.

## **35.5 Key Distinction: POST vs. PATCH**

*   **`POST /cart/{cartId}/items`:** **Creates a new item** in the cart. The body must contain a `productId`.
*   **`PATCH /cart/{cartId}/items/{itemId}`:** **Updates an existing item** in the cart. The body contains the fields to modify (e.g., `quantity`).

***
### **Key Concepts**

*   **`itemId` vs. `productId`:** The `itemId` is a unique identifier for a line item *within a specific cart*. The `productId` is a unique identifier for a product *in the store's inventory*. One `productId` can be associated with multiple `itemId`s if it's added to different carts.
*   **Partial Update:** Changing only specific attributes of a resource without affecting others.

***
### **Key Takeaways**

*   Use `PATCH` to **update existing resources**, such as changing the quantity of a cart item.
*   The `PATCH` body should contain **only the fields you want to change**.
*   You often need the resource's specific ID (e.g., `itemId`) to perform an update, not just its general ID (e.g., `productId`).
*   A `204 No Content` response is a typical and successful outcome for an update operation.
*   **Always verify** the update by retrieving the resource afterward with a `GET` request.
