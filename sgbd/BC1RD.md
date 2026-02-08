# BC1RD.prg

- Jobs: [46](#jobs)
- Tables: [11](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | BC1RD |
| ORIGIN | BMW EE-51 Senger |
| REVISION | 3.00 |
| AUTHOR | delphi Abteilung OS, Alex Franckenstein |
| COMMENT | N/A |
| PACKAGE | 1.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung Dieser Job wird vom EDIABAS automatisch beim erstem Zugriff auf eine SGBD aufgerufen. Bei weiteren Zugriffen auf die selbe SGBD wird dieser Job nicht mehr aufgerufen. in der INITIALISIERUNG werden alle Funktionen aufgerufen, die nur einmal, vor der Kommunikation mit einem SG notwendig sind. Hier : 1. Verbindung zum Interface aufbauen 2. Setzen des Wiederholungszaehlers fuer Fehler (gleich 2) 3. Setzen der SG-Kommunikationsparameter 4. Platz der Antworttelegrammlaenge
- [IDENT](#job-ident) - Identification data
- [READ_SIA_DATA](#job-read-sia-data) - Read Service information
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren Write and verify the coding data
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Beschreiben der FG-Nummer Write the VIN
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen FG-Nummer Read the VIN
- [WRITE_PLIP_CODES](#job-write-plip-codes) - Write the codes and status for a specified plip location
- [READ_PLIP_CODES](#job-read-plip-codes) - Read the codes and status for a specified plip location
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen Sonderfall: Loeschdatum (KW/Jahr) integriert !
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose Sonderfall: Loeschdatum (KW/Jahr) integriert !
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen Info-Speicher ist im Aufbau analog zum Fehlerspeicher Low-Konzept nach Lastenheft Codierung/Diagnose
- [IS_LESEN_ZV](#job-is-lesen-zv) - Infospeicher lesen / Sonderfall: ZV-Ringspeicher Analog zu FS_LESEN gibt es mehrere (15+1) Ergebnis-Saetze Im Satz  1 steht die Information zum letzten ZV-Befehl. Im Satz 15 steht die aelteste Information. Im Satz 16 steht das Ergebnis JOB_STATUS.
- [DWA_DIAGNOSE](#job-dwa-diagnose) - Force DWA Diagnose
- [STATUS_DIGITAL_INPUTS](#job-status-digital-inputs) - Read Digital Input States
- [STATUS_DIGITAL_OUTPUTS](#job-status-digital-outputs) - Read Digital outputs
- [STATUS_ANALOG](#job-status-analog) - Status der Analogsignale des BC1RD
- [STATUS_FZV](#job-status-fzv) - Auslesen FZV-Status Read the FZV State
- [STATUS_RF](#job-status-rf) - Read the RF status
- [STATUS_TILT_SENSOR](#job-status-tilt-sensor) - Read the Tilt sensor status
- [STATUS_LIGHT_OUTPUTS](#job-status-light-outputs) - Read lighting Digital outputs
- [STATUS_LIGHT_INPUTS](#job-status-light-inputs) - Read Lighting Digital Input States
- [STEUERN_IOSTATES](#job-steuern-iostates) - Ansteuern eines digitalen Ein- oder Ausgangs v. BC1RD ! erlaubte Namen des Arguments 'ORT' ueber Tool XTRACT.exe ! Aufruf 'XTRACT [-F] BC1RD.prg'
- [STEUERN_ANALOG](#job-steuern-analog) - Ansteuern eines ANALOGEN Ein- oder Ausgangs ! erlaubte Namen des Arguments 'ORT' ueber Tool XTRACT.exe ! Aufruf 'XTRACT [-F] BC1RD.prg'
- [STEUERN_PWM_OUTPUTS](#job-steuern-pwm-outputs) - Force Digital Output States
- [STEUERN_TILT_SENSOR](#job-steuern-tilt-sensor) - Force Tilt Sensor state
- [STEUERN_HSS](#job-steuern-hss) - Force Tilt Sensor state
- [STEUERN_POTI_LWR](#job-steuern-poti-lwr) - Force POTILWR state
- [LWR_ON](#job-lwr-on) - Switch on LWR2A
- [LWR_OFF](#job-lwr-off) - Switch on LWR2A
- [READ_MANUFACTURER_DATA](#job-read-manufacturer-data) - Auslesen der Herstelldaten
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers des BC1rd Als Argumente wird die Speicherart (Gruppe) und die Adresse der Datenbytes uebergeben.
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Speicherinhalt schreiben
- [WRITE_IDENT](#job-write-ident) - Identification data
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden
- [CLEAR_RF_BUFFERS](#job-clear-rf-buffers) - Clear the RF receive and status buffers
- [START_DIAGNOSTICS](#job-start-diagnostics) - Obtain diagnostic seed and send key to begin diagnostics The ecu will lock if no diagnostic messages have been sent to it for 30 seconds
- [READ_ALARM_MISLOCK](#job-read-alarm-mislock) - Read Alarm mislocks
- [READ_ALARM_TRIGGER](#job-read-alarm-trigger) - Read alarm triggers
- [STEUERN_STEPPER_MOTOR](#job-steuern-stepper-motor) - Force Stepper motor Output State
- [FLASH_ROM_TEST](#job-flash-rom-test) - Self test. Forces a fast Flash-ROM check Wait 2 seconds and read the result from error memory (Stops all ECU tasks for approx 2 seconds)
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Ping message
- [SG_RESET](#job-sg-reset) - Reset the ECU

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

<a id="job-energiesparmode"></a>
### ENERGIESPARMODE

Einstellen des Energiesparmodes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PRODUKTIONSMODE | string | "ein" -&gt; Produktions Mode ein "aus" -&gt; Produktions Mode aus table DigitalArgument TEXT Default: "aus" |
| TRANSPORTMODE | string | "ein" -&gt; Transport Mode ein "aus" -&gt; Transport Mode aus table DigitalArgument TEXT Default: "aus" |
| WERKSTATTMODE | string | "ein" -&gt; Werkstatt Mode ein "aus" -&gt; Werkstatt Mode aus table DigitalArgument TEXT Default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | real | a) Zeit nach der das Steuergerät einschläft Bereich   : 0.5 bis 20.0 [Sekunden] Auflösung : 0.5 [Sekunden] =&gt; zeitgesteuerter Power-Down (0x9B) wird aktiviert b) Default: (Es wird kein Argument übergeben!) =&gt; normaler Power-Down (0x9D) wird aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung Dieser Job wird vom EDIABAS automatisch beim erstem Zugriff auf eine SGBD aufgerufen. Bei weiteren Zugriffen auf die selbe SGBD wird dieser Job nicht mehr aufgerufen. in der INITIALISIERUNG werden alle Funktionen aufgerufen, die nur einmal, vor der Kommunikation mit einem SG notwendig sind. Hier : 1. Verbindung zum Interface aufbauen 2. Setzen des Wiederholungszaehlers fuer Fehler (gleich 2) 3. Setzen der SG-Kommunikationsparameter 4. Platz der Antworttelegrammlaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | Werte: 0 = Fehler bei der Initialisierung Werte: 1 = Initialisierung erfolgreich durchgefuehrt |

<a id="job-ident"></a>
### IDENT

Identification data

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer BMW Part Number |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW Week of manufacture |
| ID_DATUM_JAHR | int | Herstelldatum Jahr Year of manufacture |
| ID_SW_NR | string | Software version |
| ID_LIEF_NR | int | Lieferanten-Nummer Supplier code |
| ID_LIEF_TEXT | string | Lieferanten-Text Supplier Name |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) 1, If AIF data is available |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-read-sia-data"></a>
### READ_SIA_DATA

Read Service information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| TOTAL_DISTANCE_WERT | long | Total Distance |
| TOTAL_DISTANCE_EINH | string | Total distance units km |
| CONSUMED_LITRES_SINCE_SERVICE_WERT | long | Count of litres |
| LAST_SERVICE_TYPE_OIL | int | 1 = Last service was an oil service, 0 = not |
| LAST_SERVICE_TYPE_INSPECTION | int | 1 = Last service was an inspection, 0 = not |
| TIME_SINCE_INSPECTION_SERVICE_WERT | long | Time count (at/since?) inspection |
| TIME_SINCE_INSPECTION_SERVICE_EINH | string | Einheit = Tage, days |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und verifizieren Write and verify the coding data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write coding data telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write coding data response cod_schreiben antwort |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read coding data response cod_lesen antwort |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Beschreiben der FG-Nummer Write the VIN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Vehicle ID number Fahrgestellnummer 7 or 8 character string - if 8 characters the last is ignored |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write VIN Telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write VIN response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read VIN response |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Auslesen FG-Nummer Read the VIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer Last digits of the VIN |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-write-plip-codes"></a>
### WRITE_PLIP_CODES

Write the codes and status for a specified plip location

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PLIP | unsigned int | Plip location to write 1 - 4 |
| CIPHER_KEY | string | Cipher code for required plip location 16 characters ascii This is the ascii representation of the 8 hex characters used |
| WINDOW_KEY | string | Window code for required plip location 6 characters ascii This is the ascii representation of the 3 hex characters used |
| BASE_CODE_KEY | string | Base code for required plip location 6 characters ascii This is the ascii representation of the 3 hex characters used |
| ENABLE | unsigned int | 0 = plip disabled, 1 = plip enabled |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write PLIP telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write PLIP response packet |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read PLIP response packet |

<a id="job-read-plip-codes"></a>
### READ_PLIP_CODES

Read the codes and status for a specified plip location

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PLIP | unsigned int | Plip location to read 1 - 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CIPHER_KEY | string | Cipher code for required plip location |
| WINDOW_KEY | string | Window code for required plip location |
| BASE_CODE_KEY | string | Base code for required plip location |
| ENABLED | unsigned int | 0 = plip disabled, 1 = plip enabled |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen Sonderfall: Loeschdatum (KW/Jahr) integriert !

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LOESCHDATUM_KW | int | aktuelle Kalenderwoche beim Loeschen des Fehlerspeichers |
| LOESCHDATUM_JAHR | int | aktuelles Kalenderjahr beim Loeschen des Fehlerspeichers |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose Sonderfall: Loeschdatum (KW/Jahr) integriert !

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
| F_LOESCHDATUM_KW | int | Loeschdatum des Fehlerspeichers (KW) |
| F_LOESCHDATUM_JAHR | int | Loeschdatum des Fehlerspeichers (Jahr) |
| _TEL_ANTWORT0 | binary | 0. Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | 1. Hex-Antwort von SG |

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen Info-Speicher ist im Aufbau analog zum Fehlerspeicher Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_HEX_CODE | binary | Infodaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Infoort momentan identisch Infobyte |
| F_ORT_TEXT | string | Infoort als Text table IOrtTexte ORTTEXT |
| F_HFK | int | Infohaeufigkeit Bereich: 0 - 31 |
| F_ART_ANZ | int | Anzahl der Infoarten Bereich: immer 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Bereich: immer 0 |
| F_ART1_NR | int | 1. (einzige) Infoart Bereich: 0, 1 |
| F_ART1_TEXT | string | 1. (einzige) Infoart als Text table IArtTexte ARTTEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen-zv"></a>
### IS_LESEN_ZV

Infospeicher lesen / Sonderfall: ZV-Ringspeicher Analog zu FS_LESEN gibt es mehrere (15+1) Ergebnis-Saetze Im Satz  1 steht die Information zum letzten ZV-Befehl. Im Satz 15 steht die aelteste Information. Im Satz 16 steht das Ergebnis JOB_STATUS.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| I_ZEIGER_RS | int | Zeigerwert des ZV-Ringspeichers Bereich: 0-28 |
| I_HEX_CODE_RS | binary | Ringspeicherdaten (alle 15 ZV-Befehle) als Hexcode |
| I_HEX_CODE | binary | Ringspeicherdaten (einzelner ZV-Befehl) als Hexcode |
| I_ZV_BEFEHL_WERT | int | zuletzt ausgefuehrter ZV-Befehl moegliche Werte: 0=SER, 1=VR, 2=ER, 3=ZS, 4=ES |
| I_ZV_BEFEHL | string | zuletzt ausgefuehrter ZV-Befehl Bereich: SER, VR, ER, ZS, ES |
| I_SCHLOSS_FT | int | Fahrerschloss Bereich: 0, wenn FALSE / 1, wenn TRUE |
| I_SCHLOSS_BT | int | Beifahrerschloss Bereich: 0, wenn FALSE / 1, wenn TRUE |
| I_FB | int | Fernbedienung Bereich: 0, wenn FALSE / 1, wenn TRUE |
| I_CL | int | Centerlock Bereich: 0, wenn FALSE / 1, wenn TRUE |
| I_CS | int | Crash-Sensor Bereich: 0, wenn FALSE / 1, wenn TRUE |
| I_4KMH | int | groesser 4 km/h Bereich: 0, wenn FALSE / 1, wenn TRUE |
| I_EWS | int | Elektronische Wegfahrsperre Bereich: 0, wenn FALSE / 1, wenn TRUE |
| I_FB_2MIN | int | 2 Minuten nach Fernbedienung entriegeln Bereich: 0, wenn FALSE / 1, wenn TRUE |

<a id="job-dwa-diagnose"></a>
### DWA_DIAGNOSE

Force DWA Diagnose

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARAM | int | 0: Hold Stored Values (of Response Data Byte 4) 1: Delete Stored Values (of Response Data Byte 4) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DWA_TRIG_MHK | int | DWA-Trigger Motorhaubenkontakt 1: Active / 0: Inactive |
| DWA_TRIG_HKK | int | DWA-Trigger Heckklappenkontakt 1: Active / 0: Inactive |
| DWA_TRIG_KLR_15 | int | DWA-Trigger KLR,15 1: Active / 0: Inactive |
| DWA_TRIG_TKFT | int | DWA-Trigger Türkontakt Fahrerseite 1: Active / 0: Inactive |
| DWA_TRIG_TKBT | int | DWA-Trigger Türkontakt Beifahrer 1: Active / 0: Inactive |
| DWA_TRIG_NG | int | DWA-Trigger Neigungsgeber 1: Active / 0: Inactive |
| DWA_TRIG_US | int | DWA-Trigger Ultraschall INRS 1: Active / 0: Inactive |
| DWA_TRIG_PANIC | int | DWA-Trigger Panic Mode 1: Active / 0: Inactive |
| DWA_TRIG_SCHLOSS_FT | int | DWA-Trigger Schloss (ER&VR) 1: Active / 0: Inactive |
| DWA_TRIG_SCHLOSS_BT | int | DWA-Trigger ER&VR Schloss Beifahrertüre 1: Active / 0: Inactive |
| DWA_TRIG_MUW_VR | int | DWA-Trigger MUW Slave 1 1: Active / 0: Inactive |
| DWA_TRIG_MUW_HR | int | DWA-Trigger MUW Slave 2 1: Active / 0: Inactive |
| DWA_TRIG_MUW_HL | int | DWA-Trigger MUW Slave 3 1: Active / 0: Inactive |
| DWA_TRIG_MUW_VL | int | DWA-Trigger MUW Master 1: Active / 0: Inactive |
| DWA_STAT_DWA | int | Status DWA 1: Armed / 0: Disarmed |
| DWA_STAT_ALARM | int | DWA Alarm 1: Activated / 0: Not activated |
| DWA_HKK_enabled | int | HKK Status 1: enabled / 0: disabled |
| DWA_NG_enabled | int | NG Status 1: enabled / 0: disabled |
| DWA_INRS_enabled | int | INRS (US or MUW) Status 1: enabled / 0: disabled |
| DWA_SIGNAL_HKK | int | HKK Trigger Signal 1: high / 0: low |
| DWA_SIGNAL_NG | int | NG Trigger Signal 1: high / 0: low |
| DWA_SIGNAL_INRS | int | US or MUW Trigger Signal 1: high / 0: low |
| DWA_STORED_NG | int | Stored NG Alarm Trigger 1: Active / 0: Inactive |
| DWA_STORED_INRS | int | Stored INRS Alarm Trigger 1: Active / 0: Inactive |
| DWA_STORED_MUW_VR | int | Stored MUW VR Alarm Trigger 1: Active / 0: Inactive |
| DWA_STORED_MUW_HR | int | Stored MUW VR Alarm Trigger 1: Active / 0: Inactive |
| DWA_STORED_MUW_HL | int | Stored MUW VR Alarm Trigger 1: Active / 0: Inactive |
| DWA_STORED_MUW_VL | int | Stored MUW VR Alarm Trigger 1: Active / 0: Inactive |
| BYTE1 | int | Byte 1 |
| BYTE2 | int | Byte 2 |
| BYTE3 | int | Byte 3 |
| BYTE4 | int | Byte 4 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-digital-inputs"></a>
### STATUS_DIGITAL_INPUTS

Read Digital Input States

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_DIP_RF_CODE_LOGIC_ON | int | RF Code input 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_DIPPED_BEAM_SW_ON | int | Switch input dipped beam 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_PASS_WIN_DOWN_SW_ON | int | Switch input passenger window down 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_FT_WASH_PUMP_ON | int | Switch input front washer pump active 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_COL_SW_2_ON | int | Wiper switch 2 to activate front wipers 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_DRV_WIN_UP_SW_ON | int | Switch input driver window up 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RR_WIPER_SW_ON | int | Rear wiper switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RR_WASH_PUMP_ON | int | Switch for rear washer pump active 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_BRAKE_SW_ON | int | Switch input brake pedal 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_PASS_WIN_UP_SW_ON | int | Switch input passenger window up 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_BOOT_HANDLE_SW_ON | int | Switch input boot release motor 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_BONNET_SW_ON | int | Switch to detect the bonnet open 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_DRV_WIN_DOWN_SW_ON | int | Switch input driver window down 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_ULTRASONIC_IN_ON | int | Ultrasonic alarm activated 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_ALARM_TILT_SW_ON | int | Alarm tilt sensor This output cannot be read from using read digital inputs command |
| STAT_DIP_AUX_SW_ON | int | Auxiliary monitor from main ignition switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_INT_LGT_SW_ON | int | Switch input interior light 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_POSN_LGT_SW_ON | int | Switch input position lights 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_HT_RR_WIN_SW_ON | int | Switch input heated rear window 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_INERTIA_SENSE_ON | int | Inertia sensor to detect unusual stop conditions 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_BOOT_OPEN_SW_ON | int | Switch to detect the boot open 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_COL_SW_1_ON | int | Wiper switch 1 to activate front wipers 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RECIRC_SW_ON | int | Toggles between recirc and fresh 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_FT_FOG_SW_ON | int | Switch input front fog switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_MASTER_UNLK_SW_ON | int | Switch input master unlock 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_MASTER_LK_SW_ON | int | Switch input master lock 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_DRV_KEY_SW_UNLK_ON | int | Driver key switch unlock 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_PASS_DOOR_OPEN_ON | int | Passenger door open 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_PASS_KEY_SW_UNLK_ON | int | Passenger key switch unlock 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_DRV_KEY_SW_LK_ON | int | Driver key switch lock 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_DRV_DOOR_OPEN_ON | int | Driver door open 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_PASS_KEY_SW_LK_ON | int | Passenger key switch lock 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_FT_WIPER_PARK_ON | int | Front wiper at the parked position 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RR_WIPER_PARK_ON | int | Rear wiper at the parked position 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_AC_SWITCH_ON | int | Switch input air conditioning 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RR_FOG_SW_ON | int | Switch input rear fog switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_HT_FT_SCR_SW_ON | int | Heated front screen switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_HT_FT_WIN_LED_ON | int | Heated front screen LED 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RR_WIPER_RLY_ON | int | Rear wiper relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_HEATED_RR_WIN_RLY_ON | int | Heated rear window relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_AC_LED_ON | int | Air conditioning LED 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_BOOT_RELEASE_ON | int | Boot release motor 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_DRV_WIN_UP_ON | int | Driver window up 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_DRV_WIN_DOWN_ON | int | Driver window down 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_PASS_WIN_UP_ON | int | Passenger window up 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_PASS_WIN_DOWN_ON | int | Passenger window down 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_SOUND_ALARM_ON | int | BBS version alarm 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_BBS_ARM_DISARM_ON | int | BBS arm/disarm 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_COMMON_LOCK_RLY_ON | int | Common relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_SUPER_LOCK_RLY_ON | int | Super lock relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_REST_LOCK_RLY_ON | int | Rest lock relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_DRV_LOCK_RLY_ON | int | Driver lock relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_NO_PLATE_LGT_ON | int | Number plate light 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_ROTARY_SUPPLY_ON | int | Supply to the rotary switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_HEATED_FT_WIN_RLY_ON | int | Heated front screen relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_FT_FOG_LGT_RLY_ON | int | Front fog relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_FT_WIPER_PARK_RUN_ON | int | Front wiper slow park run relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_BLOWER_ENABLE_ON | int | Enable the blower motor 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RECIRC_LED_ON | int | Indicator for the recirc on 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_HT_RR_WIN_LED_ON | int | Heated rear window LED 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RR_FOG_LED_ON | int | Rear fog LED 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_ALARM_LED_ON | int | Alarm LED output 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_FT_WIPER_SLOW_FAST_ON | int | Front wiper slow fast relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_PWR_WASH_RLY_ON | int | Powerwash relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_SW_ST_752 | int | Status of CHMSL Driver 1 normale Operation / 0 Fehler |
| STAT_SW_FAULT_3408 | int | Not used |
| STAT_SW_TRAILER_RXD | int | Receive signal from trailer bus |
| STAT_SW_RF_CODE | int | Dataline from Remotecontrol |
| STAT_SW_MCD_DO | int | Data line from MCD Driver |
| STAT_SW_EE_DO | int | Dataline from EEPROM |
| STAT_SW_DVRFT | int | Diag central door locking Common lock driver door (DiagVerRiegelnFahrerTuer Fahrer/Beif) |
| STAT_SW_DER | int | Diag central door locking Common unlock motor (DiagmotorEntRiegeln Fahrer/Beif) |
| STAT_SW_DZS | int | Diag central door locking Superlock passenger/fuel(DiagmotorZentralSichern) |
| STAT_SW_DVR | int | Diag central door locking Lock motor (DiagmotorVerRiegeln) |
| STAT_SW_S56B | int | Dipped beam light |
| STAT_SW_SFBA | int | Passenger Window Down Switch (SchalterFensterheberBeifahrerAuf) |
| STAT_SW_SWA_F | int | Front Washer (1) Switch (SchalterWaschAnlageFront) |
| STAT_SW_SW2 | int | Front Wiper Switch 2 (SchalterWischer ST1, ST2, INT kodiert) |
| STAT_SW_SFFZ | int | Driver Window Up Switch (SchalterFensterheberFahrerZu) |
| STAT_SW_SFHZ | int | Rear Window Up Switch (SchalterFensterheberHintenZu) |
| STAT_SW_SFHA | int | Rear Window Down Switch (SchalterFensterheberHintenAuf) |
| STAT_SW_SWR | int | Switch Wiper Rear |
| STAT_SW_HFK | int | Glove Compartment Switch (not used) (HandschuhFachKontakt (entfaellt)) |
| STAT_SW_SWA_H | int | Rear Washer (2) Switch (SchalterWaschAnlageHeck) |
| STAT_SW_S_BLS | int | Brake Switch (BremsLichtSchalter) |
| STAT_SW_SFBZ | int | Passenger Window Up Switch (SchalterFensterheberBeifahrerZu) |
| STAT_SW_TOEHK | int | Boot Handle Switch (TasterOEffnenHeckKlappe) |
| STAT_SW_MHK | int | Bonnet Open Switch (MotorHaubenKontakt) |
| STAT_SW_SFFA | int | Driver Window Down Switch (SchalterFensterheberFahrerAuf) |
| STAT_SW_INRS | int | Ultrasonics in (InNenRaumschutzSignal) |
| STAT_SW_NG | int | Tilt Trigger (NeigungsgeberSignal) |
| STAT_SW_R | int | Power INPUT (Klemme R) |
| STAT_SW_T_IB | int | Interior Light switch (Taster InnenBeleuchtung) |
| STAT_SW_S58 | int | Position Lamp Switch (Schalter Standlicht) |
| STAT_SW_T_HHS | int | Heated Rear Window Switch (Taster HeizbareHeckScheibe) |
| STAT_SW_CS | int | Inertia Switch (Traegheitsschalter) |
| STAT_SW_HKK | int | Boot Open Switch (HeckKlappenKonkakt) |
| STAT_SW_SW1 | int | Front Wiper Switch 1 (SchalterWischer ST1, ST2, INT kodiert) |
| STAT_SW_T_UMLUFT | int | Recirc Switch (Taster Frischluft/Umluft) |
| STAT_SW_S55V | int | Front Fog Switch (Schalter Nebelscheinwerfer) |
| STAT_SW_TZE | int | Master Unlock Switch (TasterZentralverriegelungEntriegeln) |
| STAT_SW_S49W | int | Hazard Switch (Schalter Warnblinkanlage) |
| STAT_SW_TZV | int | Master Lock Switch (TasterZentralverriegelungVerriegeln) |
| STAT_SW_ERFT | int | Driver Key Unlock Switch (EntRiegelnFahrerTuere) |
| STAT_SW_TKBT | int | Passenger Door Open Switch (TuerKontaktBeifahrerTuere) |
| STAT_SW_ERBT | int | Pass Key Unlock Switch (EntRiegelnBeifahrerTuere) |
| STAT_SW_VRFT | int | Driver Key Lock Switch (VerRiegelnFahrerTuere) |
| STAT_SW_TKFT | int | Driver Door Open Switch (TuerKontaktFahrerTuere) |
| STAT_SW_VRBT | int | Pass Key Lock Switch (VerRiegelnBeifahrerTuere) |
| STAT_SW_RSK_V | int | Front Wiper Park Switch (RueckStellKontakt wischer Vorn) |
| STAT_SW_RSK_H | int | Rear Wiper Park Switch (RueckStellKontakt wischer Hinten) |
| STAT_SW_S56A_D_FLASH | int | Main Flash Switch (Status Flash) |
| STAT_SW_S56A_D_MAINBEAM | int | Main Flash Switch (Status Mainbeam) |
| STAT_SW_S49L_R_RIGHT | int | Indicator Switch right (Schalter Fahrtrichtungsanz rechts) |
| STAT_SW_S49L_R_LEFT | int | Indicator Switch left (Schalter Fahrtrichtungsanz links) |
| STAT_SW_T_AC_EIN | int | Aircon Switch (Taster AirCon EIN) |
| STAT_SW_S55H | int | Rear Fog Switch (Schalter Nebenschlussleuchte) |
| STAT_SW_T_HFS | int | Heated Front Screen Switch (Taster HeizbareFrontScheibe) |
| STAT_SW_D_MFL12V | int | Rotary Coupler Supply (Versorgung MultiFunktionsLenkrad 12V) |
| STAT_SW_D_HFS_LED | int | Heated Front Screen LED (HeizbareFrontScheibe LED) |
| STAT_SW_D_HFS_RA | int | Heated Front Screen Relay (HeizbareFrontScheibe Relaisansteuerung) |
| STAT_SW_D_55V_RA | int | Front Fog Relay (Nebelscheinwerfer Relaisansteuerung) |
| STAT_SW_D_56Z_RA | int | Auxiliary Lamps Relay (Zusatzscheinwerfer Relaisansteuerung) |
| STAT_SW_D_WI_H | int | Rear Wiper Relay (WIscher Hinten Relaisansteuerung) |
| STAT_SW_D_WI1 | int | Front Wiper Run Park Relay (Wischer Vorne Aus/An Relaisansteuerung) |
| STAT_SW_D_HHS_RA | int | Heated Rearscreen Relay (HeizbareHeckScheibe RelaisAnsteuerung) |
| STAT_SW_D_GEBL_RA | int | Heater Blower Relay (heizGEBLaese RelaisAnsteuerung) |
| STAT_SW_D_UML_LED | int | Recirc LED (UMLuft LED) |
| STAT_SW_D_HHS_LED | int | Heated Rear Screen LED (HeizbareHeckScheibe LED) |
| STAT_SW_D_55_LED | int | Rear Fog LED (Nebelschlusslicht LED) |
| STAT_SW_D_DWALED | int | Alarm System LED (DiebstahlWarnAnlageLED) |
| STAT_SW_D_AC_LED | int | Aircon LED (AirCon LED) |
| STAT_SW_D_WI2 | int | Front Wiper Fast Slow Relay (Wischer Vorne Stufe 1/Stufe 2 Relaisans) |
| STAT_SW_D_SRA | int | Headlamp Power Wash Relay (ScheinwerferReinigungsAnlageRelaisanst) |
| STAT_SW_EN_5V | int |  |
| STAT_SW_EN_PU_DIRIND | int |  |
| STAT_SW_EN_5VPU | int |  |
| STAT_SW_MUX_A0 | int |  |
| STAT_SW_MUX_A1 | int |  |
| STAT_SW_MUX_A2 | int |  |
| STAT_SW_EN_3408 | int | Not used |
| STAT_SW_TRAILER_TXD | int | Transmit signal from trailer bus |
| STAT_SW_CLA5440 | int | current limit for BTS driver (high or low current value on 1/0) |
| STAT_SW_HC238_A0 | int | ELMOS select |
| STAT_SW_HC238_A1 | int | ELMOS select |
| STAT_SW_HC238_A2 | int | ELMOS select |
| STAT_SW_MFFH | int | Window Motor Driversite rear (MotorFensterheberFahrerHinten) |
| STAT_SW_EN_STP | int | Enable Stepper motor driver |
| STAT_SW_MFBH | int | Window Motor Passengersite rear (MotorFensterheberBeifahrerHinten) |
| STAT_SW_MCD_DI | int | Dataline to MCD Driver |
| STAT_SW_CS_STP | int | CS line to Steppermotor driver |
| STAT_SW_56AL | int | LH Main Beam (Fernlicht links) |
| STAT_SW_56AR | int | RH Main Beam (Fernlicht rechts) |
| STAT_SW_49VR | int | Right Front DI (Blinker vorne rechts) |
| STAT_SW_49HR_49ZR | int | Right DI Repeater (Zusatzblinker rechts) |
| STAT_SW_58VR_58IVR_58IHR | int | Right Rear/Front Side Marker/Right Front Pos. Lamp (Seiten-Markierungsl. h/v r/Standl. v l) |
| STAT_SW_58HL | int | Left Rear Position Lamp (Schlusslicht links hinten) |
| STAT_SW_INRS_12V__NG_12V | int | Switched +12V Supply 1 (tilt sensor) (Neigungsgeber 12V Versorgung) |
| STAT_SW_ATMEL_CLK | int | Atmel Clock line |
| STAT_SW_ATMEL_DIDO | int | Atmel Data in and Data out line |
| STAT_SW_WD_TRIGGER | int | Watch dog trigger signal |
| STAT_SW_MERHK | int | Boot Release Actuator (MotorEntRiegelnHeckKlappe) |
| STAT_SW_MFFZ | int | Driver Window Up (MotorFensterheberFahrerZu) |
| STAT_SW_MFFA | int | Driver Window Down (MotorFensterheberFahrerAuf) |
| STAT_SW_MFBZ | int | Passenger Window Up (MotorFensterheberBeifahrerZu) |
| STAT_SW_MFBA | int | Passenger Window Down (MotorFensterheberBeifahrerAuf) |
| STAT_SW_SIRENE | int | BBUS Sound Alarm (Steuersignal DWA-Sirene Alarm) |
| STAT_SW_STDWA | int | BBUS Arm/Disarm (Sirene schaerfen/entsch.(StatDWA)) |
| STAT_SW_EE_CLK | int | Clock for EEPROM Interface |
| STAT_SW_EE_DI | int | Data for EEPROM Interface |
| STAT_SW_EE_CS | int | Chip select for EEPROM Interface |
| STAT_SW_MER | int | Driver/Passenger Common (MotorEntRiegeln Fahrertuere/Beif) |
| STAT_SW_MZS | int | Fuel Superlock/Passenger Superlock (MotorZentralSichern Tankkl/Beift) |
| STAT_SW_VS_PULL_EIN | int | Open Load Detection for BTS |
| STAT_SW_EN_EKS | int | Pullup pinch protection (Pullup Einklemmschutz) |
| STAT_SW_EN_PU | int | RSK Pullup (Klemme 30 Pullup) |
| STAT_SW_MVR | int | Pass Rest Lock (MotorVerRiegeln Beifahrertuere) |
| STAT_SW_MVRFT | int | Driver Door Lock (MotorVerRiegelnFahrerTuere) |
| STAT_SW_MCD_SCLK | int | MCD clock |
| STAT_SW_IB | int | Interior Light (InnenBeleuchtung) |
| STAT_SW_56BL | int | LH Dipped Beam (Abblendlicht links) |
| STAT_SW_54M | int | Middle Break light (Bremslicht Mitte) |
| STAT_SW_56BR | int | RH Dipped Beam (Abblendlicht rechts) |
| STAT_SW_KRB | int | Boot Lamp (KofferRaumBeleuchtung) |
| STAT_SW_VA | int | Map Light (VerbrAbsch(Lesel+Schminksp+Hndsf)) |
| STAT_SW_58K | int | Number Plate Lamps (Kennzeichenleuchte) |
| STAT_SW_DWA_LED_ST10 | int | Alarm System LED (DiebstahlWarnAnlage LED) |
| STAT_SW_54R | int | Right Brake Light (Bremslicht rechts) |
| STAT_SW_54L | int | Left Brake Light (Bremslicht links) |
| STAT_SW_55HL | int | Left Rear Fog Light (Nebelschlusslicht links) |
| STAT_SW_49VL | int | Left Front DI (Blinker vorne links) |
| STAT_SW_55HR | int | Right Rear Fog Light (Nebelschlusslicht rechts) |
| STAT_SW_49HL_49ZL | int | Left DI Repeater (Zusatzblinker links) |
| STAT_SW_58VL_58IVL_58IHL | int | Left Rear/Fr Side Mark/L Fr Pos.Lamp (Seiten-Mark.l h/v l/Standl. v l) |
| STAT_SW_58HR | int | Right Rear Position Lamp (Schlusslicht rechts hinten) |
| STAT_SW_MFL12V | int | Rotary Coupler Supply (Versorgung MultiFunktionsLenkrad) |
| STAT_SW_HFS_LED | int | Heated Front Screen LED (HeizbareFrontScheibe LED) |
| STAT_SW_HFS_RA | int | Heated Front Screen Relay (HeizbareFrontScheibe Relaisansteuerung) |
| STAT_SW_55V_RA | int | Front Fog Relay (Nebelscheinwerfer Relaisansteuerung) |
| STAT_SW_56Z_RA | int | Auxiliary Lamps Relay (Zusatzscheinwerfer Relaisansteuerung) |
| STAT_SW_WI_H | int | Rear Wiper Relay (Wischer Hinten Relaisansteuerung) |
| STAT_SW_WI1 | int | Front Wiper Run Park Relay (Wischer Vorne Aus/An Relaisansteuerung) |
| STAT_SW_HHS_RA | int | Heated Rear Screen Relay (HeizbareHeckScheibe RelaisAnsteuerung) |
| STAT_SW_GEBL_RA | int | Heater Blower Relay (Heizgeblaese Relaisansteuerung) |
| STAT_SW_UML_LED | int | Recirc LED (Umluft LED) |
| STAT_SW_HHS_LED | int | Heated Rear Screen LED (HeizbareHeckScheibe LED) |
| STAT_SW_55_LED | int | Rear Fog LED (Nebelschlusslicht LED) |
| STAT_SW_DWALED | int | Alarm System LED (DiebstahlWarnAnlage LED) |
| STAT_SW_AC_LED | int | Aircon LED (Klimaanlage LED) |
| STAT_SW_WI2 | int | Front Wiper Fast Slow Relay (Wischer Vorne Stufe 1/Stufe 2 Relaisans) |
| STAT_SW_SRA | int | Headlamp Power Wash Relay (ScheinwerferReinigAnlage Relaisanst) |
| STAT_SW_KBUS_R | int | Aux state received by K-Bus |
| STAT_SW_KBUS_15 | int | Contact 15 state received by K-Bus |
| STAT_SW_ENGINERUNNING | int | State of motor |
| STAT_SW_EWSMANIPULATED | int | EWS manipulation detected |
| STAT_SW_CVM_FA | int | Convertable Open Window (Cabrio: Fenster auf) |
| STAT_SW_CVM_FZ | int | Convertable Close Window (Cabrio: Fenster zu) |
| STAT_SW_CVM_VKA | int | Convertable Open Roof (Cabrio: VerdeckKlappeAuf) |
| STAT_SW_CVM_TOPCLOSED | int | Convertable Close Roof (Cabrio: VerdeckKlappeAuf) |
| STAT_SW_KL_R | int | Klemme Radio |
| STAT_SW_KL15 | int | Klemme 15 |
| STAT_SW_KL50 | int | Klemme 50 |
| STAT_SW_KL58 | int | Park Light Switch (Standlichtschalter von LSZ) |
| STAT_SW_EWS_FREE | int | Immo release (ElektronischeWeckfahrSperre freigegeben) |
| STAT_SW_EWS_KEY | int | Immo valid key available (ElektronischeWeckfahrSperre gueltiger Schluessel steckt) |
| STAT_SW_KB_CS | int | Crash signal by K-Bus (Crash-Sensor per Telegr.) |
| STAT_SW_RDC | int | Flat Tire |
| STAT_SW_CSMODE | int | Crash-Mode active |
| STAT_SW_DIAGMODE | int | Diagnose-Mode active |
| STAT_SW_ZV | int | Central Door Lock: Locked |
| STAT_SW_ZS | int | Central Door Lock: Superlock |
| STAT_SW_SER | int | Central Door Lock: Selectiv unlock |
| STAT_SW_WB | int | Alarm System: Turn indicator flash for optical acknowledge |
| STAT_SW_OA | int | Alarm System: Turn indicator flash for optical alarm |
| STAT_SW_ES | int | Central Door Lock: Unlocked |
| STAT_SW_QFFZ | int | Acknowledge Driver Front Window is Closes |
| STAT_SW_QFBZ | int | Acknowledge Passenger Front Window is Closes |
| STAT_SW_QFFHZ | int | Acknowledge Driver Rear Window is Closes |
| STAT_SW_QFBHZ | int | Acknowledge Passenger Rear Window is Closes |
| STAT_SW_SOFTON | int | Light on or ramp up light in process |
| STAT_SW_KB_FSHD | int | Sunroof unlocked |
| STAT_SW_KB_KOE | int | Comfort Open |
| STAT_SW_KB_KS | int | Comfort Close |
| STAT_SW_FB_BAT | int | Remote control: Low Battery |
| STAT_SW_FB_NR | int | Remote Control: Valid Key and ID available |
| STAT_SW_FB_SEND_L | int | Remote key # Bit 0 |
| STAT_SW_FB_SEND_H | int | Remote key # Bit 1 |
| STAT_SW_FB_VR | int | Remote Control: Lock |
| STAT_SW_FB_ER | int | Remote Control: Unlock |
| STAT_SW_FB_HK | int | Remote Control: Trunk |
| STAT_SW_KB_VKER | int | Not used |
| STAT_SW_SEND_L | int | Remote Control: ID Low Bit |
| STAT_SW_SEND_H | int | Remote Control: ID High Bit |
| STAT_SW_FZVSIG | int | Indication that any remote control signal was received |
| STAT_SW_FZVKEY | int | Remote Control: Signal received |
| STAT_SW_TASTE1 | int | Remote Control: Lock |
| STAT_SW_TASTE2 | int | Remote Control: Unlock |
| STAT_SW_TASTE3 | int | Remote Control: Trunk |
| STAT_SW_FUINIT | int | Remote Control: Key Init possible |
| STAT_SW_LOBAT1 | int | Remote Control: Key 1 low battery |
| STAT_SW_LOBAT2 | int | Remote Control: Key 2 low battery |
| STAT_SW_LOBAT3 | int | Remote Control: Key 3 low battery |
| STAT_SW_LOBAT4 | int | Remote Control: Key 4 low battery |
| STAT_SW_FSIB | int | FS Interior light |
| STAT_SW_FSAHK | int | FS Trunk |
| STAT_SW_ZV1FS | int | FS Central door locking: Unlock |
| STAT_SW_ZV0FS | int | FS Central door locking: Lock |
| STAT_DIP_POLL_SENSE_ON | int | Not existing: only for backwardscompatibility to BC1 SGBD |
| STAT_DIP_POLICE_SW_ON | int | Not existing: only for backwardscompatibility to BC1 SGBD |
| STAT_DIP_BOOT_RELEASE_MONITOR_ON | int | 0 wenn einschalten / 1 wenn ausschalten |
| STAT_DIP_RECIRC_MONITOR_ON | int | Not existing: only for backwardscompatibility to BC1 SGBD |
| STAT_DIP_RECIRC_ERROR_ON | int | Not existing: only for backwardscompatibility to BC1 SGBD |
| STAT_DIP_BOOT_REL_STATUS_ON | int | Monitor the boot release 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_LH_LATCH_ON | int | Not existing: only for backwardscompatibility to BC1 SGBD |
| STAT_DIP_RH_LATCH_ON | int | Not existing: only for backwardscompatibility to BC1 SGBD |
| STAT_DIP_KEY_IN_SW_ON | int | Switch input to detect key in ignition 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_WWA | int | Input from level switch 1 wenn einschalten / 0 wenn ausschalten |

<a id="job-status-digital-outputs"></a>
### STATUS_DIGITAL_OUTPUTS

Read Digital outputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_DOP_DRV_LOCK_RLY_ON | int | Driver lock relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_SUPER_LOCK_RLY_ON | int | Super lock relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_COMMON_LOCK_RLY_ON | int | Common relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_REST_LOCK_RLY_ON | int | Rest lock relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_PASS_WIN_DOWN_ON | int | Passenger window down 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_PASS_WIN_UP_ON | int | Passenger window up 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_DRV_WIN_DOWN_ON | int | Driver window down 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_DRV_WIN_UP_ON | int | Driver window up 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_HT_RR_WIN_LED_ON | int | Heated rear window LED 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_HT_FT_WIN_LED_ON | int | Heated front screen LED 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_AC_LED_ON | int | Air conditioning LED 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RECIRC_LED_ON | int | Indicator for the recirc on 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_FT_WIPER_PARK_RUN_ON | int | Front wiper slow park run relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_HEATED_RR_WIN_RLY_ON | int | Heated rear window relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_HEATED_FT_WIN_RLY_ON | int | Heated front screen relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_BBS_ARM_DISARM_ON | int | BBS arm/disarm 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_SOUND_ALARM_ON | int | BBS version alarm 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_FT_WIPER_SLOW_FAST_ON | int | Front wiper slow fast relay 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_BOOT_RELEASE_ON | int | Boot release motor 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RECIRC_CTL1_ON | int | Control 1 recirc (fresh) operation 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RECIRC_CTL2_ON | int | Control 2 recirc (recirc) operation 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_ROTARY_SUPPLY_ON | int | Supply to the rotary switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_AUX_RELAY_ON | int | Auxiliary relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_PWR_WASH_RLY_ON | int | Powerwash relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RR_WIPER_RLY_ON | int | Rear wiper relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_BLOWER_ENABLE_ON | int | Enable the blower motor 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_12V_EXT_PWR_ON | int | External switched 12V feed This output cannot be switched off via diagnostics 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_ALARM_LED_ON | int | Alarm LED output 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_WWA_LED | int | WWA LED output 1 wenn eingeschaltet / 0 wenn ausgeschaltet |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Status der Analogsignale des BC1RD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_V30E_WERT | real | Spannung KL30E Bereich: 0 bis 25,5 [V] |
| STAT_V30P_WERT | real | Spannung KL30PULL Bereich: 0 bis 25,5 [V] |
| STAT_IFFH_WERT | real | Strom Fensterheber Fahrer hinten Bereich: 0 bis 61,2 [A] |
| STAT_IFBH_WERT | real | Strom Fensterheber Beifahrer hinten Bereich: 0 bis 61,2 [A] |
| STAT_IFFHMAX_WERT | real | Anlaufstrom Fensterheber Fahrer hinten Bereich: 0 bis 61,2 [A] |
| STAT_IFBHMAX_WERT | real | Anlaufstrom Fensterheber Beifahrer hinten Bereich: 0 bis 61,2 [A] |
| STAT_IFHF_WERT | real | Strom Fensterheber Fahrer Bereich: 0 bis 61,2 [A] |
| STAT_IFHB_WERT | real | Strom Fensterheber Beifahrer Bereich: 0 bis 61,2 [A] |
| STAT_IFHFMAX_WERT | real | Anlaufstrom Fensterheber Fahrer Bereich: 0 bis 61,2 [A] |
| STAT_IFHBMAX_WERT | real | Anlaufstrom Fensterheber Beifahrer Bereich: 0 bis 61,2 [A] |
| STAT_SWINT_WERT | real | Wischer-Intervall-Potistufenspannung Bereich: 0 bis 25,5 [V] |
| STAT_SPANNUNG_EINH | string | Einheit: Volt |
| STAT_STROM_EINH | string | Einheit: Ampere |
| STAT_KMH_WERT | int | Geschwindigkeit ueber KBUS Bereich: 0 bis 510 [km/h] |
| STAT_KMH_EINH | string | Einheit: km/h |
| STAT_GKL_WERT | int | Geschwindigkeitsklasse fuer Wisch/Wasch Bereich: 0 bis 5 |
| STAT_GKL_EINH | string | Einheit: 1 |
| STAT_EKSFT_WERT | int | Einklemmschutz-Spannungs-Verhaeltnis Fahrertuer Bereich: 0 bis 255 |
| STAT_EKSFT_EINH | string | Einheit: 1 |
| STAT_EKSBT_WERT | int | Einklemmschutz-Spannungs-Verhaeltnis Beifahrertuer Bereich: 0 bis 255 |
| STAT_EKSBT_EINH | string | Einheit: 1 |
| STAT_EKSBH_WERT | int | Einklemmschutz-Spannungs-Verhaeltnis Beifahrertuer hinten Bereich: 0 bis 255 |
| STAT_EKSBH_EINH | string | Einheit: 1 |
| STAT_PLWR_WERT | int | LWR Poti Bereich: 0 bis 255 |
| STAT_PLWR_EINH | string | Einheit: 1 |
| STAT_GEBL_SEN_WERT | int | Gebläse Sensor Bereich: 0 bis 255 |
| STAT_GEBL_SEN_EINH | string | Einheit: 1 |
| STAT_RAW_VEDF_WERT | int | Verdampfer (Messwert) Bereich: 0 bis 255 |
| STAT_RAW_VEDF_EINH | string | Einheit: 1 |
| STAT_VEDF_WERT | int | Verdampfer (K-Bus Ausgabe) Bereich: 0 bis 255 |
| STAT_VEDF_EINH | string | Einheit: 1 |
| STAT_HSSV_WERT | int | Höhenstandssensor vorne Bereich: 0 bis 255 |
| STAT_HSSV_EINH | string | Einheit: 1 |
| STAT_HSSH_WERT | int | Höhenstandssensor hinten Bereich: 0 bis 255 |
| STAT_HSSH_EINH | string | Einheit: 1 |
| STAT_V30EKS_WERT | int | Interne Spannung EKS Bereich: 0 bis 255 |
| STAT_V30EKS_EINH | string | Einheit: 1 |
| STAT_S_KL30DW_WERT | int | Sicherung Fahrerfenster Bereich: 0 bis 255 |
| STAT_S_KL30DW_EINH | string | Einheit: 1 |
| STAT_S_KL30PW_WERT | int | Sicherung Beifahrerfenster Bereich: 0 bis 255 |
| STAT_S_KL30PW_EINH | string | Einheit: 1 |
| STAT_S_KL30CDL_WERT | int | Sicherung Zentralverriegelung Bereich: 0 bis 255 |
| STAT_S_KL30CDL_EINH | string | Einheit: 1 |
| STAT_S_KL30IB_WERT | int | Sicherung Innenlicht Bereich: 0 bis 255 |
| STAT_S_KL30IB_EINH | string | Einheit: 1 |
| STAT_S_KL30A_WERT | int | Sicherung KL30A Bereich: 0 bis 255 |
| STAT_S_KL30A_EINH | string | Einheit: 1 |
| STAT_S_KL30B_WERT | int | Sicherung KL30B Bereich: 0 bis 255 |
| STAT_S_KL30B_EINH | string | Einheit: 1 |
| STAT_RAW_AI_S56A_D_WERT | int | Messwert Schalter S56A Bereich: 0 bis 255 |
| STAT_RAW_AI_S56A_D_EINH | string | Einheit: 1 |
| STAT_RAW_AI_S49L_R_WERT | int | Messwert Schalter S49L_R Bereich: 0 bis 255 |
| STAT_RAW_AI_S49L_R_EINH | string | Einheit: 1 |
| STAT_AIP_MAIN_FLASH_SW_WERT | real | Switch to flash main beam |
| STAT_AIP_MAIN_FLASH_SW_EINH | string | Einheit: 1 |
| STAT_AIP_BLOWER_MOT_SENSE_WERT | real | Blower motor fault sense before A/C Switch on |
| STAT_AIP_BLOWER_MOT_SENSE_EINH | string | Einheit: 1 |
| STAT_AIP_INDICATOR_SW_WERT | real | Switch to change indicators |
| STAT_AIP_INDICATOR_SW_EINH | string | Einheit: 1 |
| STAT_AIP_EXT_5V_MON_WERT | real | Not used |
| STAT_AIP_EXT_5V_MON_EINH | string | Not used |
| STAT_AIP_BATT_VOLTS_MON_WERT | real | Main battery monitoring level |
| STAT_AIP_BATT_VOLTS_MON_EINH | string | Bereich: 0 bis 25,5 [V] |
| STAT_AIP_PASS_WIN_CURR_SENSE_WERT | real | Current sense to detect window stall |
| STAT_AIP_PASS_WIN_CURR_SENSE_EINH | string |  |
| STAT_AIP_WIN_RELAY_MON_WERT | real | Not existing: only for backwardscompatibility to BC1 SGBD |
| STAT_AIP_WIN_RELAY_MON_EINH | string | Not existing: only for backwardscompatibility to BC1 SGBD |
| STAT_AIP_HEAD_LGT_LEVEL_SW_WERT | long | Switch to determine headlight level |
| STAT_AIP_HEAD_LGT_LEVEL_SW_EINH | string |  |
| STAT_AIP_MAIN_FLASH_SW_STATE | string | Switch to flash main beam |
| STAT_AIP_DRV_WIN_CURR_SENSE_WERT | real | Current sense to detect window stall |
| STAT_AIP_DRV_WIN_CURR_SENSE_EINH | string |  |
| STAT_AIP_PASS_WIN_RELAY_MON_WERT | real | Not existing: only for backwardscompatibility to BC1 SGBD |
| STAT_AIP_PASS_WIN_RELAY_MON_EINH | string | Not existing: only for backwardscompatibility to BC1 SGBD |
| STAT_AIP_LOCK_RELAY_MON_WERT | real | Not existing: only for backwardscompatibility to BC1 SGBD |
| STAT_AIP_LOCK_RELAY_MON_EINH | string | Not existing: only for backwardscompatibility to BC1 SGBD |
| STAT_AIP_EVAPORATOR_SENSE_WERT | real | Evaporation sensor |
| STAT_AIP_EVAPORATOR_SENSE_EINH | string |  |
| STAT_AIP_LOCK_RELAY_MON_2_WERT | real | Not existing: only for backwardscompatibility to BC1 SGBD |
| STAT_AIP_LOCK_RELAY_MON_2_EINH | string | Not existing: only for backwardscompatibility to BC1 SGBD |
| STAT_AIP_INDICATOR_SW_STATE | string | Indicator position |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fzv"></a>
### STATUS_FZV

Auslesen FZV-Status Read the FZV State

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KEYS | int | Anzahl der Schluessel Number of keys |
| STAT_KEYPARAM1 | int | Generische Schluessel Nr Generic key Number |
| STAT_KEYPARAM2 | int | Generische Schluessel Nr Generic key Number |
| STAT_KEYPARAM3 | int | Generische Schluessel Nr Generic key Number |
| STAT_KEYPARAM4 | int | Generische Schluessel Nr Generic key Number |
| STAT_CURKEY | int | Aktuelle generische Schluessel Nr Current generic key Number |
| STAT_CURKEY_NUMBER | int | Aktuelle Schluessel Nr (1..4) Current key Number (1..4) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-rf"></a>
### STATUS_RF

Read the RF status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LAST_RF_CODE | string | Last valid RF code received from plip |
| STAT_RF_REMOTE_OK_ROLLING_CODE_OK | int | Base and window code status 1 = Correct remote, correct rolling code (Correct base and window codes) |
| STAT_RF_REMOTE_OK_ROLLING_CODE_NOT_OK | int | Rolling code synchronisation status 1 = Rolling code out of synchronisation (Correct base code, incorrect window code) |
| STAT_RF_REMOTE_INCORRECT | int | Remote (Base) code status 1 = Incorrect remote (Incorrect base code), 0 = OK |
| STAT_RF_REMOTE_BATTERY_DEAD | int | Battery status 1 = Flat battery detected, 0 = OK |

<a id="job-status-tilt-sensor"></a>
### STATUS_TILT_SENSOR

Read the Tilt sensor status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_TILT_SENSOR_PULSE_RECEIVED | int | Tilt sensor Pulse status 1 = Tilt sensor check pulse received, 0 = not received |

<a id="job-status-light-outputs"></a>
### STATUS_LIGHT_OUTPUTS

Read lighting Digital outputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_DOP_RR_FOG_LED_ON | int | Rear fog LED 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RR_FOG_LGT_ON | int | Rear fog lamps 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RH_INDICATOR_LGT_ON | int | Right hand indicator lamps 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_LH_INDICATOR_LGT_ON | int | Left hand indicator lamps 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_RH_POSITION_LGT_ON | int | Right hand position lamps 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_LH_POSITION_LGT_ON | int | Left hand position lamps 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_FT_FOG_LGT_RLY_ON | int | Front fog relay coil 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DOP_NO_PLATE_LGT_ON | int | Number plate light 1 wenn einschalten / 0 wenn ausschalten |

<a id="job-status-light-inputs"></a>
### STATUS_LIGHT_INPUTS

Read Lighting Digital Input States

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_DIP_HAZARD_SW_ON | int | Switch input hazard switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_POSN_LGT_SW_ON | int | Switch input position lights 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_INT_LGT_SW_ON | int | Switch input interior light 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RR_FOG_SW_ON | int | Switch input rear fog switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_FT_FOG_SW_ON | int | Switch input front fog switch 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_DIPPED_BEAM_SW_ON | int | Switch input dipped beam 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_AUX_LGT_SW_ON | int | Switch input auxiliary lamps 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_IND_SIGNAL_ON | int | Monitor the positive sense of indicator for sleep 1 wenn ausgeschaltet / 0 wenn eingeschaltet |
| STAT_DIP_IND_SIG_INVERTED_ON | int | Monitor the inverted sense of indicator for sleep 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_LAMP_STATUS_ON | int | Indicator of the lamp status 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_LH_DIR_IND_STATUS_ON | int | Monitor the left hand indicator 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_RH_DIR_IND_STATUS_ON | int | Monitor the right hand indicator 1 wenn einschalten / 0 wenn ausschalten |
| STAT_DIP_BRAKE_LAMP_STATUS_ON | int | Monitor the brake lamps 1 wenn einschalten / 0 wenn ausschalten |

<a id="job-steuern-iostates"></a>
### STEUERN_IOSTATES

Ansteuern eines digitalen Ein- oder Ausgangs v. BC1RD ! erlaubte Namen des Arguments 'ORT' ueber Tool XTRACT.exe ! Aufruf 'XTRACT [-F] BC1RD.prg'

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table BITS NAME TEXT |
| EIN | int | '1', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-analog"></a>
### STEUERN_ANALOG

Ansteuern eines ANALOGEN Ein- oder Ausgangs ! erlaubte Namen des Arguments 'ORT' ueber Tool XTRACT.exe ! Aufruf 'XTRACT [-F] BC1RD.prg'

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table BITS NAME TEXT |
| VALUE | int | 0-255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pwm-outputs"></a>
### STEUERN_PWM_OUTPUTS

Force Digital Output States

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | PWM output to force, AOP_? AOP_MAP_READ_LGT, AOP_INTERIOR_LGT, AOP_MAIN_BEAM, AOP_DIPPED_BEAM Argument is case sensitive |
| EIN | int | 0 for OFF, any other value for ON '&gt; 0', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read PWM outputs response |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Force PWM outputs telegram to ECU |
| _TEL_SENDE2 | binary | Sendetelegramm anzeigen Force PWM outputs telegram to ECU |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Force PWM outputs response |

<a id="job-steuern-tilt-sensor"></a>
### STEUERN_TILT_SENSOR

Force Tilt Sensor state

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EIN | int | 0 = OFF,      &gt;0 = ON '&gt;0', wenn ein / '0', wenn aus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-steuern-hss"></a>
### STEUERN_HSS

Force Tilt Sensor state

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT_VORNE | int | Wert Höhensstandsensor vorne |
| WERT_HINTEN | int | Wert Höhensstandsensor hinten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE1 | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_SENDE2 | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response packet |

<a id="job-steuern-poti-lwr"></a>
### STEUERN_POTI_LWR

Force POTILWR state

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | int | LWR Poti Wert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-lwr-on"></a>
### LWR_ON

Switch on LWR2A

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Force outputs telegram to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-lwr-off"></a>
### LWR_OFF

Switch on LWR2A

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Force outputs telegram to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-read-manufacturer-data"></a>
### READ_MANUFACTURER_DATA

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
| BYTE5 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE6 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE7 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE8 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE9 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE10 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers des BC1rd Als Argumente wird die Speicherart (Gruppe) und die Adresse der Datenbytes uebergeben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GRUPPE | int | 0 - 3 |
| ADRESSE | long | 0x000000 - 0xFFFFFF Bei Gruppe 3: BlockNr. - Offset - Offset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Speicherinhalt schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GRUPPE | int | 0 or 3 |
| ADRESSE | long | Speicheradresse |
| SPEICHER_DATEN | string | Speicherinhalt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-write-ident"></a>
### WRITE_IDENT

Identification data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ID_BMW_NR | string | BMW-Teilenummer BMW Part Number |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | string | Herstelldatum KW Week of manufacture |
| ID_DATUM_JAHR | string | Herstelldatum Jahr Year of manufacture |
| ID_LIEF_NR | string | Lieferanten-Nummer Supplier code |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-clear-rf-buffers"></a>
### CLEAR_RF_BUFFERS

Clear the RF receive and status buffers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-start-diagnostics"></a>
### START_DIAGNOSTICS

Obtain diagnostic seed and send key to begin diagnostics The ecu will lock if no diagnostic messages have been sent to it for 30 seconds

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Request seed response |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Send key telegram to ECU |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Send key response |

<a id="job-read-alarm-mislock"></a>
### READ_ALARM_MISLOCK

Read Alarm mislocks

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| MISLOCK_NR_1 | int | Mislock Fault number |
| MISLOCK_TEXT_1 | string | Mislock Fault description |
| MISLOCK_AGE_1 | int | Mislock Fault age |
| MISLOCK_NR_2 | int | Mislock Fault number |
| MISLOCK_TEXT_2 | string | Mislock Fault description |
| MISLOCK_AGE_2 | int | Mislock Fault age |
| MISLOCK_NR_3 | int | Mislock Fault number |
| MISLOCK_TEXT_3 | string | Mislock Fault description |
| MISLOCK_AGE_3 | int | Mislock Fault age |
| MISLOCK_NR_4 | int | Mislock Fault number |
| MISLOCK_TEXT_4 | string | Mislock Fault description |
| MISLOCK_AGE_4 | int | Mislock Fault age |
| MISLOCK_NR_5 | int | Mislock Fault number |
| MISLOCK_TEXT_5 | string | Mislock Fault description |
| MISLOCK_AGE_5 | int | Mislock Fault age |
| MISLOCK_NR_6 | int | Mislock Fault number |
| MISLOCK_TEXT_6 | string | Mislock Fault description |
| MISLOCK_AGE_6 | int | Mislock Fault age |
| MISLOCK_NR_7 | int | Mislock Fault number |
| MISLOCK_TEXT_7 | string | Mislock Fault description |
| MISLOCK_AGE_7 | int | Mislock Fault age |
| MISLOCK_NR_8 | int | Mislock Fault number |
| MISLOCK_TEXT_8 | string | Mislock Fault description |
| MISLOCK_AGE_8 | int | Mislock Fault age |
| MISLOCK_NR_9 | int | Mislock Fault number |
| MISLOCK_TEXT_9 | string | Mislock Fault description |
| MISLOCK_AGE_9 | int | Mislock Fault age |
| MISLOCK_NR_10 | int | Mislock Fault number |
| MISLOCK_TEXT_10 | string | Mislock Fault description |
| MISLOCK_AGE_10 | int | Mislock Fault age |
| MISLOCK_NR_11 | int | Mislock Fault number |
| MISLOCK_TEXT_11 | string | Mislock Fault description |
| MISLOCK_AGE_11 | int | Mislock Fault age |
| MISLOCK_NR_12 | int | Mislock Fault number |
| MISLOCK_TEXT_12 | string | Mislock Fault description |
| MISLOCK_AGE_12 | int | Mislock Fault age |
| MISLOCK_NR_13 | int | Mislock Fault number |
| MISLOCK_TEXT_13 | string | Mislock Fault description |
| MISLOCK_AGE_13 | int | Mislock Fault age |
| MISLOCK_NR_14 | int | Mislock Fault number |
| MISLOCK_TEXT_14 | string | Mislock Fault description |
| MISLOCK_AGE_14 | int | Mislock Fault age |
| MISLOCK_NR_15 | int | Mislock Fault number |
| MISLOCK_TEXT_15 | string | Mislock Fault description |
| MISLOCK_AGE_15 | int | Mislock Fault age |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-read-alarm-trigger"></a>
### READ_ALARM_TRIGGER

Read alarm triggers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ALARM_NR_1 | int | Alarm Fault number |
| ALARM_TEXT_1 | string | Alarm Fault description |
| ALARM_AGE_1 | int | Alarm Fault age |
| ALARM_NR_2 | int | Alarm Fault number |
| ALARM_TEXT_2 | string | Alarm Fault description |
| ALARM_AGE_2 | int | Alarm Fault age |
| ALARM_NR_3 | int | Alarm Fault number |
| ALARM_TEXT_3 | string | Alarm Fault description |
| ALARM_AGE_3 | int | Alarm Fault age |
| ALARM_NR_4 | int | Alarm Fault number |
| ALARM_TEXT_4 | string | Alarm Fault description |
| ALARM_AGE_4 | int | Alarm Fault age |
| ALARM_NR_5 | int | Alarm Fault number |
| ALARM_TEXT_5 | string | Alarm Fault description |
| ALARM_AGE_5 | int | Alarm Fault age |
| ALARM_NR_6 | int | Alarm Fault number |
| ALARM_TEXT_6 | string | Alarm Fault description |
| ALARM_AGE_6 | int | Alarm Fault age |
| ALARM_NR_7 | int | Alarm Fault number |
| ALARM_TEXT_7 | string | Alarm Fault description |
| ALARM_AGE_7 | int | Alarm Fault age |
| ALARM_NR_8 | int | Alarm Fault number |
| ALARM_TEXT_8 | string | Alarm Fault description |
| ALARM_AGE_8 | int | Alarm Fault age |
| ALARM_NR_9 | int | Alarm Fault number |
| ALARM_TEXT_9 | string | Alarm Fault description |
| ALARM_AGE_9 | int | Alarm Fault age |
| ALARM_NR_10 | int | Alarm Fault number |
| ALARM_TEXT_10 | string | Alarm Fault description |
| ALARM_AGE_10 | int | Alarm Fault age |
| ALARM_NR_11 | int | Alarm Fault number |
| ALARM_TEXT_11 | string | Alarm Fault description |
| ALARM_AGE_11 | int | Alarm Fault age |
| ALARM_NR_12 | int | Alarm Fault number |
| ALARM_TEXT_12 | string | Alarm Fault description |
| ALARM_AGE_12 | int | Alarm Fault age |
| ALARM_NR_13 | int | Alarm Fault number |
| ALARM_TEXT_13 | string | Alarm Fault description |
| ALARM_AGE_13 | int | Alarm Fault age |
| ALARM_NR_14 | int | Alarm Fault number |
| ALARM_TEXT_14 | string | Alarm Fault description |
| ALARM_AGE_14 | int | Alarm Fault age |
| ALARM_NR_15 | int | Alarm Fault number |
| ALARM_TEXT_15 | string | Alarm Fault description |
| ALARM_AGE_15 | int | Alarm Fault age |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-steuern-stepper-motor"></a>
### STEUERN_STEPPER_MOTOR

Force Stepper motor Output State

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EIN | int | 0 for START, any other value for STOP 0 fuer anfang, &gt;0 fuer halt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-flash-rom-test"></a>
### FLASH_ROM_TEST

Self test. Forces a fast Flash-ROM check Wait 2 seconds and read the result from error memory (Stops all ECU tasks for approx 2 seconds)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Ping message

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-sg-reset"></a>
### SG_RESET

Reset the ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (72 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [BC1BITS](#table-bc1bits) (272 × 5)
- [BITS](#table-bits) (509 × 6)
- [FORTTEXTE](#table-forttexte) (171 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [IORTTEXTE](#table-iorttexte) (46 × 2)
- [IARTTEXTE](#table-iarttexte) (3 × 2)
- [BC1_DWA_BITS](#table-bc1-dwa-bits) (28 × 5)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 13 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| ?10? | ERROR_ARGUMENT |
| ?20? | ERROR_FEHLERANZAHL |
| ?70? | ERROR_NUMBER_ARGUMENT |
| ?71? | ERROR_RANGE_ARGUMENT |
| ?72? | ERROR_VERIFY |
| 0x?? | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 72 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen =&gt; Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe =&gt; Lear |
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
| 0x28 | DODUCO =&gt; BERU |
| 0x29 | DENSO |
| 0x30 | NEC |
| 0x31 | DASA |
| 0x32 | Pioneer |
| 0x33 | Jatco |
| 0x34 | Fuba |
| 0x35 | UK-NSI |
| 0x36 | AABG |
| 0x37 | Dunlop |
| 0x38 | Sachs |
| 0x39 | ITT |
| 0x40 | FTE |
| 0x41 | Megamos |
| 0x42 | TRW |
| 0x43 | Wabco |
| 0x44 | ISAD Electronic Systems |
| 0x45 | HEC (Hella Electronics Corporation) |
| 0x46 | Gemel |
| 0x47 | ZF |
| 0x48 | GMPT |
| 0x49 | Harman Kardon |
| 0x50 | Remes |
| 0x51 | ZF Lenksysteme |
| 0x52 | Magneti Marelli |
| 0x53 | Borg Instruments |
| 0x54 | GETRAG |
| 0x55 | BHTC (Behr Hella Thermocontrol) |
| 0x56 | Siemens VDO Automotive |
| 0x57 | Visteon |
| 0x58 | Autoliv |
| 0x59 | Haberl |
| 0x60 | Magna Steyr |
| 0x61 | Marquardt |
| 0x62 | AB-Elektronik |
| 0x63 | Siemens VDO Borg |
| 0x64 | Hirschmann Electronics |
| 0x65 | Hoerbiger Electronics |
| 0x66 | Thyssen Krupp Automotive Mechatronics |
| 0x67 | Gentex GmbH |
| 0x68 | Atena GmbH |
| 0x69 | Magna-Donelly |
| 0x70 | Koyo Steering Europe |
| 0x71 | NSI B.V |
| 0xFF | unbekannter Hersteller |

<a id="table-roverpartnumprefix"></a>
### ROVERPARTNUMPREFIX

Dimensions: 21 rows × 2 columns

| ROVER_NR | PREFIX |
| --- | --- |
| 0xA0 | AMR |
| 0xA1 | HHF |
| 0xA2 | JFC |
| 0xA3 | MKC |
| 0xA4 | SCB |
| 0xA5 | SRB |
| 0xA6 | XQC |
| 0xA7 | XQD |
| 0xA8 | XQE |
| 0xA9 | XVD |
| 0xAA | YAC |
| 0xAB | YDB |
| 0xAC | YFC |
| 0xAD | YUB |
| 0xAE | YWC |
| 0xAF | YWQ |
| 0xB0 | EGQ |
| 0xB1 | YIB |
| 0xB2 | YIC |
| 0xB3 | YIE |
| 0xXY | ??? |

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

<a id="table-bc1bits"></a>
### BC1BITS

Dimensions: 272 rows × 5 columns

| NAME | BYTE | MASK | VALUE | DESCRIPTION |
| --- | --- | --- | --- | --- |
| SW_ST_752 | 3 | 0x01 | 0x01 | Status CHMSL driver |
| SW_Fault_3408 | 3 | 0x02 | 0x02 | Not used |
| SW_Trailer_RxD | 3 | 0x04 | 0x04 | Receive signal from trailer bus |
| SW_RF_Code | 3 | 0x08 | 0x08 | Dataline from Remotecontrol |
| DIP_RF_CODE_LOGIC | 3 | 0x08 | 0x08 | RF Signal |
| SW_MCD_DO | 3 | 0x20 | 0x20 | Dataline from MCD Driver |
| SW_EE_DO | 3 | 0x40 | 0x40 | Dataline to EEPROM |
| SW_DVRFT | 3 | 0x80 | 0x80 | Diag central door locking Lock driver door(DiagVerRiegelnFahrerTuer) |
| SW_DER | 4 | 0x01 | 0x01 | Diag central door locking Unlock motor (DiagmotorEntRiegeln) |
| SW_DZS | 4 | 0x02 | 0x02 | Diag central door locking Superlock passenger/fuel(DiagmotorZentralSichern) |
| SW_DVR | 4 | 0x04 | 0x04 | Diag central door locking Lock motor (DiagmotorVerRiegeln) |
| SW_S56B | 4 | 0x08 | 0x08 | Dipped beam light |
| DIP_DIPPED_BEAM_SW | 4 | 0x08 | 0x08 | Dipped beam light |
| SW_SFBA | 4 | 0x10 | 0x10 | Passenger Window Down Switch (SchalterFensterheberBeifahrerAuf) |
| DIP_PASS_WIN_DOWN_SW | 4 | 0x10 | 0x10 | Passenger Window Down Switch (SchalterFensterheberBeifahrerAuf) |
| SW_SWA_F | 4 | 0x20 | 0x20 | Front Washer (1) Switch (SchalterWaschAnlageFront) |
| DIP_FT_WASH_PUMP | 4 | 0x20 | 0x20 | Front Washer (1) Switch (SchalterWaschAnlageFront) |
| SW_SW2 | 4 | 0x40 | 0x40 | Front Wiper Switch 2 (SchalterWischer ST1, ST2, INT kodiert) |
| DIP_COL_SW_2 | 4 | 0x40 | 0x40 | Front Wiper Switch 2 (SchalterWischer ST1, ST2, INT kodiert) |
| SW_SFFZ | 4 | 0x80 | 0x80 | Driver Window Up Switch (SchalterFensterheberFahrerZu) |
| DIP_DRV_WIN_UP_SW | 4 | 0x80 | 0x80 | Driver Window Up Switch (SchalterFensterheberFahrerZu) |
| SW_SFHZ | 5 | 0x01 | 0x01 | Rear Window Up Switch (SchalterFensterheberHintenZu) |
| SW_SFHA | 5 | 0x02 | 0x02 | Rear Window Down Switch (SchalterFensterheberHintenAuf) |
| SW_SWR | 5 | 0x04 | 0x04 | Switch Wiper Rear |
| DIP_RR_WIPER_SW | 5 | 0x04 | 0x04 | Switch Wiper Rear |
| DIP_WWA | 5 | 0x08 | 0x08 | WWA level switch |
| SW_SWA_H | 5 | 0x10 | 0x10 | Rear Washer (2) Switch (SchalterWaschAnlageHeck) |
| DIP_RR_WASH_PUMP | 5 | 0x10 | 0x10 | Rear Washer (2) Switch (SchalterWaschAnlageHeck) |
| SW_S_BLS | 5 | 0x20 | 0x20 | Brake Switch (BremsLichtSchalter) |
| DIP_BRAKE_SW | 5 | 0x20 | 0x20 | Brake Switch (BremsLichtSchalter) |
| SW_SFBZ | 5 | 0x40 | 0x40 | Passenger Window Up Switch (SchalterFensterheberBeifahrerZu) |
| DIP_PASS_WIN_UP_SW | 5 | 0x40 | 0x40 | Passenger Window Up Switch (SchalterFensterheberBeifahrerZu) |
| SW_TOEHK | 5 | 0x80 | 0x80 | Boot Handle Switch (TasterOEffnenHeckKlappe) |
| DIP_BOOT_HANDLE_SW | 5 | 0x80 | 0x80 | Boot Handle Switch (TasterOEffnenHeckKlappe) |
| SW_MHK | 6 | 0x01 | 0x01 | Bonnet Open Switch (MotorHaubenKontakt) |
| DIP_BONNET_SW | 6 | 0x01 | 0x01 | Bonnet Open Switch (MotorHaubenKontakt) |
| SW_SFFA | 6 | 0x02 | 0x02 | Driver Window Down Switch (SchalterFensterheberFahrerAuf) |
| DIP_DRV_WIN_DOWN_SW | 6 | 0x02 | 0x02 | Driver Window Down Switch (SchalterFensterheberFahrerAuf) |
| SW_INRS | 6 | 0x04 | 0x04 | Ultrasonics in (InNenRaumschutzSignal) |
| DIP_ULTRASONIC_IN | 6 | 0x04 | 0x04 | Ultrasonics in (InNenRaumschutzSignal) |
| SW_NG | 6 | 0x08 | 0x08 | Tilt Trigger (NeigungsgeberSignal) |
| DIP_ALARM_TILT_SW | 6 | 0x08 | 0x08 | Tilt Trigger (NeigungsgeberSignal) |
| SW_R | 6 | 0x10 | 0x10 | Power INPUT (Klemme R) |
| DIP_AUX_SW | 6 | 0x10 | 0x10 | Power INPUT (Klemme R) |
| SW_T_IB | 6 | 0x20 | 0x20 | Interior Light switch (Taster InnenBeleuchtung) |
| DIP_INT_LGT_SW | 6 | 0x20 | 0x20 | Interior Light switch (Taster InnenBeleuchtung) |
| SW_S58 | 6 | 0x40 | 0x40 | Position Lamp Switch (Schalter Standlicht) |
| DIP_POSN_LGT_SW | 6 | 0x40 | 0x40 | Position Lamp Switch (Schalter Standlicht) |
| SW_T_HHS | 6 | 0x80 | 0x80 | Heated Rear Window Switch (Taster HeizbareHeckScheibe) |
| DIP_HT_RR_WIN_SW | 6 | 0x80 | 0x80 | Heated Rear Window Switch (Taster HeizbareHeckScheibe) |
| SW_CS | 7 | 0x01 | 0x01 | Inertia Switch (Traegheitsschalter) |
| DIP_INERTIA_SENSE | 7 | 0x01 | 0x01 | Inertia Switch (Traegheitsschalter) |
| SW_HKK | 7 | 0x02 | 0x02 | Boot Open Switch (HeckKlappenKonkakt) |
| DIP_BOOT_OPEN_SW | 7 | 0x02 | 0x02 | Boot Open Switch (HeckKlappenKonkakt) |
| SW_SW1 | 7 | 0x04 | 0x04 | Front Wiper Switch 1 (SchalterWischer ST1, ST2, INT kodiert) |
| DIP_COL_SW_1 | 7 | 0x04 | 0x04 | Front Wiper Switch 1 (SchalterWischer ST1, ST2, INT kodiert) |
| SW_T_UMLUFT | 7 | 0x08 | 0x08 | Recirc Switch (Taster Frischluft/Umluft) |
| DIP_RECIRC_SW | 7 | 0x08 | 0x08 | Recirc Switch (Taster Frischluft/Umluft) |
| SW_S55V | 7 | 0x10 | 0x10 | Front Fog Switch (Schalter Nebelscheinwerfer) |
| DIP_FT_FOG_SW | 7 | 0x10 | 0x10 | Front Fog Switch (Schalter Nebelscheinwerfer) |
| SW_TZE | 7 | 0x20 | 0x20 | Master Unlock Switch (TasterZentralverriegelungEntriegeln) |
| DIP_MASTER_UNLK_SW | 7 | 0x20 | 0x20 | Master Unlock Switch (TasterZentralverriegelungEntriegeln) |
| SW_S49W | 7 | 0x40 | 0x40 | Hazard Switch (Schalter Warnblinkanlage) |
| SW_TZV | 7 | 0x80 | 0x80 | Master Lock Switch (TasterZentralverriegelungVerriegeln) |
| DIP_MASTER_LK_SW | 7 | 0x80 | 0x80 | Master Lock Switch (TasterZentralverriegelungVerriegeln) |
| SW_ERFT | 8 | 0x01 | 0x01 | Driver Key Unlock Switch (EntRiegelnFahrerTuere) |
| DIP_DRV_KEY_SW_UNLK | 8 | 0x01 | 0x01 | Driver Key Unlock Switch (EntRiegelnFahrerTuere) |
| SW_TKBT | 8 | 0x02 | 0x02 | Passenger Door Open Switch (TuerKontaktBeifahrerTuere) |
| DIP_PASS_DOOR_OPEN | 8 | 0x02 | 0x02 | Passenger Door Open Switch (TuerKontaktBeifahrerTuere) |
| SW_ERBT | 8 | 0x04 | 0x04 | Pass Key Unlock Switch (EntRiegelnBeifahrerTuere) |
| DIP_PASS_KEY_SW_UNLK | 8 | 0x04 | 0x04 | Pass Key Unlock Switch (EntRiegelnBeifahrerTuere) |
| SW_VRFT | 8 | 0x08 | 0x08 | Driver Key Lock Switch (VerRiegelnFahrerTuere) |
| DIP_DRV_KEY_SW_LK | 8 | 0x08 | 0x08 | Driver Key Lock Switch (VerRiegelnFahrerTuere) |
| SW_TKFT | 8 | 0x10 | 0x10 | Driver Door Open Switch (TuerKontaktFahrerTuere) |
| DIP_DRV_DOOR_OPEN | 8 | 0x10 | 0x10 | Driver Door Open Switch (TuerKontaktFahrerTuere) |
| SW_VRBT | 8 | 0x20 | 0x20 | Pass Key Lock Switch (VerRiegelnBeifahrerTuere) |
| DIP_PASS_KEY_SW_LK | 8 | 0x20 | 0x20 | Pass Key Lock Switch (VerRiegelnBeifahrerTuere) |
| SW_RSK_V | 8 | 0x40 | 0x40 | Front Wiper Park Switch (RueckStellKontakt wischer Vorn) |
| DIP_FT_WIPER_PARK | 8 | 0x40 | 0x40 | Front Wiper Park Switch (RueckStellKontakt wischer Vorn) |
| SW_RSK_H | 8 | 0x80 | 0x80 | Rear Wiper Park Switch (RueckStellKontakt wischer Hinten); |
| DIP_RR_WIPER_PARK | 8 | 0x80 | 0x80 | Rear Wiper Park Switch (RueckStellKontakt wischer Hinten); |
| SW_S56A_D_Flash | 9 | 0x01 | 0x01 | Main Flash Switch (Status Flash) |
| SW_S56A_D_MainBeam | 9 | 0x02 | 0x02 | Main Flash Switch (Status Mainbeam) |
| SW_S49L_R_Right | 9 | 0x04 | 0x04 | Indicator Switch right (Schalter Fahrtrichtungsanz rechts) |
| SW_S49L_R_Left | 9 | 0x08 | 0x08 | Indicator Switch left (Schalter Fahrtrichtungsanz left) |
| SW_T_AC_Ein | 9 | 0x10 | 0x10 | Aircon Switch (Taster AirCon EIN) |
| DIP_AC_SWITCH | 9 | 0x10 | 0x10 | Aircon Switch (Taster AirCon EIN) |
| SW_S55H | 9 | 0x20 | 0x20 | Rear Fog Switch (Schalter Nebenschlussleuchte) |
| DIP_RR_FOG_SW | 9 | 0x20 | 0x20 | Rear Fog Switch (Schalter Nebenschlussleuchte) |
| SW_T_HFS | 9 | 0x40 | 0x40 | Heated Front Screen Switch (Taster HeizbareFrontScheibe) |
| DIP_HT_FT_SCR_SW | 9 | 0x40 | 0x40 | Heated Front Screen Switch (Taster HeizbareFrontScheibe) |
| SW_D_MFL12V | 9 | 0x80 | 0x80 | Rotary Coupler Supply (Versorgung MultiFunktionsLenkrad 12V) |
| SW_D_HFS_LED | 10 | 0x01 | 0x01 | Heated Front Screen LED (HeizbareFrontScheibe LED) |
| SW_D_HFS_RA | 10 | 0x02 | 0x02 | Heated Front Screen Relay (HeizbareFrontScheibe Relaisansteuerung) |
| SW_D_55V_RA | 10 | 0x04 | 0x04 | Front Fog Relay (Nebelscheinwerfer Relaisansteuerung) |
| SW_D_56Z_RA | 10 | 0x08 | 0x08 | Auxiliary Lamps Relay (Zusatzscheinwerfer Relaisansteuerung) |
| SW_D_WI_H | 10 | 0x10 | 0x10 | Rear Wiper Relay (WIscher Hinten Relaisansteuerung) |
| SW_D_WI1 | 10 | 0x20 | 0x20 | Front Wiper Run Park Relay (Wischer Vorne Aus/An Relaisansteuerung) |
| SW_D_HHS_RA | 10 | 0x40 | 0x40 | Heated Rearscreen Relay (HeizbareHeckScheibe RelaisAnsteuerung) |
| SW_D_GEBL_RA | 10 | 0x80 | 0x80 | Heater Blower Relay (heizGEBLaese RelaisAnsteuerung) |
| SW_D_UML_LED | 11 | 0x01 | 0x01 | Recirc LED (UMLuft LED) |
| SW_D_HHS_LED | 11 | 0x02 | 0x02 | Heated Rear Screen LED (HeizbareHeckScheibe LED) |
| SW_D_55_LED | 11 | 0x04 | 0x04 | Rear Fog LED (Nebelschlusslicht LED) |
| SW_D_DWALED | 11 | 0x08 | 0x08 | Alarm System LED (DiebstahlWarnAnlageLED) |
| SW_D_AC_LED | 11 | 0x10 | 0x10 | Aircon LED (AirCon LED) |
| SW_D_WI2 | 11 | 0x20 | 0x20 | Front Wiper Fast Slow Relay (Wischer Vorne Stufe 1/Stufe 2 Relaisans) |
| SW_D_SRA | 11 | 0x40 | 0x40 | Headlamp Power Wash Relay (ScheinwerferReinigungsAnlageRelaisanst) |
| SW_EN_5V | 11 | 0x80 | 0x80 | Power LWR Poti, Refernce HSS |
| SW_EN_PU_DirInd | 12 | 0x01 | 0x01 | Pullup Direction Indicator |
| SW_EN_5VPU | 12 | 0x02 | 0x02 | Pullup Mainflash, Evaptemp, Lamps, MCD |
| SW_MUX_A0 | 12 | 0x04 | 0x04 | ADC Multiplexer Address Selection |
| SW_MUX_A1 | 12 | 0x08 | 0x08 | ADC Multiplexer Address Selection |
| SW_MUX_A2 | 12 | 0x10 | 0x10 | ADC Multiplexer Address Selection |
| DOP_WWA_LED | 12 | 0x20 | 0x20 | WWA LED Output |
| SW_Trailer_TxD | 12 | 0x40 | 0x40 | Transmit signal from trailer bus |
| SW_CLA5440 | 12 | 0x80 | 0x80 | current limit for BTS driver (high or low current value on 1/0) |
| SW_HC238_A0 | 13 | 0x01 | 0x01 | w Atmel: I when sleeping, O when active; w/o Atmel: 0 |
| SW_HC238_A1 | 13 | 0x02 | 0x02 | w Atmel: I when sleeping, O when active; w/o Atmel: 0 |
| SW_HC238_A2 | 13 | 0x04 | 0x04 | w Atmel: I when sleeping, O when active; w/o Atmel: 0 |
| SW_MFFH | 13 | 0x08 | 0x08 | Window Motor Driversite rear (MotorFensterheberFahrerHinten) |
| SW_EN_STP | 13 | 0x10 | 0x10 | Enable Stepper motor driver |
| SW_MFBH | 13 | 0x20 | 0x20 | Window Motor Passengersite rear (MotorFensterheberBeifahrerHinten) |
| SW_MCD_DI | 13 | 0x40 | 0x40 | Data line to MCD |
| SW_CS_STP | 13 | 0x80 | 0x80 | Select Stepper motor driver |
| SW_56AL | 14 | 0x01 | 0x01 | LH Main Beam (Fernlicht links) |
| SW_56AR | 14 | 0x02 | 0x02 | RH Main Beam (Fernlicht rechts) |
| SW_49VR | 14 | 0x04 | 0x04 | Right Front DI (Blinker vorne rechts) |
| SW_49HR_49ZR | 14 | 0x08 | 0x08 | Right DI Repeater (Zusatzblinker rechts) |
| SW_58VR_58IVR_58IHR | 14 | 0x10 | 0x10 | Right Rear/Front Side Marker/Right Front Pos. Lam |
| SW_58HL | 14 | 0x20 | 0x20 | Left Rear Position Lamp (Schlusslicht links hinten) |
| SW_INRS_12V__NG_12V | 14 | 0x40 | 0x40 | Switched +12V Supply 1 (tilt sensor) (Neigungsgeber 12V Versorgung) |
| DOP_12V_EXT_PWR | 14 | 0x40 | 0x40 | Switched +12V Supply 1 (tilt sensor) (Neigungsgeber 12V Versorgung) |
| SW_Atmel_CLK | 14 | 0x80 | 0x80 | Atmel Clock line |
| SW_Atmel_DiDo | 15 | 0x01 | 0x01 | Atmel Data in and Data out line |
| SW_WD_Trigger | 15 | 0x02 | 0x02 | Watch dog trigger signal |
| SW_MERHK | 15 | 0x04 | 0x04 | Boot Release Actuator (MotorEntRiegelnHeckKlappe) |
| DOP_BOOT_RELEASE | 15 | 0x04 | 0x04 | Boot Release Actuator (MotorEntRiegelnHeckKlappe) |
| SW_MFFZ | 15 | 0x08 | 0x08 | Driver Window Up (MotorFensterheberFahrerZu) |
| DOP_DRV_WIN_UP | 15 | 0x08 | 0x08 | Driver Window Up (MotorFensterheberFahrerZu) |
| SW_MFFA | 15 | 0x10 | 0x10 | Driver Window Down (MotorFensterheberFahrerAuf) |
| DOP_DRV_WIN_DOWN | 15 | 0x10 | 0x10 | Driver Window Down (MotorFensterheberFahrerAuf) |
| SW_MFBZ | 15 | 0x20 | 0x20 | Passenger Window Up (MotorFensterheberBeifahrerZu) |
| DOP_PASS_WIN_UP | 15 | 0x20 | 0x20 | Passenger Window Up (MotorFensterheberBeifahrerZu) |
| SW_MFBA | 15 | 0x40 | 0x40 | Passenger Window Down (MotorFensterheberBeifahrerAuf) |
| DOP_PASS_WIN_DOWN | 15 | 0x40 | 0x40 | Passenger Window Down (MotorFensterheberBeifahrerAuf) |
| SW_SIRENE | 15 | 0x80 | 0x80 | BBUS Sound Alarm (Steuersignal DWA-Sirene Alarm) |
| DOP_SOUND_ALARM | 15 | 0x80 | 0x80 | BBUS Sound Alarm (Steuersignal DWA-Sirene Alarm) |
| SW_STDWA | 16 | 0x01 | 0x01 | BBUS Arm/Disarm (Sirene schaerfen/entsch.(StatDWA)) |
| DOP_BBS_ARM_DISARM | 16 | 0x01 | 0x01 | BBUS Arm/Disarm (Sirene schaerfen/entsch.(StatDWA)) |
| SW_EE_CLK | 16 | 0x02 | 0x02 | Clock for EEPROM Interface |
| SW_EE_DI | 16 | 0x04 | 0x04 | Data for EEPROM Interface |
| SW_EE_CS | 16 | 0x08 | 0x08 | Chip select for EEPROM Interface |
| SW_MER | 16 | 0x10 | 0x10 | Driver/Passenger Common (MotorEntRiegeln Fahrertuere/Beif) |
| DOP_COMMON_LOCK_RLY | 16 | 0x10 | 0x10 | Driver/Passenger Common (MotorEntRiegeln Fahrertuere/Beif) |
| SW_MZS | 16 | 0x20 | 0x20 | Fuel Superlock/Passenger Superlock (MotorZentralSichern Tankkl/Beift) |
| DOP_SUPER_LOCK_RLY | 16 | 0x20 | 0x20 | Fuel Superlock/Passenger Superlock (MotorZentralSichern Tankkl/Beift) |
| SW_VS_PULL_EIN | 16 | 0x40 | 0x40 | Open Load Detection for BTS |
| SW_EN_EKS | 16 | 0x80 | 0x80 | Pullup pinch protection (Pullup Einklemmschutz) |
| SW_EN_PU | 17 | 0x01 | 0x01 | RSK Pullup (Klemme 30 Pullup) |
| SW_MVR | 17 | 0x02 | 0x02 | Pass Rest Lock (MotorVerRiegeln Beifahrertuere) |
| DOP_REST_LOCK_RLY | 17 | 0x02 | 0x02 | Pass Rest Lock (MotorVerRiegeln Beifahrertuere) |
| SW_MVRFT | 17 | 0x04 | 0x04 | Driver Door Lock (MotorVerRiegelnFahrerTuere) |
| DOP_DRV_LOCK_RLY | 17 | 0x04 | 0x04 | Driver Door Lock (MotorVerRiegelnFahrerTuere) |
| SW_MCD_SCLK | 17 | 0x08 | 0x08 | MCD clock |
| SW_IB | 17 | 0x10 | 0x10 | Interior Light (InnenBeleuchtung) |
| SW_56BL | 17 | 0x20 | 0x20 | Left Dipped Beam (Abblendlicht links) |
| SW_54M | 17 | 0x40 | 0x40 | Middle Break light (Bremslicht Mitte) |
| SW_56BR | 17 | 0x80 | 0x80 | Right Dipped Beam (Abblendlicht rechts) |
| SW_KRB | 18 | 0x01 | 0x01 | Boot Lamp (KofferRaumBeleuchtung) |
| SW_VA | 18 | 0x02 | 0x02 | Map Light (VerbrAbsch(Lesel+Schminksp+Hndsf)) |
| SW_58K | 18 | 0x04 | 0x04 | Number Plate Lamps (Kennzeichenleuchte) |
| DOP_NO_PLATE_LGT | 18 | 0x04 | 0x04 | Number Plate Lamps (Kennzeichenleuchte) |
| SW_DWA_LED_ST10 | 18 | 0x08 | 0x08 | Alarm System LED (DiebstahlWarnAnlage LED) |
| SW_54R | 18 | 0x10 | 0x10 | Right Brake Light (Bremslicht rechts) |
| SW_54L | 18 | 0x20 | 0x20 | Left Brake Light (Bremslicht links) |
| SW_55HL | 18 | 0x40 | 0x40 | Left Rear Fog Light (Nebelschlusslicht links) |
| SW_49VL | 18 | 0x80 | 0x80 | Left Front DI (Blinker vorne links) |
| SW_55HR | 19 | 0x01 | 0x01 | Right Rear Fog Light (Nebelschlusslicht rechts) |
| SW_49HL_49ZL | 19 | 0x02 | 0x02 | Left DI Repeater (Zusatzblinker links) |
| SW_58VL_58IVL_58IHL | 19 | 0x04 | 0x04 | Left Rear/Fr Side Mark/L Fr Pos.Lamp (Seiten-Mark.l h/v l/Standl. v l) |
| SW_58HR | 19 | 0x08 | 0x08 | Right Rear Position Lamp (Schlusslicht rechts hinten) |
| SW_MFL12V | 19 | 0x10 | 0x10 | Rotary Coupler Supply (Versorgung MultiFunktionsLenkrad) |
| DOP_ROTARY_SUPPLY | 19 | 0x10 | 0x10 | Rotary Coupler Supply (Versorgung MultiFunktionsLenkrad) |
| SW_HFS_LED | 19 | 0x20 | 0x20 | Heated Front Screen LED (HeizbareFrontScheibe LED) |
| DOP_HT_FT_WIN_LED | 19 | 0x20 | 0x20 | Heated Front Screen LED (HeizbareFrontScheibe LED) |
| SW_HFS_RA | 19 | 0x40 | 0x40 | Heated Front Screen Relay (HeizbareFrontScheibe Relaisansteuerung) |
| DOP_HEATED_FT_WIN_RLY | 19 | 0x40 | 0x40 | Heated Front Screen Relay (HeizbareFrontScheibe Relaisansteuerung) |
| SW_55V_RA | 19 | 0x80 | 0x80 | Front Fog Relay (Nebelscheinwerfer Relaisansteuerung) |
| DOP_FT_FOG_LGT_RLY | 19 | 0x80 | 0x80 | Front Fog Relay (Nebelscheinwerfer Relaisansteuerung) |
| SW_56Z_RA | 20 | 0x01 | 0x01 | Auxiliary Lamps Relay (Zusatzscheinwerfer Relaisansteuerung) |
| SW_WI_H | 20 | 0x02 | 0x02 | Rear  Relay (Wischer Hinten Relaisansteuerung) |
| DOP_RR_WIPER_RLY | 20 | 0x02 | 0x02 | Rear  Relay (Wischer Hinten Relaisansteuerung) |
| SW_WI1 | 20 | 0x04 | 0x04 | Front Wiper Run Park Relay (Wischer Vorne Aus/An Relaisansteuerung) |
| DOP_FT_WIPER_PARK_RUN | 20 | 0x04 | 0x04 | Front Wiper Run Park Relay (Wischer Vorne Aus/An Relaisansteuerung) |
| SW_HHS_RA | 20 | 0x08 | 0x08 | Heated Rear Screen Relay (HeizbareHeckScheibe RelaisAnsteuerung) |
| DOP_HEATED_RR_WIN_RLY | 20 | 0x08 | 0x08 | Heated Rear Screen Relay (HeizbareHeckScheibe RelaisAnsteuerung) |
| SW_GEBL_RA | 20 | 0x10 | 0x10 | Heater Blower Relay (Heizgeblaese Relaisansteuerung) |
| DOP_BLOWER_ENABLE | 20 | 0x10 | 0x10 | Heater Blower Relay (Heizgeblaese Relaisansteuerung) |
| SW_UML_LED | 20 | 0x20 | 0x20 | Recirc LED (Umluft LED) |
| DOP_RECIRC_LED | 20 | 0x20 | 0x20 | Recirc LED (Umluft LED) |
| SW_HHS_LED | 20 | 0x40 | 0x40 | Heated Rear Screen LED (HeizbareHeckScheibe LED) |
| DOP_HT_RR_WIN_LED | 20 | 0x40 | 0x40 | Heated Rear Screen LED (HeizbareHeckScheibe LED) |
| SW_55_LED | 20 | 0x80 | 0x80 | Rear Fog LED (Nebelschlusslicht LED) |
| DOP_RR_FOG_LED | 20 | 0x80 | 0x80 | Rear Fog LED (Nebelschlusslicht LED) |
| SW_DWALED | 21 | 0x01 | 0x01 | Alarm System LED (DiebstahlWarnAnlage LED) |
| DOP_ALARM_LED | 21 | 0x01 | 0x01 | Alarm System LED (DiebstahlWarnAnlage LED) |
| SW_AC_LED | 21 | 0x02 | 0x02 | Aircon LED (Klimaanlage LED) |
| DOP_AC_LED | 21 | 0x02 | 0x02 | Aircon LED (Klimaanlage LED) |
| SW_WI2 | 21 | 0x04 | 0x04 | Front Wiper Fast Slow Relay (Wischer Vorne Stufe 1/Stufe 2 Relaisans) |
| DOP_FT_WIPER_SLOW_FAST | 21 | 0x04 | 0x04 | Front Wiper Fast Slow Relay (Wischer Vorne Stufe 1/Stufe 2 Relaisans) |
| SW_SRA | 21 | 0x08 | 0x08 | Headlamp Power Wash Relay (ScheinwerferReinigAnlage Relaisanst) |
| DOP_PWR_WASH_RLY | 21 | 0x08 | 0x08 | Headlamp Power Wash Relay (ScheinwerferReinigAnlage Relaisanst) |
| SW_KBUS_R | 21 | 0x10 | 0x10 | Aux by K-bus |
| SW_KBUS_15 | 21 | 0x20 | 0x20 | KL15 by K-Bus |
| SW_EngineRunning | 21 | 0x40 | 0x40 | Engine running by K-Bus |
| SW_EwsManipulated | 21 | 0x80 | 0x80 | EWS manipulated by K-Bus |
| SW_CVM_FA | 22 | 0x01 | 0x01 | Convertable Open Window (Cabrio: Fenster auf) |
| SW_CVM_FZ | 22 | 0x02 | 0x02 | Convertable Close Window (Cabrio: Fenster zu) |
| SW_CVM_VKA | 22 | 0x04 | 0x04 | Convertable Open Roof (Cabrio: VerdeckKlappeAuf) |
| SW_CVM_TopClosed | 22 | 0x08 | 0x08 | Convertable Close Roof (Cabrio: VerdeckKlappeAuf) |
| SW_KL_R | 22 | 0x10 | 0x10 | Klemme Radio |
| SW_KL15 | 22 | 0x20 | 0x20 | Klemme 15 |
| SW_KL50 | 22 | 0x40 | 0x40 | Klemme 50 |
| SW_KL58 | 22 | 0x80 | 0x80 | Park Light Switch (Standlichtschalter von LSZ) |
| SW_EWS_free | 23 | 0x01 | 0x01 | Immo release (ElektronischeWeckfahrSperre freigegeben) |
| SW_EWS_Key | 23 | 0x02 | 0x02 | Immo valid key availabl |
| SW_KB_CS | 23 | 0x04 | 0x04 | Crash signal by K-Bus |
| SW_RDC | 23 | 0x08 | 0x08 | Flat Tire |
| SW_CSMODE | 23 | 0x10 | 0x10 | Crash-Mode active |
| SW_DIAGMODE | 23 | 0x20 | 0x20 | Diagnose-Mode active |
| SW_ZV | 23 | 0x40 | 0x40 | Central Door Lock: Locked |
| SW_ZS | 23 | 0x80 | 0x80 | Central Door Lock: Superlock |
| SW_SEr | 24 | 0x01 | 0x01 | Central Door Lock: Selectiv unlock |
| SW_WB | 24 | 0x02 | 0x02 | Alarm System: Turn indicator flash for optical acknowledge |
| SW_OA | 24 | 0x04 | 0x04 | Alarm System: Turn indicator flash for optical alarm |
| SW_ES | 24 | 0x08 | 0x08 | Central Door Lock: Unlocked |
| SW_QFFZ | 24 | 0x10 | 0x10 | Acknowledge Driver Front Window is Closes |
| SW_QFBZ | 24 | 0x20 | 0x20 | Acknowledge Passenger Front Window is Closes |
| SW_QFFHZ | 24 | 0x40 | 0x40 | Acknowledge Driver Rear Window is Closes |
| SW_QFBHZ | 24 | 0x80 | 0x80 | Acknowledge Passenger Rear Window is Closes |
| SW_SoftOn | 25 | 0x01 | 0x01 | Light on or lamp up light in process |
| SW_KB_FSHD | 25 | 0x02 | 0x02 | Sunroof unlocked |
| SW_KB_KOE | 25 | 0x04 | 0x04 | Comfort Open |
| SW_KB_KS | 25 | 0x08 | 0x08 | Comfort Close |
| SW_FB_Bat | 25 | 0x10 | 0x10 | Remote control: Low Battery |
| SW_FB_NR | 25 | 0x20 | 0x20 | Remote Control: Valid Key and ID available |
| SW_FB_Send_L | 25 | 0x40 | 0x40 | Remote key # Bit 0 |
| SW_FB_Send_H | 25 | 0x80 | 0x80 | Remote key # Bit 1 |
| SW_FB_VR | 26 | 0x01 | 0x01 | Remote Control: Lock |
| SW_FB_ER | 26 | 0x02 | 0x02 | Remote Control: Unlock |
| SW_FB_HK | 26 | 0x04 | 0x04 | Remote Control: Trunk |
| SW_KB_VKER | 26 | 0x08 | 0x08 | Not used |
| SW_Send_L | 26 | 0x10 | 0x10 | Remote Control: ID Low Bit |
| SW_Send_H | 26 | 0x20 | 0x20 | Remote Control: ID High Bit |
| SW_FZVSIG | 26 | 0x40 | 0x40 | Remote Control: Any Signal received |
| SW_FZVKEY | 26 | 0x80 | 0x80 | Remote Control: Signal received |
| SW_TASTE1 | 27 | 0x01 | 0x01 | Remote Control: Lock |
| SW_TASTE2 | 27 | 0x02 | 0x02 | Remote Control: Unlock |
| SW_TASTE3 | 27 | 0x04 | 0x04 | Remote Control: Trunk |
| SW_FuInit | 27 | 0x08 | 0x08 | Remote Control: Key Init possible |
| SW_LOBAT1 | 27 | 0x10 | 0x10 | Remote Control: Key 1 low battery |
| SW_LOBAT2 | 27 | 0x20 | 0x20 | Remote Control: Key 2 low battery |
| SW_LOBAT3 | 27 | 0x40 | 0x40 | Remote Control: Key 3 low battery |
| SW_LOBAT4 | 27 | 0x80 | 0x80 | Remote Control: Key 4 low battery |
| SW_FSIB  | 28 | 0x01 | 0x01 | FS Interior light |
| SW_FsaHK | 28 | 0x02 | 0x02 | FS Trunk |
| SW_Zv1Fs | 28 | 0x04 | 0x04 | FS Central door locking: Unlock |
| SW_Zv0Fs | 28 | 0x08 | 0x08 | FS Central door locking: Lock; |
| SW_Frischl | 28 | 0x40 | 0x40 | Recirc 1: Fresh |
| SW_Umluft | 28 | 0x80 | 0x80 | Recirc 1: Recirc |
| SW_LWR12V | 29 | 0x01 | 0x01 | LWR 12Volt: Current Supply to LWR ECU |
| XY | XY | 0xXY | 0xXY | Unknown Item |

<a id="table-bits"></a>
### BITS

Dimensions: 509 rows × 6 columns

| ZELLE | BYTE | MASK | VALUE | NAME | TEXT |
| --- | --- | --- | --- | --- | --- |
| 1 | 0 | 0x01 | 0x01 | ST_752 | -- |
| 2 | 0 | 0x02 | 0x02 | 0L1 | -- |
| 3 | 0 | 0x04 | 0x04 | 0L2 | -- |
| 4 | 0 | 0x08 | 0x08 | 0L4 | -- |
| 5 | 0 | 0x10 | 0x10 | 0L8 | -- |
| 6 | 0 | 0x20 | 0x20 | 0L5 | -- |
| 7 | 0 | 0x40 | 0x40 | 0L6 | -- |
| 8 | 0 | 0x80 | 0x80 | 0L7 | -- |
| 9 | 1 | 0x01 | 0x01 | 0H0 | -- |
| 10 | 1 | 0x02 | 0x02 | 0H1 | -- |
| 11 | 1 | 0x04 | 0x04 | Fault_4808 | -- |
| 12 | 1 | 0x08 | 0x08 | 0H4 | -- |
| 13 | 1 | 0x10 | 0x10 | 0H8 | -- |
| 14 | 1 | 0x20 | 0x20 | 0H5 | -- |
| 15 | 1 | 0x40 | 0x40 | 0H6 | -- |
| 16 | 1 | 0x80 | 0x80 | 0H7 | -- |
| 17 | 2 | 0x01 | 0x01 | 1L0 | -- |
| 18 | 2 | 0x02 | 0x02 | 1L1 | -- |
| 19 | 2 | 0x04 | 0x04 | 1L2 | -- |
| 20 | 2 | 0x08 | 0x08 | 1L4 | -- |
| 21 | 2 | 0x10 | 0x10 | 1L8 | -- |
| 22 | 2 | 0x20 | 0x20 | 1L5 | -- |
| 23 | 2 | 0x40 | 0x40 | 1L6 | -- |
| 24 | 2 | 0x80 | 0x80 | 1L7 | -- |
| 25 | 3 | 0x01 | 0x01 | 1H0 | -- |
| 26 | 3 | 0x02 | 0x02 | 1H1 | -- |
| 27 | 3 | 0x04 | 0x04 | 1H2 | -- |
| 28 | 3 | 0x08 | 0x08 | 1H4 | -- |
| 29 | 3 | 0x10 | 0x10 | Trailer_RxD | -- |
| 30 | 3 | 0x20 | 0x20 | 1H5 | -- |
| 31 | 3 | 0x40 | 0x40 | 1H6 | -- |
| 32 | 3 | 0x80 | 0x80 | 1H7 | -- |
| 33 | 4 | 0x01 | 0x01 | 2_0 | -- |
| 34 | 4 | 0x02 | 0x02 | 2_1 | -- |
| 35 | 4 | 0x04 | 0x04 | 2_2 | -- |
| 36 | 4 | 0x08 | 0x08 | 2_4 | -- |
| 37 | 4 | 0x10 | 0x10 | 2_8 | -- |
| 38 | 4 | 0x20 | 0x20 | 2_5 | -- |
| 39 | 4 | 0x40 | 0x40 | 2_6 | -- |
| 40 | 4 | 0x80 | 0x80 | 2_7 | -- |
| 41 | 5 | 0x01 | 0x01 | RF_Code | -- |
| 41 | 5 | 0x01 | 0x01 | DIP_RF_CODE_LOGIC | RF Code input |
| 42 | 5 | 0x02 | 0x02 | 2_9 | -- |
| 43 | 5 | 0x04 | 0x04 | 2_10 | -- |
| 44 | 5 | 0x08 | 0x08 | 2_11 | -- |
| 45 | 5 | 0x10 | 0x10 | Atmel_DiDo | -- |
| 46 | 5 | 0x20 | 0x20 | MCD_DO | -- |
| 47 | 5 | 0x40 | 0x40 | 2_18 | -- |
| 48 | 5 | 0x80 | 0x80 | 2_15 | -- |
| 49 | 6 | 0x01 | 0x01 | 4_0 | -- |
| 50 | 6 | 0x02 | 0x02 | 4_1 | -- |
| 51 | 6 | 0x04 | 0x04 | 4_2 | -- |
| 52 | 6 | 0x08 | 0x08 | 4_4 | -- |
| 53 | 6 | 0x10 | 0x10 | 4_8 | -- |
| 54 | 6 | 0x20 | 0x20 | 4_5 | -- |
| 55 | 6 | 0x40 | 0x40 | 4_6 | -- |
| 56 | 6 | 0x80 | 0x80 | 4_7 | -- |
| 57 | 7 | 0x01 | 0x01 | 4_8 | -- |
| 58 | 7 | 0x02 | 0x02 | 4_9 | -- |
| 59 | 7 | 0x04 | 0x04 | 4_10 | -- |
| 60 | 7 | 0x08 | 0x08 | 4_11 | -- |
| 61 | 7 | 0x10 | 0x10 | 4_12 | -- |
| 62 | 7 | 0x20 | 0x20 | 4_14 | -- |
| 63 | 7 | 0x40 | 0x40 | 4_18 | -- |
| 64 | 7 | 0x80 | 0x80 | 4_15 | -- |
| 65 | 8 | 0x01 | 0x01 | 8_0 | -- |
| 66 | 8 | 0x02 | 0x02 | 8_1 | -- |
| 67 | 8 | 0x04 | 0x04 | EE_DO | -- |
| 68 | 8 | 0x08 | 0x08 | 8_4 | -- |
| 69 | 8 | 0x10 | 0x10 | 8_8 | -- |
| 70 | 8 | 0x20 | 0x20 | 8_5 | -- |
| 71 | 8 | 0x40 | 0x40 | DVRFT | -- |
| 72 | 8 | 0x80 | 0x80 | DER | -- |
| 73 | 9 | 0x01 | 0x01 | 6_0 | -- |
| 74 | 9 | 0x02 | 0x02 | 6_1 | -- |
| 75 | 9 | 0x04 | 0x04 | 6_2 | -- |
| 76 | 9 | 0x08 | 0x08 | DZS | -- |
| 77 | 9 | 0x10 | 0x10 | DVR | -- |
| 78 | 9 | 0x20 | 0x20 | 6_5 | -- |
| 79 | 9 | 0x40 | 0x40 | 6_6 | -- |
| 80 | 9 | 0x80 | 0x80 | 6_7 | -- |
| 81 | 10 | 0x01 | 0x01 | 7_0 | -- |
| 82 | 10 | 0x02 | 0x02 | 7_1 | -- |
| 83 | 10 | 0x04 | 0x04 | 7_2 | -- |
| 84 | 10 | 0x08 | 0x08 | 7_4 | -- |
| 85 | 10 | 0x10 | 0x10 | 7_8 | -- |
| 86 | 10 | 0x20 | 0x20 | 7_5 | -- |
| 87 | 10 | 0x40 | 0x40 | 7_6 | -- |
| 88 | 10 | 0x80 | 0x80 | 7_7 | -- |
| 89 | 11 | 0x01 | 0x01 | 8_0 | -- |
| 90 | 11 | 0x02 | 0x02 | 8_1 | -- |
| 91 | 11 | 0x04 | 0x04 | 8_2 | -- |
| 92 | 11 | 0x08 | 0x08 | 8_4 | -- |
| 93 | 11 | 0x10 | 0x10 | 8_8 | -- |
| 94 | 11 | 0x20 | 0x20 | 8_5 | -- |
| 95 | 11 | 0x40 | 0x40 | 8_6 | -- |
| 96 | 11 | 0x80 | 0x80 | 8_7 | -- |
| 97 | 12 | 0x01 | 0x01 | S56B | -- |
| 97 | 12 | 0x01 | 0x01 | DIP_DIPPED_BEAM_SW | switch input dipped beam |
| 98 | 12 | 0x02 | 0x02 | SFBA | -- |
| 98 | 12 | 0x02 | 0x02 | DIP_PASS_WIN_DOWN_SW | switch input passenger window down |
| 99 | 12 | 0x04 | 0x04 | SWA_F | -- |
| 99 | 12 | 0x04 | 0x04 | DIP_FT_WASH_PUMP | switch input front washer pump active |
| 100 | 12 | 0x08 | 0x08 | SW2 | -- |
| 100 | 12 | 0x08 | 0x08 | DIP_COL_SW_2 | wiper switch, to activate front wipers |
| 101 | 12 | 0x10 | 0x10 | SFFZ | -- |
| 101 | 12 | 0x10 | 0x10 | DIP_DRV_WIN_UP_SW | switch input driver window up |
| 102 | 12 | 0x20 | 0x20 | SFHZ | -- |
| 103 | 12 | 0x40 | 0x40 | SFHA | -- |
| 104 | 12 | 0x80 | 0x80 | IC0_7 | -- |
| 105 | 13 | 0x01 | 0x01 | SWR | -- |
| 105 | 13 | 0x01 | 0x01 | DIP_RR_WIPER_SW | Rear Wiper switch |
| 106 | 13 | 0x02 | 0x02 | WWA | -- |
| 107 | 13 | 0x04 | 0x04 | SWA_H | -- |
| 107 | 13 | 0x04 | 0x04 | DIP_RR_WASH_PUMP | switch for rear washer pump active |
| 108 | 13 | 0x08 | 0x08 | S_BLS | -- |
| 108 | 13 | 0x08 | 0x08 | DIP_BRAKE_SW | Switch input brake pedal |
| 109 | 13 | 0x10 | 0x10 | SFBZ | -- |
| 109 | 13 | 0x10 | 0x10 | DIP_PASS_WIN_UP_SW | switch input passenger window up |
| 110 | 13 | 0x20 | 0x20 | IC1_5 | -- |
| 111 | 13 | 0x40 | 0x40 | IC1_6 | -- |
| 112 | 13 | 0x80 | 0x80 | IC1_7 | -- |
| 113 | 14 | 0x01 | 0x01 | TOEHK | -- |
| 113 | 14 | 0x01 | 0x01 | DIP_BOOT_HANDLE_SW | switch input boot release motor |
| 114 | 14 | 0x02 | 0x02 | MHK | -- |
| 114 | 14 | 0x02 | 0x02 | DIP_BONNET_SW | -- |
| 115 | 14 | 0x04 | 0x04 | SFFA | -- |
| 115 | 14 | 0x04 | 0x04 | DIP_DRV_WIN_DOWN_SW | switch input driver window down |
| 116 | 14 | 0x08 | 0x08 | IC2_4 | -- |
| 117 | 14 | 0x10 | 0x10 | INRS | -- |
| 117 | 14 | 0x10 | 0x10 | DIP_ULTRASONIC_IN | ultrasonic alarm activated |
| 118 | 14 | 0x20 | 0x20 | NG | -- |
| 118 | 14 | 0x20 | 0x20 | DIP_ALARM_TILT_SW | Alarm Tilt sensor |
| 119 | 14 | 0x40 | 0x40 | R | -- |
| 119 | 14 | 0x40 | 0x40 | DIP_AUX_SW | auxiliary monitor from main ign switch |
| 120 | 14 | 0x80 | 0x80 | IC2_7 | -- |
| 121 | 15 | 0x01 | 0x01 | T_IB | -- |
| 121 | 15 | 0x01 | 0x01 | DIP_INT_LGT_SW | switch input interior light |
| 122 | 15 | 0x02 | 0x02 | S58 | -- |
| 122 | 15 | 0x02 | 0x02 | DIP_POSN_LGT_SW | Switch input position lights |
| 123 | 15 | 0x04 | 0x04 | T_HHS | -- |
| 123 | 15 | 0x04 | 0x04 | DIP_HT_RR_WIN_SW | switch input heated rear window |
| 124 | 15 | 0x08 | 0x08 | CS | -- |
| 124 | 15 | 0x08 | 0x08 | DIP_INERTIA_SENSE | Inertia sensor to detect unusual stop conditions |
| 125 | 15 | 0x10 | 0x10 | IC8_8 | -- |
| 126 | 15 | 0x20 | 0x20 | IC8_5 | -- |
| 127 | 15 | 0x40 | 0x40 | IC8_6 | -- |
| 128 | 15 | 0x80 | 0x80 | IC8_7 | -- |
| 129 | 16 | 0x01 | 0x01 | HKK | -- |
| 129 | 16 | 0x01 | 0x01 | DIP_BOOT_OPEN_SW | switch to detect the boot open |
| 130 | 16 | 0x02 | 0x02 | SW1 | -- |
| 130 | 16 | 0x02 | 0x02 | DIP_COL_SW_1 | wiper switch, to activate front wipers |
| 131 | 16 | 0x04 | 0x04 | T_UMLUFT | -- |
| 131 | 16 | 0x04 | 0x04 | DIP_RECIRC_SW | toggles between recirc and fresh |
| 132 | 16 | 0x08 | 0x08 | S55V | -- |
| 132 | 16 | 0x08 | 0x08 | DIP_FT_FOG_SW | Switch input Front Fog Switch |
| 133 | 16 | 0x10 | 0x10 | TZE | -- |
| 133 | 16 | 0x10 | 0x10 | DIP_MASTER_UNLK_SW | switch input master unlock |
| 134 | 16 | 0x20 | 0x20 | S49W | -- |
| 135 | 16 | 0x40 | 0x40 | TZV | -- |
| 135 | 16 | 0x40 | 0x40 | DIP_MASTER_LK_SW | switch input master lock |
| 136 | 16 | 0x80 | 0x80 | Polling_BL | -- |
| 137 | 17 | 0x01 | 0x01 | ERFT | -- |
| 137 | 17 | 0x01 | 0x01 | DIP_DRV_KEY_SW_UNLK | -- |
| 138 | 17 | 0x02 | 0x02 | TKBT | -- |
| 138 | 17 | 0x02 | 0x02 | DIP_PASS_DOOR_OPEN | -- |
| 139 | 17 | 0x04 | 0x04 | ERBT | -- |
| 139 | 17 | 0x04 | 0x04 | DIP_PASS_KEY_SW_UNLK | Passenger key switch unlock |
| 140 | 17 | 0x08 | 0x08 | VRFT | -- |
| 140 | 17 | 0x08 | 0x08 | DIP_DRV_KEY_SW_LK | -- |
| 141 | 17 | 0x10 | 0x10 | TKFT | -- |
| 141 | 17 | 0x10 | 0x10 | DIP_DRV_DOOR_OPEN | -- |
| 142 | 17 | 0x20 | 0x20 | IC6_5 | -- |
| 143 | 17 | 0x40 | 0x40 | VRBT | -- |
| 143 | 17 | 0x40 | 0x40 | DIP_PASS_KEY_SW_LK | Passenger key switch lock |
| 144 | 17 | 0x80 | 0x80 | IC6_7 | -- |
| 145 | 18 | 0x01 | 0x01 | 21_0 | -- |
| 146 | 18 | 0x02 | 0x02 | 21_1 | -- |
| 147 | 18 | 0x04 | 0x04 | 21_2 | -- |
| 148 | 18 | 0x08 | 0x08 | 21_4 | -- |
| 149 | 18 | 0x10 | 0x10 | 21_8 | -- |
| 150 | 18 | 0x20 | 0x20 | RSK_V | -- |
| 150 | 18 | 0x20 | 0x20 | DIP_FT_WIPER_PARK | Font wiper at park position |
| 151 | 18 | 0x40 | 0x40 | RSK_H | -- |
| 151 | 18 | 0x40 | 0x40 | DIP_RR_WIPER_PARK | Rear wiper at park position |
| 152 | 18 | 0x80 | 0x80 | 21_7 | -- |
| 153 | 19 | 0x01 | 0x01 | S56A_D_Flash | -- |
| 154 | 19 | 0x02 | 0x02 | S56A_D_MainBeam | -- |
| 155 | 19 | 0x04 | 0x04 | S89L_R_Right | -- |
| 156 | 19 | 0x08 | 0x08 | S89L_R_Left | -- |
| 157 | 19 | 0x10 | 0x10 | T_AC_Ein | -- |
| 157 | 19 | 0x10 | 0x10 | DIP_AC_SWITCH | switch input A/C |
| 158 | 19 | 0x20 | 0x20 | S55H | -- |
| 158 | 19 | 0x20 | 0x20 | DIP_RR_FOG_SW | Switch input Rear Fog switch |
| 159 | 19 | 0x40 | 0x40 | T_HFS | -- |
| 159 | 19 | 0x40 | 0x40 | DIP_HT_FT_SCR_SW | Heated Front Screen Switch |
| 160 | 19 | 0x80 | 0x80 | empty_7 | -- |
| 161 | 20 | 0x01 | 0x01 | D_MFL12V | -- |
| 162 | 20 | 0x02 | 0x02 | D_HFS_LED | -- |
| 163 | 20 | 0x04 | 0x04 | D_HFS_RA | -- |
| 164 | 20 | 0x08 | 0x08 | D_55V_RA | -- |
| 165 | 20 | 0x10 | 0x10 | D_56Z_RA | -- |
| 166 | 20 | 0x20 | 0x20 | D_WI_H | -- |
| 167 | 20 | 0x40 | 0x40 | D_WI1 | -- |
| 168 | 20 | 0x80 | 0x80 | D_HHS_RA | -- |
| 169 | 21 | 0x01 | 0x01 | D_GEBL_RA | -- |
| 170 | 21 | 0x02 | 0x02 | D_UML_LED | -- |
| 171 | 21 | 0x04 | 0x04 | D_HHS_LED | -- |
| 172 | 21 | 0x08 | 0x08 | D_55_LED | -- |
| 173 | 21 | 0x10 | 0x10 | D_DWALED | -- |
| 174 | 21 | 0x20 | 0x20 | D_AC_LED | -- |
| 175 | 21 | 0x40 | 0x40 | D_WI2 | -- |
| 176 | 21 | 0x80 | 0x80 | D_SRA | -- |
| 1 | 22 | 0x01 | 0x01 | 0L0 | -- |
| 2 | 22 | 0x02 | 0x02 | EN_5V | -- |
| 3 | 22 | 0x04 | 0x04 | EN_PU_DirInd | -- |
| 4 | 22 | 0x08 | 0x08 | EN_5VPU | -- |
| 5 | 22 | 0x10 | 0x10 | 0L4 | -- |
| 6 | 22 | 0x20 | 0x20 | MUX_A0 | -- |
| 7 | 22 | 0x40 | 0x40 | MUX_A1 | -- |
| 8 | 22 | 0x80 | 0x80 | MUX_A2 | -- |
| 9 | 23 | 0x01 | 0x01 | WWA_LED | WWA LED driver |
| 10 | 23 | 0x02 | 0x02 | EN_3408 | -- |
| 11 | 23 | 0x04 | 0x04 | 0H2 | -- |
| 12 | 23 | 0x08 | 0x08 | Trailer_TxD | -- |
| 13 | 23 | 0x10 | 0x10 | MCD_CS1 | -- |
| 14 | 23 | 0x20 | 0x20 | 0H5 | -- |
| 15 | 23 | 0x40 | 0x40 | 0H6 | -- |
| 16 | 23 | 0x80 | 0x80 | 0H7 | -- |
| 17 | 24 | 0x01 | 0x01 | 1L0 | -- |
| 18 | 24 | 0x02 | 0x02 | 1L1 | -- |
| 19 | 24 | 0x04 | 0x04 | 1L2 | -- |
| 20 | 24 | 0x08 | 0x08 | 1L3 | -- |
| 21 | 24 | 0x10 | 0x10 | 1L4 | -- |
| 22 | 24 | 0x20 | 0x20 | 1L5 | -- |
| 23 | 24 | 0x40 | 0x40 | 1L6 | -- |
| 24 | 24 | 0x80 | 0x80 | 1L7 | -- |
| 25 | 25 | 0x01 | 0x01 | CLA5440 | -- |
| 26 | 25 | 0x02 | 0x02 | HC238_A0 | -- |
| 27 | 25 | 0x04 | 0x04 | HC238_A1 | -- |
| 28 | 25 | 0x08 | 0x08 | HC238_A2 | -- |
| 29 | 25 | 0x10 | 0x10 | 1H4 | -- |
| 30 | 25 | 0x20 | 0x20 | MFFH | driver window: relais front to rear window |
| 30 | 25 | 0x20 | 0x20 | MFFHZ | driver window rear up (MFFH+MFFZ) |
| 30 | 25 | 0x20 | 0x20 | MFFHA | driver window rear down (MFFH+MFFA) |
| 31 | 25 | 0x40 | 0x40 | EN_STP | -- |
| 32 | 25 | 0x80 | 0x80 | MFBH | passenger window: relais front to rear window |
| 32 | 25 | 0x80 | 0x80 | MFBHZ | passenger window rear up (MFBH+MFBZ) |
| 32 | 25 | 0x80 | 0x80 | MFBHA | passenger window rear down (MFBH+MFBA) |
| 33 | 26 | 0x01 | 0x01 | MCD_DI | -- |
| 34 | 26 | 0x02 | 0x02 | CS_STP | -- |
| 35 | 26 | 0x04 | 0x04 | 56AL | -- |
| 36 | 26 | 0x08 | 0x08 | 56AR | -- |
| 37 | 26 | 0x10 | 0x10 | 49VR | -- |
| 37 | 26 | 0x10 | 0x10 | DOP_RH_INDICATOR_LGT | right hand indicator (49VR+49HR_49ZR) |
| 38 | 26 | 0x20 | 0x20 | 49HR_49ZR | -- |
| 39 | 26 | 0x40 | 0x40 | 58VR_58IVR_58IHR | -- |
| 39 | 26 | 0x40 | 0x40 | DOP_RH_POSITION_LGT | right hand position light (58VR_58IVR_58IHR+58HR) |
| 40 | 26 | 0x80 | 0x80 | 58HL | -- |
| 41 | 27 | 0x01 | 0x01 | 2_8 | -- |
| 42 | 27 | 0x02 | 0x02 | 2_9 | -- |
| 43 | 27 | 0x04 | 0x04 | INRS_12V__NG_12V | -- |
| 43 | 27 | 0x04 | 0x04 | DOP_12V_EXT_PWR | -- |
| 44 | 27 | 0x08 | 0x08 | Atmel_CLK | -- |
| 45 | 27 | 0x10 | 0x10 | Atmel_DiDo | -- |
| 46 | 27 | 0x20 | 0x20 | 2_13 | -- |
| 47 | 27 | 0x40 | 0x40 | WD_Trigger | -- |
| 48 | 27 | 0x80 | 0x80 | MERHK | -- |
| 48 | 27 | 0x80 | 0x80 | DOP_BOOT_RELEASE | boot release motor |
| 49 | 28 | 0x01 | 0x01 | MFFZ | driver window up |
| 49 | 28 | 0x01 | 0x01 | DOP_DRV_WIN_UP | driver window up |
| 50 | 28 | 0x02 | 0x02 | MFFA | driver window down |
| 50 | 28 | 0x02 | 0x02 | DOP_DRV_WIN_DOWN | driver window down |
| 51 | 28 | 0x04 | 0x04 | MFBZ | passenger window up |
| 51 | 28 | 0x04 | 0x04 | DOP_PASS_WIN_UP | passenger window up |
| 52 | 28 | 0x08 | 0x08 | MFBA | passenger window down |
| 52 | 28 | 0x08 | 0x08 | DOP_PASS_WIN_DOWN | passenger window down |
| 53 | 28 | 0x10 | 0x10 | P34 | -- |
| 54 | 28 | 0x20 | 0x20 | P35 | -- |
| 55 | 28 | 0x40 | 0x40 | SIRENE | -- |
| 55 | 28 | 0x40 | 0x40 | DOP_SOUND_ALARM | BBS version Alarm |
| 56 | 28 | 0x80 | 0x80 | STDWA | -- |
| 56 | 28 | 0x80 | 0x80 | DOP_BBS_ARM_DISARM | BBS Arm/Disarm |
| 57 | 29 | 0x01 | 0x01 | 3_8 | -- |
| 58 | 29 | 0x02 | 0x02 | 3_9 | -- |
| 59 | 29 | 0x04 | 0x04 | 3_10 | -- |
| 60 | 29 | 0x08 | 0x08 | 3_11 | -- |
| 61 | 29 | 0x10 | 0x10 | MCD_CS2 | -- |
| 62 | 29 | 0x20 | 0x20 | 3_13 | -- |
| 63 | 29 | 0x40 | 0x40 | 3_14 | -- |
| 64 | 29 | 0x80 | 0x80 | 3_15 | -- |
| 65 | 30 | 0x01 | 0x01 | EE_CLK | -- |
| 66 | 30 | 0x02 | 0x02 | EE_DI | -- |
| 67 | 30 | 0x04 | 0x04 | 4_2 | -- |
| 68 | 30 | 0x08 | 0x08 | EE_CS | -- |
| 69 | 30 | 0x10 | 0x10 | MER | -- |
| 69 | 30 | 0x10 | 0x10 | DOP_COMMON_LOCK_RLY | common relay |
| 70 | 30 | 0x20 | 0x20 | MZS | -- |
| 70 | 30 | 0x20 | 0x20 | DOP_SUPER_LOCK_RLY | super lock relay |
| 71 | 30 | 0x40 | 0x40 | 4_6 | -- |
| 72 | 30 | 0x80 | 0x80 | 4_7 | -- |
| 73 | 31 | 0x01 | 0x01 | VS_PULL_EIN | -- |
| 74 | 31 | 0x02 | 0x02 | EN_EKS | -- |
| 75 | 31 | 0x04 | 0x04 | EN_PU | -- |
| 76 | 31 | 0x08 | 0x08 | 6_3 | -- |
| 77 | 31 | 0x10 | 0x10 | 6_4 | -- |
| 78 | 31 | 0x20 | 0x20 | MVR | -- |
| 78 | 31 | 0x20 | 0x20 | DOP_REST_LOCK_RLY | rest lock relay |
| 79 | 31 | 0x40 | 0x40 | MVRFT | -- |
| 79 | 31 | 0x40 | 0x40 | DOP_DRV_LOCK_RLY | driver lock relay |
| 80 | 31 | 0x80 | 0x80 | MCD_SCLK | -- |
| 81 | 32 | 0x01 | 0x01 | IB | -- |
| 82 | 32 | 0x02 | 0x02 | 56BL | -- |
| 83 | 32 | 0x04 | 0x04 | 54M | -- |
| 84 | 32 | 0x08 | 0x08 | 56BR | -- |
| 85 | 32 | 0x10 | 0x10 | KRB | -- |
| 86 | 32 | 0x20 | 0x20 | VA | -- |
| 87 | 32 | 0x40 | 0x40 | 58K | -- |
| 87 | 32 | 0x40 | 0x40 | DOP_NO_PLATE_LGT | number plate light |
| 88 | 32 | 0x80 | 0x80 | DWA_LED_ST10 | -- |
| 89 | 33 | 0x01 | 0x01 | 54R | -- |
| 90 | 33 | 0x02 | 0x02 | 54L | -- |
| 91 | 33 | 0x04 | 0x04 | 55HL | left rear fog light |
| 91 | 33 | 0x04 | 0x04 | DOP_RR_FOG_LGT | rear fog light (55HL+55HR) |
| 92 | 33 | 0x08 | 0x08 | 49VL | -- |
| 92 | 33 | 0x08 | 0x08 | DOP_LH_INDICATOR_LGT | left hand indicator (49VL+49HL_49ZL) |
| 93 | 33 | 0x10 | 0x10 | 55HR | right rear fog light |
| 93 | 33 | 0x10 | 0x10 | IB2 | Puddle lights |
| 94 | 33 | 0x20 | 0x20 | 49HL_49ZL | -- |
| 95 | 33 | 0x40 | 0x40 | 58VL_58IVL_58IHL | -- |
| 95 | 33 | 0x40 | 0x40 | DOP_LH_POSITION_LGT | left hand position light (58VL_58IVL_58IHL+58HL) |
| 96 | 33 | 0x80 | 0x80 | 58HR | -- |
| 97 | 34 | 0x01 | 0x01 | MFL12V | -- |
| 97 | 34 | 0x01 | 0x01 | DOP_ROTARY_SUPPLY | Supply to the rotary switch |
| 98 | 34 | 0x02 | 0x02 | HFS_LED | -- |
| 98 | 34 | 0x02 | 0x02 | DOP_HT_FT_WIN_LED | HFS LED |
| 99 | 34 | 0x04 | 0x04 | HFS_RA | -- |
| 99 | 34 | 0x04 | 0x04 | DOP_HEATED_FT_WIN_RLY | HFS Relay coil |
| 100 | 34 | 0x08 | 0x08 | 55V_RA | -- |
| 100 | 34 | 0x08 | 0x08 | DOP_FT_FOG_LGT_RLY | Front Fog Relay coil |
| 101 | 34 | 0x10 | 0x10 | 56Z_RA | -- |
| 102 | 34 | 0x20 | 0x20 | WI_H | -- |
| 105 | 13 | 0x01 | 0x01 | DOP_RR_WIPER_RLY | Rear Wiper switch (Wischer Hinten Schalter) |
| 103 | 34 | 0x40 | 0x40 | WI1 | -- |
| 103 | 34 | 0x40 | 0x40 | DOP_FT_WIPER_PARK_RUN | front wiper slow park run relay |
| 104 | 34 | 0x80 | 0x80 | HHS_RA | -- |
| 104 | 34 | 0x80 | 0x80 | DOP_HEATED_RR_WIN_RLY | heated rear window relay coil |
| 105 | 35 | 0x01 | 0x01 | GEBL_RA | -- |
| 105 | 35 | 0x01 | 0x01 | DOP_BLOWER_ENABLE | enable the blower motor |
| 106 | 35 | 0x02 | 0x02 | UML_LED | -- |
| 106 | 35 | 0x02 | 0x02 | DOP_RECIRC_LED | Indicator for the Recirc ON |
| 107 | 35 | 0x04 | 0x04 | HHS_LED | -- |
| 107 | 35 | 0x04 | 0x04 | DOP_HT_RR_WIN_LED | heated rear window LED |
| 108 | 35 | 0x08 | 0x08 | 55_LED | -- |
| 108 | 35 | 0x08 | 0x08 | DOP_RR_FOG_LED | Rear fog light indicator |
| 109 | 35 | 0x10 | 0x10 | DWALED | -- |
| 109 | 35 | 0x10 | 0x10 | DOP_ALARM_LED | alarm LED output |
| 110 | 35 | 0x20 | 0x20 | AC_LED | -- |
| 110 | 35 | 0x20 | 0x20 | DOP_AC_LED | A/C LED |
| 111 | 35 | 0x40 | 0x40 | WI2 | -- |
| 111 | 35 | 0x40 | 0x40 | DOP_FT_WIPER_SLOW_FAST | front wiper slow fast relay |
| 112 | 35 | 0x80 | 0x80 | SRA | -- |
| 112 | 35 | 0x80 | 0x80 | DOP_PWR_WASH_RLY | powerwash relay coil |
| 113 | 36 | 0x01 | 0x01 | KBUS_R | -- |
| 114 | 36 | 0x02 | 0x02 | KBUS_15 | -- |
| 115 | 36 | 0x04 | 0x04 | EngineRunning | -- |
| 116 | 36 | 0x08 | 0x08 | EwsManipulated | -- |
| 117 | 36 | 0x10 | 0x10 | CVM_FA | -- |
| 118 | 36 | 0x20 | 0x20 | CVM_FZ | -- |
| 119 | 36 | 0x40 | 0x40 | CVM_VKA | -- |
| 120 | 36 | 0x80 | 0x80 | CVM_TopClosed | -- |
| 121 | 37 | 0x01 | 0x01 | KL_R | -- |
| 122 | 37 | 0x02 | 0x02 | KL15 | -- |
| 123 | 37 | 0x04 | 0x04 | KL50 | -- |
| 124 | 37 | 0x08 | 0x08 | KL58 | -- |
| 125 | 37 | 0x10 | 0x10 | EWS_free | -- |
| 126 | 37 | 0x20 | 0x20 | EWS_Key | -- |
| 127 | 37 | 0x40 | 0x40 | KB_CS | -- |
| 128 | 37 | 0x80 | 0x80 | RDC | -- |
| 129 | 38 | 0x01 | 0x01 | CSMODE | -- |
| 130 | 38 | 0x02 | 0x02 | DIAGMODE | -- |
| 131 | 38 | 0x04 | 0x04 | ZV | -- |
| 132 | 38 | 0x08 | 0x08 | ZS | -- |
| 133 | 38 | 0x10 | 0x10 | SEr | -- |
| 134 | 38 | 0x20 | 0x20 | WB | -- |
| 135 | 38 | 0x40 | 0x40 | OA | -- |
| 136 | 38 | 0x80 | 0x80 | ES | -- |
| 137 | 39 | 0x01 | 0x01 | QFFZ | -- |
| 138 | 39 | 0x02 | 0x02 | QFBZ | -- |
| 139 | 39 | 0x04 | 0x04 | QFFHZ | -- |
| 140 | 39 | 0x08 | 0x08 | QFBHZ | -- |
| 141 | 39 | 0x10 | 0x10 | SoftOn | -- |
| 142 | 39 | 0x20 | 0x20 | KB_FSHD | -- |
| 143 | 39 | 0x40 | 0x40 | KB_KOE | -- |
| 144 | 39 | 0x80 | 0x80 | KB_KS | -- |
| 145 | 40 | 0x01 | 0x01 | FB_Bat | -- |
| 146 | 40 | 0x02 | 0x02 | FB_NR | -- |
| 147 | 40 | 0x04 | 0x04 | FB_Send_L | -- |
| 148 | 40 | 0x08 | 0x08 | FB_Send_H | -- |
| 149 | 40 | 0x10 | 0x10 | FB_VR | -- |
| 150 | 40 | 0x20 | 0x20 | FB_ER | -- |
| 151 | 40 | 0x40 | 0x40 | FB_HK | -- |
| 152 | 40 | 0x80 | 0x80 | KB_VKER | -- |
| 153 | 41 | 0x01 | 0x01 | Send_L | -- |
| 154 | 41 | 0x02 | 0x02 | Send_H | -- |
| 155 | 41 | 0x04 | 0x04 | FZVSIG | -- |
| 156 | 41 | 0x08 | 0x08 | FZVKEY | -- |
| 157 | 41 | 0x10 | 0x10 | TASTE1 | -- |
| 158 | 41 | 0x20 | 0x20 | TASTE2 | -- |
| 159 | 41 | 0x40 | 0x40 | TASTE3 | -- |
| 160 | 41 | 0x80 | 0x80 | FuInit | -- |
| 161 | 42 | 0x01 | 0x01 | LOBAT1 | -- |
| 162 | 42 | 0x02 | 0x02 | LOBAT2 | -- |
| 163 | 42 | 0x04 | 0x04 | LOBAT3 | -- |
| 164 | 42 | 0x08 | 0x08 | LOBAT4 | -- |
| 165 | 42 | 0x10 | 0x10 | FSIB | -- |
| 166 | 42 | 0x20 | 0x20 | FsaHK | -- |
| 167 | 42 | 0x40 | 0x40 | Zv1Fs | -- |
| 168 | 42 | 0x80 | 0x80 | Zv0Fs | -- |
| 169 | 43 | 0x01 | 0x01 | FRISCHL | Ansteuern der Umluftklappe |
| 169 | 43 | 0x01 | 0x01 | DOP_RECIRC_CTL1 | Ansteuern der Umluftklappe |
| 170 | 43 | 0x02 | 0x02 | UMLUFT | Ansteuern der Umluftklappe |
| 170 | 43 | 0x02 | 0x02 | DOP_RECIRC_CTL2 | Ansteuern der Umluftklappe |
| 171 | 43 | 0x04 | 0x04 | LWR12V | -- |
| 172 | 43 | 0x08 | 0x08 | KB_ShdPanicClose | -- |
| 173 | 43 | 0x10 | 0x10 | spare21_4 | -- |
| 174 | 43 | 0x20 | 0x20 | PLWR | -- |
| 175 | 43 | 0x40 | 0x40 | HSSV | -- |
| 176 | 43 | 0x80 | 0x80 | HSSH | -- |
| 177 | 44 | 0x01 | 0x01 | WIST1 | -- |
| 178 | 44 | 0x02 | 0x02 | WIST2 | -- |
| 179 | 44 | 0x04 | 0x04 | POTIST1 | -- |
| 180 | 44 | 0x08 | 0x08 | POTIST2 | -- |
| 181 | 44 | 0x10 | 0x10 | POTIERR | -- |
| 182 | 44 | 0x20 | 0x20 | WAPO | -- |
| 183 | 44 | 0x40 | 0x40 | spare22_7 | -- |
| 184 | 44 | 0x80 | 0x80 | spare22_8 | -- |
| 185 | 45 | 0x01 | 0x01 | DippedBeam | -- |
| 186 | 45 | 0x02 | 0x02 | PosLamp | -- |
| 187 | 45 | 0x04 | 0x04 | MainBeam | -- |
| 188 | 45 | 0x08 | 0x08 | FrontFog | -- |
| 189 | 45 | 0x10 | 0x10 | RearFog | -- |
| 190 | 45 | 0x20 | 0x20 | DirectionIndicatorLeftHand | -- |
| 191 | 45 | 0x40 | 0x40 | DirectionIndicatorRightHand | -- |
| 192 | 45 | 0x80 | 0x80 | DirectionIndicatorFaultDblFrq | -- |
| 193 | 46 | 0x01 | 0x01 | DirectionIndicatorLeftFault | -- |
| 194 | 46 | 0x02 | 0x02 | DirectionIndicatorRightFault | -- |
| 195 | 46 | 0x04 | 0x04 | DirectionIndicatorReSync | -- |
| 196 | 46 | 0x08 | 0x08 | TrailerPresent | -- |
| 197 | 46 | 0x10 | 0x10 | RearFogSwitchState | -- |
| 198 | 46 | 0x20 | 0x20 | Pictograms | -- |
| 199 | 46 | 0x40 | 0x40 | spare25_7 | -- |
| 200 | 46 | 0x80 | 0x80 | spare25_8 | -- |
| 201 | 47 | 0x01 | 0x01 | ClimaxStateAC | -- |
| 202 | 47 | 0x02 | 0x02 | AskKompressorState | -- |
| 203 | 47 | 0x04 | 0x04 | CommandCoolingFluidOff | -- |
| 204 | 47 | 0x08 | 0x08 | SwitchDLH | -- |
| 205 | 47 | 0x10 | 0x10 | spare26_5 | -- |
| 206 | 47 | 0x20 | 0x20 | spare26_6 | -- |
| 207 | 47 | 0x40 | 0x40 | FreshAir_Status | -- |
| 208 | 47 | 0x80 | 0x80 | AirCirculation_Status | -- |
| 209 | 48 | 0x01 | 0x01 | VentVal | -- |
| 210 | 48 | 0x02 | 0x02 | VentValBit2 | -- |
| 211 | 48 | 0x04 | 0x04 | VentValBit3 | -- |
| 212 | 48 | 0x08 | 0x08 | VentValBit4 | -- |
| 213 | 48 | 0x10 | 0x10 | VentValSpare5 | -- |
| 214 | 48 | 0x20 | 0x20 | VentValSpare6 | -- |
| 215 | 48 | 0x40 | 0x40 | VentValSpare7 | -- |
| 216 | 48 | 0x80 | 0x80 | VentValSpare8 | -- |
| 217 | 49 | 0x01 | 0x01 | Command_HHS_KB | -- |
| 218 | 49 | 0x02 | 0x02 | Command_HFS_KB | -- |
| 219 | 49 | 0x04 | 0x04 | Command_FreshAir | -- |
| 220 | 49 | 0x08 | 0x08 | Command_AirCirculation | -- |
| 221 | 49 | 0x10 | 0x10 | AirStatusReq | -- |
| 223 | 49 | 0x40 | 0x40 | Compressor | -- |
| 224 | 49 | 0x80 | 0x80 | RadioOn | -- |
| 225 | 50 | 0x01 | 0x01 | OutdoorTemp | -- |
| 226 | 50 | 0x02 | 0x02 | OutdoorTempBit1 | -- |
| 227 | 50 | 0x04 | 0x04 | OutdoorTempBit2 | -- |
| 228 | 50 | 0x08 | 0x08 | OutdoorTempBit3 | -- |
| 229 | 50 | 0x10 | 0x10 | OutdoorTempBit4 | -- |
| 230 | 50 | 0x20 | 0x20 | OutdoorTempBit5 | -- |
| 231 | 50 | 0x40 | 0x40 | OutdoorTempBit6 | -- |
| 232 | 50 | 0x80 | 0x80 | OutdoorTempBit7 | -- |
| 233 | 51 | 0x01 | 0x01 | KMH | -- |
| 234 | 51 | 0x02 | 0x02 | KMHBit1 | -- |
| 235 | 51 | 0x04 | 0x04 | KMHBit2 | -- |
| 236 | 51 | 0x08 | 0x08 | KMHBit3 | -- |
| 237 | 51 | 0x10 | 0x10 | KMHBit4 | -- |
| 238 | 51 | 0x20 | 0x20 | KMHBit5 | -- |
| 239 | 51 | 0x40 | 0x40 | KMHBit6 | -- |
| 240 | 51 | 0x80 | 0x80 | KMHBit7 | -- |
| 241 | 52 | 0x01 | 0x01 | GKL | -- |
| 242 | 52 | 0x02 | 0x02 | GKLBit1 | -- |
| 243 | 52 | 0x04 | 0x04 | GKLBit2 | -- |
| 244 | 52 | 0x08 | 0x08 | GKLBit3 | -- |
| 245 | 52 | 0x10 | 0x10 | GKLBit4 | -- |
| 246 | 52 | 0x20 | 0x20 | GKLBit5 | -- |
| 247 | 52 | 0x40 | 0x40 | GKLBit6 | -- |
| 248 | 52 | 0x80 | 0x80 | GKLBit7 | -- |
| 249 | 53 | 0x01 | 0x01 | EwsActKeyNum | -- |
| 250 | 53 | 0x02 | 0x02 | EwsActKeyNumBit1 | -- |
| 251 | 53 | 0x04 | 0x04 | EwsActKeyNumBit2 | -- |
| 252 | 53 | 0x08 | 0x08 | EwsActKeyNumBit3 | -- |
| 253 | 53 | 0x10 | 0x10 | EwsActKeyNumBit4 | -- |
| 254 | 53 | 0x20 | 0x20 | EwsActKeyNumBit5 | -- |
| 255 | 53 | 0x40 | 0x40 | EwsActKeyNumBit6 | -- |
| 256 | 53 | 0x80 | 0x80 | EwsActKeyNumBit7 | -- |
| XY | XY | 0xXY | 0xXY | XY | nicht definiertes Signal |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 171 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Interner Fehler: interne Spannung |
| 0x01 | Wischer: Sicherung fuer Pumpe, Innenlicht, Verbraucherabschaltung |
| 0x02 | Zentralverriegelung: Sicherung |
| 0x03 | Zentralverriegelung: Crash-Eingang dauernd aktiv/Crash-Sensor ausgelöst |
| 0x04 | Energiesparmode gesetzt |
| 0x05 | BC1rd Kodierung im Anlieferzustand |
| 0x06 | Diebstahlwarnanlage: Sirene Kurzschluss gegen U-Batt |
| 0x07 | Diebstahlwarnanlage: STDWA Kurzschluss gegen U-Batt |
| 0x08 | Fensterheber: Sicherung |
| 0x09 | Fensterheber: Unterbrechung Elektro-Motor oder Relais Fahrertuer |
| 0x0A | Fensterheber: Unterbrechung Elektro-Motor oder Relais Beifahrertuer |
| 0x0B | Fensterheber: Unterbrechung Elektro-Motor oder Relais Fahrerseite hinten |
| 0x0C | Fensterheber: Unterbrechung Elektro-Motor oder Relais Beifahrerseite hinten |
| 0x0D | Fensterheber: Unterbrechung Einklemmschutzleiste Fahrertuer |
| 0x0E | Fensterheber: Unterbrechung Einklemmschutzleiste Beifahrertuer |
| 0x0F | Fensterheber: Unterbrechung Einklemmschutzleiste Fahrerseite hinten |
| 0x10 | Fensterheber: Unterbrechung Einklemmschutzleiste Beifahrerseite hinten |
| 0x20 | Interner Fehler: Prozessor Watchdog |
| 0x21 | Interner Fehler: Prozessor ROM |
| 0x22 | Interner Fehler: Taktgeber |
| 0x23 | Interner Fehler: EEPROM schreiben |
| 0x24 | Zentralverriegelung Relais Verriegeln: Oeffnerkontakt unterbricht oder Schliesserkontakt klebt |
| 0x25 | Zentralverriegelung Relais Entriegeln: Oeffnerkontakt unterbricht oder Schliesserkontakt klebt |
| 0x26 | Zentralverriegelung Relais Sichern: Oeffnerkontakt unterbricht oder Schliesserkontakt klebt |
| 0x27 | Zentralverriegelung Relais Verriegeln Fahrertuer: Oeffnerkontakt unterbricht oder Schliesserkontakt klebt |
| 0x28 | Zentralverriegelung: Relais zieht nicht an bei Verriegeln |
| 0x29 | Zentralverriegelung: Relais zieht nicht an bei Entriegeln |
| 0x2A | Zentralverriegelung: Relais zieht nicht an bei Sichern |
| 0x2B | Zentralverriegelung: Relais zieht nicht an bei Verriegeln Fahrertuer |
| 0x2C | Fensterheber: Relais klebt bei Fahrertuer |
| 0x2D | Fensterheber: Relais klebt bei Beifahrertuer |
| 0x30 | K-Bus oder Steuergeraet fuer Instrumenten-Kombination (Gateway) |
| 0x31 | Wischerschalter (Potentiometer): Leitungsunterbrechung oder Kurzschluss gegen U-Batt |
| 0x32 | Wischerschalter (Potentiometer): Kurzschluss gegen Masse |
| 0x33 | Wischer vorne: blockiert oder Rueckstellkontakt |
| 0x34 | Wischer vorne: Relais oder Leitung WI1 Kurzschluss gegen U-Batt fuer Wischer ein |
| 0x35 | Wischer vorne: Relais oder Leitung WI2 Kurzschluss gegen U-Batt fuer Wischer ein |
| 0x36 | Wischer vorne: Relais fehlt oder Leitung fuer Wischer ein Kurzschluss gegen Masse oder Leitungsunterbrechung |
| 0x37 | Wischer vorne: Relais fehlt oder Leitung fuer Wischerstufe 2 Kurzschluss gegen Masse oder Leitungsunterbrechung |
| 0x38 | Wischer vorne: Pumpe fuer Scheibenwaschen oder Behaelter leer |
| 0x39 | Scheinwerferpumpe: Relais oder Leitung SRA Kurzschluss gegen U-Batt |
| 0x3A | Scheinwerferreinigung: Relais oder Leitung fuer Pumpe Kurzschluss gegen Masse oder Leitungsunterbrechung |
| 0x3B | Innenlicht: Kurzschluss |
| 0x3C | Zentralverriegelung: Leitungsunterbrechung bei Antrieb Heckklappe |
| 0x3D | Zentralverriegelung: Kurzschluss bei Antrieb Heckklappe |
| 0x3E | Heckscheibe: Aggregat oder Leitung RERHS Kurzschluss gegen U-Batt |
| 0x3F | Zentralverriegelung: Kurzschluss gegen Masse oder Leitungsunterbrechung bei Relais fuer Entriegeln Heckscheibe |
| 0x40 | Diebstahlwarnanlage: DWA-LED oder Leitung DWALED Kurzschluss gegen U-Batt |
| 0x41 | Diebstahlwarnanlage: Neigungsgeber |
| 0x42 | Diebstahlwarnanlage: Innenraumschutz |
| 0x43 | Diebstahlwarnanlage: Innenraumschutz hinten |
| 0x44 | BC1rd: uncodiert oder Codierung verloren |
| 0x45 | Zentralverriegelung: Schlosskontakt Fahrertuer ERFT und VRFT gleichzeitig aktiv |
| 0x46 | Zentralverriegelung: Schlosskontakt Beifahrertuer ERBT und VRBT gleichzeitig aktiv |
| 0x47 | Interner Fehler: Prozessor Interrupt |
| 0x48 | Innenlicht: Leitungsunterbrechung |
| 0x4A | Verbraucherabschaltung 1: Kurzschluss gegen Masse |
| 0x4B | Interner Fehler: Checksum ROM |
| 0x4C | MuW Master (vorn links): defekt |
| 0x4D | MuW Slave1 (vorn rechts): defekt |
| 0x4E | MuW Slave2 (hinten rechts):defekt |
| 0x4F | MuW Slave3 (hinten links): defekt |
| 0x50 | 49VR: Blinker vorne rechts Kurzschluss |
| 0x51 | 49VL: Blinker vorne links Kurzschluss |
| 0x52 | 49HR+49ZR: Blinker hinten rechts und Zusatzblinker rechts Kurzschluss |
| 0x53 | 49HL+49ZL: Blinker hinten links und Zusatzblinker links Kurzschluss |
| 0x54 | 54R: Bremslicht rechts Kurzschluss |
| 0x55 | 54L: Bremslicht links Kurzschluss |
| 0x56 | 54M: Bremslicht Mitte Kurzschluss |
| 0x57 | 55V RA Kurzschluss |
| 0x58 | 55HR: Nebelschlusslicht rechts Kurzschluss |
| 0x59 | 55HL: Nebelschlusslicht links Kurzschluss |
| 0x5A | 56AR: Fernlicht rechts Kurzschluss |
| 0x5B | 56AL: Fernlicht links Kurzschluss |
| 0x5C | 56BR: Abblendlicht rechts Kurzschluss |
| 0x5D | 56BL: Abblendlicht links Kurzschluss |
| 0x5E | 56Z RA Kurzschluss |
| 0x5F | 58VR/58IVR/58IHR: Standlicht vorne rechts oder Seitenmarkierungslicht vorne rechts oder Seitenmarkierungslicht hinten rechts Kurzschluss |
| 0x60 | 58VL/58IVL/58IHL: Standlicht vorne links oder Seitenmarkierungslicht vorne links oder Seitenmarkierungslicht hinten links Kurzschluss |
| 0x61 | 58HR: Schlusslicht rechts hinten Kurzschluss |
| 0x62 | 58HL: Schlusslicht links hinten Kurzschluss |
| 0x63 | 58K: Kennzeichenleuchte Kurzschluss |
| 0x64 | 49VR: Blinker vorne rechts Unterbrechung |
| 0x65 | 49VL: Blinker vorne links Unterbrechung |
| 0x66 | 49HR: und 49ZR Blinker hinten rechts und Zusatzblinker rechts Unterbrechung |
| 0x67 | 49HR: Blinker hinten rechts Unterbrechung |
| 0x68 | 49ZR: Zusatzblinker rechts Unterbrechung |
| 0x69 | 49HL und 49ZL Blinker hinten links und Zusatzblinker links Unterbrechung |
| 0x6A | 49HL: Blinker hinten links Unterbrechung |
| 0x6B | 49ZL: Zusatzblinker links Unterbrechung |
| 0x6C | 54R: Bremslicht rechts Unterbrechung |
| 0x6D | 54L: Bremslicht links Unterbrechung |
| 0x6E | 54M: Bremslicht Mitte Unterbrechung |
| 0x6F | 55V RA Unterbrechung |
| 0x70 | 55HR: Nebelschlusslicht rechts Unterbrechung |
| 0x71 | 55HL: Nebelschlusslicht links Unterbrechung |
| 0x72 | 56AR: Fernlicht rechts Unterbrechung |
| 0x73 | 56AL: Fernlicht links Unterbrechung |
| 0x74 | 56BR: Abblendlicht rechts Unterbrechung |
| 0x75 | 56BL: Abblendlicht links Unterbrechung |
| 0x76 | 56Z RA Unterbrechung  |
| 0x77 | 58VR: und 58IVR und 58IHR: Standlicht vorne rechts und Seitenmarkierungslicht vorne rechts und Seitenmarkierungslicht hinten rechts Unterbrechung |
| 0x78 | 58VL: und 58IVL und 58IHL: Standlicht vorne links und Seitenmarkierungslicht vorne links und Seitenmarkierungslicht hinten links Unterbrechung |
| 0x79 | 58HR: Schlusslicht rechts hinten Unterbrechung |
| 0x7A | 58HL: Schlusslicht links hinten Unterbrechung |
| 0x7B | 58K: Kennzeichenleuchte Unterbrechung |
| 0x7C | KRB: Kofferraumbeleuchtung Unterbrechung |
| 0x7D | KRB: Kofferraumbeleuchtung Kurzschluss |
| 0x7E | MFL12V: Versorgungsspannung MFL Kurzschluss gegen Masse |
| 0x7F | MFL12V: Versorgungsspannung MFL Unterbrechung oder Kurzschluss gegen U-Batt |
| 0x80 | HFS LED: Frontscheibenheizung LED Kurzschluss gegen Masse |
| 0x81 | HFS LED: Frontscheibenheizung LED Unterbrechung oder Kurzschluss gegen U-Batt |
| 0x82 | HFS RA: Frontscheibenheizung Relais Kurzschluss gegen U-Batt |
| 0x83 | HFS RA: Frontscheibenheizung Relais Unterbrechung oder Kurzschluss gegen Masse |
| 0x84 | 55V RA: Nebelscheinwerfer Relais Kurzschluss gegen U-Batt |
| 0x85 | 55V RA: Nebelscheinwerfer Relais Unterbrechung oder Kurzschluss gegen Masse |
| 0x86 | 56Z RA: Zusatzscheinwerfer Relais Kurzschluss gegen U-Batt |
| 0x87 | 56Z RA: Zusatzscheinwerfer Relais Unterbrechung oder Kurzschluss gegen Masse |
| 0x88 | WI H: Relais Wischer hinten Kurzschluss gegen U-Batt |
| 0x89 | WI H: Relais Wischer hinten Unterbrechung oder Kurzschluss gegen Masse |
| 0x8A | HHS RA: Heckscheibenheizung Relais Kurzschluss gegen U-Batt |
| 0x8B | HHS RA: Heckscheibenheizung Relais Unterbrechung oder Kurzschluss gegen Masse |
| 0x8C | GEBL RA: Gebläsemotor Relais Kurzschluss gegen U-Batt |
| 0x8E | GEBL RA: Gebläsemotor Relais Unterbrechung oder Kurzschluss gegen Masse |
| 0x8F | UML LED: Umluft LED Kurzschluss gegen Masse |
| 0x90 | UML LED: Umluft LED Unterbrechung oder Kurzschluss gegen U-Batt |
| 0x91 | HHS LED: Heckscheibenheizung LED Unterbrechung oder Kurzschluss gegen Masse |
| 0x92 | HHS LED: Heckscheibenheizung LED Kurzschluss gegen U-Batt |
| 0x93 | 55 LED: Nebelschlusslicht LED Kurzschluss gegen Masse |
| 0x94 | 55 LED: Nebelschlusslicht LED Unterbrechung oder Kurzschluss gegen U-Batt |
| 0x95 | DWALED: DWA LED Kurzschluss gegen Masse |
| 0x96 | DWALED: DWA LED Unterbrechung oder Kurzschluss gegen U-Batt |
| 0x97 | AC LED: Klimaanlage LED Kurzschluss gegen Masse |
| 0x98 | AC LED: Klimaanlage LED Unterbrechung oder Kurzschluss gegen U-Batt |
| 0x99 | Interner Fehler: ADC defekt |
| 0x9A | Trailer |
| 0x9B | Trailer BLK L |
| 0x9C | Trailer BLK R |
| 0x9D | Trailer BL |
| 0x9E | Trailer SL L |
| 0x9F | Trailer SL R |
| 0xA0 | Trailer NSL RF |
| 0xA1 | FUSE 30DW |
| 0xA2 | FUSE 30PW |
| 0xA3 | FUSE 30CDL |
| 0xA4 | FUSE 30IB |
| 0xA5 | FUSE 30A |
| 0xA6 | FUSE 30B |
| 0xA7 | FUSE 30E |
| 0xB2 | Interner Fehler: EEPROM lesen |
| 0xC0 | FLASH BEAM Schalter Kurzschluss |
| 0xC1 | DIRECTION INDICATOR Schalter Kurzschluss |
| 0xC2 | Bremslicht Schalter Kurzschluss |
| 0xC3 | Umluft Motor FRISCH Kurzschluss |
| 0xC4 | Umluft Motor UMLUFT Kurzschluss |
| 0xC8 | Klima Kompressor antwortet nicht zum BC1 |
| 0xC9 | LWR Treiberfehler |
| 0xCA | LWR Spulenfehler |
| 0xCB | LWR vorderer Sensor Unterbrechung |
| 0xCC | LWR hinterer Sensor Unterbrechung |
| 0xCD | Wischer hinten: blockiert oder Rueckstellkontakt |
| 0xCE | Keine Rückmeldung vom Regensensor |
| 0xCF | IB2 Vorfeldleuchte Kurzschluss |
| 0xD0 | IB2 Vorfeldleuchte Unterbrechung |
| 0xD1 | WWA-LED: Kurzschluss |
| 0xD2 | WWA-LED: Unterbrechung |
| 0xD3 | Regen/Licht-Sensor: Fehler oder unplausibles Signal (FLC in Fail Save Mode) |
| 0xE7 | 58VR+58IVR+58IHR+58HR: mehrdeutige Fehlerkombination |
| 0xE8 | 58VL+58IVL+58IHL+58HL: mehrdeutige Fehlerkombination |
| 0xEB | 58K+KRB: mehrdeutige Fehlerkombination |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0xXY | unbekannte Fehlerart |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 46 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x80 | Alarmspeicher: Klemme R |
| 0x81 | Alarmspeicher: Tuerkontakt Fahrertuer |
| 0x82 | Alarmspeicher: Tuerkontakt Beifahrertuer |
| 0x85 | Alarmspeicher: Heckklappe |
| 0x87 | Alarmspeicher: RDC |
| 0x88 | Alarmspeicher: Motorhaube |
| 0x89 | Alarmspeicher: Neigungsgeber |
| 0x8A | Alarmspeicher: Funkinnenraumschutz |
| 0x8B | Alarmspeicher: Funkinnenraumschutz hinten (R52) |
| 0x8C | Alarmspeicher: Reserve |
| 0x8D | Alarmspeicher: Schlosskontakt Fahrertuer |
| 0x8E | Alarmspeicher: Schlosskontakt Beifahrertuer |
| 0x8F | Alarmspeicher: Panik-Mode wurde ausgeloest |
| 0x90 | Batteriespannung: Unterbrechung |
| 0x91 | Crash: wurde ausgeloest |
| 0x92 | Wiederholsperre: Zentralverriegelung |
| 0x93 | Wiederholsperre: Entriegelung Heckklappe |
| 0x95 | Wiederholsperre: Fensterheber |
| 0xA0 | Prozessor Reset Info: TRAP_NMI |
| 0xA1 | Prozessor Reset Info:TRAP_STKOF |
| 0xA2 | Prozessor Reset Info:TRAP_STKUF |
| 0xA3 | Prozessor Reset Info:TRAP_UNDOPC |
| 0xA4 | Prozessor Reset Info:TRAP_PRTFLT |
| 0xA5 | Prozessor Reset Info:TRAP_ILLOPA |
| 0xA6 | Prozessor Reset Info:TRAP_ILLINA |
| 0xA7 | Prozessor Reset Info:TRAP_ILLBUS |
| 0xA8 | Prozessor Reset Info:TRAP_NOT_POWERON_RESET |
| 0xA9 | Prozessor Reset Info:PLL_UNLOCK |
| 0xB0 | Handling K-Bus Nachricht Info: KBUS_UNKNOWN |
| 0xB1 | Handling K-Bus Nachricht Info: KBUS_RECEPTION |
| 0xB2 | Handling K-Bus Nachricht Info: KBUS_PARITY |
| 0xB3 | Handling K-Bus Nachricht Info: KBUS_FRAMING |
| 0xB4 | Handling K-Bus Nachricht Info: KBUS_OVERRUN |
| 0xB5 | Handling K-Bus Nachricht Info: KBUS_RX_FULL_ERROR |
| 0xB6 | Handling K-Bus Nachricht Info: KBUS_RX_FULL_CS |
| 0xB7 | Handling K-Bus Nachricht Info: KBUS_BITKIPPER |
| 0xB8 | Handling K-Bus Nachricht Info: KBUS_LENGTH |
| 0xB9 | Handling K-Bus Nachricht Info: KBUS_RX_FULL |
| 0xBA | Handling K-Bus Nachricht Info: KBUS_SSM |
| 0xBB | Handling K-Bus Nachricht Info: KBUS_TOO_SHORT |
| 0xC0 | Rear wiper off due to KL.15 off without RSK |
| 0xD0 | Alarmspeicher: MuW Slave1 (vorn rechts) |
| 0xD1 | Alarmspeicher: MuW Slave2 (hinten rechts) |
| 0xD2 | Alarmspeicher: MuW Slave3 (hinten links) |
| 0xD3 | Alarmspeicher: MuW Master (vorn links) |
| 0xXY | unbekannter Info-Ort |

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0xXY | unbekannte Fehlerart |

<a id="table-bc1-dwa-bits"></a>
### BC1_DWA_BITS

Dimensions: 28 rows × 5 columns

| NAME | BYTE | MASK | VALUE | DESCRIPTION |
| --- | --- | --- | --- | --- |
| T_MHK | 3 | 0x01 | 0x01 | DWA-Trigger MHK |
| T_HKK | 3 | 0x02 | 0x02 | DWA-Trigger HKK |
| T_KLR_15 | 3 | 0x04 | 0x04 | DWA-Trigger KLR_15 |
| T_TKFT | 3 | 0x08 | 0x08 | DWA-Trigger TKFT |
| T_TKBT | 3 | 0x10 | 0x10 | DWA-Trigger TKBT |
| T_NG | 3 | 0x20 | 0x20 | DWA-Trigger NG |
| T_US | 3 | 0x40 | 0x40 | DWA-Trigger INRS |
| T_PANIC | 3 | 0x80 | 0x80 | DWA-Trigger Panic Mode |
| T_SCLOSS_FT | 4 | 0x01 | 0x01 | DWA-Trigger Schloss FT ER&VR |
| T_SCHLOSS_BT | 4 | 0x02 | 0x02 | DWA-Trigger Schloss BT ER&VR |
| T_MUW_VR | 4 | 0x10 | 0x10 | DWA-Trigger MUW Sensor VR |
| T_MUW_HR | 4 | 0x20 | 0x20 | DWA-Trigger MUW Sensor HR |
| T_MUW_HL | 4 | 0x40 | 0x40 | DWA-Trigger MUW Sensor HL |
| T_MUW_VL | 4 | 0x80 | 0x80 | DWA-Trigger MUW Sensor VL |
| ST_DWA | 5 | 0x01 | 0x01 | Status DWA |
| ST_ALARM | 5 | 0x02 | 0x02 | Status DWA ALarm |
| ST_HKK | 5 | 0x04 | 0x04 | Status HKK (aktiviert/deaktiviert) |
| ST_NG | 5 | 0x08 | 0x08 | Status NG (aktiviert/deaktiviert) |
| ST_INRS | 5 | 0x10 | 0x10 | Status INRS (aktiviert/deaktiviert) |
| SIG_HKK | 5 | 0x20 | 0x20 | Signal HKK |
| SIG_NG | 5 | 0x40 | 0x40 | Signal NG |
| SIG_INRS | 5 | 0x80 | 0x80 | Signal INRS |
| STORED_NG | 6 | 0x01 | 0x01 | Gespeicherter Trigger NG |
| STORED_INRS | 6 | 0x02 | 0x02 | Gespeicherter Trigger INRS |
| STORED_MUW_VR | 6 | 0x10 | 0x10 | Gespeicherter Trigger MUW VR |
| STORED_MUW_HR | 6 | 0x20 | 0x20 | Gespeicherter Trigger MUW HR |
| STORED_MUW_HL | 6 | 0x40 | 0x40 | Gespeicherter Trigger MUW HL |
| STORED_MUW_VL | 6 | 0x80 | 0x80 | Gespeicherter Trigger MUW VL |
