# SSH Honeypot-Server-Project
## Objective
 * I deployed a T-Pot honeypot on a DigitalOcean cloud server with no firewall restrictions, intentionally leaving it exposed to the entire world. Within minutes, attackers began probing my server. Within three hours, I had logged over 2,000 attack attempts from dozens of countries.
This project is a controlled experiment in cybersecurity threat intelligence. By creating a decoy server that mimics real services such as SSH, Telnet, HTTP, SIP, and more, I can watch attackers in real time on an animated global attack map. Capture their usernames and passwords as they try to break in. Analyze their behavior, what they target, where they come from, and what commands they run.

## Skills learned

* Configuring a cloud server with no inbound firewall rules 

* Creating a fake admin user ("Zach") with sudo privileges for monitoring attacker targeting

* Cloning and deploying T-Pot from GitHub

* Understanding T-Pot deployment types (Hive vs. Sensor vs. MINI vs. Mobile vs. Tarpit vs. LLM)

* Navigating T-Pot's tools: Attack Map, Kibana, CyberChef, Elasticvue, Spiderfoot

* Analyzing live attack data across multiple protocols (SSH, HTTP, Telnet, SIP)
 
## Tools used
* DigitalOcean a CaaS with a configuration of 8GB/4CPU Droplet

* Windows PowerShell – SSH client for remote server management

* Ubuntu 22.04/24.04 – Operating system on DigitalOcean Droplet

* Git – To clone T-Pot repository

* T-Pot (telekom-security/tpotce) A All-in-one multi-honeypot platform that allows access to the T-Pot Attack Map, Kibana, CyberChef, Elasticvue, Spiderfoot and Cowrie    

* T-Pot Hive – Deployment type selected (includes all honeypots + visualization tools)

* Various honeypots – SIP, HTTP, Telnet, and other protocols automatically included

## Step-by-Step Build Process (From My Experience)
1. Create DigitalOcean Server
  At first I created a 2GB RAM / 1 CPU Droplet powering through Ubuntu but unfortunately it was not enough so I upped it to an 8GB RAM / 4 CPU system. 
also on the server I made sure to Intentionally disabled all inbound firewall restrictions this allowed anyone in the world to attempt connections on any port

2. Connect via Windows PowerShell
   I Used SSH to connect: ssh root@<server-ip> I used the root Ipv4 provided by DigitalOcean.  

3. Update the Server apt-get update && apt-get upgrade -y
At this step I made sure all system tools were current and up to date before deployment.

4. Created a Fake User called "Zach" by following these commands.
    bash, adduser zach ,usermod -aG sudo zach I then gave the Fake User Admin roles. 
    
5. Switched to Zach's Home Directory
bash, su - zach, cd ~

7. Clone T-Pot Repository
bash
git clone https://github.com/telekom-security/tpotce
8. Navigate and Install
bash
cd tpotce
ls -la                    # Located install.sh script
./install.sh
9. Selected a  T-Pot Type
The installer prompted me to choose from:

  *  Hive

  *  Sensor

   * LLM

  *  MINI

   * Mobile

   * Tarpit

I selected: Hive because it was perfect for my single server.  
10. Complete Installation
Followed remaining prompts

Installer configured Docker, changed SSH port to 64295, set up firewall rules (for protection while keeping honeypot ports open)

Rebooted server when finished: sudo reboot

11. Access T-Pot WebGUI
Opened browser to: https://<my-server-ip>:64297
At this point I Entered the username and password I created during installation and Was greeted with T-Pot home screen containing:

   * Attack Map - live animated map

   * Kibana - dashboards

   * CyberChef - encoding/decoding

   * Elasticvue - Elasticsearch browser

   * Spiderfoot - OSINT tool

12. Monitored the Attack Map
When I neared the end of my project I decided to leave the attack map open for almost 3 hours, and i was met with over 2,000 attacks detected and the top cvountrties being the United states, China, United Kingdom and France. I also observed a wide range of attack protocols thanks to the attack maps very well put together dashboard SIP (VoIP), HTTP/HTTPS, Telnet brute force, SSH brute force and more.

# Screenshots 
