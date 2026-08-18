<div align="center">
  <h1 style="color: #0366d6;">Corporate Network Architecture & Security Shield</h1>
  <h3 style="color: #24292e;">Cisco Packet Tracer Technical Documentation</h3>
  <p><b>Connecting & Securing a Headquarters and Branch Office</b></p>
  <p><i>Lead Architect: Mekal Butt | Contact: mekalbutt.services@gmail.com</i></p>
</div>

<hr size="4" color="#0366d6">

<h2 style="color: #0366d6;">1. Executive Summary & Network Topology</h2>
<p>This project simulates a realistic company network connecting a main Headquarters (HQ) to a remote Branch office over an Internet Service Provider (ISP). Instead of plugging everything into one big open network, this design separates different departments for better security.</p>
<p>It uses smart routing so the network automatically knows where to send data, and it relies on a Cisco ASA firewall to act as a strict security guard, blocking unwanted internet traffic from getting inside.</p>

<div align="center">
  <img src="https://github.com/user-attachments/assets/1a0ec0c4-455a-4831-9f26-3b5849658264" alt="Network Topology" width="850" style="border: 2px solid #0366d6; border-radius: 8px;">
  <p><i>The Complete Multi-Site Network Topology</i></p>
</div>

<h3 style="color: #28a745;">The Core Network Features</h3>
<ul>
  <li><b>Separating Traffic (VLANs):</b> The Operations department and the Server Farm are kept apart. This stops basic network issues and keeps traffic clean.</li>
  <li><b>Connecting the Networks:</b> The main router is set up to let these separated departments talk to each other only when allowed.</li>
  <li><b>Smart Routing (OSPF):</b> The routers automatically learn the best paths to send data. If a link goes down, the network figures out another way to keep working.</li>
  <li><b>Network Helpers (DHCP & DNS):</b> Servers automatically hand out IP addresses to computers so users don't have to do it manually, and they translate website names (like <i>www.hq-internal.com</i>) into IP addresses.</li>
  <li><b>Strong Firewall:</b> The Cisco firewall blocks outside traffic by default and uses rules to make sure only safe, approved data gets through to the servers.</li>
</ul>

<hr size="2" color="#e1e4e8">

<h2 style="color: #0366d6;">2. Devices & Tools Used</h2>
<table border="1" width="100%" cellspacing="0" cellpadding="8" style="border-collapse: collapse; border: 1px solid #d1d5da;">
  <tr style="background-color: #f1f8ff; color: #0366d6;">
    <th><b>Category</b></th>
    <th><b>Hardware / Tool</b></th>
    <th><b>What It Does</b></th>
  </tr>
  <tr>
    <td><b>Security Firewall</b></td>
    <td>Cisco ASA 5506-X</td>
    <td>The security guard. It inspects traffic and blocks unauthorized access.</td>
  </tr>
  <tr>
    <td><b>Core Routers</b></td>
    <td>Cisco ISR 4331 Routers</td>
    <td>The traffic directors. They share routing maps to connect HQ, the ISP, and the Branch.</td>
  </tr>
  <tr>
    <td><b>Network Switches</b></td>
    <td>Cisco Catalyst 2960</td>
    <td>Connects the PCs and servers together while keeping different departments separated.</td>
  </tr>
  <tr>
    <td><b>Servers</b></td>
    <td>DHCP & DNS Servers</td>
    <td>Provides IP addresses automatically and hosts the internal company website.</td>
  </tr>
  <tr>
    <td><b>Software</b></td>
    <td>Cisco Packet Tracer</td>
    <td>The virtual lab environment used to build and test this entire network.</td>
  </tr>
</table>

<hr size="2" color="#e1e4e8">

<h2 style="color: #0366d6;">3. How the Pieces Work Together</h2>

<h3 style="color: #d73a49;">Headquarters (HQ) Setup</h3>
<ul>
  <li><b>The Switch:</b> Connects all the computers and servers, putting them into their correct security zones.</li>
  <li><b>The Router:</b> Handles traffic moving between the different zones inside the building.</li>
  <li><b>The Firewall:</b> Sits at the edge of the building, separating the safe inside network from the risky outside internet.</li>
</ul>

<h3 style="color: #d73a49;">Branch Office Setup</h3>
<ul>
  <li><b>The Remote Network:</b> A smaller setup that uses smart routing to find its way back to the main Headquarters across the internet.</li>
</ul>

<hr size="2" color="#e1e4e8">

<h2 style="color: #0366d6;">4. Step-by-Step Data Flow</h2>
<ol>
  <li><b>The Request:</b> A user at the Branch office types <i>www.hq-internal.com</i> into their browser.</li>
  <li><b>Finding the Address:</b> The PC asks the DNS server at HQ to turn that website name into an IP address.</li>
  <li><b>Finding the Path:</b> The Branch router looks at its map and sends the request across the internet to HQ.</li>
  <li><b>Passing Security:</b> The HQ Firewall inspects the request. Since it comes from the trusted Branch office, it lets it pass.</li>
  <li><b>Delivering the Page:</b> The HQ router delivers the request to the Web Server, which successfully sends the webpage back to the Branch PC.</li>
</ol>

<hr size="2" color="#e1e4e8">

<h2 style="color: #0366d6;">5. Core Concepts Covered</h2>
<ul>
  <li><b>Subnetting & IP Addressing:</b> Designed logical IP layouts (like `192.168.10.0` and `192.168.20.0`) to organize the network.</li>
  <li><b>Dynamic Routing (OSPF):</b> Programmed routers to automatically learn and update paths across the network without manual intervention.</li>
  <li><b>Access Control Lists (ACLs):</b> Built network-level security rules to explicitly allow or deny data packets (like blocking random internet traffic while allowing Branch office traffic).</li>
  <li><b>Network Address Translation (NAT):</b> Configured firewall rules to translate private internal IPs into public internet IPs.</li>
  <li><b>VLANs & Segmentation:</b> Sliced a single physical switch into multiple isolated virtual networks to separate departments.</li>
  <li><b>Server Administration:</b> Deployed and configured HTTP (Web), DNS (Name Resolution), and DHCP (Automated IP leasing) services.</li>
  <li><b>Cabling & Ports:</b> Applied the correct physical wiring logic (Straight-through vs. Crossover cables) and mapped specific router/switch ports (Gigabit vs. FastEthernet) to interface commands.</li>
</ul>

<hr size="2" color="#e1e4e8">

<h2 style="color: #0366d6;">6. Conclusion</h2>
<p>In short, this project is a fully functional simulation of a corporate network that securely connects a headquarters to a remote branch office over the internet. I set up routers to automatically find the best paths for data, servers to handle IP addresses and internal websites, and a strict firewall to ensure only authorized traffic can pass through. It proves that the network is not only fully connected from end to end, but properly secured against outside threats.</p>
