# CSRF-DVWA-SOLUTION
This repository contains an in-depth exploration and demonstration of Cross-Site Request Forgery (CSRF) vulnerabilities using the Damn Vulnerable Web Application (DVWA) platform. The project is conducted by Nihar Rathod, also known as BugBot19.

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/10b44cf3-d0c5-41eb-8291-3d61a8113e54)

# Overview
Cross-Site Request Forgery (CSRF) is a type of attack that tricks a web browser into executing an unwanted action on a different site for which the user is authenticated. This repository serves as an educational resource for understanding the mechanics of CSRF attacks and the measures to prevent them. This resource covers all levels of security (Low, Medium, and High) to ensure a thorough understanding of CSRF attacks and defenses.

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/4d996ab7-a364-4c8a-b5fb-29bb4916830a)

Cross-Site Request Forgery (CSRF) is a type of web security vulnerability that allows an attacker to trick a user into performing actions on a web application in which they are authenticated. Essentially, CSRF exploits a web application's trust in the user’s browser.

# How CSRF Works
1)User Authentication: The user logs into a web application (e.g., a banking site) and receives an authentication token, typically stored in a cookie.

2)Attack Setup: The attacker creates a malicious website or email containing a request that will be sent to the target web application. This request is crafted to perform an action on behalf of the authenticated user, such as transferring money or changing account details.

3)User Interaction: The user, while still logged into the target web application, visits the malicious website or clicks on a malicious link.

4)Request Execution: The malicious request is sent to the target web application using the user’s credentials (the authentication token from the cookie). Because the user is authenticated, the web application processes the request, believing it to be legitimate.

# CSRF(LOW)
