# Introduction #

This repository includes common guidelines, samples and references which needs to be followed when automating solutions for TG execution. TG is a versatile platform which enables tests to be execute on top of different hardware/software combinations along with deployment pattern. You can read more about TG from here.

## Repository Structure

```
solution-test-toolkit
    ├── APIM
    │   └── README.md
    ├── IS
    │   ├── artifacts
    │   │   └── ReadME.md
    │   └── samples
    │       ├── Create_IDP_using_AdminService.jmx
    │       └── Delete_IDP_using_AdminService.jmx
    ├── README.md
    └── templates
        └── README.md

```

**/templates**

This are the generic templates that can be used when writing tests. For example JMeter templates can be used as basic building blocks for solution automation. 

**<Product-Directory>/samples**

This contains samples for different operations, you can read more from here.

**<Product-Directory>/artifacts**

This contains references for product specific common artifacts templates.

# Test Execution Phases



===== Need to add a proper Diagram and following points should be addressed ====

What you need to know in each phase. What are the scripts needed. What each script does and How to add scripts.

<explain high-level>









	




# How to Develop Solution Tests
## Writing Infrastructure creation Scripts
At the moment this is done manually, test infrastructure always reside on AWS and they are up and running. When a new instance is required this is created manually. This can be done automatically by developing CF scripts. 
## Test Solution Repository Structure
When writing solution tests for a given product, we need to follow the following repository structure. This structure contains scripts necessary to deploy/undeploy infrastructure, deploy/undeploy artefacts, test scripts and cleanup scripts. 

```
.
├── README.md
├── base-setup.sh
├── jmeter
│   ├── XX-Solution-01-Facebook.jmx
│   ├── XX-Solution-02-Google.jmx
│   ├── YY-post-scenario-steps.sh
│   └── YY-pre-scenario-steps.sh
├── resources

```

- XX - Sequential number : starts from 01..
- YY - Use solution number

You can find a detailed description of the repository structure in 3.3 section

## Writing Test-Artifacts Deployment Scripts

Test artifacts deployment is handled by the set of shell scripts which are specific to the solution. Travelocity.com application[<url_for_repo>] is the main artifact we use in the identity server solutions.

Lets consider **Solution 02** as an example. Inside the directory, we can see below hierarchy of files. All other scenarios should have the same hierarchy of contents.

```
.
├── README.md
├── base-setup.sh
├── jmeter
│   ├── 01-Solution-02-Facebook.jmx
│   ├── 02-Solution-02-Google.jmx
│   ├── 02-post-scenario-steps.sh
│   └── 02-pre-scenario-steps.sh
├── resources
│   └── user.properties
└── teardown.sh

```

Below is the correct order of the steps which TG runs the scripts of the solutions.

**Step [1]**
xx-pre-scenario-steps.sh - This is the initial file run by TG. Inside here, we are configuring the serverHost, serverPort, tomcatHost and tomcatPort parameters in user.properties file.
And it calls to the base-setup.sh file which is in one level up.
**[1.1]**
base-setup.sh - this is where we configure third party apps. Have used several linux command to configure and build applications. Also it will call tomcat rest API to publish configured apps.

**Step [2]**
As the next step TG invokes all the jmeter scripts inside jmeter directory.

**Step [3]**
Finally TG invokes xx-post-scenario-steps.sh and it calls to the teardown.sh. Mainly we un-deploy the apps deployed in the tomcat server and also remove temporary directories which were created from step [1]

We have to follow the same way of above naming convention on all the scenario scripts. 
Ex:- pre and post scenario scripts’ name should be started with the solution number (two digits)
The name of all jmeter scripts should be started with two digit number which starts from 01 and increment by sequentially.

**How to test and verify locally:**

Once you are done with the automation scripts please verify those as in the same order explained above. 
For verifying this locally, you can simply follow the below steps.
Export input variables in the terminal
**>>export serverHost=<is_host> serverPort=<is_port> tomcatHost=<tomcatHost> tomcatPort=<tomcatPort>**
Ex:
```
>>export serverHost=is.localtest.com serverPort=9454 tomcatHost=localhost tomcatPort=8090
```
Update below two lines in the base-setup.sh as replaccing values with your tomact user/password.
```
tomcatUsername=<username>
tomcatPassword=<password>
```
**Important** you have to enable the role manager-script and assign that role to the particular user in tomcat-users.xml file which is in <tomcat_home>/conf/ directory

Follow the Step [1] above ( as being on the same terminal )
```
ex:-> sh xx.pre-scenario-steps.sh
```

Run jmeter scripts in command line (still on the same terminal)
```
ex:-> path/to/jmeter/bin -n -t xx.xxxx.jmx -p path/to/user.properties -l xxxx.jtl
```

Follow the step [2] above. 
```
ex:-> sh xx-post-scenario-steps.sh
```

**Verifications**

Check and verify with the console while you run above scripts and check whether there is no any errors in the console, server console or tomcat server logs.
Use the Jmeter GUI and open the jtl file which generated from above step 3. If there is any jmeter failure then you can easily figure it out by using GUI.

# Product deployment alterations

This script should be used to make changes to the the deployment, for example if you need to change a configuration in the IS deployment you need have that within this script. Similarly for changes regarding to connectors (copy .jars, add configurations) should also be handled in this script.

# How to Write Tests

What are the tools you can use. 

- JMeter
- Selenium

Where to apply each option;

All the product level admin service calls and external API calls should be automated using Jmeter.
Selenium is the option when it has the limitations to automate the scenario from jmeter or when it needs some mandatory UI validations to be done.
## Writing Test Scripts

The test should be written in JMeter and you can use selenium within JMeter. Following explains how to write JMeter scripts and best practices to follow.

### Writing Jmeter Scripts and Naming Conventions.

When writing JMeter scripts you can use the template available at <template_repo>. 

Always follow the recommended best practices for managing the scripts. 
Use meaningful naming conventions for all the components(Thread groups, samplers) inside the scripts.
Use setup and teardown thread groups in addition to the default thread/s with test steps.


Use “Simple Controller” component for grouping and managing samples inside the Thread Groups.



Generic best practices for writing JMeter scripts can be found in the below urls. http://jmeter.apache.org/usermanual/best-practices.html

### Writing Selenium Tests

First, have in mind that selenium tests will also be run within JMeter and not as a separate selenium project. These tests are ideally used to automate 3rd party app interactions such as login to twitter, facebook etc. Selenium scripts should be scripted using JSR223 Sampler ( Do not use beanshell sampler).

Steps to add a JSR223 Sampler to your test suite.
Right click on your thread group and select Add -> Sampler -> JSR223 Sampler
	
	


Ones you add the JSR223 Sampler make sure to change the “Language” as java (BeanShell / Beanshell Engine)
	
	

 

# Setting up Prerequisites

If IntroductionIntroduction

Tests can be written in JMeter 





ACRONYMS
TG - TestGrid



