# Beschreibung des Lab

## Netzwerkdiagram

```plantuml
@startuml
!define osaPuml https://raw.githubusercontent.com/Crashedmind/PlantUML-opensecurityarchitecture2-icons/master
!include osaPuml/Common.puml
!include osaPuml/User/all.puml
!include osaPuml/Hardware/all.puml
!include osaPuml/Misc/all.puml
!include osaPuml/Server/all.puml
!include osaPuml/Site/all.puml

together {
osa_cloud(cloud, "Internet", "Network")
osa_laptop(laptop, "DHCP", "HostNB")
}

together {
osa_device_wireless_router(NAT, "10.0.2.0/24", "NAT-Netzwerk on VBox")

osa_desktop(pc, "10.0.2.16", "Windows 11", "Client-VM")
osa_server(server_L, "10.0.2.14", "Linux Server ELK", "Server-VM")
osa_server(server_W, "10.0.2.15", "Windows Server 2019", "Server-VM")
}

cloud --> laptop
laptop --> NAT
NAT --> pc
NAT --> server_W
NAT --> server_L

@enduml
```

## VMs

Uns stehen zwei Windows und eine Linux VMs zur Verfügung. Die eine ist ein Windows 2016 Server und die andere, ein Windows 11 Client.

### Windows 11 Client

> #### IP-Adresse:
> 10.0.2.16
> #### username:
> vagrant
> #### password:
> vagrant

#### Software:
Bei Windows 11 kann man sich im Verwaltungsprogramm "Dienste" alle installierten Dienste und Programme anzeigen lassen.
<img src="../assets/img/infrastructure/dienste.png" alt="Dienste" width="70%"/>

#### Zugriff:

Auf dem Windows Client ist keine Software installiert für die spezielle Berechtigungen von nöten sind. Der Zugriff erfolgt also einfach über den Standardbenutzer Vagrant.

### Domain Controller (Win 2016 Server)

> #### IP-Adresse:
> 10.0.2.15
> #### username:
> vagrant
> #### password:
> vagrant

#### Software:
Auch auf dem Windows Server gibt es das Verwaltungstool "Dienste" auf dem einem alle dienste und SW angezeigt wird. 

#### Zugriff:
Da alle VMs mit Vagrant generiert wurden, kann mann die Zugangsdaten für die verschiedenen Applikationen im Vagrantfile nachschlagen und bearbeiten/vordefinieren. Wir gehen später genauer auf das Vagrantfile ein. Allerdings ist auch beim Windows Server keine Software mit speziellem Zugriff vorinstalliert.

## ELK VM

> #### IP-Adresse:
> 10.0.2.14
> #### username:
> vagrant
> #### password:
> vagrant

#### Software:
Auf der Linux VM sind sicher mal Kibana, Elasticsearch und JDK installiert, diese werden im Vagrantfile zur installation angegeben. Weitere Software kann man sich mit folgendem Befehl anzeigen lassen:

systemctl list-units --type=service --all

<img src="../assets/img/infrastructure/systemctl.png" alt="Dienste" width="70%"/>

#### Zugriff:

Der Zugriff auf Kibana und Elasticsearch ist in der ELK.sh Datei festgelegt und kann dort auch bearbeitet werden. Auf Kibana kann man über **192.168.60.105:5601** zugreifen und auf Elasticsearch über **192.168.60.105:9200**. Wobei bei Kibana User und Password wie unten angegeben benötigt werden.

Ausschnitte aus ELK.sh:

```bash
setup.kibana:
  host: "192.168.60.105:5601"
  username: vagrant
  password: vagrant

setup.dashboards.enabled: true
setup.ilm.enabled: false

output.elasticsearch:
  hosts: ["192.168.60.105:9200"]
EOF
```

```bash
cat >/etc/elasticsearch/elasticsearch.yml <<EOF
...
xpack.security.enabled: true
xpack.security.authc:
        api_key.enabled: true
        anonymous:
                username: anonymous
                roles: superuser
                authz_exception: false
EOF
```