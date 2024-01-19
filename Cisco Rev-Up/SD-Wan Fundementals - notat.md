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


## SD-Wan network deployment
Course mål: 
- Describe secure control plane operations
- Deploy a WAN Edge device and verify control plane operation
- Describe secure data plane operations
- Identify the various services provided by cloud deployments
- List the high-availability redundancy options

### Secure control plane Operations

vBond - Orchestrator (Autentisering av alle komponenter)
vSmart - Controller (Control plane)
vManage - Management plane

#### Fabric bring up - ZT-Model
vBond gjer automatisk autentisering av alle WAN-Edge routers.  SD-WAN devices autentiserer seg sjølv automatisk når
dei blir med i overlay nettverket. 

vBond og vSmart trenger manuell installasjon av autentiserings-filer, som lastast ned frå vManage. 
vEdge Cloud og 8000v cloud router må generere ein CSR og installere det signerte sertifikatet og legge serienummeret i sertifikatet inn i vManage. 

Wan-Edge HW routers bruker ZTP / Cisco PnP.  

Alle devices bruker vBond for autentisering og å sette opp kryptert kanal mellom kvarandre.  Bruker kanalen til å validere og autentisere kvarandre for å få eit full-mesh overlay network. 
Devices laster ned config frå vManage. 

![bilde1](/Pasted image 20231228161326.png)


Automatisk validering og autentisering krever att vBond og vSmart kjenner til serienummer og chassis-number for devices som skal delta i nettverket. 
Serial-number file må lastast opp til vManage manuelt.  

Alle devices må også vere konfigurert med same organization name.  Org-Name settast på vManage (case-sensitiv). 
Org-name er  inkludert i config-fila til alle devices og i cert for alle devices.  Cert er laga enten av Cisco eller ein Org-CA. 

#### Secure Control Channel - Control Elements

![[Pasted image 20231228164713.png]]

vBond <-> vSmart session blir initiert av vSmart over DTLS.  Begge devices genererer ein RSA key pair ved boot som blir brukt for DTLS-kryptering. 

DTLS-tunell blir brukt for å autentisere kvarandre. 

Etter bidirectional authentication er ferdig blir DTLS-connection endra frå ein temp-connection til permanent connection. 

vBond har ein permanent DTLS-connection til kvar vSmart controller i topologien.  Desse tunellane er ein del av Control Plane,  ingen Data-Trafikk over dei. 
Når alle vSmart har registrert seg mot vBond er dei klar for å validere / Autentisere WAN-Edge routera. 

#### vSmart <-> vBond authentication 

Two-Way auth.  Skjer i paralell  
Permanent DTLS-tunell dersom two-way auth er suksessfull. 
Dersom eine devicen registrerer auth-failure, noden som registrerer feilen vil rive ned tilkoblinga. 

IP eller DNS-name for vBond blir lagt inn på vSmart manuelt ved provisjonering av vSmart node. 
![[Pasted image 20231228165423.png]]

##### vSmart autentiserer vBond 
	1.vBond sender cert signert av root CA til vSmart. 
	2. vBond sender fil med autoriserte wan-edge serienummer til vSmart
	3. vSmart henter org-name frå tilsendt Cert, og samenlikne med konfigurert org-name. 
	4. vSmart verifiserer att cert er signert av korrekt root-ca. 

##### vBond autentiserer vSmart 
	1.vSmart sender signert cert til vBond. 
	2. vBond henter serienummer frå cert. Matcher det mot authorized serialnumber file. 
	3. vBond henter org-name frå Cert og matcher mot konfigurert org-name. 
	4. vBond verifisert att cert er signert av korrekt root-CA. 

#### vSmart <-> vSmart authentication. 
![[Pasted image 20231228171919.png]]

Miljø med fleire vSmart-controllera må autentisere kvarandre for å etablere full-mesh DTLS-tuneller.  Trengs for å synce OMP-ruter. 
vSmart lærer ip-adressa til andre vSmart-noder frå vBond. 

	1.vSmart1 sender signed cert til vSmart2. 
	2.vSmart2 henter serienummer frå cert, matcher mot authorized serial-number file. 
	3. vSmart2 henter org-name frå cert og matcher mot konfigurert org-name. 
	4. vSmart2 verifiserer att cert er signert av korrekt root-ca. 
	5. vSmart2 har autentisert vSmart1. One-Way DTLS-connection oppe. 
	6. vSmart1 autentiserer vSmart2 gjennom same stega. 

![[Pasted image 20231228172809.png]]


#### Establish WAN-Edge router Identity 

![[Pasted image 20231228172821.png]]

XE-Wan Edge - Fysiske Cisco bokser. 
Viptela vEdge - Physical Viptela (vEdge2000 / 5000)
Virtual Wan Edge - ASR1002-X, ISRv, CSR1000v, Cat8000v, vEdge Cloud. 

 **XE-WAN Edge**: 
Unik ID er Chassis-ID og Sertifikat Serienummer (SUDI-Cert).  Cert er lagra på ein trusted chip under produksjon (ACT2-chip). 
Cert helde public-key,  private-key er "embedded" i ACT2-chip.  Cisco root CA har signert cert. 
ACT2 er tamper-proof.  Private Key kan ikkje hentast ut frå ACT2-chip.  Ved brute-force vil chippen feile og all tilgang til ruteren er disabled. 
![[Pasted image 20231230150508.png]]


**Viptela vEdge (physical router)** 
Chassis-ID og Cert-serial gir unik ID. 
Cert lagra i TPM chip. Installert under produksjon. 
Cert signert av AVNET root CA. 
Control-Plane devices truster AVNET. 
vEdge har Cisco Root CA installert og truster Cisco chain. For å validere Control-Plane Devices (vbond/vSmart/vManage).  Kan erstattast med enterprise CA. 
![[Pasted image 20231230151231.png]]

**Virtual WAN Edge**
Får eit signert cert frå vManage. 
vManage generere ein OTP/Token for kvar device lista i opplasta WAN-Edge List file. 
OTP/Token blir gitt til Virtual WAN-Edge under VM-deployment eller via CLI. 
Når WAN-Edge blir aktivert vil vManage signere sertifikatet og installere det i routeren. 
Cisco/Symantec root CA validerer control-plane devices.  Kan erstattast med Enterprise CA. 

#### WAN-Edge <-> vBond authentication. 

#### Control Connection ports
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

#### DDoS protection 
![[Pasted image 20231230162809.png]]


#### Summary 
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


### Secure Device Onboarding 

- Explain ZTP prosess
- Configure WAN-Edge from CLI 
- Register WAN-Edge in vManage. 
- Verify controll connections and certs. 

#### ZTP 
![[Pasted image 20231230163311.png]]

	3.Resolve ztp.viptela.com.  Får IP-adresse til Cisco ZTP-Server. 
	4. Connect to ZTP-Server som verifiserer WAN-Edge. Får IP til vBond. 
	5. Kobler til vBond som verifiserer WAN-Edge. Får IP til vManage. 
	6. Kobler vManage som verifiserer wan-edge. Får tildelt og sendt system IP-addr. 
	7. Reestablish vBond connection med system-IP. 
	8. Reestablish vSmart connection med system-ip. Får tilsendt korrekt software-image. 
	9. reboot og reestablish vbond connection. 
	10. vManage connection, download full config. 
	11. Joins overlay. 


> [!NOTE] Note
> ZTP feiler dersom vManage ikkje har en device config template for WAN-Edge. 


#### Configure WAN-Edge routers

![[Pasted image 20231230170908.png]]


