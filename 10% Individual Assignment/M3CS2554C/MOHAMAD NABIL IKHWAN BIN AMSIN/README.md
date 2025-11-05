# 🧪 Comprehensive Web Application Performance Testing & Analysis Using Apache JMeter

![Apache JMeter](https://img.shields.io/badge/Apache%20JMeter-v5.6%2B-orange?logo=apache&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![License](https://img.shields.io/badge/License-MIT-blue)

## 📝 Project Overview
This repository documents a **performance testing project** conducted on a publicly accessible web application using **Apache JMeter**. The goal was to evaluate system stability, responsiveness, and scalability under different load conditions by performing:

- **Load Test**
- **Stress Test**
- **Spike Test**

The results from these tests were analyzed to identify performance bottlenecks and provide recommendations for improvement.

---

## 🎯 Objectives
- Design and execute realistic performance test scenarios.
- Collect and analyze key performance metrics such as *response time*, *throughput*, and *error rate*.
- Interpret findings to assess system reliability and scalability.
- Document the testing methodology and insights for professional review.

---

## 🧰 Tool Used: Apache JMeter

<img width="500" height="650" alt="image" src="https://github.com/user-attachments/assets/f9c49813-b859-4d18-8674-243f1085f6ae" />


### 📘 What is Apache JMeter?
**Apache JMeter** is an open-source tool developed by the **Apache Software Foundation**, used primarily for **performance and load testing** of web applications. It simulates multi-user interactions and provides detailed performance reports through built-in listeners and custom extensions.

### 🔧 Key Features Leveraged
- 🧍‍♂️ **Thread Groups**: Simulated concurrent users.
- 🔁 **HTTP Samplers**: Sent requests to target endpoints.
- ⏱️ **Timers & Controllers**: Made user behavior realistic.
- 📊 **Listeners**: Captured metrics like response time, throughput, and error rate.
- 📁 **CSV Export**: Exported raw performance data for external analysis.

### 🧩 Why JMeter?
| Reason | Benefit |
|--------|---------|
| Open-source | Free and widely supported |
| Protocol support | HTTP(S), REST, FTP, JDBC, etc. |
| Extensibility | Plugins and CI/CD compatibility |
| GUI + CLI Support | Easy to use and test automation-friendly |

---

## 💻 Hardware Configuration

The performance tests were conducted on a personal workstation equipped with the following specifications:

| Component | Specification |
|------------|----------------|
| **Processor (CPU)** | AMD Ryzen 5 5500U with Radeon Graphics (2.10 GHz) |
| **Memory (RAM)** | 8 GB DDR4 |
| **Storage** | 512 GB NVMe SSD |
| **Network** | 300 Mbps Stable Broadband Connection |
| **Operating System** | Windows 11 Pro (64-bit) |

---

> ⚙️ The chosen hardware configuration ensured sufficient computational resources to simulate multiple concurrent users in Apache JMeter without client-side bottlenecks. It provided a stable environment for executing load, stress, and spike test scenarios effectively.

## 📋 Test Scenarios Conducted
| Test Type | Description | Key Purpose |
|------------|-------------|--------------|
| **Load Test** | Simulates expected number of users accessing the application | Assess baseline performance |
| **Stress Test** | Pushes system beyond normal capacity | Identify breaking point and behavior under pressure |
| **Spike Test** | Sudden sharp increase in load | Test system recovery and elasticity |

Each test plan included configured thread groups, realistic user think times, and controlled ramp-up periods.

---

## 📊 Performance Metrics
| Metric | Description |
|---------|-------------|
| **Avg. Response Time (ms)** | Time taken for server to respond to requests |
| **Throughput (req/sec)** | Requests handled per second |
| **Error Rate (%)** | Percentage of failed requests |
| **Latency** | Delay before receiving the first byte of a response |

Data was visualized using spreadsheets and charts to compare performance across different test types.

---

## 📈 Insights & Recommendations
- 🔍 The system handled moderate load well, but performance degraded sharply under stress.
- ⚠️ Database queries caused bottlenecks at high loads.
- 💡 Suggested optimizations:
  - Implement caching
  - Enable load balancing
  - Improve database indexing

---

## 💼 Repository Contents
```plaintext
├── test_plans/       # JMeter .jmx files
├── results/          # CSV/HTML reports for each test
├── charts/           # Visualized performance charts
├── README.md         # Project documentation
└── LICENSE
