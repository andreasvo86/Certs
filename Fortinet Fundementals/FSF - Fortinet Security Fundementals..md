https://training.fortinet.com/course/view.php?id=39249

# FCF - Introduction to the Threat Landscape 2.0 Self-Paced

## Module 1 intro to cybersec
### Lesson 1
Principels of information security 
ID what is Cybersec 
Learn about first line of decence. 

### Lesson 2 what is cybersec
Describe terms:  
cybersec, 
Information sec and 
Information system security

Explain how IT sec determine what information needs protection

Explain the first line defence against cyber-attacks. 

#### What is cybersec. 
The practice of ptorecting computer networks, devices and info from damage, loss, unath access. 
Categories: 
Critical infra
app sec 
net sec
iot sec 
cloud sec 
people and processes 

Info-sec: 
Tools and processes used for Preventing, detecting and remediating threats.  Digital and physical.  

Information systems sec is part of info-sec. 
Protection of information systems from unath access, modification, destruction, denial of access. 


#### First line of defence and precautions. 
Educate people 
prepare for disaster.  Backup and recovery. 


---------------------------------------------

### Lesson 3 Principles of information sec 
Objective 
List principles of infosec 
Describe terms:  
Authentication, athorization, accountng. 

CIA 
Confidentiality 
  Data is  kept confidential and private 
Integrity 
  Data is authentic, accurate, reliable and free of tampering. 
Availability. 
  Data is available to those who need it. 

Info-sec 
DAD - 
Disclosure
   Confidential data is exposed to unath parties. 
Alteration
   tampering of data cannot be prevented, or authenticity  of data cannot be determined. 
Denial 
   unathorized agents prevents from accessing data. 


AAA 
Controll resources 
enforce policies 
audit usage 

Auth - ID and verify a person or thing. 
Authorization - Controlling access to resources. 
Record keeping and tracing of agent activities on devices and networks. 


## Module 2 The threat landscape 

### Lesson 1 - Overview 
Threat landscape: 
All known and possible threat to computer networks. 
Objectives:  
* ID different type of bad actors. 
* Describe attack vectors, cybersec threats, and the categoris the threat fit into. 
* define threat intelligence and explain how it is processed. 
* Describe different attack frameworks. 

### Lesson 2 - threat actors. 
Objective 
Describe different type of bad actors and motivations 
Describe different categories of hackers 

Bad actors = person who try to steal, sabotage, or stop you from using computer systems or accessing info that is stored on or in transit between compute devices. 

Categorised based on:  
Character 
Motivation 
Attack method 

Types: 
Explorer
Hactivist 
Cyber terrorist 
Cyber criminal 
Cyber warrior 

Explorer - 
self-interested 
Biggest motivator - notorierty. 
Attack vector - Phishing. 

Hactivist - 
Believe in a cause 
Motivated by ideologi. 
Acts colletivibly. 
Attack vector - Botnet, Ddos

Cyber-terrorist 
Driven by ideology. 
Want to disrupt society.  
Attacks IoT (critical infrastructure) 
Operate as a cohesive unit. 
attack vector - Spear Phishing. 

Cyber criminal. 
Motivation = Money . 
Attack vector - Ransomware, ID-theft. 

Cyber warrior. 
Least self-interested, but most dangerous. 
Nation state resources. 
Attack vector - Espionage, zero-days.  
Do their own research. 

Hacker categories 
White hat 
 - Ethical 
Black hat 
 - Malicious
Grey hat 
* Not malicious, but not always ethical (explorer)
Blue hat
* Ethical, hired third-party (pentesting). 


### Lesson 3 - Cybersec threats
objectives: 
Describe cyber sec threats and list examples. 
List the main cyber threat categories 
Describe the attack vectors profiled. 

What is cyber sec threat? 
A action exploiting a vulnrabiltiy that result in harm to network or computer system. 
Black hat are instigators. 
attack vectors are methods used by a bad actor to access or inhibit a network, system or facility. 
method = How a vulnrabiltiy is explotied. 
  - Vulnrability  (user)
  - Mechanism  (malware, and social engineered message)
  - Pathway  (email)
  - Vulnrability, mechanism and pathway = an Attack Vector. 

Attack path is the chain of events that happen when  attack vectors is exploited. 

Cyber sec - 4 main cetgories 
Social engineering 
Malware 
unath access 
system design failure
 - Sec flaw in computer system or app used to gain access. 

Attack vectors - common ones. 
- DoS and DDoS
- Phishing 
	- whale phishing - High level target.  
	- spear phishing - Targed phishing 
