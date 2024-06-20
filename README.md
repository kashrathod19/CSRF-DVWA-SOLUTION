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

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/971a65d8-fc72-4444-8723-a4d9e2842453)

We can see from the above that the page contains two text fields and two buttons where ```Test credentials``` can be used to check whether the password is changed or not, So firstly we will try to change the password and observe how the page reacts.

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/f8676cce-c5f7-468a-b362-487f4c73466e)

I have changed the password i.e ```12345``` we can see that the password is reflected in the URL 

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/705d57a9-1759-4cd1-9a93-92e21d1ec18b)

So we can use the URL for further attack I will be creating an HTML file that will contain with anchor tag but we will be changing the password parameter from ```12345``` to ```bugbot19```

```HTML file```
```<html>```
      ```<title>Free Dollars $$$</title>```
	  ```<body>```
	        ```<b><i><u>Click fast to win 100$ </b></i></u>```
            ```<a href="http://localhost/dvwa/vulnerabilities/csrf/?password_new=bugbot19&password_conf=bugbot19&Change=Change#">Click here!!!</a>```
	  ```</body>```
```</html>```

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/105b0d7b-19cf-44ed-bc05-96fb3cc614df)

By clicking on ```Click here!!!``` the password will be changed to ```bugbot19```

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/f4e4c1fc-9ca8-41d9-8d92-de902ff2193c)

You can see in the URL that the password has been changed now so this means our HTML file has run successfully. We will be using test credentials to check whether the password has been changed or not.

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/ebb17174-e896-4d1b-9aee-4fc4dc3f90a0)

You can see that ```bugbot19``` is a valid password for ```admin```

