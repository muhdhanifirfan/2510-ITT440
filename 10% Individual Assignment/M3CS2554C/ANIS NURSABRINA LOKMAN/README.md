# 🧠 Web Perfomance Testing on JMeter

## 📘 1. Introduction
This project focuses on **evaluating the performance of a Moodle-based web application** through **load testing** and **stress testing** using **Apache JMeter**.  
The objective is to identify how the system behaves under normal, heavy, and extreme traffic conditions — measuring response time, throughput, and server stability.

---

## 💡 2. What is Load and Stress Testing?

| Test Type | Description | Purpose |
|------------|--------------|----------|
| **Load Testing** | Simulates a specific number of concurrent users accessing the system to measure performance under multiple users. | Determines the maximum operating capacity of the system under normal conditions. |
| **Stress Testing** |Test the robustness of the system under extreme load and varying data amounts. | Identifies performance bottlenecks, failure points, and recovery ability. |

---

## ⚙️ 3. Tool Selection

### 🧰 Apache JMeter
**JMeter** is an open-source software testing tool developed  to load test functional behaviour and measure performance by Apache. It is widely used for testing web applications, APIs, and databases.

#### 🔹 Reasons for Choosing JMeter:
- Supports **HTTP/HTTPS** requests, ideal for testing Moodle web applications.
- Can simulate **multiple virtual users** concurrently.
- Provides **detailed reports** (response time, throughput, error %).
- Compatible with **Windows, Linux, and macOS**.
- Easy to integrate with **Moodle** for web/API testing.

#### 🔹 Target Application:
- **System Under Test (SUT):** Moodle (Learning Management System)
- **URL:** `https://moodle.com/`
- **Tested Modules:** Login Page, Product Page, Service Page.

---

## 🧩 4. Test Environment and Configuration

| Component | Specification |
|------------|----------------|
| **Testing Tool** | Apache JMeter 5.6.3 |
| **Operating System** | Windows 11 (64-bit) |
| **Target Server** | Moodle Web Application (Localhost) |
| **Protocol Used** | HTTP / HTTPS |
| **Thread Group** | 100 Virtual Users |
| **Ramp-Up Period** | 30 seconds |
| **Loop Count** | 5 iterations |

---

## 🧪 5. Methodology

1. **Setup JMeter:**
   - Install Apache JMeter.
   - Launch `jmeter.bat` (Windows) 
   
2. **Create Test Plan:**
   - Add **Thread Group** → set 100 users, ramp-up 30 sec, loop 5.
   - Add **HTTP Request Defaults** → set Moodle base URL.
   - Add **HTTP Request Samplers** → e.g., `/login/index.php`, `/my/`, `/mod/assign/view.php`.
   - Add **Listeners** → View Results Tree, Summary Report, Aggregate Graph.

3. **Run Load Test:**
   - Simulate 100 concurrent users logging in and navigating Moodle.
   - Monitor average response time, throughput, and error rate.

4. **Run Stress Test:**
   - Gradually increase user load (e.g., 100 → 200 → 500 users).
   - Observe server response degradation and possible failure points.

5. **Capture Results:**
   - Export data as `.jtl` or `.csv` file.
   - Analyze graphs for **bottlenecks** or **server timeout**.

---

## 🧮 6. Example JMeter Test Script (Code Snippet)

```xml
??
