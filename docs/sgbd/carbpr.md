# carbpr.prg

- Jobs: [23](#jobs)
- Tables: [0](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | SCANTOOL-Schnittstelle nach SAE J1979 speziell fuer FASTA |
| ORIGIN | BMW EA34 Hecht |
| REVISION | 1.30 |
| AUTHOR | Josef Greppmair, GD |
| COMMENT | Abgeleitet von CARB.B2V |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Dieser Job wird vom EDIABAS automatisch beim erstem Zugriff auf eine SGBD aufgerufen. Bei weitern Zugriffen auf die selbe SGBD wird dieser Job nicht mehr aufgerufen. In der INITIALISIERUNG werden alle Funktionen aufgerufen, die nur einmal, vor der Kommunikation mit einem SG notwendig sind.
- [SCAN_ENDE](#job-scan-ende)
- [SCAN_IDENT](#job-scan-ident) - Information ueber verbaute Steuergeraete
- [SCAN_STATUS_READYNESS](#job-scan-status-readyness) - Anzahl Fehler, und MIL-Status
- [SCAN_KM_MIL_ON](#job-scan-km-mil-on) - Zurueckgelegte Wegstrecke mit eingeschalteter MIL
- [SCAN_ZEIT_MIL_ON](#job-scan-zeit-mil-on) - Zeit mit eingeschalteter MIL
- [SCAN_FF_TROUBLE_CODE](#job-scan-ff-trouble-code) - Last holen
- [SCAN_OBD_REQUIREMENT_VERSION](#job-scan-obd-requirement-version) - SCAN_OBD_REQUIREMENT_VERSION
- [SCAN_FF_ENGINE_RPM](#job-scan-ff-engine-rpm) - Freezeframewert fuer Drehzahl lesen
- [SCAN_ENGINE_RPM](#job-scan-engine-rpm) - aktuelle Drehzahl lesen
- [SCAN_PCODE_MODE3_LESEN](#job-scan-pcode-mode3-lesen) - PCODES holen
- [SCAN_FF_FUEL_SYSTEM](#job-scan-ff-fuel-system) - Status des Kraftstoffsystems
- [SCAN_FF_CALCULATED_LOAD](#job-scan-ff-calculated-load) - Last holen
- [GET_TEMPERATUR_MOTOR](#job-get-temperatur-motor) - Motortemperatur holen
- [GET_STATUS_LAMDAREGLER_BANK1](#job-get-status-lamdaregler-bank1) - Statuswert holen
- [GET_ADAPTION_LAMDAREGLER_BANK1](#job-get-adaption-lamdaregler-bank1) - Statuswert holen
- [GET_STATUS_LAMDAREGLER_BANK2](#job-get-status-lamdaregler-bank2) - Statuswert holen
- [GET_ADAPTION_LAMDAREGLER_BANK2](#job-get-adaption-lamdaregler-bank2) - Statuswert holen
- [GET_DRUCK_KRAFTSTOFF](#job-get-druck-kraftstoff) - Statuswert holen
- [GET_DRUCK_EINLASS](#job-get-druck-einlass) - Statuswert holen
- [GET_DREHZAHL](#job-get-drehzahl) - Statuswert holen
- [GET_GESCHWINDIGKEIT](#job-get-geschwindigkeit) - Statuswert holen

<a id="job-info"></a>
### INFO

Information SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergeraet im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Name aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch, english |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Dieser Job wird vom EDIABAS automatisch beim erstem Zugriff auf eine SGBD aufgerufen. Bei weitern Zugriffen auf die selbe SGBD wird dieser Job nicht mehr aufgerufen. In der INITIALISIERUNG werden alle Funktionen aufgerufen, die nur einmal, vor der Kommunikation mit einem SG notwendig sind.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 0:n.i.O. 1:i.O Default Automatic Required Result |

<a id="job-scan-ende"></a>
### SCAN_ENDE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |

<a id="job-scan-ident"></a>
### SCAN_IDENT

Information ueber verbaute Steuergeraete

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| SID_STEUERGERAETENR | int | Adresse des Steuergeraets |
| SID_TEL_ANTWORT | binary | Telegram eines Steuergeraets |

<a id="job-scan-status-readyness"></a>
### SCAN_STATUS_READYNESS

Anzahl Fehler, und MIL-Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| SCAN_STAT_PCODE_ANZAHL | int | Anzahl der Pcodes |
| SCAN_STAT_MIL | int | Status der MIL-Lampe (0 oder 1) |
| SCAN_STAT_READYNESS_TEL_ANTWORT | binary | Dump des Telegramms |
| SCAN_MISFIRE_SUPP | int | DATA B.0 (0 oder 1) |
| SCAN_FUEL_SYSTEM_SUPP | int | DATA B.1 (0 oder 1) |
| SCAN_COMPREHENSIVE_COMP_SUPP | int | DATA B.2 (0 oder 1) |
| SCAN_MISFIRE_STAT | int | DATA B.4 (0 oder 1) |
| SCAN_FUEL_SYSTEM_STAT | int | DATA B.5 (0 oder 1) |
| SCAN_COMPREHENSIVE_COMP_STAT | int | DATA B.6 (0 oder 1) |
| SCAN_CATALYST_SUPP | int | DATA C.0 (0 oder 1) |
| SCAN_HEATED_CATALYST_SUPP | int | DATA C.1 (0 oder 1) |
| SCAN_EVAPORATIVE_SYSTEM_SUPP | int | DATA C.2 (0 oder 1) |
| SCAN_SECONARY_AIR_SYSTEM_SUPP | int | DATA C.3 (0 oder 1) |
| SCAN_A_C_SYSTEM_REFRIGERANT_SUPP | int | DATA C.4 (0 oder 1) |
| SCAN_OXYGEN_SENSOR_SUPP | int | DATA C.5 (0 oder 1) |
| SCAN_OXYGEN_SENSOR_HEATER_SUPP | int | DATA C.6 (0 oder 1) |
| SCAN_EGR_SYSTEM_SUPP | int | DATA C.7 (0 oder 1) |
| SCAN_CATALYST_STAT | int | DATA D.0 (0 oder 1) |
| SCAN_HEATED_CATALYST_STAT | int | DATA D.1 (0 oder 1) |
| SCAN_EVAPORATIVE_SYSTEM_STAT | int | DATA D.2 (0 oder 1) |
| SCAN_SECONARY_AIR_SYSTEM_STAT | int | DATA D.3 (0 oder 1) |
| SCAN_A_C_SYSTEM_REFRIGERANT_STAT | int | DATA D.4 (0 oder 1) |
| SCAN_OXYGEN_SENSOR_STAT | int | DATA D.5 (0 oder 1) |
| SCAN_OXYGEN_SENSOR_HEATER_STAT | int | DATA D.6 (0 oder 1) |
| SCAN_EGR_SYSTEM_STAT | int | DATA D.7 (0 oder 1) |

<a id="job-scan-km-mil-on"></a>
### SCAN_KM_MIL_ON

Zurueckgelegte Wegstrecke mit eingeschalteter MIL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| SCAN_KM_MIL_ON_WERT | long | Wert fuer Zurueckgelegte Wegstrecke mit eingeschalteter MIL (0-65535km) |

<a id="job-scan-zeit-mil-on"></a>
### SCAN_ZEIT_MIL_ON

Zeit mit eingeschalteter MIL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| SCAN_ZEIT_MIL_ON_WERT | long | Zeitwert mit eingeschalteter MIL |

<a id="job-scan-ff-trouble-code"></a>
### SCAN_FF_TROUBLE_CODE

Last holen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| SCAN_FF_TROUBLE_CODE_WERT | int | Trouble Code |

<a id="job-scan-obd-requirement-version"></a>
### SCAN_OBD_REQUIREMENT_VERSION

SCAN_OBD_REQUIREMENT_VERSION

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| SCAN_OBD_REQUIREMENT_VERSION_WERT | int | Wert fuer SCAN_OBD_REQUIREMENT_VERSION $01 - OBDII (California ARB) $02 - OBDII (Federal EPA) $03 - OBD and OBDII $04 - OBDI $05 - Not intended to meet any OBD requirements $06 - EOBD (Europe) |

<a id="job-scan-ff-engine-rpm"></a>
### SCAN_FF_ENGINE_RPM

Freezeframewert fuer Drehzahl lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| SCAN_FF_ENGINE_RPM_WERT | real | Freezeframewert fuer Drehzahl lesen (0-16383.75 1/min) |

<a id="job-scan-engine-rpm"></a>
### SCAN_ENGINE_RPM

aktuelle Drehzahl lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| SCAN_ENGINE_RPM_WERT | real | aktuelle Drehzahl lesen (0-16383.75 1/min) |

<a id="job-scan-pcode-mode3-lesen"></a>
### SCAN_PCODE_MODE3_LESEN

PCODES holen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| S_PM3_PCODE | int | PCODE als integer |
| S_PM3_STEUERGERAETENR | int | Adresse des SG |

<a id="job-scan-ff-fuel-system"></a>
### SCAN_FF_FUEL_SYSTEM

Status des Kraftstoffsystems

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| SYSTEM1 | string | Status System 1 |
| SYSTEM2 | string | Status System 2 |

<a id="job-scan-ff-calculated-load"></a>
### SCAN_FF_CALCULATED_LOAD

Last holen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| WERT | int | Lastwert (0-100%) |

<a id="job-get-temperatur-motor"></a>
### GET_TEMPERATUR_MOTOR

Motortemperatur holen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| WERT | int | Temperaturwert (-40-215 Grad C) |

<a id="job-get-status-lamdaregler-bank1"></a>
### GET_STATUS_LAMDAREGLER_BANK1

Statuswert holen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| WERT | int | Statuswert (-100 - +99.22%) |

<a id="job-get-adaption-lamdaregler-bank1"></a>
### GET_ADAPTION_LAMDAREGLER_BANK1

Statuswert holen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| WERT | int | Statuswert (-100 - +99.22%) |

<a id="job-get-status-lamdaregler-bank2"></a>
### GET_STATUS_LAMDAREGLER_BANK2

Statuswert holen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| WERT | int | Statuswert (-100 - +99.22%) |

<a id="job-get-adaption-lamdaregler-bank2"></a>
### GET_ADAPTION_LAMDAREGLER_BANK2

Statuswert holen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| WERT | int | Statuswert (-100 - +99.22%) |

<a id="job-get-druck-kraftstoff"></a>
### GET_DRUCK_KRAFTSTOFF

Statuswert holen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| WERT | int | Statuswert (0-765kPaA) |

<a id="job-get-druck-einlass"></a>
### GET_DRUCK_EINLASS

Statuswert holen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| WERT | int | Statuswert (0-255kPaA) |

<a id="job-get-drehzahl"></a>
### GET_DREHZAHL

Statuswert holen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| WERT | int | Statuswert (0-16383/min) |

<a id="job-get-geschwindigkeit"></a>
### GET_GESCHWINDIGKEIT

Statuswert holen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Gibt fuer jeden Ergenissatz den Ergebnis- und Fehlerstatus zurueck Folgende Werte sind definiert: "OKAY"       =&gt; Alle Results dieses Satzes sind gueltig "ERROR"      =&gt; Allgemeiner Fehler (DEFAULT) "ERROR_NACK" =&gt; Kommunikationsfehler |
| SEND_TELEGRAM | binary | Dump des Telegramms |
| RECV_TELEGRAM | binary | Dump des Telegramms |
| WERT | int | Statuswert (0-255km/h) |

## Tables

No tables found.
