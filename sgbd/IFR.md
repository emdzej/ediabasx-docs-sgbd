# IFR.PRG

- Jobs: [65](#jobs)
- Tables: [1](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | IFR |
| ORIGIN | BMW TI-430 Haase |
| REVISION | 10.01 |
| AUTHOR | BMW TI-430 Penzenstadler, BMW TI-430 Huber, BMW TI-430 Drexel,  |
| COMMENT | communication with MDA as pseudo ECU |
| PACKAGE | 1.05 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [INIT_IFR](#job-init-ifr) - Initialisierung mit Zuordnung Adresse
- [START_PRUEFUNG](#job-start-pruefung) - Start mit FZS
- [ENDE_PRUEFUNG](#job-ende-pruefung) - Trennt logische Verbindung zum Slave-MDA Ab V3.07: 3s Wartezeit wenn Antwort nicht OK (0x00) war gewaehrleistet Umschaltung des Slave in Koordinierungskanal bei entsprechender Slave-Konfiguration
- [SET_COMMUNICATION_PARA](#job-set-communication-para) - Setzen Kommunikationsparameter AUTOMATIK und CAN_EIN aus INIT_IFR
- [GET_COMMUNICATION_PARA](#job-get-communication-para) - Auslesen Kommunikationsparameter AUTOMATIK und CAN_EIN aus INIT_IFR
- [SET_CONFIRMED_COM](#job-set-confirmed-com) - Setzt den MDA in Kommunikationsmodus ConfirmedCom
- [CPU_PORT_K1_EIN](#job-cpu-port-k1-ein) - Einschalten des Relais K1 im Funk-Mobilteil
- [CPU_PORT_K1_AUS](#job-cpu-port-k1-aus) - Ausschalten des Relais K1 im Funk-Mobilteil
- [CPU_PORT_K1_LESEN](#job-cpu-port-k1-lesen) - Lesen ob das Relais K1 im Funk-Mobilteil aktiv ist
- [CPU_PORT_K2_EIN](#job-cpu-port-k2-ein) - Einschalten des Relais K2 im Funk-Mobilteil
- [CPU_PORT_K2_AUS](#job-cpu-port-k2-aus) - Ausschalten des Relais K2 im Funk-Mobilteil
- [CPU_PORT_K2_LESEN](#job-cpu-port-k2-lesen) - Lesen ob das Relais K2 im Funk-Mobilteil aktiv ist
- [CPU_CAN_EIN](#job-cpu-can-ein) - Einschalten des CAN Relais im Funk-Mobilteil
- [CPU_CAN_AUS](#job-cpu-can-aus) - Ausschalten des CAN Relais im Funk-Mobilteil
- [CPU_CAN_LESEN](#job-cpu-can-lesen) - Lesen ob das CAN Relais im Funk-Mobilteil aktiv ist
- [STATUS_CPU_K1_K2_CAN](#job-status-cpu-k1-k2-can) - Lesen ob das CAN Relais im Funk-Mobilteil aktiv ist
- [CPU_PORT_STROMREGELUNG_EIN](#job-cpu-port-stromregelung-ein) - Einschalten des Stromregelung im Funk-Mobilteil
- [CPU_PORT_STROMREGELUNG_AUS](#job-cpu-port-stromregelung-aus) - Einschalten des Stromregelung im Funk-Mobilteil
- [CPU_PORT_STROMREGELUNG_LESEN](#job-cpu-port-stromregelung-lesen) - Lesen ob die Stromregelung im Funk-Mobilteil aktiv ist
- [ADRESSE_LESEN](#job-adresse-lesen) - Abfrage Adresse des Mobiladapters (Slave-MDA) HINWEIS: wird nur noch aus Kompatibilaetsgruenden unterstuetzt HINWEIS: neuer Job ADRESSEN_LESEN_SLAVE
- [ADRESSE_LESEN_MASTER](#job-adresse-lesen-master) - Abfrage der Adresse des Master-MDA HINWEIS: schnelle Ausfuehrung, da keine Funk-Kommunikation
- [ADRESSE_LESEN_SLAVE](#job-adresse-lesen-slave) - Abfrage der Adresse des Slave-MDA
- [ADRESSEN_LESEN](#job-adressen-lesen) - Abfrage der Adressen des Master- und des Slave-MDA HINWEIS: Verbindung zum Slave-MDA erforderlich
- [SLEEP_IFR](#job-sleep-ifr) - Abbruch der Infrarot-Verbindung (IFR-ADS -&gt; SLEEP-Mode) Es kommt keine Antwort zurueck !
- [VERSION_LESEN](#job-version-lesen) - Abfrage der Version des Masters und des Mobiladapters Abfrage der Adresse des Masters und des Mobiladapters
- [CHECK_SLEEP](#job-check-sleep) - Test ob MDA in den Sleepmodus geschaltet hat bei Sleep Modus Adresse = 0 und Softwareversion = 0000
- [STATUS_KLEMMEN](#job-status-klemmen) - Abfrage der Klemmenstati des Mobiladapters
- [STATUS_SLAVE_ZIELNUMMER](#job-status-slave-zielnummer) - Abfrage der Slave Zielnummer
- [STATUS_STATISTIK_MASTER](#job-status-statistik-master) - Statistik aus dem Master lesen
- [STATUS_STATISTIK_SLAVE](#job-status-statistik-slave) - Statistik aus dem Slave lesen
- [LOESCHEN_STATISTIK_MASTER](#job-loeschen-statistik-master) - Statistik im Master loeschen
- [LOESCHEN_STATISTIK_SLAVE](#job-loeschen-statistik-slave) - Statistik im Slave loeschen
- [ZIEL_MASTER_LESEN](#job-ziel-master-lesen) - Zieladresse des Masters lesen (Auto-Update) Erweiteter ADS-Befehl: 0x01
- [BIN_DOWNLOAD_START](#job-bin-download-start) - Download Start, binären Datentransfer vom PC in den SDA-RAM starten (Auto-Update) Erweiteter ADS-Befehl: 0x10
- [BIN_FILE_DOWNLOAD](#job-bin-file-download) - Download, binaeren Datentransfer vom PC in den SDA-RAM (Auto-Update) Erweiteter ADS-Befehl: 0x11
- [BIN_DOWNLOAD_ENDE](#job-bin-download-ende) - Download Ende, binaeren Datentransfer vom PC in den SDA-RAM beenden (Auto-Update) Erweiteter ADS-Befehl: 0x12
- [START_FLASHEN](#job-start-flashen) - Start des Flashens vom SDA-RAM in den MDA oder in den SDA Erweiteter ADS-Befehl: 0x19
- [CHECK_FIRMWARE](#job-check-firmware) - Versions- und Checksummenprüfung der mit 0x10-0x12 in den SDA-RAM geladenen Firmware Erweiteter ADS-Befehl: 0x18
- [FORTSCHRITT_FLASHEN](#job-fortschritt-flashen) - Fortschrittsabfrage des Flashens Erweiteter ADS-Befehl: 0x1A
- [RUECKLESEN_FW_AUS_MDA](#job-ruecklesen-fw-aus-mda) - Start des Rücklesens vom MDA in den SDA-RAM Erweiteter ADS-Befehl: 0x1B
- [FORTSCHRITT_RUECKLESEN](#job-fortschritt-ruecklesen) - Fortschrittsabfrage des Ruecklesens der FW aus MDA Erweiteter ADS-Befehl: 0x1C
- [KONFIG_LESEN](#job-konfig-lesen) - Konfiguration lesen Erweiteter ADS-Befehl: 0x20
- [KONFIG_SCHREIBEN](#job-konfig-schreiben) - Konfiguration schreiben Erweiteter ADS-Befehl: 0x21
- [RESET](#job-reset) - Reset MDA/SDA Erweiteter ADS-Befehl: 0x30
- [KL15_VER_LESEN](#job-kl15-ver-lesen) - KL15 FW-Version lesen (incl. Checksum) Erweiteter ADS-Befehl: 0x40
- [KL15_RESET](#job-kl15-reset) - Reset Klemme-15-Simulator Erweiteter ADS-Befehl: 0x41
- [KL15_START_FLASH](#job-kl15-start-flash) - Start des Flashens KL15 vom MDA-RAM in die KL15 Erweiteter ADS-Befehl: 0x42
- [KL15_STATUS_FLASH](#job-kl15-status-flash) - Fortschrittsabfrage des Ruecklesens der FW aus MDA Erweiteter ADS-Befehl: 0x1C
- [KL15_START_DOWNLOAD](#job-kl15-start-download) - Download Start, binären Datentransfer KL15-FW vom PC in den MDA-RAM starten Erweiteter ADS-Befehl: 0x44
- [KL15_DOWNLOAD_PCMDA](#job-kl15-download-pcmda) - Download, binaeren Datentransfer KL15 FW vom PC in den MDA-RAM Erweiteter ADS-Befehl: 0x45
- [KL15_ENDE_DOWNLOAD](#job-kl15-ende-download) - Download Ende, binaeren Datentransfer KL15 Firmware beendet Erweiteter ADS-Befehl: 0x46
- [KL15_CHECK_FIRMWARE](#job-kl15-check-firmware) - Versions- und Checksummenprüfung der mit 0x44-0x46 in das MDA-RAM geladenen KL15-Firmware Erweiteter ADS-Befehl: 0x47
- [SET_CAN_ACCEPT_FILTER](#job-set-can-accept-filter) - Set CAN Acceptance Filter (11 Bit ID) ID A und ID B geben den gültigen ID Bereich an Wird A = B = 0 übergeben, ist das Acceptance Filter nicht aktiv
- [GET_CAN_MESSAGE](#job-get-can-message) - Emfangen von CAN-Botschaften Die erwartete ID muss sich im Bereich der mit "Set CAN Acceptance Filter" gesetzten Werte A und B befinden
- [SEND_CAN_MESSAGE](#job-send-can-message) - Send CAN Message (11 Bit ID) Sendet 0 bis 8 Datenbytes (0 = nur Frame)
- [SET_AUTO_ASSIGN](#job-set-auto-assign) - Aktivieren der Automatischen Taufe 0 == "OFF" 1 == "ON"
- [WRITE_AUTO_ASSIGN_DATA](#job-write-auto-assign-data) - Schreiben der Daten die für die automaische Taufe im MDA abgelegt werden sollen
- [READ_AUTO_ASSIGN_DATA](#job-read-auto-assign-data) - Auslesen der Daten die für die automatische Taufe im MDA abgelegt sind
- [READ_AUTO_ASSIGN_STATUS](#job-read-auto-assign-status) - Auslesen des aktuellen Status der automatischen Taufe
- [GET_RUNNING_TIME](#job-get-running-time) - Liefert Systemzeit nach dem Einschalten
- [GET_ERROR_COUNT](#job-get-error-count) - Liefert Fehlerspeicherausgaben
- [CLR_ERROR_COUNT](#job-clr-error-count) - Rücksetzen des Fehlerspreichers
- [_SET_MASTER_COM_MODE](#job-set-master-com-mode) - Einstellen Kommunikationsmode Master-to-Slave

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

Initialisierung und Kommunikationsparameter DS2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-init-ifr"></a>
### INIT_IFR

Initialisierung mit Zuordnung Adresse

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FZS | string | Fahrzeug-Steuerschluessel wenn nur numerisch wird in  4 Byte-long   gewandelt wenn alphanumerisch wird in 7 Byte-String gewandelt |
| ADRESSE_IFR | string | Adresse Mobiladapter (muss ungleich 0 sein) |
| AUTOMATIK | long | 0 = Automatische CAN / K-Line Umschaltung aus 1 = Automatische CAN / K-Line Umschaltung ein |
| CAN_EIN | long | 0 = K-Line 1 = CAN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_NAK |

<a id="job-start-pruefung"></a>
### START_PRUEFUNG

Start mit FZS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FZS | string | Fahrzeug-Steuerschluessel wenn nur numerisch wird in  4 Byte-long   gewandelt wenn alphanumerisch wird in 7 Byte-String gewandelt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-ende-pruefung"></a>
### ENDE_PRUEFUNG

Trennt logische Verbindung zum Slave-MDA Ab V3.07: 3s Wartezeit wenn Antwort nicht OK (0x00) war gewaehrleistet Umschaltung des Slave in Koordinierungskanal bei entsprechender Slave-Konfiguration

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | die derzeitige Implementierung liefert immer OKAY |
| JOB_STATUS_WERT | int | tatsaechlicher Zahlenwert des Jobstatus vom Master |

<a id="job-set-communication-para"></a>
### SET_COMMUNICATION_PARA

Setzen Kommunikationsparameter AUTOMATIK und CAN_EIN aus INIT_IFR

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUTOMATIK | long | 0 = Automatische CAN / K-Line Umschaltung aus 1 = Automatische CAN / K-Line Umschaltung ein |
| CAN_EIN | long | 0 = K-Line 1 = CAN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-get-communication-para"></a>
### GET_COMMUNICATION_PARA

Auslesen Kommunikationsparameter AUTOMATIK und CAN_EIN aus INIT_IFR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AUTOMATIK | int | 0 = Automatische CAN / K-Line Umschaltung aus 1 = Automatische CAN / K-Line Umschaltung ein |
| CAN_EIN | int | 0 = K-Line 1 = CAN |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-set-confirmed-com"></a>
### SET_CONFIRMED_COM

Setzt den MDA in Kommunikationsmodus ConfirmedCom

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COM_PORT | int | Parameter Confirmed Communication 0 = K-Line, 1 = D-CAN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-cpu-port-k1-ein"></a>
### CPU_PORT_K1_EIN

Einschalten des Relais K1 im Funk-Mobilteil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-cpu-port-k1-aus"></a>
### CPU_PORT_K1_AUS

Ausschalten des Relais K1 im Funk-Mobilteil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-cpu-port-k1-lesen"></a>
### CPU_PORT_K1_LESEN

Lesen ob das Relais K1 im Funk-Mobilteil aktiv ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CPU_PORT_K1 | long | OKAY, wenn fehlerfrei |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-cpu-port-k2-ein"></a>
### CPU_PORT_K2_EIN

Einschalten des Relais K2 im Funk-Mobilteil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-cpu-port-k2-aus"></a>
### CPU_PORT_K2_AUS

Ausschalten des Relais K2 im Funk-Mobilteil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-cpu-port-k2-lesen"></a>
### CPU_PORT_K2_LESEN

Lesen ob das Relais K2 im Funk-Mobilteil aktiv ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CPU_PORT_K2 | long | OKAY, wenn fehlerfrei |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-cpu-can-ein"></a>
### CPU_CAN_EIN

Einschalten des CAN Relais im Funk-Mobilteil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-cpu-can-aus"></a>
### CPU_CAN_AUS

Ausschalten des CAN Relais im Funk-Mobilteil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-cpu-can-lesen"></a>
### CPU_CAN_LESEN

Lesen ob das CAN Relais im Funk-Mobilteil aktiv ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CPU_CAN | long | OKAY, wenn fehlerfrei |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-status-cpu-k1-k2-can"></a>
### STATUS_CPU_K1_K2_CAN

Lesen ob das CAN Relais im Funk-Mobilteil aktiv ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CPU_CAN | long | OKAY, wenn fehlerfrei |
| CPU_K1 | long | OKAY, wenn fehlerfrei |
| CPU_K2 | long | OKAY, wenn fehlerfrei |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-cpu-port-stromregelung-ein"></a>
### CPU_PORT_STROMREGELUNG_EIN

Einschalten des Stromregelung im Funk-Mobilteil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-cpu-port-stromregelung-aus"></a>
### CPU_PORT_STROMREGELUNG_AUS

Einschalten des Stromregelung im Funk-Mobilteil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-cpu-port-stromregelung-lesen"></a>
### CPU_PORT_STROMREGELUNG_LESEN

Lesen ob die Stromregelung im Funk-Mobilteil aktiv ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CPU_PORT_STROMREGELUNG | long | OKAY, wenn fehlerfrei |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-adresse-lesen"></a>
### ADRESSE_LESEN

Abfrage Adresse des Mobiladapters (Slave-MDA) HINWEIS: wird nur noch aus Kompatibilaetsgruenden unterstuetzt HINWEIS: neuer Job ADRESSEN_LESEN_SLAVE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| NUMMER | int | Slave-Adresse als Integer |

<a id="job-adresse-lesen-master"></a>
### ADRESSE_LESEN_MASTER

Abfrage der Adresse des Master-MDA HINWEIS: schnelle Ausfuehrung, da keine Funk-Kommunikation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY wenn Job erfolgreich ausgefuehrt |
| ADRESSE_MASTER | int | Adresse des Master-MDA |

<a id="job-adresse-lesen-slave"></a>
### ADRESSE_LESEN_SLAVE

Abfrage der Adresse des Slave-MDA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY wenn Job erfolgreich ausgefuehrt |
| ADRESSE_SLAVE | int | Adresse des Slave-MDA |

<a id="job-adressen-lesen"></a>
### ADRESSEN_LESEN

Abfrage der Adressen des Master- und des Slave-MDA HINWEIS: Verbindung zum Slave-MDA erforderlich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY wenn Job erfolgreich ausgefuehrt |
| ADRESSE_MASTER | int | Adresse des Masters-MDA |
| ADRESSE_SLAVE | int | Adresse des Slave-MDA |

<a id="job-sleep-ifr"></a>
### SLEEP_IFR

Abbruch der Infrarot-Verbindung (IFR-ADS -&gt; SLEEP-Mode) Es kommt keine Antwort zurueck !

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-version-lesen"></a>
### VERSION_LESEN

Abfrage der Version des Masters und des Mobiladapters Abfrage der Adresse des Masters und des Mobiladapters

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| VERSION_MASTER | string | Version des Masters |
| ADRESSE_MASTER | int | Adresse des Masters |
| VERSION_SLAVE | string | Version des Mobilteils |
| ADRESSE_SLAVE | int | Adresse des Mobilteils |

<a id="job-check-sleep"></a>
### CHECK_SLEEP

Test ob MDA in den Sleepmodus geschaltet hat bei Sleep Modus Adresse = 0 und Softwareversion = 0000

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| VERSION_SLAVE | string | Version des Mobilteils, "0000" im Sleepmodus |
| ADRESSE_SLAVE | int | Adresse des Mobilteils, "0" im Sleepmodus |

<a id="job-status-klemmen"></a>
### STATUS_KLEMMEN

Abfrage der Klemmenstati des Mobiladapters

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_K1 | int | Status K1-Relay als Integer |
| STAT_K2 | int | Status K2-Relay als Integer |
| STAT_K15 | int | Status K15 als Integer |
| STAT_K30 | int | Status K30 als Integer |
| STAT_KONSTANTSTROM | int | Status Konstantstrom als Integer |

<a id="job-status-slave-zielnummer"></a>
### STATUS_SLAVE_ZIELNUMMER

Abfrage der Slave Zielnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SLAVE_ZIELNUMMER | int | Rückgabe Zielnummer Master bei P2P |

<a id="job-status-statistik-master"></a>
### STATUS_STATISTIK_MASTER

Statistik aus dem Master lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ABBRUCH | int | Anzahl der Verbindungsabbrueche am Master |
| STAT_WIEDERHOLUNGEN | int | Anzahl der WIEDERHOLUNGEN am Master |
| STAT_VERBUNDENER_SLAVE | int | Verbundener Slave |
| _TEL_ANTWORT | binary | Anwort-Telegramm vom SG |
| JOB_STATUS | string | die derzeitige Implementierung liefert immer OKAY |
| JOB_STATUS_WERT | int | tatsaechlicher Zahlenwert des Jobstatus vom Master |

<a id="job-status-statistik-slave"></a>
### STATUS_STATISTIK_SLAVE

Statistik aus dem Slave lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ABBRUCH | int | Anzahl der Verbindungsabbrueche am Slave |
| STAT_WIEDERHOLUNGEN | int | Anzahl der WIEDERHOLUNGEN am Slave |
| STAT_VERBUNDENER_MASTER | int | Verbundener Master |
| _TEL_ANTWORT | binary | Anwort-Telegramm vom SG |
| JOB_STATUS | string | die derzeitige Implementierung liefert immer OKAY |
| JOB_STATUS_WERT | int | tatsaechlicher Zahlenwert des Jobstatus vom Master |

<a id="job-loeschen-statistik-master"></a>
### LOESCHEN_STATISTIK_MASTER

Statistik im Master loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-loeschen-statistik-slave"></a>
### LOESCHEN_STATISTIK_SLAVE

Statistik im Slave loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-ziel-master-lesen"></a>
### ZIEL_MASTER_LESEN

Zieladresse des Masters lesen (Auto-Update) Erweiteter ADS-Befehl: 0x01

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ZIEL_ADRESSE | int | Zieladresse (Slave-Nummer bei P2P) aus Konfigurationdaten |

<a id="job-bin-download-start"></a>
### BIN_DOWNLOAD_START

Download Start, binären Datentransfer vom PC in den SDA-RAM starten (Auto-Update) Erweiteter ADS-Befehl: 0x10

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FILE_LEN | long | Uebergabe File-Laenge |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-bin-file-download"></a>
### BIN_FILE_DOWNLOAD

Download, binaeren Datentransfer vom PC in den SDA-RAM (Auto-Update) Erweiteter ADS-Befehl: 0x11

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Puffer zur Aufnahme der Firmware-Daten-Bloecke |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-bin-download-ende"></a>
### BIN_DOWNLOAD_ENDE

Download Ende, binaeren Datentransfer vom PC in den SDA-RAM beenden (Auto-Update) Erweiteter ADS-Befehl: 0x12

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FILE_LEN | long | Uebergabe File-Länge |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei, Dateilänge OK |

<a id="job-start-flashen"></a>
### START_FLASHEN

Start des Flashens vom SDA-RAM in den MDA oder in den SDA Erweiteter ADS-Befehl: 0x19

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_TARGET | int | Ziel der Daten aus dem SDA-RAM "1" = Start des Flashens vom SDA-RAM in den SDA (Master) "2" = Start des Flashens vom SDA-RAM in den MDA (Slave) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-check-firmware"></a>
### CHECK_FIRMWARE

Versions- und Checksummenprüfung der mit 0x10-0x12 in den SDA-RAM geladenen Firmware Erweiteter ADS-Befehl: 0x18

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FW_VER | string | FW-Version der geladenen FW(wie im MDA-Display angezeigt) Eingabe als [HIGH-byte] [LOW-byte] |
| CHECK_SUM | string | Check-Summe der geladenen FW Eingabe als [HIGH-byte] [LOW-byte] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_REJECTED --&gt; Keine FW geladen, Argumentfehler, MDA nicht bereit |
| FW_STATUS | long | 00 = NOK --&gt; FW nicht geladen, Versionsabgleich NOK oder Checksumme NOK 01 = OK |
| FW_VER_LOADED | long | FW-Version der im SDA-RAM vorhandenen FW Rueckgabe als [HIGH-byte] [LOW-byte] |
| CHECK_SUM_LOADED | long | Check-Summe der im SDA-RAM vorhandenen FW Rueckgabe als [HIGH-byte] [LOW-byte] |

<a id="job-fortschritt-flashen"></a>
### FORTSCHRITT_FLASHEN

Fortschrittsabfrage des Flashens Erweiteter ADS-Befehl: 0x1A

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| FORTSCHRITT | long | Fortschrittsanzeige des Flashens |

<a id="job-ruecklesen-fw-aus-mda"></a>
### RUECKLESEN_FW_AUS_MDA

Start des Rücklesens vom MDA in den SDA-RAM Erweiteter ADS-Befehl: 0x1B

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-fortschritt-ruecklesen"></a>
### FORTSCHRITT_RUECKLESEN

Fortschrittsabfrage des Ruecklesens der FW aus MDA Erweiteter ADS-Befehl: 0x1C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| FORTSCHRITT | long | Fortschrittsanzeige des Ruecklesens |

<a id="job-konfig-lesen"></a>
### KONFIG_LESEN

Konfiguration lesen Erweiteter ADS-Befehl: 0x20

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SOURCE | int | Quelle der Konfigurationsdaten 1 = Lesen aus SDA (Master) 2 = Lesen aus MDA (Slave) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| KONFIG | string | OKAY |

<a id="job-konfig-schreiben"></a>
### KONFIG_SCHREIBEN

Konfiguration schreiben Erweiteter ADS-Befehl: 0x21

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TARGET | int | Wahl des Ziels zum schreiben der Konfigurationsdaten 1 = Schreiben in den SDA (Master) 2 = Schreiben in den MDA (Slave) |
| CONFIG_STRING | string | Konfigurationsstring ohne Checksum Byte |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-reset"></a>
### RESET

Reset MDA/SDA Erweiteter ADS-Befehl: 0x30

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TARGET | int | Wahl des Ziels für den RESET 1 = SDA (Master) 2 = MDA (Slave) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-kl15-ver-lesen"></a>
### KL15_VER_LESEN

KL15 FW-Version lesen (incl. Checksum) Erweiteter ADS-Befehl: 0x40

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| KL15_FW_VER | string | KL15-FW-Version Rueckgabe als [HIGH-byte] [LOW-byte] |
| KL15_CHECK_SUM | long | Check-Summe KL15-FW Rueckgabe als [HIGH-byte] [LOW-byte] |

<a id="job-kl15-reset"></a>
### KL15_RESET

Reset Klemme-15-Simulator Erweiteter ADS-Befehl: 0x41

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-kl15-start-flash"></a>
### KL15_START_FLASH

Start des Flashens KL15 vom MDA-RAM in die KL15 Erweiteter ADS-Befehl: 0x42

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-kl15-status-flash"></a>
### KL15_STATUS_FLASH

Fortschrittsabfrage des Ruecklesens der FW aus MDA Erweiteter ADS-Befehl: 0x1C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| FLASH_RESULT | string | "0" = Flashen i.O, "Fehlernummer" = n.i.O. |

<a id="job-kl15-start-download"></a>
### KL15_START_DOWNLOAD

Download Start, binären Datentransfer KL15-FW vom PC in den MDA-RAM starten Erweiteter ADS-Befehl: 0x44

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATA_LEN | long | Uebergabe File-Laenge |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-kl15-download-pcmda"></a>
### KL15_DOWNLOAD_PCMDA

Download, binaeren Datentransfer KL15 FW vom PC in den MDA-RAM Erweiteter ADS-Befehl: 0x45

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Puffer zur Aufnahme der Firmware-Daten-Bloecke |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-kl15-ende-download"></a>
### KL15_ENDE_DOWNLOAD

Download Ende, binaeren Datentransfer KL15 Firmware beendet Erweiteter ADS-Befehl: 0x46

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATA_LEN | long | Längeninformation der geschriebenen Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei, Dateilänge OK |

<a id="job-kl15-check-firmware"></a>
### KL15_CHECK_FIRMWARE

Versions- und Checksummenprüfung der mit 0x44-0x46 in das MDA-RAM geladenen KL15-Firmware Erweiteter ADS-Befehl: 0x47

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FW_VER | string | KL15-FW-Version der geladenen FW Eingabe als [HIGH-byte] [LOW-byte] |
| CHECK_SUM | string | Check-Summe der geladenen KL15-FW Eingabe als [HIGH-byte] [LOW-byte] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_REJECTED --&gt; fehlerhafte Parameter |
| FW_STATUS | long | 00 = NOK --&gt; KL15-FW nicht geladen, Versionsabgleich NOK oder Checksumme NOK 01 = OK |
| FW_VER_LOADED | long | KL15-FW-Version der im MDA-RAM vorhandenen FW Rueckgabe als [HIGH-byte] [LOW-byte] |
| CHECK_SUM_LOADED | long | Check-Summe der im MDA-RAM vorhandenen KL15-FW Rueckgabe als [HIGH-byte] [LOW-byte] |

<a id="job-set-can-accept-filter"></a>
### SET_CAN_ACCEPT_FILTER

Set CAN Acceptance Filter (11 Bit ID) ID A und ID B geben den gültigen ID Bereich an Wird A = B = 0 übergeben, ist das Acceptance Filter nicht aktiv

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ACCEPTANCEFILTER_FROM | unsigned int | Kennzeichnet Bereichsstart --&gt; erste gültige ID Eingabe als z.B. 0x700 |
| ACCEPTANCEFILTER_TO | unsigned int | Kennzeichnet Bereichsende --&gt; letzte gültige ID Eingabe als z.B. 0x7FF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-get-can-message"></a>
### GET_CAN_MESSAGE

Emfangen von CAN-Botschaften Die erwartete ID muss sich im Bereich der mit "Set CAN Acceptance Filter" gesetzten Werte A und B befinden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| CANIDENTIFIER | unsigned int |  |
| DATALEN | unsigned int |  |
| DATA | binary |  |

<a id="job-send-can-message"></a>
### SEND_CAN_MESSAGE

Send CAN Message (11 Bit ID) Sendet 0 bis 8 Datenbytes (0 = nur Frame)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CANIDENTIFIER | unsigned int |  |
| DATALENGTH | unsigned char |  |
| D1 | unsigned char |  |
| D2 | unsigned char |  |
| D3 | unsigned char |  |
| D4 | unsigned char |  |
| D5 | unsigned char |  |
| D6 | unsigned char |  |
| D7 | unsigned char |  |
| D8 | unsigned char |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| IN | binary |  |

<a id="job-set-auto-assign"></a>
### SET_AUTO_ASSIGN

Aktivieren der Automatischen Taufe 0 == "OFF" 1 == "ON"

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_MODE | int | 0 == "OFF" 1 == "ON" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-write-auto-assign-data"></a>
### WRITE_AUTO_ASSIGN_DATA

Schreiben der Daten die für die automaische Taufe im MDA abgelegt werden sollen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUTO_ASSIGN_DATA | string | Auto-Assign-Daten sind auf 252 Zeichen durch SGBD begrenzt Hexadezimalwerte Daten für Auto-Taufstring --&gt; 0x00,0x02,0x00,0x02,0x1A,0x90,.... String_Bsp: 000200021A90.... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-read-auto-assign-data"></a>
### READ_AUTO_ASSIGN_DATA

Auslesen der Daten die für die automatische Taufe im MDA abgelegt sind

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| AUTO_ASSIGN_DATA | string | Rückgabe-Bsp: 000200021A900208100322F1900D13 zu lesen wie --&gt; 0x00,0x02,0x00,0x02,0x1A,0x90,.... |

<a id="job-read-auto-assign-status"></a>
### READ_AUTO_ASSIGN_STATUS

Auslesen des aktuellen Status der automatischen Taufe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| AUTO_ASSIGN_STATE | string | Automatische Taufe ON/OFF 0 == OFF 1 == ON |
| MDA_VIN_CONF | string | Status VIN confirmed/unconfirmed 0x00 == unconfirmed 0x01 == confirmed 0xFF == AUTO_ASSIGN_STATE "OFF" |
| ECU_NR | string | Nummer des SGs mit dem die Auto-Taufe zuletzt erfolgreich war 0xFF: keine erfolgreiche Auto-Taufe durchgeführt |

<a id="job-get-running-time"></a>
### GET_RUNNING_TIME

Liefert Systemzeit nach dem Einschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_TARGET | int | 1 == "Zeit des SDA" 2 == "Zeit des MDA" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| RUNNING_TIME | long | Systemzeit nach dem Einschalten in 100ms (z.B. 1011 --&gt; 101,1sec Rueckgabe als [HIGH-byte] [LOW-byte] |

<a id="job-get-error-count"></a>
### GET_ERROR_COUNT

Liefert Fehlerspeicherausgaben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_TARGET | int | 1 == "Zeit des SDA" 2 == "Zeit des MDA" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| SLEEP_ERROR | long | Rueckgabe als [HIGH-byte] [LOW-byte] |
| WATCHDOG_RESET | long | Rueckgabe als [HIGH-byte] [LOW-byte] |
| STACK_OVERFLOW | long | Rueckgabe als [HIGH-byte] [LOW-byte] |
| STACK_UNDERFLOW | long | Rueckgabe als [HIGH-byte] [LOW-byte] |
| NMI_INTERRUPT | long | Rueckgabe als [HIGH-byte] [LOW-byte] |
| PAR_ERROR_STARTUP | long | Rueckgabe als [HIGH-byte] [LOW-byte] |
| PAR_ERROR_RUNNING | long | Rueckgabe als [HIGH-byte] [LOW-byte] |

<a id="job-clr-error-count"></a>
### CLR_ERROR_COUNT

Rücksetzen des Fehlerspreichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_TARGET | int | 1 == "Zeit des SDA" 2 == "Zeit des MDA" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-set-master-com-mode"></a>
### _SET_MASTER_COM_MODE

Einstellen Kommunikationsmode Master-to-Slave

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TARGET | int | Adresse SLAVE TARGET = 0  --&gt; Verheiratungsmode TARGET &gt; 0 (bis 9999) --&gt; P2P-Mode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

## Tables

### Index

- [BITS](#table-bits) (5 × 4)

<a id="table-bits"></a>
### BITS

Dimensions: 5 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| STAT_K1 | 3 | 0x01 | 0x01 |
| STAT_K2 | 3 | 0x02 | 0x02 |
| STAT_K15 | 3 | 0x20 | 0x20 |
| STAT_K30 | 3 | 0x10 | 0x10 |
| STAT_STROM | 3 | 0x80 | 0x80 |
