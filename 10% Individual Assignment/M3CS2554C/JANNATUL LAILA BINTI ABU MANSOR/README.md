# WEB PERFORMANCE ANALYSIS: JOOMLA DEMO WEBSITE STRESS TEST USING GTMetrix
####  STUDENT NAME : JANNATUL LAILA BINTI ABU MANSOR
####  ITT440 INDIVIDUAL ASSIGNMENT 
####  GROUP : M3CS2554C
 <hr> <!-- This creates a horizontal divider line -->
<p align="center">
<img width="252" height="132" alt="image" src="https://github.com/user-attachments/assets/98e81f4f-aa05-4463-a5d0-eb8b50864f49" /> </p>

 <p align="center">
<img width="272" height="186" alt="JOOMLA" src="https://github.com/user-attachments/assets/b95c696b-fb75-478f-8f08-60160ea11a6a" /> </p>

 <hr> <!-- This creates a horizontal divider line -->

## 1. INTRODUCTION
<p align="justify"> In the digital age, a website's performance is directly correlated with user satisfaction, conversion rates, and search engine rankings. Stress testing is an essential performance engineering technique that evaluates a web application's stability and resilience by applying a significant load, often over its average operational capability. The primary goal is to identify an application's breaking point and understand how it fails, which is crucial for ensuring reliability during unexpected increases in traffic. <BR> This report details the extensive stress test conducted on the Joomla Demo website that is accessible to the public. This study uses the GTMetrix performance tool to simulate stressful scenarios in an effort to find potential performance bottlenecks, stability issues, and failure points that could negatively impact user experience or cause a complete service outage. </p>
 <hr> <!-- This creates a horizontal divider line -->
 
## 2. OBJECTIVES
<p align="justify"> This stress testing assignment's main goals are:</p>
<p align="justify"> 1. To Create a Stress Test Plan: Using GTMetrix's capabilities, create a methodology to replicate stressful situations for the target web application. <BR> 2. To carry out stress tests, run tests that cause the application to experience load profiles that are higher than usual, such as network throttling and fast consecutive requests. <BR> 3. Key Performance Indicators (KPIs) Analysis: Examine metrics like error rates under stress, Largest Contentful Paint (LCP), Page Load Time, and Time to First Byte (TTFB) critically. <BR> 4. Determine which particular server-side, network, or front-end components deteriorate or malfunction under load in order to identify bottlenecks. <BR> 5. To Offer Practical Suggestions: Provide evidence-based recommendations for improving the application's resilience to stressful situations. </p>
 <hr> <!-- This creates a horizontal divider line -->

 ## 3. WHAT IS STRESS TESTING
<p align="justify"> Stress Testing is a type of non-functional performance testing that involves analyzing how a system behaves in harsh circumstances. The following are a stress test's essential features: </p>
<p align="justify"> 1. Beyond the Normal Capacity: It deliberately puts an application under more stress than it would normally see in a day like a sudden spike from a viral social media post. <BR> 2. Find the breaking points: The test is meant to find out how much the app can handle and how it fails. <BR> 3. Finds Recovery Mechanisms: A stress test looks at how fast and efficiently an application can return to its normal state after the extreme load has been removed. <BR> 4. Focus on Stability: Stress testing is about knowing limits and making sure the system stays stable or fails safely, in contrast to load testing, which examines performance under anticipated load. <BR> In this study, we adjust GTMetrix, a tool frequently used for baseline performance checks, to perform a type of stress testing by examining performance degradation under extremely constrained network bandwidth and over repeated, fast requests. </p>
 <hr> <!-- This creates a horizontal divider line -->

## 4. TOOL SELECTION JUSTIFICATION
<p align="justify"> The tool selected for this analysis is GTMetrix. </p>
<p align="justify"> Justification of selected tool while GTMetrix is not a traditional load-testing tool like Apache JMeter that can simulate thousands of concurrent virtual users, it was chosen for this stress test for several reasons: </p>
<p align="justify"> 1. Front-End Focus: A major factor in user-perceived stress is front-end performance (rendering, asset loading, etc.), and GTMetrix offers an unmatched, detailed analysis of this performance. A resilient front-end can help alleviate a slow server, and GTMetrix is excellent at locating front-end bottlenecks. <BR> 2. Real Browser Monitoring: It generates performance data using a real Google Chrome browser, giving Core Web Vitals like Cumulative Layout Shift (CLS) and Largest Contentful Paint (LCP), which are closely related to user experience under load, extremely accurate metrics. <BR> Methodology Adaptation for Server Stress: We can create a server-side stress scenario by running several tests quickly one after the other and tracking the trend in server-side metrics such as Time to First Byte (TTFB). This allows us to determine when server resources (such as CPU and database connections) are being exhausted. <BR> Accessibility and Clarity: Because it is a software as a service platform, it doesn't require complicated setup, and its visual reports (performance grading, waterfall charts) are perfect for professional, understandable documentation. </p>
 <hr> <!-- This creates a horizontal divider line -->

 ## 5. TEST ENVIRONMENT SETUP
<p align="justify"> The test environment was set up to create a baseline before carefully introducing stressors.
 <ul>
    <li> Testing Tool: GTMetrix (Free Plan) </li>
    <li> Test Server Location: Seattle, WA, USA (This location was consistently used for all tests to ensure result comparability). </li>
    <li> Browser Engine: Google Chrome 125.0.0.0 (Desktop) with Lighthouse 12.3.0 </li>
    <li> Target Application URL: https://launch.joomla.org/ </li>
    <li>  </li>
  </ul>
  </p>
<p align="justify">  </p>
<p align="justify">  </p>
 <ul>
    <li>  </li>
  </ul>
