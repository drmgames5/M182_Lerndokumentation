# Installation Sysmon

## Manuell

1. Sysmon kann in den [Microsoft Docs](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon) als EXE Datei heruntergeladen werden

<img src="../assets/img/Sysmon/download.png" alt="download" width="50%"/>

2. Nun kann man die Exe einfach ausführen und den Assistenten mit den Standardeinstellungen durchklicken
<img src="../assets/img/Sysmon/install.png" alt="install" width="70%"/>

3. Um zu checken ob es installiert ist, kann man im Verwaltungstool "Dienste" den Dienst **Sysmon64** suchen. Falls er vorhanden ist, ist es richtig installiert
<img src="../assets/img/Sysmon/check.png" alt="check" width="70%"/>

## Automatisiert

Da unsere VMs mit Vagrant erstellt werden, kann man die Installation von Sysmon auch Vagrant überlassen. Dafür ist im PS-Script **"install-sysinternals.ps1"** die benötigte Exe Datei zur installation angegeben. Das Script wird vom Vagrantfile aus beim Erstellen der VM aufgerufen.
<img src="../assets/img/Sysmon/autoinstall.png" alt="autoinstall" width="70%"/>
