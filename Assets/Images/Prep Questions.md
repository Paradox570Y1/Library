Part 1: Functional Requirements (FRs)

**Question 1: "Let's discuss User Management. Your HLD specifies using OAuth 2.0 and JWT for authentication. Can you justify this choice and explain why you didn't opt for a more traditional session-based approach?"**

**Answer:**

"We selected **OAuth 2.0 and JWT** for three primary reasons: scalability, performance, and security in a modern microservices architecture.

• **Reasoning for JWT/OAuth 2.0:**

   ◦ **Statelessness and Scalability:** The core advantage is that JWTs are **stateless**. Each token is self-contained with verified user information, meaning any microservice can validate a user's identity without needing to contact a central authentication server or a shared session store. This is critical for **horizontal scaling**, as we can add more instances of a service and they can all operate independently, which is a key requirement.

   ◦ **Performance:** Verifying a JWT is a fast, local cryptographic operation. This is significantly faster than a traditional session approach, which would require a network call to a shared data store for every single request to validate the session.

   ◦ **Standardisation and Decoupling:** **OAuth 2.0** is the industry standard for delegated access, making it simple and secure to integrate third-party social logins like Google or Facebook. This reduces friction for new users and increases sign-up rates.

• **Why Not Traditional Sessions?**

   ◦ Traditional server-side sessions are **stateful**, meaning they require a shared session store, like Redis. This store can become a **performance bottleneck** under heavy load and introduces a single point of failure.

   ◦ In a microservices architecture, a shared session store creates unwanted coupling between services and complicates the architecture. The stateless nature of JWTs aligns perfectly with our decoupled microservices approach."

--------------------------------------------------------------------------------

**Question 2: "For the Product Catalogue, you've specified a dedicated search service using Elasticsearch. Why not just use standard SQL** **LIKE** **queries on your primary database? Isn't that simpler?"**

**Answer:**

"While SQL `LIKE` queries are simpler for basic cases, they are fundamentally unsuited for a high-performance, user-friendly search experience in a large e-commerce catalogue. We chose **Elasticsearch** for its superior performance, advanced features, and relevance control.

• **Reasoning for Elasticsearch:**

    ◦ **Performance:** SQL `LIKE` queries are notoriously slow and inefficient on large datasets, especially with leading wildcards, as they cannot use database indexes effectively. Elasticsearch is built on an inverted index, which makes it incredibly fast for full-text search. Our performance NFR of a **<2 second page load time** would be difficult to meet with SQL for search-heavy pages.

    ◦ **Advanced Features:** Elasticsearch provides crucial search features **out-of-the-box** that are very difficult to implement with SQL. These include **typo tolerance (fuzzy search), autocomplete, and synonym handling**. This directly improves the user experience and helps customers find products faster, which drives sales.

    ◦ **Relevance and Merchandising:** A key business requirement is the ability to control search results, such as boosting promoted items. Elasticsearch allows us to programmatically adjust the relevance score of search results based on business logic, a feature that is nearly impossible to achieve with a standard database.

• **Why Not SQL** **LIKE****?**

    ◦ It is simply too **slow and inefficient** for the scale we anticipate.

    ◦ It lacks the **intelligent search capabilities** (like typo tolerance) that customers now expect from a modern e-commerce platform.

    ◦ It offers no effective way to implement **business-driven merchandising rules**."

--------------------------------------------------------------------------------

**Question 3: "Your design stores the Shopping Cart in Redis. Why use an in-memory cache for this instead of your primary relational database, where user and order data is already stored?"**

**Answer:**

"The shopping cart is a highly dynamic and frequently accessed component. We chose **Redis** specifically to ensure a fast and responsive user experience during the browsing and checkout process, which is critical for conversion rates.

• **Reasoning for Redis:**

    ◦ **Performance and Low Latency:** Redis is an **in-memory data store**, which means it offers sub-millisecond read and write times. A traditional disk-based relational database is orders of magnitude slower because it involves disk I/O. For frequent operations like adding or removing items from a cart, this speed is essential for a smooth user experience.

    ◦ **Reduced Database Load:** Offloading cart operations to Redis prevents the primary transactional database (like PostgreSQL) from being burdened with frequent, temporary writes, allowing it to focus on critical operations like processing orders and payments.

    ◦ **Built-in Features:** Redis has a built-in **Time-To-Live (TTL)** feature, which is perfect for automatically expiring abandoned guest carts after a set period, keeping our data store clean without extra logic.

• **Why Not a Relational Database?**

    ◦ **Latency:** The performance would be significantly worse. The high frequency of cart updates would lead to slow response times and a poor user experience.

    ◦ **Load:** It would create a heavy, unnecessary load on the database that is responsible for our most critical, ACID-compliant transactions.

    ◦ **Data Structure Mismatch:** The flexible data structures in Redis, like hashes, are a more natural fit for storing cart data compared to the rigid tabular structure of a SQL database."

--------------------------------------------------------------------------------

**Question 4: "For Order Management, you've chosen an event-driven architecture using a message broker like Kafka. What is the advantage of this over simpler, direct API calls between services?"**

