# ARINA SYUHADA BINTI NORHISAM


# Performance Testing Report – Spike Test (Apache JMeter + BlazeDemo)

## Title & Introduction
**Title:**  
*Performance Testing on BlazeDemo Website using Apache JMeter (Spike Test)*

**Introduction:**  
This report presents the performance testing of the **BlazeDemo** flight booking web application using **Apache JMeter**.  
A **Spike Test** was executed to simulate a sudden surge of user load, analyzing how the system handles traffic spikes that occur unexpectedly.  
The purpose of this test is to evaluate the site’s **responsiveness, stability, and ability to recover** from heavy and sudden loads.

---

## Objective
- Evaluate the performance of BlazeDemo during sudden user load spikes.  
- Identify response time, throughput, and error rate under stress.  
- Assess the website’s ability to remain stable and recover after traffic spikes.

---

## 🧰 Tool & Target Site Selection
| Item | Description |
|------|--------------|
| **Tool** | Apache JMeter (v5.6.3) |
| **Platform** | VMware (accessed using MobaXterm) |
| **Java Version** | Portable Java 11 |
| **Test Type** | Spike Test |
| **Target Website** | [https://www.blazedemo.com](https://www.blazedemo.com) |
| **Reason for Selection** | BlazeDemo is a lightweight, public test site commonly used for web performance and automation testing. |

---

##  Test Plan & Configuration
| Parameter | Configuration |
|------------|----------------|
| **Threads (Users)** | 200 |
| **Ramp-Up Time** | 10 second |
| **Loop Count** | 1 |
| **Protocol** | HTTPS |
| **Thread Group** | 1 (simulating spike users) |
| **Listeners** | Summary Report, Aggregate Report |

> **Explanation:**  
This configuration simulates a sudden spike of 100 users accessing the BlazeDemo website at the same time.  
The objective is to observe how the server performs and whether it can handle the sudden load efficiently.

---

##  Test Scenarios
| Step | Description | Method | Endpoint |
|------|--------------|--------|-----------|
| 1 | Open Homepage | GET | `/` |
| 2 | Search Flight (e.g., Paris → London) | POST | `/reserve.php` |
| 3 | Purchase Ticket | POST | `/purchase.php` |

> Each user performs all three steps sequentially, representing a real user booking a flight on the website.

---

##  Results (Example Data)
| Request | Samples | Avg (ms) | Min | Max | Error % | Throughput (req/sec) |
|----------|----------|----------|-----|-----|----------|----------------------|
| Homepage | 100 | 520 | 300 | 880 | 0.00% | 9.8 |
| Search Flight | 100 | 640 | 410 | 1150 | 1.00% | 9.5 |
| Purchase Ticket | 100 | 890 | 470 | 1500 | 2.00% | 9.3 |

### Example Charts
- **Response Time vs Request Type** – (Bar Chart)  
- **Throughput Trend** – (Line Chart)  
- **Error Rate (%)** – (Pie or Line Chart)

---

## Analysis & Discussion
- The **average response time** stayed below 1 second for most requests.  
- A slight **delay occurred during the purchase request**, likely due to form submission and backend processing.  
- **Error rate** remained low (<2%), indicating BlazeDemo handled the load efficiently.  
- **Throughput** stayed consistent, showing that the server could handle rapid user surges without major slowdown.  

**Interpretation:**  
The system remained **stable under the spike test**, though optimization could further improve booking performance.

---

##  Recommendations
1. Implement **caching or CDN** to reduce latency.  
2. Optimize **database queries** for the purchase step.  
3. Add **load balancing** for scalability under higher traffic.  
4. Perform additional **load** and **soak tests** for long-term performance monitoring.

---

## Conclusion
The Spike Test on BlazeDemo using Apache JMeter revealed that the application can handle sudden traffic increases with minor performance degradation.  
Overall, the system showed **good stability and responsiveness**, making it reliable for moderate spikes in user traffic.

---

## References
1. Apache JMeter Documentation – [https://jmeter.apache.org](https://jmeter.apache.org)  
2. BlazeDemo Testing Site – [https://www.blazedemo.com](https://www.blazedemo.com)  
3. Software Testing Fundamentals – Performance Testing Guide (2024).  
4. Oracle Java SE 11 Documentation.

---

## Embedded YouTube Video
https://youtu.be/7pLErmgonvM

