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
This meant I could safely connect to my VMs without punching holes in the firewall.

---------------------------------------------------------------------------------------

<img width="792" height="371" alt="image" src="https://github.com/user-attachments/assets/7e466fc8-ee1c-4d81-95ac-d7056a215f72"/><br>
The Application Gateway became the front door of this architecture.
It handles all incoming traffic, but more importantly, I configured it with:
- Frontend IP & port listeners
- HTTP/HTTPS routing rules
- and most importantly, the Web Application Firewall (WAF)

<img width="1187" height="819" alt="project1" src="https://github.com/user-attachments/assets/5e9d711e-f618-424b-a90c-c552f237f95f" /><br>

I Configured a backend pool so the gateway could communicate with my web application<br>
<img width="1263" height="567" alt="image" src="https://github.com/user-attachments/assets/442be686-41fa-47b5-b7de-1625eccc2f30" />

