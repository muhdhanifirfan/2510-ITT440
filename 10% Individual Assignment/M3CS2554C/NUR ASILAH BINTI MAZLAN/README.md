# Stress Testing on QuickPizza Using Grafana Cloud K6  

**Name:** NUR ASILAH BINTI MAZLAN  
**Student ID:** 2025160559 
**Course Code:** ITT440  
**Course Name:** Network Programming
**Class:** CDCS2554C

---
## **Abstract**
<p align="justify">
This article details the results from a web application stress test on the QuickPizza demo site using Grafana Cloud K6. The purpose of the experiment was to test how the system behaved under progressively increasing concurrent user loads, with the goal of demonstrating performance stability, identifying potential bottlenecks, and observing how the system responded under pressure. This testing was done completely within the Grafana Cloud K6 web app interface rather than running K6 on a local device via Visual Studio Code or Windows Command Prompt to ease the setup time and also in a way to see results in real time. The K6 cloud stress test was initiated by ramping up virtual users (VU) from 1 to 50 concurrent users, which was increased to 75 and 100 users. That was the maximum limit of concurrent users allowed under the Grafana Cloud free-tier plan. The results indicated response times were stable during the test, but one HTTP request timed out due to simulated login credentials being used in the performance test. Overall the system managed concurrent sessions well. 

## 1. Introduction
<p align="justify">
The performance of web applications is fundamentally important to user satisfaction and operational reliability. As applications scale, they must withstand increased traffic without sacrificing responsiveness or stability. Stress testing is one type of non-functional testing that observes how an application performs under extreme conditions. For example, the load will be gradually increased until the system is near or has exceeded its expected limits.
<p align="justify">
For purposes of the experiment, the QuickPizza demo website was chosen as the target system. The demo site provided static and dynamic content such as menu listings, news pages, and login forms. Thus, it was fitting for replicating realistic browsing and transaction activity. Grafana Cloud K6 is an open-source, cloud-based performance testing platform which was used to assess the website’s reaction as the number of simulated users increased. 

## 2. Hypothesis
<p align="justify">
It was expected that the QuickPizza website would be stable and responsive under a moderate user load roughly for about 75 virtual users. However, we do expect to see some slight increases in response time and potential request failures as we push towards 100 concurrent users. The bottlenecks were expected to be in the higher latency for pages that needed server-side processing, but it was hoped that the static pages would continue to respond without issue. 

## 3. Tool Selection and Justification

### 3.1 Why Grafana Cloud K6
<p align="center">
  <img width="318" height="159" alt="k6 logo" src="https://github.com/user-attachments/assets/21f99ddf-391c-42c7-b55f-2f3e5aea2a3a" />
</p>

<p align="justify">
The reason why I chose Grafana Cloud K6 is because it provides a fully cloud-based environment. It allows users to run and monitor performance tests from their browser without having to install local command-line tools. Local command line tools can complicate the setup process and lead to platform dependency on either Windows or macOS.
  
### 3.2 Comparison with Other Tools
<p align="justify">
Unlike other tools like Apache JMeter or Locust, Grafana Cloud K6 puts an emphasis on simplicity and real time visualization. The scripting uses JavaScript which provides flexibility and simplicity for beginners. The dashboards automatically plot important metrics like response time, throughput, and failure rate, making it easy to visualize performance trends. 
<p align="justify">
For this project, the test was executed entirely on the Grafana Cloud K6 web platform instead of in a local Visual Studio Code or Windows Command Prompt environment. The decision to perform the test in the cloud allowed for easier monitoring, cloud-managed execution, and instant graph visualization. 

## 4. Test Environment Setup
<p align="justify">
The Performance menu was utilized in Grafana Cloud K6 to carry out the stress test. A specific project named QuickPizza-StressTest was created for this purpose. The execution environment was set to be hosted in the Columbus load zone to ensure balanced request distribution and reliable result sampling.
<p align="justify">
The maximum virtual users was set to 100, which is the upper limit for the plan offered by Grafana Cloud. While this limit constrained the possible load testing of the service at an extreme level, it was sufficient for determining performance trends and potential bottlenecks.

The JavaScript-based K6 test script defined a gradual user ramp-up pattern to simulate real world browsing behavior. The stages were:

- Ramp to 50 users in 1 minute
- Increase to 75 users in the next minute
- Peak at 100 users for the final 2 minutes
This configuration enabled controlled load escalation and sustained stress conditions, revealing how performance evolved at each stage.


