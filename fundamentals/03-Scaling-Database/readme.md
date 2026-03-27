# 🧠 How Databases Scale (Replication & Sharding)

These are my notes while learning and explaining how real systems scale databases.

This is not a textbook.  
It’s a simple mental model you can actually remember.

---

## 🚨 The Problem Starts Here

You scaled your backend:

Users → Load Balancer → Multiple Servers → ONE Database

Everything looks fine… but:

👉 **Your app is still slow**

---

## 🤔 Why?

Because all servers are hitting the same database.

And the database is doing everything:
- Reads (SELECT)
- Writes (INSERT / UPDATE)

---

## Under load, this happens:

- More requests come in  
- Queries start waiting  
- Latency increases  
- Eventually… things break  

---

### 💡 Key realization

> You scaled servers… but not the database.

---

## 💥 Single Point of Failure

If that one database goes down:

👉 Your entire system is down

Doesn’t matter:
- Servers are healthy  
- Traffic is low  

Everything depends on that DB.

---

## 🔧 First Attempt — Make DB Bigger

We try:

- More CPU  
- More RAM  
- Bigger machine  

---

### It works… for some time

But:

- There’s always a limit  
- It gets expensive  
- Still only one database  

---

### 💡 Insight

> Stronger… but still single.

---

## 🔁 Enter Replication

Instead of one database:

👉 We create copies

---

### Basic idea

- **Primary DB** → handles writes  
- **Replicas** → handle reads  

---

### Flow

Writes:
Server → Primary → Replicas (sync)

Reads:
Server → Replicas

---

### 💡 Mental model

> One database writes… many databases read.

---

## ⚙️ How Data Reaches Replicas

There are 2 ways this is done.

---

### ✅ 1. Direct Replication (most common)

Primary sends data to all replicas:

Primary → Replica 1  
Primary → Replica 2  
Primary → Replica 3  

Simple. Widely used.

---

### ⚠️ 2. Chained Replication (less common)

Primary → Replica 1 → Replica 2 → Replica 3  

- Reduces load on primary  
- But adds delay (lag increases as chain grows)

---

👉 For most systems, think in terms of **direct replication**

---

## 💸 Replication Is Not Free

Every write now does more work:

1. Write to primary  
2. Send data to replicas  
3. Replicas apply the change  

---

### Costs:

- Network usage  
- CPU + disk on replicas  
- More moving parts  

---

### 💡 Insight

> Replication improves reads… but adds overhead.

---

## ⏳ Replication Lag (Important)

Replication is usually **asynchronous**.

Meaning:
- Primary updates instantly  
- Replicas catch up after some time  

---

### Result

You might:

- Update data  
- Immediately read it  
- Still see old value  

---

### This is called:

👉 **Eventual Consistency**

---

📌 We’ll go deeper into this when we cover CAP theorem.

---

## Why Replication Works

- Read traffic is distributed  
- System becomes faster  
- Better availability  
- If one replica fails → others still work  

---

## ⚠️ But There’s Still a Problem

👉 Writes still go to ONE database

---

### What happens?

- Write requests pile up  
- Primary becomes bottleneck again  

---

### 💥 Important line

> Replication solves reads… but not writes.

---

## 🧠 Small but Important — Caching

Before doing anything complex, systems often add:

👉 Cache

---

### Why?

- Store frequently accessed data  
- Avoid hitting DB every time  

---

### Flow

Request → Cache → DB (only if needed)

---

### 📌 Note

We’ll cover caching separately — it’s a big topic.

---

## ⚡ Final Step — Sharding

When writes become the bottleneck:

👉 We split the database itself

---

### What is Sharding?

Divide data across multiple databases.

---

### Example

- DB1 → Users 1–1000  
- DB2 → Users 1001–2000  
- DB3 → Users 2001–3000  

---

### Now what happens?

- Each DB handles part of data  
- Writes are distributed  

---

### 💡 Mental model

> Instead of one huge database…  
> we use multiple smaller ones.

---

## ⚠️ Trade-offs of Sharding

- More complex system  
- Harder queries (joins become tricky)  
- Need logic to decide “which DB to hit”  

---

## 🔁 The Bigger Picture

This is how systems usually evolve:

Single DB ❌  
→ Bigger DB ⚠️  
→ Replication ✅ (reads solved)  
→ Cache ✅  
→ Sharding ✅(writes solved)

---

## 🔥 Final Thought

> Scaling is not one solution.  
> It’s a journey of fixing bottlenecks one by one.

---

## What’s Next

I’ll go deeper into:

- Sharding (real examples)
- Caching
- CAP theorem (consistency trade-offs)

---

If this helped, try explaining it to someone else.  
That’s where it really clicks.

And if you're following along with the series, consider subscribing to the channel — more simple system design videos coming.
https://www.youtube.com/@TheEngineersLabOfficial

Thank you for your time.
