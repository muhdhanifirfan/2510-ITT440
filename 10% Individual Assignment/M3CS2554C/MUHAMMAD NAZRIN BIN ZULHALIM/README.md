# :tiger: Performance Analysis of ‘https://demo.nopcommerce.com’ using Grafana k6

### 👨‍💻 Name: Muhammad Nazrin bin Zulhalim
### 🎓 Student ID: 2025157375
### 🧾 Course: ITT440 – Individual Assignment  
### 🧠 Group: M3CS2554C

---

## 🚀 Introduction: Why Are We Doing This?
### What is Load Testing?
### Load testing is a type of Performance Testing that determines the performance of a system, software product, or software application under real-life-based load conditions. Load testing determines the behavior of the application when multiple users use it at the same time. It is the response of the system measured under varying load conditions.

---
## :building_construction: Project Objective
### The objective of this is to analyse how ‘https://demo.nopcommerce.com’ will behave under soak testing using Grafana k6. k6 is used to simulate continuous real life traffic loads and identify performance degradation, memory and resource leaks and stability issues. The result of the test will be the indicators(KPIs) of the key performance and application endurance.

---
## 🔨 Tools Selection
### 🔥Grafana k6

<p align="center">
<img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/ce07a1f9-b3e4-49e1-962e-a9aa77d878ec" />
</p>

### 🚀 Key Features of Grafana k6

| Feature | Description |
| :--- | :--- |
| **Primary Approach** | 💻 **Code-Driven** |
| **Test Scripting** | Tests are written in **JavaScript (ES6)** as simple `.js` code files. |
| **Target Audience** | Developers, SREs, and DevOps/QA teams practicing "performance-as-code". |
| **Core Technology** | Written in **Go (GoLang)**, making it a fast, single native binary with no external dependencies. |
| **Performance** | **Very Low Resource Usage.** It uses an event-loop-based model, not a thread-per-user, allowing a single machine to simulate tens of thousands of users. |
| **CI/CD Integration** | **Native & Simple.** Designed for automation. You can define pass/fail criteria (called **Thresholds**) directly in your script, which is perfect for CI/CD pipelines. |
| **Protocol Support** | **Modern & Web-Focused.** Excellent out-of-the-box support for HTTP/1.1, HTTP/2, WebSockets, and gRPC. |
| **Reporting** | Provides a detailed command-line summary. It's built to stream metrics to external dashboards, most notably **Grafana**, InfluxDB, or Datadog. |
| **Extensibility** | Supports extensions (like `xk6-browser`) to add capabilities, such as real browser automation for frontend performance. |
---
## :dart: Target Application
<p align="center">
<img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/9d6be43b-c143-4beb-898a-fcc94426d2be" />
</p>

## 🎯 `https://demo.nopcommerce.com`

| Feature | Description |
| :--- | :--- |
| **:dart: Target Application** | The application we're testing is **`https://demo.nopcommerce.com`**, which is a public demo of an online store. |
| **Why This Target?** | We chose an e-commerce site because it's a perfect, real-world challenge. Online stores have to do two very hard things at once:<br><br>1.  **Handle Heavy Traffic:** They must stay fast and stable even when thousands of people are shopping at the same time (like during a Black Friday sale).<br><br>2.  **Handle Complex Journeys:** People don't just look at one page. They perform a series of steps (a "user flow") like searching for a product, adding it to their cart, logging in, and checking out. This multi-step journey puts much more stress on the servers and database than simple page browsing.<br><br>Since this is a public demo, it's the perfect, safe environment to simulate this kind of heavy, realistic user activity without breaking a real business. |
---
## 🛠️ Test Environment
| Component | Details |
|------------|----------|
| **Test Machine** | HP Probook 440 G8 |
| **CPU** | 11th Gen Intel(R) Core(TM) i7-1165G7 |
| **RAM** | 16GB DDR4 |
| **Tool** | Grafana k6 v1.3.0 |
| **Target Application URL** | ‘https://demo.nopcommerce.com’ |

---

## :microscope: Test Methodology: Simulating Realistic Behaviour
### To ensure the testing is valid, a realistic user scenario was created. The test simulates a user browsing the site, searching for a product and viewing certain product's page, with random pause between each steps. The test runs for a total of **35 minutes** and is broken into the following stages:

