# Recherche WSUS

## Verwendungszweck

WSUS steht für **Windows Server Update Services** und ist seit Windows Server 2016 ein eingebautes Feature von Windows Servern. Mithilfe dieses Dienstes kann man Updates von Windows Geräten, wie Servern oder Computern, ausrollen. Dabei kann man kontrollieren welche Updates geladen werden dürfen und welche nicht.

Wenn ein neues Update rauskommt, ist es vernünftig eine Weile zu warten bevor man es installiert. Sollten damit Probleme auftreten, kann man das Update auf dem WSUS Server blockieren. 

**Fazit:** WSUS vereinfacht das Updaten von mehreren Geräten und dient als Kontrollstelle um Updates zu verhindern oder zuzulassen. 

## Alternativen

Es gibt einige andere Update Dienste. Darunter:

* Aagon ACMP CAWUM
* Solar Winds Patch Manager
* ManageEngine Patch Connect Plus
* Kaseya VSA
* PDQ Deploy
* Ivanti PatchLink
* BatchPatch

## PowerShell Cmdlets

**Get-WsusServer:**
Baut eine Verbindung zu einem WSUS Server auf. Man muss den Namen des Servers und den Port des WSUS dienstes angeben.

```PowerShell
$WSUS = Get-WsusServer -Name ws2016-wsus -PortNumber 8530
```

### Infos von WSUS

```PowerShell
$WSUS.GetConfiguration()
# Gibt die konfiguration des WSUS Servers zurück

$WSUS.GetDatabaseConfiguration()
# Gibt die konfiguration der WSUS Datenbank zurück

$WSUS.GetSubscription()
# Gibt den Synchronisierungszeitplan des WSUS Servers zurück
```

https://www.windowspro.de/wolfgang-sommergut/wsus-powershell-verwalten-computer-updates-genehmigungen
