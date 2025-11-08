<p align="center">
<img width="202" height="202" alt="2893aede23f01bfcbd2319326bc96a6ed0524eba759745ed6d73405a3a8b67a8" src="https://github.com/user-attachments/assets/1382fd86-1d9d-4035-a199-417cca9e308b" />
</p>

<h1 align="center">🔍 API Testing with Postman & FakeStoreAPI</h1>

**Name:** MUHAMMAD SYAHMI ISYRAF BIN MOHD SYAHER

**Class:** M3CS2554A  

**Course Code:** ITT440

## 🎯 Title
This project demonstrates **Spike Testing** using **Postman** with the **Fake Store API**. Imagine a flash sale on an online store where thousands of users rush in at once to get their item checkout. Can the system handle it without crashing?
This project simulates that exact situation using Spike Testing with the Fake Store API. 

---

## 🎯 Objective
- To perform Spike Testing on an open REST API using Postman.  
- To observe how response time and success rate behave under sudden, high request volume.  
- To analyze API stability and reliability during load spikes.

---

## ⚙️ Tool & Target Site Selection
**Tool:** Postman  
**Target Site:** [Fake Store API](https://fakestoreapi.com)

### ⚙️ Postman Configuration
- Collection Runner with iteration delay: 0ms
- Environment: Fake Store API Public Endpoint
- Test Data: Static (no dynamic variables)

### 🧠 Why Fake Store API?
It provides dummy product, user, and cart data that is ideal for performance and reliability testing.

### 🧠 Why Postman?
It supports **Collection Runner** and **Newman CLI** for automated, repeated, or concurrent test executions. It is also **easy** to use.

---

## 🧪 Test Plan & Configuration
- **Test Type:** Spike Testing  
- **Request Method:** `GET`  
- **Endpoint:** `https://fakestoreapi.com/products`  
- **Test Duration:** 3 Phases  
  1. **Normal Load** – 10 requests (baseline)  
  2. **Spike Load** – 500 requests (sudden surge)  
  3. **Recovery Load** – 10 requests (return to normal)
 - **Test Script**
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response time is below 1000ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});

```

### 🧠 Assertions
- Verify `Status Code = 200`  
- Record **Average Response Time (ms)** and **Duration (s)** and **Error %**

---

## 🧪 Test Scenarios
1. Send 10 GET requests under normal conditions.  
2. Rapidly send 500 GET requests to simulate a sudden spike in traffic.  
3. Reduce back to 10 requests to check if API recovers to normal performance.  
4. Log and compare average response times between phases.

---

## 📊 Results (with charts)

| Phase | Total Requests | Passed | Failed | Avg Response Time (ms) | Duration | Error % |
|--------|----------------|--------|--------|-------------------------|---------|----------|
| Normal Load | 10 | ✅ 10 | ❌ 0 | 260 | 3s 717ms | 0.0 |
| Spike Load | 500 | ✅ 497 | ❌ 3 | 275 | 2m 59s | 0.6 |
| Recovery | 10 | ✅ 10 | ❌ 0 | 268 | 3s 819ms | 0.0 |

- 📈 Average Response Time (ms)

| Phase       | Avg Response Time |
|--------------|-------------------|
| Normal Load  | ████████ 260 ms   |
| Spike Load   | ██████████ 275 ms |
| Recovery     | ████████ 268 ms   |

### 🧠 Observations
- During the spike, average response time increased from **260 ms → 275 ms**, as more requests are being processed.  
- After the spike, the API recovered to **268 ms**, indicating it is starting to stabilize.  
- Only **3 failures (timeouts)** occurred during the highest load.

*(Insert Postman result screenshot or chart below)*  
Example Result:

- Normal Phase 
<img width="1141" height="221" alt="Screenshot 2025-10-31 121612" src="https://github.com/user-attachments/assets/25ee43a0-12d9-4659-811f-ff08c31975cb" />

- Spike Phase
<img width="1162" height="250" alt="Screenshot 2025-10-31 120956" src="https://github.com/user-attachments/assets/f391ce76-da66-4bfe-8d33-b1fe1e3b1b83" />

- Recovery Phase
<img width="1177" height="259" alt="Screenshot 2025-10-31 121009" src="https://github.com/user-attachments/assets/e78b4e13-e32c-4be6-9c8f-2292fd93cca5" />


---

## 🧠 Analysis & Discussion
- The **Fake Store API** handled the sudden spike with minor degradation in response time.  
- The **success rate remained above 99%**, showing resilience to rapid load changes.  
- The **response size** remained constant, confirming data integrity.  
- **Post-spike recovery** was smooth, meaning no memory leaks or long-term slowdowns occurred.

---

## ⚡ Key Findings

- API remained 99.4% stable under 500 request spike

- Response time increased only +15 ms during load

- No permanent degradation after traffic spike

- 3 minor timeouts observed, all recovered automatically

---

## 💡 Recommendations
- Implement **rate limiting** and **load balancing** to handle spikes more effectively in production systems.  
- Use **Postman + Newman CLI** to simulate concurrent users via command line.  
- Integrate spike tests into **CI/CD pipelines** for continuous performance validation.

---

## ✅ Conclusion
The Spike Testing conducted using the Fake Store API successfully demonstrated how system performance behaves under sudden load surges. Despite a 50× increase in request volume, the API maintained a stable average response time with minimal errors which is (0.6%). Once the load decreased, the performance recovered to near baseline levels without persistent degradation. These results indicate that the Fake Store API is resilient, well optimized, and capable of maintaining reliability even during abrupt traffic spikes. The experiment also emphasizes the importance of spike testing as part of performance assurance, ensuring that real world systems remain stable under unpredictable user demand. 

---

## Embedded YouTube Video Link
[Click here to watch the demo](https://www.youtube.com/)

## References
- About: [Fake Store API Documentation](https://fakestoreapi.com)  
- Learn About: [Postman Learning Center – Performance Testing](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/)
- [Demonstration of How to Use the Postman ]https://www.youtube.com/watch?v=0qQjd_SoJb4