* **Stage 1 (Warm-up):** Ramp up from 0 to **50** users over 5 minutes.
* **Stage 2 (Building Load):** Ramp up from 50 to **100** users over 5 minutes.
* **Stage 3 (Growing Load):** Ramp up from 100 to **200** users over 5 minutes.
* **Stage 4 (Peak Load):** Ramp up from 200 to **300** users over 5 minutes.
* **Stage 5 (Soak Test):** Hold the peak load of **300** users steady for **10 minutes**. This is where we look for stability issues.
* **Stage 6 (Ramp Down):** Gradually remove all users over 5 minutes.

---
## 🧪 Test Scripts

### 🔹 `k6_script.js` 

```javascript
import http from 'k6/http';
import { sleep, group } from 'k6';


export const options = {
  stages: [
    { duration: '5m', target: 50 }, 
    { duration: '5m', target: 100 },
    { duration: '5m', target: 200 },
    { duration: '5m', target: 300 },
    { duration: '10m', target: 300 }, 
    { duration: '5m', target: 0 },    
  ],
};

export default function() {
  const BASE_URL = 'https://demo.nopcommerce.com';

  group('User Flow: Browse Products', function() {
    
    // 1. Visit Homepage
    http.get(BASE_URL);
    sleep(Math.random() * 2 + 1); // Think time: 1-3s

    // 2. Search for "laptop"
    http.get(`${BASE_URL}/search?q=laptop`);
    sleep(Math.random() * 2 + 1); // Think time: 1-3s

    // 3. Visit a specific product page
    http.get(`${BASE_URL}/apple-macbook-pro-13-inch`);
    sleep(Math.random() * 2 + 1); // Think time: 1-3s
  });
}
```
---

### The User Simulation: What Are They Doing?
The VU are designed to act like real, curious shoppers, not just bots hitting the homepage. Each user will repeatedly execute a 3-step "Browse and Search" journey.

1.  **Visit Homepage:** The user first lands on the `demo.nopcommerce.com` homepage.
2.  **"Think Time":** The user pauses for 1-3 seconds, just like a real person would.
3.  **Search for Product:** The user then uses the search bar to look for `"laptop"`.
4.  **"Think Time":** The user pauses for another 1-3 seconds while looking at the results.
5.  **View Product:** Finally, the user clicks on a specific product, the `"Apple MacBook Pro 13-inch"`, to see its details.
6.  **"Think Time":** The user pauses for 1-3 seconds to "read" the page before starting their journey over again.

### `https://demo.nopcommerce.com` Web Page Preview
- **Home Page** 
<p align="center">
<img width="800" alt="Screenshot (796)" src="https://github.com/user-attachments/assets/52688a50-438a-4055-948d-783c73638bf0" />
</p>


---

- **View Product Page**
<p align="center">
<img width="800" alt="Screenshot (797)" src="https://github.com/user-attachments/assets/339199a3-8ed3-4964-b4e2-0ea8af812771" />
</p>

---

## 📝Result : In-Depth Analysis
#### 1. The `Load` Chart
* **What it shows:** This chart confirms the test ran exactly as planned.
* **The Pattern:** We can see a perfect "stair-step" pattern:
    1.  A gradual ramp-up in user load (from timestamp `...750755` to `...751954`).
    2.  A flat 10-minute "soak test" plateau where the load held steady at 300 users (`...751954` to `...752530`).
    3.  A final ramp-down as users left the site (`...752530` onwards).

<p align="center">
<img width="800" alt="Screenshot (797)" src="https://github.com/user-attachments/assets/3b77bcf3-76ed-4cb3-943c-2aa1130f89fa" />
</p>

#### 2. The `P95 Average Response Time` Chart

* **What it shows:** This is the P95 response time, a key metric for user experience. It means "95% of users had a response time *at or below* this value." The Y-axis is in milliseconds (ms).
* **The Pattern (The Bad):** During the entire ramp-up phase (the first 20 minutes), the performance was *extremely* volatile. We see multiple massive spikes, with the worst one hitting **~55,000ms (55 seconds!)**. This is a completely unacceptable wait time.
* **The Pattern (The Good):** The *moment* the load stabilized at 300 users (at timestamp `...751954`), the response time **immediately** dropped and became stable, staying consistently below 5,000ms (5 seconds).

<p align="center">
<img width="800" alt="Screenshot (797)" src="https://github.com/user-attachments/assets/446ad4a5-b9db-45c3-8ee1-8990e5205aca" />
</p>

#### 3. The `Error Rate` Chart

