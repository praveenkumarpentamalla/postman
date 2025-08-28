# **Chapter 8: Using Variables for Configuration**

## **8.1 The Problem: Hard-Coded Configuration**

A common issue when working with multiple API requests is managing repeated values, such as the **base URL**. If this value changes (e.g., the API moves to a new server), you must manually update it in every single request, which is inefficient and error-prone.

## **8.2 The Solution: Variables**

Postman **variables** solve this problem. They allow you to store a value (like a base URL) in one place and reference it dynamically in multiple requests. This creates a single source of truth for your configuration.

### **Variable Syntax**
Variables are referenced in requests using double curly braces: `{{variable_name}}`.
*   Example: `{{baseURL}}/status`

When the request is sent, Postman automatically replaces `{{baseURL}}` with its stored value.

## **8.3 Creating a Collection Variable**

The most effective way to manage shared configuration like a base URL is by using **collection variables**. These are variables scoped to a specific collection, making them available to every request within that collection.

**Steps to Create a Collection Variable from a URL:**

1.  **Select the Value:** In the address bar, highlight the base URL portion (do not include the endpoint path, e.g., `/status`).
2.  **Open the Context Menu:** Right-click the selected text or use the menu that appears above the selection.
3.  **Set as Variable:** Choose **"Set as variable"** -> **"Set as a new variable"**.
4.  **Configure the Variable:**
    *   **Variable name:** Enter a name (e.g., `baseURL`).
    *   **Value:** The selected URL is pre-filled as the value.
    *   **Scope:** Select **Collection** and choose the relevant collection from the dropdown.
5.  **Save:** Click **"Set variable"**.

Once set, the URL in your request will be replaced with the variable syntax (e.g., `{{baseURL}}/status`). **Remember to save the request** to persist this change.

## **8.4 How Variables Work**

*   **Internal Replacement:** The variable replacement happens internally within Postman *before* the HTTP request is sent. The server receives the fully resolved URL and is unaware that variables were used.
*   **Scope is Crucial:** Variables are only resolved if they are defined within a scope that the current request can access.
    *   A **collection variable** is only available to requests saved *within that specific collection*.
    *   An **unsaved request** (in a new tab) has no collection context and cannot resolve collection variables, resulting in an "unresolved variable" error.

## **8.5 Verifying Variable Replacement**

To confirm that the variable is being correctly replaced, use the **Postman Console** (View > Developer > Show DevTools).
1.  Open the Console.
2.  Send the request.
3.  In the console log, inspect the outgoing request. You will see the full, resolved URL, proving the `{{baseURL}}` variable was successfully replaced with its actual value.

***
### **Key Concepts**

*   **Variable:** A named container that stores a value which can be reused throughout requests and collections.
*   **Collection Variable:** A variable defined at the collection level, making it available to all requests within that collection.
*   **Variable Syntax:** The pattern `{{variableName}}` used to reference a variable's value within a request.
*   **Scope:** The context in which a variable is available (e.g., Global, Collection, Environment, Local).

***
### **Key Takeaways**

*   Using **variables for configuration** (like `baseURL`) is a best practice that makes your collections more **maintainable and robust**.
*   The syntax for using a variable is **`{{variableName}}`**.
*   **Collection variables** are the ideal scope for values shared by all requests in an API collection.
*   Variable replacement is an **internal Postman process**; the server receives the final, resolved value.
*   Always **check the Postman Console** to verify that variables are being resolved correctly before troubleshooting other issues.
*   An **"unresolved variable"** error almost always means the current request does not have access to a variable defined in the expected scope (e.g., the request is not part of the collection where the variable is stored).
