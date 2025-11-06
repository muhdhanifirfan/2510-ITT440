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

<img width="1200" height="1162" alt="image" src="https://github.com/user-attachments/assets/7b9dcf5a-caf2-4d66-9772-87941762961b" />

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
**k6 run --out csv=results/output100.csv scripts/test100.js**

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







