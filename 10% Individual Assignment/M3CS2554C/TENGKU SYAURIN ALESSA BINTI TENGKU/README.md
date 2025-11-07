# TENGKU SYAURIN ALESSA BINTI TENGKU
# Comprehensive Web Application Performance Testing & Analysis 

- **Tools :** Locust
- **Testing Type :** Stress Testing
- **Target Web Application:** Docker (Nginx) Web Server
    <p align="center">
    <img width="298" height="100" alt="image" src="https://github.com/user-attachments/assets/f39b9542-7f9f-432f-92fd-0b25e7cf79ed" />

    <p align="center">
    <img width="246" height="65" alt="image" src="https://github.com/user-attachments/assets/a283fd9e-4320-438f-b12c-0d5591caadbd" />



---
## Introduction
This project focuses on conducting stress testing on a Dockerized web application using Locust, an open-source performance testing framework written in Python.
The goal of this testing is to determine the maximum performance capacity of the web server and identify performance bottlenecks when the system is subjected to extremely high loads.

Web applications must deliver consistent performance under various traffic conditions. Stress testing helps developers and administrators understand the breaking point of their application — where response times become unacceptable or the service begins to fail.

## Tool Selection Justification
A variety of performance testing tools are available today, including Apache JMeter, K6, Artillery, and LoadRunner. Each has distinct advantages and target use cases.
Locust was chosen for this study due to several key reasons:

| **Feature** | **Description** |
|--------------|-----------------|
| 🐍 **Python-based and highly scriptable** | Locust allows users to define realistic user behaviors using simple Python code, rather than relying on complex XML or GUI-based configurations like JMeter. This makes it ideal for flexible, programmatic test scenarios. |
| 🌐 **Web-based interface for live monitoring** | Locust provides a clean and interactive web dashboard where users can start/stop tests, adjust concurrency, and view performance metrics in real time — making it user friendly. |
| ⚙️ **Lightweight and scalable** | It can simulate thousands of users from a single machine and can also be distributed across multiple systems for large-scale testing. |
| 🔄 **Integration with modern CI/CD pipelines** | Locust integrates easily with Docker, GitHub Actions, and Jenkins, making it suitable for automated testing environments. |
| 🐳 **Ease of use for containerized environments** | Since both the target and testing tool can run as Docker containers, Locust is perfectly aligned with this project’s objective. |

In summary, Locust was selected for its simplicity, scalability, and modern Python-based design, which make it ideal for containerized performance testing environments.


## 🔧 Installations

- **Install Docker Desktop**
 📘 [Install Docker Desktop on Windows](https://docs.docker.com/desktop/setup/install/windows-install/)
  <br>After that, open Docker Desktop and make sure it is running</br>
  In Powershell or VS Code Terminal, run:
  ```bash
  docker --version
  docker ps
  ```

- **Install Python**
  📘 [Install Python](https://www.python.org/downloads/)
  <br>Verify it in terminal:</br>
  ```bash
  python --version
  pip --version
  ```

- **Install Locust**
  Open PowerShell or VS Code terminal and run:
  ```bash
  pip install locust
  ```
  Verify Installation:
  ```bash
  locust --version
  ```
  if failed:
   ```bash
  python -m locust --version
  ```
- **Install Visual Studio Code (VS Code)**
  <br>This is for editing the Locust test script and run commands in an integrated terminal.</br>
  📘 [Install Visual Studio Code (VS Code)](https://code.visualstudio.com/)
  <br>It is recommended to add these extensions in VS Code:
  - 🐍 Python extension
  - 🐳 Docker extension </br>

## Setup Procedure

**1. Launch Docker container**
It is up to you to use any name for the Docker container.
  ```bash
  docker run -d -p 8088:80 --name stress-target nginx
  ```
 This creates a running container serving static web pages at http://localhost:8088.
 <br></br>
 **2. Create Locust test script**
 <br></br>
 This will be the file you run on your terminal or PowerShell, and make sure that this script is in the *locust folder*.
 ```javascript
  from locust import HttpUser, task, between

class StressUser(HttpUser):
    wait_time = between(1, 3)

    @task
    def load_homepage(self):
        self.client.get("/")
  ```
 **3. Run Locust**
 ```bash
  locust -f (filename).py --host http://localhost:8088
  ```
 Open the web interface at http://localhost:8088 to configure and start the test.

 ## Demostration
 

 ## Methodology

| Component | Specification |
|:----------:|:-------------:|
| Testing Target | Docker 28.5.1 |
| Container Engine | Docker Desktop |
| Target App | Nginx (`latest`) |
| Testing Tool | Locust 2.42 |
| Python | 3.13.9 |

# Raw Data Presentation

- **500 Users**

<img width="1841" height="1125" alt="number_of_users_1762229559 305" src="https://github.com/user-attachments/assets/3c0d6ef3-b552-468f-9662-ab73e50c25f9" />

- **4000 Users**

<img width="1841" height="1125" alt="total_requests_per_second_1762278295 045" src="https://github.com/user-attachments/assets/a41461ff-a37d-42ac-bf8f-6f2e2e2af5d7" />

<br></br>

<img width="1521" height="126" alt="image" src="https://github.com/user-attachments/assets/ff184131-2ce9-4052-bfde-54302f5641ce" />

## Interpretation on the Results

On the 500 users graph, you can see the stable graph and has successful responses to all 500 concurrent users without any problem. 

<br></br>

The graph that shows 4000 users above shows that Locust sends many concurrent requests that is beyond its capability, the Docker container can't process all of them instantly. So, it closes connection (10054) or your local machine aborts waiting (10053). These are the failures shown in the failures table and also in the terminal inside VS Code will give the statements.

<br></br>

It has mentioned here that the CPU usage is too high at some point during the test which may constrain the throughput and may even give inconsistent response time measurements.


### Hypothesis
The Nginx container can handle moderate concurrent loads but will show increased latency under heavy stress. OR The hypothesis is that Nginx can handle up to 400–450 concurrent users efficiently, but performance will degrade as CPU usage reaches near saturation.
