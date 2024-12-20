# Performace-Testing-OpenCart-Website
# Content

- Load testing Report
- Summary
- Introduction 
- Install
- Prerequisites 
- Elements of a Minimal Test Plan
- Test Plan] 
- Collection of API
    - List of API
    - Load the JMeter Script     
- Make csv File
  [Make jtl File
- Make html File  
- HTML Report
- Stress Testing   
- Read Test Data from CSV file in Jmeter




# Load testing Report

| Concurrent Request  | Loop Count | Avg TPS for Total Samples  | Error Rate | Total Concurrent API request |
|               :---: |      :---: |                      :---: |                        :---: |      :---: |
| 1  | 1  | 3.350  | 0%      | 460   |
| 2  | 1  |  7.7     | 0%      | 460   |
| 3  | 1  |  12    | 0.29%   | 690   |
| 4  | 1  |  15.3  | 0.65%   | 920   |

### Summary
- While executed 3 concurrent request, found  636 request got connection timeout and error rate is 0.29%.
- Server can handle almost concurrent 460 API call with almost zero (0) error rate.



# Introduction

This document explains how to run a performance test with JMeter against an OpenCart E-commerce Site.

# Install

**Java**  
https://www.oracle.com/java/technologies/downloads/

**JMeter**  
https://jmeter.apache.org/download_jmeter.cgi  

Click =>Binaries    
=>**apache-jmeter-5.6.3\zip**

**We use BlazeMeter to generate JMX files**    
https://chrome.google.com/webstore/detail/blazemeter-the-continuous/mbopgmdnpcbohhpnfglgohlbhfongabi?hl=en

# Prerequisites
- As of JMeter 4.0, Java 8 and above are supported.
- we suggest  multicore cpus with 4 or more cores.
- Memory 16GB RAM is a good value.

# Elements of a minimal test plan
- Thread Group

    The root element of every test plan. Simulates the (concurrent) users and then run all requests. Each thread simulates a single user.

- HTTP Request Default (Configuration Element)

- HTTP Request (Sampler)

- Summary Report (Listener)

# Test Plan

Testplan > Add > Threads (Users) > Thread Group (this might vary dependent on the jMeter version you are using)

- Name: Users
- Number of Threads (users): 1 to 4
- Ramp-Up Period (in seconds): 10
- Loop Count: 1  

  1) The general setting for the tests execution, such as whether Thread Groups will run simultaneously or sequentially, is specified in the item called Test Plan.

  2) All HTTP Requests will use some default settings from the HTTP Request, such as the Server IP, Port Number, and Content-Encoding.

  3) Each Thread Group specifies how the HTTP Requests should be carried out. To determine how many concurrent "users" will be simulated, one must first know the number of threads. The number of actions each "user" will perform is determined by the loop count.

  4) The HTTP Header Manager, which allows you to provide the Request Headers that will be utilized by the upcoming HTTP Requests, is the first item in Thread Groups.

# Collection of API

- Run BlazeMeter  
- Collect Frequently used API  
- Save JMX file then paste => **apache-jmeter-5.6.3\bin**

    ### List of API 

    - [https://www.opencart.com/index.php?route=common/home](https://www.opencart.com/index.php?route=common/home)
    - [https://www.opencart.com/index.php?route=cms/feature](https://www.opencart.com/index.php?route=cms/feature)
    - [https://www.opencart.com/index.php?route=marketplace/extension](https://www.opencart.com/index.php?route=marketplace/extension)
    - [https://www.opencart.com/index.php?route=cms/company](https://www.opencart.com/index.php?route=cms/company)
    - [https://www.opencart.com/index.php?route=account/login](https://www.opencart.com/index.php?route=account/login)

   **OR**
    
  ### Load the JMeter Script 
   - File > Open (CTRL + O)
   - Locate the "OPENCART_T1.jmx" file contained on this repo
   - Continue open OPENCART_T1 to OPENCART_T6
   - Open those file
   - The Test Plan will be loaded  
   
   ![c](https://user-images.githubusercontent.com/92669932/189541560-025b250b-b00e-46a1-9b55-c4ed4f7835ec.jpg)

                                   
# Test execution (from the Terminal)
 
- JMeter should be initialized in non-GUI mode.
- Make a report folder in the **bin** folder.  
- Run Command in __jmeter\bin__ folder. 


 ### Make jtl file

```bash
  jmeter -n -t  Opencart_t1.jmx -l Opencart_t1.jtl
```      
  Then continue to upgrade Threads(1 to 6) by keeping Ramp-up Same.   
  
  ![a](https://user-images.githubusercontent.com/92669932/189541580-9345c967-36a3-48c1-bf51-692431658b27.jpg)   
  
  ![d](https://user-images.githubusercontent.com/92669932/189541861-ce9b4d40-3edb-408b-affd-c3c98020fddf.jpg)

After completing this command  
   ### Make html file   
  
  ```bash
  jmeter -g report\Opencart_t1.jtl -o Opencart_t1.html
```
 

  - **g**: jtl results file

  - **o**: path to output folder  

  ![b](https://user-images.githubusercontent.com/92669932/189541594-c608e5c9-9679-4c80-9f90-855985cfb630.jpg)  
  ![f](https://user-images.githubusercontent.com/92669932/189541801-59a45bdd-6a12-44f3-9194-ff41b2c3d954.jpg)  
  

# HTML Report

**Number of Threads 1 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![1](https://user-images.githubusercontent.com/92669932/189543492-df0751ca-3642-4e3f-a050-0454e38117ef.jpg)  |  ![2](https://user-images.githubusercontent.com/92669932/189543499-17c168a2-5b32-4710-9bc0-df7a2b3656c7.jpg)

**Number of Threads 2 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![image](https://github.com/user-attachments/assets/875be6f5-c94d-4fce-b326-48750720a106) |  ![image](https://github.com/user-attachments/assets/cf05fe55-4130-41ad-8304-8178c37afd46)
)


**Number of Threads 3 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![image](https://github.com/user-attachments/assets/d0913bb2-0d21-4e6d-9e52-a50640174b5a) |  ![image](https://github.com/user-attachments/assets/41ee7752-6634-4bd7-bdf7-0786681bddef)


**Number of Threads 4 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![image](https://github.com/user-attachments/assets/3557e30a-bd53-4fbd-b823-0f3a279771c6)  |  ![image](https://github.com/user-attachments/assets/be54af9e-91e5-406b-ad34-48e8ac93c028).







