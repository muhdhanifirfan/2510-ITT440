# 🐻Web Application Performance Testing & Analysis Using Grafana K6
***

### 🧑 Name: MOHAMAD AMIRUL AIMAN BIN ZAINAL
### 🎓 Student ID: 2025140465
### 📄 Course: ITT440
### 👥 Group: M3CS2554C
***

## 📘 Introduction
Performance testing is essential to evaluate how a system behaves under different load conditions. This project focuses on testing the public API **https://httpbin.org** using **Grafana k6**, an open-source performance testing tool. The purpose is to observe how the API responds when subjected to various levels of traffic and identify any performance issues that may occur.

<br>Objective<br>
Two types of testing were conducted:
- **Smoke Testing** – to verify the API’s basic stability and responsiveness under light to moderate load.  
- **Breakpoint Testing** – to progressively increase the load and determine the system’s performance limit.  
<br><br>

## 🛠️ Tool Selection 
<img width="1200" height="675" alt="image" src="https://github.com/user-attachments/assets/76923bbf-370c-4469-a47f-e2d8d01ead94" />
<br><br>
Grafana k6 was chosen as the main performance testing tool because it is open-source, easy to use, and supports various testing types such as smoke and breakpoint tests. It allows scripting in JavaScript and effectively measures system performance and reliability.
The tool was chosen because it offers:

- 🟢 Easy scripting and configuration using **JavaScript**.  
- ⚡ Real-time monitoring of performance metrics such as **response time**, **error rate**, and **throughput**.   

## ⚙️ Installation Steps for Grafana k6 (Windows)
1) Install Chocolatey (Package Manager)
2) Install Grafana k6 using Chocolatey :
   
   choco install k6 -y
   
4) Run a Quick Test:
   
   k6 run https://test.k6.io

5) Ready to Use

   k6 run smoke-test.js
   k6 run breakpoint-test.js
<br><br>

## 🌐 Target Application Description
The target application for this project is https://httpbin.org ,a free and public HTTP request and response service. It is commonly used for testing, 
debugging, and experimenting with HTTP methods such as GET, POST, PUT, and DELETE. The website returns data about the requests it receives, making it 
suitable for performance and API testing without affecting any real production system.
<br><br>

## 🛠️ Test Environment

This section details the hardware and software used to execute the performance test, ensuring the results are reproducible.

| Component | Details |
| :--- | :--- |
| **Test Machine** | IdeaPad Gaming 3 |
| **CPU** | 11th Gen Intel(R) Core(TM) i5-11300H @ 3.10GHz (3.11 GHz)|
| **RAM** | 8GB DDR4 |
| **Tool** | Grafana k6 v1.3.0 |
| **Test Type** | Smoke and Breakpoint Testing |
| **Target Application URL** | 'https://httpbin.org' |

## 💻 Test Plan and Configuration
| **Test Type**          | **Configuration Details**                                                                                                                                        |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Smoke Test**         | 50 Virtual Users (VUs), 45-second duration. Purpose: to verify basic system stability and response under a small, short load.                                    |
| **Breakpoint Test**    | Gradual load increase from 50 to 250 VUs, 20 seconds per stage. Purpose: to identify the maximum load the application can handle before performance degradation. |
| **Request Type**       | HTTP GET requests sent to `https://httpbin.org/get`.                                                                                                             |
| **Metrics Observed**   | Response time (latency), error rate, and throughput (requests per second).                                                                                       |
| **Threshold Criteria** | 95% of requests must complete under 1.5 seconds with less than 5% failed requests.                                                                               |
| **Script Language**    | JavaScript (k6 test scripts).                                                                                                                                    |

## 📊 Key Metrics Measured

| **Metric** | **Description** |
|-------------|-----------------|
| **Response Time (ms)** | Time taken for the server to respond to a request. |
| **Requests per Second (RPS)** | Number of requests handled each second. |
| **Error Rate (%)** | Percentage of failed requests during testing. |
| **Throughput** | Total data sent and received in the test. |
| **95th Percentile (p95)** | Response time met by 95% of all requests. |
| **Virtual Users (VUs)** | Number of users simulated during testing. |