## 5. Methodology and Execution
```js
import http from 'k6/http';
import { sleep } from 'k6';

// stages configuration
export let options = {
  stages: [
    { duration: '1m', target: 50 },
    { duration: '1m', target: 75 },
    { duration: '2m', target: 100 },
  ],
  thresholds: {
    http_req_duration: ['p(95)<2000'],
    http_req_failed: ['rate<0.05'],
  },
};

export default function () {
  http.get('https://test.k6.io/');
  http.get('https://test.k6.io/news.php');
  http.get('https://test.k6.io/contacts.php');
  const payload = { login: 'admin', password: '123' };
  http.post('https://test.k6.io/login', payload);
  sleep(1);
}
```
The script simulates a typical user flow visiting the homepage, reading a news section, checking contact details, and then attempting a login. This utilized intentionally invalid credentials to simulate authentication handling under load.

Test execution was conducted by writing the script into the Grafana Cloud K6 Script Editor and clicking ‘Run Test’. Real time metrics were served on the Grafana dashboards showing total requests, the failure rate, and response duration.

### 5.1 Test Configuration Summary

| **Parameter** | **Configuration** |
|----------------|-------------------|
| Test Type | Stress Test |
| Tool Used | Grafana Cloud K6 |
| Total Duration | 4 minutes |
| Virtual Users (VU) Range | 50 → 75 → 100 |
| Thresholds | p(95) < 2000 ms, failure rate < 5% |
| Endpoints Tested | `/`, `/news.php`, `/contacts.php`, `/login` |

## 6. Results and Raw Data
<p align="justify">!
After performing the stress test on Grafana Cloud K6, a comprehensive array of performance metrics was generated. The platform automatically presented the output using numerous visualization and analysis panels such as Graph, Cloud Insights, HTTP Summary, Thresholds, and Profile. All of these panels together, show how the QuickPizza test site performed when put under a gradually increasing load.

### 6.1 Graph Overview
<p align="center">
  <img src="https://github.com/user-attachments/assets/249cb860-0f32-4177-9602-e13c9dcdcc2a" width="600">
  <br>
  <strong>Figure 6.1 </strong><em>Response time under 100 concurrent users</em>
</p>

<p align="justify">
The chart depicts the path of the virtual users (VUs) as they ramped from 50 to 75 and finally peaked at 100 over the course of four minutes. As the VUs increased, requests per second (RPS) also increased but levelled off at approximately 682 RPS. Through the entire testing process, the average and 95th percentile (P95) response times remained comfortably under 3.65 ms. The P95 confirms stable performance even during maximum VU ramp up phase.

### 6.2 Cloud Insights Summary
<p align="center">
  <img src="https://github.com/user-attachments/assets/103808c2-708c-495b-901f-7552d4637c6b" width="600">
  <br>
  <strong>Figure 6.2 </strong><em>Average response time, throughput, and successful completion rates</em>
</p>

<p align="justify">
The Cloud Insights panel of Grafana gave a succinct overview of system health and performance. It reported 100% tests completed with no serious degradation of service. It showed VU scaling smoothly and only minimal deviation in latency. Values summarized included mean response time, throughput, and error rate which were all acceptable values.

### 6.3 Threshold Evaluation
<p align="center">
  <img src="https://github.com/user-attachments/assets/dd781230-3b02-44a8-8ed1-2545166f3478" width="600">
  <br>
  <strong>Figure 6.3 </strong><em>All thresholds passed</em>
</p>

| **Metric** | **Threshold Condition** | **Observed Result** | **Status** |
|-------------|--------------------------|----------------------|-------------|
| HTTP Request Duration (p95) | < 2000 ms | ~3.6 ms | ✅ Passed |
| HTTP Failure Rate | < 5 % | ~0.01 % | ✅ Passed |

Both defined thresholds were satisfied, indicating that the system maintained the targeted performance level throughout the test.

### 6.4 HTTP Summary
<p align="center">
  <img src="https://github.com/user-attachments/assets/d78ae507-d68d-4028-aef5-2c000452eb3c" width="600">
  <br>
  <strong>Figure 6.4 </strong>
</p>

The HTTP summary indicates that all requests were successfully completed except for one request which failed when attempting to authenticate using the `/login` endpoint. The failure was deliberate as an invalid credential was used.

### 6.5 Key Observations

- Peak load: **100 virtual users**
- Average throughput: **~682 requests/second**
- 95th percentile response time: **3.6 ms**
- Failed requests: **1 (HTTP 403 on /login)** – expected
- Both thresholds passed ✅

