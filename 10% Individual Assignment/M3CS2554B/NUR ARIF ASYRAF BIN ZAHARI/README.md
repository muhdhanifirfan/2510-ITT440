# Comprehensive Web Application Performance Testing & Analysis
---

### STUDENT NAME : NUR ARIF ASYRAF BIN ZAHARI
### ITT440 - INDIVIDUAL ASSIGNMENT
### GROUP : M3CS2554B
---

# 🔍 Stress Testing on DummyJSON using Artillery
---

## Introduction

The assignment demands Artillery execution of a stress test on DummyJSON API to evaluate its operational stability when facing high traffic volumes. The test evaluates API performance under heavy traffic conditions to detect rate limit violations that result in HTTP 429 errors and assesses its recovery time after traffic decreases. The test evaluates API scalability through performance metrics which include response time and data processing capacity and error frequency during warm-up, high load and recovery phases.

---

## Objectives

- To evaluate the performance and stability of the DummyJSON API under different load conditions.
- To observe how the API responds during warm-up, sustained high load, and recovery phases.
- To identify potential performance bottlenecks or timeout issues under heavy traffic.
- To measure response times, throughput, and error rates for performance analysis.

---

## Tool & Test Selection Justification

<p align="center">
<img width="500" height="243" alt="1_p4IQfjORMIMZtN8SJRjzcA" src="https://github.com/user-attachments/assets/9bcc62c7-bf15-4428-a6d8-d43b25c77ad2" />    

## Performance Testing Tool (Artillery)

The experiment used Artillery because this open-source tool enables simple testing framework designed for HTTP, WebSocket, and API-level testing. Stress testing through YAML script execution. The tool delivers precise measurements of response times and errors while Built-in Cloud dashboard for reporting which is Artillery Cloud generates visual performance graphs for better analysis.

---

<p align="center">
<img width="500" height="497" alt="image" src="https://github.com/user-attachments/assets/51d8c870-99b9-4708-ba60-9dffb25ca339" />

## Target Web Application (DummyJson)

The experiment used DummyJSON because it offers a free stable fake REST API that performs well for performance testing. The API generates realistic data about products and users which enables Artillery to perform simulations of actual API operations. The API generates stable responses which make it perfect for studying system performance and stability during high-stress situations.

---

## Test Environment Setup

