# Why Systems Crash When Users Increase

This is the first step in understanding how systems scale from a single server to handling millions of users.

---

## 1. The Problem: Single Server Limitation

In a basic system:

User → Server

All requests go to a single machine.

### What happens when traffic increases?

- CPU usage increases
- Memory gets exhausted
- Requests start queueing
- Latency increases
- Eventually → system crashes

This is a **bottleneck**.

---

## 2. Bottleneck (Definition)

A bottleneck is any component in the system that limits overall performance.

If one component handles all traffic, it becomes a:

- Single Point of Failure (SPOF)
- Performance bottleneck

---

## 3. Solution: Horizontal Scaling

Instead of upgrading one machine (vertical scaling),
we add more machines.

User → Server1  
     → Server2  
     → Server3  

### Benefits:

- Distributes load
- Improves availability
- Prevents single machine overload

---

## 4. The New Problem

Now we have multiple servers.

Question:

👉 Who decides which server handles the request?

---

## 5. Load Balancer (Definition)

A Load Balancer is a component that:

- Receives incoming requests
- Distributes them across multiple servers

### Updated Flow:

User → Load Balancer → Servers

---

## 6. How Load Balancer Fits in System

### DNS Role

When a user enters a URL:

- DNS resolves the domain to the **Load Balancer’s IP**
- NOT to individual servers

---

### Network Structure

- Load Balancer → Public IP (accessible from internet)
- Servers → Private Network (not directly exposed)

---

### Final Flow

User → DNS → Load Balancer → Server

---

## 7. Key Idea: Single Entry Point

The Load Balancer is the **only entry point** to the system.

To the user:
👉 It looks like one system

Internally:
👉 It is multiple servers working together

---

## 8. Bottlenecks Shift

When we fix one bottleneck, another appears.

Example:

- First bottleneck → Server
- After scaling → Load Balancer
- Later → Database

### Important Principle:

Systems don’t fail at one place.

They fail at the **weakest component under load**.

---

## 9. Scaling Load Balancer

If Load Balancer becomes bottleneck:

We scale it.

---

### a. Active-Passive

- One Load Balancer is active
- Another is standby
- If active fails → standby takes over

---

### b. Active-Active

- Multiple Load Balancers handle traffic simultaneously
- Traffic is distributed (often via DNS)

---

## 10. Load Balancing Algorithms (Intro)

Load Balancer needs logic to decide:

👉 Which server should handle a request?

Common strategies:

### Round Robin
Requests are distributed sequentially:
S1 → S2 → S3 → repeat

---

### Least Connections
Send request to server with least active connections

---

### IP Hash
Same user → same server (useful for session consistency)

---

Each algorithm has trade-offs.

We will cover them in detail in a separate video.

---

## 11. What’s Next?

Now that we understand:

- system design basics
- load balancing
- bottlenecks

The next question is:

👉 How do we scale the database?

---

## Summary

- Single server systems fail under load
- Horizontal scaling distributes traffic
- Load Balancer manages request distribution
- Bottlenecks shift as systems grow
- Scaling is a continuous process

---

Understand Design First. Prioritize the big picture before the details.
Start with the blueprint, then build the foundation.
Then deep dive

