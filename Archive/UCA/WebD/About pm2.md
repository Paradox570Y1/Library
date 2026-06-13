## 🧠 Let's Start with the Basics

### ❓What is PM2?

**PM2** is a **process manager** for Node.js. Think of it like a smart assistant that:

- Starts your app
    
- Restarts it if it crashes
    
- Runs it multiple times in **cluster mode** (which allows for load balancing)
    

---

## 🚦What Happens When You Run This?

`pm2 start server.js -i 0 --name web-loadbalancedapp`

### Here's What That Command Is Doing:

1. **`start server.js`** → It tells PM2 to run your Node.js file (`server.js`) which probably contains something like:
    
    js
    
    CopyEdit
    
    `const express = require('express'); const app = express(); app.listen(8080, () => console.log("Server running on 8080"));`
    
2. **`-i 0`** → This tells PM2:
    
    > "Use all available CPU cores to run multiple copies (instances) of this app."
    
    For example, if your server has 4 CPU cores, PM2 will create **4 worker processes** of your app — all listening on the same port `8080`.
    
3. **`--name web-loadbalancedapp`** → Gives a readable name to your app in PM2’s process list.
    

---

## 🤖 What Does PM2 Do Internally?

Here’s the magic:

### 🔁 PM2 uses Node’s **Cluster Module**

- Normally, only **one Node.js process** can listen on a port (like 8080).
    
- But Node has a **cluster module** that allows you to create **multiple child processes** — all running your app — and they can **share the same port**!
    
- PM2 handles this for you under the hood when you use `-i`.
    

### 🧪 So What Happens Now?

- PM2 creates 1 **master process** (PID: 2185 in your image).
    
- Then it creates **multiple worker processes** (like PIDs 2454, 2461).
    
- These workers **all listen on port 8080**, but **only one handles each incoming request** — thanks to internal load balancing.
    

---

## 🏃‍♂️ Load Balancing in Action

Imagine your app is a restaurant. You now have:

- 1 front-desk (PM2 master)
    
- 4 waiters (Node.js workers)
    

When 3 customers come in:

- PM2 sends Customer 1 to Waiter 1
    
- Customer 2 to Waiter 2
    
- Customer 3 to Waiter 3
    

Each request is handled **by only one worker**, and PM2 makes sure to **balance the load evenly** between all workers. If one worker is busy, the next request goes to another.

---

## 📸 Back to Your Screenshot

Here's what it's showing:

### ✅ PM2 Master:
t

`PM2\x20v6   2185 ubuntu  ... TCP *:http-alt (LISTEN)`

- The master process is listening on port `8080` (`http-alt` is another name for it).
    
- It's waiting for HTTP requests.
    

### ✅ Node Workers:


`node       2454 ubuntu  ... ESTABLISHED http-alt->136.233.11.130:21970 node       2461 ubuntu  ... ESTABLISHED http-alt->136.233.11.130:55125`

- Each worker is handling connections from the same remote IP (`136.233.11.130`), possibly you testing from a browser.
    
- Each one is actively **handling a request** (status: ESTABLISHED).
    

---

## ⚖️ So How is It Load Balancing?

1. All Node processes are **identical** — they run the same `server.js`.
    
2. PM2 distributes **incoming connections** among them using **round-robin** (by default).
    
3. Your system handles **more traffic** without slowing down, since requests are **shared** between all CPU cores instead of piling up on one.
    

---

## 🛠️ Extra Tip: Check How Many Instances

`pm2 list`

This shows how many instances PM2 started.

---

## 🎯 Summary

|Term|What It Means|
|---|---|
|PM2|A smart process manager for Node apps|
|Cluster Mode|Runs multiple copies of your app on different CPU cores|
|`-i 0`|Use all CPU cores automatically|
|Load Balancing|PM2 distributes requests evenly to multiple worker processes|
|Benefit|Handles more users without crashing or slowing down|