# 🧪 WordPress Load Test using BlazeMeter

## 📖 Overview
This project demonstrates a basic **load testing** process on a WordPress website using **BlazeMeter (based on Apache JMeter)**.  
The goal of this test is to analyze how a WordPress site performs under different user loads — focusing on response time, throughput, and error rate

---

## ⚙️ Test Configuration

| Parameter | Details |
|------------|----------|
| **Tool Used** | BlazeMeter  |
| **Test Type** | URL Test |
| **Target Website** | [https://wp-themes.com/twentytwentyfour/](https://wp-themes.com/twentytwentyfour/) |
| **Number of Virtual Users (VU)** | 10 |
| **Test Duration** | 5 minutes |
| **Location** | Asia Southeast (Singapore, Google) |
| **Ramp-up Time** | Default (BlazeMeter handles automatically) |

---

## 🎯 Test Objectives
- Measure the average response time of the WordPress site.  
- Observe throughput (hits per second).  
- Check for any failed requests or errors during high load.  
- Analyze server behavior during multiple simultaneous connections.

---

## 📊 Test Results

> 📌 <img width="1283" height="112" alt="image" src="https://github.com/user-attachments/assets/e9675d04-4dcc-480d-95ac-7d3657054cbd" />

### 🔹 Summary Report
| Metric | Result |
|---------|---------|
| **Max Users** | `10` |
| **Average Throughput (Hits/s)** | `27.03` |
| **Error Rate** | `0%` |
| **Average Response Time** | `336.32 ms` |
| **90th Percentile Response Time** | `363 ms` |
| **Average Bandwidth** | `3.17 MiB/s` |

🖼️ 

---

### 🔹 Timeline Report (Response Time vs Load)
🖼️ Graft for Load Time <br>
<img width="609" height="406" alt="image" src="https://github.com/user-attachments/assets/dc200594-aa9f-43d1-85ec-407a9c89ea5a" />

🖼️ Graft for Respon Time <br>
<img width="594" height="406" alt="image" src="https://github.com/user-attachments/assets/4088d0a7-7963-4546-ae97-154a97e72d53" />


---

### 🔹 Request Statistics
🖼️ Graft for all the data that been gather
<img width="1920" height="1160" alt="timeline charts" src="https://github.com/user-attachments/assets/c6138158-dc9e-4abc-b538-1330e2d398fb" />


---

## 🧠 Analysis
- The average response time stayed below **400 ms**, which indicates that the website handled 10 users efficiently.  
- There were **no errors**, showing good server stability.  
- Throughput (hits per second) remained consistent, meaning the site could sustain the simulated traffic.  
- Overall performance was **stable and responsive** under the given test conditions.

---

## 🚀 Conclusion
The BlazeMeter test results show that the selected WordPress site performs well under a moderate load of 10 virtual users.  
For future improvements, you can:
- Increase the number of users to test scalability.  
- Try running tests from multiple regions.  
- Include login or comment interactions to simulate real user behavior.

---

## Video Demo
For the demo how to use BlazeMeter to make a load test on WordPress you can watch the video via the link below:
https://youtu.be/xP7-TOZOCJ8?si=1P-AY5u7uzC875TU
