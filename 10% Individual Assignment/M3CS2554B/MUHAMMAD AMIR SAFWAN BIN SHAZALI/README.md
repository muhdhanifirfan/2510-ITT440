#### STUDENT NAME : MUHAMMAD AMIR SAFWAN BIN SHAZALI
#### STUDENT ID : 2024963165
### GROUP : M3CS2554B
# 🔍 Spike Testing of JSONPlaceHolder using Grafana k6
### 💥 INTRODUCTION
 <div align="justify"> Performance testing helps determine how a system handles sudden increases in user load. In this project, I conducted a spike test using Grafana k6, a modern open-source load testing tool. The spike test measures how well a system responds to an unexpected surge of traffic in a short period of time. For this test, I used JSONPlaceholder, a free online REST API commonly used for testing and prototyping. It simulates real-world API responses without affecting a live production system. The purpose of this test is to observe how the API behaves when it suddenly receives a large number of requests — checking for slowdowns, failed requests, or performance recovery after the spike ends. </div>

---
### OBJECTIVES
- To simulate a sudden spike in virtual users sending requests to the JSONPlaceholder API using Grafana k6.
- To measure the system’s response time, throughput, and error rate during and after the spike period.
- To observe how quickly the system recovers after the sudden increase in load.
- To analyze the test results and provide recommendations for improving performance and stability.

---
### Tool Used:Grafana K6

<p align="center">
<img width="500" height="243" alt="image" src="https://github.com/user-attachments/assets/5df4a326-0bf7-4b27-8fdc-4072251865ba" />
Grafana k6 is a modern open-source load testing tool designed for testing APIs, microservices, and web applications.
Key reasons for choosing k6:
- It supports scripting in JavaScript, which is easy to customize.
- Command-line interface works efficiently in Ubuntu.
- Real-time results and integration with Grafana dashboards.
- Lightweight yet capable of handling thousands of virtual users.

---
### Type of Test: Spike Test

A spike test is a type of performance test where the number of virtual users suddenly increases to a high level and then rapidly drops.
#### Purpose:
To evaluate how the system behaves when subjected to a sharp load increase — checking for crashes, slow responses, or recovery delays.

---
### Target Web Application: JSONPlaceholder API

<p align="center">
<img width="500" height="243" alt="image" src="https://github.com/user-attachments/assets/a341382c-47fc-4092-a9d8-a3e14e23c960" />
URL: https://jsonplaceholder.typicode.com/posts
This is a public REST API commonly used for testing and prototyping. It safely allows simulated requests without impacting any real systems, making it an ethical and legal target for performance testing.

---
### Test Environment Setup

Operating System: Ubuntu 22.04 LTS
Tool: Grafana k6 (installed via apt)
Target URL: JSONPlaceholder (/posts)

Command Used:
import http from "k6/http";
import { sleep } from "k6";

export let options = {
  stages: [
    { duration: "30s", target: 10 },   // warmup
    { duration: "25s",  target: 100 },  // spike
    { duration: "30s", target: 10 },   // recovery
    { duration: "20s",  target: 0 },    // cooldown
  ],
};

export default function () {
  http.get("https://jsonplaceholder.typicode.com/posts");
  sleep(1);
}

---
### Test Hypothesis

It is expected that JSONPlaceholder, being a mock API service, will handle the spike load efficiently without any failed requests. Response time may slightly increase during the 100-VU spike but should remain stable and below 1 second for most requests.

---
## Test Plan

| **Stage**    | **Duration** | **Target Virtual Users (VUs)** | **Stage Name**        | **Expected Behaviour** |
| ------------ | ------------ | ------------------------------ | --------------------- | -----------
| **Warm-up**  | 30 seconds   | 10 VUs                         | Normal baseline load  | Starts with a small number of users to gradually warm up the system, establish a connection, and record normal response   times before the spike. |
| **Spike**    | 25 seconds   | 100 VUs                        | Sudden load surge     | A rapid increase from 10 to 100 virtual users to simulate a sudden burst of traffic (e.g., flash sale, viral event, or unexpected user influx). Tests how the system reacts to a sudden spike. |
| **Recovery** | 30 seconds   | 10 VUs                         | Load reduction        | Reduces load back to normal levels to observe how quickly and smoothly the system recovers and stabilizes after the high-stress period. |
| **Cooldown** | 20 seconds   | 0 VUs                          | Test completion       | Gradually reduces all users to zero, ending the test while monitoring if performance metrics return to baseline. |
