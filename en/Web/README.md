# Getting Started

* In this section, Web application enumeration tools, tips and tactics, exploitation types are tried to explain.  


# Enumeration & Information Gathering

### Web Server Type & Version Detection

* By determining the web server information and version information, a road map can be determined for attacks against web applications. It is necessary to learn the server name and version information so that we can quickly detect the vulnerabilities caused by the version. So how can we learn the web server information.

    - Looking at the **header information** returned from the web server (**whatweb tool**, **curl**, **browser inspect** etc. tools can be used.)
    - **Wappalyzer** tool can be used. (chrome, mozilla plugin)
    - Scanning to the web server port can be done with **nmap**. (The **-sSVC** parameter is recommended.)
    - Prediction can be made by doing **os detection with nmap**.

### Web Technologies in Use

* Various critical vulnerabilities may occur in applications running on web servers, ready-made systems, frameworks or systems that are not updated. In this respect, it can be very useful to learn what technologies are used. So how can we learn about the technologies that work on the application?

    - **Whatcms** tool can be used. (online)
    - **Nikto** tool can be used.
    - **Retirejs** plugin can be used. (to detect outdated js files)
    - **Wappalyzer** plugin can be used
    - **Wpscan** can be used to scan wordpress applications.
    - **Joomscan** can be used for Joomla sites.

### Firewall Detection

* If the web application is located behind a web application firewall, some scans may give false positive results, may not work properly, and therefore may not be healthy. Therefore, if the existence of a firewall is detected, different techniques can be used in enumeration vs exploit stages. So how to determine if any firewall is in use?

    - **wafw00f** tool can be used.
    - Web server **response header information** can be viewed. (waf or the server name might be in headers)
    - **Whatwaf** tool can be used.
    - Nmap can be used for banner grabbing and get information from live port.


### Ip History Search
* If web applications are not hosted directly at cloud service providers, web application firewalls will only be active with dns redirection for WAF use. Therefore, requests are forwarded to the real server via WAF with the reverse proxy step. Incorrectly configured servers can be accessed by using the real IP address. At this point the WAF can be bypassed. The real ip address can be used directly or with the dns hosts configuration files. To search ip history of a server, we can use the following applications/tools.

    - **https://securitytrails.com** web site can be used.
    - **https://www.virustotal.com/gui/** web site can be used.
    - **https://viewdns.info/iphistory/** web site can be used.


### Port scan
* By scanning the port where the web application is running, information can be collected by the banner grabbing method. Different ports of the ip address pointed to by the web application may be open. It is useful to examine the web server port and other known ports together. Different open ports can lead us learn informations about the server. What can we use for this enumration?
    - Of course **nmap**.
        - Nmap with **-sS** means syn scan. This options should used to get more accurate results for port status.
        - **-sV** parameter use for server detection. Probe open ports to determine service/version info.
        - nmap **-h** parameter can be used for more information. (**https://nmap.org/book/man-briefoptions.html**)
    

### Directory Search
* One of the most important enumeration steps is directory browsing. Accessible pages of web applications are the only content that we can scan and search for vulnerabilities. If the configuration files, password-free management interfaces and site archive files are accessible on the server, serious information disclosure and vulnerabilities can be caused. How can we enumerate these files/pages?

    - Crawlers can be used to enumerate all accessible pages from links. (**Burp suite** crawler can be used)
    - Directory bruteforce tools can be used. (**Dirsearch**, **wfuzz**, **gobuster**, you are strong as your wordlist)
    - **robots.txt** file can be viewed
    - Platform spesific pages should be checked. If the site uses wordpress, web can search for well known WP upload and configuration pages etc. 

### Subdomain Search

### Google Dorks

### Internal Ip/Path Disclosure (HTML Source Code Analysis)

### Shodan Search
?> **Time** is money, my friend!
> test
### Web Archive Search

# Exploitation 

### XSS

### SQL Injection

### File Upload

### File Inclusion

### Command Injection

### Brute Force

### DNS Zone Transfer

### CSRF

### Host Header Injection

### SSL Encrytptions Vulnerabilities