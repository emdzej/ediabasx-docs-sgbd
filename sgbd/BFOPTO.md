# BFOPTO.prg

- Jobs: [34](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | OPPS Optisches Prüf- und Programmiersystem |
| ORIGIN | BMW VS-22 Volk |
| REVISION | 1.00 |
| AUTHOR | BMW VS-22 Volk |
| COMMENT | N/A |
| PACKAGE | 1.24 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [STEUERN_KOMMUNIKATIONS_MODE](#job-steuern-kommunikations-mode) - OPPS in Kommunikationsmodus setzen
- [STEUERN_MOST_MESSMODE](#job-steuern-most-messmode) - Einstellen Messmodus MOST
- [STEUERN_KOMMUNIKATIONSPARAMETER](#job-steuern-kommunikationsparameter) - Einstellen der Kommunikationsparameter für BMW fast
- [STEUERN_ADS4MOST_MODE](#job-steuern-ads4most-mode) - Kommandos nach STEUERN_ADS4MOST_MODE an ADS4MOST Treiber
- [STEUERN_BYTEFLIGHT_MODE](#job-steuern-byteflight-mode) - Kommandos nach STEUERN_BYTEFLIGHT_MODE an BYTEFLIGHT
- [STEUERN_SET_MODUS](#job-steuern-set-modus) - Master oder Slave, Clockmaster
- [STEUERN_FORCE_WAKEUP](#job-steuern-force-wakeup)
- [STATUS_IDENT](#job-status-ident) - OPPS Identdaten
- [STATUS_SELBSTTEST](#job-status-selbsttest) - Ausführen System-Check
- [STEUERN_OPPS_RESET](#job-steuern-opps-reset) - Durchführen Reset OPPS
- [STATUS_SPANNUNG_MOST](#job-status-spannung-most) - Spannungsüberwachung
- [STATUS_SENDELEISTUNG_MESSUNG](#job-status-sendeleistung-messung) - Messung der Sendeleistung
- [STATUS_MEASUREOPTICALPOWER](#job-status-measureopticalpower) - Messung der Sendeleistung
- [STATUS_GETOPTICALPOWER](#job-status-getopticalpower) - Messung der Sendeleistung
- [STATUS_TEMPERATUR](#job-status-temperatur)
- [STEUERN_SENDELEISTUNG](#job-steuern-sendeleistung)
- [STEUERN_KALIBRIERUNG_MOST](#job-steuern-kalibrierung-most)
- [STATUS_POTENTIOMETER_OFFSET_ABGLEICH](#job-status-potentiometer-offset-abgleich) - Digitaler Offset Abgleich im Sende- und Empfangstrakt Immer vor Opto-Abgleich durchführen Faser: max. 3dB Dämpfung darf verwendet werden
- [STEUERN_OPTISCHER_ABGLEICH](#job-steuern-optischer-abgleich) - Abgleich des Sendetrakts mit Referenzempfaenger
- [STEUERN_SPANNUNGSVERSORGUNG_UISIS](#job-steuern-spannungsversorgung-uisis) - UISIS, Spannungsversorgung der Satelliten zu/abschalten
- [STATUS_SPANNUNG_OPPS_BYTEFLIGHT](#job-status-spannung-opps-byteflight) - Spannungswerte
- [STATUS_LEITUNGSTEST_OPPS_BYTEFLIGHT](#job-status-leitungstest-opps-byteflight) - Leitungstest auf Kurzschluss
- [STEUERN_GATEWAY_PARAMETER](#job-steuern-gateway-parameter) - Sende/Empfangsparameter einstellen  
- [STEUERN_SENDELEISTUNG_A_W_DBM](#job-steuern-sendeleistung-a-w-dbm) - Sendeleistung fuer Kommunikation mit Satellit einstellen
- [STEUERN_START_KOMMUNIKATION](#job-steuern-start-kommunikation) - Start Kommunikation mit Satellit  
- [STEUERN_NACHRICHTEN_SENDEN_EMPFANGEN](#job-steuern-nachrichten-senden-empfangen) - Kommunikation Sende/Empfangstest  
- [STEUERN_SLEEP_MODE](#job-steuern-sleep-mode) - SG in Schlafmodus setzen  
- [STEUERN_EMPFANGSPEAK_LEISTUNG](#job-steuern-empfangspeak-leistung) - Empfangspeakleistung messen
- [STATUS_EMPFANGSPEAK_LEISTUNG](#job-status-empfangspeak-leistung) - Empfangspeakleistung messen
- [STEUERN_MODUL_INITIALISIEREN](#job-steuern-modul-initialisieren) - Optotestermodul aktivieren/Moduladresse bereitstellen KWP2000: $31 SG spezifische Daten lesen $E0 Modul aktivieren
- [STATUS_MODUL_RESET](#job-status-modul-reset) - Optotesterservices allgemein (JOB_NUMMER+JOB_DATEN) KWP2000: $31 SG spezifische Daten lesen $E1 Steuergeraete Status lesen Modus  : Default

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

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

<a id="job-ident"></a>
### IDENT

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-kommunikations-mode"></a>
### STEUERN_KOMMUNIKATIONS_MODE

OPPS in Kommunikationsmodus setzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-steuern-most-messmode"></a>
### STEUERN_MOST_MESSMODE

Einstellen Messmodus MOST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-steuern-kommunikationsparameter"></a>
### STEUERN_KOMMUNIKATIONSPARAMETER

Einstellen der Kommunikationsparameter für BMW fast

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-ads4most-mode"></a>
### STEUERN_ADS4MOST_MODE

Kommandos nach STEUERN_ADS4MOST_MODE an ADS4MOST Treiber

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-steuern-byteflight-mode"></a>
### STEUERN_BYTEFLIGHT_MODE

Kommandos nach STEUERN_BYTEFLIGHT_MODE an BYTEFLIGHT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-steuern-set-modus"></a>
### STEUERN_SET_MODUS

Master oder Slave, Clockmaster

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CLOCK_MASTER | int | 0 = Slave 1 = Clock Master |
| NETWORK_MASTER | int | 0 = Network Master deaktiviert 1 = Network Master |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-steuern-force-wakeup"></a>
### STEUERN_FORCE_WAKEUP

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WAKEUP | int | 0 = Forcing wakeup deaktiviert 1 = Forcing wakeup aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-status-ident"></a>
### STATUS_IDENT

OPPS Identdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_PRODUCERNAME | string | Byte 0-31 in Response von ifraw |
| STAT_HARDWARE_VERSION_WERT | int |  |
| STAT_HARDWARE_VERSION_EINH | string |  |
| STAT_FIRMWARE_VERSION_WERT | int |  |
| STAT_FIRMWARE_VERSION_EINH | string |  |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-status-selbsttest"></a>
### STATUS_SELBSTTEST

Ausführen System-Check

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SELBSTTEST_WERT | int | 0 OK Rest Nicht OK |
| STAT_SELBSTTEST_EINH | string | ohne Einheit |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-steuern-opps-reset"></a>
### STEUERN_OPPS_RESET

Durchführen Reset OPPS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-status-spannung-most"></a>
### STATUS_SPANNUNG_MOST

Spannungsüberwachung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SPANNUNG_MOST_WERT | int | Boardpower 1 EIN 0 AUS |
| STAT_SPANNUNG_MOST_EINH | string | Keine Einheit (Boolscher Wert) |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-status-sendeleistung-messung"></a>
### STATUS_SENDELEISTUNG_MESSUNG

Messung der Sendeleistung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_LICHTLEISTUNG_WERT | real | Bereich (3 bis 28)dB Ergebnis ohne Vorzeichen, muss von Anwendung mit -1 multipliziert werden |
| STAT_LICHTLEISTUNG_EINH | string | Einheit in dbm |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-status-measureopticalpower"></a>
### STATUS_MEASUREOPTICALPOWER

Messung der Sendeleistung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_MEASUREOPTICALPOWER_WERT | real |  |
| STAT_MEASUREOPTICALPOWER_EINH | string | Einheit in dbm |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-status-getopticalpower"></a>
### STATUS_GETOPTICALPOWER

Messung der Sendeleistung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_GETOPTICALPOWER_WERT | real |  |
| STAT_GETOPTICALPOWER_EINH | string | Einheit in dbm |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-status-temperatur"></a>
### STATUS_TEMPERATUR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TEMPERATUR_WERT | real |  |
| STAT_TEMPERATUR_EINH | string | Einheit in °C |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-steuern-sendeleistung"></a>
### STEUERN_SENDELEISTUNG

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENDELEISTUNG | int | Eingabe von negativen Werten im Bereich von -4 bis -10 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-steuern-kalibrierung-most"></a>
### STEUERN_KALIBRIERUNG_MOST

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NUMBER | int | Kalibrierwert wird unter Nummer 1,2 oder 3 gespeichert |
| USAGETYPE | int | 0: Make 1: MakeSave 2: MakeSaveUse |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_RUECKMELDUNG_WERT | int | Rückmeldung von OPPS 0 = OK 1 = Temperaturbereich ueberschritten 2 = Kalibrierwerte überschritten |
| STAT_RUECKMELDUNG_EINH | string | Keine Einheit |
| _TEL_ANTWORT | binary | Antwort des IFRAWMODE Befehls |

<a id="job-status-potentiometer-offset-abgleich"></a>
### STATUS_POTENTIOMETER_OFFSET_ABGLEICH

Digitaler Offset Abgleich im Sende- und Empfangstrakt Immer vor Opto-Abgleich durchführen Faser: max. 3dB Dämpfung darf verwendet werden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| STAT_POTENTIOMETER_OFFSET_ABGLEICH | int | 1 OK 0 Nicht OK |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-optischer-abgleich"></a>
### STEUERN_OPTISCHER_ABGLEICH

Abgleich des Sendetrakts mit Referenzempfaenger

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_EEPROM | int | 00h, Abgleich ohne EEPROM Speicherung F0h=240, Abgleich mit EEPROM Speicherung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OPTISCHER_ABGLEICH_WERT | int | 0 Nicht OK Alle Werte ungleich 0 OK |
| STAT_OPTISCHER_ABGLEICH_EINH | string |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-spannungsversorgung-uisis"></a>
### STEUERN_SPANNUNGSVERSORGUNG_UISIS

UISIS, Spannungsversorgung der Satelliten zu/abschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPANNUNGSVERSORGUNG_UISIS | int | 1 UISIS zuschalten 2 UISIS abschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spannung-opps-byteflight"></a>
### STATUS_SPANNUNG_OPPS_BYTEFLIGHT

Spannungswerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| STAT_SPANNUNG_EINH | string | Volt |
| STAT_SPANNUNG_OPPS_WERT | real | Kanal0: +12V auf +9V bei 1A, korrektes Ergebnis +9V |
| STAT_UISIS_PLUS_WERT | real | Kanal1: Spannungsversorgung UISIS |
| STAT_UISIS_PLUS_REFERENZ_WERT | real | Kanal2: Spannung Lastwiderstand Referenzempfaenger |
| STAT_UISIS_MASSE_REFERENZ_WERT | real | Kanal3, Masse-Seite des Lastwiderstands |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-leitungstest-opps-byteflight"></a>
### STATUS_LEITUNGSTEST_OPPS_BYTEFLIGHT

Leitungstest auf Kurzschluss

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| STAT_LEITUNGSTEST_OPPS_BYTEFLIGHT | int | 0 Nicht in Ordnung 1 In Ordnung |
| STAT_LEITUNGSTEST_BYTEFLIGHT_ADAPTER | int | 1 In Ordnung 2 UISIS Leitung offen oder Kabel nicht gesteckt 3 Masse Leitung offen 4 Kurzschluss zwischen UISIS und Masseleitung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-gateway-parameter"></a>
### STEUERN_GATEWAY_PARAMETER

Sende/Empfangsparameter einstellen  

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GATEWAY_MASTER_SLAVE | int | 0 Optotester=Slave(für SIM) 1 Optotester=Master |
| GATEWAY_DIAGNOSE_ADRESSE | int | Diagnose_ID aus byteflight-Nachrichtenkatalog ZGM  Diagnose_ID=144 SIM  Diagnose_ID=145 SZL  Diagnose_ID=146 SASL Diagnose_ID=147 SASR Diagnose_ID=148 STVL Diagnose_ID=149 STVR Diagnose_ID=150 SSFA Diagnose_ID=151 SSBF Diagnose_ID=152 SBSL Diagnose_ID=153 SBSR Diagnose_ID=154 SSH  Diagnose_ID=157 SFZ  Diagnose_ID=158 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sendeleistung-a-w-dbm"></a>
### STEUERN_SENDELEISTUNG_A_W_DBM

Sendeleistung fuer Kommunikation mit Satellit einstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TESTSIGNAL | int | 0 Testsignal aus 1 Testsignal ein |
| ART_SENDELEISTUNG_A_W_DBM | int | 0 Vorgabe in Ampere (LSB:0.0833A) 1 Vorgabe in Watt (LSB:0.25µW) 2 Vorgabe in dBm (LSB:0.1 dBm) |
| SENDELEISTUNG_A_W_DBM | int | Leistungsvorgabe nach Art_Sendeleistung Bsp.: in Watt ACHTUNG! Bitte Eingabe abh. von Art_Sendeleistung siehe folgende Zeilen Eingabe in Ampere n/12 (muss durch 12 teilbar sein) Eingabe in Watt n/4 (muss durch 4 teilbar sein) Eingabe in dBm n/10 (muss durch 10 teilbar sein) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-start-kommunikation"></a>
### STEUERN_START_KOMMUNIKATION

Start Kommunikation mit Satellit  

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MASTER_SLAVE | int | 1 Optotester=Master 2 Optotester=Slave (fuer SIM) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-nachrichten-senden-empfangen"></a>
### STEUERN_NACHRICHTEN_SENDEN_EMPFANGEN

Kommunikation Sende/Empfangstest  

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ADRESSE | int | Steuergeraet    Steuergeraeteadressen(hex/dec) ZGM             0h/0 SIM             1h/1 SZL             2h/2 SASL            3h/3 SASR            4h/4 STVL            5h/5 STVR            6h/6 SSFA            7h/7 SSBF            8h/8 SBSL            9h/9 SBSR            Ah/10 SSH             Dh/13 SFZ             Eh/14 |
| BYTE_1 | int | Schlechtester Fall: Byte_1=240 |
| BYTE_2 | int | Schlechtester Fall: Byte_2=255 |
| BYTE_3 | int | Schlechtester Fall: Byte_3=170 |
| BYTE_4 | int | Schlechtester Fall: Byte_4=85 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NACHRICHT | int | 0 Nicht in Ordnung 1 In Ordnung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sleep-mode"></a>
### STEUERN_SLEEP_MODE

SG in Schlafmodus setzen  

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-empfangspeak-leistung"></a>
### STEUERN_EMPFANGSPEAK_LEISTUNG

Empfangspeakleistung messen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABTASTZEITRAUM | int | ACHTUNG! Eingabe n/10 (muss durch 10 teilbar sein) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EMPFANGSPEAKLEISTUNG_W_WERT | real | Empfangspeakleistung in Watt am Faserende zum Optotester |
| STAT_EMPFANGSPEAKLEISTUNG_W_EINH | string | Empfangspeak-Leistung in Watt |
| STAT_EMPFANGSPEAKLEISTUNG_DBM_WERT | real | Empfangspeakleistung in dBm am Faserende zum Optotester |
| STAT_EMPFANGSPEAKLEISTUNG_DBM_EINH | string | Empfangspeak-Leistung in dBm |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-empfangspeak-leistung"></a>
### STATUS_EMPFANGSPEAK_LEISTUNG

Empfangspeakleistung messen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EMPFANGSPEAKLEISTUNG_W_WERT | real | Empfangspeakleistung in µWatt am Faserende zum Optotester |
| STAT_EMPFANGSPEAKLEISTUNG_W_EINH | string | Empfangspeak-Leistung in Watt |
| STAT_EMPFANGSPEAKLEISTUNG_DBM_WERT | real | Empfangspeakleistung in dBm am Faserende zum Optotester |
| STAT_EMPFANGSPEAKLEISTUNG_DBM_EINH | string | Empfangspeak-Leistung in dBm |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-modul-initialisieren"></a>
### STEUERN_MODUL_INITIALISIEREN

Optotestermodul aktivieren/Moduladresse bereitstellen KWP2000: $31 SG spezifische Daten lesen $E0 Modul aktivieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-modul-reset"></a>
### STATUS_MODUL_RESET

Optotesterservices allgemein (JOB_NUMMER+JOB_DATEN) KWP2000: $31 SG spezifische Daten lesen $E1 Steuergeraete Status lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERSION_SOFTWARE_WERT | real | Software-Version-Nummer |
| STAT_VERSION_SOFTWARE_EINH | string | Software-Version-Nummer_Einheit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (69 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 2 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0C | KWP2000 |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 95 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x10 | ERROR_ECU_GENERAL_REJECT |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUBFUNCTION_NOT_SUPPORTED__INVALID_FORMAT |
| 0x21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT_OR_REQUEST_SEQUENCE_ERROR |
| 0x23 | ERROR_ECU_ROUTINE_NOT_COMPLETE |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x33 | ERROR_ECU_SECURITY_ACCESS_DENIED__SECURITY_ACCESS_REQUESTED |
| 0x36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0x37 | ERROR_ECU_REQUIRED_TIME_DELAY_NOT_EXPIRED |
| 0x40 | ERROR_ECU_DOWNLOAD_NOT_ACCEPTED |
| 0x41 | ERROR_ECU_IMPROPER_DOWNLOAD_TYPE |
| 0x42 | ERROR_ECU_CANNOT_DOWNLOAD_TO_SPECIFIED_ADDRESS |
| 0x43 | ERROR_ECU_CANNOT_DOWNLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0x50 | ERROR_ECU_UPLOAD_NOT_ACCEPTED |
| 0x51 | ERROR_ECU_IMPROPER_UPLOAD_TYPE |
| 0x52 | ERROR_ECU_CANNOT_UPLOAD_FROM_SPECIFIED_ADDRESS |
| 0x53 | ERROR_ECU_CANNOT_UPLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0x71 | ERROR_ECU_TRANSFER_SUSPENDED |
| 0x72 | ERROR_ECU_TRANSFER_ABORTED |
| 0x74 | ERROR_ECU_ILLEGAL_ADDRESS_IN_BLOCK_TRANSFER |
| 0x75 | ERROR_ECU_ILLEGAL_BYTE_COUNT_IN_BLOCK_TRANSFER |
| 0x76 | ERROR_ECU_ILLEGAL_BLOCK_TRANSFER_TYPE |
| 0x77 | ERROR_ECU_BLOCKTRANSFER_DATA_CHECKSUM_ERROR |
| 0x78 | ERROR_ECU_REQUEST_CORRECTLY_RECEIVED__RESPONSE_PENDING |
| 0x79 | ERROR_ECU_INCORRECT_BYTE_COUNT_DURING_BLOCK_TRANSFER |
| 0x80 | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_DIAGNOSTIC_MODE |
| ?00? | OKAY |
| ?02? | ERROR_ECU_INCORRECT_RESPONSE_ID |
| ?03? | ERROR_ECU_INCORRECT_LEN |
| ?04? | ERROR_ECU_INCORRECT_LIN_RESPONSE_ID |
| ?05? | ERROR_ECU_INCORRECT_LIN_LEN |
| ?10? | ERROR_F_CODE |
| ?11? | ERROR_TABLE |
| ?12? | ERROR_INTERPRETATION |
| ?13? | ERROR_F_POS |
| ?20? | ERROR_SEGMENT |
| ?21? | ERROR_ADDRESS |
| ?22? | ERROR_NUMBER |
| ?30? | ERROR_DATA |
| ?40? | ERROR_MODE |
| ?41? | ERROR_BAUDRATE |
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?60? | ERROR_DATA_OUT_OF_RANGE |
| ?70? | ERROR_NUMBER_ARGUMENT |
| ?71? | ERROR_RANGE_ARGUMENT |
| ?72? | ERROR_VERIFY |
| ?73? | ERROR_NO_BIN_BUFFER |
| ?74? | ERROR_BIN_BUFFER |
| ?75? | ERROR_DATA_TYPE |
| ?76? | ERROR_CHECKSUM |
| ?80? | ERROR_FLASH_SIGNATURE_CHECK |
| ?81? | ERROR_VIHICLE_IDENTFICATON_NR |
| ?82? | ERROR_PROGRAMMING_DATE |
| ?83? | ERROR_ASSEMBLY_NR |
| ?84? | ERROR_CALIBRATION_DATASET_NR |
| ?85? | ERROR_EXHAUST_REGULATION_OR_TYPE_APPROVAL_NR |
| ?86? | ERROR_REPAIR_SHOP_NR |
| ?87? | ERROR_TESTER_SERIAL_NR |
| ?88? | ERROR_MILAGE |
| ?89? | ERROR_PROGRAMMING_REFERENCE |
| ?8A? | ERROR_NO_FREE_UIF |
| ?8B? | ERROR_MAX_UIF |
| ?8C? | ERROR_SIZE_UIF |
| ?8D? | ERROR_LEVEL |
| ?8E? | ERROR_KEY |
| ?8F? | ERROR_AUTHENTICATION |
| ?90? | ERROR_NO_DREF |
| ?91? | ERROR_CHECK_PECUHN |
| ?92? | ERROR_CHECK_PRGREF |
| ?93? | ERROR_AIF_NR |
| ?94? | ERROR_CHECK_DREF |
| ?95? | ERROR_CHECK_HWREF |
| ?96? | ERROR_CHECK_HWREF |
| ?97? | ERROR_CHECK_PRGREFB |
| ?98? | ERROR_CHECK_VMECUH*NB |
| ?99? | ERROR_CHECK_PRGREFB |
| ?9A? | ERROR_CHECK_VMECUH*N |
| ?9B? | ERROR_MOST_CAN_GATEWAY_DISABLE |
| ?9C? | ERROR_NO_P2MIN |
| ?9D? | ERROR_NO_P2MAX |
| ?9E? | ERROR_NO_P3MIN |
| ?9F? | ERROR_NO_P3MAX |
| ?A0? | ERROR_NO_P4MIN |
| ?B0? | ERROR_DIAG_PROT |
| ?B1? | ERROR_SG_ADRESSE |
| ?B2? | ERROR_SG_MAXANZAHL_AIF |
| ?B3? | ERROR_SG_GROESSE_AIF |
| ?B4? | ERROR_SG_ENDEKENNUNG_AIF |
| ?B5? | ERROR_SG_AUTHENTISIERUNG |
| ?C0? | ERROR_TELEGRAM_LEN_OUT_OFF_RANGE |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 69 rows × 2 columns

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
| 0xFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 14 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | kein passendes Fehlersymptom |
| 0x01 | Signal oder Wert oberhalb Schwelle |
| 0x02 | Signal oder Wert unterhalb Schwelle |
| 0x04 | kein Signal oder Wert |
| 0x08 | unplausibles Signal oder Wert |
| 0x10 | Testbedingungen erfuellt |
| 0x11 | Testbedingungen noch nicht erfuellt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler wuerde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler wuerde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 16 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |
