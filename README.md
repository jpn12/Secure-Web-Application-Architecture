# Secure-Web-Application-Architecture
<img width="1321" height="406" alt="Project Diagram" src="https://github.com/user-attachments/assets/b3d1db62-0895-4c3b-9777-4f9a720d9fde" />


This diagram represents a secure web app architecture i built while learning some of the azure services.
The goal was to design a web application that is accessible from the internet but not directly exposed, while implementing security layers.

-----------------------------------------------------------------------------------------------------------------------------------------------

While designing this project, I realized I didn’t want my web application to be directly exposed to the internet.
Why is that?

When a web app is publicly exposed, it becomes an easy target for attackers. They can freely scan it for vulnerabilities using tools like Nmap, Nikto, or automated bots that constantly crawl the internet looking for weaknesses. These scans can reveal: 
- Open Ports
- Outdated Frameworks
- Exposed endpoints
- misconfigurations
- etc...


I built a Virtual Network (VNet)
Azure enforces a rule:
The Application Gateway must have its own subnet, so I created the App Gateway Subnet and placed it there.
From that subnet, it routes traffic, but only internally to a Web App Subnet.
This is where my web application lives, running on Azure App Service(Not directly facing the internet, no public IP)

To simulate a real environment, i added a VM subnet.
here i placed a virtual machine that represents optional backend workloads—databases, internal services, or admin tools.

<img width="510" height="401" alt="image" src="https://github.com/user-attachments/assets/a4b9664b-6173-4b35-8f19-c2393b2ed9a1"/><br>

but i also wanted to avoid exposing SSH/RDP ports, so i implemented bastion.<br>
It provides SSH/RDP access directly through the Azure portal, without being exposed to the internet.
This meant I could safely connect to my VMs without punching holes in the firewall.<br>

<img width="1021" height="641" alt="image" src="https://github.com/user-attachments/assets/d99898ad-3a81-4f4a-83b8-0c521e36e103" />


---------------------------------------------------------------------------------------

<img width="792" height="371" alt="image" src="https://github.com/user-attachments/assets/7e466fc8-ee1c-4d81-95ac-d7056a215f72"/><br>

The Application Gateway became the front door of this architecture.
It handles all incoming traffic, but more importantly, I configured it with:
- Frontend IP & port listeners
- HTTP/HTTPS routing rules
- and most importantly, the Web Application Firewall (WAF)

<img width="1187" height="819" alt="project1" src="https://github.com/user-attachments/assets/5e9d711e-f618-424b-a90c-c552f237f95f" /><br>

I configured a backend pool so the Application Gateway knows where to route incoming traffic to my web application<br>
<img width="1269" height="541" alt="image" src="https://github.com/user-attachments/assets/17c3f3d6-ba6f-40b0-81d8-ef6ba9a53071" />

I created some custom rules on the WAF, including a geoblocking and rate limiting rule.<br>
<img width="1519" height="607" alt="image" src="https://github.com/user-attachments/assets/a82c4ac6-6f00-4890-b0e4-71c33053fa01" />

To continue monitoring all services, ive decided to create a Log Analytics workspace to centralize all the logs. These logs will then be sent to Sentinel.<br>

<img width="384" height="390" alt="image" src="https://github.com/user-attachments/assets/8e869fc2-9306-4217-aa98-1d3430a44eb4" /><br>

<img width="1095" height="643" alt="SEND" src="https://github.com/user-attachments/assets/2555dbf9-097b-451c-807f-38df32f03e57" />





