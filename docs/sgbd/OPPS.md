# OPPS.prg

- Jobs: [44](#jobs)
- Tables: [0](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Optisches Programmier- und Prüfsystem |
| ORIGIN | BMW VS-40 Rowedder |
| REVISION | 1.010 |
| AUTHOR | DMC Garcia-Herreros, BMW AG, VS-40 Rowedder, BMW AG VS-43 Kirma |
| COMMENT | Steuer-SGBD für Spezialfunktionen des OPPS |
| PACKAGE | 1.42 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung)
- [STATUS_BATT_IGNITION](#job-status-batt-ignition) - Ubatt(Kl. 30) ignition (Kl. 15) Werte
- [STATUS_TYP_VER](#job-status-typ-ver) - Typ und Version des Interfaces zurückliefern Wenn ICOM, dann wird "OPPS" zurückgeliefert
- [STEUERN_ROUTER_AUTOCOMM](#job-steuern-router-autocomm) - Setze Router in Auto-Communication Mode
- [STEUERN_ROUTER_MOST](#job-steuern-router-most) - Setze Router in MOST Modus
- [STEUERN_ROUTER_OBD](#job-steuern-router-obd) - Setze Router in OBD Mode
- [STEUERN_ROUTER_BYTEFLIGHT](#job-steuern-router-byteflight) - Setze Router in Byteflight Mode
- [STEUERN_ROUTER_MOSTMEAS](#job-steuern-router-mostmeas) - Set_Meas_Mode
- [STEUERN_ROUTER_PAR_FREE](#job-steuern-router-par-free) - veranlaßt eine IFH Instanz, alle Interfaces freizugeben
- [STEUERN_ROUTER_RESET](#job-steuern-router-reset) - veranlaßt eine IFH Instanz, alle Interfaces freizugeben
- [STEUERN_ROUTER_PAR_OBD](#job-steuern-router-par-obd) - Parallelbetrieb auf K-Line, alle anderen Interfaces werden freigegeben
- [STEUERN_ROUTER_PAR_MOST](#job-steuern-router-par-most) - Parallelbetrieb auf K-Line, alle anderen Interfaces werden freigegeben
- [STATUS_ROUTER](#job-status-router) - liefert den Namen des aktuell eingestellten Bus- interfaces oder "AUTO" für Automatik Modus
- [STEUERN_ROUTER_TRACEON](#job-steuern-router-traceon) - Router Trace einschalten
- [STEUERN_ROUTER_TRACEOFF](#job-steuern-router-traceoff) - Router command: Windows Ce Trace off
- [STATUS_MOST_NODES](#job-status-most-nodes) - Ads4Most Kommando: Get diagnose nodes der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST
- [STEUERN_MOST_BUILDREGISTRY](#job-steuern-most-buildregistry) - Abfragen der MOST Central Registry  auslösen der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST
- [STATUS_MOST_ONOFFTIME](#job-status-most-onofftime) - Ads4Most Kommando: Ermitteln MOST On- und Off- Zeiten sowie Zustand MOST Supervisor Achtung: dieser Job funktioniert erst ab OPPS Version 616. der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST.
- [STEUERN_MOST_MASTER_MODE](#job-steuern-most-master-mode) - CLock und Network Master Funktionalität für MOST schalten der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST
- [STEUERN_MOST_ASYNCOFF](#job-steuern-most-asyncoff) - MOST Asynchronkanal abschalten der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST
- [STEUERN_MOST_ASYNCON](#job-steuern-most-asyncon) - Ads4Most Kommando: Asynchronkanal einschalten der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST
- [STEUERN_MOST_ASYNCMINLENGTH](#job-steuern-most-asyncminlength) - Setze Minimallänge für Asynchronkanal der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST Default in OPPS Registry: 200d
- [STATUS_MOST_SG_ASYNC](#job-status-most-sg-async) - Fragt auf dem MOST die Asynchron-Fähigkeit eines SG ab
- [STEUERN_MOST_NOWAKEUP](#job-steuern-most-nowakeup) - MOST Wakeup abschalten der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST
- [STEUERN_MOST_WAKEUP](#job-steuern-most-wakeup) - Ads4Most Kommando: Wakeup einschalten der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST
- [STEUERN_MOSTCTRL_LLINTERVALL](#job-steuern-mostctrl-llintervall) - Setze den zeitlichen Abstand, in dem die Low Level Telegramme des MOST Kontrollkanals gesendet werden. Der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST Achtung! dieser Befehl ist erst ab OPPS Version 408 verfügbar!
- [STEUERN_MOSTCTRL_LLRETRY](#job-steuern-mostctrl-llretry) - Setze die Zeit, nach der nach einem Fehler ein  Low Level Telegramm des MOST Kontrollkanals wiederholt wird sowie die maximale Anzahl der Wiederholungen. Der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST Achtung! dieser Befehl ist erst ab OPPS Version 408 verfügbar!
- [STEUERN_MOST_DIAG_FBLOCK](#job-steuern-most-diag-fblock) - Ein und Ausschalten des Diagnose Funktionsblockes im OPPS
- [STATUS_MOST_DIAG_FBLOCK](#job-status-most-diag-fblock) - Prüfen, ob MOST Diagnose FBlock aktiv ist
- [STEUERN_MOST_TESTER_ADRESSE](#job-steuern-most-tester-adresse) - Setzen der Tester-Diagnoseadresse, die das OPPS auf dem MOST verwendet Ist der Diagnose Funktionsblock aktiv, so wird er umgemeldet Default nach Booten : 0xF5
- [STATUS_THREADS](#job-status-threads) - liefert die Anzahl möglicher parallel laufender IFH-Slaves auf einem Remote Interface
- [STATUS_MOST_REGISTRY](#job-status-most-registry) - Ads4Most Kommando: GETREGSTATUS (0x95) Holt Informationen über den Zustand der MOST Registry der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST
- [STEUERN_MOST_TRACEON](#job-steuern-most-traceon) - Trace für MOST einschalten der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST
- [STEUERN_MOST_TRACEOFF](#job-steuern-most-traceoff) - Ads4Most Kommando: Windows Ce Trace aus der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST
- [STEUERN_MOST_ETHTRACE](#job-steuern-most-ethtrace) - Ads4Most command: Enables/disables the ethernet trace
- [STATUS_MOST_REGISTERS](#job-status-most-registers) - Liest Bank 0 .. 3 der Register im MOST Chipsatz aus
- [STATUS_MOST_ACCLOG](#job-status-most-acclog) - liest das Access Log der 8104 nur in speziellen OPPS Testversionen verfügbar!
- [STEUERN_CAN_MODE](#job-steuern-can-mode) - Setzen des Umschaltemodus für CAN
- [STATUS_CAN_MODE](#job-status-can-mode) - Prüfen des Umschaltemodus für CAN
- [STATUS_CAN_KL_15](#job-status-can-kl-15) - Prüft ob Klemmenstatus Botschaft auf CAN empfangen wird
- [STATUS__OBD_KWP2KS](#job-status-obd-kwp2ks) - Holt Fehlerstatus KWP2000*
- [STEUERN_DLE_TRACEON](#job-steuern-dle-traceon) - Download Engine Trace einschalten
- [STEUERN_DLE_TRACEOFF](#job-steuern-dle-traceoff) - Abschalten Download Engine Trace

<a id="job-info"></a>
### INFO

Information SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergerät im Klartext |
| ORIGIN | string | Steuergeräte-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Namen aller Autoren |
| COMMENT | string | wichtige Hinweise |
| PACKAGE | string | Include-Paket-Nummer |
| SPRACHE | string | deutsch, english |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-status-batt-ignition"></a>
### STATUS_BATT_IGNITION

Ubatt(Kl. 30) ignition (Kl. 15) Werte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIE | long | Spannung in mV |
| STAT_IGNITION | long | Spannung in mV |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-status-typ-ver"></a>
### STATUS_TYP_VER

Typ und Version des Interfaces zurückliefern Wenn ICOM, dann wird "OPPS" zurückgeliefert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TYP | string | Interface-Klasse ("ICOM" wird zu "OPPS") ADS, PICO, EDIC, IDBSS, OPPS... |
| STAT_VERSION | int | Versionsnummer |
| STAT_SUBTYP | string | Tatsächliches Interface |
| STAT_SUBVERSION | int | Tatsächliche Version |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-router-autocomm"></a>
### STEUERN_ROUTER_AUTOCOMM

Setze Router in Auto-Communication Mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-router-most"></a>
### STEUERN_ROUTER_MOST

Setze Router in MOST Modus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-router-obd"></a>
### STEUERN_ROUTER_OBD

Setze Router in OBD Mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-router-byteflight"></a>
### STEUERN_ROUTER_BYTEFLIGHT

Setze Router in Byteflight Mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-router-mostmeas"></a>
### STEUERN_ROUTER_MOSTMEAS

Set_Meas_Mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-router-par-free"></a>
### STEUERN_ROUTER_PAR_FREE

veranlaßt eine IFH Instanz, alle Interfaces freizugeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-router-reset"></a>
### STEUERN_ROUTER_RESET

veranlaßt eine IFH Instanz, alle Interfaces freizugeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-router-par-obd"></a>
### STEUERN_ROUTER_PAR_OBD

Parallelbetrieb auf K-Line, alle anderen Interfaces werden freigegeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-router-par-most"></a>
### STEUERN_ROUTER_PAR_MOST

Parallelbetrieb auf K-Line, alle anderen Interfaces werden freigegeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-router"></a>
### STATUS_ROUTER

liefert den Namen des aktuell eingestellten Bus- interfaces oder "AUTO" für Automatik Modus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INTERFACE | string | Name des aktuell eingestellten Fahrzeuginterfaces {"AUTO", "OBD", "MOST", "CAN" ,"MOSTMEAS", "BFMEAS", "NONE", "UNKNOWN"} |
| STAT_ERROR | int | Für Versuch zweckentfremdet für die Fehlerrückmeldung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-router-traceon"></a>
### STEUERN_ROUTER_TRACEON

Router Trace einschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-router-traceoff"></a>
### STEUERN_ROUTER_TRACEOFF

Router command: Windows Ce Trace off

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-most-nodes"></a>
### STATUS_MOST_NODES

Ads4Most Kommando: Get diagnose nodes der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-buildregistry"></a>
### STEUERN_MOST_BUILDREGISTRY

Abfragen der MOST Central Registry  auslösen der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CLEARFIRST | int | 0 = Dezentrale Registry im OPPS nicht löschen (default) nur neue Einträge hinzu bzw. geänderte Einträge auf Stand bringen 1 = Dezentrale Registry im OPPS löschen, dann Einträge von NM übernehmen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-most-onofftime"></a>
### STATUS_MOST_ONOFFTIME

Ads4Most Kommando: Ermitteln MOST On- und Off- Zeiten sowie Zustand MOST Supervisor Achtung: dieser Job funktioniert erst ab OPPS Version 616. der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OFFTIME | unsigned int | Zeit seit Net Off in ms |
| STAT_ONTIME | unsigned int | Zeit seit Net On in ms |
| STAT_NET | string | Zustand des MOST Supervisors |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-master-mode"></a>
### STEUERN_MOST_MASTER_MODE

CLock und Network Master Funktionalität für MOST schalten der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CLOCK_MASTER | int | 0 = Clock Master functionality off, 1 = Clock Master functionality on |
| NETWORK_MASTER | int | 0 = Network Master functionality off, 1 = Network Master functionality on |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-asyncoff"></a>
### STEUERN_MOST_ASYNCOFF

MOST Asynchronkanal abschalten der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-asyncon"></a>
### STEUERN_MOST_ASYNCON

Ads4Most Kommando: Asynchronkanal einschalten der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-asyncminlength"></a>
### STEUERN_MOST_ASYNCMINLENGTH

Setze Minimallänge für Asynchronkanal der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST Default in OPPS Registry: 200d

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ASYNC_MIN_LENGTH | int | 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-most-sg-async"></a>
### STATUS_MOST_SG_ASYNC

Fragt auf dem MOST die Asynchron-Fähigkeit eines SG ab

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | Diagnoseadresse des abzufragenden SG's |
| REG_UPDATE | int | Veranlasst den Update des Asnc Flags in der dezentralen Registry des OPPS wenn != 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SG_ASYNC | string | "ERR_CONF_NOTOK"      = MOST Central Registry Not OK "ERR_NOT_IN_REGISTRY" = SG nicht in MOST Registry eingetragen "ERR_NO_RESPONSE"     = SG antwortet nicht "OK_CONTROL"          = SG kann nur über Kontrollkanal kommunizieren "OK_ASYNC"            = SG kann auch über Asynchron- kanal kommunizieren "ERR_UNKNOWN"         = Unbekannter Fehler |
| STAT_SG_MOSTADDR | string | MOST Adresse des SG als Hex String |
| STAT_ASYNCMINLENGTH | string | Minimallänge, ab der ein Telegramm auf Asynchronkanal gesendet wird als Dezimalstring |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-nowakeup"></a>
### STEUERN_MOST_NOWAKEUP

MOST Wakeup abschalten der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-wakeup"></a>
### STEUERN_MOST_WAKEUP

Ads4Most Kommando: Wakeup einschalten der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mostctrl-llintervall"></a>
### STEUERN_MOSTCTRL_LLINTERVALL

Setze den zeitlichen Abstand, in dem die Low Level Telegramme des MOST Kontrollkanals gesendet werden. Der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST Achtung! dieser Befehl ist erst ab OPPS Version 408 verfügbar!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LL_INTERVALL | int | Zeitlicher Abstand der LL-Telegramme in ms |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort vom OPPS |

<a id="job-steuern-mostctrl-llretry"></a>
### STEUERN_MOSTCTRL_LLRETRY

Setze die Zeit, nach der nach einem Fehler ein  Low Level Telegramm des MOST Kontrollkanals wiederholt wird sowie die maximale Anzahl der Wiederholungen. Der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST Achtung! dieser Befehl ist erst ab OPPS Version 408 verfügbar!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LL_RECOVERY | int | Zeit nach der ein LL-Telegramm wiederholt wird in ms |
| LL_RETRIES | int | Anzahl der LL-Telegramm Wiederholungen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an das OPPS |
| _TEL_ANTWORT | binary | Hex-Antwort vom OPPS |

<a id="job-steuern-most-diag-fblock"></a>
### STEUERN_MOST_DIAG_FBLOCK

Ein und Ausschalten des Diagnose Funktionsblockes im OPPS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAG_FB_AKTIV | int | enable function block |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-most-diag-fblock"></a>
### STATUS_MOST_DIAG_FBLOCK

Prüfen, ob MOST Diagnose FBlock aktiv ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAG_FB_AKTIV | int | 1 = MOST Diagnose FBlock aktiv |
| STAT_DIAG_FB_INST | int | Instanz des vom OPPS angemeldeten Diagnose-FB (Diagnoseadresse) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-tester-adresse"></a>
### STEUERN_MOST_TESTER_ADRESSE

Setzen der Tester-Diagnoseadresse, die das OPPS auf dem MOST verwendet Ist der Diagnose Funktionsblock aktiv, so wird er umgemeldet Default nach Booten : 0xF5

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | Diagnoseadresse |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-threads"></a>
### STATUS_THREADS

liefert die Anzahl möglicher parallel laufender IFH-Slaves auf einem Remote Interface

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| THREADS | int | mögliche Anzahl parallel laufender IFHs |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-most-registry"></a>
### STATUS_MOST_REGISTRY

Ads4Most Kommando: GETREGSTATUS (0x95) Holt Informationen über den Zustand der MOST Registry der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CONFIG | string | Letzte Config Meldung vom NetworkMaster {"NotOK", "OK", "Invalid", "New"} |
| STAT_USABLE | string | "OK" wenn Registry im OPPS gültig, sonst "NotOK" |
| STAT_COMPLETED | string | Interner OPPS Status "COMPLETE" wenn Registry im OPPS vollständig augebaut, sonst "UNDER_CONSTRUCTION" |
| STAT_DEBUG | string | Interner OPPS Status {"Loading", "Wait_For_Config_IDs", "WaitForRegistry"} |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-traceon"></a>
### STEUERN_MOST_TRACEON

Trace für MOST einschalten der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-traceoff"></a>
### STEUERN_MOST_TRACEOFF

Ads4Most Kommando: Windows Ce Trace aus der Router muß auf MOST geschaltet sein mit STEUERN_ROUTER_MOST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-ethtrace"></a>
### STEUERN_MOST_ETHTRACE

Ads4Most command: Enables/disables the ethernet trace

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ENABLE | int | enable eternet trace |
| PORT | int | Target Port |
| IPADDR | string | Target IP Address |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-most-registers"></a>
### STATUS_MOST_REGISTERS

Liest Bank 0 .. 3 der Register im MOST Chipsatz aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BANK_0 | binary | Inhalt der Bytes 0..254 von Bank 0 |
| STAT_BANK_1 | binary | Inhalt der Bytes 0..254 von Bank 1 |
| STAT_BANK_2 | binary | Inhalt der Bytes 0..254 von Bank 2 |
| STAT_BANK_3 | binary | Inhalt der Bytes 0..254 von Bank 3 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-most-acclog"></a>
### STATUS_MOST_ACCLOG

liest das Access Log der 8104 nur in speziellen OPPS Testversionen verfügbar!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ACC_0_41 | binary | Zugriffe 0..41 |
| STAT_ACC_42_83 | binary | Zugriffe 42..83 |
| STAT_ACC_84_99 | binary | Zugriffe 84..99 |

<a id="job-steuern-can-mode"></a>
### STEUERN_CAN_MODE

Setzen des Umschaltemodus für CAN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAN_MODE | string | "AUTO"   = Umschalten anhand Klemmenstatus Botschaft "CAN"    = immer CAN "K_LINE" = immer K-Line "TRY_CANFIRST" = erst DCAN probieren "TRY_KFIRST"   = erst K-Line probieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-mode"></a>
### STATUS_CAN_MODE

Prüfen des Umschaltemodus für CAN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CAN_MODE | string | OKAY, wenn fehlerfrei |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-kl-15"></a>
### STATUS_CAN_KL_15

Prüft ob Klemmenstatus Botschaft auf CAN empfangen wird

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KL_15 | string | Klemmenstatus über CAN |
| STAT_DNMT | string | "DNMT" = im DNMT Modus |
| STAT_BOTSCHAFT | string | "VORHANDEN" = Klemmenstatus Botschaft kommt auf D-CAN |
| STAT_SWITCH | string | "GESETZT" = Klemmenstatus botschaft min. 1x empfangen "NICHT_GESETZT" Klemmenstatus Botschaft noch nicht empfangen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-obd-kwp2ks"></a>
### STATUS__OBD_KWP2KS

Holt Fehlerstatus KWP2000*

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dle-traceon"></a>
### STEUERN_DLE_TRACEON

Download Engine Trace einschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dle-traceoff"></a>
### STEUERN_DLE_TRACEOFF

Abschalten Download Engine Trace

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

No tables found.
