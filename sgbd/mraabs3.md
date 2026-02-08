# mraabs3.prg

- Jobs: [45](#jobs)
- Tables: [14](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ABS Steuergerät ABS3  |
| ORIGIN | I+ME_Actia_GmbH R&D Keck |
| REVISION | 1.090 |
| AUTHOR | I+ME Actia GmbH, Keck und BMW, Motorrad Kufer BMW |
| COMMENT | N/A |
| PACKAGE | 1.65 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [DIAGNOSEMODE_AUS](#job-diagnosemode-aus) - Diagnose Modus beenden
- [DIAGNOSEMODE_EIN](#job-diagnosemode-ein) - Diagnose Modus starten
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnose Mode des Steuergerätes aufrecht erhalten TesterPresent (0x3E)
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler)
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher Löschen
- [IDENT](#job-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [SECURITY_ACCESS](#job-security-access) - SG für erweiterte Diagnose freischalten Security Access (0x27)
- [START_KOMMUNIKATION](#job-start-kommunikation) - Kommunikation mit dem Steuergerät aufbauen
- [STATUS_AD_WERTE](#job-status-ad-werte) - AD-Werte lesen RDBLI 21, 01 bis 04
- [STATUS_ANALOG_RADGESCHWINDIGKEIT](#job-status-analog-radgeschwindigkeit)
- [STATUS_ANALOG_SPANNUNG](#job-status-analog-spannung) - analoge Spannungswerte auslesen
- [STATUS_DATE_OF_ECU_MANUFACTURING](#job-status-date-of-ecu-manufacturing) - Fahrzeughersteller Hardware Nr. Servcie 0x21, 0x9D
- [STATUS_DIGITAL](#job-status-digital)
- [STATUS_DRUCKWERTE](#job-status-druckwerte) - Druckwerte auslesen
- [STATUS_ECU_IDENTIFICATION_DATA_TABLE](#job-status-ecu-identification-data-table) - Steuergeräte Identifikation lesen Service 0x21, 0x80
- [STATUS_EEPROM_VERSION](#job-status-eeprom-version) - EEPROM Version lesen
- [STATUS_EEPROM_ZAEHLER](#job-status-eeprom-zaehler) - EEPROM Zähler lesen
- [STATUS_FAHRGESTELL_NR](#job-status-fahrgestell-nr) - Fahrgestell Nr. lesen, 7 letzte Stellen
- [STATUS_FAHRGESTELL_NR_EOL](#job-status-fahrgestell-nr-eol) - Fahrgestell Nr. EOL 7 letzte Stellen lesen
- [STATUS_FTE_SERIENNUMMER](#job-status-fte-seriennummer) - Hersteller (FTE) Serien Nr. auslesen
- [STATUS_FTE_SOFTWARE_NR](#job-status-fte-software-nr) - Security Access notwendig Job Hauptschleife anhalten notwendig
- [STATUS_GEHAEUSE_BARCODE](#job-status-gehaeuse-barcode)
- [STATUS_ICT_BARCODE](#job-status-ict-barcode)
- [STATUS_KODIERUNG_AD](#job-status-kodierung-ad) - Fahrzeugkodierung Ad Wert lesen SecurityKey notwendig Hardware Test Modus notwendig (job STEUERN_HAUPTSCHLEIFE_ANHALTEN)
- [STATUS_KODIERUNG_EEPROM](#job-status-kodierung-eeprom) - Fahrzeugkodierung aus dem Eeprom auslesen
- [STATUS_KODIERUNG_RAM](#job-status-kodierung-ram) - Fahrzeugkodierung aus dem RAM auslesen
- [STATUS_MAX_BAUDRATE](#job-status-max-baudrate) - Zeit Hauptschleife lesen maximale Baudrate lesen
- [STATUS_MODULATOR](#job-status-modulator) - Version Modulator lesen
- [STATUS_SOFTWARE_VERSION](#job-status-software-version) - Software Version Hauptrechner lesen
- [STATUS_VEHICLE_MANUFACTURER_HW_NR](#job-status-vehicle-manufacturer-hw-nr) - Fahrzeughersteller Hardware Nr. Servcie 0x21, 0x91
- [STATUS_ZULAESSIGE_KODIERUNGEN](#job-status-zulaessige-kodierungen) - zulässige Fahrzeugkodierungen auslesen
- [STEUERN_BREMSLICHT](#job-steuern-bremslicht) - Bremslicht einschalten Seed + HardwareTestModus integriert in Job Security Access notwendig Hardware Test Modus notwendig (job STEUERN_HAUPTSCHLEIFE_ANHALTEN)
- [STEUERN_BREMSLICHT_GEDIMMT](#job-steuern-bremslicht-gedimmt) - Bremslicht gedimmt einschalten Security Access notwendig Normal Modus notwendig (kein Hardware Test Modus) Job STEUERN_HAUPTSCHLEIFE_STARTEN
- [STEUERN_DEINIT_KLINE_KOMMUNIKATION](#job-steuern-deinit-kline-kommunikation) - Beendet eine laufende K-Line Kommunikation
- [STEUERN_FAHRZEUGCODIERUNG_EEPROM](#job-steuern-fahrzeugcodierung-eeprom) - Fahrzeug Kodierung in das EEPROM schreiben zulässige Kodierungen mit dem Dienst STATUS_ZULAESSIGE_KODIEURNGEN auslesen Security Access notwendig
- [STEUERN_HAUPTSCHLEIFE_ANHALTEN](#job-steuern-hauptschleife-anhalten) - Hauptschleife anhalten, Wechsel in den Hardware Test Modus Security Access notwendig
- [STEUERN_HAUPTSCHLEIFE_STARTEN](#job-steuern-hauptschleife-starten) - Hauptschleife starten, Wechsel in den Normal Modus Security Access notwendig
- [STEUERN_PUMPENMOTOR_HINTEN](#job-steuern-pumpenmotor-hinten) - Pumpenmotor hinten ansteuern, PWM Mode Seed + HardwareTestModus integriert in Job Security Access notwendig Hardware Test Modus notwendig (job STEUERN_HAUPTSCHLEIFE_ANHALTEN)
- [STEUERN_PUMPENMOTOR_VORN](#job-steuern-pumpenmotor-vorn) - Pumpenmotor vorn ansteuern, PWM Mode Seed + HardwareTestModus integriert in Job Security Access notwendig Hardware Test Modus notwendig (job STEUERN_HAUPTSCHLEIFE_ANHALTEN)
- [STEUERN_REGELVENTIL_HINTEN](#job-steuern-regelventil-hinten) - Regelventil hinten ansteuern, PWM Mode Seed + HardwareTestModus integriert in Job Security Access notwendig Hardware Test Modus notwendig (job STEUERN_HAUPTSCHLEIFE_ANHALTEN)
- [STEUERN_REGELVENTIL_VORN](#job-steuern-regelventil-vorn) - Regelventil vorn ansteuern, PWM Mode Seed + HardwareTestModus integriert in Job Security Access notwendig Hardware Test Modus notwendig (job STEUERN_HAUPTSCHLEIFE_ANHALTEN)
- [STEUERN_VIN_SCHREIBEN](#job-steuern-vin-schreiben) - Fahrgestell Nr. 7 letzte Stellen schreiben Security Access notwendig
- [STOP_KOMMUNIKATION](#job-stop-kommunikation) - Kommunikation mit dem Steuergerät beenden

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

<a id="job-diagnosemode-aus"></a>
### DIAGNOSEMODE_AUS

Diagnose Modus beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-diagnosemode-ein"></a>
### DIAGNOSEMODE_EIN

Diagnose Modus starten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BAUDRATEN_WERT | long | Baudrate default 10400, Baudrate 1200..156000 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANFRAGE | binary | Hex Antwort vom SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnose Mode des Steuergerätes aufrecht erhalten TesterPresent (0x3E)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen (alle Fehler)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers für KWP-2000 immer 2 |
| F_ANZAHL | int | Anzahl der Fehler im Speicher |
| F_ORT_NR | long | Index für den Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text Table FOrteTexte als ORTTEXT |
| F_SYMPTOM_NR | int | Index für die Fehlerart |
| F_SYMPTOM_TEXT | string | Fehlerart als Text Table FArtTexte als ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard Fehlerart) als Text |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard Fehlerart) als Text Fehlerart table ArtTexte als Text |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard Fehlerart) als Text |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hex Code |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher Löschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-ident"></a>
### IDENT

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_INDEX | string | Steuergerät Hardware Version |
| ID_COD_INDEX | int | Steuergerät Identifikation Code |
| ID_DIAGNOSE_INDEX | string | Steuergerät Diagnose Version |
| ID_NAME_WERT | int | System Name als Zahl |
| ID_NAME | string | System Name als Text |
| ID_DATE | string | Herstell Datum Tag.Monat.Jahr |
| ID_SUPPLIER_INDEX | int | Hersteller Index |
| ID_SUPPLIER_INDEX_TEXT | string | Hersteller Index |
| ID_CODE_VERSION | string | Software Version |
| VARIANTE_IND | string | Name der SGBD, immer MRAABS3 |
| ID_BUS_TYPE | string | CAN Bus Typ |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-security-access"></a>
### SECURITY_ACCESS

SG für erweiterte Diagnose freischalten Security Access (0x27)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-start-kommunikation"></a>
### START_KOMMUNIKATION

Kommunikation mit dem Steuergerät aufbauen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-ad-werte"></a>
### STATUS_AD_WERTE

AD-Werte lesen RDBLI 21, 01 bis 04

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_UBATT | int | AD Wert Batteriespannung |
| STAT_BREMSCHALTER_SPANNUNG_VORN | int | AD Wert Bremsschalter vorn |
| STAT_BREMSCHALTER_SPANNUNG_HINTEN | int | AD Wert Bremsschalter hinten |
| STAT_DREHZAHLSENSOR_VORN | int | AD Wert Drehzahlsensor vorn |
| STAT_DREHZAHLSENSOR_HINTEN | int | AD Wert Drehzahlsensor hinten |
| STAT_RADZYLINDERDRUCK_VORN | int | AD Wert Rad Zylinder Druck vorn |
| STAT_RADZYLINDERDRUCK_HINTEN | int | AD Wert Rad Zylinder Druck hinten |
| STAT_STEUERDRUCK_VORN | int | AD Wert Steuer Druck vorn |
| STAT_STEUERDRUCK_HINTEN | int | AD Wert Steuer Druck hinten |
| STAT_RADGESCHWINDIGKEIT_VORN | int | AD Wert Radgeschwindigkeit vorn |
| STAT_RADGESCHWINDIGKEIT_HINTEN | int | AD Wert Radgeschwindigkeit hinten |
| STAT_DIGITAL | int | Status Werte lesen |
| STAT_KODIERUNG_RAM | int | Status Werte lesen |

<a id="job-status-analog-radgeschwindigkeit"></a>
### STATUS_ANALOG_RADGESCHWINDIGKEIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_RAD_GESCHW_VORN_WERT | real | Rad Geschwindigkeit vorn |
| STAT_RAD_GESCHW_HINTEN_WERT | real | Rad Geschwindigkeit vorn |
| STAT_RAD_GESCHW_VORN_EINH | string | Einheit RadGeschwindigkeit |
| STAT_RAD_GESCHW_HINTEN_EINH | string | Einheit RadGeschwindigkeit hinten |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-analog-spannung"></a>
### STATUS_ANALOG_SPANNUNG

analoge Spannungswerte auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_UBATT_WERT | real | Batterispannung Kl.15 in V |
| STAT_BREMSSCHALTER_VORN_WERT | real | Spannung Bremslichtschalter vorn |
| STAT_BREMSSCHALTER_HINTEN_WERT | real | Spannung Bremslichtschalter hinten |
| STAT_DREHZAHLSENSOR_VORN_WERT | real | Spannung DrehzahlSensor vorn |
| STAT_DREHZAHLSENSOR_HINTEN_WERT | real | Spannung Drehzahlsensor hinten |
| STAT_EINHEIT | string | Einheit Volt |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-date-of-ecu-manufacturing"></a>
### STATUS_DATE_OF_ECU_MANUFACTURING

Fahrzeughersteller Hardware Nr. Servcie 0x21, 0x9D

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_DATE | string | Herstellungsdatum |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_BREMSLICHT | string | Bremslicht: nicht defekt, defekt |
| STAT_RUECKLICHT | string | Rücklicht: nicht defekt, defekt |
| STAT_BREMSFLUESSIGKEIT | string | Niveau Bremsflüssigkeit: OK, nicht OK |
| STAT_BREMSLICHTSCHALTER_VORN | string | Bremslichtschalter vorn: Ein, Aus |
| STAT_BREMSLICHTSCHALTER_HINTEN | string | Bremslichtschalter hinten: Ein, Aus |
| STAT_ABS_TASTER | string | ABS-Taster: Ein, Aus |
| STAT_REGELVENTIL_VORN | string | ABS-Regelventil vorn Status: Ein, Aus |
| STAT_REGELVENTIL_HINTEN | string | ABS-Regelventil hinten Status: Ein, Aus |
| STAT_STEUERVENTIL_VORN | string | ABS-Steuerventil vorn: Ein, Aus |
| STAT_STEUERVENTIL_HINTEN | string | ABS-Steuerventil hinten: Ein, Aus |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-druckwerte"></a>
### STATUS_DRUCKWERTE

Druckwerte auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_RADBREMSKREIS_VORN_WERT | real | Druckwert Radbremskreis vorn |
| STAT_RADBREMSKREIS_HINTEN_WERT | real | Druckwert Radbremskreis hinten |
| STAT_STEUERKREIS_VORN_WERT | real | Druckwert Radbremskreis vorn |
| STAT_STEUERKREIS_HINTEN_WERT | real | Druckwert Radbremskreis hinten |
| STAT_EINHEIT | string | Einheit Volt |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-ecu-identification-data-table"></a>
### STATUS_ECU_IDENTIFICATION_DATA_TABLE

Steuergeräte Identifikation lesen Service 0x21, 0x80

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_INDEX | string | Steuergerät Hardware Version |
| ID_COD_INDEX | int | Steuergerät Identifikation Code |
| ID_DIAGNOSE_INDEX | string | Steuergerät Diagnose Version |
| ID_NAME_WERT | int | System Name |
| ID_NAME | string | System Name |
| ID_DATE | string | Herstell Datum Tag.Monat.Jahr |
| ID_SUPPLIER_INDEX | int | Hersteller Index |
| ID_SUPPLIER_INDEX_TEXT | string | Hersteller Index |
| ID_CODE_VERSION | string | Software Version |
| ID_BUS_TYPE | string | CAN Bus Typ |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-eeprom-version"></a>
### STATUS_EEPROM_VERSION

EEPROM Version lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_VERSION | int | Eeprom Version |

<a id="job-status-eeprom-zaehler"></a>
### STATUS_EEPROM_ZAEHLER

EEPROM Zähler lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_EINSCHALTZEIT_WERT | string | Einschaltzeit |
| STAT_BREMSZEIT_VORN_WERT | string | Bremszeit vorn |
| STAT_BREMSZEIT_HINTEN_WERT | string | Bremszeit hinten |
| STAT_ABS_ZEIT_VORN_WERT | string | ABS Zeit vorn |
| STAT_ABS_ZEIT_HINTEN_WERT | string | ABS Zeit hinten |
| STAT_FEHLEZEITPUNKT_WERT | string | Fehlerzeitpunkt |
| STAT_EINHEIT | string | Zeit in Stunden:Minuten:Sekunden |

<a id="job-status-fahrgestell-nr"></a>
### STATUS_FAHRGESTELL_NR

Fahrgestell Nr. lesen, 7 letzte Stellen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Fahrgestell Nr. 7 letzte Stellen |

<a id="job-status-fahrgestell-nr-eol"></a>
### STATUS_FAHRGESTELL_NR_EOL

Fahrgestell Nr. EOL 7 letzte Stellen lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Fahrgestell Nr. 7 letzte Stellen |

<a id="job-status-fte-seriennummer"></a>
### STATUS_FTE_SERIENNUMMER

Hersteller (FTE) Serien Nr. auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SERIEN_NR | int | FTE Serien Nr. |
| WOCHE | int | Kalenderwoche |
| JAHR | int | Jahr |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-fte-software-nr"></a>
### STATUS_FTE_SOFTWARE_NR

Security Access notwendig Job Hauptschleife anhalten notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| HAUPTRECHNER | string | Version Hauptrechner |
| DATUM_HAUPTRECHNER | string | Datum Version Hauptrechner (Tag.Monat.Jahr) |
| KONTROLLRECHNER | string | Version Kontrollrechner |
| DATUM_KONTROLLRECHNER | string | Datum Version Kontrollrechner (Tag.Monat.Jahr) |
| KONTROLLRECHNER_ROM_CHECKSUMME | int | Checksumme Kontrollrechner |
| EEPROM_VERSION | int | Eeprom Version als Zahl |
| MODULATOR | string | Modulator |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-gehaeuse-barcode"></a>
### STATUS_GEHAEUSE_BARCODE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| TEILE_NR | unsigned long | Teilenummer |
| LAUFENDE_SERIEN_NR | unsigned long | Serien Nr |
| INTERNE_INDEX_NR | int | interne Index Nr |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-ict-barcode"></a>
### STATUS_ICT_BARCODE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| ICT_BARCODE | unsigned long | ICT Barcode |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-kodierung-ad"></a>
### STATUS_KODIERUNG_AD

Fahrzeugkodierung Ad Wert lesen SecurityKey notwendig Hardware Test Modus notwendig (job STEUERN_HAUPTSCHLEIFE_ANHALTEN)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STATUS_CODIERUNG1 | real | Codierung 1 als Zahl |
| STATUS_CODIERUNG2 | real | Codierung 2 als Zahl |
| STATUS_CODIERUNG3 | real | Codierung 3 als Zahl |
| STATUS_CODIERUNG4 | real | Codierung 4 als Zahl |
| STATUS_EINHEIT | string | Wert in Volt |

<a id="job-status-kodierung-eeprom"></a>
### STATUS_KODIERUNG_EEPROM

Fahrzeugkodierung aus dem Eeprom auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STATUS_CODIERUNG | int | Codierung als Zahl |
| STATUS_CODIERUNG_TEXT | string | Codierung als Text |

<a id="job-status-kodierung-ram"></a>
### STATUS_KODIERUNG_RAM

Fahrzeugkodierung aus dem RAM auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STATUS_CODIERUNG | int | Codierung als Zahl |
| STATUS_CODIERUNG_TEXT | string | Codierung als Text |

<a id="job-status-max-baudrate"></a>
### STATUS_MAX_BAUDRATE

Zeit Hauptschleife lesen maximale Baudrate lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_MAIN_LOOP_TIME_WERT | long | Zeit Hauptschleife in µs |
| STAT_MAIN_LOOP_TIME_EINHEIT | string | Einheit Zeit in Mikro Sekunden |
| STAT_MAX_BAUDRATE_WERT | long | maximale Baudrate |

<a id="job-status-modulator"></a>
### STATUS_MODULATOR

Version Modulator lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_VERSION | string | Modulator Version |

<a id="job-status-software-version"></a>
### STATUS_SOFTWARE_VERSION

Software Version Hauptrechner lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_VERSION | int | Software Version Hauptrechner |
| STAT_DATE | string | Datum Software Version Hauptrechner |

<a id="job-status-vehicle-manufacturer-hw-nr"></a>
### STATUS_VEHICLE_MANUFACTURER_HW_NR

Fahrzeughersteller Hardware Nr. Servcie 0x21, 0x91

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW Teile Nr |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-zulaessige-kodierungen"></a>
### STATUS_ZULAESSIGE_KODIERUNGEN

zulässige Fahrzeugkodierungen auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STATUS_CODIERUNG_WERT | int | Codierung als Zahl |
| STATUS_CODIERUNG_TEXT | string | Codierung als Text |

<a id="job-steuern-bremslicht"></a>
### STEUERN_BREMSLICHT

Bremslicht einschalten Seed + HardwareTestModus integriert in Job Security Access notwendig Hardware Test Modus notwendig (job STEUERN_HAUPTSCHLEIFE_ANHALTEN)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | int | 0 - ausgeschaltet, 1 - eingeschaltet |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-bremslicht-gedimmt"></a>
### STEUERN_BREMSLICHT_GEDIMMT

Bremslicht gedimmt einschalten Security Access notwendig Normal Modus notwendig (kein Hardware Test Modus) Job STEUERN_HAUPTSCHLEIFE_STARTEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | int | 0 - ausgeschaltet, 1 - eingeschaltet |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-deinit-kline-kommunikation"></a>
### STEUERN_DEINIT_KLINE_KOMMUNIKATION

Beendet eine laufende K-Line Kommunikation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | STEUERN_DEINIT_KLINE_KOMMUNIKATION erfolgreich |

<a id="job-steuern-fahrzeugcodierung-eeprom"></a>
### STEUERN_FAHRZEUGCODIERUNG_EEPROM

Fahrzeug Kodierung in das EEPROM schreiben zulässige Kodierungen mit dem Dienst STATUS_ZULAESSIGE_KODIEURNGEN auslesen Security Access notwendig

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KODIERUNG | int | mögliche Kodierungen, siehe Job: STATUS_ZULAESSIGE_KODIERUNGEN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-hauptschleife-anhalten"></a>
### STEUERN_HAUPTSCHLEIFE_ANHALTEN

Hauptschleife anhalten, Wechsel in den Hardware Test Modus Security Access notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-hauptschleife-starten"></a>
### STEUERN_HAUPTSCHLEIFE_STARTEN

Hauptschleife starten, Wechsel in den Normal Modus Security Access notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| JOB_STATUS2 | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-pumpenmotor-hinten"></a>
### STEUERN_PUMPENMOTOR_HINTEN

Pumpenmotor hinten ansteuern, PWM Mode Seed + HardwareTestModus integriert in Job Security Access notwendig Hardware Test Modus notwendig (job STEUERN_HAUPTSCHLEIFE_ANHALTEN)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PEGEL | int | PWM Pegel, gültig wenn PWM Mode = 1, mögliche Werte: 0, 1 |
| MODE | int | PWM Mode: 0 - normal, 1 - statisch |
| WERT | int | Motor: 0 - aus, 1 - ein |
| ZEIT | int | Zeit in Sekunden, max. 20 Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-pumpenmotor-vorn"></a>
### STEUERN_PUMPENMOTOR_VORN

Pumpenmotor vorn ansteuern, PWM Mode Seed + HardwareTestModus integriert in Job Security Access notwendig Hardware Test Modus notwendig (job STEUERN_HAUPTSCHLEIFE_ANHALTEN)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PEGEL | int | PWM Pegel, gültig wenn PWM Mode = 1, mögliche Werte: 0, 1 |
| MODE | int | PWM Mode: 0 - normal, 1 - statisch |
| WERT | int | Motor: 0 - aus, 1 - ein |
| ZEIT | int | Zeit in Sekunden, max. 20 Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-regelventil-hinten"></a>
### STEUERN_REGELVENTIL_HINTEN

Regelventil hinten ansteuern, PWM Mode Seed + HardwareTestModus integriert in Job Security Access notwendig Hardware Test Modus notwendig (job STEUERN_HAUPTSCHLEIFE_ANHALTEN)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PWM_WERT | int | Bereich: 1..622 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-regelventil-vorn"></a>
### STEUERN_REGELVENTIL_VORN

Regelventil vorn ansteuern, PWM Mode Seed + HardwareTestModus integriert in Job Security Access notwendig Hardware Test Modus notwendig (job STEUERN_HAUPTSCHLEIFE_ANHALTEN)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PWM_WERT | int | Bereich: 1..622 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-vin-schreiben"></a>
### STEUERN_VIN_SCHREIBEN

Fahrgestell Nr. 7 letzte Stellen schreiben Security Access notwendig

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FIN | string | Fahrgestell Nr. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-stop-kommunikation"></a>
### STOP_KOMMUNIKATION

Kommunikation mit dem Steuergerät beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

## Tables

### Index

- [BAUDRATE](#table-baudrate) (6 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (3 × 2)
- [DIGITALFEHLERSTATUS](#table-digitalfehlerstatus) (3 × 2)
- [FARTTEXTE](#table-farttexte) (10 × 2)
- [FORTTEXTE](#table-forttexte) (83 × 2)
- [FEHLERSTATUS](#table-fehlerstatus) (5 × 2)
- [FEHLERCODETEST](#table-fehlercodetest) (3 × 2)
- [JOBRESULT](#table-jobresult) (13 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [KODIERUNG](#table-kodierung) (12 × 2)
- [RESPONSECODE](#table-responsecode) (14 × 2)
- [SYSTEMNAMEORENGINETYPE](#table-systemnameorenginetype) (18 × 3)
- [WARNLAMPE](#table-warnlampe) (3 × 2)
- [LIEFERANTEN](#table-lieferanten) (81 × 2)

<a id="table-baudrate"></a>
### BAUDRATE

Dimensions: 6 rows × 2 columns

| BAUDRATENWERT | WERT |
| --- | --- |
| 9600 | 0x01 |
| 19200 | 0x02 |
| 38400 | 0x03 |
| 57600 | 0x04 |
| 115200 | 0x05 |
| 200000 | 0xFFFFFFFF |

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 3 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | AUS |
| 0x01 | EIN |
| 0xFF | UNBEKANNT |

<a id="table-digitalfehlerstatus"></a>
### DIGITALFEHLERSTATUS

Dimensions: 3 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Nicht in Ordnung |
| 0x01 | in Ordnung |
| 0xFF | UNBEKANNT |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 10 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | - |
| 0x01 | Unterbrechung oder Kurzschluss nach Plus |
| 0x02 | Kurzschluss nach Masse |
| 0x04 | kein Signal |
| 0x08 | Signal unplausibel |
| 0xFF | unbekannte Fehlerart |
| 0x20 | NICHT VORHANDEN |
| 0x21 | SPORADISCH |
| 0x22 | MOMEMTAN VORHANDEN |
| 0x23 | MOMEMTAN VORHANDEN UND GESPEICHERT |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 83 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x4113 | Interner Steuergerätefehler (Rechenfehler) Übertragungsfehler zwischen Rechner |
| 0x4181 | Interner Steuergerätefehler Zu langer Schlupfeinlauf während Regelung |
| 0x4182 | ABS-Sensorfehler Vorn |
| 0x4183 | Interner Steuergerätefehler Regelventil vorne defekt |
| 0x4184 | Interner Steuergerätefehler Analogwert Steuerdrucksensor vorn |
| 0x4185 | Radgeschwindigkeit Vorn fehlerhaft |
| 0x4187 | Kontrollrechner liefert keine Frequenz, während Hauptrechner Frequenz sieht |
| 0x41FF | Fehler bei erkanntem Spannungseinbruch aufgetreten |
| 0x4213 | Interner Steuergerätefehler (Rechenfehler) Übertragungsfehler zwischen Rechner |
| 0x4281 | Interner Steuergerätefehler Zu langer Schlupfeinlauf während Regelung |
| 0x4282 | ABS-Sensorfehler Hinten |
| 0x4285 | Radgeschwindigkeit Hinten fehlerhaft |
| 0x4287 | Kontrollrechner liefert keine Frequenz, während Hauptrechner Frequenz sieht |
| 0x42FF | Fehler bei erkanntem Spannungseinbruch aufgetreten |
| 0x4301 | Interner Steuergerätefehler Unzulässiger Interrupt |
| 0x4303 | Interner Steuergerätefehler RAM-Fehler im Test erkannt |
| 0x4304 | Interner Steuergerätefehler ROM-Fehler im Test erkannt |
| 0x4307 | Interner Steuergerätefehler (Rechenfehler) Hauptrechner Loop to long |
| 0x4308 | Interner Steuergerätefehler Stack Fehler |
| 0x4309 | Unterspannungsfehler bei Systemstart |
| 0x430A | Interner Steuergerätefehler Staudruck &gt; 5.5 bar Vorn |
| 0x430B | ABS-Motor vorn defekt |
| 0x430C | Interner Steuergerätefehler (Rechenfehler) Hauptrechner Loop to short |
| 0x430D | Interner Steuergerätefehler Kontrollrechner Loop to long |
| 0x430E | Interner Steuergerätefehler Analogwert Drucksensor vorne |
| 0x430F | Unzulässige Fahrzeugkodierung |
| 0x4312 | Interner Steuergerätefehler EEPROM Version passt nicht zum Hauptrechner |
| 0x4313 | Interner Steuergerätefehler (Rechenfehler) Übertragungsfehler zwischen Rechner |
| 0x4314 | Interner Steuergerätefehler (Rechenfehler) Timeout MainLoopStart |
| 0x4315 | Interner Steuergerätefehler Hauptrechner |
| 0x4316 | Interner Steuergerätefehler EEPROM defekt |
| 0x4317 | Interner Steuergerätefehler Kontrollrechner |
| 0x4318 | Interner Steuergerätefehler (Rechenfehler) Timeout Kommunikation Rechner |
| 0x431A | Interner Steuergerätefehler (Rechenfehler) Übertragungsfehler zwischen Rechner |
| 0x431B | Interner Steuergerätefehler Fehlerhafter Wert bei Berechnung |
| 0x431C | Interner Steuergerätefehler Fahrzeugparameter im EEPROM fehlerhaft |
| 0x431D | Zu geringer Druck im vorderen Radkreis |
| 0x431E | Zu hoher Druck im vorderen Radkreis |
| 0x431F | Interner Steuergerätefehler 2 mal AD-Wandlung unvollständig |
| 0x4320 | Interner Steuergerätefehler Kontrollrechner reagiert nicht auf Synchro |
| 0x437F | Fehler bei erkanntem Spannungseinbruch aufgetreten |
| 0x43FF | Fehler bei erkanntem Spannungseinbruch aufgetreten |
| 0x4401 | Interner Steuergerätefehler Unzulässiger Interrupt |
| 0x4403 | Interner Steuergerätefehler RAM-Fehler im Test erkannt |
| 0x4404 | Interner Steuergerätefehler ROM-Fehler im Test erkannt |
| 0x4407 | Interner Steuergerätefehler (Rechenfehler) Hauptrechner Loop to long |
| 0x4408 | Interner Steuergerätefehler Stack Fehler |
| 0x4409 | Unterspannungsfehler bei Systemstart |
| 0x440A | Interner Steuergerätefehler Staudruck &gt; 5.5 bar Hinten |
| 0x440B | ABS-Motor hinten defekt |
| 0x440C | Interner Steuergerätefehler (Rechenfehler) Hauptrechner Loop to short |
| 0x440D | Interner Steuergerätefehler Kontrollrechner Loop to long |
| 0x440E | Interner Steuergerätefehler Analogwert Drucksensor hinten |
| 0x440F | Unzulässige Fahrzeugkodierung |
| 0x4410 | Interner Steuergerätefehler Analogwert Steuerdrucksensor hinten |
| 0x4411 | Interner Steuergerätefehler Regelventil hinten defekt |
| 0x4412 | Interner Steuergerätefehler EEPROM Version passt nicht zum Hauptrechner |
| 0x4413 | Interner Steuergerätefehler (Rechenfehler) Übertragungsfehler zwischen Rechner |
| 0x4414 | Interner Steuergerätefehler (Rechenfehler) Timeout MainLoopStart |
| 0x4415 | Interner Steuergerätefehler Hauptrechner |
| 0x4416 | Interner Steuergerätefehler EEPROM defekt |
| 0x4417 | Interner Steuergerätefehler Kontrollrechner |
| 0x4418 | Interner Steuergerätefehler (Rechenfehler) Timeout Kommunikation Rechner |
| 0x4419 | Zu geringer Druck im hinteren Radkreis |
| 0x441A | Interner Steuergerätefehler (Rechenfehler) Übertragungsfehler zwischen Rechner |
| 0x441B | Interner Steuergerätefehler Fehlerhafter Wert bei Berechnung |
| 0x441C | Interner Steuergerätefehler Fahrzeugparameter im EEPROM fehlerhaft |
| 0x441E | Zu hoher Druck im hinteren Radkreis |
| 0x441F | Interner Steuergerätefehler 2 mal AD-Wandlung unvollständig |
| 0x4420 | Interner Steuergerätefehler Kontrollrechner reagiert nicht auf Synchro |
| 0x447F | Fehler bei erkanntem Spannungseinbruch aufgetreten |
| 0x45F4 | zu viele Tracevariablen |
| 0x45F5 | Bremslicht defekt |
| 0x45F6 | Bremsflüssigkeitsstand zu tief |
| 0x45F7 | Rücklicht defekt |
| 0x45F9 | ABS-Taster unzulässig |
| 0x45FA | Spannungsversorgung Warnlampenrelais defekt |
| 0x45FB | Warnlampendefekt |
| 0x45FC | Interner Steuergerätefehler Kontrollrechner kann Warnlampe nicht bedienen |
| 0x45FD | Bremsschalter Hinten defekt |
| 0x45FE | Bremsschalter Vorn defekt |
| 0x45FF | Fehler bei erkanntem Spannungseinbruch aufgetreten |
| 0xFFFFFF | unbekannter Fehler |

<a id="table-fehlerstatus"></a>
### FEHLERSTATUS

Dimensions: 5 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | NICHT VORHANDEN |
| 0x01 | SPORADISCH |
| 0x02 | MOMEMTAN VORHANDEN |
| 0x03 | MOMEMTAN VORHANDEN UND GESPEICHERT |
| 0xFF | STATUS: UNBEKANNT |

<a id="table-fehlercodetest"></a>
### FEHLERCODETEST

Dimensions: 3 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | TEST VOLLSTAENDIG |
| 0x01 | TEST UNVOLLSTAENDIG |
| 0xFF | UNBEKANNT |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 13 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x01 | FEHLER |
| 0x02 | FEHLER: ARGUMENTE |
| 0x03 | FEHLER: AUSSERHALB BEREICH |
| 0x04 | FEHLER: ZUGRIFF VERWEIGERT |
| 0x05 | FEHLER: FORMATFEHLER DATEN (NICHT HEX) |
| 0x06 | FEHLER: PAUSENZEIT ZU GERING |
| 0x07 | FEHLER: SG BEREITS FREIGESCHALTET |
| 0x08 | OKAY: SG FREIGESCHALTET |
| 0x09 | FEHLER: FREISCHALTUNG FEHLGESCHLAGEN |
| 0x0A | FEHLER: FALSCHER KEY |
| 0x0B | FEHLER: MAXIMALE ANZAHL DER VERSUCHE ERREICHT |
| 0xFF | FEHLER: UNBEKANNT |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-kodierung"></a>
### KODIERUNG

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Test/Produktion |
| 0x01 | K 1200 LT |
| 0x03 | R 1150 GS / R 1150 GS Adventure |
| 0x04 | K 1200 RS |
| 0x09 | R 850 RT / R 1150 RT |
| 0x0A | R 1200 C |
| 0x0B | R 1200 C Montauk |
| 0x0C | R 1200 CL |
| 0x0D | R 1150 RS |
| 0x1B | R 1100 S |
| 0x24 | R 850 R / R 1150 R / R 1150 R Rockster |
| 0xFF | UNBEKANNT |

<a id="table-responsecode"></a>
### RESPONSECODE

Dimensions: 14 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | KEIN FEHLER |
| 0x10 | Fehler: 0x10 - ALLGEMEINER FEHLER |
| 0x11 | Fehler: 0x11 - SERVICE NICHT UNTERSTUETZT |
| 0x12 | Fehler: 0x12 - TEILFUNKTION NICHT UNTERSTUETZT, FORMATFEHLER |
| 0x21 | Fehler: 0x21 - BESCHAEFITGT, ANFRAGE WIEDERHOLEN |
| 0x31 | Fehler: 0x31 - ANFRAGE AUSSERHALB BEREICH |
| 0x33 | Fehler: 0x33 - ANFRAGE VERWEIGERT, SECURITY ACCESS NOTWENDIG |
| 0x35 | Fehler: 0x35 - UNGUELTIGER KEY |
| 0x80 | Fehler: 0x80 - ANFRAGE NICHT UNTERSTÜTZT |
| 0xFA | Fehler: 0xFA - ZU VIELE TRACE RECORDS |
| 0xFB | Fehler: 0xFB - INTERNER FEHLER |
| 0xFC | Fehler: 0xFC - KR FEHLER |
| 0xFD | Fehler: 0xFD - FALSCHER MODUS |
| 0xFF | UNBEKANNT |

<a id="table-systemnameorenginetype"></a>
### SYSTEMNAMEORENGINETYPE

Dimensions: 18 rows × 3 columns

| WERT | VK_BEZEICHNUNG | EW_BEZEICHNUNG |
| --- | --- | --- |
| 0x6B72 | K1200RS | K589RS |
| 0x6B6C | K1200LT | K589LT |
| 0x4B40 |  | K40 |
| 0x4B41 | K 1200RS | K41 |
| 0x7273 | R1100S | R259S |
| 0x7263 | R850/1200C | R259C |
| 0x5221 | R1150GS | R21 |
| 0x5222 | R850/1150RT | R22 |
| 0x5228 | R850/1150R | R28 |
| 0x4301 | C1 | C1 |
| 0x5213 | F650GS/GD | R13 |
| 0x4B14 | F650CS | K14 |
| 0x4B30 |  | K30 |
| 0x4B43 |  | K43 |
| 0x4B44 |  | K44 |
| 0x7201 | R1150RS | R259 RS MÜ |
| 0x4B25 |  | K25 |
| 0xFFFF | UNBEKANNT | UNBEKANNT |

<a id="table-warnlampe"></a>
### WARNLAMPE

Dimensions: 3 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Aus |
| 0x01 | Ein |
| 0xFF | UNBEKANNT |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 81 rows × 2 columns

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
| 0x18 | Continental Teves |
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
| 0x72 | ASIN AWCO.LTD |
| 0x73 | Shorlock |
| 0x74 | Schrader |
| 0x75 | BERU Electronics GmbH |
| 0x76 | CEL |
| 0x77 | Audio Mobil |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia Automotive GmbH |
| 0xFF | unbekannter Hersteller |
