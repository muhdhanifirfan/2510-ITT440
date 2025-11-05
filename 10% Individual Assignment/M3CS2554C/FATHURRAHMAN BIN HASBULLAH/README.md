# 🚀 A Spike Test and Analysis of Drupal-Based Hosting Using JMeter

<div style="text-align: justify;">
There are currently many web hosting services on the internet. As of this day web hosts, such as Bluehost, Hostinger, IONOS, etc., all share one common service, which is to provide a place on a server and allocate all the web application's files, creating an accessible storage for internet users. Although they provide the same service, the performance and vulnerability of the service play an important role for consumers to choose their preferred web host. Hence, the objective of this article is to design, execute, and analyse a performance test plan for a web application using a specialised testing tool.
</div>

---
## 🔧 About JMeter

<div style="text-align: justify;">
The tool that was used for this experiment is JMeter. It is an open-source testing tool from Apache that provides a wide range of performance testing capabilities. The application is Java-based and allows testing of client-server applications such as databases, FTP servers, websites, web services, etc. <b>The main interest for this study is to use JMeter and run a spike test on a local web application (demo).</b> The tool was chosen for the benefits of:
</div>

### 🌐 Server Compatibility

<div style="text-align: justify;">
JMeter is a thoroughly capable tool that can address load and performance testing for different products, ignoring the server or protocol. JMeter disregards protocols such as HTTP or HTTPS web services, databases, FTP, LDAP, MOM (message-orientated middleware) through NoSQL (MongoDB), and JMS.
</div>

### 📊 Distributed Load Testing

<div style="text-align: justify;">
JMeter supplies distributed load testing, permitting developers and testers to manipulate a master-slave set, enabling load testing on different machines.
</div>

### ⚙️ Customizations

<div style="text-align: justify;">
JMeter enables customization since it allows users to take advantage of its open-source nature. The customization can be related to its source code and create anything that suits users' requirements.
</div>

---

## 🛡️ About Drupal

<div style="text-align: justify;">
Drupal is an up-to-date, open-source CMS. Thanks to its flexibility and strong security features, it is perfect for making complex websites. Drupal was not chosen as one pleases; it has one of the best built-in security implementations. Drupal exerts an extensive API for secure data management and automated testing to catch vulnerabilities before they become a threat.
</div>

---

## 🖥️ Testing Enviroment Setup and Methodology

### 📦 Resources:
 
#### **Hardware**
- **Server:** Workstation
- **Storage (GB):** 512
- **RAM (GB):** 16

#### **Software**
- **Database:** phpMyAdmin (MySQL)
- **Operating Systems:** Windows 11

#### **Network**
- **Network Standard:** 802.11ax
- **Band:** 5 GHz

#### **Target**
- **Web Application:** Drupal CMS Demo

### 📋 Methodology

<div style="text-align: justify;">
The test was conducted on a single laptop workstation connected to a Wi-Fi (802.11x) with a 5 GHz band network. The scenario can be described as a single server testing. The single laptop workstation locally hosts the website's web server and, at the same time, acts as threads to the website itself. The results of the test cannot be taken as literal, since the environment or setup of the test does not fully utilise the <b>real-world</b> simulation of web application testing. However, after a few literature reviews, the best setup for the testing was considered; hence, it was implemented in the current setup. The steps taken for the test were:
</div>

#### 🔹 Drupal and Apache XAMPP

1. Install Apache XAMPP on a local machine.

<!--![A screenshot of a computer](media/image1.png)-->

2. Install Drupal demo's website on a local machine.

<!--![A website page of a website](media/image2.png)-->

3. Set up Drupal's demo server using phpMyAdmin.

<!--![A screenshot of a computer](media/image3.png)-->

#### 🔹 Apache JMeter Web Configuration

##### **Server Configuration**
- **Server IP**: 192.168.1.24
- **Application Path**: /websitegua
- **Protocol**: HTTP
- **Platform**: Drupal CMS Demo (locally hosted)

##### **HTTP Request Configuration**
**HTTP Request Defaults**:
  - Base URL: `http://192.168.1.24/websitegua`
  - Shared across all requests

##### **HTTP Cache Manager**:
  - Max cache elements: 5000
  - Cache-Control/Expires headers: Enabled
  - Simulates realistic browser caching behavior

##### **Test Endpoints (4 HTTP Requests)**:
1. **Pork Ribs Recipe** - `GET /websitegua/en/recipes/borscht-with-pork-ribs`
2. **Chili Sauce Recipe** - `GET /websitegua/en/recipes/fiery-chili-sauce`
3. **Soup Recipe** - `GET /websitegua/en/recipes/watercress-soup`
4. **Search Function** - `GET /websitegua/en/search/node?keys=pasta`

#### 🔹 Apache JMeter User Configuration (3 Spikes)

| **Spike** | **Start Threads Count** | **Initial Delay (sec)** | **Startup Time (sec)** | **Hold Load For (sec)** | **Shutdown Time (sec)** |
|-----------|-------------------------|-------------------------|------------------------|-------------------------|-------------------------|
| 1 | 100 | 0 | 10 | 10 | 10 |
| 2 | 200 | 30 | 10 | 5 | 10 |
| 3 | 100 | 55 | 10 | 10 | 5 |

**Total Virtual Users**: 400 threads across entire test duration (~2 minutes)
