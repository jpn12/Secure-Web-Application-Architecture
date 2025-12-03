# Secure-Web-Application-Architecture
<img width="1321" height="406" alt="Project Diagram" src="https://github.com/user-attachments/assets/b3d1db62-0895-4c3b-9777-4f9a720d9fde" />


This diagram represents a secure web app architecture i built while learning some of the azure services.
The goal was to design a web application that is accessible from the internet but not directly exposed, while implementing security layers.

-----------------------------------------------------------------------------------------------------------------------------------------------

While designing this project, i decided that i didnt want my web application to be directly exposed to the internet. whys that?
if my web app is exposed to the internet, attackers can scan for vulnerabilities, using tools like nmap, nikto or automated bots trying to find:
- Open Ports
- Outdated Frameworks
- Exposed endpoints
- misconfigurations
- etc...


