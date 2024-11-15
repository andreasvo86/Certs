---
tags:
  - notat
---
- [SD-Wan network deployment](#SD-Wan%20network%20deployment)
	- [Secure control plane Operations](#Secure%20control%20plane%20Operations)
		- [Fabric bring up - ZT-Model](#Fabric%20bring%20up%20-%20ZT-Model)
		- [Secure Control Channel - Control Elements](#Secure%20Control%20Channel%20-%20Control%20Elements)
		- [vSmart <-> vBond authentication](#vSmart%20%3C-%3E%20vBond%20authentication)
			- [vSmart autentiserer vBond](#vSmart%20autentiserer%20vBond)
			- [vBond autentiserer vSmart](#vBond%20autentiserer%20vSmart)
		- [vSmart <-> vSmart authentication.](#vSmart%20%3C-%3E%20vSmart%20authentication.)
		- [Establish WAN-Edge router Identity](#Establish%20WAN-Edge%20router%20Identity)
		- [WAN-Edge <-> vBond authentication.](#WAN-Edge%20%3C-%3E%20vBond%20authentication.)


# SD-Wan network deployment
Course mål: 
- Describe secure control plane operations
- Deploy a WAN Edge device and verify control plane operation
- Describe secure data plane operations
- Identify the various services provided by cloud deployments
- List the high-availability redundancy options

## Secure control plane Operations

vBond - Orchestrator (Autentisering av alle komponenter)
vSmart - Controller (Control plane)
vManage - Management plane

### Fabric bring up - ZT-Model
vBond gjer automatisk autentisering av alle WAN-Edge routers.  SD-WAN devices autentiserer seg sjølv automatisk når
dei blir med i overlay nettverket. 

vBond og vSmart trenger manuell installasjon av autentiserings-filer, som lastast ned frå vManage. 
vEdge Cloud og 8000v cloud router må generere ein CSR og installere det signerte sertifikatet og legge serienummeret i sertifikatet inn i vManage. 

Wan-Edge HW routers bruker ZTP / Cisco PnP.  

Alle devices bruker vBond for autentisering og å sette opp kryptert kanal mellom kvarandre.  Bruker kanalen til å validere og autentisere kvarandre for å få eit full-mesh overlay network. 
Devices laster ned config frå vManage. 

![bilde1](/cisco-rev-up/img/bilde1.png)


Automatisk validering og autentisering krever att vBond og vSmart kjenner til serienummer og chassis-number for devices som skal delta i nettverket. 
Serial-number file må lastast opp til vManage manuelt.  

Alle devices må også vere konfigurert med same organization name.  Org-Name settast på vManage (case-sensitiv). 
Org-name er  inkludert i config-fila til alle devices og i cert for alle devices.  Cert er laga enten av Cisco eller ein Org-CA. 

### Secure Control Channel - Control Elements

![](/cisco-rev-up/img/bilde2.png)

vBond <-> vSmart session blir initiert av vSmart over DTLS.  Begge devices genererer ein RSA key pair ved boot som blir brukt for DTLS-kryptering. 

DTLS-tunell blir brukt for å autentisere kvarandre. 

Etter bidirectional authentication er ferdig blir DTLS-connection endra frå ein temp-connection til permanent connection. 

vBond har ein permanent DTLS-connection til kvar vSmart controller i topologien.  Desse tunellane er ein del av Control Plane,  ingen Data-Trafikk over dei. 
Når alle vSmart har registrert seg mot vBond er dei klar for å validere / Autentisere WAN-Edge routera. 

### vSmart <-> vBond authentication 

Two-Way auth.  Skjer i paralell  
Permanent DTLS-tunell dersom two-way auth er suksessfull. 
Dersom eine devicen registrerer auth-failure, noden som registrerer feilen vil rive ned tilkoblinga. 

IP eller DNS-name for vBond blir lagt inn på vSmart manuelt ved provisjonering av vSmart node. 
![](/cisco-rev-up/img/bilde3.png)

#### vSmart autentiserer vBond 
	1.vBond sender cert signert av root CA til vSmart. 
	2. vBond sender fil med autoriserte wan-edge serienummer til vSmart
	3. vSmart henter org-name frå tilsendt Cert, og samenlikne med konfigurert org-name. 
	4. vSmart verifiserer att cert er signert av korrekt root-ca. 

#### vBond autentiserer vSmart 
	1.vSmart sender signert cert til vBond. 
	2. vBond henter serienummer frå cert. Matcher det mot authorized serialnumber file. 
	3. vBond henter org-name frå Cert og matcher mot konfigurert org-name. 
	4. vBond verifisert att cert er signert av korrekt root-CA. 

### vSmart <-> vSmart authentication. 
![](/cisco-rev-up/img/bilde4.png)

Miljø med fleire vSmart-controllera må autentisere kvarandre for å etablere full-mesh DTLS-tuneller.  Trengs for å synce OMP-ruter. 
vSmart lærer ip-adressa til andre vSmart-noder frå vBond. 

	1.vSmart1 sender signed cert til vSmart2. 
	2.vSmart2 henter serienummer frå cert, matcher mot authorized serial-number file. 
	3. vSmart2 henter org-name frå cert og matcher mot konfigurert org-name. 
	4. vSmart2 verifiserer att cert er signert av korrekt root-ca. 
	5. vSmart2 har autentisert vSmart1. One-Way DTLS-connection oppe. 
	6. vSmart1 autentiserer vSmart2 gjennom same stega. 

![](/cisco-rev-up/img/bilde5.png)


### Establish WAN-Edge router Identity 

![](/cisco-rev-up/img/bilde6.png)

XE-Wan Edge - Fysiske Cisco bokser. 
Viptela vEdge - Physical Viptela (vEdge2000 / 5000)
Virtual Wan Edge - ASR1002-X, ISRv, CSR1000v, Cat8000v, vEdge Cloud. 

 **XE-WAN Edge**: 
Unik ID er Chassis-ID og Sertifikat Serienummer (SUDI-Cert).  Cert er lagra på ein trusted chip under produksjon (ACT2-chip). 
Cert helde public-key,  private-key er "embedded" i ACT2-chip.  Cisco root CA har signert cert. 
ACT2 er tamper-proof.  Private Key kan ikkje hentast ut frå ACT2-chip.  Ved brute-force vil chippen feile og all tilgang til ruteren er disabled. 
![](/cisco-rev-up/img/bilde8.png)


**Viptela vEdge (physical router)** 
Chassis-ID og Cert-serial gir unik ID. 
Cert lagra i TPM chip. Installert under produksjon. 
Cert signert av AVNET root CA. 
Control-Plane devices truster AVNET. 
vEdge har Cisco Root CA installert og truster Cisco chain. For å validere Control-Plane Devices (vbond/vSmart/vManage).  Kan erstattast med enterprise CA. 
![](/cisco-rev-up/img/bilde9.png)

**Virtual WAN Edge**
Får eit signert cert frå vManage. 
vManage generere ein OTP/Token for kvar device lista i opplasta WAN-Edge List file. 
OTP/Token blir gitt til Virtual WAN-Edge under VM-deployment eller via CLI. 
Når WAN-Edge blir aktivert vil vManage signere sertifikatet og installere det i routeren. 
Cisco/Symantec root CA validerer control-plane devices.  Kan erstattast med Enterprise CA. 

### WAN-Edge <-> vBond authentication. 

### Control Connection ports
Base port: 12346 
Port-Offset: 0 
Port-Hopping: 
12346
12366
12386
12406
12426 - return to 12346. 

WAN-Edge bruker port-hopping mot vManage, vBond, vSmart.  Kan også manuelt starte port-hopping.   
vSmart og vManage trenger generelt ikkje port-hopping. Difor mostly not used. 
vBond port-hopper ALDRI.  Alltid 12346. 

### DDoS protection 
![](/cisco-rev-up/img/bilde10.png)


### Summary 
- ZTE tillater kun autentiserte og autoriserte devices å bli med i SD-WAN overlay nettverk.   
- Controllers gjer multual authentication.  
- vSmart controller gjer authentication på alle WAN-Edges før dei får sende data over nettverket.  
- DTLS controll channels mellom controllera.  DTLS-Channels er ein del av control-plane.  
- Auth mellom controllers skjer med signed Certs + andre konfigurerte parameterra.  Inkludert org-name. 
- WAN-Edges må først etablere sikker connection med vManage og vSmart.  Dei blir automatisk oppdage av WAN-Edge ved hjelp av vBond. 
- Initiell config av WAN-Edge inneheld IP-addr/FQDN på vBond. 
- DDoS protection ligger i overlay ved å bruke: 
	- Authenticated sources(vBond, vManage,vSmart, wan-edge) 
	- implisert trusted sources (WAN-Edge) 
	- Eksplisitt definerte sources. (Cloud-sec)


------------------------------------


## Secure Device Onboarding 

- Explain ZTP prosess
- Configure WAN-Edge from CLI 
- Register WAN-Edge in vManage. 
- Verify controll connections and certs. 

### ZTP 
![](/cisco-rev-up/img/bilde11.png)

	3.Resolve ztp.viptela.com.  Får IP-adresse til Cisco ZTP-Server. 
	4. Connect to ZTP-Server som verifiserer WAN-Edge. Får IP til vBond. 
	5. Kobler til vBond som verifiserer WAN-Edge. Får IP til vManage. 
	6. Kobler vManage som verifiserer wan-edge. Får tildelt og sendt system IP-addr. 
	7. Reestablish vBond connection med system-IP. 
	8. Reestablish vSmart connection med system-ip. Får tilsendt korrekt software-image. 
	9. reboot og reestablish vbond connection. 
	10. vManage connection, download full config. 
	11. Joins overlay. 


> [!NOTE]
> ZTP feiler dersom vManage ikkje har en device config template for WAN-Edge. 


### Configure WAN-Edge routers

![](/cisco-rev-up/img/bilde12.png)


#### Avtivating a Virtual WAN Edge 

Følgande må settast opp manuelt på WAN Edge først: 
- System IP
- Site ID
- Organization Name
- vBond IP Address
- Hostname
++ Network connectivity til Transport network.  (Wan-interface og tilknytt tunell-interface)

```
# Minimal config for C8000v
Catalyst8000v# **config-transaction**
Catalyst8000v(config)# **hostname Branch1**
Catalyst8000v(config)# **system**
Catalyst8000v(config-system)# **system-ip 172.27.0.12**
Catalyst8000v(config-system)# **site-id 20**
Catalyst8000v(config-system)# **organization-name "Cisco-LearningAtCisco - 20998"**
Catalyst8000v(config-system)# **vbond 10.2.6.2**
Catalyst8000v(config-system)# **commit**

Branch1(config)# **interface GigabitEthernet 1**
Branch1(config-int)# **ip address 10.2.8.2/24**
Branch1(config-int)# **no shutdown**
Branch1(config-int)# **exit**
Branch1(config)# **interface Tunnel1**
Branch1(config-int)# **ip unnumbered GigabitEthernet 1**
Branch1(config-int)# **tunnel source GigabitEthernet 1**
Branch1(config-int)# **tunnel mode sdwan**
Branch1(config-int)# **no shut**
Branch1(config-int)# **exit**
Branch1(config)# **sdwan**
Branch1(config-sdwan)# **interface GigabitEthernet 1**
Branch1(config-interface-GigabitEthernet1)# **tunnel-interface allow-service all**
Branch1(config-tunnel-interface)# **encapsulation ipsec**
Branch1(config-tunnel-interface)# **color mpls**
Branch1(config-tunnel-interface)# **exit**
Branch1(config)# **ip route 0.0.0.0 0.0.0.0 10.2.8.1**
Branch1(config)# **commit**
```

Cisco vManage uses the system IP address to identify the device so that you can download the full configuration to the device.

**Note on colour**
```
Branch1(config-tunnel-interface)# **color mpls**
#Configure a color for the tunnel to identify the type of WAN transport.
#You can use the default color (**default**) but you can also # **mpls** or **metro-ethernet**, depending on the actual WAN transport.'

# here are two types of colors: private and public. Private colors are mpls, #metro-ethernet, private1 through private6. Public colors include biz-internet, #public-internet, gold, lte, 3g.


```

Activate the Virtual WAN Edge Router using chassis number and one-time password/Token 
```
Catalyst8000v# Request platform software sdwan vedge_cloud activate chassis-number *chassis-number* token *token*
```

Cisco vManage authenticates the Virtual WAN Edge router and install the signed certs on the router.  Sjå virtual wan edge lenge oppe. 

```
show sdwan control local-properties 
# certificate-status - Installed  # Bør vere statusen på denne linja. 

token: invalid = Er ein OK status så lenge certificate-status = installed. 
Token kun bruke ved aktivering. 
```

```
show sdwan control connections
= Control connection on WAN Edge Router 

show control connections
= Control connections on vSmart. 
```

```
show sdwan certificate installed 
# Viser dekoded CSR på vBond, vManage eller vSmart. 
# Dette er CRS som er signert av root CA. 

show sdwan certificate root-ca-cert
# Display root cert installed on SD-WAN Device. 

Show sdwan certificate serial 
# Display serial number for a vBond or vSmart. 
# Display serial number and chassis number for WAN Edge router

Show sdwan certificate signing-reqquest 
# Display CSR installed on vSmart or vBond. Dette er CSR som er signert av devicens private key. 

show sdwan certificate validity 
# display kor lenge cert er valid. Kun på vSmart og vBond. 

```


## Secure data plane operations

![](/cisco-rev-up/img/bilde13.png)