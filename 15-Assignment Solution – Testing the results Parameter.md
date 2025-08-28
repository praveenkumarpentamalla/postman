# **Chapter 15: Assignment Solution – Testing the `results` Parameter**

## **15.1 Objective Recap**

The goal was to test the `results` query parameter for the `/products` endpoint, validate its functionality against the API documentation, and identify any bugs or unexpected behavior.

## **15.2 Expected Behavior (Based on Documentation)**

According to the API documentation, the `results` parameter should:
*   Be an **integer**.
*   Have a value between **1 and 20**.
*   **Limit the number of products** returned in the response.
*   Have a **default value** (implied to be 20 if not specified).

## **15.3 Test Results and Analysis**

### **✅ Valid Inputs (Working as Expected)**
*   **Values 1-20:** Parameters like `results=1`, `results=5`, and `results=20` work correctly. The API returns the exact number of products specified.
*   **Combination with `category`:** Using `results` in combination with `category=fresh%20produce` works as expected, limiting the results within the specified category.

### **❌ Invalid Inputs & Identified Bugs (Unexpected Behavior)**
The API exhibits several issues when handling inputs that violate the documented contract:

1.  **Non-Integer Values:**
    *   **`results=2.5`** returns a status `200 OK` and **2 results**. This is a bug. Since the parameter is defined as an integer, it should reject non-integer values with a `400 Bad Request` error.

2.  **Non-Numeric Prefixes:**
    *   **`results=john`** and **`results=5john`** return a status `200 OK`. The API seems to parse only the leading numeric part (e.g., it interprets `5john` as `5`), which is inconsistent and error-prone behavior.

3.  **Value of Zero:**
    *   **`results=0`** returns a status `200 OK` and **all results** instead of an empty list or an error. This contradicts the documentation stating the value must be "greater than zero."

### **✅ Proper Error Handling (Working as Expected)**
*   **Values > 20:** `results=30` correctly returns a `400 Bad Request` error with a clear message: "cannot be greater than 20."
*   **Negative Values:** `results=-20` correctly returns a `400 Bad Request` error with the message "must be greater than zero."

## **15.4 Additional Context: Pagination**

The test revealed a design limitation of the API: it lacks **pagination**. Pagination is a standard API technique to handle large datasets by splitting results into manageable "pages."
*   The hard limit of 20 results means it's impossible to retrieve the entire product list if it contains more than 20 items.
*   A more robust API would use parameters like `page` and `limit` to allow clients to navigate through all available data.

## **15.5 Conclusion and Next Steps**

The `results` parameter functions correctly for standard use cases but contains significant validation flaws. These findings should be reported to the development team as bugs. The API should be updated to:
1.  Strictly validate that the value is an integer.
2.  Properly handle the edge case of `0`.
3.  Reject values with non-numeric characters entirely.

This exercise highlights the importance of thorough API testing, including edge cases and invalid inputs, to ensure robustness and security.

***
### **Key Concepts**

*   **Input Validation:** The process of ensuring data entered into a system is correct, useful, and secure. The API's validation for the `results` parameter is weak.
*   **Pagination:** A technique for dividing a large set of results into discrete pages to improve performance and usability. This API does not implement it.
*   **Edge Case Testing:** Testing the boundaries of acceptable input values (e.g., 0, 1, 20, 21) and invalid inputs (e.g., negative numbers, decimals, text).

***
### **Key Takeaways**

*   **Always test beyond the "happy path."** Deliberately try invalid and edge-case inputs to uncover bugs.
*   **APIs often have undocumented behavior** when receiving invalid requests. Documenting this behavior is a key part of the testing process.
*   **Validation logic is a common source of bugs.** Never assume the server will correctly handle malformed data.
*   **The lack of pagination is a design limitation** that restricts the usability of the API for large datasets.
