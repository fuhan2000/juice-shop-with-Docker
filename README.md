# juice-shop-with-Docker

## Objective
In this project, we set up OWASP Juice Shop to run under Docker in Kali Linux. 

The original idea for this project came from <a href="https://www.youtube.com/watch?v=xwcPgeEFnuM">Bug Bounty and Pentesting with Docker</a> by Netsec Explained.

### Tools Used
- Kali Linux
- Docker

### Summary of Findings
It is possible to set up, run, and stop OWASP Juice Shop in Docker. 

## Lab Details
### Virtualbox NAT Network Settings
<img src="https://i.imgur.com/ThaONKq.png" width="400" />

*Ref 1: Kali Linux Network Settings*

Kali Linux has internet access.

### Procedures
On Kali Linux, go to https://hub.docker.com.

<img src="https://i.imgur.com/S2kjv5M.png" width="400" />

*Ref 2: Screenshot of hub.docker.com*

Click on bkimminich/juice-shop, the first result.

<img src="https://i.imgur.com/UI8flzL.png" width="400" />

*Ref 3: bkimminich/juice-shop*

Click on Copy.

<img src="https://i.imgur.com/oA3zr2b.png" width="400" />

*Ref 4: Click Copy (highlighted in yellow)*

 In Kali Linux, run the following commands:
 
 *sudo apt-get update*
 
 *sudo apt install docker.io*
 
 *sudo apt install podman-docker*

 Modify the /etc/containers/registries.conf such that unqualified-search-registries show the following:
 
 <img src="https://i.imgur.com/4WcTqJs.png" width="400" />

 *Ref 5: /etc/containers/registries.conf*

Reboot Kali Linux and run:

*docker pull bkimminich/juice-shop*

A sample output is shown below:

<img src="https://i.imgur.com/siA54Gw.png" width="400" />

*Ref 6: Sample output from docker pull bkimminich/juice-shop*

To run Juice Shop in the background, run:

*docker run -d -p 127.0.0.1:3000:3000 bkimminich/juice-shop*

<img src="https://i.imgur.com/IM5SEe2.png" width="400" />

*Ref 7: docker run*

On Burp, start the browser. Point the browser to 127.0.0.1:3000.
The browser will show OWASP Juice Shop.

<img src="https://i.imgur.com/L1pivTm.png" width="400" />

*Ref 8: Browser on the left-hand side. Burp on the right-hand side*

To stop the docker process, it is necessary to find its 'Container ID' through *docker ps*.

Then run *docker stop [Container ID]*

<img src="https://i.imgur.com/rHft7qu.png" width="400" />

*Ref 9: [Container ID] = b5c7fb05af54*
