# Projekt Állapotjelentés - 2025-03-02

## Összefoglaló
A "HA Telefonközpont" projekt gyakorlati szakasza folytatódott 2025. március 2-án. A cél egy magas rendelkezésre állású (HA) telefonközpont kiépítése klaszterezett környezetben, amely biztonságos távoli hozzáférést és globális VPN-kapcsolatokat biztosít. A mai nap két fő területre fókuszált: a SIP regisztráció hibaelhárítására a VoIP komponensen (félretettük), valamint a Pacemaker konfiguráció előkészítésére és a projekt dokumentálására.

## Elvégzett Feladatok
1. **SIP regisztráció hibaelhárítás (VoIP komponens):**
   - **Cél:** A ha-node2 (10.0.0.101) linphonec klienssel való regisztrálása a ha-node1 (10.0.0.100) Asterisk szerverére.
   - **Lépések:**
     - linphonec -d 6 és egister sip:testuser1@10.0.0.100:5060 sip:10.0.0.100:5060 testpass1: Regisztrációs kísérletek.
     - 	cpdump -i any port 5060 -n -v: Forgalom figyelése a ha-node2-n. **Eredmény:** 0 csomag a 5060-as porton.
     - status register: Regisztrációs állapot ellenőrzése. **Eredmény:** egistered=-1.
     - Proxy beállítás: proxy add (sip:10.0.0.100:5060, sip:testuser1@10.0.0.100:5060), de nem aktiválva (proxy use 0 hiányzott).
     - cat /root/.linphonerc: Konfigurációs fájl ellenőrzése – proxy beállítás nem mentődött.
     - sterisk -rvvvvvv és sip set debug on a ha-node1-en: Nem érkezett REGISTER kérés.
   - **Eredmény:** A linphonec nem küld REGISTER kérést, valószínűleg szoftveres vagy konfigurációs hiba miatt. Ezt az irányt félretettük.

2. **Pacemaker előkészítése (klaszter komponens):**
   - A Pacemaker alapvető erőforrásainak tervezése megkezdődött a klaszterezett környezetben.
   - A klaszter aktuális állapotának ellenőrzése a crm_mon -1 paranccsal, hogy biztosítsuk a Corosync és Pacemaker együttes működését.
   - **Eredmény:** A klaszter stabilan fut, a node-ok (ha-node1, ha-node2) online állapotban vannak.

3. **Dokumentáció:**
   - A GitHub repository frissítése a mai előrehaladással: a README.md aktualizálása és a napi jelentés előkészítése.
   - A projekt történetének pontos vezetése a változtatások nyomon követéséhez.

4. **Ellenőrzés (klaszter):**
   - A rendszer stabilitásának tesztelése a Corosync és Pacemaker együttes működésével.
   - **Eredmény:** A klaszter alapvető működése megfelelő, de a teljes erőforrás-konfiguráció még hátravan.

## Tervezett Lépések
- **Pacemaker konfiguráció befejezése:** A klaszter erőforrások (pl. MySQL replikáció, virtuális IP) teljes definiálása és tesztelése a következő napokban.
- **MySQL replikáció integrálása:** A MySQL slave beállítása a ha-node1-en Pacemaker alá helyezve, systemd szolgáltatásként, a replikáció stabilitásának ellenőrzése.
- **Proxmox mentés:** A Proxmox jelenlegi állapotának elmentése a storage boxba (pl. ackup_2.tar.gz).
- **SIP regisztráció folytatása (ha szükséges):** Alternatív SIP kliens (pl. sipsak) tesztelése vagy a linphonec hibájának további elemzése.

## Megjegyzések
- A SIP regisztráció hibaelhárítása nem zárult le, a linphonec problémája miatt ezt az irányt átmenetileg felfüggesztettük.
- A Pacemaker konfiguráció előkészítése sikeresen megkezdődött, a dokumentáció naprakész, és a klaszter stabilitása ígéretes.
- A holnapra tervezett feladatok (MySQL replikáció, Pacemaker alá helyezés, Proxmox backup) előkészítése folyamatban van.

**Készítette:** SysCoreX  
**Dátum:** 2025-03-02
