## Hi there 👋

I'm currently a student at Temple University studying Cybersecurity & Human Behavior
This page is to document the hands-on labs and project i do outside of class
Instead of reading things in textbooks, I want to actually build, break, and understand how networks, operating systems, and defense controls function in the real world

Lab 01: Inspecting Plaintext HTTP traffic (info.cern.ch)
* **Date:** November 1st 2026
* **Target:** 'http://info.cern.ch/'
* **Tools Used:** Wireshark, macOS Terminal, Firefox

#### Steps
* Set up a live packet capture on my Mac using Wireshark
* Navigated to `http://info.cern.ch/` (the world's first website, which runs over unencrypted HTTP on port 80)
* Applied an `http` display filter in Wireshark and isolated packet `147` containing the `GET / HTTP/1.1` request
* Right-clicked the packet and used **Follow -> TCP Stream** to reconstruct the entire communication stream between my Macbook and the CERN web server

#### Why It Matters
* Demonstrates what unencrypted web traffic looks like to anyone on the same network or running a passive packet sniffer
* No password, private key, or certificate needed to read the page headers, server type (Apache), and the raw HTML text (`<h1>http://info.cern.ch - home of the first website</h1>`). Everything traveled over the physical wire in clear text
  
#### What I Learned
* In Wireshark's TCP stream window, the **red text** shows what my machine requested, and the **blue text** shows what the server returned
* The "Follow TCP Stream" feature strips away the lower-layer transport overhead so you can read the exact application payload crossing the wire
* If a site doesn't enforce HTTPS, any sensitive data—like passwords, session tokens, or personal info—is completely visible to anyone sniffing the network
  
* **The human side:** Users will click anything without inspecting what they are clicking first. Security architecture can't rely on human caution; networks and browsers have to enforce automated redirects and HSTS (HTTP Strict Transport Security) to protect users from their own habits.

#### Wireshark capture
![Wireshark TCP stream showing plaintext HTTP traffic from CERN](./wireshark%20cern%20traffic.png)
