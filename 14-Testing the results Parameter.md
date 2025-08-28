# **Chapter 14: Assignment – Testing the `results` Parameter**

## **14.1 Objective**

This assignment is designed to reinforce your understanding of API documentation and query parameters. Your task is to test the `results` parameter for the `/products` endpoint, validate its functionality against the documentation, and identify any potential bugs.

## **14.2 Instructions**

1.  **Study the Documentation:** Carefully review the API documentation for the `/products` endpoint. Locate and understand the description of the `results` parameter.
2.  **Modify the Request:**
    *   In your existing "Get All Products" request in Postman, navigate to the **Params** tab.
    *   Disable or remove the `category` parameter.
    *   Add a new query parameter with the key `results`.
3.  **Test with Different Values:**
    *   Experiment with different numeric values for the `results` parameter (e.g., 1, 5, 10).
    *   Observe the changes in the API's response for each value you test.
4.  **Validate Functionality:** Determine if the `results` parameter behaves exactly as described in the API documentation. Does it limit the number of products returned in the response?
5.  **Test Parameter Combination:** Try combining the `results` parameter with the `category` parameter (e.g., `category=dairy&results=2`). Observe how the API handles multiple filters.
6.  **Identify Anomalies:** Actively try to find unexpected behavior or bugs. Does the API handle edge cases correctly (e.g., very high numbers, zero, negative numbers, non-numeric values)?

## **14.3 Goal**

The goal is not just to complete the task but to adopt a testing mindset. Approach this as a Quality Assurance engineer would: verify correctness, probe for weaknesses, and document any discrepancies between the documented behavior and the actual API behavior.

## **14.4 Next Steps**

After attempting this assignment independently, proceed to the next lecture for a guided solution. A follow-up quiz will provide a step-by-step breakdown to help you consolidate your learning and ensure you've identified the key aspects of the parameter's behavior.

***
### **Key Concepts**

*   **Validation:** The process of checking whether software behaves as specified in its requirements or documentation.
*   **Edge Case:** An extreme or unusual input or situation that tests the limits of a system's functionality.
*   **Regression Testing:** Re-running functional and non-functional tests to ensure that previously developed and tested software still performs after a change.

***
### **Key Takeaways**

*   API testing requires meticulous **attention to the documentation**.
*   A methodical approach to testing parameters involves **varying inputs** and **observing outputs**.
*   Effective testing often involves **combining parameters** to see how they interact.
*   The goal is to **validate expected behavior** and **uncover unexpected bugs**.