Pre and post exploit stages.  

Birthday attack - Hash-algo weakness. Multiple inputs produce same output. 

### Lesson 4 - Threat intelligence 
Objectices: 
Define threat intelligence 
Describe formatting stanrads for threat intel 
Describe steps for processing threat intel 


What is threat intel 
Evicence-based knowledge  (include context, mechanism, indicators, implications, and actionable advice)  about an existing or emerging menace or hazard to assets that can be used to inform decisions about the subjects responce to the hazard. 

Thre characteristics.  
Relevant 
 - Must impact your org 
actionable 
 * Is there enough info to act upon ? 
contextual 
* is there eough info to asess the threat? 

multiple pieces of Information that in itself is not threat intel can become intel when put toghether. 

Where is threat intel found? 
internally - Logs, incident repots, network traffic, pentesting results. 
Externally - NIST, government sites/orgs, 
Private - fortiguard. Sans.org institute.  

CVSS - common vulnrability scoring system. 
Mitre attack - online db 

Formating standards for threat intel. 
STRIX - Structured threat info expression. 
  Community driven. 
  IoC 
  
TAXII - Trusted automated Exchange of Indicator Information.  
App protocol for system to system 
https 
rest api 

Processing threat intell 
Convert data to intel you can act on 
1. ID the most vital threat to stop 
2. assemble threat intel from intenal and extenal sources 
3. process the info.  
	1. Find baselines. 
4. Analyze info, 
	1. look for IoCopromise
5. Disseminate analysis and any new info 
	1. STIX and TAXII 
6. Implement lessons learned 

### Lesson 5 - Attack frameworks 
Objectives:   
Describe the cyber kill chain 
List and explain the stages of the cyber kill chain 
Explain the befits to MITRE and ATT&CK matrix 

Attack frameworks:   
- ID situation 
- Classifying problem 
- Analayzing impact 
- Develop strategies

Used to combat APT (advanced persistent threats). 

Cyber Kill Chain.  
Widely used.  
Developed by Lockheed martin. 
1. Reconnaissance 
	1. Gather intel. 
2. Weaponization. 
	1. Creates payload that can be delivered to the target.  
3. Delivery 
	1. Deliver payload to target. 
4. Exploitation 
	1. Access systems to leverage vulnrabilities. 
5. Installation 
	1. Establish foothold in target systems.  (persistent stay)
6. C & C
	1. Establish communcation with compromised systems remotly. 
7. Exfiltration 
	1. Extract data. 

Disadvantage to kill chain. 
Assumes origin of attack is external. 
Aims to  support and reinforce traditional defence methods. 


MITRE ATT&CK. 
Guidelines. 
Evolving resource.  
Provides a language to describe cyber-attacks. 

Lists techniques and methods used by attackers to compromise targets. 
Techniques are grouped by categories based on type of attack or activity. 
Categories examples:  Initial access, execution, persistence, defence evation. 

Key benefit - Provide common languge to describe threaths.  
Helps ID and priority most critical threat and vulnrability. 

Provide overview of most common: 
Tactics
Techniques 
Procedures  
TTP  used by attackers. 



## Module 3 - Social engineering 

### Lesson 1 -  Social engineering overview 
Mainipulating people to gain advantage.  Often at expence of the victim. 

Describe the different methods of social engineering. 
Describe attack vectors, methods, and threat indicators associated with insider threats. 
Describe fraud, scams and influence campaings. 

### Lesson 2 - Social engineering technique part A
Objectives:  
Explain social engineering 
Describe the different methods of social enginering. 

1. The aim is to achieve an outcome desirebele to the attacker. 
2. the method is emotional manipulation. 

Signs: 
Plays on targets emotions.  
Urgency. 

### Lesson 3 - Social engineering technique part B
Objectives:   
Same as part A 

Scareware attack - virus-alert, click here to fix.. 
Watering hole - Targeting a site the targets frequents. 

### Lesson 4 - Insider threat 
Objectives:   
Define insider threat 
Explain different insider types 
Describe different threat vectors and methods used by or against insiders 
Describe threat indicators of insider threats and mitigations methods. 

Individuals who work for or have access to org systems. Who pose a physical or cyberthreat. 

Type of insiders:  
Unintential - Negligent 
Malicious. 
 - Espionage
 - Sabotage 
 - IP theft 
 - Fraud 
3 types of malicious 
- Lone wolf 
- Collaborators 
- Mole 
Types of negligent insiders. 
	-Pawns 
		-Manipulated by bad actor. 
	- Goofs
		- Deliberatly takes careless.  (Arrogant, ignorant, incompetent)

