# **Chapter 7: Organizing Requests with Collections**

## **7.1 The Purpose of Collections**

In Postman, individual API requests cannot be saved in isolation. They must be organized within a **Collection**. A collection acts as a folder or a project that groups related API requests together, typically for a specific API or a particular testing workflow. This is essential for organization, reuse, and automation.

## **7.2 Creating a Collection and Saving a Request**

The process for saving a request involves first creating a collection to house it.

**Step-by-Step Guide:**

1.  **Initiate Save:** Click the **"Save"** button after configuring a request you wish to keep.
2.  **Create a New Collection:**
    *   In the save dialog, click **"Create Collection"**.
    *   Give the collection a descriptive name (e.g., "Simple Grocery Store API").
    *   Click **"Create"** to finalize the new collection.
3.  **Name the Request:** Provide a meaningful name for the request (e.g., "API Status") instead of using the default URL. This makes it easily identifiable later.
4.  **Finalize Save:** Ensure the correct collection is selected and click **"Save"**. The request is now permanently stored within that collection.

## **7.3 Accessing and Managing Saved Requests**

*   **Navigation:** All saved collections and their requests are listed in the left-hand **Collections** sidebar.
*   **Re-running Requests:** To execute a saved request, click on its name within the collection. This opens the request in a new tab; click **"Send"** to run it.
*   **Modifying Requests:** You can make changes to any saved request (e.g., altering the URL, parameters, or body).
*   **Saving Changes:** Postman does **not** save changes automatically.
    *   An orange dot appears on the request tab and in the sidebar to indicate there are **unsaved changes**.
    *   If you try to close a modified request, Postman will prompt you to save.
    *   To manually save changes, click the **"Save"** button. **Failure to save will result in all changes being lost.**

## **7.4 Best Practices for Using Collections**

*   **Use Descriptive Names:** Clearly name both collections and requests to create a self-documenting structure.
*   **Organize by Functionality:** Create separate collections for different APIs or different purposes (e.g., "User Authentication Tests," "Data Reporting API").
*   **Save Iteratively:** Get into the habit of clicking "Save" frequently after making successful changes to avoid losing work.

***
### **Key Concepts**

*   **Collection:** A container within Postman used to group and organize related API requests.
*   **Workspace:** The overarching environment where your collections live. You can have personal and team workspaces.

***
### **Key Takeaways**

*   All saved requests in Postman must belong to a **Collection**.
*   Always give requests **meaningful names** for easy identification.
*   Postman **does not auto-save** changes to requests. The orange dot is a critical visual indicator for unsaved work.
*   You must manually click **"Save"** to persist any modifications to a request.
*   The **Collections sidebar** is the central hub for accessing, organizing, and managing all your saved API workflows.