## 💻 Smoke Test Configuration
```js
import http from 'k6/http';
import { check, sleep } from 'k6';

// Smoke Test Configuration
export let options = {
  vus: 50,                  
  duration: '45s',          
  thresholds: {
    http_req_failed: ['rate<0.05'],    
    http_req_duration: ['p(95)<1500'],
  },
};

export default function () {
  const res = http.get('https://httpbin.org/get');
  check(res, { 'status is 200': (r) => r.status === 200 });
  sleep(1);
}
```
## 💻 Breakpoint Test Configuration
```js
import http from 'k6/http';
import { check, sleep } from 'k6';

// Breakpoint Test Configuration
export let options = {
  stages: [
    { duration: '20s', target: 50 },   // ramp up to 50 VUs
    { duration: '20s', target: 100 },  // ramp up to 100 VUs
    { duration: '20s', target: 150 },  // ramp up to 150 VUs
    { duration: '20s', target: 200 },  // ramp up to 200 VUs
    { duration: '20s', target: 250 },  // ramp up to 250 VUs
    { duration: '20s', target: 0 },    // ramp down
  ],
  thresholds: {
    http_req_failed: ['rate<0.10'],     
    http_req_duration: ['p(95)<2000'],  // 
  },
};

export default function () {
  const res = http.get('https://httpbin.org/get');  

  // Check response status
  check(res, {
    'status is 200': (r) => r.status === 200,
  });

  sleep(1); 
}
```
<br><br>
## 📊 Performance Result and Analysis
### Smoke Test Summary

| **Metric** | **Result** | **Description / Analysis** |
|-------------|------------|-----------------------------|
| **Virtual Users (VUs)** | 50 | Simulated 50 users as planned. |
| **Duration** | 45 seconds | Test ran for the configured time. |
| **Requests Completed** | 990 | Total requests processed. |
| **Average Response Time** | 1.28 seconds | Stable response time. |
| **95th Percentile (p95)** | 2.96 seconds | Slightly above the 1.5s target. |
| **Failed Requests** | 1.81% (18 of 990) | Within acceptable limit (<5%). |
| **Data Received** | 650 kB | Total data received. |
| **Data Sent** | 74 kB | Total data sent. |

### Breakpoint Test Summary
| **Metric** | **Result** | **Description / Analysis** |
|-------------|------------|-----------------------------|
| **Virtual Users (VUs)** | 250 | Simulated 250 users as configured. |
| **Duration** | 2m 30s | Test executed for the planned duration. |
| **Requests Completed** | 3,900 | All iterations finished successfully. |
| **Average Response Time** | 2.94s | Higher than ideal, may need optimization. |
| **95th Percentile (p95)** | 9.62s | Exceeds 2s target; performance issue detected. |
| **Failed Requests** | 0.61% (24 of 3,900) | Within acceptable failure threshold. |
| **Iteration Duration (avg)** | 4.03s | Indicates moderate server processing time. |
| **Data Received** | 2.8 MB | Normal data throughput. |
| **Data Sent** | 319 kB | Consistent network output. |
<br><br>

## 📈 Visual Comparisons
<img width="1562" height="980" alt="image" src="https://github.com/user-attachments/assets/5698bdfb-d961-4aa1-9e44-eee228f96108" />

<br><img width="1566" height="980" alt="image" src="https://github.com/user-attachments/assets/3fd1032e-5d1e-43dd-ad58-31421e984ce6" /><br>
<br><br>
**🧠 Analysis:**  
The **Smoke Test** showed that *https://httpbin.org* handled 50 users smoothly with stable response times (avg 1.28s) and a low error rate (1.81%).  
The **Breakpoint Test** with 250 users remained stable but had slower responses (avg 2.94s, p95 9.62s), indicating performance degradation under heavy load.  

**Overall:**  
⚙️ The system performs well under light load but needs optimization to handle higher concurrency efficiently.
<br><br>

## 🧩 Recommendations
- Optimize backend code and database queries to reduce response latency.  
- Implement caching and load balancing to enhance scalability and performance.  
- Use asynchronous request handling or queueing for better load management.  
- Increase server resources or use auto-scaling during peak load periods.  
- Continue running periodic performance tests to track improvements.  
- Monitor key metrics (response time, error rate, throughput) with dashboards for early issue detection.
<br><br>
## 🧾 Conclusion
This project evaluated the performance of https://httpbin.org using Grafana k6 through Smoke and Breakpoint Testing. The smoke test showed that the 
API remained stable under a light load of 50 virtual users, with low error rates and acceptable response times. The breakpoint test revealed that 
performance started to decline after around 200 users.

Overall, The use of Grafana k6 provided clear insights into response time, error rate, and system behavior under different traffic conditions
achieving the project’s objective of assessing system performance and reliability.
