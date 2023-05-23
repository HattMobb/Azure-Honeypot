# Azure-Honeypot
Using T-pot to create a virtualized honeypot on Azure

Technologies used:
- Microsoft Azure
- Telekom Security's Tpot honeypot

In short, a honeypot is a mechanism used to detect, deceive, or gather information about unauthorized access attempts or malicious activities on computer networks or systems. 
The purpose of a honeypot is to divert and distract attackers from the actual target systems, allowing security professionals to observe and analyze their techniques, motivations, and objectives. By closely monitoring the activities within the honeypot, security professionals can gain insights into the attackers' methods, tools, and vulnerabilities they exploit.

Given my interest in cybersecurity, I was naturally curious about how attackers in the real world might attack a system in the wild and decided to find out first hand. I used Azure so spin up a VM for safety (no "real"/ procuction system would be put at risk) and Telekom Security's Tpot honeypot to act as an irresistible  target (https://github.com/telekom-security/tpotce). 


## How to

- I began by creating a host machine using Azure, the basic specs of which are below (make sure to consult system requirements of T-pot found here https://github.com/telekom-security/tpotce#system-requirements)
- Nothing fancy needs to be configured for disk storage or networking for the purpose of this lab.
![Screenshot 2023-05-22 111542](https://github.com/HattMobb/Azure-Honeypot/assets/134090089/0139dc72-c3bd-4e9b-a78e-a5bf6ca40c4e)

- A private key will be generated with which you will use to log into the fresh VM (if you get stuck, follow these instructions)


![Screenshot 2023-05-22 120955](https://github.com/HattMobb/Azure-Honeypot/assets/134090089/0363f4fb-afb5-4413-a535-66993bc439b8)

- Make sure your fresh VM is up to date via 
  `sudo apt update && sudo apt upgrade -y`
 
- I'm pulling T-pot straight from Github so install Git
   `sudo apt install git`
  
 - Clone the repo onto the VM
  `https://github.com/dtag-dev-sec/tpotce`
  
 - Drill through the directories to the install script and run it via 
  `sudo ./install.sh --type=user` 
  
 - Once installed the SSh session will end and there is a little configuration to be done.
 - Tpot lists it's required ports to fully function here: https://github.com/telekom-security/tpotce#required-ports
 - Per the documentation, to allow access to the Tpot dashboard via the browser, port 64297 must be enabled and for SSH access, port 64295  must be enabled. This can be done from the Azure Networking tab by clicking the "add inbound rule" button and setting peramenters. Make sure to set the "Source IP" of the SSH and BROWSER rules to your own public network IP so that you are able to access the management options. The last rule opens ports and allows us to collect attacker information as the machine is targeted from any IP address in the world.

![Screenshot 2023-05-22 140522](https://github.com/HattMobb/Azure-Honeypot/assets/134090089/59102268-127a-4b5a-9767-e444a45849fb)

- Once rules are in place, you can navigate to `https://<YOUR_VM_IP>:64297` to view the Tpot browser access page 
![Screenshot 2023-05-22 135331](https://github.com/HattMobb/Azure-Honeypot/assets/134090089/a396ce55-ffca-420e-ae3b-8af458dea243)

- Or via SSH with `ssh -i <private key path> username@YOUR_VM_IP -p 64295`

- You can view many different stats about attacks on your machine via the Kibina - Dashboard options 



![Screenshot 2023-05-22 144021](https://github.com/HattMobb/Azure-Honeypot/assets/134090089/a1bd2ebc-264f-469e-ada9-e1dbda8f2cbd)


![Screenshot 2023-05-22 144055](https://github.com/HattMobb/Azure-Honeypot/assets/134090089/47fcd279-0eb2-4c00-9ad8-cb6161d99ce9)



- Play around and check out the attacks that start pouring in.

  
