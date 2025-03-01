# HA Telefonközpont Globális Híddal

## Projekt Célok
- Magas rendelkezésre állású (HA) telefonközpont kiépítése virtualizált környezetben RAID1 redundanciával.
- Globális hálózati összeköttetés biztosítása VPN-ekkel (OpenVPN/IPsec) és SIP-alapú konferenciahívások támogatása.
- Automatizált szervermenedzsment (MySQL, Nginx) konfigurációkezelő eszközzel, titkosított adattárolással.

## Eddigi Előrehaladás (2025.03.01.)
- Virtualizációs hoszt stabil, 5 virtuális gépet futtat.
- Hálózati tűzfal és VPN szerver konfigurálva, belső LAN hálózat működik.
- Első HA csomópont (ha-node1) hálózati beállításokkal és távoli hozzáféréssel ellátva.
- Klaszterezési előkészületek folyamatban.

## Használt Technológiák
- Virtualizációs platform: Proxmox VE
- Tűzfal/VPN: pfSense
- Klaszterezés: Pacemaker, Corosync
- Hálózati eszközök: OpenVPN, SSH