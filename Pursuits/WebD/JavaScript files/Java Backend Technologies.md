Java provides two main technologies for building **dynamic web applications**:

- **Servlet** — Java class that handles backend logic
    
- **JSP (JavaServer Pages)** — HTML page with Java embedded for UI
    

Think of it like this:

|Technology|What it does|Equivalent to|
|---|---|---|
|**Servlet**|Brains/logic|Controller|
|**JSP**|Display/output|View|

---

# 🌐 **How a Java Web App Works (Big Picture)**

Browser → Server → Servlet → JSP → Browser

1. User requests a page
    
2. Request goes to a **Servlet**
    
3. Servlet processes data (DB call, business logic)
    
4. Servlet forwards data to **JSP**
    
5. JSP displays the UI to the user
    

---

# 🧩 **SERVLET (Detailed Explanation)**

### ✔ Definition

A **Servlet** is a Java class that runs on the server and handles:

- HTTP Requests
    
- Backend logic
    
- Database interactions
    
- Business processing
    
- Forwarding results to JSP
    

### ✔ Lifecycle of a Servlet

1. **init()** — Called once when servlet loads
    
2. **service()** — Called for every request
    
3. **doGet() / doPost()** — Handles GET/POST requests
    
4. **destroy()** — When server shuts down