# LWS5.prg

- Jobs: [24](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Lenkradwinkel mit CAN-Schnittstelle |
| ORIGIN | BMW EE-23 Schoenherr |
| REVISION | 1.14 |
| AUTHOR | BMW TP-421 Gerd Huber, Kostal AVC3 Hillebrand |
| COMMENT | N/A |
| PACKAGE | 0.04 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung / Kommunikationsparameter fuer Lenkwinkelsensor 5 (CAN) automatischer Aufruf beim ersten Zugriff auf die SGBD
- [IDENT](#job-ident) - Ident-Daten fuer Lenkwinkelsensor 5
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose Dummy-Job ohne Diagnosetelegramm (d.h. immer OKAY)
- [STATUS_DIGITAL](#job-status-digital) - Auslesen der digitalen IO-Stati des Lenkwinkelsensors 5 Der Wertebereich ist bei allen Results gleich: Bereich: 0, wenn FALSE / 1, wenn TRUE
- [STATUS_ANALOG](#job-status-analog) - Auslesen der Analogwerte
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern eines digitalen Ein- oder Ausgangs v. LWS5 ! erlaubte Namen des Arguments 'FUNKTION' ueber Tool XTRACT.exe ! Aufruf 'XTRACT [-F] LWS5.prg'
- [STATUS_SG_DIGITAL](#job-status-sg-digital) - Auslesen der digitalen SG-Stati des Lenkwinkelsensors 5 Der Wertebereich ist bei allen Results gleich: Bereich: 0, wenn FALSE / 1, wenn TRUE
- [STATUS_SG_ONLINE](#job-status-sg-online) - Auslesen der analogen Online-Werte des LWS5
- [STATUS_SG_VIRTUELL](#job-status-sg-virtuell) - Auslesen der analogen Online-Werte / virtuelle Sensorik
- [ABGLEICH_LESEN](#job-abgleich-lesen) - Auslesen der Abgleich-Werte
- [CODIERUNG_LESEN](#job-codierung-lesen) - Fahrzeugcodierung des LWS5 auslesen
- [CODIERUNG_CHECK](#job-codierung-check) - Checksumme der Codierung des LWS5 auslesen
- [STATUS_KL30](#job-status-kl30) - Lesen des Unterspannungszählers
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des ROM/RAM bzw. EEPROM-Speichers
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen der Herstelldaten
- [IDENT_E](#job-ident-e) - Ident-Daten fuer Lenkwinkelsensor 5
- [CODIERUNG_SCHREIBEN_DATEI](#job-codierung-schreiben-datei) - Beschreiben der Codierdaten des LWS5 ueber Datei
- [ABGLEICH_SCHREIBEN](#job-abgleich-schreiben) - Programmieren der Abgleich-Werte
- [ABGLEICH_VORGEBEN](#job-abgleich-vorgeben) - Vorgeben der Abgleichwerte

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

Initialisierung / Kommunikationsparameter fuer Lenkwinkelsensor 5 (CAN) automatischer Aufruf beim ersten Zugriff auf die SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer Lenkwinkelsensor 5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR | int | Softwarenummer |
| _TEL_ANTWORT | int | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Fehlerort momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit Bereich: 0 - 31 |
| F_ART_ANZ | int | Anzahl der Fehlerarten Bereich: immer 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Bereich: immer 0 |
| F_ART1_NR | int | 1. (einzige) Fehlerart Bereich: 0, 1 |
| F_ART1_TEXT | string | 1. (einzige) Fehlerart als Text table FArtTexte ARTTEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose Dummy-Job ohne Diagnosetelegramm (d.h. immer OKAY)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | immer OKAY |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Auslesen der digitalen IO-Stati des Lenkwinkelsensors 5 Der Wertebereich ist bei allen Results gleich: Bereich: 0, wenn FALSE / 1, wenn TRUE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_U_CAN_TREIBER_AKTIV | int | Statusbit fuer die CAN-Treiber Spannung |
| STAT_U_BASISSENSOR_AKTIV | int | Statusbit fuer die Versorgungsspannung des Basissensors |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Auslesen der Analogwerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SENSOR_U_SCHLEIFER_1_WERT | long | Sensor-Schleiferspannung 1 Bereich: 0 bis 255 [Digit] |
| STAT_SENSOR_U_SCHLEIFER_2_WERT | long | Sensor-Schleiferspannung 2 Bereich: 0 bis 255 [Digit] |
| STAT_SENSOR_I_WERT | long | Sensor-Stromwert Bereich: 0 bis 4 [mA] |
| STAT_U_KLEMME_87_WERT | long | Spannung an Klemme 87 Bereich: 0 bis 18 [V] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern eines digitalen Ein- oder Ausgangs v. LWS5 ! erlaubte Namen des Arguments 'FUNKTION' ueber Tool XTRACT.exe ! Aufruf 'XTRACT [-F] LWS5.prg'

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTION | string | gewuenschte Komponente table Steuern_Digital SIGNAL |
| EIN | int | "1", wenn einschalten / "0", wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sg-digital"></a>
### STATUS_SG_DIGITAL

Auslesen der digitalen SG-Stati des Lenkwinkelsensors 5 Der Wertebereich ist bei allen Results gleich: Bereich: 0, wenn FALSE / 1, wenn TRUE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LWS_FABNEU_AKTIV | int | LWS-Status fabrikneu |
| STAT_LWS_POR_AKTIV | int | LWS hat einen Power on Reset erhalten |
| STAT_LWS_WDR_AKTIV | int | LWS hat einen Watchdogreset erhalten |
| STAT_LWS_REL_AKTIV | int | LWS gibt nur einen relativen Lenkwinkel aus |
| STAT_LWS_FILTER_INIT_AKTIV | int | LWS Filter noch nicht initialisiert |
| STAT_LWS_ABGL_AKTIV | int | LWS im Abgleichmodus |
| STAT_CAN_INIT_AKTIV | int | CAN Initialisierung |
| STAT_ASC2_RCV_AKTIV | int | ASC2 Botschaft empfangen |
| STAT_DIAG_RCV_AKTIV | int | ASC3 Botschaft mit Abgleichinformation empfangen |
| STAT_PSI_PKT_RCV_AKTIV | int | ASC3 Botschaft mit Lenkwinkelgeschwindigkeitsinformation empfangen |
| STAT_CAN_STAND_RCV_AKTIV | int | DME Botschaft mit CAN-Stand empfangen |
| STAT_CAN_STAND_OK_AKTIV | int | CAN-Stand ist i.O. |
| STAT_CAN_TX_OFF_AKTIV | int | CAN-Bus fuer Senden gesperrt |
| STAT_CAN_OFF_AKTIV | int | CAN-Bus gesperrt |
| STAT_SDL_ZYKL_SYC_AKTIV | int | Scheduler-Status = SDL_ZYKL_SYC |
| STAT_SDL_ZYKL_START_AKTIV | int | Scheduler-Status = SDL_ZYKL_START |
| STAT_SDL_LWR_AKTIV | int | Scheduler-Status = SDL_LRW |
| STAT_SDL_ASC2_AKTIV | int | Scheduler-Status = SDL_ASC2 |
| STAT_SDL_PSI_PKT_AKTIV | int | Scheduler-Status = SDL_PSI_PKT |
| STAT_SDL_VIR_SENS_AKTIV | int | Scheduler-Status = SDL_VIR_SENS |
| STAT_SDL_KLASS_AKTIV | int | Scheduler-Status = SDL_KLASS |
| STAT_SDL_STAT_ERR_AKTIV | int | Scheduler-Status = SDL_STAT_ERR |
| STAT_SDL_LWS1_TR_AKTIV | int | Scheduler-Status = SDL_LWS1_TR |
| STAT_SDL_INIT_MOD_AKTIV | int | Scheduler-Modus = SDL_INIT_MOD |
| STAT_ASC2_SYC1_MOD_AKTIV | int | Scheduler-Modus = ASC2_SYC1_MOD |
| STAT_ASC2_SYC2_MOD_AKTIV | int | Scheduler-Modus = ASC2_SYC2_MOD |
| STAT_ASC2_ASYC_MOD_AKTIV | int | Scheduler-Modus = ASC2_ASYC_MOD |
| STAT_SDL_SLOW_MOD_AKTIV | int | Scheduler-Modus = SDL_SLOW_MOD |
| STAT_SDL_NACHLF_MOD_AKTIV | int | Scheduler-Modus = SDL_NACHL_MOD |
| STAT_SDL_CAN_ERR_MOD_AKTIV | int | Scheduler-Modus = SDL_CAN_ERR_MOD |
| STAT_LWS_ERR_USPG_AKTIV | int | LWS-Fehler: Kl.30 Fehler |
| STAT_LWS_ERR_I_SENS_AKTIV | int | LWS-Fehler: Sensorstrom ausserhalb der Toleranz |
| STAT_LWS_ERR_ABGL_90GR_AKTIV | int | LWS-Fehler: 90 Grad-Fehler waehrend des Abgleichs |
| STAT_LWS_ERR_90GR_AKTIV | int | LWS-Fehler: 90 Grad-Fehler |
| STAT_LWS_ERR_EEPROM_AKTIV | int | LWS-Fehler: EEPROM-Fehler |
| STAT_LWS_ERR_AD_AKTIV | int | LWS-Fehler: A/D-Wandler Fehler |
| STAT_LWS_ERR_ROM_AKTIV | int | LWS-Fehler: ROM-Checksummenfehler |
| STAT_LWS_ERR_RAM_AKTIV | int | LWS-Fehler: RAM-Check-Fehler |
| STAT_LWS_ERR_ASC_AKTIV | int | LWS-Fehler: Fehlende oder fehlerhafte ASC2 Botschaft |
| STAT_LWS_ERR_CAN_STAND_AKTIV | int | LWS-Fehler: Falscher CAN-Stand |
| STAT_LWS_ERR_ID_AKTIV | int | LWS-Fehler: Zuordnung zum Fahrzeug falsch |
| STAT_LWS_ERR_SW_AKTIV | int | LWS-Fehler: Ungueltiger Programmverlauf |
| STAT_LWS_ERR_LRWPKT_AKTIV | int | LWS-Fehler: Lenkradwinkelgradient zu gross |
| STAT_LWS_ERR_LRWMAX_AKTIV | int | LWS-Fehler: Max. Lenkradeinschlagsbereich ueberschritten |
| STAT_LWS_ERR_STACK_AKTIV | int | LWS-Fehler: Stackfehler |
| STAT_LWS_ERR_WDG_AKTIV | int | LWS-Fehler: Watchdogreset |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sg-online"></a>
### STATUS_SG_ONLINE

Auslesen der analogen Online-Werte des LWS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_INLRW_G_WERT | long | Lenkwinkel Bereich: -1000 bis +1000 [Grad] |
| STAT_INLRWPKT_G_WERT | long | Lenkwinkelgeschwindigkeit Bereich: -2500 bis +2500 [Grad/s] |
| STAT_WVREF_G_WERT | long | Fahrzeuggeschwindigkeit Bereich: 0 bis 350 [km/h] |
| STAT_PRGDLZ_G_WERT | long | Programmdurchlaufzeit Bereich: 0 bis 14000 [Mikro-Sekunden] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sg-virtuell"></a>
### STATUS_SG_VIRTUELL

Auslesen der analogen Online-Werte / virtuelle Sensorik

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_UVRDLVASC_GV_WERT | long | Radgeschwindigkeit links vorne Bereich: 0 bis 350 [km/h] |
| STAT_UVRDRVASC_GV_WERT | long | Radgeschwindigkeit rechts vorne Bereich: 0 bis 350 [km/h] |
| STAT_UVRDLHASC_GV_WERT | long | Radgeschwindigkeit links hinten Bereich: 0 bis 350 [km/h] |
| STAT_UVRDRHASC_GV_WERT | long | Radgeschwindigkeit rechts hinten Bereich: 0 bis 350 [km/h] |
| STAT_UPSIPKTSYN_G_WERT | long | Giergeschwindigkeit Bereich: -1 bis +1 [rad/s] |
| STAT_UAYSYN_G_WERT | long | Querbeschleunigung Bereich: -15 bis +15 [m/s*s] |
| STAT_ULRWSYN_G_WERT | long | synthetische Lenkradwinkel Bereich: -600 bis +600 [Grad] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-lesen"></a>
### ABGLEICH_LESEN

Auslesen der Abgleich-Werte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ABGL_LRW_OFFSET | long | Abgleichwert: LRW-Offset Bereich: 0000 bis FFFF [Digit] |
| ABGL_LWS_ID | int | Abgleichwert: LWS-ID Bereich: 0 bis 255 [Digit] |
| ABGL_FGSTNR | string | Abgleichwert: Fahrgestellnummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Fahrzeugcodierung des LWS5 auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | int | Block der Codierdaten Bereich: derzeit 00 bis 06 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| COD_DATEN | binary | 16 Datenbytes |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierung-check"></a>
### CODIERUNG_CHECK

Checksumme der Codierung des LWS5 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| COD_CHECK | int | Checksumme ueber alle 112 Codierdaten |
| COD_CHECK_HIGH | int | Checksumme ueber alle 112 Codierdaten (High-Byte) |
| COD_CHECK_LOW | int | Checksumme ueber alle 112 Codierdaten (Low-Byte) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kl30"></a>
### STATUS_KL30

Lesen des Unterspannungszählers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KL30_ZAEHLER | int | ausgelesener Unterspannungszähler |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des ROM/RAM bzw. EEPROM-Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | int | Speichersegment Bereich: 01, 03, 04, 05 oder 0B |
| ADRESSE | long | Speicheradresse Bereich: 0x0000-0xFFFF |
| ANZAHL | int | Anzahl der Daten Bereich: 1 bis 256 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATEN | binary | ausgelesene Hex-Daten |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Auslesen der Herstelldaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE4 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-e"></a>
### IDENT_E

Ident-Daten fuer Lenkwinkelsensor 5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR | int | Softwarenummer |
| _TEL_ANTWORT | int | Hex-Antwort von SG |

<a id="job-codierung-schreiben-datei"></a>
### CODIERUNG_SCHREIBEN_DATEI

Beschreiben der Codierdaten des LWS5 ueber Datei

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEI | string | Dateiname z.B.: "/EDIABAS/ECU/LWS5.cod" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-schreiben"></a>
### ABGLEICH_SCHREIBEN

Programmieren der Abgleich-Werte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-vorgeben"></a>
### ABGLEICH_VORGEBEN

Vorgeben der Abgleichwerte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGL_LRW_OFFSET | long | Abgleichwert: LRW-Offset Bereich: 0x0000-0xFFFF |
| ABGL_LWS_ID | int | Abgleichwert: LWS-ID Bereich: 0x00-0xFF |
| ABGL_FGSTNR | string | Abgleichwert: Fahrgestellnummer Bereich: ? String aus ? Zeichen / ACSII / rueckwaerts ? z.B.: ? |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (33 × 2)
- [FORTTEXTE](#table-forttexte) (17 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [STEUERN_DIGITAL](#table-steuern-digital) (9 × 2)
- [ASCII](#table-ascii) (27 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 33 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen / Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe |
| 0x10 | VDO |
| 0x11 | Valeo |
| 0x12 | MBB |
| 0x13 | Kammerer |
| 0x14 | SWF |
| 0x15 | Blaupunkt |
| 0x16 | Philips |
| 0x17 | Alpine |
| 0x18 | Teves |
| 0x19 | Elektromatik Suedafrika |
| 0x20 | Becker |
| 0x21 | Preh |
| 0x22 | Alps |
| 0x23 | Motorola |
| 0x24 | Temic |
| 0x25 | Webasto |
| 0x26 | MotoMeter |
| 0x27 | Delphi PHI |
| 0x28 | DODUCO |
| 0x29 | DENSO |
| 0x30 | NEC |
| 0x31 | DASA |
| 0x32 | Pioneer |
| 0xXY | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 17 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Klemme 30 fehlerhaft |
| 0x02 | Sensorstrom ausserhalb Toleranz |
| 0x03 | 90 Grad-Differenz der Schleifer zu gross (Normalbetrieb) |
| 0x04 | 90 Grad-Differenz der Schleifer zu gross (Abgleichbetrieb) |
| 0x05 | EEPROM defekt |
| 0x06 | AD-Wandler defekt |
| 0x07 | ROM-Checkfehler |
| 0x08 | RAM-Checkfehler |
| 0x09 | keine ASC2-Botschaft |
| 0x0A | CAN-Stand falsch |
| 0x0B | LWS-ID falsch |
| 0x0C | CAN-Bus off |
| 0x0D | Lrw-Gradient zu gross |
| 0x0E | Lrw-Maximum ueberschritten |
| 0x0F | Stack-Fehler / Case-Fehler |
| 0x10 | Watchdog |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0xXY | unbekannte Fehlerart |

<a id="table-steuern-digital"></a>
### STEUERN_DIGITAL

Dimensions: 9 rows × 2 columns

| SIGNAL | BYTE |
| --- | --- |
| B0 | 0x01 |
| KL87 | 0x02 |
| U_CAN | 0x04 |
| U_BAS | 0x08 |
| B4 | 0x10 |
| B5 | 0x20 |
| B6 | 0x40 |
| TAST | 0x80 |
| XY | 0xFF |

<a id="table-ascii"></a>
### ASCII

Dimensions: 27 rows × 2 columns

| ASCII_NR | ASCII_ZCH |
| --- | --- |
| 0x41 | A |
| 0x42 | B |
| 0x43 | C |
| 0x44 | D |
| 0x45 | E |
| 0x46 | F |
| 0x47 | G |
| 0x48 | H |
| 0x49 | I |
| 0x4A | J |
| 0x4B | K |
| 0x4C | L |
| 0x4D | M |
| 0x4E | N |
| 0x4F | O |
| 0x50 | P |
| 0x51 | Q |
| 0x52 | R |
| 0x53 | S |
| 0x54 | T |
| 0x55 | U |
| 0x56 | V |
| 0x57 | W |
| 0x58 | X |
| 0x59 | Y |
| 0x5A | Z |
| 0xXY | ? |
