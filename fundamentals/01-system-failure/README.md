# Why Systems Crash Under Load

## Problem
Systems work perfectly with low users, but crash when traffic increases.

---

## 🔍 Root Cause Thinking
- Limited throughput (capacity)
- Increased latency (waiting time)
- Resource exhaustion (CPU, memory, DB connections)

---

## ⚠️ Bottleneck
The component that becomes the limit under load.

It fails first and slows down the entire system.

---

## 💣 Single Point of Failure (SPOF)
A component whose failure brings down the entire system.

---

## Engineer Checklist

When a system slows down or crashes, ask:

1. Where is latency increasing?
2. Which component is overloaded?
3. What fails first under load?
4. Is there a single dependency?

---

## Next Step
How to handle load → Scaling (Vertical vs Horizontal)
