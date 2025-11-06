# WEB PERFORMANCE ANALYSIS: JOOMLA DEMO WEBSITE STRESS TEST USING GTMetrix
####  STUDENT NAME : JANNATUL LAILA BINTI ABU MANSOR
####  ITT440 INDIVIDUAL ASSIGNMENT 
####  GROUP : M3CS2554C
 <hr>
<p align="center">
<img width="352" height="232" alt="image" src="https://github.com/user-attachments/assets/98e81f4f-aa05-4463-a5d0-eb8b50864f49" /> </p>

 <p align="center">
<img width="372" height="286" alt="JOOMLA" src="https://github.com/user-attachments/assets/b95c696b-fb75-478f-8f08-60160ea11a6a" /> </p>

 <hr>

## 1. INTRODUCTION

<p align="justify"> Web application performance is a crucial factor in determining user satisfaction and business success in today's digital environment.  This report uses stress testing techniques to provide a thorough performance analysis of the Joomla Launch website (https://launch.joomla.org/).  Stress testing helps find breaking points and performance degradation before they affect actual users by assessing how a system responds to extreme load conditions.  In order to evaluate the application's responsiveness, stability, and resource management under pressure, this study uses GTMetrix to simulate high user traffic. </p>
 <hr>
 
## 2. OBJECTIVES

<p align="justify"> This stress testing assignment's main goals are: 
<ul>
 <li> To use GTMetrix to perform stress testing on https://launch.joomla.org/. </li>
 <li> To assess key performance indicators (KPIs) like Core Web Vitals, error rate, throughput, and response time. </li>
 <li> To locate failure points and performance bottlenecks under heavy load. </li>
 <li> To offer data-based suggestions for web application optimization. </li>
</ul>
</p>
 <hr>

 ## 3. WHAT IS STRESS TESTING
 
<p align="justify"> One kind of performance testing called stress testing assesses a system's ability to function in harsh circumstances which beyond its typical operating range. Determining the system's resilience, stability, and error-handling skills in the face of extreme traffic spikes, resource depletion, or peak loads is the aim.  In contrast to load testing, which replicates anticipated user loads, stress testing tests the system's limits in order to identify potential failures and breaking points. </p>
 <hr>

## 4. TOOL SELECTION JUSTIFICATION

<p align="justify"> The tool selected for this analysis is GTMetrix. </p>
<p align="justify"> 
<ol>
    <li> Easy to Use: web-based and accessible; no installation needed. </li>
    <li> Comprehensive Reporting: Offers waterfall charts, Core Web Vitals, and comprehensive performance metrics. </li>
    <li> Real-Browser Testing: This method mimics real-user circumstances by using real Chrome browsers. </li>
    <li> Global Test Servers: Enables testing from various geographical locations, such as Seattle, Washington. </li>
    <li> Free Tier Availability: Ideal for personal and academic use. </li>
  </ol> 
 While not a traditional stress testing tool like JMeter, GTMetrix can simulate repeated loads and analyze performance degradation, making it a practical choice for this study. </p>
 <hr>

 ## 5. TEST ENVIRONMENT SETUP
 
<p align="justify"> The test environment was set up to create a baseline before carefully introducing stressors.
 <ol>
    <li> Testing Tool: GTMetrix (Web-based) </li>
    <li> Test Server Location: Seattle, WA, USA </li>
    <li> Browser: Chrome 125.0.0.0 </li>
    <li> Lighthouse Version: 12.3.0 </li>
    <li> Target Application URL: https://launch.joomla.org/ </li>
    <li> Network Throttling: Simulated (Default GTMetrix settings) </li>
    <li> Type of Test: Stress testing using performance trend tracking and repeated analysis </li>
  </ol>
   </p>

<p align="center">
<img width="954" height="685" alt="INTRO PIC" src="https://github.com/user-attachments/assets/d8c62d79-c185-46f4-afe0-dae28eaa5a43" /> </p>

<p align="center">
<img width="954" height="685" alt="PERFORMANCE" src="https://github.com/user-attachments/assets/39af9551-714b-4e48-a2a1-6fc7755aff6b" /> </p>
 <hr>
 
## 6. METHODOLOGY

<p align="justify">
 <ol>
    <li> Target Selection: The publicly accessible Joomla Launch site was chosen. </li> <!-- 1 -->
    <li> Test Execution: <!-- 2 -->
     <ul>
      <li> Multiple test runs were conducted via GTmetrix. </li>
      <li> Performance data was collected including: </li>
       <ul>
         <li> Redirect Duration </li>
         <li> Time to First Byte (TTFB) </li>
         <li> DOM Content Loaded Time </li>
         <li> Connection Duration </li>
         <li> First Paint </li>
         <li> Onload Time </li>
         <li> Backend Duration </li>
         <li> DOM Interactive Time </li>
         <li> Fully Loaded Time </li>
       </ul>
     </ul>
    </li>
<BR> <p align="center">
<img width="954" height="685" alt="BROWSER TIMING" src="https://github.com/user-attachments/assets/6946ea31-4153-4bb0-beee-28f6d5109818" /> </p>
    <li> Stress simulation: Despite GTmetrix's inability to support conventional multi-user stress tests, load was simulated through repeated runs and performance analysis under cached and uncached conditions. </li> <!-- 3 -->
   <li> Data Collection: Metrics were recorded from GTmetrix reports and Lighthouse audits. </li>
 </ol>
</p>
<hr>

## 7. PERFORMANCE DATA ANALYSIS
### 7.1 Overall Scoring
<p align="justify">
<ul> 
 <li> Performance Scoring: 67% </li>
 <li> Structure Score: 79% </li>
 <li> Fully Loaded Time: 8.7s </li>
</ul> </p>

### 7.2 Core web Vitals (User Experience Metrics)
<p align="justify">
<ul> 
 <li> Largest Contentful Paint (LCP): 2.5s </li>
 <li> Total Blocking Time (TBT): 236ms </li>
</ul> </p>
<hr>

<p align="justify">  </p>

<!-- [ <p align="justify">  </p> ]paragraph -->
<!-- [ <ul> <li>  </li>  </ul> ] bullet points --> 
<!-- <ol> <li>  </li>  </ol> numeric points -->
<!-- [ <hr> section devider ] [ <br> enter ] -->

<!-- 
8. Result Interpretation
The stress test revealed several performance issues:
= Slow LCP: Indicating slow rendering of the main content.
= High TBT: Suggesting unoptimized JavaScript execution blocking the main thread.
= Long Fully Loaded Time (8.7s): Highlights resource-heavy elements and slow server response.

Under repeated access, the site showed consistent degradation in performance metrics, especially in TBT and LCP, indicating poor stress tolerance.

9. Identification of Bottlenecks and Failure Points
= Backend Duration (1.3s): Suggests server-side processing delays.
= Large Image Files: Several images over 100KB (e.g., what-is-joomla4.jpg – 179KB) contribute to slow loading.
= Render-Blocking Resources: CSS and JavaScript files delay page rendering.
= Third-Party Scripts: Google Tag Manager and reCAPTCHA add significant overhead.

10. Summary
The stress testing of https://launch.joomla.org/ using GTmetrix highlighted significant performance bottlenecks under load, particularly in LCP and TBT. The application struggles with resource-heavy content and render-blocking scripts, leading to suboptimal user experience under stress. Recommendations include optimizing images, deferring non-critical JavaScript, and improving server response times. These changes would enhance both performance and stability under high-load conditions.

-->
