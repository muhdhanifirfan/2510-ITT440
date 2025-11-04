# 🧪  Web Application Performance Testing & Analysis  
## Title: Load Testing of FakeStoreAPI Using K6  

### 👤 Author  
**Name:** MUHAMMAD FITRI BIN ABDUL WAHAB  
**Student ID:** 2025172963  
**Course:** ITT440 – Web Application Performance Testing  
**Institution:** UiTM Kampus Jasin 

---

## 🧠 Background

**Load testing** evaluates how well a system handles concurrent requests.  
Each **virtual user (VU)** acts like a real human user sending API requests.  

By running **50 VUs** for **30 seconds**, this test simulates moderate user traffic to the API.  
We use **k6**, a modern developer-centric load testing tool, and send real-time data to **Grafana Cloud** using an authentication token.

---

## 🎯  Objective  

The purpose of this project is to perform a **Load Test** on a public web application using **K6**, a modern and developer-friendly load testing tool.  
The target system is [FakeStoreAPI](https://fakestoreapi.com/), an open REST API that simulates an online store.  

This test aims to evaluate:
- Response time under concurrent requests  
- System throughput (requests per second)  
- Error rate and performance stability  

---

## ⚙️  Tool Selection Justification  

### 🔸 Why Grafana K6?  
<img width="200" height="174" alt="k6 logo" src="https://github.com/user-attachments/assets/4695c7f3-f91f-4b71-887c-fabcbfc25044" />

Grafana K6 was selected due to its simplicity, lightweight setup, and developer-friendly scripting language (JavaScript).  
Compared to other tools, K6 offers:
- Easier scripting and execution from the command line  
- Faster performance with minimal resource usage  
- Built-in metrics summary and Grafana integration for visualization  

---

## 🌐  Target Web Application  

**Application:** [FakeStoreAPI](https://fakestoreapi.com/)  
**Description:** A free online API for testing and prototyping e-commerce applications.  
**Sample Endpoint Used:**  
`https://fakestoreapi.com/products`

---

## 🧰  Test Environment Setup  

| Component | Description |
|------------|-------------|
| **Operating System** | Windows 11 |
| **Tool** | K6 v0.52.0 |
| **Platform** | Window Comand Prompt |
| **Target URL** | `https://fakestoreapi.com/products` |


## ⚙️ Test Configuration 
   Test Script (loadtest.js):
   ```bash
    import http from 'k6/http';  
    import { sleep } from 'k6';  
    
    export const options = {  
      vus: 50,         // Number of virtual users  
      duration: '30s', // Test duration  
      };  
      export default function () {  
      // Target: FakeStoreAPI 
      const res = http.get('https://fakestoreapi.com/products');  
      sleep(1); // Simulate user wait time between requests  
      }
   ```

## ⚙️ Step 1: Run in CLI  
<img width="1237" height="151" alt="image" src="https://github.com/user-attachments/assets/667f24b4-6df1-4d46-bcfe-733bcad0d2e4" />  
Output  
<img width="1337" height="982" alt="image" src="https://github.com/user-attachments/assets/d49d6cc7-7776-4d0e-a2f6-b5449ff5c08b" />  
Graph Analysis  
<img width="1444" height="605" alt="image" src="https://github.com/user-attachments/assets/47c19d6b-2754-4d29-8b61-3e41e39a27bf" />