## 7. Analysis and Interpretation
<p align="justify">
The collected data confirms that the QuickPizza demo site performed reliably under stress. As virtual users increased, there was no significant rise in latency or failure rate. The system maintained efficient throughput and quickly responded to all GET requests.

### 7.1 Response Time Stability
<p align="justify">
The graph showed that response times maintained a flat trend line which leads us to believe the web server operated with consistent processing capacity. Even under peak load, the P95 value of 3.65 ms held far below 4 seconds threshold, showcasing an efficient backend processing capability.

### 7.2 Throughput and Scalability Capability
<p align="justify">
Throughput followed the number of users ramped and held a steady state at 682 RPS approximately. No sharp spikes or dips inferred that QuickPizza performed well at handling concurrency and Grafana’s load generators load balanced effectively over the test period. 

### 7.3 Failure and Error Handling
<p align="justify">
The one failed HTTP 403 request observed was not unexpected from the `/login` endpoint confirming authentication logic was acting in the intended mode rather than exhibiting a performance error. The Logs tab confirmed no connection timeouts nor any unexpected 5xx server errors occurred. 

### 7.4 Resource Utilization Perspective
<p align="justify">
Since the test occurred in Grafana’s cloud environment, CPU and memory usage at the server were not available as the major perspective. However, there were no latency spikes or throttling behaviour that would indicate that the requested infrastructure operated within safe performance ranges. 

### 7.5 Insights from Grafana's Analysis Panel
<p align="justify">
The Analysis tab in Grafana aggregated the run to be “Healthy”, with all thresholds listed as “Passed”. Average request time and data transfer remain unchanged and confirm that the system can sustain moderate to heavy traffic.

## 8. Recommendations and Best Practices
- **Increase Test Duration:** Extend test duration beyond four minutes to capture long-term stability trends.  
- **Scale Beyond 100 VUs:** Upgrade Grafana Cloud plan for more extensive stress evaluation.  
- **Improve Login Simulation:** Use valid credentials to test actual authentication load.  
- **Add Resource Monitoring:** Integrate backend CPU and memory metrics for complete system visibility.  
- **Implement Continuous Testing:** Automate recurring stress tests after major code updates to ensure consistent performance.

## 9. Conclusion
<p align="justify">
It was demonstrated through this experiment on how stress testing can measure a web application’s stability when subjected to rising load of users. The use of Grafana Cloud K6 web environment facilitated a smooth, installation free approach to the experiment and supported the real time visualizing of metrics.
<p align="justify">
Even though the free-tier plan is limited to a maximum of 100 virtual users, the test was able to successfully indicate QuickPizza’s ability to sustain its performance while it was being stressed. QuickPizza obtained low response times while achieving high throughput and did not experience any critical performance failures. The one HTTP 403 failure that occurred on login indicated simulated behaviour of the program and was not an indication of instability.
<p align="justify">
In conclusion, QuickPizza was able to process the simulated concurrent traffic successfully and did so within defined performance thresholds. The experiment provides evidence Grafana Cloud K6 is a great option as an accessible tool for academic and professional load testing purposes. 

## 10. Reflection
<p align="justify">
This project offered a hands-on experience utilizing real world performance testing concepts. Initially, I faced difficulties establishing local execution via Visual Studio Code and the command prompt particularly those related to authentication and token configuration. Once I moved to Grafana K6’s web interface, these difficulties were greatly reduced and it enhanced my comprehension of testing workflows in the cloud. 
<p align="justify">
From this assignment, I learned how to create load profiles, interpret response metrics, and find bottlenecks using real world testing data. I also gained an even greater appreciation for how using visual dashboards quickly speeds the interpretation of trends. Overall, this experience reinforced my understanding of performance testing best practices and the concept is especially relevant to make sure end users are satisfied with the web systems. 

## 11. Video Demonstration
A short walkthrough video showcasing the test execution, configuration steps, and the result visualization is available on : 

👉 [**Watch on YouTube**](https://www.youtube.com/watch?v=CDNLb47zqJQ) 

## 12. References

- Grafana Labs. (2024). *Grafana Cloud k6 Documentation.* Retrieved from [https://grafana.com/docs/grafana-cloud/testing/k6/](https://grafana.com/docs/grafana-cloud/testing/k6/)

- Grafana Labs. (2024). *Test.k6.io – Demo Website for Load Testing.* Retrieved from [https://test.k6.io/](https://test.k6.io/)

- Isaiah, A. (2025, March 3). _Introduction to Modern Load Testing with Grafana k6._ Better Stack Community. Retrieved from [https://betterstack.com/community/guides/testing/grafana-k6/](https://betterstack.com/community/guides/testing/grafana-k6/)



