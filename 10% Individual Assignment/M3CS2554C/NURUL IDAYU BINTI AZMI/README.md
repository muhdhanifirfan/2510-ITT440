<h1 align="center"> ⚙️ Website Capacity Testing Using K6 🧰 </h1>
<img width="1280" height="719" alt="image" src="https://github.com/user-attachments/assets/cdac8a55-346d-4a1c-8b1d-fd8499924830" />

---
### 🎯 Prepared for: MR. SHAHADAN BIN SAAD

**Name: NURUL IDAYU BINTI AZMI**  
**Student ID: 2025156453**  
**Group: CDCS2554C**  
**Subject: ITT440 - Network Programming**  

---

## 1. Introduction

<img width="900" height="681" alt="image" src="https://github.com/user-attachments/assets/cd379d19-6437-46e6-a66a-a4973900b595" />


This report focuses on capacity testing of a web application using Grafana k6. Capacity testing aims to determine the maximum number of concurrent users or requests a system can handle before performance degrades or failures occur. In this study, the target system is the Fake REST API hosted at https://fakerestapi.azurewebsites.net/, which simulates typical REST-based API operations.

---

## 2. Objectives

The objective of this test is to perform capacity testing on the target web API to identify the system’s upper performance limit. Specifically, the test measures how response time, throughput, and error rate change as the number of virtual users (VUs) increases.

---

## 3. Test Plan and Methodology

| Type | Content |
|----------------|--------------------|
| Testing type | Capacity Testing | 
| Tool name | k6 (command-line load testing tool |
| Target | https://fakerestapi.azurewebsites.net/ |
| Test duration | 10 seconds per scenario |
| Virtual users | 100, 1000, 2000, 3000, 4000,(for comparison) | 
  
---

## 4. Test Environment Setup

**System Configuration:**
- Operating System: Windows 11  
- Processor: Intel i5 processor 
- RAM: 8 GB  
- Internet Connection: Stable broadband

---

## 5. Test Setup Configuration

The test was conducted using k6, written in JavaScript (.js) format.
The following code defines the test scenario, including the target website URL and virtual user configuration

<img width="834" height="287" alt="image" src="https://github.com/user-attachments/assets/7a3889ee-d81f-4e42-8823-58ed496c6ccd" />

In this experiment, five separated scripts were written in JavaScript (.js) format where each script simulated 10, 1000, 2000, 3000, and 4000 concurrent virtual users respectively, with each test running for 10 seconds. Above is one of the example coding that include 100 virtual users in 10 seconds.


The k6 testing was performed using the command:

<img width="512" height="30" alt="image" src="https://github.com/user-attachments/assets/7789cf47-43d2-4799-9485-8bf34f8674f5" />


This command runs the k6 test script named test100.js, simulating the defined virtual users (VUs) and test duration. The --out csv=results/output100.csv option exports the test results in CSV format and saves them in the results folder for further analysis.

---

## 6. Result Capacity Testing

| Test | VUs | Avg (ms) | P95 (ms) | Max (ms) | Req/s | Error % |
|--------------|-------|---------|--------|-------|-------|------|
| Capacity 100 | 100 | 989.30 | 1690 | 3090 | 37.79 | 0.00 |
| Capacity 1000 | 1000 | 10574.46 | 18690 | 38180 | 24.90 | 0.20 |
| Capacity 2000 | 2000 | 3504.95 | 16850 | 37650 | 49.92 | 32.49 |
| Capacity 3000 | 3000 | 5731.73 | 18960 | 32070 | 51.56 | 43.58 |
| Capacity 4000 | 4000 | 4124.37 | 18020 | 37570 | 84.60 | 37.97 |

---

## 7. Graphs and Data Analysis

### Average Response Time
<img width="650" height="377" alt="image" src="https://github.com/user-attachments/assets/6ffefc9e-bea2-4f54-8cb7-7fa60534326d" />

The average response time represents how long the server takes to respond to user requests under different levels of load. In this capacity testing, the average latency increased significantly as the number of virtual users (VUs) rose from 100 to 1000, with the mean response time jumping from 989 ms to 10,574 ms. This sharp increase indicates that the system began experiencing  queuing delays as the number of concurrent requests grew, suggesting that the server’s available processing capacity or bandwidth was being stretched.

Interestingly, when the number of users increased further to 2000, 3000, and 4000 VUs, the average response time dropped again, ranging between 3504 ms to 5731 ms. This behavior appears counterintuitive, as one would normally expect response times to keep rising under heavier load.

Overall, the response time results show that the system started to slow down when more users were added. After a certain point, the performance seemed to stabilize, possibly because the system adjusted to the heavy load. However, this improvement did not mean the system was fully stable, as shown in the Error Rate section, some requests still failed or timed out. This means the recovery was only partial and temporary.

### Error Percentage
<img width="622" height="375" alt="image" src="https://github.com/user-attachments/assets/6fc733b3-65cb-415d-bbb8-ddc8014b100b" />

The error percentage metric indicates the proportion of failed requests compared to the total number of requests made during the test. This is a critical measure for identifying when a system begins to fail or become unreliable under increasing load.

In the results, no errors were observed at 100 virtual users (VUs), which confirms that the Fake REST API can handle low levels of traffic efficiently and respond successfully to all incoming requests. However, at 1000 VUs, errors began appearing (0.2%), indicating the system was nearing its limit.

When the load increased to 2000 and 3000 VUs, the error rate jumped to 32.49% and 43.58%, showing that the server could not process all requests successfully. This suggests the Fake REST API started to become overloaded or reached its resource capacity, resulting in request timeouts or dropped connections.

At 4000 VUs, the error percentage slightly dropped to 37.97%, possibly because the system rejected requests faster instead of letting them time out. Overall, this shows that the maximum stable capacity for the API is around 1000 VUs, as performance degrades rapidly beyond that point.
