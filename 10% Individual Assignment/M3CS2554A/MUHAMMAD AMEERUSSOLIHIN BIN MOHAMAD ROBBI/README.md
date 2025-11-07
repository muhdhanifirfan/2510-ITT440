# ⚡ Spike Testing On OWASP Using Gatling ⚡

### 📝 *ITT440 - INDIVIDUAL ASSIGNMENT*
#### 🧑‍🎓 NAME : MUHAMMAD AMEERUSSOLIHIN BIN MOHAMAD ROBBI
#### 🎓 STUDENT ID : 2024963323
#### 👥 GROUP : M3CS2554A
---
## 🎯  Project Overview
The purpose of this spike test was to evaluate the stability and behavior of the target web application under a sudden surge in user load. The test emulates an abrupt influx of users performing concurrent actions, such as visiting the home page and searching for flights.

## ⚙️ Test Setup

| Parameter | Configuration |
|------------|---------------|
| **💻System Environment** | Windows 11, Java JDK 17, 24 GB RAM |
| **🛠️Tool** |  Gatling 3.10.4 (Highcharts bundle) |
| **📋Language** | Scala simulation (SpikeTest.scala |
| **📈Type of Test** | Spike Test |
| **🌍Target URL** | (https://owasp.org/www-project-juice-shop/) |
| **🧍Total Virtual Users** | 320 concurrent |
| **⏱Duration** | ~47 seconds |
| **📽️Scenario** | 1️⃣ Open Home Page → 2️⃣ Search Flights |

## 🧾 Script/Command

###  Gatling
```scala
import io.gatling.core.Predef._
import io.gatling.http.Predef._
import scala.concurrent.duration._

class SpikeTest extends Simulation {

  val httpProtocol = http
    .baseUrl("https://owasp.org/www-project-juice-shop/")
    .acceptHeader("text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8")
    .userAgentHeader("Gatling Spike Test")

  val scn = scenario("OWASP Spike Test")
    .exec(http("Open Home Page").get("/").check(status.is(200)))
    .pause(1)
    .exec(http("Search Flights")
      .post("/reserve.php")
      .formParam("fromPort", "Boston")
      .formParam("toPort", "London")
      .check(status.is(200))
    )

  setUp(
    scn.inject(
      nothingFor(5.seconds),             // wait before starting
      atOnceUsers(10),                   // baseline load
      nothingFor(10.seconds),
      atOnceUsers(300),                  // sudden spike 🚀
      nothingFor(30.seconds),
      atOnceUsers(10)                    // recovery phase
    )
  ).protocols(httpProtocol)
}
```

###  Command Prompt
```bash
// In Command
cd (FileLocation)
gatling.bat
```
---

## 🧠 Hypothesis
The test expected successful HTTP 200 responses from both endpoints.
## 📊 Raw Data
## 🧬 Analysis
## 💡 Recommendations
## 🧩 Conclusion
✅ Test Execution

The simulation executed correctly:

Most users will injected and complete their scenarios.

Gatling will successfully parse and generated logs and summary reports.

❌ Response Outcome

All requests to the “Search Flights” endpoint failed, producing HTTP 405 (Method Not Allowed) errors instead of the expected 200 OK.
Output excerpt:

status.find.is(200), but actually found 405


This indicates that:

The server rejected the HTTP method (e.g., POST vs. GET mismatch), or

The endpoint was inaccessible or restricted under high load.

4. Quantitative Results
Metric	Total	OK	KO
Total Requests	640	320	320
Response Time (ms)			
Minimum	61	222	61
Maximum	3536	3536	661
Mean	641	1175	107
Std. Deviation	587	342	51
50th Percentile	279	1200	112
75th Percentile	1199	1384	122
95th Percentile	1478	1550	142
99th Percentile	1756	2095	219
Requests/sec	14.88	7.44	7.44

Distribution Summary

6% of requests completed below 800 ms.

19% between 800–1200 ms.

25% exceeded 1200 ms.

50% failed (405 responses).

5. Analysis
a. Functional Behavior

The home page requests (Open Home Page) were consistently successful, confirming that:

The Gatling setup and load injection worked properly.

The web server could handle the basic GET request load.

The Search Flights requests, however, all failed. Since the error was 405, not 500 or 503, this points to a client-side or configuration issue rather than outright server overload.

Possible causes:

The Gatling script is using the wrong HTTP method (e.g., POST instead of GET).

The target API endpoint blocks certain request types or origins.

The sudden spike triggered an application security rule (e.g., rate limiting, WAF protection).

b. Performance Metrics

Even though half the requests failed:

The server remained responsive (no timeouts).

Successful responses showed average latency around 1.1 s, with a max near 3.5 s, which is within typical limits for spike testing.

This suggests that the infrastructure could handle load, but application logic or routing caused functional failures.

c. Stability Observation

The system handled 320 concurrent users over ~47 s without crashing or producing critical errors (like 500s or timeouts).
Thus, stability at the infrastructure level is acceptable, but functional correctness under load is problematic.

6. Recommendations

Verify HTTP Methods:
Check whether the “Search Flights” endpoint should be accessed with GET, POST, or another method. Align your Gatling request definition accordingly.

Validate Endpoints Before Spike Testing:
Run a small smoke test (1–5 users) to confirm 200 OK responses before performing high-load spikes.

Monitor Server Logs:
Review application or API gateway logs to confirm why requests were rejected (look for “405” or “Method Not Allowed” entries).

Implement Gradual Ramp-Up:
Add a short warm-up or ramp phase before the spike to mimic more realistic traffic surges and prevent immediate overload.

Check Security Configurations:
Firewalls or API gateways may interpret repeated identical requests as suspicious; temporarily relax security settings for controlled performance testing.

7. Conclusion

The Gatling spike test successfully simulated a sudden increase of 320 users and provided valuable insights.
While the server infrastructure showed resilience and remained responsive, the application layer rejected half of the requests with HTTP 405 errors.
This indicates that under sudden high load, the system fails functionally rather than performance-wise — the requests reach the server but are not processed as intended.

Next Steps:
Refine request methods, confirm endpoint behavior, and rerun the spike test to verify whether the errors are configuration-related or true load-induced failures.
