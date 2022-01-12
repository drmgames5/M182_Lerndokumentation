# Recherche Sysmon

Sysmon ist eine Monitoring Lösung mit der man Betriebssysteme überwachen kann. Sysmon ist ein Treiber und wird bei jedem start automatisch mitgestartet. Es nimmt alle Ereignisse auf dem Gerät auf, auf dem es installiiert wurde. Daraufhin generiert Sysmon für jedes Ereignis Windows Event-Logs. Es verbessert sozusagen die Funktionalität von Windows Logs. Die gesammelten Daten können anschliessend nach belieben analysiert werden.

## Version
> [!Tip]
> Sysmon ist aktuell in der Version 13.31

## Use Cases

Sysmon kann sehr vielfältig eingesetzt werden, weshalb ich hier nur auf die verbreiteste Nutzung eingehen werde.

Der wohl verbreiteste Use Case von Sysmon ist, Sicherheitslücken zu erkennen. Da Sysmon alle Events des Systems aufnimmt, kann das gesamte System damit Analysiert werden. Man kann zum Beispiel ausschau nach bestimmten verhalten halten. Falls Sysmon dieses bestimmte verhalten oder bestimmte Zustände erkennt kann es eine Warnung dafür melden. Somit kann man nach bekannten Sicherheitslücken oder Malware auf den Systemen suchen. Dies wird Thread-Hunting gennant.

Des weiteren wird Sysmon z.B für die nachverfolgung von Netzwerkverbindungen verwendet
