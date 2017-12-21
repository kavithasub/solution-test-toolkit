### Create_IDP_using_AdminService.jmx 

*Supported IS versions : 5.4.1*

This JMeter script can be used to Automate creating IDP. The IDP is created by calling adimin services. For Authentication, HTTP Authorization Manager is used. If you need to alter IDP properties you need to alter the SOAP message sent for admin service. The script is variabalized and variables can be changes at test plan level.

### Delete_IDP_using_AdminService.jmx

*Supported IS versions : 5.4.1*

This JMeter script can be used to Automate deleting IDP. The IDP is deleted by calling adimin services. The script is variabalized and variables can be changes at test plan level.

### Create_User_and_Role_using_AdminService.jmx

*Supported IS versions : 5.4.1*

This is sample JMeter script that can be used for role and user creation. This script calls IS admin services to create users and roles. You can edit the soap message and test parameters accordingly to alter thedefault user.


### Login_To_Travelocity_Twitter_As_IDP.jmx

*Supported IS versions : 5.4.1*

This script uses sellenium within JMeter and Automated Twitter login. First, have in mind that selenium tests will also be run within JMeter and not as a separate selenium project. These tests are ideally used to automate 3rd party app interactions such as login to twitter, facebook etc. Selenium scripts should be scripted using JSR223 Sampler ( Do not use beanshell sampler).

#How to setup JMeter
- Add the Selenium/WebDriver Support plugin to JMeter. You can download this from the JMeter Plugins Manager by searching for "Selenium/WebDriver Support"
- Add the "Selenium Standalone Server" .jar to <JMeter_HOME>/lib folder. You can download the .jar from (here) [https://goo.gl/hvDPsK]


Steps to add a JSR223 Sampler to your test suite.
Right click on your thread group and select Add -> Sampler -> JSR223 Sampler
	
![Alt text](/screenshots/1.png?raw=true "Login")	


Ones you add the JSR223 Sampler make sure to change the “Language” as java (BeanShell / Beanshell Engine)
	
	
![Alt text](/screenshots/2.png?raw=true "Login")