| **Component**          | **Details**                                                                        |
| ---------------------- | ---------------------------------------------------------------------------------- |
| **Environment**        | Windows 11 operating system                                                        |
| **Testing Framework**  | Artillery v2.0.26                                                                   |
| **Configuration File** | `stress_test.yml`                                                                  |
| **Execution Method**   | `artillery run stress_test.yml --record --key a9_x5xh12axy495k0pmfhng64nkpf3u2kti` |
| **Target Endpoint**    | [DummyJSON API](https://dummyjson.com) – REST API for fake data testing            |
| **Test Category**      | Stress Test                                                                        |
| **Test Duration**      | 3 minutes, 6 seconds                                                               |
| **Load Pattern**       | Warm-up → Sustained High Load → Recovery                                           |
| **Reporting Platform** | Artillery Cloud Dashboard                                                          |

Test Run URL : https://app.artillery.io/otv0ucti84aw9

---

## Hypothesis Application's Performance

The DummyJSON API will maintain operational stability at normal usage levels but will start to show delayed responses and HTTP 429 rate-limiting errors when handling large numbers of users. The API will experience rising latency and server throttling timeouts when request numbers exceed its maximum processing threshold. The API performance will return to normal after load reduction during the recovery phase because the system failure is not the cause of performance degradation under stress.

---

## Test Plan

| **Phase**                     | **Duration** | **Arrival Rate (Users/sec)** | **Description**                                                                                                            |
| ----------------------------- | ------------ | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Warm-up Phase**             | 30 seconds   | 20 users/sec                 | Begins with moderate virtual user traffic to prepare the DummyJSON API for consistent load testing.                        |
| **Sustained High Load Phase** | 120 seconds  | 150 users/sec                | Applies continuous heavy virtual user traffic to test the API’s stability, response time, and error handling under stress. |
| **Recovery Phase**            | 30 seconds   | 50 users/sec                 | Gradually reduces the number of virtual users to observe how the API performance stabilizes after intense usage.           |

---

## Test Result Summary

| Metric                                  | Result       | Observation                               |
| --------------------------------------- | ---------------- | ------------------------------------------------------------------------------------------- |
| **Total Requests**                      | 100,500          | High number of requests                           |
| **Request Users Rate**                        | 534 users/sec      | Steady high throughput                            |
| **HTTP (200+201) Responses**                  | 73,730  | Majority of requests succeeded      |
| **HTTP 429 Responses**                  | 26,770           | Significant rate-limit errors        |
| **Error Rate (4xx)**                    | 26.7%            | A notable portion of requests failed           |
| **Min Response Time**             | 2 ms             | Some requests were extremely fast |
| **Max Response Time**             | 2,574 ms         | Some requests experienced very high latency       |
| **Median Response Time**          | 22.9 ms          | Typical response time is low                       |
| **95th Percentile** | 290.1 ms         | Most requests completed within acceptable time            |
| **99th Percentile** | 415.8 ms         | Worst-case requests were slower            |
| **Virtual Users Created**               | 20,100           | Large number of users simulated                        |
| **Virtual Users Completed**             | 20,100           | All simulated users completed successfully                     |
| **Virtual Users Failed**                | 0                | No test script errors occurred.                                    |

---

## Performance Summary Observation

### Throughput

- Request Rate: 534 requests/sec
- Total Requests: 100,500
- Observation: High throughput shows the API can handle continuous heavy load.

### Error Rate

- HTTP 2xx Responses: 73,730 (73.4%)
- HTTP 429 Responses (Rate-Limit): 26,770 (26.7%)
- Observation: 27% of requests failed due to throttling, indicating the server limits concurrent requests under stress.

## Raw Data Presentation

<img width="1378" height="566" alt="image" src="https://github.com/user-attachments/assets/cb400c17-8603-4e81-abbe-ba8a2c60ff3d" />
 The evaluation system maintained fast response times throughout the Warm-up period while the load continued to rise. The system maintained 600–900 req/s performance during the Sustained phase while keeping latency at a low level. The system restored its performance to normal levels during Recovery which demonstrated its ability to maintain stability and recover from stress.

---

<img width="1379" height="376" alt="image" src="https://github.com/user-attachments/assets/ebb36622-577c-4923-9283-d6341676d0a6" />
The test system processed 100.5K requests which resulted in fast successful responses with median 23 ms response times and 95% of responses under 290 ms and a maximum response time of 2.5 seconds. The system returned 200/201 responses for 73% of requests but produced 26.7K (26.7%) rate-limit errors which indicated excellent performance with only occasional throttling during high traffic conditions.

## Overall Observation

- The API sustains high throughput efficiently.
- Most responses are fast, but the server triggers rate limiting under heavy load.
- Tail latency indicates some requests may experience delays at peak stress.

---

## Interpretation

| **Section**                        | **Description**                                                                                                                                                                                                                                                                                                                     |
| -----------------------------      | -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  |
| **Interpretation Results**    | - The DummyJSON API handled varying loads effectively with a median response time of 34.8 ms and throughput of 534 req/sec. |
|                               | - HTTP 429 errors appeared during peak load, indicating the API reached its rate limit. |
|                               | - The system recovered quickly, showing good resilience and scalability. |

---

## Identified Bottleneck

| **Section**                   | **Description**                                                                                                                                                                                                                                                                                                               |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Identified Bottlenecks**    | - High HTTP 429 (Too Many Requests) errors (26.7%) show that the rate limit was exceeded under heavy load. |
|                               | - Slight response time increases suggest possible backend or network latency. |
|                               | - These issues limit throughput and scalability during peak conditions. |

---

## Recommendations

### API Performance Improvement:
- Raise rate-limit thresholds to reduce HTTP 429 errors.
- Optimize backend handling for high request loads.
- Add caching to speed up frequent API responses.

### System Scalability Enhancement:
- Apply load balancing to distribute traffic evenly.
- Enable auto-scaling for dynamic resource usage.
- Monitor performance using real-time dashboards.

### Further Testing:
- Run spike tests for sudden load increases.
- Conduct soak tests for long-term stability.
- Validate SLA targets for consistent response times.

---

## Conclusion

The Artillery performance test evaluated the DummyJSON API through various load tests which successfully demonstrated its performance capabilities. The system operated at a stable rate while processing 534 requests per second with an average response time of 34.8 ms. The API showed fast recovery from rate-limited errors which occurred in 26.7% of responses during peak traffic but the system maintained strong scalability and resilience. The system performs well under normal to heavy traffic but additional performance enhancements and extended testing are needed to achieve better long-term stability and reduce rate-limiting events.

---

## **YouTube Demo:** [Click to Watch Demonstration Video][(https://youtu.be/fHesKKUZHLI)](https://youtu.be/NC-dLn--po8)
