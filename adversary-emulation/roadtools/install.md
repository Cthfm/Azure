# Install

### **RoadTools Install Instructions & How it Works**

1. **Installation:**
   *   RoadTools is written in **Python** and can be installed via `pip`:

       ```bash
       pip install roadtools
       ```
2. **Authentication:**
   * Can authenticate using:
     * **Service Principal** credentials.
     * **OAuth Device Code Flow**, which makes it easy to get tokens without client secrets.
3. **Using RoadRecon:**
   *   Run the following command to start collecting data:

       ```bash
       roadrecon gather
       ```
   * This command collects information and stores it in a **SQLite database**.
   * The **interactive mode** lets you explore the data via queries or through its visualization interface.