Threat indicators against Negligant.  
Det vanlige.. 

Threat indicators against malicious insider 
- attempts to circumvent procedures. 
- dissatified / hold grude against org. 
- employee behaviour changes without explanation. 
- Digital activity: 
	- Activity at unusal times. 
	- Unusual data traffic. 
	- Access data not needed for the job. 
	- Request for system not needed for job function. 
	- using unathorized devices. 
	- emailing sensitive info outside the org. 

Mitigation actions:  

Personal actions to protect org assets 
	-learn org policies. 
	- Alt det vanlige (path, )

Network actions to protect org assets:  
- Detect 
- Analyze 
- Alert 
User and event behaviour analytics.  ML/AI learning tools.. 
Monitor, aggregate and analyze user action tools.  

Define, document disseminate org policies. 
Provice training. 
Promote a culture of security awareness. 



### Lesson 5 - Fraud, Scams, influence campaigns 
Objectives:  
Describe fraud, scams and influence campaings 
List examples of cyber fraud and scams 
Describe how typical online influence campaign unfolds. 

Scams = type of fraud.  Scam more petty, not as serious as fraud. 

Examples. 
Copycat government websites.  
Dating and romance scams. 
Holiday fraud  (no vaancy )
Mandate fraud (duplicates invoice, request payment) 
Pharming - Traffic redirection.  
Greeting card scams.  

Online influence campaing.  
Large scale effort to shift public opinion.  
1. Create fake SoMe accoutn 
2. Create content 
3. post content 
4. real people see and share content 
5. mass media amplifiy content 



## Module 4 - Malware 

### Lesson 1 - Malware Overview 
Malware = Malicious Software.  (Short for). 
used for 
	-Modifying programs
	- Spying on users 
	- Exifltrating data 
	- Denying access to data/devices. 
	- encrypitn important data. 

Objectives: 
Categorize and describe the different types of malware (virus, wormes and ransomware). 
Describe what a attack vector is.  And how it is composed of three different parts. 
Explain how different types of malware and mechanisms exploit a computer. 

### Lesson 2 - Malware Types 
Objectives:  
Define malware 
Describe traits of a computer virus 
Describe the different types of computer virus and malware. 

symptoms of computer malware infections:   
- Degraded perfomance
- pop-ups. 
- app auto launching or shutdown 
- apps not launching 
- Accounts locked 
- computer crashing 
- mass email sent from email account 
- Changes to homepage or browser settings. 

Malware: 
Malicious software that disrupts, damages, or gains unath acccess to systems. 

Virus: 
Type of malicious code written to alter how a computer operates, and is designed to spread itself. 
  Defining traits: 
  - Invoked by user 
  - Attached to application 
  - Designed to spread 

Types of viruses: 
1. Resident virus
	1. Infects apps when they are opened. 
2. Non-Resident virus
	1. Infects executables files when they are not running. 
3. multipartite 
	1. infects many computers, remain in memory. 
4. Direct action 
	1. Access main memory and infecs all apps and files, before deleting itself. 
5. browser hijacker 
	1. changes browser settings. (technically not a virus)
6. overwrite 
	1. delete and replace data in files with their own content and code. Can only be removed by deleting everything it infected. 
7. Web scripting 
	1. Injection of malicious code into the browser. 
8. File infector 
	1. Overwrites files when they are opened.  Often .exe or .com extensions get infected. 
9. Network 
	1. criple networks and spreads to connected devices. 
10. boot sector 
	1. target MBR and injects into HD prtition. 


Other types of malware:  
Worm malware:  
	- Does not require user-action. 
	- Does not need a host system. 
- root kit
	- often masks excisting of other software. 
	- does not self-replicate and spread. 
- DLL Injections. 
- Driver manipulation. 
	- Replaces drivers. 
- Keylogger 
	- Type of spyware. 
- PUP (potenially unwanted program)
	- Spyware 
	- adware 
- spyware 
	- tracks activity. 
	- gather data 
- ad-ware 
	- display ads 
- dialer 
	- tries to use dialing features. 
- adversial AI 
	- malicius input to ML networks. 
- ransomware 
- trojan horse 
- RAT (remote access trojan horse)
- Dropper 
	- trojan horse designed to install malware. 
- Rogueware / Scareware 
- Botnet 
- Cryptojacking 

### Lesson 3 Malware Attack Vectors and Methods 
Objectives: 
Distinguish between attack vector and attack surface 
Describe the three components of and attack vector. 
Describe examples of attack vector malware and its mechanisms. 

