# BurpSuite Guide

## Introduction

BurpSuite is a powerful web application security testing tool used for performing penetration tests. It allows security professionals to intercept, inspect, and manipulate HTTP/S traffic between the browser and a web application. BurpSuite is widely used for tasks such as vulnerability scanning, web application testing, and automating security tests.

## Setting Up BurpSuite

1. Installation: Download BurpSuite from the [official website](https://portswigger.net/burp) and follow the installation instructions for your operating system.
2. Browser Proxy Configuration: Set up your browser to route traffic through BurpSuite by configuring the proxy settings. Usually, BurpSuite runs on `127.0.0.1:8080`.
3. Installing BurpSuite CA Certificate:
    - Access `http://burp` in your browser while BurpSuite is running.
    - Download and install the Burp CA certificate to ensure BurpSuite can intercept HTTPS traffic.
4. Configuring Browser with FoxyProxy for BurpSuite

### Configuring Browser with FoxyProxy for BurpSuite

Using an extension like FoxyProxy makes it easy to switch between proxy settings when testing with BurpSuite. Here’s how to set it up:

1. Install FoxyProxy Extension
   - Install the FoxyProxy extension for your browser:
     - [FoxyProxy for Chrome](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp)
     - [FoxyProxy for Firefox](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/)
2. Set Up Proxy Configuration
   - Open the FoxyProxy extension and add a new proxy configuration.
   - Proxy Type: HTTP
   - Proxy IP Address: `127.0.0.1`
   - Port: `8080` (or the port configured in BurpSuite)
   - Title: Name it something identifiable like "BurpSuite Proxy."
3. Enable the Proxy
   Once the configuration is saved, you can easily toggle the proxy on or off using the FoxyProxy extension.
4. Testing the Configuration
   With the proxy enabled in FoxyProxy, navigate to any website. BurpSuite should now intercept the traffic if it is configured correctly. Remember to check if the Burp CA certificate is installed to avoid SSL/TLS warnings.

By using FoxyProxy, you can efficiently manage and switch between proxy configurations without needing to manually adjust your browser’s settings every time you want to test with BurpSuite.

## BurpSuite Tabs Overview

BurpSuite organizes its tools and features into different tabs, each designed to help with specific aspects of web security testing. Here's a breakdown of the main tabs and their uses:

1. **Dashboard**  
   The Dashboard provides an overview of your project’s activity, including issues found during scans, task progress, and key metrics. It’s a great place to monitor ongoing scans and get updates on critical findings.

2. **Target**  
	The Target tab is central to managing your engagement and defining which areas of the application you will be testing. It includes two key sub-tabs:
	
	**2.1 Scope**  
	The Scope tab allows you to specify the areas of the application that you want BurpSuite to focus on during testing. This is critical for staying within the boundaries of your engagement and avoiding testing parts of the application or systems that are out of scope.
	
	- Include/Exclude Specific URLs: You can manually include or exclude specific URLs, paths, or file extensions using simple string matching or regular expressions. This ensures that BurpSuite tools like the Scanner, Spider, or Intruder only interact with relevant content.
	- Wildcard and Regex Support: The Scope tab supports wildcards and regex for advanced configurations, making it easy to define complex patterns that match multiple endpoints.
	- Defining Scope for Automated Tools: By setting a clear scope, you prevent BurpSuite’s automated tools from interacting with out-of-scope targets, reducing the risk of accidental disruption or legal issues.
	
	Best Practice: Before starting any scans or attacks, always define your scope in detail. This ensures that all activities remain within the authorized boundaries of your testing engagement.
	
	**2.2 Site Map**  
	The Site Map tab provides a hierarchical and visual representation of all the endpoints, paths, and resources discovered within the target application.
	
	- Tree View: The Site Map displays the entire structure of the application in a tree format, allowing you to navigate through domains, paths, and individual resources.
	- Resource Information: Each item in the Site Map provides detailed information, such as request/response details, status codes, content types, and more. You can right-click on any item to send it to other tools like Repeater, Intruder, or Scanner.
	- Filtering Options: You can filter the Site Map based on criteria like response codes (e.g., 200, 404), content types (e.g., HTML, JavaScript), or the presence of certain keywords in the responses.
	
	Use Case: The Site Map is especially useful when navigating large or complex applications, as it visually maps out all discovered endpoints, making it easier to prioritize targets for further testing.
	
	**2.3 Issue Definitions**  
	The Issue Definitions tab provides a comprehensive list of potential vulnerabilities and issues that BurpSuite can detect during scans. Each issue type is categorized based on its severity and type index. This section allows you to review the definitions and descriptions of various security issues that might arise during a web application test.
	
	- **List of Issue Types**: The table presents a list of known vulnerabilities like SQL Injection, OS Command Injection, and more. The typical severity of each issue is indicated, ranging from High to Medium or Low, helping prioritize issues based on their potential impact.
	
	- **Detailed Descriptions**: When you select a specific issue, detailed information about that issue is displayed in the panel on the right. This information includes a **description** of the issue, the risks it poses, and suggested **remediation** steps.
	
	- **References and Vulnerability Classifications**: The selected issue definition also provides references to external resources and vulnerability classifications like CWE (Common Weakness Enumeration) and CAPEC (Common Attack Pattern Enumeration and Classification). These links guide further research or in-depth understanding of the specific vulnerability.

3. Proxy  
	The Proxy tab is a central component of BurpSuite, allowing you to intercept, inspect, and modify HTTP/S traffic between your browser and the target application. It is primarily used for manual testing, where you can observe and manipulate requests and responses in real-time.
	
	3.1 **Intercept**  
	You can control whether requests are intercepted or passed through unaltered. When intercepting requests, you have the option to forward, drop, or modify them before sending them to the server. This allows you to test specific inputs, handle unwanted traffic, or explore different scenarios by altering the request content.
		
	3.2 **HTTP History**  
	The Proxy tab logs all HTTP requests and responses that pass through it, providing a detailed history of the interactions. Each entry includes information such as request method, URL, response status, and more. This history is useful for reviewing past traffic and identifying areas for further testing. You can apply filters to view only in-scope items, specific file types, or other criteria to focus on the most relevant data.
	
	3.3 **WebSockets**  
	In addition to HTTP traffic, the Proxy tab also supports intercepting and modifying WebSocket messages, making it suitable for testing modern applications that use this communication protocol.
	
	3.4  **Proxy Settings**  
	The Proxy Settings section allows you to configure key parameters for your proxy, including:
    - **Port Configuration**: You can change the port number used by BurpSuite if another service is already using the default port (8080). This flexibility ensures that BurpSuite runs without conflict, even in environments where multiple services are in use.

    - **Mobile Device Configuration**: BurpSuite can be set up as a proxy for your mobile device by adding your machine’s IP address and configuring your mobile device to route traffic through that IP and port. This is particularly useful for testing mobile applications or analyzing mobile web traffic.

    - **Request Interception Rules**: You can define rules to control when BurpSuite should intercept requests. For example, you can configure BurpSuite to intercept only in-scope items, specific URL patterns, or requests with certain headers. These rules help focus your testing on relevant traffic.

    - **Response Interception Rules**: BurpSuite can also intercept responses based on defined rules. This allows you to inspect and modify responses before they reach your browser. 

    - **Response Modification**: BurpSuite offers options for automatically modifying intercepted responses. For instance, you can unhide hidden form fields, adjust page content, or alter scripts before the response is rendered in your browser. This is useful for testing scenarios that rely on hidden inputs or need specific conditions to be met.

    - **Match and Replace**: The Match and Replace feature lets you define patterns to match in requests or responses and replace them with other values. This is useful for repetitive tasks such as:
		- **Manipulating the Referrer Header**: Automatically replace the referrer header with a custom value in all outgoing requests. This can help you test how the application handles traffic coming from different sources.

	The Proxy tab is where much of the hands-on, real-time testing occurs in BurpSuite. By combining interception, traffic inspection, and automation, it provides powerful control over the data exchanged between the client and the server.

4. Scanner (Pro Edition Only)  
   The Scanner tab is available in BurpSuite Professional and is used to automate security scans for discovering vulnerabilities like SQL Injection, XSS, and other common web application security issues. You can initiate scans from the Target tab or Proxy tab.

5. Intruder  
	The Intruder tab in BurpSuite is designed for performing automated and semi-automated attacks against web applications. It is particularly useful for testing scenarios such as brute-force attacks, parameter fuzzing, and identifying vulnerable inputs.
	
	The Intruder tab is broken down into several key sections:  
	
	- **Target**: In this section, you specify the host and port that the Intruder will target. The request that you want to attack is defined here. Typically, you send a request from another tab (like Proxy or Repeater) to the Intruder for automated testing.
	
	- **Positions**: The Positions tab is where you define which parts of the request should be manipulated during the attack. BurpSuite automatically highlights potential injection points, which you can adjust manually. You can choose to attack specific parts of the request, such as headers, query parameters, or the body.
	
	- **Payloads**: This section is where you configure the payloads that BurpSuite will inject into the specified positions. The Payloads tab allows you to:
	    - Choose from different payload types, such as lists, numbers, characters, or predefined payload sets.
	    - Configure multiple payload sets for complex attacks.
	    - Define payload processing rules to encode or transform payloads automatically before they are sent.
	
	- **Attack Types**: BurpSuite offers different attack types based on the desired test:
	    - **Sniper**: Targets one position at a time.
	    - **Battering Ram**: Sends the same payload to multiple positions simultaneously.
	    - **Pitchfork**: Sends different payloads to multiple positions simultaneously.
	    - **Cluster Bomb**: Tests all combinations of multiple payloads across positions.
	
	- **Results**: After launching an attack, results are displayed in this tab. The results include the request and response for each payload tested. You can sort, filter, and analyze these results to identify potential vulnerabilities. For example, you might look for response patterns that indicate successful injection attacks.
	
	- **Filters and In-Scope Items**: You can filter the results based on criteria such as response codes, length, or keywords. Additionally, BurpSuite allows you to restrict Intruder attacks to in-scope items only, ensuring that the automated tests stay within the authorized testing boundaries.

6. Repeater  
   The Repeater tab is used for manual testing by sending the same request multiple times with different parameters or payloads. This tool is invaluable for exploring how the application responds to different inputs, often used in testing authentication, authorization, or input validation.

7. Sequencer  
   The Sequencer tab helps analyze the randomness and predictability of session tokens, CSRF tokens, and other important values generated by the web application. This analysis is crucial for understanding whether such tokens can be guessed or predicted by attackers.
   
8. Decoder  
   The Decoder tab allows you to encode or decode data in various formats, such as Base64, URL encoding, or hexadecimal. It’s useful for analyzing data that might be obfuscated or transformed by the application.

9. Comparer  
   The Comparer tab lets you compare two pieces of data side-by-side, such as HTTP responses or encoded payloads. It highlights differences, making it easier to detect subtle changes that could indicate a vulnerability.

10. Extender  
   The Extender tab is where you can manage BurpSuite extensions, either by installing third-party extensions from the BApp Store or by loading custom-built ones. These extensions can significantly enhance BurpSuite’s capabilities.

11. Project Options  
   The Project Options tab contains settings that apply specifically to the current project. You can configure scan settings, proxy behavior, authentication details, and much more based on the requirements of your specific engagement.

Each of these tabs serves a distinct purpose in the overall security testing workflow, and understanding how they fit together will help you maximize BurpSuite’s effectiveness.

## Extending BurpSuite

BurpSuite can be extended using third-party extensions from the [BApp Store](https://portswigger.net/bappstore).
## Best Practices

**Scope Configuration**: Always define the target scope to avoid testing unintended domains.

**Handling Sensitive Data**: Use BurpSuite in an isolated environment to prevent exposure of sensitive information.

**Use Extensions Wisely**: Choose extensions based on your specific testing needs. Overloading BurpSuite with unnecessary extensions may lead to performance issues.

**Understand Legal Implications**: Always ensure you have permission to test a web application before proceeding.

---
## More
- [Official Documentation](https://portswigger.net/burp/documentation)
- [Community Extensions](https://portswigger.net/bappstore)
- [What is Proxy Server?](https://www.geeksforgeeks.org/what-is-proxy-server/)