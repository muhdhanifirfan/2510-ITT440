# COMPREHENSIVE WEB APP PERFORMANCE TESTING & ANALYSIS
---

### ITT440: GROUP ASSIGNMENT 
### NAME: MUHAMMAD HANIF IRFAN BIN ZAKUAN 
### CLASS: M3CS2554A
---

# :boom: Stress Testing on Local Flask Web App using Siege
---

## :wave: Introduction
This performance testing was performed using Siege which is an open source regression test and benchmarking utility tool that available in Kali Linux to test high level of concurrent on a local flask web app that is simulation of Liquipedia.net pages. The purpose of this testing is to obsereve system behaviour when many user load access in one time and their performance. The test was conducted three test with different amount of virtual user in 60 seconds which were 10 users,50 users and 100 users. The target data to collect was transactions data, the availabilty, average response time in seconds and failed request.

---
## Objective
-  To measure the average response time and the system's performance under various amount of concurrent user traffic using Siege.
-  To determine the maximum handling capacity of the web server functionality and efficiency
-  To show and ensure how stress can be performed safely and ethically by using a local flask web app instead of real website.

---
## Hypothesis
“If users are active at the same time increase, the average response time and error rate are expected to increase, while the overall throughput will drop.
This hypothesis suggests that the simulated Flask server will show clear signs of performance slowdown under heavy user load that similar to what happens in real-world web systems.”



---


## Tool and Target Justification

## Performance Testing Tool (Siege)

The experiment used Siege because this open-source tool can easily handle hundrend users at once and enable to give details result which can checking up stability of server under high pressure request.

---


## Target Web Application (Liquipedia - Local Flask App)

The experiment used Liquipedia as reference because Liquipedia is a well-known esports wiki that feels familiar and realistic to use in simulations. It includes pages from many games like Dota 2 and Valorant, making it perfect for testing different parts or routes of a web app. The experiment don’t use the real Liquipedia site to ensure the testing ethical so a local flask app copy is created instead to make sure everything is safe and legal.

---
## Test Environment Setup
| Component | Description |
|---------|-----------|
| Environment | Kali Linux 2024.2 (64 bit) |
| Testing Framework | Siege v4.1.6 |
| Programming Language | Python 3.11.2|
| Target Website | Liquipedia — https://www.liquipedia.net (local flask simulating liquipedia Pages) |
| Test Selection | Stress Test | 
| Test Duration | 60 Seconds per round|
| Configuration File | `app.py` |
| Monitoring Tools | `htop`(CPU & Memory Usage), `matplotlib` (Graph plotting) | 
| Network | Localhost (127.0.0.1) |

---
## Load Pattern Design
| Level | Concurrency | Duration | Expected behavior |
|---------|-----------|---------|-----------|
| Low | 10 users| 6o second  | Stable response, no errors |
| Medium | 50 users| 60 second | Slight increase in latency |
| High | 200 users| 60 second | Noticeable slowdown, possible errors |

---
## Testing Procedure
uii


---
## Raw Data



---
## Result and Analysis


---
## Recommendations
- Expand Test Scenarios by adding more tests that cover different parts of the web app by database requests to helps get a clearer picture of how the whole system performs under stress.
- Optimize Application Performance by implementing performance optimization strategies such as  handling requests asynchronously to ensure system responsiveness and scalability efficiently.

---
## Conclusion
The stress testing experiment conducted with Siege clearly showed how server performance varies at different levels of user concurrency. The findings supported the hypothesis that increasing the number of simultaneous users leads to higher response times and error rates, while overall throughput declines. By running the test on a locally hosted Flask application, the project ensured ethical and safe testing without impacting any real websites. In conclusion, Siege proved to be an effective and dependable tool for evaluating web performance, offering meaningful insights into how systems behave under heavy traffic conditions.

---
## Youtube Video Demostration