What is an attack vector: 
AKA Threat vector. 
A method a bad actor uses to illegallly access or inhibit a networ/system or facility. 
Can be a specific method of attack or a category of attack. 

Social engineering = Category of attack vector. 
Spear-phising = specific attack vector. 

Attack vector consit of three components: 
Vulnreability
Mechaninsm 
Pathway. 


Attack vector = Method of attack. 
Attack surface = total number of entry points that the vector creates to gain unath access to the target. 

Malware Attack vectors:  
two examples:  
- Watering hole attack
	- Vulnrability = User 
	- Pathway = Watering hole 
	- mechanism = malware. 
- botnet 
	- Vulnrability = Server 
	- pathway = internet 
	- mechanism = malware (botnet)

Attack vector mechanisms: 
- Backdoor 
	- undocumented way of gaining access to a system. 
- Logic bomb 
	- Malicious code that execute under specific conditions. 
- easter egg
	- hidden feature that could leave network or data exposed. 
- droppers
	- Programs that extrac files  to a machine. 
- downloader
	- trojan that download additional malware
- shellcode 
	- instrucional code that take control of computer. 
- Code injection. 
	- injects code into an application to change the way it runs. 





# FCF - Getting started in CyberSecurity 2.0 - self paced 

## Lesson 1 - Firewalls 
Objectives: 
Define FW and their evolution 
Describe how FW works 
Explain the latest fw status. 

gen1. Stateless / Packet filters. 
gen2: Statefull fw
gen3: third-gen fw - looks at data payloads. L7.   (UTM-fw)
gen4: NGFW - Rule-based + DPI + Sandbox.
	- Control apps by classifications or users. 
	- Segregate users, devices, and apps. Eliminate single-point of entry. 
	- moved from reactive to proactive.  AI/ML to enforce policies. 
	- High perfomance inspection. 
	- little to no degradation. 
	- greater network visibiltiy. 


## Lesson 2 -  Network access control 
NAC 
.1x. 

Parts: 
Client 
Authenticator (AP, Switch etc)
Authentication server (nac)

NAC builds profile for different types of devices.  
Devices gain access based on device type, and function. 

Issues: 
Single-vendor systems. 

Today: 
complete visibiltiy 
categorize devices. 
effective perfomance 
integrated with SOC


## Lesson 3 - sandbox 
2nd gen fixes lack of communication between devices. 
Gives single-pane of glass. 
AI/ML. 

3rd gen 
standards for threat analysis 
MITRE attack frameworkd. 
common language. 
integration. 
OT 
cloud
fortisandbox. 
Fortinet security fabric. 

## Lesson 4 - WAF 
Web application firewalls. 

Monitors http/https apps.  And block malicious traffic to/from web-app. 
Differs from fw in it targeting content from specific web-apps and att web-level. 

SQL-Injection 
CSS

Evolved from application firewalls. 

1st gen 
Blocklists. 
Signature based http-attributes. 

2nd gen. 
Learn app-behaviour to set baselevel. 
session-monitoring. 
heuristics. 

3rd. gen 
ML
Behaviour analysis at machine speed 
DDos-defense 
IP-reputation 
AV 
DLP 

Monitor HTTP  block non-acceptable behaviour. 
ID user 
Correlate user action with permission. 

Share and collaborate with other security devices. 
Sandboxing. 

Fortiweb = WAF
Fortugard labs = Threat intelligence center. 

## Lesson 8 - Endpoint Hardening technique
objectives: 
List ways to harden endpoint using commong administrative controls 
Describe methods used to secure endpoint software and firmware. 
explain why managing endpoints is critical for maintaining overall cybersec 
Describe  how to harden an endpoint without admin access. 

**Hardening endpoints**
several categoris: 
	1. Administrative controls
		1. Password
		2. user restrictions
		3. Principle of Least Privilage (PoLP)
	2. Local Endpint Protection 
		1. OS and Startup hardening 
		2. Boot management 
		3. Disk security and ecryption 
		4. DLP 
	3. Endpoint maintenance 
		1. Auto-update/ patching 
		2. Policy checks 
		3. backp 
	4. Endpoint monitoring 
		1. Endpoint protection Platform (EPP)
		2. IDS
		3. Endpoint Detection and Response (EDR) - real-time monitoring. Preemptive block av unkown attacks.  

**administrative controls**
PoLP - Only allow permission needed to perfom duties. 
Restricted access.  Not full admin access. 
Restrction. 
	- Secure password 
	- mfa 
	- restricting IP-addresses. 
Multiple layers. 