**Answer:**

"We opted for an **event-driven architecture** because it provides resilience, loose coupling, and scalability, which are essential for a critical workflow like order processing.

• **Reasoning for Event-Driven Architecture:**

    ◦ **Resilience and Fault Tolerance:** This is the primary driver. If one service makes a direct API call to another service that is temporarily down, the call fails and the entire process can halt. With an event-driven model, the 'payment.succeeded' event is published to a message broker like **Kafka**. If the Order service is down, the event remains in the queue and is processed as soon as the service recovers. This prevents data loss and ensures the order is eventually processed.

    ◦ **Loose Coupling and Extensibility:** Services do not need to know about each other. The Payment service simply emits an event; it doesn't care if the Order service, a Notification service, or an Analytics service consumes it. This makes the system much easier to maintain and extend. We can add new services that react to existing events without changing any of the original services.

    ◦ **Scalability:** A message broker like **Kafka** is built for very high throughput and durability, making it ideal for handling a large volume of order events during peak times like sales.

• **Why Not Direct API Calls?**

    ◦ They create a **brittle system** with tight dependencies. A failure in one downstream service can cause a cascading failure upstream.

    ◦ They require **complex retry logic** to be built into every service that makes a call, whereas a message broker handles this persistence automatically.

    ◦ The system becomes **harder to extend**. Adding a new step to the order process would require modifying the service that makes the API calls, increasing development complexity and risk."

--------------------------------------------------------------------------------

Part 2: Non-Functional Requirements (NFRs)

**Question 5: "The HLD is based on a Microservices architecture. Why did you choose this complex pattern over a simpler Monolith, especially for an MVP?"**

**Answer:**

"While a monolith might seem simpler initially, a **microservices architecture** was chosen to directly address our key non-functional requirements of **scalability, fault isolation, and maintainability**.

• **Reasoning for Microservices:**

    ◦ **Independent Scaling:** This is the most significant advantage. During a sale, the Product Catalogue and Search services will experience massive read traffic, while the Checkout and Order services will see a spike in writes. With microservices, we can scale each of these services **independently and horizontally**, using resources far more efficiently. A monolith would require us to scale the entire application, which is costly and inefficient.

    ◦ **Fault Isolation:** In a microservices architecture, a failure is contained. A bug in the less critical 'Reviews' service will not bring down the entire platform, particularly the checkout process. This directly supports our **high availability goal of 99.9% uptime**.

    ◦ **Maintainability & Technology Flexibility:** Small, independent services are easier for teams to understand, develop, and deploy. It also allows us to use the best technology for each job—for example, using a different programming language or database for the Search service than for the Order service.

• **Why Not a Monolith?**

    ◦ **Scaling Limitations:** A monolithic application can typically only be scaled "vertically" (adding more power to a single server), which is expensive and has a hard limit. It cannot be scaled efficiently to handle traffic spikes as required by our NFRs.

    ◦ **Lack of Resilience:** A single bug in any part of a monolith can crash the entire application, making it a single point of failure and jeopardising our availability targets.

    ◦ **Deployment Rigidity:** Deploying a small change requires re-deploying the entire application, making deployments slow, risky, and infrequent, which conflicts with our goal of having smooth CI/CD pipelines."

--------------------------------------------------------------------------------

**Question 6: "You've mentioned using Distributed Tracing with OpenTelemetry for observability. How is this better than just having centralised logging with the ELK stack, which is also in your design?"**

**Answer:**

"Centralised logging is essential, but in a distributed microservices system, logs alone are insufficient for effective troubleshooting. We chose **Distributed Tracing with OpenTelemetry** because it provides a complete, end-to-end view of a request as it travels across multiple services.

• **Reasoning for Distributed Tracing:**

    ◦ **Diagnosing Complex Issues:** When a single user action, like 'place order', triggers a chain of calls across five or six different microservices, simple logs make it extremely difficult to pinpoint the source of a failure or a performance bottleneck. Distributed tracing tags a request with a unique ID and follows its entire journey, allowing developers to visualise the full request path, see the latency at each step, and immediately identify which service is slow or has failed.

    ◦ **Reducing Debugging Time:** This visibility drastically reduces the Mean Time to Resolution (MTTR) for issues, which is critical for maintaining our availability and performance SLAs.

• **Why Not Just Centralised Logging?**

    ◦ Logs tell you _what_ happened within a single service, but they don't give you the context of the entire transaction across _all_ services. Correlating logs from multiple services based on timestamps is difficult and often inconclusive.

    ◦ Distributed tracing provides the causal link between events in different services, which is something logs cannot do on their own.

• **Why OpenTelemetry specifically?**

    ◦ We chose **OpenTelemetry** because it is the emerging **vendor-neutral industry standard** for observability. It provides a single set of APIs and SDKs for traces, metrics, and logs. This prevents vendor lock-in, meaning we can switch our observability backend (e.g., from Jaeger to another tool) in the future with minimal changes to our application code, which future-proofs our stack."