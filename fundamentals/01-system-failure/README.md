# Why Systems Crash Under Load

## 🧠 Problem

A system works perfectly with a small number of users…  
but slows down and eventually crashes when traffic increases.

---

## 🔍 What Actually Happens

System failure is not instant. It happens in stages:

1. Increased load (more users)
2. Higher latency (responses become slow)
3. Timeouts (requests start failing)
4. Complete failure (system crashes)

---

## ⚠️ Bottleneck

Every system has a limit.

The component that reaches its limit first becomes the **bottleneck**.

It could be:
- Database
- CPU
- Memory
- Network

---

## 💣 Single Point of Failure (SPOF)

If one component failure causes the entire system to go down:

→ That component is a **Single Point of Failure**

---

## Engineer Thinking Area

When a system slows down or crashes, ask:

1. Where is latency increasing?
2. Which component is overloaded?
3. What fails first under load?
4. Is there a single dependency?

---

## Solution Direction

Once the bottleneck is identified:

→ We scale

Two types:
- Vertical Scaling → increase power of one machine
- Horizontal Scaling → add more machines and distribute load

---

## Key Insight

System Design is not about adding components first.

It is about identifying:

→ Where the system breaks under pressure

---

## Takeaway

System Design = Finding bottlenecks
