There are **many types of software testing**, each with a specific purpose. To simplify, we can divide testing into **major categories**, then list **common types** within those.

---

## 🔹 **Main Categories of Testing**

1. **Functional Testing**
2. **Non-Functional Testing**
3. **Maintenance Testing**
4. **Based on Test Execution (Manual vs. Automation)**
5. **Based on Development Stage (e.g., Unit, Integration, System, Acceptance)**

---

## ✅ **Popular Types of Software Testing (with Differences)**

| **#** | **Type of Testing**       | **Category**             | **Purpose / Difference**                                                                 |
| ----- | ------------------------- | ------------------------ | ---------------------------------------------------------------------------------------- |
| 1.    | **Unit Testing**          | Functional               | Tests **individual units** or components (e.g., functions, methods). Done by developers. |
| 2.    | **Integration Testing**   | Functional               | Checks if **modules work together** correctly.                                           |
| 3.    | **System Testing**        | Functional               | Tests the **entire system** as a whole.                                                  |
| 4.    | **Acceptance Testing**    | Functional               | Ensures the system meets **business requirements**. Usually done before release.         |
| 5.    | **Smoke Testing**         | Functional               | Quick test to see if basic features work. “Build verification.”                          |
| 6.    | **Sanity Testing**        | Functional               | Verifies **minor changes/bug fixes** haven’t broken anything important.                  |
| 7.    | **Regression Testing**    | Functional               | Ensures **new changes don’t break** existing features.                                   |
| 8.    | **Alpha Testing**         | Functional (pre-release) | Done **internally by QA** before release.                                                |
| 9.    | **Beta Testing**          | Functional (pre-release) | Done by **real users** in the real environment.                                          |
| 10.   | **Usability Testing**     | Non-Functional           | Checks if the system is **easy to use** and user-friendly.                               |
| 11.   | **Performance Testing**   | Non-Functional           | Tests how the system behaves under **load/stress**.                                      |
| 12.   | **Load Testing**          | Non-Functional           | Measures performance under **expected traffic**.                                         |
| 13.   | **Stress Testing**        | Non-Functional           | Tests system behavior under **extreme conditions**.                                      |
| 14.   | **Security Testing**      | Non-Functional           | Identifies **vulnerabilities, threats, and risks** in the software.                      |
| 15.   | **Compatibility Testing** | Non-Functional           | Verifies app works on **different devices, OS, browsers**.                               |
| 16.   | **Installation Testing**  | Maintenance              | Checks if the software **installs/uninstalls correctly**.                                |
| 17.   | **Manual Testing**        | Based on Execution       | Done **by humans**, clicking, typing, observing outcomes.                                |
| 18.   | **Automation Testing**    | Based on Execution       | Uses **tools/scripts** to run tests automatically. Faster and repeatable.                |

---

## 📌 Key Differences

|**Functional** Testing|**Non-Functional** Testing|
|---|---|
|Validates **what the system does**|Validates **how the system behaves**|
|Example: Login works or not|Example: Login page loads in 2 seconds|
|Focus on business logic/features|Focus on performance, security, usability|

---

## 🎯 Which to Use When?

- **Unit & Integration**: During development
    
- **System & Acceptance**: Before release
    
- **Regression & Sanity**: After updates
    
- **Performance & Security**: For production readiness
    
- **Beta Testing**: Before final launch with real users