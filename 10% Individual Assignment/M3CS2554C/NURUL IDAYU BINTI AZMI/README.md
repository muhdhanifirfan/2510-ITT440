# 🏷️ Website Capacity Testing Using K6
### Prepared for: MR. SHAHADAN BIN SAAD

**Name: NURUL IDAYU BINTI AZMI**  
**Student ID: 2025156453**  
**Group: CDCS2554C**  
**Subject: ITT440 - Network Programming**  

---

## 🧩 Introduction

This project focuses on performing **capacity testing** on the [Fake REST API](https://fakerestapi.azurewebsites.net/) website using K6, an open-source load testing tool. The goal of this test is to analyze how the system performs under an increasing number of concurrent virtual users (VUs) and identify its performance limit. Capacity testing helps determine the **maximum number of users a system can handle** before performance starts to degrade, such as longer response times or failed requests.

---

## 🎯 Objectives

- To evaluate how the website responds under different user loads.
- To identify the system’s capacity threshold (the point where performance degrades).
- To observe response time, request rate, and error rate during peak load.
- To generate data for future optimization and scaling.

---

## 🧰 Test Plan and Methodology
k6 was selected as a tool to be used in this experiment because it is a modern, lightweight, and developer-friendly performance testing tool that supports scripting with JavaScript. k6 requires less configuration and provides clean command-line output suitable for small-scale experiments.

| Tool name | k6 |  
| Testing type | Capacity Testing |  
| Target: https | fakerestapi.azurewebsites.net/ |  
| Test duration | 10 seconds per scenario |  
| Virtual users | 100, 1000, 2000, 3000, 4000, 5000 (for comparison) |  

---

## ⚙️ Test Environment Setup

**System Configuration:**
- Operating System: Windows 11  
- Processor: Intel i5 processor 
- RAM: 8 GB  
- Internet Connection: Stable broadband