**Local endpoint Protection**
Firmware and boot process. 
	- ekstra viktig for IoT-devices. 
	- Physically securing devices, don't allow attacked physical access. 
	- Lock down BIOS and Boot time systems. 
	- firmware between IO and endpoint.  
		- BIOS or UEFI 
	- Restrict firmware to only load approved software. UEFI feature. 
Select and use an OS that is easy to manage and secure. 
Only allow known OS and versions to access networks. 

Encryption. 
Full disk encryption (FDE).  OS kryptere disken. 
Key lagra på TPM. 
- SELF-Encrpyting drive (SED)
	- Crypto-effort is shifted to the built-in hdd-module not cpu. 
- DLP
	- Detect copying of sensitive information from a device or send it over network. 
	- block og log the transaction. 
	- prevents or limits use of attachable drives 
	- can be network based. 

Modern devices like phones automatically use Full Disk encryption. 
Always check if FDE and DLP is available. 


**Endpoint Maintenance**
Auto-update/patching. 
	-Difficulty keeping up with number of devices 
	- standardize laptop, os, server, set. 
	- not always possible because IoT and BYOD. 
- Backups. 
- Many IoT devices do not have backup capability. 

## Lesson 9 - endpoint monitoring 
objectives 
Define endpoint monitoring and its role within the different endpoint hardening categories. 
Describe the features of endpoint protection platform (EEP) and Endpoint Detection and Response (EDR) software. 
List different ways admins can secure unknown endpoints. 

**EPP**
Verify software and firmare version. 
scan for virus and malware 
enforce DLP and other security policies. 

defensive meassure 
Helps maintain uniform software updates accross enterprise. 
allow basic monitoring and visibility 

**EDR** 
Constantly scans the device for IOC (indicator of compromise)
	- Suspicious connections, programs, behavior. 
	- ID and stop ransomware and zero-days. 

Uses: 
	- AI/ML and databases. 
	- predics and recognize suspicises files / apps 
	- send alerts to other connected endpoints 
	- has tools to help gather data on new threats. 
	- quarantine systems that are suspected of comproomise. 
	- immediate respons to zero-days and undefined attacks. 

**EPP and EDR**
	-Give admins Top-Down visibility. 
	EDR allow immediate response by automating the process of either locking down devices or execute operations in response to a threat detected by other parts of the networks. 

**Secure unknown devices**
Force unknown devices to isolated network. 
Register device by: 
MAC/Static IP 
Serial number 
hostname 
then install security software. 

Enforce PoLP. 
Isolate on unique network. 
Zero-Trust should be applied. 


## Lesson 10 - SOAR 
Security Orchestration automation and Response 

SOAR connects tools in the security stack toghether into defined workflows. 
which can be run automatically. 

Automating repetetive manual processes. 
Responding to alerts. 
 - Alert fatigue due to many alerts. 
 - Not enough analysts. 
SOAR reduced context switching analysts have to do between tools. 

Processes can be manually or automatically translated into a playbook. 
Playbook = Flowchart-like set of steps that can be repeated on demand. 
This is called orchestration and automation. 

Can querry SIM (Security informatio system)

SOAR can assigns alerts to different analysts at different steps. 

Playbooks (called workflows too)
	-Respond the same way every time. 
	-Playbooks do the repetetive tasks. 
	-Key to automation capability. 
	-Reduced analyst workload, 
	-reduced error rate. 
	



## Lesson 11 - SIEM 
Security and Information Event Management 
Analyze sec-alerts in real-time. 

Collects logs from: 
	-Sec devices
	-Servers 
	-Endpoints 
	-Applications 

Run advanced analytics on the data. 
Potential incidents listed and priorited by: 
- Risk
- Severity 
- Impact 

Simple Cross correlation rules -> 
user behaviour anomalies -> 
Known IoC 
ML-models. 

Prove security models are in place and effective. 
	-Regulatory compliance. 
	- PCI 
	- HIPAA
	- GDPR 

Threat-Detection Capabilities 
Built-in threat intelligence 
Historical and real-time analytics. 
User and entity behavior analytics UEABA
ML 

Difficult to setup and integrate. 
Hard to know what you looked for. 
Not enough people with skills. 
Siloed approach in NOC and SOC 
Multi-vendor and single-point solition. Different OS and patching. 

Integrates NOC and SOC. 
Single-Pane of glass. 
self learning, inventory, discovery. 
baseline of normal behavior. 

##Lesson 12 - SD-WAN 


## SASE 
Network as a service + security as a service. 
connecting it. 

Expanding thin edge 
growing amount of off-site users. 

