# Setup

## Vagrantfie

Vagrant ist eine Software mit der man VMs generieren kann. Dabei schreibt man sozusagen eine Bauanleitung für die VMs und Vagrant erstellt diese nach den Angaben. Das Vagrantfile ist diese Bauanleitung. Darin definiert man z.b Gerätename, Arbeitsspeicher, CPUs, IP-Adresse usw. Man definiert auch z.B für welche "Engine" es erstellt werden soll, z.B VBox oder VMWare

Ausschnitt aus Vagrantfile: 

```vagrantfile
config.vm.define "win11" do |cfg|
     cfg.vm.box = "StefanScherer/windows_11"
     cfg.vm.hostname = "win11"
     cfg.vm.boot_timeout = 1200
     cfg.vm.communicator = "winrm"
     cfg.winrm.basic_auth_only = true
     cfg.winrm.timeout = 1200
     cfg.winrm.retry_limit = 20
     cfg.vm.network :private_network, ip: "192.168.60.104", gateway: "192.168.60.1", dns: "192.168.60.102"
```

## Provisioning Befehle

Man kann auch Software hinzufügen oder spezielle Einstellungen vornehmen in dem man scripts mit den gewünschten Parametern hinzufügt. Diese werden dann beim Setup der VM auf selbiger ausgeführt. Um das zu machen ruft man die gewünschten Scripts im vagrantfile mit Provisioning-Befehlen auf.

Ein paar Beispiele aus einem Vagrantfile:

```vagrantfile
cfg.vm.provision "shell", path: "scripts/fix-second-network.ps1", privileged: true, args: "-ip 192.168.60.104 -dns 8.8.8.8 -gateway 192.168.60.1" 
cfg.vm.provision "shell", path: "scripts/provision.ps1", privileged: false
cfg.vm.provision "reload"
cfg.vm.provision "shell", path: "scripts/provision.ps1", privileged: false
cfg.vm.provision "shell", path: "scripts/download_palantir_wef.ps1", privileged: false
cfg.vm.provision "shell", inline: 'wevtutil el | Select-String -notmatch "Microsoft-Windows-LiveId" | Foreach-Object {wevtutil cl "$_"}', privileged: false
cfg.vm.provision "shell", path: "scripts/install-utilities.ps1", privileged: false
cfg.vm.provision "shell", path: "scripts/install-redteam.ps1", privileged: false
cfg.vm.provision "shell", path: "scripts/install-choco-extras.ps1", privileged: false
cfg.vm.provision "shell", path: "scripts/install-osquery.ps1", privileged: false
cfg.vm.provision "shell", path: "scripts/install-sysinternals.ps1", privileged: false
cfg.vm.provision "shell", path: "scripts/install-velociraptor.ps1", privileged: false
cfg.vm.provision "shell", path: "scripts/install-autorunstowineventlog.ps1", privileged: false
cfg.vm.provision "enable-public-winrm", type: "shell", path: "scripts/enable-winrm.ps1", privileged: false
cfg.vm.provision "shell", inline: 'cscript c:\windows\system32\slmgr.vbs /dlv', privileged: false
cfg.vm.provision "shell", inline: 'cscript c:\windows\system32\slmgr.vbs /rearm', privileged: false
cfg.vm.provision "reload"
```

## Installations-Scripts

Im folgenden eine Liste aller PS-Scripts die für die Windows VMs verwendet wurden:

* fix-second-network.ps1
* provision.ps1
* download_palantir_wef.ps1
* install-utilities.ps1
* install-redteam.ps1
* install-choco-extras.ps1
* install-osquery.ps1
* install-sysinternals.ps1
* install-velociraptor.ps1
* configure-ou.ps1
* configure-wef-gpo.ps1
* configure-powershelllogging.ps1
* configure-AuditingPolicyGPOs.ps1
* configure-rdp-user-gpo.ps1
* configure-disable-windows-defender-gpo.ps1
* install-autorunstowineventlog.ps1
* enable-winrm.ps1

## Bootstrap.sh

Die Bootstrap.sh Datei wird benötigt um damit Linux VMs vorkonfigurieren zu können. Da Linux eine andere Shell (Bash) verwendet, braucht es dafür ein eigenes Script. In dieser Datei gibt man Software an die in der Linux VM installiert werden soll mitsamt parameter usw an und konfiguriert per Bash z.B auch Netzwerkadapter usw. Im grunde ist es nur ein Bash Script das die installationen auf den Linux VMs macht.

Die Bootstrap.sh Datei muss im Vagrantfile für die Linux VM angegeben werden.

## ELK.sh 

Diese Datei dient dem Zweck spezielle Software zu installieren. Und zwar wird hiermit Elasticsearch zusammen mit Kibana installiert. JDK wird als abhängigkeit mitinstalliert.

Elasticsearch ist ein Indexingtool für Daten. Damit kann man Daten wie z.B Logs schnell indexieren, filtern usw. Es wird zur Analyse und Aufbereitung von Daten verwendet. Man kann damit Querys erstellen um bestimmte Daten rauszufiltern.

Kibana wiederum ist sozusagen das Frontend dafür. In Kibana können Elasticsearch Querys erstellt werden und die Ergebnisse können in Kibana dargestellt werden.

Beides sind OpenSource Freewares. Sie stehen allen gratis zur Verfügung.