# :tiger: Performance Analysis of ‘https://demo.nopcommerce.com’ using Grafana k6

### 👨‍💻 Name: Muhammad Nazrin bin Zulhalim
### 🎓 Student ID: 2025157375
### 🧾 Course: ITT440 – Individual Assignment  
### 🧠 Group: M3CS2554C

---
## :building_construction: Project Objective
### The objective of this is to analyse how ‘https://demo.nopcommerce.com’ will behave under soak testing using Grafana k6. k6 is used to simulate continuous real life traffic loads and identify performance degradation, memory and resource leaks and stability issues. The result of the test will be the indicators(KPIs) of the key performance and application endurance.

---
## 🔨 Tools Selection
<img width="1200" height="976" alt="K6_software_logo" src="https://github.com/user-attachments/assets/ce07a1f9-b3e4-49e1-962e-a9aa77d878ec" />

<p align="center">
<img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/ce07a1f9-b3e4-49e1-962e-a9aa77d878ec" />
</p>

## 🔥Grafana k6
## 🚀 Key Features of Grafana k6

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
## 🎯 **`https://demo.nopcommerce.com`**
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

### The User Simulation: What Are They Doing?
The VU are designed to act like real, curious shoppers, not just bots hitting the homepage. Each user will repeatedly execute a 3-step "Browse and Search" journey.

1.  **Visit Homepage:** The user first lands on the `demo.nopcommerce.com` homepage.
2.  **"Think Time":** The user pauses for 1-3 seconds, just like a real person would.
3.  **Search for Product:** The user then uses the search bar to look for `"laptop"`.
4.  **"Think Time":** The user pauses for another 1-3 seconds while looking at the results.
5.  **View Product:** Finally, the user clicks on a specific product, the `"Apple MacBook Pro 13-inch"`, to see its details.
6.  **"Think Time":** The user pauses for 1-3 seconds to "read" the page before starting their journey over again.

