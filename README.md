# CSRF-DVWA-SOLUTION
This repository contains an in-depth exploration and demonstration of Cross-Site Request Forgery (CSRF) vulnerabilities using the Damn Vulnerable Web Application (DVWA) platform. The project is conducted by Nihar Rathod, also known as BugBot19.

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/10b44cf3-d0c5-41eb-8291-3d61a8113e54)

# Overview
Cross-Site Request Forgery (CSRF) is a type of attack that tricks a web browser into executing an unwanted action on a different site for which the user is authenticated. This repository serves as an educational resource for understanding the mechanics of CSRF attacks and the measures to prevent them. This resource covers all levels of security (Low, Medium, and High) to ensure a thorough understanding of CSRF attacks and defenses.

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/4d996ab7-a364-4c8a-b5fb-29bb4916830a)

Cross-Site Request Forgery (CSRF) is a type of web security vulnerability that allows an attacker to trick a user into performing actions on a web application in which they are authenticated. Essentially, CSRF exploits a web application's trust in the user’s browser.

# How CSRF Works
1)User Authentication: The user logs into a web application (e.g., a banking site) and receives an authentication token, typically stored in a cookie.

2)Attack Setup: The attacker creates a malicious website or email containing a request that will be sent to the target web application. This request is crafted to act on behalf of the authenticated user, such as transferring money or changing account details.

3)User Interaction: The user, while still logged into the target web application, visits the malicious website or clicks on a malicious link.

4)Request Execution: The malicious request is sent to the target web application using the user’s credentials (the authentication token from the cookie). Because the user is authenticated, the web application processes the request, believing it to be legitimate.

# CSRF(LOW)

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/971a65d8-fc72-4444-8723-a4d9e2842453)

We can see from the above that the page contains two text fields and two buttons where ```Test credentials``` can be used to check whether the password is changed or not, So firstly we will try to change the password and observe how the page reacts.

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/f8676cce-c5f7-468a-b362-487f4c73466e)

I have changed the password i.e ```12345``` we can see that the password is reflected in the URL 

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/705d57a9-1759-4cd1-9a93-92e21d1ec18b)

So we can use the URL for further attacks I will be creating an HTML file that will contain with anchor tag but we will be changing the password parameter from ```12345``` to ```bugbot19```

```HTML file```

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/484e250b-5737-4a8f-afaa-e3f862dc5370)


![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/105b0d7b-19cf-44ed-bc05-96fb3cc614df)

By clicking on ```Click here!!!``` the password will be changed to ```bugbot19```

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/f4e4c1fc-9ca8-41d9-8d92-de902ff2193c)

You can see in the URL that the password has been changed now so this means our HTML file has run successfully. We will be using test credentials to check whether the password has been changed or not.

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/ebb17174-e896-4d1b-9aee-4fc4dc3f90a0)

You can see that ```bugbot19``` is a valid password for ```admin```

# CSRF(MEDIUM)

If we follow the low-level method it will not work 

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/f4a39049-0396-4143-abbe-b5495b8f0b0d)

copy the URL paste it into the burp browser see the HTTP history request you can see that it does not contain ```referer``` header

So we will be using the ```XSS-Stored``` low level to make it work, Let's first draft a malicious URL to change the password 

I have made up this URL ```http://localhost/dvwa/vulnerabilities/csrf/?password_new=123456&password_conf=123456&Change=Change#``` where password has been changed to ```123456``` from ```bugbot19```

Now we will use a script in the XSS-stored module to make it run we will need burp for this step

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/ef239e88-bc86-4089-8545-b886e2b7354b)

Change the ```max-length``` to ```200``` so that we can insert this payload ```<img src=http://localhost/dvwa/vulnerabilities/csrf/?password_new=123456&password_conf=123456&Change=Change#>```

Keep an eye on the HTTP history 

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/cff89b31-2e58-4e67-8502-5ca574d6e5c7)

After clicking on sign guestbook you can observe that we get two requests with two different methods ```get``` and ```post``` and both contain ```referer``` header this means the password has been changed so we will check it by using test credentials.

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/b237be69-945b-4a64-8ab4-317a57decc6e)

You can see ```123456``` is valid 

# CSRF(HIGH)

For this level, we cannot use the previous method first try to understand the request with the help of ```burp``` you can notice it has a csrf token 

So first, we will change the password to ```admin``` and after changing the password copy the URL 

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/7d9802c8-0ea7-423f-a7dc-357ee953601f)

We can see the password has been changed now draft the URL with a different token and refresh the page after refreshing ```inspect``` the page go to ```console``` and type ```document.getElementsByName("user_token")``` and press enter we will get the output in the below way

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/a593fcfd-e849-42d9-acc9-0320de6cdc50)

Expand it you will find a token in ```deafaultvalue``` variable 

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/97d7600d-822f-4989-b007-317c82fc8e45)

Copy the token and replace it with the previous token 

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/e0b90bf6-4048-4d54-a89d-3c5a65a99fe9)

Send the drafted URL to the browser and you can observe that the password is changed you can also try it on test credentials 

![image](https://github.com/kashrathod19/CSRF-DVWA-SOLUTION/assets/54115061/6a894e46-0255-49f9-ae2c-62e5ae559dec)




