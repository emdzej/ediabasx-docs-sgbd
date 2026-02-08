# icom_p.prg

- Jobs: [82](#jobs)
- Tables: [20](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Steuerdatei für Diagnoseinterface ICOMP und ICOMP Next |
| ORIGIN | BMW TI-538 Rothenberger |
| REVISION | 3.020 |
| AUTHOR | I+ME_ACTIA SW_Entwicklung Stephan_Keilholz, ACTIA_I+ME SW_Entwi |
| COMMENT | steuern_trace_retrieve und steuern_trace_retrieve_all mit Asynchrone, Zusammenführung ICOMP und ICOMP Next |
| PACKAGE | 1.990 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [STATUS_BATT_IGNITION](#job-status-batt-ignition) - Ubatt(Kl. 30) ignition (Kl. 15) Werte
- [STATUS_TYP_VER](#job-status-typ-ver) - Ubatt(Kl. 30) ignition (Kl. 15) Werte
- [STATUS_CAN_KL_15](#job-status-can-kl-15) - Prüft ob Klemmenstatus Botschaft auf CAN empfangen wird
- [STEUERN_TRIGGER_AUTOASSIGN_BROADCAST](#job-steuern-trigger-autoassign-broadcast) - Erzwingt das neu Senden der Autoassign Statusbotschaft via HTTP
- [STEUERN_BEEP](#job-steuern-beep) - Steuert den Summer mit der angegebenen Frequenz und Dauer an gültig nur bei ICOMP Next
- [STEUERN_MELODY](#job-steuern-melody) - Spilet eine Melody mithilfe des Summers gültig nur bei ICOMP Next
- [STEUERN_HSFZ_ENABLE](#job-steuern-hsfz-enable) - Einschalten des HSFZ
- [STEUERN_HSFZ_DISABLE](#job-steuern-hsfz-disable) - Ausschalten des HSFZ
- [STATUS_HSFZ_GET_STATUS](#job-status-hsfz-get-status) - STATUS des HSFZ
- [STATUS_HSFZ_GET_STATUS_NEU](#job-status-hsfz-get-status-neu) - STATUS des HSFZ
- [STATUS_HSFZ_GET_STATUS_DETAIL](#job-status-hsfz-get-status-detail) - erweiterter STATUS des HSFZ
- [STATUS_GET_CANBRIDGE_STATUS](#job-status-get-canbridge-status) - Abfragen des HSFZ-CANBridge Status
- [STEUERN_SET_CANBRIDGE_STATUS](#job-steuern-set-canbridge-status) - HsfzCanBridge  einschalten/ausschalten
- [STEUERN_RESTART_HSFZ_STR](#job-steuern-restart-hsfz-str) - Restart HSFZ Start Routine
- [STEUERN_RESTART_HSFZ_RRR](#job-steuern-restart-hsfz-rrr) - Restart HSFZ Request Routine Results
- [STEUERN_CREATE_ECU_ROUTES_STR](#job-steuern-create-ecu-routes-str) - CreateEcuRoutes Start Routine Anlegen der Routen für ein Steuergerät
- [STEUERN_CREATE_ECU_ROUTES_RRR](#job-steuern-create-ecu-routes-rrr) - Restart HSFZ Request Routine Results
- [STEUERN_SWITCH_ACT_LINE_STR](#job-steuern-switch-act-line-str) - SwitchActLine Start Routine Ethernet Aktivierungsleitung schalten
- [STEUERN_SWITCH_ACT_LINE_STP](#job-steuern-switch-act-line-stp) - SwitchActLine Stop Routine
- [STEUERN_SWITCH_ACT_LINE_RRR](#job-steuern-switch-act-line-rrr) - SwitchActLine Request Routine Results
- [STEUERN_SWITCH_LINK_STR](#job-steuern-switch-link-str) - SwitchActLine Start Routine Ethernet Aktivierungsleitung schalten
- [STEUERN_SWITCH_LINK_STP](#job-steuern-switch-link-stp) - SwitchActLine Stop Routine
- [STEUERN_SWITCH_LINK_RRR](#job-steuern-switch-link-rrr) - SwitchActLine Request Routine Results
- [STEUERN_INQ_HSFZ_GW_STR](#job-steuern-inq-hsfz-gw-str) - Inquire HSFZ GatewayStart Routine
- [STEUERN_INQ_HSFZ_GW_STP](#job-steuern-inq-hsfz-gw-stp) - Inquire HSFZ Gateway Stop Routine
- [STEUERN_INQ_HSFZ_GW_RRR](#job-steuern-inq-hsfz-gw-rrr) - Inquire HSFZ Gateway Request Routine Results
- [STEUERN_CHECK_URL_STR](#job-steuern-check-url-str) - Inquire HSFZ GatewayStart Routine
- [STEUERN_CHECK_URL_STP](#job-steuern-check-url-stp) - Inquire HSFZ Gateway Stop Routine
- [STEUERN_CHECK_URL_RRR](#job-steuern-check-url-rrr) - Inquire HSFZ Gateway Request Routine Results
- [STEUERN_PIN_CONTROL_STR](#job-steuern-pin-control-str) - PinControl Start Routine Einstellen der gewünschten Pullup-Werte
- [STEUERN_PIN_CONTROL_RRR](#job-steuern-pin-control-rrr) - Pin Control Request Results Routine
- [STATUS_GET_VIN](#job-status-get-vin) - Auslesen der im ICOM gesetzten VIN
- [STEUERN_SET_VIN](#job-steuern-set-vin) - Setzen der VIN im ICOM
- [STEUERN_VERIFY_VIN](#job-steuern-verify-vin) - Verifizieren einer VIN mit der im ICOM gesetzten
- [STEUERN_VIN_XML_ERASE](#job-steuern-vin-xml-erase) - Löschen der vom Autoassign generierten VIN-XML Files auf den Servern
- [STATUS_GET_VERSIONS](#job-status-get-versions) - Auslesen der Image Versionen des ICOM
- [STATUS_GET_CONFIG](#job-status-get-config) - Auslesen der Konfiguration des ICOM, erzeugt eine variable Liste von Ergebnissen
- [STATUS_GET_CONFIG_DETAIL](#job-status-get-config-detail) - Auslesen eines bestimmten Konfiguartionsparameters
- [STEUERN_START_NET_CONFIG](#job-steuern-start-net-config) - Einlesen der Konfiguration über das Netzwerk
- [STEUERN_UPDATE](#job-steuern-update) - Softwareupdate des ICOM-P über das Netzwerk
- [STATUS_GET_IWCONFIG](#job-status-get-iwconfig) - Führt ein iwconfig auf dem ICOM aus und liefert dessen Ergebnisse. Es wird eine variable Liste von Ergebnissen erzeugt.
- [STEUERN_MANUAL_ROAMING](#job-steuern-manual-roaming) - Erzwingen eines WLAN-Roaming vorganges
- [STEUERN_TRACEON](#job-steuern-traceon) - ICOM CAN/HSFZ Trace einschalten
- [STEUERN_TRACEOFF](#job-steuern-traceoff) - Abschalten CAN/HSFZ Trace
- [STATUS_TRACE_STATE](#job-status-trace-state) - Lesen von Trace Informationen
- [STEUERN_TRACE_BOOT_ENABLE](#job-steuern-trace-boot-enable) - Automatisches tracen nach Neustart des ICOMs
- [STATUS_TRACE_GET_CONFIG](#job-status-trace-get-config) - Lesen der Trace-Konfiguration
- [STEUERN_DCAN_TRACE](#job-steuern-dcan-trace) - D-CAN Trace einschalten/ausschalten
- [STEUERN_KL15_TRACE](#job-steuern-kl15-trace) - KL15 (0x130) Trace einschalten/ausschalten
- [STEUERN_ETHERNET_TRACE](#job-steuern-ethernet-trace) - ETHERNET Trace einschalten/ausschalten
- [STEUERN_UDP_TRACE](#job-steuern-udp-trace) - UDP Logging einschalten/ausschalten
- [STEUERN_ARP_TRACE](#job-steuern-arp-trace) - ARP Logging einschalten/ausschalten
- [STEUERN_LS_TRACE](#job-steuern-ls-trace) - Link Status Logging einschalten/ausschalten
- [STEUERN_WLANPING_TRACE](#job-steuern-wlanping-trace) - Link Status Logging einschalten/ausschalten
- [STEUERN_IFHENET_TRACE](#job-steuern-ifhenet-trace) - IFH ETHERNET Logging einschalten/ausschalten
- [STEUERN_TRACE_TARGET](#job-steuern-trace-target) - Ablageziel der Tracedateien festlegen
- [STEUERN_TRACE_FILENAMEBASE](#job-steuern-trace-filenamebase) - Variable Basis des Dateinames der Tracedateien setzen
- [STEUERN_TRACE_REMOTEURL](#job-steuern-trace-remoteurl) - URL-Freigabe für die Ablage der Tracedaten (remote/offline)
- [STEUERN_TRACE_DCANSIZE](#job-steuern-trace-dcansize) - Maximale Grösse der D-CAN Tracedateien auf dem ICOM setzen
- [STEUERN_TRACE_ETHERNETSIZE](#job-steuern-trace-ethernetsize) - Maximale Grösse der ETHERNET Tracedateien auf dem ICOM setzen
- [STEUERN_TRACE_RETRIEVE](#job-steuern-trace-retrieve) - Tracedatei vom ICOM auf REMOTEURL übertragen
- [STEUERN_TRACE_RETRIEVE_ALL](#job-steuern-trace-retrieve-all) - gesamte Tracedaten vom ICOM auf REMOTEURL übertragen
- [STEUERN_TRACE_ERASE](#job-steuern-trace-erase) - Löschen aller Tracefiles auf dem ICOM
- [STEUERN_DEBUGMODE](#job-steuern-debugmode) - ICOM DEBUGMODE einschalten
- [STEUERN_DEBUGMODE_GETFILES](#job-steuern-debugmode-getfiles) - Auslesen der Debugmode Dateien über das Netzwerk
- [STEUERN_DEBUGMODE_ERASEFILES](#job-steuern-debugmode-erasefiles) - Löschen der Debugmode Dateien auf der SD Karte
- [STEUERN_REBOOT](#job-steuern-reboot) - Neustart des ICOM_P
- [STEUERN_SWITCH_OFF](#job-steuern-switch-off) - Ausschalten des ICOM_P
- [STEUERN_CONSTANT_CURRENT](#job-steuern-constant-current) - Ein/Ausschalten des Konstantstrommodus
- [STATUS_CONSTANT_CURRENT](#job-status-constant-current) - Zustand des Konstantstrommodus
- [STEUERN_SEND_WAKE_UP](#job-steuern-send-wake-up) - Senden eine WakeUp-Pulses auf OBD Pin 8 (HSFZ-Aktivierungsleitung) Unterstützung des Fahrzeuges vorausgesetzt
- [STEUERN_ON_SET_CAN_ID](#job-steuern-on-set-can-id) - Einschalten des ICOM_P durch ein bestimmtes CAN Telegramm
- [STEUERN_SET_CAN_IDLE_TIME](#job-steuern-set-can-idle-time) - Ausschalten des ICOM_P wenn keine CAN Kommunikation vorhanden ist
- [STEUERN_ENABLE_ACC_WAKEUP](#job-steuern-enable-acc-wakeup) - Einschalten des ICOM_P durch den Bewegungssensor
- [STEUERN_WAKEUP_TIMER](#job-steuern-wakeup-timer) - Setzt die Zeit nach der das ICOMP Next wieder erwacht
- [STEUERN_FEHLERSPEICHER_LESEN](#job-steuern-fehlerspeicher-lesen) - Auslesen des Fehlerspeichers des ICOMs
- [STEUERN_FEHLERSPEICHER_LOESCHEN](#job-steuern-fehlerspeicher-loeschen) - Löscht den Fehlerspeichers des ICOMs
- [STEUERN_WAKE_ON_EX_TRIGGER](#job-steuern-wake-on-ex-trigger) - gültig nur bei ICOMP Next mit Funkmodul Wakeup über Funkmodul Ein- Ausschalten
- [STEUERN_WAKE_ON_EX_TRIGGER_FREQ](#job-steuern-wake-on-ex-trigger-freq) - gültig nur bei ICOMP Next mit Funkmodul Benutzte Frequenz des Funkmoduls
- [STEUERN_SEND_EX_TRIGGER](#job-steuern-send-ex-trigger) - gültig nur bei ICOMP Next mit Funkmodul Senden eines Aufweckkommandos

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

Initialisierung und Kommunikationsparameter

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

Ubatt(Kl. 30) ignition (Kl. 15) Werte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TYP | string | ADS, PICO, EDIC, IDBSS, OPPS... |
| STAT_VERSION | int | Versionsnummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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

<a id="job-steuern-trigger-autoassign-broadcast"></a>
### STEUERN_TRIGGER_AUTOASSIGN_BROADCAST

Erzwingt das neu Senden der Autoassign Statusbotschaft via HTTP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn erfolgreich |
| _TEL_ANTWORT | binary | STEUERN_TRIGGER_AUTOASSIGN_BROADCAST erfolgreich |

<a id="job-steuern-beep"></a>
### STEUERN_BEEP

Steuert den Summer mit der angegebenen Frequenz und Dauer an gültig nur bei ICOMP Next

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREQUENCE | int | Frequenz mit der der Summer angesteuert wird Gültiger Bereich: 100-10000 |
| DURATION | int | Dauer in ms für die der Summer angesteuert wird Gültiger Bereich: 10-5000 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn erfolgreich |
| _TEL_ANTWORT | binary | STEUERN_BEEP erfolgreich |

<a id="job-steuern-melody"></a>
### STEUERN_MELODY

Spilet eine Melody mithilfe des Summers gültig nur bei ICOMP Next

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MELODY | int | Nummer der zu spielenden Melody (1..5) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn erfolgreich |
| _TEL_ANTWORT | binary | STEUERN_BEEP erfolgreich |

<a id="job-steuern-hsfz-enable"></a>
### STEUERN_HSFZ_ENABLE

Einschalten des HSFZ

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | OKAY ist gestartet |

<a id="job-steuern-hsfz-disable"></a>
### STEUERN_HSFZ_DISABLE

Ausschalten des HSFZ

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | OKAY, HSFZ gestoppt |

<a id="job-status-hsfz-get-status"></a>
### STATUS_HSFZ_GET_STATUS

STATUS des HSFZ

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HSFZ_STATUS | string | ENABLED  -&gt; HSFZ ist aktiv DISABLED -&gt; HSFZ ist deaktiviert |
| _TEL_ANTWORT | binary | ENABLED                      -&gt; HSFZ ist aktiv DISABLED                     -&gt; HSFZ ist deaktiviert BUSY                         -&gt; HSFZ ist belegt ERROR_INVALID_RESPONSE HSFZ  -&gt; ungültige Antwort ERROR_NO_HSFZ                -&gt; kein Link zum Fahrzeug ERROR_ZGW_NOT_FOUND          -&gt; kein ZGW gefunden ERROR_BROKEN_LINK            -&gt; Nicht alle Ethernetleitungen verbunden |

<a id="job-status-hsfz-get-status-neu"></a>
### STATUS_HSFZ_GET_STATUS_NEU

STATUS des HSFZ

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HSFZ_WORKAROUND | int | HSFZ_Workaround bei Status BUSY enhaelt schaltbaren Workaround: BUSY--&gt;Disable--&gt; Pause 1s --&gt; Enable --&gt;Pause 5s --&gt; Status nochmal auslesen "1"    	=  aktiv Default	=  nicht aktiv |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HSFZ_STATUS | string | ENABLED                       -&gt; HSFZ ist aktiv DISABLED                      -&gt; HSFZ ist deaktiviert BUSY                          -&gt; HSFZ ist belegt ERROR_INVALID_RESPONSE HSFZ   -&gt; ungültige Antwort ERROR_NO_HSFZ                 -&gt; kein Link zum Fahrzeug ERROR_ZGW_NOT_FOUND           -&gt; kein ZGW gefunden ERROR_BROKEN_LINK             -&gt; Nicht alle Ethernetleitungen verbunden |
| _TEL_ANTWORT | binary | Antwortelegramm vom ICOMP |

<a id="job-status-hsfz-get-status-detail"></a>
### STATUS_HSFZ_GET_STATUS_DETAIL

erweiterter STATUS des HSFZ

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_LINK_DIAG_RESULT | string | LINKDIAG_OK  -&gt; kein Fehler erkannt LINKDIAG_ERR_TXPAIR -&gt; Fehler auf dem Tx Paar LINKDIAG_ERR_RXPAIR -&gt; Fehler auf dem Rx Paar LINKDIAG_ERR_BOTH_PAIRS -&gt; Fehler auf beiden Paaren LINKDIAG_PHYERR -&gt; Problem beim Loopbacktest mit dem Switch |
| STAT_CURRENT_STATE | string | STATUS_WAIT_FOR_LINK STATUS_WAIT_FOR_REPLY STATUS_WAIT_FOR_PING STATUS_HSFZ_ACTIVE STATUS_MUST_DISABLE STATUS_DISABLED STATUS_MUST_ENABLE STATUS_BROKEN_LINK |
| STAT_CURRENT_STATE_TIME | string | Zeit, die sich der HSFZ Link in diesem Status befindet ,Format: sekunden.microsekunden |
| STAT_ZGW_IP | string | IP Adresse des ZGW |
| STAT_PING_RESULT | string | Ergebnis des durch dieses Kommando ausgelösten Pings OK NOK No IP |
| STAT_DISTANCE_TO_FAULT | int | Distanz zur Problemquelle in dm, Genauigkeit +- 20 dm |
| _TEL_ANTWORT | binary | Antwortelegramm vom ICOMP |

<a id="job-status-get-canbridge-status"></a>
### STATUS_GET_CANBRIDGE_STATUS

Abfragen des HSFZ-CANBridge Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_CURRENT_STATE | string | running = ist gestartet not running = ist nicht gestartet |
| STAT_ENABLED_ON_STARTUP | string | enabled = HSFZ-CANBridge wird nach reboot automatisch gestartet disabled = iHSFZ-CANBridge wird nach reboot nicht gestartet |
| _TEL_ANTWORT | binary | Antwortelegramm vom ICOMP |

<a id="job-steuern-set-canbridge-status"></a>
### STEUERN_SET_CANBRIDGE_STATUS

HsfzCanBridge  einschalten/ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CANBRIDGE_STATUS | string | "ON"   = einschalten "OFF"  = ausschalten |
| CANBRIDGE_PERSISTENT | string | "P"   = persistent speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antwortelegramm vom ICOMP |

<a id="job-steuern-restart-hsfz-str"></a>
### STEUERN_RESTART_HSFZ_STR

Restart HSFZ Start Routine

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DEACT_TIME_MS | int | Zeit, die die Aktivierungsleitung auf 0 gezogen wird in Millisekunden, Default = 1000 |
| ROUTING_MODE | string | "ROUTING" (Default) \| "DIRECT" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-restart-hsfz-rrr"></a>
### STEUERN_RESTART_HSFZ_RRR

Restart HSFZ Request Routine Results

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HSFZ_READY | string | BUSY = HSFZ Restart laeuft READY = HSFZ Restart laeuft nicht |
| STAT_ETH_LINK | string | ON = Fahrzeug Ethernet hat Link OFF = Fahrzeug Ethernet hat kein Link |
| STAT_GW_STATUS | string | OK = GW hat sich gemeldet, IP i.O. BAD GATEWAY_IP = GW hat sich gemeldet, IP n.i.O. NO_GATEWAY = GW hat sich nicht gemeldet |
| STAT_GW_DIAGADR | string | Diagnoseadresse des Gateways als Hexstring |
| STAT_VIN | string | Fahrgestellnummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-create-ecu-routes-str"></a>
### STEUERN_CREATE_ECU_ROUTES_STR

CreateEcuRoutes Start Routine Anlegen der Routen für ein Steuergerät

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_DIAG_ADDRESS | string | Diagnoseadresse des Steuergeräts (z.B. "0x63") |
| SG_IP_ADDRESS | string | IP-Adresse des Steuergeräts (z.B. "169.254.10.99") |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _IP1 | int | IP-Adresse Byte 1 |
| _IP2 | int | IP-Adresse Byte 2 |
| _IP3 | int | IP-Adresse Byte 3 |
| _IP4 | int | IP-Adresse Byte 4 |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-create-ecu-routes-rrr"></a>
### STEUERN_CREATE_ECU_ROUTES_RRR

Restart HSFZ Request Routine Results

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAG_ADDR | string | Diagnoseadresse in Hex |
| STAT_ROUTETYPE | string | "HSFZ" \| "DOIP" |
| STAT_IP_ADDR | string | IP-Adresse des SG |
| STAT_PORT | string | Basisport in dezimal |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-switch-act-line-str"></a>
### STEUERN_SWITCH_ACT_LINE_STR

SwitchActLine Start Routine Ethernet Aktivierungsleitung schalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | Modus: "OFF" \| "ON" \| "PULSE" |
| PULSE_DURATION_MS | int | Ausschaltzeit in ms wenn MODE == "PULSE" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-switch-act-line-stp"></a>
### STEUERN_SWITCH_ACT_LINE_STP

SwitchActLine Stop Routine

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-switch-act-line-rrr"></a>
### STEUERN_SWITCH_ACT_LINE_RRR

SwitchActLine Request Routine Results

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LEVEL | string | "ON" \| "OFF" |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-switch-link-str"></a>
### STEUERN_SWITCH_LINK_STR

SwitchActLine Start Routine Ethernet Aktivierungsleitung schalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | Modus: "OFF" \| "ON" \| "PULSE" |
| PULSE_DURATION_MS | int | Ausschaltzeit in ms wenn MODE == "PULSE" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-switch-link-stp"></a>
### STEUERN_SWITCH_LINK_STP

SwitchActLine Stop Routine

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-switch-link-rrr"></a>
### STEUERN_SWITCH_LINK_RRR

SwitchActLine Request Routine Results

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CONTROL | string | "ON" \| "OFF" |
| STAT_LINK | string | "ON" \| "OFF" |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-inq-hsfz-gw-str"></a>
### STEUERN_INQ_HSFZ_GW_STR

Inquire HSFZ GatewayStart Routine

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TIMEOUT_MS | int | Zeit, die auf eine Antwort vom Gateway gewartet wird in Millisekunden, Default = 1000, Max = 2000 |
| RETRIES | int | Anzahl der Wiederholungen, wenn keine Antwort vom Gateway kommt Default = 2, Max. = 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-inq-hsfz-gw-stp"></a>
### STEUERN_INQ_HSFZ_GW_STP

Inquire HSFZ Gateway Stop Routine

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-inq-hsfz-gw-rrr"></a>
### STEUERN_INQ_HSFZ_GW_RRR

Inquire HSFZ Gateway Request Routine Results

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HSFZ_READY | string | BUSY = HSFZ Restart laeuft READY = HSFZ Restart laeuft nicht |
| STAT_ETH_LINK | string | ON = Fahrzeug Ethernet hat Link OFF = Fahrzeug Ethernet hat kein Link |
| STAT_GW_STATUS | string | OK = GW hat sich gemeldet, IP i.O. BAD GATEWAY_IP = GW hat sich gemeldet, IP n.i.O. NO_GATEWAY = GW hat sich nicht gemeldet |
| STAT_GW_DIAGADR | string | Diagnoseadresse des Gateways als Hexstring |
| STAT_VIN | string | Fahrgestellnummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-check-url-str"></a>
### STEUERN_CHECK_URL_STR

Inquire HSFZ GatewayStart Routine

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TIMEOUT_S | int | Zeit, die auf eine Antwort vom Server gewartet wird in Sekunden, Default = 30, Min = 10, Max = 2000 |
| RETRIES | int | Anzahl der Wiederholungen, wenn keine Antwort vom Server kommt Default = 0, Max. = 255 Da bereits Retries auf TCP - Ebene erfolgen, sind Retries auf HTTP Ebene wenig erfolgversprechend. Daher Default = 0 |
| LENGTH | int | Laenge des URL - Strings, max. 1200 |
| URL | string | URL - String, max. 1200 Zeichen, nullterminiert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-check-url-stp"></a>
### STEUERN_CHECK_URL_STP

Inquire HSFZ Gateway Stop Routine

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-check-url-rrr"></a>
### STEUERN_CHECK_URL_RRR

Inquire HSFZ Gateway Request Routine Results

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NET_ERROR_INT | int | Fehler auf TCP Ebene Codierung siehe Tabelle CU_ERR_TEXT |
| STAT_NET_ERROR_STRING | string | Fehler auf TCP Ebene als String Codierung siehe Tabelle CU_ERR_TEXT |
| STAT_HTTP_STATUS | int | HTTP-Statuscode Ergebnis wird nur angelegt, wenn NET_ERROR_INT == 0 |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-pin-control-str"></a>
### STEUERN_PIN_CONTROL_STR

PinControl Start Routine Einstellen der gewünschten Pullup-Werte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PUP7 | int | Pullup in Ohm für Pin 7 der OBD-Dose. 0 = kein Pullup (0,500,1000) Default = 0 |
| PUP8 | int | Pullup in Ohm für Pin 8 der OBD-Dose. 0 = kein Pullup (0,500,1000) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-pin-control-rrr"></a>
### STEUERN_PIN_CONTROL_RRR

Pin Control Request Results Routine

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag zum SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| PUP7 | int | Pullup in Ohm für Pin 7 der OBD-Dose. Default: 0 = kein Pullup (0,500,1000) |
| UPin7 | int | Spannung an Pin 7 der OBD-Dose in mV |
| PUP8 | int | Pullup in Ohm für Pin 8 der OBD-Dose. Default: 0 = kein Pullup (0,500,1000) |
| UPin8 | int | Spannung an Pin 8 der OBD-Dose in mV |
| UPin1 | int | Spannung an Pin 1 der OBD-Dose in mV |
| UPin16 | int | Spannung an Pin 16 der OBD-Dose in mV |
| AdapterConf | string | Bitmaske, die angibt, welche Adapter angesteckt sind: 0x01 = ICOM B angesteckt 0x02 = ICOM C angesteckt 0x04 = ICOM D angesteckt 0x08 = ICOM E angesteckt |
| CanCl | string | Bitmaske, die angibt, welche zyklischen CAN-Botschaften empfangen werden: 0x01 : Klemmenstatus Botschaft (130h) 0x02 : Fahrzeugzustands – Botschaft (3Ch) |
| CanCl15 | string | 0x01 = Klemme 15 in Botschaft 130h Ein, 0x00 sonst |
| CanPWF | string | Signal ST_CON_VEH( Bit 0 .. Bit 3) aus Byte 6 der Fahrzeugzustands-Botschaft (3Ch) |

<a id="job-status-get-vin"></a>
### STATUS_GET_VIN

Auslesen der im ICOM gesetzten VIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn VIN vorhanden NO_VIN, wenn keine VIN im ICOM gesetzt |
| STAT_VIN | string | VIN aus dem ICOM |
| _TEL_ANTWORT | binary | STATUS_GET_VIN erfolgreich |

<a id="job-steuern-set-vin"></a>
### STEUERN_SET_VIN

Setzen der VIN im ICOM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VIN | string | VIN des Fahrzeuges |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| SERVER_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | STEUERN_SET_VIN erfolgreich |

<a id="job-steuern-verify-vin"></a>
### STEUERN_VERIFY_VIN

Verifizieren einer VIN mit der im ICOM gesetzten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VIN | string | VIN zum Vergleichen |
| USEACTUAL | string | optional 0=VIN neu aus dem Fahrzeug auslesen und dann Vergleichen (default) 1=VIN mit der bereits ausgelesen VIN Vergleichen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn VINs gleich NO_VIN, wenn keine VIN im ICOM gesetzt VIN_DIFFERENT, wenn VINs unterschiedlich |
| _TEL_ANTWORT | binary | STEUERN_VERIFY_VIN erfolgreich |

<a id="job-steuern-vin-xml-erase"></a>
### STEUERN_VIN_XML_ERASE

Löschen der vom Autoassign generierten VIN-XML Files auf den Servern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VIN | string | Zu löschende VIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | STEUERN_SET_VIN erfolgreich |

<a id="job-status-get-versions"></a>
### STATUS_GET_VERSIONS

Auslesen der Image Versionen des ICOM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SYSTEM_VERSION | string | Version des ICOM Bootimage |
| STAT_APPLICATION_VERSION | string | Version des ICOM Applicationimage |
| STAT_PACKAGE_VERSION | string | Package Version der Images |
| STAT_SERIALNUMBER | string | Seriennummer des ICOM |
| _TEL_ANTWORT | binary | ICOMP_GET_VERSIONS erfolgreich |

<a id="job-status-get-config"></a>
### STATUS_GET_CONFIG

Auslesen der Konfiguration des ICOM, erzeugt eine variable Liste von Ergebnissen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WPACERTIFICATE | binary | WPA-Zertifikat |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-status-get-config-detail"></a>
### STATUS_GET_CONFIG_DETAIL

Auslesen eines bestimmten Konfiguartionsparameters

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARAMETER | string | Auszulesender Konfiguartionsparameter (siehe dazu Ergebniss von STATUS_GET_CONFIG) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VALUE | string | Ausgelesener Wert |
| JOB_STATUS | string | OKAY, wenn der Wert gelesen werden konnte NOT_FOUND, wenn der Wert nicht gefunden wurde |
| _TEL_ANTWORT | binary | STATUS_GET_CONFIG_DETAIL erfolgreich |

<a id="job-steuern-start-net-config"></a>
### STEUERN_START_NET_CONFIG

Einlesen der Konfiguration über das Netzwerk

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| URL | string | Name der Netzwerkfreigabe Format: username=xx,password=xx,workgroup=xx //ServerIP oder Servername/Freigabename/Dateiname workgroup (Domäne des Users) ist optional |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_CONFIG_ERROR | string | Fehlerinfo bei ICOMP_START_NET_CONFIG |
| _TEL_ANTWORT | binary | ICOMP_START_NET_CONFIG erfolgreich |

<a id="job-steuern-update"></a>
### STEUERN_UPDATE

Softwareupdate des ICOM-P über das Netzwerk

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NAME | string | Name der Updatedatei mit der Netzwerkfreigabe Format: username=xx,password=xx,workgroup=xx //ServerIP oder Servername/Freigabename/Dateiname workgroup (Domäne des Users) ist optional |
| FORCE | string | Erzwingt das Update (mögliche Werte "F" oder "1") Versionsinformationen werden ignoriert (für Updates von Stand auf Stand) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | ICOMP_UPDATE erfolgreich |

<a id="job-status-get-iwconfig"></a>
### STATUS_GET_IWCONFIG

Führt ein iwconfig auf dem ICOM aus und liefert dessen Ergebnisse. Es wird eine variable Liste von Ergebnissen erzeugt.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_ICOMP_WIRELESS_NOT_ACTIVE, WLAN nicht activiert" ERROR_ICOMP_IWCONFIG_FAILED, Fehler beim Ausführen von iwconfig" |

<a id="job-steuern-manual-roaming"></a>
### STEUERN_MANUAL_ROAMING

Erzwingen eines WLAN-Roaming vorganges

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | STEUERN_MANUAL_ROAMING erfolgreich |

<a id="job-steuern-traceon"></a>
### STEUERN_TRACEON

ICOM CAN/HSFZ Trace einschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | TraceOn erfolgreich |

<a id="job-steuern-traceoff"></a>
### STEUERN_TRACEOFF

Abschalten CAN/HSFZ Trace

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | TraceOff erfolgreich |

<a id="job-status-trace-state"></a>
### STATUS_TRACE_STATE

Lesen von Trace Informationen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort vom ICOM |
| STAT_TRACE | string | Trace aktiv oder inaktiv |
| STAT_TRACE_MEMORY_DCAN | unsigned long | Freier DCAN Trace-Speicher in kB |
| STAT_USED_MEMORY_DCAN | unsigned long | Momentan verwendeter DCAN Trace-Speicher in kB |
| STAT_TRACE_MEMORY_ETH | unsigned long | Freier ETH Trace-Speicher in kB |
| STAT_USED_MEMORY_ETH | unsigned long | Momentan verwendeter ETH Trace-Speicher in kB |

<a id="job-steuern-trace-boot-enable"></a>
### STEUERN_TRACE_BOOT_ENABLE

Automatisches tracen nach Neustart des ICOMs

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ENABLE_TRACE | string | "ON"   = einschalten "OFF"  = ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Trace On/Off |

<a id="job-status-trace-get-config"></a>
### STATUS_TRACE_GET_CONFIG

Lesen der Trace-Konfiguration

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort vom ICOM |
| STAT_TRACE | string | Trace aktiviert |
| STAT_DCAN_TRACE | string | D-CAN Trace aktiviert/deaktiviert |
| STAT_KL15EW_TRACE | string | KL15 Trace aktiviert/deaktiviert |
| STAT_ETHERNET_TRACE | string | ETHERNET Trace aktiviert/deaktiviert |
| STAT_UDP_LOGGING | string | UDP Logging aktiviert/deaktiviert |
| STAT_IFHENET_LOGGING | string | IFHENET Logging aktiviert/deaktiviert |
| STAT_ARP_LOGGING | string | ARP Logging aktiviert/deaktiviert |
| STAT_LS_LOGGING | string | Link Status Logging aktiviert/deaktiviert |
| STAT_WLANPING_LOGGING | string | Wlan Ping Logging aktiviert/deaktiviert |
| STAT_TARGET | string | Ablageziel der Tracedateien |
| STAT_FILENAMEBASE | string | Variable Basis des Dateinames der Tracedateien |
| STAT_REMOTEURL | string | URL-Freigabe für die Ablage der Tracedaten (remote/offline) |
| STAT_DCAN_SIZE | string | Größe des Buffers für den D-CAN Trace |
| STAT_ENET_SIZE | string | Größe des Buffers für den ETHERNET Trace |

<a id="job-steuern-dcan-trace"></a>
### STEUERN_DCAN_TRACE

D-CAN Trace einschalten/ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DCAN_TRACE | string | "ON"   = einschalten "OFF"  = ausschalten |
| DCAN_PERSISTENT | string | "P"   = persistent speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | DCAN Trace On/Off |

<a id="job-steuern-kl15-trace"></a>
### STEUERN_KL15_TRACE

KL15 (0x130) Trace einschalten/ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KL15_TRACE | string | "ON"   = einschalten "OFF"  = ausschalten |
| KL15_PERSISTENT | string | "P"   = persistent speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | KL15 Trace On/Off |

<a id="job-steuern-ethernet-trace"></a>
### STEUERN_ETHERNET_TRACE

ETHERNET Trace einschalten/ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ETHERNET_TRACE | string | "OFF"  = Ethernet Trace ausschalten "VehicleSide"  = ETHERNET Trace für Fahrzeugseite (HSFZ) einschalten "FactorySide"  = ETHERNET Trace für Werksseite (WLAN/LAN) einschalten "BothSides"    = ETHERNET Trace für beide Seiten einschalten |
| ETHERNET_PERSISTENT | string | "P"   = persistent speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | ETHERNET Trace On/Off |

<a id="job-steuern-udp-trace"></a>
### STEUERN_UDP_TRACE

UDP Logging einschalten/ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| UDP_TRACE | string | "ON"   = einschalten "OFF"  = ausschalten |
| UDP_PERSISTENT | string | "P"   = persistent speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | UDP Logging On/Off |

<a id="job-steuern-arp-trace"></a>
### STEUERN_ARP_TRACE

ARP Logging einschalten/ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARP_TRACE | string | "ON"   = einschalten "OFF"  = ausschalten |
| ARP_PERSISTENT | string | "P"   = persistent speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | ARP Logging On/Off |

<a id="job-steuern-ls-trace"></a>
### STEUERN_LS_TRACE

Link Status Logging einschalten/ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LS_TRACE | string | "ON"   = einschalten "OFF"  = ausschalten |
| LS_PERSISTENT | string | "P"   = persistent speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Link Status Logging On/Off |

<a id="job-steuern-wlanping-trace"></a>
### STEUERN_WLANPING_TRACE

Link Status Logging einschalten/ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WLANPING_TRACE | string | "ON"   = einschalten "OFF"  = ausschalten |
| WLANPING_PERSISTENT | string | "P"   = persistent speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Link Status Logging On/Off |

<a id="job-steuern-ifhenet-trace"></a>
### STEUERN_IFHENET_TRACE

IFH ETHERNET Logging einschalten/ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IFHENET_TRACE | string | "ON"   = einschalten "OFF"  = ausschalten |
| IFHENET_PERSISTENT | string | "P"   = persistent speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | IFHENET Logging On/Off |

<a id="job-steuern-trace-target"></a>
### STEUERN_TRACE_TARGET

Ablageziel der Tracedateien festlegen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TARGET | string | "RAM"     = in den RAM (/tmp --&gt; nur temporär) "MassInt" = auf den internen Massenspeicher "MassExt" = auf einen externen Massenspeicher (z.B. USB-Stick) "Remote"  = auf eine Netzwerkfreigabe |
| TARGET_PERSISTENT | string | "P"   = persistent speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Ablageziel gesetzt |

<a id="job-steuern-trace-filenamebase"></a>
### STEUERN_TRACE_FILENAMEBASE

Variable Basis des Dateinames der Tracedateien setzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FILENAMEBASE | string | &lt;variable Basis&gt; des Dateinames der Tracedateien &lt;VIN/DATE&gt;.&lt;variable Basis&gt;.&lt;SerNumICOM&gt;.&lt;NUM&gt;.&lt;LOG/PCAP&gt; |
| FNB_PERSISTENT | string | "P"   = persistent speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Filenamebase gesetzt |

<a id="job-steuern-trace-remoteurl"></a>
### STEUERN_TRACE_REMOTEURL

URL-Freigabe für die Ablage der Tracedaten (remote/offline)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REMOTEURL | string | Name der Netzwerkfreigabe Format: username=xx,password=xx,workgroup=xx //ServerIP oder Servername/Freigabename workgroup (Domäne des Users) ist optional |
| URL_PERSISTENT | string | "P"   = persistent speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | RemoteURL gesetzt |

<a id="job-steuern-trace-dcansize"></a>
### STEUERN_TRACE_DCANSIZE

Maximale Grösse der D-CAN Tracedateien auf dem ICOM setzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DCANSIZE | string | Maximale Grösse in Bytes / Prozent (des Gesamtspeichers) |
| DS_PERSISTENT | string | "P"   = persistent speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | D-CAN Tracegrösse gesetzt |

<a id="job-steuern-trace-ethernetsize"></a>
### STEUERN_TRACE_ETHERNETSIZE

Maximale Grösse der ETHERNET Tracedateien auf dem ICOM setzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ETHERNETSIZE | string | Maximale Gösse in Bytes oder Prozent (des Gesamtspeichers) Beispiele: |
| ES_PERSISTENT | string | "P"   = persistent speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | ETHERNET Tracegrösse gesetzt |

<a id="job-steuern-trace-retrieve"></a>
### STEUERN_TRACE_RETRIEVE

Tracedatei vom ICOM auf REMOTEURL übertragen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NAME | string | Name der Tracedatei auf REMOTEURL |
| FILTER | string | Name der Tracedatei(en), die abgeholt werden |
| RESTART | int | 0   = Trace nach dem Abholen nicht neu starten 1   = Trace nach dem Abholen neu starten |
| PACKED | int | 0   = Tracedatei nicht packen 1   = Tracedatei packen |
| ASYNCHRON | int | gültig nur bei ICOMP Next 0   = Warten, bis Trace komplett abgeholt (Default) 1   = Befehl kehrt nach dem mounten des shares zurück |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Abholen des Trace gestartet |

<a id="job-steuern-trace-retrieve-all"></a>
### STEUERN_TRACE_RETRIEVE_ALL

gesamte Tracedaten vom ICOM auf REMOTEURL übertragen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NAME | string | Name der Tracedatei auf REMOTEURL |
| RESTART | int | 0   = Trace nach dem Abholen nicht neu starten 1   = Trace nach dem Abholen neu starten |
| PACKED | int | 0   = Tracedatei nicht packen 1   = Tracedatei packen |
| ASYNCHRON | int | gültig nur bei ICOMP Next 0   = Warten, bis Trace komplett abgeholt (Default) 1   = Befehl kehrt nach dem mounten des shares zurück |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Abholen des Trace gestartet |

<a id="job-steuern-trace-erase"></a>
### STEUERN_TRACE_ERASE

Löschen aller Tracefiles auf dem ICOM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ERASE_TYPE | string | "CAN"  = D-CAN Trace löschen "ETH"  = ETHERNET Trace löschen "BOTH" = D-CAN und ETHERNET Trace löschen (default) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort vom ICOM |

<a id="job-steuern-debugmode"></a>
### STEUERN_DEBUGMODE

ICOM DEBUGMODE einschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| OPTIONS | string | "S"  = zusätzliche Logs für den Startvorgang einschalten "K"  = zusätzliche Logs für die Kommunikation einschalten "P"  = Debugmode für 24 Stunden persistent einschalten "W"  = zusätzliche Logs für WLAN, gültig nur bei ICOMP Next "L"  = Lightmodus, gültig nur bei ICOMP Next  "DISABLE"  = Debugmode ausschalten (keine Zusatzoptionen möglich) |
| LEVEL | unsigned long | Optional: Debuglevel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | STEUERN_DEBUGMODE erfolgreich |

<a id="job-steuern-debugmode-getfiles"></a>
### STEUERN_DEBUGMODE_GETFILES

Auslesen der Debugmode Dateien über das Netzwerk

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NAME | string | Name der Netzwerkfreigabe Format: username=xx,password=xx,workgroup=xx //ServerIP oder Servername/Freigabename workgroup (Domäne des Users) ist optional |
| REBOOT | int | 0   = ICOM nach dem Abholen der Files nicht neu starten (default) 1   = ICOM nach dem Abholen der Files neu starten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | STEUERN_DEBUGMODE_GETFILES erfolgreich |

<a id="job-steuern-debugmode-erasefiles"></a>
### STEUERN_DEBUGMODE_ERASEFILES

Löschen der Debugmode Dateien auf der SD Karte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | STEUERN_DEBUGMODE_ERASEFILES erfolgreich |

<a id="job-steuern-reboot"></a>
### STEUERN_REBOOT

Neustart des ICOM_P

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | STEUERN_REBOOT erfolgreich |

<a id="job-steuern-switch-off"></a>
### STEUERN_SWITCH_OFF

Ausschalten des ICOM_P

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TIME | unsigned long | Zeit in ms, die bis zum Ausschalten gewartet wird |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | STEUERN_SWITCH_OFF erfolgreich |

<a id="job-steuern-constant-current"></a>
### STEUERN_CONSTANT_CURRENT

Ein/Ausschalten des Konstantstrommodus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CCMODE | string | "ON"   = Konstantstrommodus einschalten "OFF"  = Konstantstrommodus ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | ICOMP_CONSTANT_CURRENT_SET erfolgreich |

<a id="job-status-constant-current"></a>
### STATUS_CONSTANT_CURRENT

Zustand des Konstantstrommodus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CONSTANT_CURRENT | string | ON = CONSTANT CURRENT MODE aktiv OFF= CONSTANT CURRENT MODE inaktiv |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | ICOMP_CONSTANT_CURRENT_GET erfolgreich |

<a id="job-steuern-send-wake-up"></a>
### STEUERN_SEND_WAKE_UP

Senden eine WakeUp-Pulses auf OBD Pin 8 (HSFZ-Aktivierungsleitung) Unterstützung des Fahrzeuges vorausgesetzt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DELAY_TIME | string | Wartezeit bis zur steigenden Flanke (wake_up) in ms(Default= 1000ms) Falls HSFZ_ACTIVATE nicht angegeben wird, kann hier durch angeben von ON oder OFF die HSFZ Aktivierung mit der Default-Zeit gesteuert werden. |
| HSFZ_ACTIVATE | string | ON =HSFZ aktivieren nach Wake_Up (Default) OFF=HSFZ deaktivieren nach Wake_Up |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | OKAY |

<a id="job-steuern-on-set-can-id"></a>
### STEUERN_ON_SET_CAN_ID

Einschalten des ICOM_P durch ein bestimmtes CAN Telegramm

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ENABLE | string | ON = Einschalten der Aufweckfunktion OFF = Ausschalten der Aufweckfunktion Die überwachte CAN-Botschaft wird durch eine Mask und einen Code beschrieben Hier definiert Mask die Positonen der relevanten Bits in der Id bzw. den Nutzdaten Eine 1 bedeutet das Bit ist relevant, eine 0 das Bit ist irrelevant Code beschreibt den Zustand der relevanten Bits Als Beispiel würde bei einer Mask von 0x7ff und einem Code von 0x130 für den CAN-Identifier nur auf den Frame 0x130 reagiert. Ändert man die Mask auf 0x7f0 würde auf den Identifier- Bereich 0x130-013f reagiert. |
| CANID_MASK | unsigned long | Mask des CAN Identifieres vom Aufwecktelegramms als Dezimal- oder Hexadezimalwert z.B.: 2047 oder 0x7ff |
| CANID_CODE | unsigned long | Code des CAN Identifieres vom Aufwecktelegramm als Dezimal- oder Hexadezimalwert z.B. 304 oder 0x130 |
| CANDATA_MASK | string | Mask der CAN Daten des Aufwecktelegramms als Hexdezimalstring z.B.: FFFF   : nur die 1. beiden Bytes sind relevant 0000FF : nur das 3. Byte ist relevant F0     : nur das obere Nibble im 1. Byte ist relevant |
| CANDATA_CODE | string | Code der CAN Daten des Aufwecktelegramms als Hexdezimalstring z.B.: (bezogen auf die als Bespiel bei CANDATA_MASK genannten Werte) 0123   : in den 1. beiden Bytes muß 0123 stehen 000045 : im 3. Byte muß 45 stehen 60     : im 1. Byte muß ein Wert zwischen 60 und 6F stehen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | STEUERN_ON_SET_CAN_ID erfolgreich |

<a id="job-steuern-set-can-idle-time"></a>
### STEUERN_SET_CAN_IDLE_TIME

Ausschalten des ICOM_P wenn keine CAN Kommunikation vorhanden ist

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| T_IDLE | unsigned long | 0 = CAN Idle-Überwachung aus &gt;0 = CAN Idle-Überwachung ein (Zeit in Sekunden, mindestens 60) Das ICOM_P schläft ein, wenn CAN Kommunikation erkannt worden ist und diese dann für eine Zeit &gt; T_Idle ausbleibt |
| T_SHUTDOWN | unsigned long | Zeit in Sekunden, nach der das ICOM_P einschläft, wenn keine CAN Kommunikation erkannt worden ist T_SHUTDOWN muss grösser T_IDLE sein |
| CHECK_CAN_FRAME | string | ON = CAN-Botschaft wird überwacht OFF = CAN-Botschaft wird nicht überwacht Die überwachte CAN-Botschaft wird durch eine Mask und einen Code beschrieben Hier definiert Mask die Positonen der relevanten Bits in der Id bzw. den Nutzdaten Eine 1 bedeutet das Bit ist relevant, eine 0 das Bit ist irrelevant Code beschreibt den Zustand der relevanten Bits Als Beispiel würde bei einer Mask von 0x7ff und einem Code von 0x130 für den CAN-Identifier nur auf den Frame 0x130 reagiert. Ändert man die Mask auf 0x7f0 würde auf den Identifier- Bereich 0x130-013f reagiert. |
| CANID_MASK | unsigned long | Mask des CAN-Identifieres des zu überwachenden Telegramms als Dezimal- oder Hexadezimalwert z.B.: 2047 oder 0x7ff |
| CANID_CODE | unsigned long | Code des CAN-Identifieres des zu überwachenden Telegramms als Dezimal- oder Hexadezimalwert z.B. 304 oder 0x130 |
| CANDATA_MASK | string | Mask der CAN-Daten des zu überwachenden Telegramms als Hexdezimalstring z.B.: FFFF   : nur die 1. beiden Bytes sind relevant 0000FF : nur das 3. Byte ist relevant F0     : nur das obere Nibble im 1. Byte ist relevant |
| CANDATA_CODE | string | Code der CAN-Daten des zu überwachenden Telegramms als Hexdezimalstring z.B.: (bezogen auf die als Bespiel bei CANDATA_MASK genannten Werte) 0123   : in den 1. beiden Bytes muß 0123 stehen 000045 : im 3. Byte muß 45 stehen 60     : im 1. Byte muß ein Wert zwischen 60 und 6F stehen |
| NON_PERSISTENT | string | "N"   = nicht persistent speichern, gültig nur bei ICOMP Next |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | STEUERN_SET_CAN_IDLE_TIME erfolgreich |

<a id="job-steuern-enable-acc-wakeup"></a>
### STEUERN_ENABLE_ACC_WAKEUP

Einschalten des ICOM_P durch den Bewegungssensor

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ENABLE | string | ON = ICOM_P kann durch den Bewegungssenor aufgeweckt werden OFF = ICOM_P kann nicht durch den Bewegungssenor aufgeweckt werden |
| SENSIBILITY | int | 1..255 = Empfindlichkeit des Bewegungssenors |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | STEUERN_ENABLE_ACC_WAKEUP erfolgreich |

<a id="job-steuern-wakeup-timer"></a>
### STEUERN_WAKEUP_TIMER

Setzt die Zeit nach der das ICOMP Next wieder erwacht

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TIME | string | Zeit in s, nach der das ICOMP Next wieder erwacht,0 schaltet das zeitgesteuerte Aufwachen aus |
| PERSISTENT | string | (Optional) P = ICOM-P Next wacht immer wieder auf nicht vorhanden oder N = zeitgesteuertes Aufwachen wird nur einmal ausgeführt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | OKAY |

<a id="job-steuern-fehlerspeicher-lesen"></a>
### STEUERN_FEHLERSPEICHER_LESEN

Auslesen des Fehlerspeichers des ICOMs

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| OPTIONS | string | S = Zeigt zusätzlich die Softrebootaufrufzeiten an |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| UPTIME | string | Zeit in Sekunden, die seit dem Booten vergangen ist |
| HARDREBOOT | string | Anzahl der Hardreboots |
| SOFTREBOOT | string | Anzahl der Softreboots |
| SOFTREBOOTIME | string | Aufrufzeiten der Softreboots |
| BATTERY | string | Die Batterie muß gewechselt werden |
| FEHLERORT | string | Art des Fehlers |
| FEHLERTEXT | string | Beschreibung des Fehlers |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | STEUERN_FEHLERSPEICHER_LESEN erfolgreich |

<a id="job-steuern-fehlerspeicher-loeschen"></a>
### STEUERN_FEHLERSPEICHER_LOESCHEN

Löscht den Fehlerspeichers des ICOMs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | STEUERN_FEHLERSPEICHER_LOESCHEN erfolgreich |

<a id="job-steuern-wake-on-ex-trigger"></a>
### STEUERN_WAKE_ON_EX_TRIGGER

gültig nur bei ICOMP Next mit Funkmodul Wakeup über Funkmodul Ein- Ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| OPTIONS | string | ON =Lauschen auf externen Trigger ein OFF=Lauschen auf externen Trigger aus |
| MODE | string | V =Überprüfen auf VIN (Default) I =Überprüfen auf IP B =Aufwachen bei Broadcast |
| PERSISTENT | string | (Optional) P = Einstellung bleibt nach Neustart erhalten nicht vorhanden oder N = Einstellung wird nur einmal ausgeführt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,          Werte konnten gesetzt werden ERROR_FAILED,  Werte konnten nicht gesetzt werden NO_RADIO,      Kein Funkmodul verbaut |
| _TEL_ANTWORT | binary | OKAY |

<a id="job-steuern-wake-on-ex-trigger-freq"></a>
### STEUERN_WAKE_ON_EX_TRIGGER_FREQ

gültig nur bei ICOMP Next mit Funkmodul Benutzte Frequenz des Funkmoduls

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREQUENCE | int | 1 =433,139 Mhz 2 =433,439 Mhz 3 =433,739 Mhz 4 =434,038 Mhz 5 =434,339 Mhz 6 =434,639 Mhz |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,          Werte konnten gesetzt werden ERROR_FAILED,  Werte konnten nicht gesetzt werden NO_RADIO,      Kein Funkmodul verbaut |
| _TEL_ANTWORT | binary | OKAY |

<a id="job-steuern-send-ex-trigger"></a>
### STEUERN_SEND_EX_TRIGGER

gültig nur bei ICOMP Next mit Funkmodul Senden eines Aufweckkommandos

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TIMEOUT | int | Zeit in ms, die auf die Bestätigung gewartet wird |
| REPEAT | int | Anzahl der Wiederholungen, wenn keine Bestätigung empfangen wird |
| PING | int | Anzahl der Netzwerk Pings, die gesendet werden sollen, wenn kein Ack ankommt |
| FREQUENCE | int | Benutzte Frequenz für das Aufweckkommando 1 =433,139 Mhz 2 =433,439 Mhz 3 =433,739 Mhz 4 =434,038 Mhz 5 =434,339 Mhz 6 =434,639 Mhz |
| PATH | string | Verzeichnis, in dem die Übergabedatei liegt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,          Werte konnten gesetzt werden ERROR_FAILED,  Werte konnten nicht gesetzt werden NO_RADIO,      Kein Funkmodul verbaut |
| _TEL_ANTWORT | binary | OKAY |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (149 × 2)
- [FARTTEXTE](#table-farttexte) (35 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (9 × 9)
- [TAB_ZEIT_SYNCMETHOD](#table-tab-zeit-syncmethod) (4 × 2)
- [TAB_ZEIT_USER_INFO](#table-tab-zeit-user-info) (8 × 2)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [CU_ERR_TEXT](#table-cu-err-text) (7 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (1 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (1 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 4)
- [IUMWELTTEXTE](#table-iumwelttexte) (1 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 76 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x10 | ERROR_ECU_GENERAL_REJECT |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUB_FUNCTION_NOT_SUPPORTED |
| 0x13 | ERROR_ECU_INCORRECT_MESSAGE_LENGTH_OR_INVALID_FORMAT |
| 0x14 | ERROR_ECU_RESPONSE_TOO_LONG |
| 0x21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT |
| 0x24 | ERROR_ECU_REQUEST_SEQUENCE_ERROR |
| 0x25 | ERROR_ECU_NO_RESPONSE_FROM_SUBNET_COMPONENT |
| 0x26 | ERROR_ECU_FAILURE_PREVENTS_EXECUTION_OF_REQUESTED_ACTION |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x33 | ERROR_ECU_SECURITY_ACCESS_DENIED |
| 0x35 | ERROR_ECU_INVALID_KEY |
| 0x36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0x37 | ERROR_ECU_REQUIRED_TIME_DELAY_NOT_EXPIRED |
| 0x70 | ERROR_ECU_UPLOAD_DOWNLOAD_NOT_ACCEPTED |
| 0x71 | ERROR_ECU_TRANSFER_DATA_SUSPENDED |
| 0x72 | ERROR_ECU_GENERAL_PROGRAMMING_FAILURE |
| 0x73 | ERROR_ECU_WRONG_BLOCK_SEQUENCE_COUNTER |
| 0x78 | ERROR_ECU_REQUEST_CORRECTLY_RECEIVED__RESPONSE_PENDING |
| 0x7E | ERROR_ECU_SUB_FUNCTION_NOT_SUPPORTED_IN_ACTIVE_SESSION |
| 0x7F | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_SESSION |
| 0x81 | ERROR_ECU_RPM_TOO_HIGH |
| 0x82 | ERROR_ECU_RPM_TOO_LOW |
| 0x83 | ERROR_ECU_ENGINE_IS_RUNNING |
| 0x84 | ERROR_ECU_ENGINE_IS_NOT_RUNNING |
| 0x85 | ERROR_ECU_ENGINE_RUN_TIME_TOO_LOW |
| 0x86 | ERROR_ECU_TEMPERATURE_TOO_HIGH |
| 0x87 | ERROR_ECU_TEMPERATURE_TOO_LOW |
| 0x88 | ERROR_ECU_VEHICLE_SPEED_TOO_HIGH |
| 0x89 | ERROR_ECU_VEHICLE_SPEED_TOO_LOW |
| 0x8A | ERROR_ECU_THROTTLE_PEDAL_TOO_HIGH |
| 0x8B | ERROR_ECU_THROTTLE_PEDAL_TOO_LOW |
| 0x8C | ERROR_ECU_TRANSMISSION_RANGE_NOT_IN_NEUTRAL |
| 0x8D | ERROR_ECU_TRANSMISSION_RANGE_NOT_IN_GEAR |
| 0x8F | ERROR_ECU_BRAKE_SWITCH_NOT_CLOSED |
| 0x90 | ERROR_ECU_SHIFTER_LEVER_NOT_IN_PARK |
| 0x91 | ERROR_ECU_TORQUE_CONVERTER_CLUTCH_LOCKED |
| 0x92 | ERROR_ECU_VOLTAGE_TOO_HIGH |
| 0x93 | ERROR_ECU_VOLTAGE_TOO_LOW |
| ?00? | OKAY |
| ?01? | ERROR_ECU_NO_RESPONSE |
| ?02? | ERROR_ECU_INCORRECT_LEN |
| ?03? | ERROR_ECU_INCORRECT_RESPONSE_ID |
| ?04? | ERROR_ECU_TA_RESPONSE_NOT_SA_REQUEST |
| ?05? | ERROR_ECU_SA_RESPONSE_NOT_TA_REQUEST |
| ?06? | ERROR_ECU_RESPONSE_INCORRECT_DATA_IDENTIFIER |
| ?07? | ERROR_ECU_RESPONSE_TOO_MUCH_DATA |
| ?08? | ERROR_ECU_RESPONSE_TOO_LESS_DATA |
| ?09? | ERROR_ECU_RESPONSE_VALUE_OUT_OF_RANGE |
| ?0A? | ERROR_TABLE |
| ?10? | ERROR_F_CODE |
| ?12? | ERROR_INTERPRETATION |
| ?13? | ERROR_F_POS |
| ?14? | ERROR_ECU_RESPONSE_INCORRECT_IO_CONTROL_PARAMETER |
| ?15? | ERROR_ECU_RESPONSE_INCORRECT_ROUTINE_CONTROL_TYPE |
| ?16? | ERROR_ECU_RESPONSE_INCORRECT_SUB_FUNCTION |
| ?17? | ERROR_ECU_RESPONSE_INCORRECT_DYNAMICALLY_DEFINED_DATA_IDENTIFIER |
| ?18? | ERROR_ECU_RESPONSE_NO_STRING_END_CHAR |
| ?19? | ERROR_ECU_RESPONSE_INCORRECT_ROUTINE_IDENTIFIER |
| ?1A? | ERROR_ECU_RESPONSE_INCORRECT_RESET_TYPE |
| ?1B? | ERROR_ECU_RESPONSE_INCORRECT_SERIAL_NUMBER_FORMAT |
| ?1C? | ERROR_ECU_RESPONSE_INCORRECT_DTC_BY_STATUS_MASK |
| ?1D? | ERROR_ECU_RESPONSE_INCORRECT_DTC_STATUS_AVAILABILITY_MASK |
| ?1E? | ERROR_ECU_RESPONSE_INCORRECT_ROUTINE_CONTROL_IDENTIFIER |
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?60? | ERROR_VERIFY |
| ?61? | ERROR_ECU_RESPONSE_ZGW |
| ?62? | ERROR_ECU_RESPONSE_BACKUP |
| ?70? | ERROR_CALID_CVN_INCORRECT_LEN |
| ?80? | ERROR_SVK_INCORRECT_LEN |
| ?81? | ERROR_SVK_INCORRECT_FINGERPRINT |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 149 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x000001 | Reinshagen / Delphi |
| 0x000002 | Leopold Kostal GmbH & Co. KG |
| 0x000003 | Hella Fahrzeugkomponenten GmbH |
| 0x000004 | Siemens |
| 0x000005 | Eaton |
| 0x000006 | UTA |
| 0x000007 | Helbako GmbH |
| 0x000008 | Robert Bosch GmbH |
| 0x000009 | Lear Corporation |
| 0x000010 | VDO |
| 0x000011 | Valeo GmbH |
| 0x000012 | MBB |
| 0x000013 | Kammerer |
| 0x000014 | SWF |
| 0x000015 | Blaupunkt |
| 0x000016 | Philips |
| 0x000017 | Alpine Electronics GmbH |
| 0x000018 | Continental Teves AG & Co. OHG |
| 0x000019 | Elektromatik Südafrika |
| 0x000020 | Harman Becker Automotive Systems |
| 0x000021 | Preh GmbH |
| 0x000022 | Alps Electric Co. Ltd. |
| 0x000023 | Motorola |
| 0x000024 | Temic |
| 0x000025 | Webasto SE |
| 0x000026 | MotoMeter |
| 0x000027 | Delphi Automotive PLC |
| 0x000028 | DODUCO (Beru) |
| 0x000029 | DENSO |
| 0x000030 | NEC |
| 0x000031 | DASA |
| 0x000032 | Pioneer Corporation |
| 0x000033 | Jatco |
| 0x000034 | FUBA Automotive GmbH & Co. KG |
| 0x000035 | UK-NSI |
| 0x000036 | AABG |
| 0x000037 | Dunlop |
| 0x000038 | Sachs |
| 0x000039 | ITT |
| 0x000040 | FTE (Fahrzeugtechnik Ebern) |
| 0x000041 | Megamos |
| 0x000042 | TRW Automotive GmbH |
| 0x000043 | WABCO Fahrzeugsysteme GmbH |
| 0x000044 | ISAD Electronic Systems |
| 0x000045 | HEC Hella Electronics Corporation |
| 0x000046 | Gemel |
| 0x000047 | ZF Friedrichshafen AG |
| 0x000048 | GMPT |
| 0x000049 | Harman Becker Automotive Systems GmbH |
| 0x000050 | Remes GmbH |
| 0x000051 | ZF Lenksysteme GmbH |
| 0x000052 | Magneti Marelli S.p.A. |
| 0x000053 | Johnson Controls Inc. |
| 0x000054 | GETRAG Getriebe- und Zahnradf. Hermann Hagenmeyer GmbH & Co. KG |
| 0x000055 | Behr-Hella Thermocontrol GmbH |
| 0x000056 | Siemens VDO Automotive |
| 0x000057 | Visteon Innovation & Technology GmbH |
| 0x000058 | Autoliv AB |
| 0x000059 | Haberl Electronic GmbH & Co. KG |
| 0x000060 | Magna International Inc. |
| 0x000061 | Marquardt GmbH |
| 0x000062 | AB Elektronik GmbH |
| 0x000063 | SDVO/BORG |
| 0x000064 | Hirschmann Car Communication GmbH |
| 0x000065 | hoerbiger-electronics |
| 0x000066 | Thyssen Krupp Automotive |
| 0x000067 | Gentex Corporation |
| 0x000068 | Atena GmbH |
| 0x000069 | Magna-Donelly |
| 0x000070 | Koyo Steeting Europe |
| 0x000071 | NSI Beheer B.V. |
| 0x000072 | Aisin AW Co. Ltd. |
| 0x000073 | Schorlock |
| 0x000074 | Schrader Electronics Ltd. |
| 0x000075 | Huf-Electronics Bretten GmbH |
| 0x000076 | CEL |
| 0x000077 | AUDIO MOBIL Elektronik GmbH |
| 0x000078 | rd electronic |
| 0x000079 | iSYS RTS GmbH |
| 0x000080 | Westfalia-Automotive GmbH |
| 0x000081 | Tyco Electronics |
| 0x000082 | Paragon AG |
| 0x000083 | IEE S.A. |
| 0x000084 | TEMIC AUTOMOTIVE of NA |
| 0x000085 | Sonceboz S.A. |
| 0x000086 | Meta System S.p.A. |
| 0x000087 | Huf Hülsbeck & Fürst GmbH & Co. KG |
| 0x000088 | MANN+HUMMEL GmbH |
| 0x000089 | Brose Fahrzeugteile GmbH & Co. |
| 0x000090 | Keihin |
| 0x000091 | Vimercati S.p.a |
| 0x000092 | CRH |
| 0x000093 | TPO Display Corp |
| 0x000094 | Küster Automotive GmbH |
| 0x000095 | Hitachi Automotive |
| 0x000096 | Continental AG |
| 0x000097 | TI-Automotive |
| 0x000098 | Hydro |
| 0x000099 | Johnson Controls Inc. |
| 0x00009A | Takata-Petri |
| 0x00009B | Mitsubishi Electric B.V. (Melco) |
| 0x00009C | Autokabel |
| 0x00009D | GKN Plc |
| 0x00009E | Zollner Elektronik AG |
| 0x00009F | peiker acustic GmbH & Co. KG |
| 0x0000A0 | Bosal-Oris |
| 0x0000A1 | Cobasys |
| 0x0000A2 | Automotive Lighting Reutlingen GmbH |
| 0x0000A3 | CONTI VDO |
| 0x0000A4 | A.D.C. Automotive Distance Control Systems GmbH |
| 0x0000A5 | Novero Dabendorf GmbH |
| 0x0000A6 | LAMES S.p.a. |
| 0x0000A7 | Magna/Closures |
| 0x0000A8 | Harbin Wan Yu Technology Co |
| 0x0000A9 | ThyssenKrupp Presta AG |
| 0x0000AA | ArvinMeritor |
| 0x0000AB | Kongsberg Automotive GmbH |
| 0x0000AC | SMR Automotive Mirrors Stuttgart GmbH |
| 0x0000AD | So.Ge.Mi. |
| 0x0000AE | MTA S.p.A. |
| 0x0000AF | Alfmeier Präzision AG |
| 0x0000B0 | Eltek Deutechland GmbH |
| 0x0000B1 | OMRON Automotive Electronics Europe GmbH |
| 0x0000B2 | ASK Industries GmbH |
| 0x0000B3 | CML Innovative Technologies GmbH & Co. KG |
| 0x0000B4 | APAG Elektronik AG |
| 0x0000B5 | Nexteer Automotive |
| 0x0000B6 | Hans Widmaier Fernmelde- und Feinwerktechnik |
| 0x0000B7 | Robert Bosch Battery Systems GmbH |
| 0x0000B8 | Kyocera Display Europe GmbH |
| 0x0000B9 | Magna Powertrain AG & Co. KG |
| 0x0000BA | BorgWarner Beru Systems GmbH |
| 0x0000BB | BMW AG |
| 0x0000BC | Benteler Duncan Plant |
| 0x0000BD | U-Shin Deutschland Zugangssysteme GmbH |
| 0x0000BE | Schaeffler Technologies AG & Co. KG |
| 0x0000BF | JTEKT Corporation |
| 0x0000C0 | VLF |
| 0x0000C1 | Flextronics |
| 0x0000C2 | LG Chem |
| 0x0000C3 | Panasonic |
| 0x0000C4 | Alpitronic GmbH |
| 0x0000C5 | Telemotive AG |
| 0x0000C6 | Garmin |
| 0x0000C7 | RSG Elotech Elektronische Baugruppen GmbH |
| 0x0000C8 | KEBODA TECHNOLOGY CORP |
| 0x0000C9 | Aptiv |
| 0x0000CA | SEG Automotive Germany GmbH |
| 0xFFFFFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 35 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler momentan vorhanden und bereits gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler momentan vorhanden und bereits gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler momentan vorhanden und bereits gespeichert |
| 0x20 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x21 | Fehler momentan vorhanden und bereits gespeichert |
| 0x24 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x25 | Fehler momentan vorhanden und bereits gespeichert |
| 0x28 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x29 | Fehler momentan vorhanden und bereits gespeichert |
| 0x2C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x2D | Fehler momentan vorhanden und bereits gespeichert |
| 0x40 | unbekannte Fehlerart |
| 0x44 | Fehler gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler gespeichert |
| 0x4D | Fehler gespeichert |
| 0x60 | Fehler gespeichert |
| 0x61 | Fehler gespeichert |
| 0x64 | Fehler gespeichert |
| 0x65 | Fehler gespeichert |
| 0x68 | Fehler gespeichert |
| 0x69 | Fehler gespeichert |
| 0x6C | Fehler gespeichert |
| 0x6D | Fehler gespeichert |
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x80 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x81 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 17 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
| an | 1 |
| yes | 1 |
| no | 0 |
| on | 1 |
| off | 0 |
| up | 1 |
| down | 0 |
| true | 1 |
| false | 0 |
| 1 | 1 |
| 0 | 0 |

<a id="table-prozessklassen"></a>
### PROZESSKLASSEN

Dimensions: 26 rows × 3 columns

| WERT | PROZESSKLASSE | BEZEICHNUNG |
| --- | --- | --- |
| 0x00 | - | ungueltig |
| 0x01 | HWEL | Hardware (Elektronik) |
| 0x02 | HWAP | Hardwareauspraegung |
| 0x03 | HWFR | Hardwarefarbe |
| 0x05 | CAFD | Codierdaten |
| 0x06 | BTLD | Bootloader |
| 0x08 | SWFL | Software ECU Speicherimage |
| 0x09 | SWFF | Flash File Software |
| 0x0A | SWPF | Pruefsoftware |
| 0x0B | ONPS | Onboard Programmiersystem |
| 0x0F | FAFP | FA2FP |
| 0x1A | TLRT | Temporaere Loeschroutine |
| 0x1B | TPRG | Temporaere Programmierroutine |
| 0x07 | FLSL | Flashloader Slave |
| 0x0C | IBAD | Interaktive Betriebsanleitung Daten |
| 0x10 | FCFA | Freischaltcode Fahrzeug-Auftrag |
| 0x1C | BLUP | Bootloader-Update Applikation |
| 0x1D | FLUP | Flashloader-Update Applikation |
| 0xC0 | SWUP | Software-Update Package |
| 0xC1 | SWIP | Index Software-Update Package |
| 0xA0 | ENTD | Entertainment Daten |
| 0xA1 | NAVD | Navigation Daten |
| 0xA2 | FCFN | Freischaltcode Funktion |
| 0x04 | GWTB | Gateway-Tabelle |
| 0x0D | SWFK | BEGU: Detaillierung auf SWE-Ebene |
| 0xFF | - | ungueltig |

<a id="table-svk-id"></a>
### SVK_ID

Dimensions: 65 rows × 2 columns

| WERT | BEZEICHNUNG |
| --- | --- |
| 0x01 | SVK_AKTUELL |
| 0x02 | SVK_SUPPLIER |
| 0x03 | SVK_WERK |
| 0x04 | SVK_BACKUP_01 |
| 0x05 | SVK_BACKUP_02 |
| 0x06 | SVK_BACKUP_03 |
| 0x07 | SVK_BACKUP_04 |
| 0x08 | SVK_BACKUP_05 |
| 0x09 | SVK_BACKUP_06 |
| 0x0A | SVK_BACKUP_07 |
| 0x0B | SVK_BACKUP_08 |
| 0x0C | SVK_BACKUP_09 |
| 0x0D | SVK_BACKUP_10 |
| 0x0E | SVK_BACKUP_11 |
| 0x0F | SVK_BACKUP_12 |
| 0x10 | SVK_BACKUP_13 |
| 0x11 | SVK_BACKUP_14 |
| 0x12 | SVK_BACKUP_15 |
| 0x13 | SVK_BACKUP_16 |
| 0x14 | SVK_BACKUP_17 |
| 0x15 | SVK_BACKUP_18 |
| 0x16 | SVK_BACKUP_19 |
| 0x17 | SVK_BACKUP_20 |
| 0x18 | SVK_BACKUP_21 |
| 0x19 | SVK_BACKUP_22 |
| 0x1A | SVK_BACKUP_23 |
| 0x1B | SVK_BACKUP_24 |
| 0x1C | SVK_BACKUP_25 |
| 0x1D | SVK_BACKUP_26 |
| 0x1E | SVK_BACKUP_27 |
| 0x1F | SVK_BACKUP_28 |
| 0x20 | SVK_BACKUP_29 |
| 0x21 | SVK_BACKUP_30 |
| 0x22 | SVK_BACKUP_31 |
| 0x23 | SVK_BACKUP_32 |
| 0x24 | SVK_BACKUP_33 |
| 0x25 | SVK_BACKUP_34 |
| 0x26 | SVK_BACKUP_35 |
| 0x27 | SVK_BACKUP_36 |
| 0x28 | SVK_BACKUP_37 |
| 0x29 | SVK_BACKUP_38 |
| 0x2A | SVK_BACKUP_39 |
| 0x2B | SVK_BACKUP_40 |
| 0x2C | SVK_BACKUP_41 |
| 0x2D | SVK_BACKUP_42 |
| 0x2E | SVK_BACKUP_43 |
| 0x2F | SVK_BACKUP_44 |
| 0x30 | SVK_BACKUP_45 |
| 0x31 | SVK_BACKUP_46 |
| 0x32 | SVK_BACKUP_47 |
| 0x33 | SVK_BACKUP_48 |
| 0x34 | SVK_BACKUP_49 |
| 0x35 | SVK_BACKUP_50 |
| 0x36 | SVK_BACKUP_51 |
| 0x37 | SVK_BACKUP_52 |
| 0x38 | SVK_BACKUP_53 |
| 0x39 | SVK_BACKUP_54 |
| 0x3A | SVK_BACKUP_55 |
| 0x3B | SVK_BACKUP_56 |
| 0x3C | SVK_BACKUP_57 |
| 0x3D | SVK_BACKUP_58 |
| 0x3E | SVK_BACKUP_59 |
| 0x3F | SVK_BACKUP_60 |
| 0x40 | SVK_BACKUP_61 |
| 0xXY | ERROR_UNKNOWN |

<a id="table-dtcextendeddatarecordnumber"></a>
### DTCEXTENDEDDATARECORDNUMBER

Dimensions: 5 rows × 3 columns

| WERT | TEXT | ANZ_BYTE |
| --- | --- | --- |
| 0x00 | ISO_RESERVED | 0 |
| 0x01 | CONDITION_BYTE | 1 |
| 0x02 | HFK | 1 |
| 0x03 | HLZ | 1 |
| 0xFF | RECORD_UNKNOWN | 0 |

<a id="table-dtcsnapshotidentifier"></a>
### DTCSNAPSHOTIDENTIFIER

Dimensions: 9 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | KM_STAND | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1701 | ABS_ZEIT | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1702 | SAE_CODE | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1731 | Fehlerklasse_DTC | - | - | u char | - | 1 | 1 | 0.000000 |
| 0x1750 | PWF_Basinetz | 0-n | - | 0xFF | - | 1 | 1 | 0.000000 |
| 0x1751 | PWF_Teilnetz | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1768 | KM_STAND_SUP | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1769 | ABS_ZEIT_SUP | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0xFFFF | IDENTIFIER_UNKNOWN | - | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |

<a id="table-tab-zeit-syncmethod"></a>
### TAB_ZEIT_SYNCMETHOD

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Combi-Time |
| 0x01 | DMCS |
| 0x02 | IEEE802.1AS |
| 0x03 | invalid |

<a id="table-tab-zeit-user-info"></a>
### TAB_ZEIT_USER_INFO

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | out of sync, no time available |
| 0x01 | insync, ms ECU overall, not comparable |
| 0x02 | ms ECU overall, not comparable |
| 0x03 | ms ECU overall, comparable |
| 0x04 | ms ECU overall, not comparable |
| 0x05 | ms ECU overall, comparable |
| 0x06 | invalid |
| 0x07 | invalid |

<a id="table-fehlerklasse"></a>
### FEHLERKLASSE

Dimensions: 5 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x00 | Keine Fehlerklasse verfuegbar |
| 0x01 | Ueberpruefung bei naechstem Werkstattbesuch |
| 0x02 | Ueberpruefung bei naechstem Halt |
| 0x04 | Ueberpruefung sofort erforderlich ! |
| 0xFF | unbekannte Fehlerklasse |

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 6 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | Allgemeiner Fertigungs- und Energiesparmode | Hier deaktivierte Funktionen gemäß FeTra-Liste festhalten |
| 0x01 | Spezieller Energiesparmode | - |
| 0x02 | ECOS-Mode | - |
| 0x03 | MOST-Mode | - |
| 0x04 | Rollenmode | - |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-cu-err-text"></a>
### CU_ERR_TEXT

Dimensions: 7 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x00 | CUE_NO_ERROR |
| 0x01 | CUE_NO_FREE_SOCKET |
| 0x02 | CUE_NOT_RESOLVED |
| 0x03 | CUE_NO_CONNECTION |
| 0x04 | CUE_SEND_FAILED |
| 0x05 | CUE_TIMEOUT |
| 0xFF | CUE_UNKNOWN |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |
| F_HLZ_VIEW | - |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 1 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 1 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 5 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 1 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |
