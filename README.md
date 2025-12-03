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


