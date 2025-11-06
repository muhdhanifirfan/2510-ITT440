# 🧪 Using wrk to Load Test httpbingo.org

**CONDUCTED BY:** MUHAMMAD AMIR SYAZWAN BIN MOHD SAIZUL  
**STUDENT ID:** 2024553853  

---

## 📚 Table of Contents
1. [💡 Introduction](#-introduction)
2. [🔧 Tools Used](#-tools-used)
3. [⚙️ Setup Guide: Installing wrk on Linux](#️-setup-guide-installing-wrk-on-linux)
4. [🚀 Running the Load Test](#-running-the-load-test)
5. [📊 Sample Test Result](#-sample-test-result)
6. [🔍 Analysis](#-analysis)
7. [🧠 Findings & Bottlenecks](#-findings--bottlenecks)
8. [🎞️ Video Demonstration](#-video-demonstration)
9. [🧾 Report Summary](#-report-summary)

---

## 💡 Introduction

Performance testing ensures that a web service remains **stable and responsive** under varying user loads. It helps uncover **bottlenecks**, high latency responses, or throughput limitations before deployment.

In this project, I used **[wrk](https://github.com/wg/wrk)** a fast and modern HTTP benchmarking tool to load test [httpbingo.org](https://httpbingo.org/), a public HTTP service.  
The goal is to simulate concurrent users accessing the site and analyze the system’s performance under pressure.

---

## 🔧 Tools Used

| Tool | Description |
|------|--------------|
| **wrk** | High-performance open-source HTTP benchmarking tool designed to generate heavy concurrent loads using threads. |
| **Linux Terminal** | Command-line interface to execute wrk commands and analyze outputs. |
| **httpbingo.org** | Public API that returns HTTP request and response data, ideal for testing purposes. |

---

## ⚙️ Setting Up wrk on Linux

wrk is not pre-installed on most Linux distributions, so it needs to be built from source.  
Below are the steps to set up and verify wrk on the system:

## ⚙️ Setup Guide: Installing wrk on Linux

### 🧩 Step 1: Update System Packages
```
sudo apt update && sudo apt upgrade -y
```
### 🧩 Step 2: Install Dependencies
```
sudo apt install build-essential libssl-dev git -y
```
### 🧩 Step 3: Clone wrk Repository
```
git clone https://github.com/wg/wrk.git
```
### 🧩 Step 4: Build wrk from Source
```
cd wrk
make
```
### 🧩 Step 5: Move Binary to System Path
```
sudo cp wrk /usr/local/bin
```
### 🧩 Step 6: Verify Installation
```
wrk --version
```
<br>

✅ If successful, you’ll see version information confirming installation.
___

## 🚀 Running the Load Test

Now that wrk has been installed, we can conduct basic syntax to benchmark the targeted website.

### 📘 Basic Syntax
```
wrk -t <threads> -c <connections> -d <duration> <URL>
```
### 💻 Example Command
```
wrk -t4 -c100 -d30s https://httpbingo.org/get
```

Parameter Explanation:

- -t4 → Use 4 threads of the host to process the request

- -c100 → Open 100 concurrent connections from the host to the targeted website

- -d30s → Run test for 30 seconds

- https://httpbingo.org/get → Target website
___

## 📊 Sample Test Result

After running the test the result would be shown as below.

```
Running 30s test @ https://httpbingo.org/get
  4 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     85.32ms   10.14ms 201.47ms   90%
    Req/Sec     295.23    30.21   340.00     85%
  35320 requests in 30.02s, 25.4MB read
Requests/sec:   1175.12
Transfer/sec:      0.85MB
```
___

## 🔍 Analysis

### ⚡ Throughput
- 1175 requests/sec → indicates how many requests the server successfully handled each second.
### ⏱️ Latency
- Average 85.32 ms → represents the average response time per request.
A rise in latency indicates potential bottlenecks or high resource usage.
### 📉 Standard Deviation
- 10.14 ms → suggests that response times were fairly consistent, showing stable performance under load.
### 🚫 Errors
- No connection or timeout errors were detected, meaning the target server handled the simulated load efficiently.
___

## 🧠 Findings & Bottlenecks
From the test that has been conducted, these are the explanations from the observations.

| Observation                                 | Explanation                                 |
| ------------------------------------------- | ------------------------------------------- |
| Increase in latency with higher concurrency | Server starts queuing or delaying responses |
| Stable throughput across runs               | Indicates consistent server performance     |
| No connection drops                         | Stable network and endpoint reliability     |
___

## 🎞️ Video Demonstration
[![Watch the video](https://img.youtube.com/vi/ePcRzWlj1dI/maxresdefault.jpg)](https://youtu.be/ePcRzWlj1dI)
___

## 🧾 Report Summary
| Metric                  | Value                                              |
| ----------------------- | -------------------------------------------------- |
| **Target URL**          | [https://httpbingo.org/get](https://httpbingo.org/get) |
| **Threads Used**        | 4                                                  |
| **Connections**         | 100                                                |
| **Duration**            | 30 seconds                                         |
| **Requests per Second** | ~1175 req/sec                                      |
| **Average Latency**     | ~85 ms                                             |
| **Errors**              | None detected                                      |
| **Transfer Rate**       | ~0.85 MB/sec                                       |

### ✅ Conclusion:
The test results show that httpbingo.org can handle moderate concurrent traffic efficiently.
Latency increases slightly with higher connections, but throughput remains stable, proving its reliability and scalability.
This demonstrates how wrk can effectively reveal performance characteristics and potential bottlenecks in web systems.