* **What it shows:** This chart shows the percentage of requests that failed. A `1.0` on this chart means **100% of requests were failing** at that moment.
* **The Pattern (The Ugly):** This chart mirrors the response time chart perfectly. During the ramp-up, the error rate was wild, frequently spiking to `1.0` (100% failures). This means that when the system got slow, it wasn't just slow—it was **down**. It was actively dropping connections and failing to serve users.
* **The Pattern (The Recovery):** Just like the response time, the error rate **immediately** fell and stabilized as soon as the 300-user soak test began. While not zero, it dropped from a catastrophic 100% to a much lower, spikier average of 10-20%.

<p align="center">
<img width="800" alt="Error Rate" src="https://github.com/user-attachments/assets/bad6b6ec-6c27-4fe6-be34-05699811cd32" />
</p>

---
## 🧐 Bottleneck Observed: The "Cold Start" & Scaling Failure

Based on the test results, the application's primary bottleneck is **not the peak load, but the rate of change.**

The system **failed to handle the ramp-up**.

We can clearly see that during the 20-minute ramp-up (Stages 1-4), the system was completely unstable. Response times spiked to an unusable **55 seconds**, and the error rate hit **100%** multiple times. This indicates the server was overwhelmed, dropping connections, and failing to serve users.

The "smoking gun" is this: the *instant* the load stopped *growing* and held steady at 300 users (Stage 5), the system recovered. Response times and error rates immediately dropped to a (mostly) stable level.

This points to a classic **elasticity bottleneck**. The application's infrastructure (like web servers, database connection pools, or auto-scalers) cannot provision new resources fast enough to meet a rapid increase in demand. It's like a restaurant with only one waiter taking reservations—they get completely overwhelmed as guests arrive, but once everyone is finally seated, they can (mostly) keep up.

---

## 💡 Recommendations to Improve the Web Page

Here are actionable steps to fix this instability and improve the website's performance.

### 1. Fix the Scaling Bottleneck

The goal is to help the server "warm up" faster or be warm *before* traffic hits.

* **Tune Auto-Scaling Triggers:** If you're using cloud auto-scaling, make it **more aggressive**. For example, trigger a scale-up at **60% CPU** usage, not 80%. This gives new server instances time to boot up *before* the current ones are at their breaking point.
* **"Pre-Warm" the Environment:** For a known event like a sale, don't wait for the traffic. **Manually scale up** your servers 30 minutes *before* the event starts. This ensures you already have the capacity to handle the initial rush.
* **Optimize Resource Pools:** Check the `min` and `max` sizes for **database connection pools** and **thread pools**. If the minimum is too low (e.g., 10), the application wastes critical time creating new connections/threads under load. Increase the *minimum* size to handle a larger baseline load.

### 2. Implement or Improve Caching

A "cold" system (one with no cache) puts all the load on the database. This is likely what's happening during the ramp-up.

* **Implement a Cache-Warmer:** Create a simple script that automatically "visits" your most popular pages (like the homepage, category pages, and top products) every 15-30 minutes. This keeps the cache full of fresh data, so users are served from fast memory, not the slow database.
* **Analyze Cache Strategy:** Review your caching rules. Use server-side caching for product data that doesn't change often. Use browser caching for static assets like images, CSS, and JavaScript.

### 3. Investigate the Lingering Errors

Even after the system stabilized, the error rate was *not* zero. It averaged 10-20% during the 300-user soak test.

* **Check Server Logs:** This is critical. You must dig into the application and server logs for the exact timeframe of the soak test (from timestamp `...751954` to `...752530`). Look for **HTTP 500-level errors** (e.g., `500`, `502`, `503`, `504`). These logs will tell you *exactly* what was failing (e.g., "database connection timed out," "out of memory," etc.).
* **Add a Load Balancer:** If not already in place, a load balancer is essential. It will distribute traffic evenly across your servers, preventing one server from being overloaded while others are idle.
---

## :dart: Overall Conclusion

**The application cannot handle a *rapidly increasing* load.**

The data tells a clear story:

1.  While the user load was growing, the server was overwhelmed. It couldn't cope with the *change* in traffic, leading to massive 55-second response times and 100% error rates. For a real business, this is a disaster.
2.  However, once the load *stabilized* (even at its peak of 300 users), the application "caught its breath" and recovered. This could be due to caches warming up, database connection pools finally scaling, or an auto-scaler kicking in too late.

**Key Takeaway:** If this were a real e-commerce site, a "flash sale" or a successful marketing email would **crash the site** for the first 15-20 minutes—exactly when you need it to be working the most. The system's ability to handle *changing* load (its "elasticity") is its biggest weakness.

---

## 🎥 Demonstration Video
## https://youtu.be/v87tvTjvAgA
