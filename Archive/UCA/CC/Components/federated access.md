### 🌐 What is Federated Access?

**Federated access** means **allowing users from one system (or identity provider)** to access **resources in another system**, **without creating a new account** in the second system.

---

### 🔑 Simple Explanation:

> **Federated access lets users "bring their identity" from one trusted system to log into another.**

---

### 🧩 Real-World Example:

You work at a company that uses **Google Workspace**. Your company also uses **AWS**.

- Instead of creating a separate AWS username/password for you,
    
- AWS **trusts Google** to confirm your identity (via **federation**),
    
- You log in to AWS using your **Google account**,
    
- AWS gives you access based on the **role** you are assigned.
    

---

### 💬 One-liner:

> **Federation = Trust between identity systems.**

---

### ✅ Common Federated Identity Providers:

- Google
    
- Microsoft Azure AD
    
- Facebook (for apps)
    
- Okta
    
- SAML 2.0 / OpenID Connect (OIDC) systems
    

---

### 🔁 Federated Access vs SSO

|Feature|Federated Access|SSO (Single Sign-On)|
|---|---|---|
|Trust across domains|✅ Yes (e.g., Google to AWS)|❌ Typically within one domain/system|
|User account|Comes from **external** identity provider|Managed **internally**|
|Use case|Enterprise integration across platforms|Internal login to multiple apps after one login|