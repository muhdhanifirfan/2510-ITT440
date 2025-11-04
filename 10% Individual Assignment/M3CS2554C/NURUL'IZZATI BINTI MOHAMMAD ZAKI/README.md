# 🚀 Performance Load Testing on JSONPlaceholder API Using Artillery


**Name:** Nurul’Izzati binti Mohammad Zaki  
**Student ID:** 2025395205  
**Class:** M3CS2554C

🎥 **Demo Video:** [Watch on YouTube](https://youtu.be/YOUR_VIDEO_LINK)

---

## 🧭 Introduction

This project focuses on evaluating the performance and stability of the **JSONPlaceholder API** by running a **load test** using **Artillery**, a popular open-source performance testing tool built for Node.js.  
The aim is to measure the system’s behavior when multiple users access it simultaneously and to determine how well it performs under different traffic conditions.

---

## 🎯 Goal and Hypothesis

The main goal of this test is to analyze how **JSONPlaceholder** handles increasing user load and whether it remains stable under pressure.

**Hypothesis:**  
> The JSONPlaceholder API will maintain good performance under load, with average response times below 500 milliseconds, minimal latency spikes, and no request failures even at peak user load.

---

## ⚙️ Tool Selection Justification

| Reason | Explanation |
| --- | --- |
| Easy setup | Artillery uses simple YAML configuration files that are easy to modify and read. |
| Detailed metrics | Provides in-depth response time and throughput reports with percentiles (p50, p95, p99). |
| Cloud visualization | Integrates with **Artillery Cloud** for graphical results and trend analysis. |
| Lightweight | Works efficiently on local machines without extra dependencies. |
| Industry adoption | Commonly used for API and backend performance testing in CI/CD pipelines. |

Artillery was chosen because it offers the balance of simplicity, accuracy, and modern visualization tools that fit academic and industry testing standards.

---

## 🧩 Test Environment

| Component | Details |
| --- | --- |
| Operating System | Windows 11 |
| Node.js Version | 22.21.0 |
| Artillery Version | 2.0.26 |
| Target URL | https://jsonplaceholder.typicode.com |
| Internet Connection | Stable broadband |

---

## 📋 Test Scenario Configuration

Each virtual user (VU) simulates a normal usage pattern by sending a sequence of API requests.  

| Step | Action | Endpoint | Method |
| --- | --- | --- | --- |
| 1 | Retrieve a post | `/posts/1` | GET |
| 2 | Retrieve a user | `/users/1` | GET |
| 3 | Create a new post | `/posts` | POST |
| 4 | Wait between requests | — | think(1s) |

---

## 📈 Load Phases

| Phase | Duration | Arrival Rate | Ramp To | Description |
| --- | --- | --- | --- | --- |
| Low | 30s | 2 users/sec | 5 users/sec | Establish baseline load |
| Moderate | 60s | 5 users/sec | 10 users/sec | Typical daily traffic simulation |
| Heavy | 90s | 10 users/sec | 15 users/sec | Peak traffic to test stability |

This gradual increase simulates real-world traffic, helping to identify how performance scales with concurrent users.

---

## 🧰 Test Execution

### Step 1: Install Node.js and Artillery (in VS Code Terminal)

Open the integrated terminal in **Visual Studio Code** and run these commands step by step.

### 1️⃣ Install Node.js (if not installed)

- After installation, verify using:

```bash
node -v
npm -v
```
### 2️⃣ Install Artillery globally
```bash
npm install -g artillery

```
### 3️⃣ Verify Artillery installation
```bash
artillery --version

```
or
```bash
artillery -v

```
---

## 🧮 Test Summary

| **Metric** | **Result** |
|-------------|------------|
| **Total Duration** | 3 minutes 6 seconds |
| **Total Requests Sent** | 5,040 |
| **Completed Requests** | 5,040 |
| **Failed Requests** | 0 |
| **Average Request Rate** | 44 requests/sec |
| **Average Response Time** | 126.1 ms |
| **95th Percentile** | 320.6 ms |
| **99th Percentile** | 415.8 ms |
| **Error Rate** | 0% |
| **Virtual Users Simulated** | 1,680 |

---

## 📊 Data Analysis

<p align="center">
  <img src="https://github.com/user-attachments/assets/adf1012e-c5d3-4669-bbb6-39fc5f0a6aad" alt="Artillery Response Time Graph" width="750"/><br>
  <em>Figure: Artillery Cloud graph showing response time and request rate trends</em>
</p>


### 🔹 Throughput
The request rate increased smoothly from **8–10/sec** in the low phase to around **44/sec** at the heavy phase.  
✅ The API managed the higher request load without errors or timeouts.

---

### 🔹 Response Time

| **Metric** | **Value** |
|-------------|-----------|
| **Minimum** | 3 ms |
| **Mean** | 126.1 ms |
| **Median (p50)** | 67.4 ms |
| **95th Percentile** | 320.6 ms |
| **99th Percentile** | 415.8 ms |
| **Maximum** | 1,070 ms |

⚡ Most responses were completed in under **0.3 seconds**, which is fast and efficient for an open REST API.

---

### 🔹 HTTP Status Codes

| **Status Code** | **Count** | **Description** |
|------------------|-----------|-----------------|
| **200** | 3,360 | Successful `GET` requests |
| **201** | 1,680 | Successful `POST` requests |
| **Errors** | 0 | No failures recorded |

✅ The high number of `2xx` codes confirms consistent uptime and stability during all test phases.

---

## 📉 Graph Interpretation (Artillery Cloud)
<p align="center">
  <img src="https://github.com/user-attachments/assets/69b9b09c-7817-4fe4-a743-5b3afed799d0" alt="Artillery Cloud Graph" width="750"/><br>
  <em>Figure: Artillery Cloud graph showing load test metrics</em>
</p>


| **Metric** | **Interpretation** |
|-------------|--------------------|
| **Request Rate Graph** | Shows consistent increase across phases, confirming stable ramp-up. |
| **Response Time (p95)** | Slight rise during heavy load, but remains within acceptable range. |
| **Virtual Users Graph** | Demonstrates smooth user scaling and proper concurrency simulation. |

---

## 🧠 Result Interpretation and Discussion

The system remained **responsive and reliable** through all test stages.  
No requests failed, and latency stayed below **500 ms** for nearly all interactions.  
Occasional response spikes (around **1 second**) appeared only in the 99th percentile — normal during high concurrency.

This result demonstrates that **JSONPlaceholder’s API infrastructure** is resilient and capable of handling steady traffic.

---

### ⚠️ Identified Bottlenecks

| **Observation** | **Impact** |
|------------------|------------|
| Minor latency spikes during heavy load | Negligible; short-lived and within expected tolerance |
| Lack of backend metrics | Could not monitor CPU/memory since the API is public |
| Network delay variance | Slight changes due to routing and external latency factors |

---

## 🧭 Recommendations and Test Plan Justification

### 💡 Recommendations for Real Scenarios

- Add **caching and CDN layers** to optimize repeated request delivery.  
- Integrate **Prometheus** or **Grafana** for system-level monitoring (CPU, RAM).  
- Conduct **stress** and **soak tests** to identify maximum capacity and memory leaks.  
- Run tests from **multiple regions** to study global latency performance.  

---

### 📘 Test Plan and Tool Justification

| **Aspect** | **Justification** |
|-------------|-------------------|
| **Test Design** | Gradual ramp-up mimics real-world behavior, avoiding traffic spikes. |
| **Tool Selection** | Artillery chosen for clarity, YAML-based config, and detailed percentile tracking. |
| **Industry Practice** | Follows ISO/IEC 25010 and ISTQB testing guidelines for performance evaluation. |
| **Evidence Collected** | Data shows stable throughput, consistent latency, and zero error rate. |

The approach aligns with **performance engineering best practices** and shows Artillery’s reliability in producing reproducible results.

---

## 🧾 Justification Based on Industry Standards

The testing plan and conclusions align with **industry best practices** for performance testing:

- Gradual load ramping ensures reliable data without artificial stress spikes.  
- Percentile metrics (**p95**, **p99**) provide realistic latency insights beyond averages.  
- Zero error rate confirms **strong API reliability**.  
- Visualization and documentation meet **DevOps and QA** reporting standards.

These findings demonstrate professional-level application of empirical testing and analysis methods suitable for **production-grade API evaluation**.

---

## 🏁 Conclusion

The load testing results on the **JSONPlaceholder API** confirm that the system remains **stable and responsive** even under increasing load.  
Across all three phases, a total of **5,040 requests** were executed with **no failures** and an **average response time of 126 ms**.

This indicates:

- ✅ The API can handle concurrent user requests effectively.  
- 🧩 Artillery is a dependable tool for replicating real-world load patterns.  
- ⚙️ Proper test design and gradual load increments ensure meaningful, accurate insights.  

Overall, this project successfully demonstrates how **Artillery** can be used to measure **performance stability**, identify **bottlenecks**, and validate **API reliability** in a realistic testing environment.

---














