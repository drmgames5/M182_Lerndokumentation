# Konfiguration Sysmon

## Config-File
Sysmon hat eine Zentrale XML-Konfigurationsdatei. Mit folgendem Befehl könnt ihr euch die gesammte Sysmonkonfiguration ausgeben lassen:

```bash
Sysmon64.exe -c
```
<img src="../assets/img/Sysmon/sysconf.png" alt="sysconf" width="70%"/>

Da die Datei über 2000 Zeillen hat, werde ich sie hier nicht einfügen. Sie kann unter dem Pfad **"C:\ProgramData\Sysmon\sysmonConfig.xml"** geöffnet und angeschaut werden.

Die Datei enthält hauptsächlich RuleGroups für die Filterung von Events. Ansonsten enthält sie nur wenige Parameter. Dies kann man sehr gut betrachten wenn man die Datei in einem guten Editor "Collapsed":
<img src="../assets/img/Sysmon/conf.png" alt="conf" width="70%"/>

Wenn wir es genauer anschauen, sehen wir das jede RuleGroup eine Bestimmte Art von Events abfängt. Für jede Art von Event scheint es 2 Regelgruppen zu geben, einmal include und einmal exclude:
<img src="../assets/img/Sysmon/analysis1.png" alt="analysis1" width="70%"/>

Innerhalb der RegelGruppen werden nun alle nötigen Prozesse angegeben. Wenn man genauere Erbgebnisse möchte, kann man scheinbar auch einzelne Befehle der Prozesse angeben:
<img src="../assets/img/Sysmon/analysis2.png" alt="analysis2" width="80%"/>
