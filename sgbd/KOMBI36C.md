# KOMBI36C.prg

- Jobs: [39](#jobs)
- Tables: [12](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | KOMBI E36C |
| ORIGIN | BMW TI-433 Dennert |
| REVISION | 2.05 |
| AUTHOR | BMW TP-422 Zender, BMW TI-433 Dennert |
| COMMENT | CAN-Kombi fuer E36/5/7 |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer Kombi 36 CAN
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Default ident job
- [AIF_GWSZ_LESEN](#job-aif-gwsz-lesen) - Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen
- [AIF_FG_NR_LESEN](#job-aif-fg-nr-lesen) - Auslesen der Fahrgestellnummer
- [AIF_SIA_DATEN_LESEN](#job-aif-sia-daten-lesen) - Anwenderinfofeld Block 3 auslesen
- [AIF_ZENTRALCODE_LESEN](#job-aif-zentralcode-lesen) - Anwenderinfofeld Block 4 auslesen
- [AIF_DATUM_FZ_LESEN](#job-aif-datum-fz-lesen) - Auslesen des Herstelldatums aus dem Anwenderinfofeld
- [VERRIEGELUNG_LESEN](#job-verriegelung-lesen) - Auslesen der Verriegelungsbits aus dem EEPROM
- [TACHO_ENDWERT_LESEN](#job-tacho-endwert-lesen) - Auslesen des Tacho-Endausschlags aus dem EEPROM
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicherinhalt aus SG lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [RAM_LESEN](#job-ram-lesen) - RAM-Speicher auslesen
- [EEPROM_LESEN](#job-eeprom-lesen) - EEPROM-Daten auslesen
- [DPRAM_LESEN](#job-dpram-lesen) - DPRAM des CAN-Controllers auslesen
- [STATUS_IO_LESEN](#job-status-io-lesen) - Eingangs- und Ausgangsstati lesen
- [STATUS_ANALOG_LESEN](#job-status-analog-lesen) - Spezielle analoge Eingaenge lesen
- [STATUS_TANKINHALT_LESEN](#job-status-tankinhalt-lesen) - Tankinhalt aus RAM lesen
- [STEUERN_ANZEIGE](#job-steuern-anzeige) - Anzeigenkomponenten steuern
- [STEUERN_LEUCHTE](#job-steuern-leuchte) - Leuchten in der Anzeigeeinheit steuern
- [STEUERN_GONG3](#job-steuern-gong3) - Ausgang Gong T3 ansteuern
- [STEUERN_SCHNARRE](#job-steuern-schnarre) - Schnarre (Relais) einschalten
- [SIA_GWSZ_RESET](#job-sia-gwsz-reset) - Ruecksetzen der Service-Intervall-Anzeige u. des GWSZ Es koennen 1 bis 4 Parameter uebergeben werden.
- [STEUERN_TACHO_A](#job-steuern-tacho-a) - TACHO_A ansteuern
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Default pruefstempel_lesen job
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [SELBSTTEST](#job-selbsttest) - SG - Selbsttest ausloesen
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - SG - Selbsttest ausloesen
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Fortsetzen der Diagnose
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [SOFTWARE_RESET](#job-software-reset) - Kombi loest selbststaendig einen Reset aus
- [STATUS_CAN_MOTORDREHZAHL_LESEN](#job-status-can-motordrehzahl-lesen) - DUAL PORT RAM des CAN-Controllers auslesen und Motordrehzahl ausgeben
- [STATUS_CAN_KUEHLMITTELTEMP_LESEN](#job-status-can-kuehlmitteltemp-lesen) - DUAL PORT RAM des CAN-Controllers auslesen Kuehlmitteltemperatur u. Status der Kuehlmitteltemperaturleuchte ausgeben
- [STATUS_CAN_GETRIEBEINFO_LESEN](#job-status-can-getriebeinfo-lesen) - DUAL PORT RAM des CAN-Controllers auslesen Zielgang, Positionswaehlhebelanzeige, Programminformations- anzeige und Stoeranzeige ausgeben
- [STATUS_CAN_EINSPRITZMENGE_LESEN](#job-status-can-einspritzmenge-lesen) - DUAL PORT RAM des CAN-Controllers auslesen und Einspritzmenge ausgeben
- [STATUS_CAN_SIGNALE_LESEN](#job-status-can-signale-lesen) - DUAL PORT RAM des CAN-Controllers auslesen und Kontrollsignale ausgeben
- [SIA_ZEIT_MAX_USA](#job-sia-zeit-max-usa) - Umkodierung der SIA
- [SERVICE_STATUS](#job-service-status)

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job fuer Kombi 36 CAN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

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

<a id="job-ident"></a>
### IDENT

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_COD_INDEX | int | Codierindex |
| ID_DIAG_INDEX | int | Diagnoseindex |
| ID_BUS_INDEX | int | Busindex |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferantennummer |
| ID_LIEF_TEXT | string | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| ID_CAN_INDEX | int | CAN-Index |
| ID_AENDERUNGSINDEX | int | Aenderungsindex |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-aif-gwsz-lesen"></a>
### AIF_GWSZ_LESEN

Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| STAT_GWSZ_WERT | long | Gesamtwegstreckenzaehler |
| STAT_GWSZ_EINH | string | Einheit des GWSZ [km] |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-aif-fg-nr-lesen"></a>
### AIF_FG_NR_LESEN

Auslesen der Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| AIF_FG_NR | string | Fahrgestellnummer |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-aif-sia-daten-lesen"></a>
### AIF_SIA_DATEN_LESEN

Anwenderinfofeld Block 3 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| STAT_CAN_FUNKTION_EIN | int | 0 = keine CAN-Funktionalitaet,d.h. konventionelles Kombi, 1 = CAN-Kombi |
| STAT_MOTORTYP_NR | int | 0 = Benzinmotor, 1 = Dieselmotor |
| STAT_MOTORTYP_TEXT | string | "Benzinmotor", "Dieselmotor" |
| STAT_GETRIEBE_NR | int | 0 = Schaltgetriebe, 1 = Automatikgetriebe, (siehe table Getriebetypen) |
| STAT_GETRIEBE_TEXT | string | "Schaltgetriebe", "Automatikgetriebe",siehe table Getriebetypen |
| STAT_ZEITINSPEKTION_AUS | int | keine Zeitinspektion = 1 |
| STAT_VORGEZOGENE_ZEITINSPEKTION_AUS | int | keine vorgezogene Zeitinspektion = 1 |
| STAT_INSPEKTIONSGRENZE_WERT | unsigned int | Inspektionsgrenze [Liter] |
| STAT_INSPEKTIONSGRENZE_EINH | string | Einheit "Liter" |
| STAT_ZEITGRENZE_WERT | unsigned int | Zeitgrenze [Tage] |
| STAT_ZEITGRENZE_EINH | string | Einheit "Tage" |
| STAT_KRAFTSTOFFMENGE_WERT | unsigned int | verbrauchte SI-Kraftstoffmenge [Liter] |
| STAT_KRAFTSTOFFMENGE_EINH | string | Einheit "Liter" |
| STAT_ZEIT_INSP_ZAEHLER_WERT | unsigned int | Zeitinspektionszaehler [Tage] |
| STAT_ZEIT_INSP_ZAEHLER_EINH | string | Einheit "Tage" |
| STAT_SERVICE_ART | int | Gibt die letzte durchgefuehrte Serviceart an 0 = Inspektion, 1 = Oelservice |
| STAT_SERVICE_TEXT | string | "Inspektion", "Oelservice" |
| STAT_WEGINSPEKTIONSINTERVALL_WERT | int | Weginspektionsintervall [256 km] |
| STAT_WEGINSPEKTIONSINTERVALL_EINH | string | Einheit "256 km" |
| STAT_ZEITINSPEKTIONSINTERVALL_WERT | unsigned int | Zeitinspektionsintervall [Tage] |
| STAT_ZEITINSPEKTIONSINTERVALL_EINH | string | Einheit "Tage" |
| STAT_DREHZAHLGRENZE_WERT | int | Drehzahlgrenze [1/32 Upm] |
| STAT_DREHZAHLGRENZE_EINH | string | Einheit "1/32 Upm" |
| STAT_ANZAHL_SERVICE_WERT | int | Anzahl Service pro Intervall |
| STAT_SIA_WEGSTRECKE_WERT | unsigned int | Sia Wegstrecke aus RAM [km] |
| STAT_SIA_WEGSTRECKE_EINH | string | Einheit "km" |
| STAT_SIA_TAGE_WERT | unsigned int | Sia Tage aus RAM [Tage] |
| STAT_SIA_TAGE_EINH | string | Einheit "Tage" |
| STAT_SIA_WEGSTRECKE_SERVICE_WERT | unsigned int | Sia Wegstrecke bei letztem Service aus RAM [km] |
| STAT_SIA_WEGSTRECKE_SERVICE_EINH | string | Einheit "Tage" |
| STAT_ANZAHL_OELWECHSEL_WERT | int | Anzahl erfolgter Oelwechsel aus RAM |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-aif-zentralcode-lesen"></a>
### AIF_ZENTRALCODE_LESEN

Anwenderinfofeld Block 4 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| GM | string | C1 Zifferncode fuer Grundmerkmal |
| SA | string | C2 Zifferncode fuer Sonderausstattung |
| VM | string | C3 Zifferncode fuer Versionsmerkmal |
| STAT_ZENTRALCODE_ANLIEFERCODIERUNG | int | True falls der Zentralcode der Anliefercodierung entspricht |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-aif-datum-fz-lesen"></a>
### AIF_DATUM_FZ_LESEN

Auslesen des Herstelldatums aus dem Anwenderinfofeld

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| DATUM_FZ | string | Herstelldatum des FZ |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-verriegelung-lesen"></a>
### VERRIEGELUNG_LESEN

Auslesen der Verriegelungsbits aus dem EEPROM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| STAT_VERRIEGELUNG_EIN | int | 1 wenn EEPROM schreibgeschuetzt, 0 wenn EEPROM nicht verriegelt |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-tacho-endwert-lesen"></a>
### TACHO_ENDWERT_LESEN

Auslesen des Tacho-Endausschlags aus dem EEPROM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| TACHO_ENDWERT | int | gibt den Anzeigeendwert des Tachoinstruments in [km/h] aus |
| TACHO_ENDWERT_TEXT | string | gibt den Anzeigeendwert des Tachoinstruments als String aus |
| TACHO_ENDWERT_EINH | string | Einheit des Tacho-Endwerts: [km/h] |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicherinhalt aus SG lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| F_ORT_NR | int | Index fuer Fehlerort (z.B. 0x8B, 0x83) |
| F_ORT_TEXT | string | Text zum Fehlerort (z.B. Gong T3, Tacho A) |
| F_HFK | int | Fehlerhaeufigkeit (vgl. obiger Infotext) |
| F_ART_ANZ | int | Anzahl der Fehlerarten (Unterbr.,Schluss nach Plus o. Masse, ungueltiger Arbeitsbereich, Fehler momentan o. sporadisch) |
| F_ART1_NR | int | Nr. der Fehlerart (z.B. "6" fuer Fehler sporadisch vorhanden) |
| F_ART1_TEXT | string | Fehlerarttext |
| F_ART2_NR | int | Nr. der Fehlerart (z.B. "6" fuer Fehler sporadisch vorhanden) |
| F_ART2_TEXT | string | Fehlerarttext |
| F_ART3_NR | int | Nr. der Fehlerart (z.B. "6" fuer Fehler sporadisch vorhanden) |
| F_ART3_TEXT | string | Fehlerarttext |
| F_ART4_NR | int | Nr. der Fehlerart (z.B. "6" fuer Fehler sporadisch vorhanden) |
| F_ART4_TEXT | string | Fehlerarttext |
| F_ART5_NR | int | Nr. der Fehlerart (z.B. "6" fuer Fehler sporadisch vorhanden) |
| F_ART5_TEXT | string | Fehlerarttext |
| F_ART6_NR | int | Nr. der Fehlerart (z.B. "6" fuer Fehler sporadisch vorhanden) |
| F_ART6_TEXT | string | Fehlerarttext |
| F_UW_ANZ | int | Umweltbedingung, immer = 0 |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |

<a id="job-ram-lesen"></a>
### RAM_LESEN

RAM-Speicher auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RAM_TYPE | string | "INTERN" oder "EXTERN" |
| ADRESSE | string | Hexwert (0x000-0xFFF) der Adresse ,ab der das Ram gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der auszulesenden Bytes (max. 32 !) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| DATEN | binary | Datenfeld |

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

EEPROM-Daten auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x00-0xBF) der Wortadresse ,ab der das EEPROM gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der 2-Byte-Worte (max. 16 Worte = 32 Bytes), die ausgelesen werden koennen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| DATEN | binary | Datenfeld |

<a id="job-dpram-lesen"></a>
### DPRAM_LESEN

DPRAM des CAN-Controllers auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x80-0xDF) der Adresse ,ab der das DPRAM gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der Bytes (max. 32 !) die ausgelesen werden sollen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| DATEN | binary | Datenfeld |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Eingangs- und Ausgangsstati lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| STAT_TUERKONTAKT_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_ZUENDSCHLOSS_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_GURTKONTAKT_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_GONGT3_IN_EIN | int | 1, wenn "TRUE" , 0, wenn "FALSE" |
| STAT_GONGT3_OUT_EIN | int | 1, wenn "TRUE" , 0, wenn "FALSE" |
| STAT_SUMMER_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KLR_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KL15_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_EGS_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KOMBITASTE_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_SIA_RESET_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-status-analog-lesen"></a>
### STATUS_ANALOG_LESEN

Spezielle analoge Eingaenge lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| STAT_5V_WERT | int | AD - Kanal 0, 5V fixe Spannung |
| STAT_5V_EINH | string | Einheit [ADC-WERT] |
| STAT_HEBELGEBER1_WERT | int | AD - Kanal 1, Wert des 1. Hebelgebers |
| STAT_HEBELGEBER1_EINH | string | Einheit [ADC-WERT] |
| STAT_FOTOTRANSISTOR_WERT | int | AD - Kanal 3, Wert des Fototransistors |
| STAT_FOTOTRANSISTOR_EINH | string | Einheit [ADC-WERT] |
| STAT_KL58G_WERT | int |  |
| STAT_KL58G_EINH | string | Einheit [ADC-WERT] |
| STAT_KUEHLMITTELTEMP_WERT | int | AD - Kanal 5, Wert der Kuehlmittel`temperatur |
| STAT_KUEHLMITTELTEMP_EINH | string | Einheit [ADC-WERT] |
| STAT_BREMSVERSCHLEISS_WERT | int | Wert AD - Kanal 6, Wert des Bremsbelagverschleisses |
| STAT_BREMSVERSCHLEISS_EINH | string | Einheit [ADC-WERT] |
| STAT_GESCHWINDIGKEIT_WERT | long | Wert des Wegeingangs, Wert der Geschwindigkeit |
| STAT_GESCHWINDIGKEIT_EINH | string | Einheit [km/h] |
| STAT_DREHZAHL_WERT | long | Wert des Drehzahleingangs als string |
| STAT_DREHZAHL_EINH | string | Einheit [U/min] |
| STAT_DREHZAHL_CAN_WERT | long | Wert des Drehzahleingangs als string |
| STAT_DREHZAHL_CAN_EINH | string | Einheit [U/min] |
| STAT_VERBRAUCH_CAN_WERT | long | Wert des Verbrauchssignal 1 |
| STAT_VERBRAUCH_CAN_EINH | string | Einheit [ms] |
| STAT_KUEHLMITTELTEMP_CAN_WERT | int | AD - Kanal 5, Wert der Kuehlmittel`temperatur |
| STAT_KUEHLMITTELTEMP_CAN_EINH | string | Einheit [ADC-WERT] |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-status-tankinhalt-lesen"></a>
### STATUS_TANKINHALT_LESEN

Tankinhalt aus RAM lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| STAT_TANKINHALT_WERT | real | Tankinhalt gesamt in Liter |
| STAT_TANKINHALT_EINH | string | Einheit Tankinhalt gesamt: "Liter" |
| STAT_TANKINHALT_ANZEIGE_WERT | real | Tankinhalt gesamt in Liter |
| STAT_TANKINHALT_ANZEIGE_EINH | string | Einheit Tankinhalt gesamt: "Liter" |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-steuern-anzeige"></a>
### STEUERN_ANZEIGE

Anzeigenkomponenten steuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | Zu steuernde Komponente, siehe table Komponenten moegliche Komponenten: TACHO, DREHZAHL, TANKINHALT, KUEHLMITTELTEMPERATUR, ALLE |
| WERT | int | Winkelgrade im Bereich von (10-90) Grad, Mit Spruengen von mehr als 90 Grad sollten die Messwerke nicht beaufschlagt werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-steuern-leuchte"></a>
### STEUERN_LEUCHTE

Leuchten in der Anzeigeeinheit steuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bitbelegung des 1. Datenbytes: Bit 0: SIA-Beleuchtung Bit 1: Tankreserve Bit 2: Tempomat Bit 3: Vorgluehen/Diesel-Diagnose Bit 4: EGS Bit 5: Check-Engine Bit 6: frei Bit 7: frei |
| BYTE2 | int | Bitbelegung des 2. Datenbytes: Bit 0: Kuehlmitteluebertemperatur Bit 1: Feststellbremse Bit 2: Bremsfluessigkeitsniveau Bit 3: ASC Kontrolleuchte Bit 4: BVA Kontrolleuchte Bit 5: Oelstandsniveau Bit 6: Gurtwarnung Bit 7: frei |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-steuern-gong3"></a>
### STEUERN_GONG3

Ausgang Gong T3 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-steuern-schnarre"></a>
### STEUERN_SCHNARRE

Schnarre (Relais) einschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-sia-gwsz-reset"></a>
### SIA_GWSZ_RESET

Ruecksetzen der Service-Intervall-Anzeige u. des GWSZ Es koennen 1 bis 4 Parameter uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | Oel_Reset, Inspektion_Reset, Zeit_Reset oder GWSZ_Reset |
| ARG2 | string | Oel_Reset, Inspektion_Reset, Zeit_Reset oder GWSZ_Reset |
| ARG3 | string | Oel_Reset, Inspektion_Reset, Zeit_Reset oder GWSZ_Reset |
| ARG4 | string | Oel_Reset, Inspektion_Reset, Zeit_Reset oder GWSZ_Reset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| TELEGRAMM | binary | Telegram an SG |

<a id="job-steuern-tacho-a"></a>
### STEUERN_TACHO_A

TACHO_A ansteuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | int | Geschwindigkeit in km/h, Wertebereich (3 bis 250) km/h |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Default pruefstempel_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| BYTE1 | int | Pruefstempel Datenbyte1 |
| BYTE2 | int | Pruefstempel Datenbyte2 |
| BYTE3 | int | Pruefstempel Datenbyte3 |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden (0x00-0xFF) |
| BYTE2 | int | kann beliebig verwendet werden (0x00-0xFF) |
| BYTE3 | int | kann beliebig verwendet werden (0x00-0xFF) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-selbsttest"></a>
### SELBSTTEST

SG - Selbsttest ausloesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

SG - Selbsttest ausloesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Fortsetzen der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |

<a id="job-software-reset"></a>
### SOFTWARE_RESET

Kombi loest selbststaendig einen Reset aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |

<a id="job-status-can-motordrehzahl-lesen"></a>
### STATUS_CAN_MOTORDREHZAHL_LESEN

DUAL PORT RAM des CAN-Controllers auslesen und Motordrehzahl ausgeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| STAT_MOTORDREHZAHL_WERT | long | Ausgabe der Motordrehzahl in U/min |
| STAT_MOTORDREHZAHL_EINH | string | Einheit [U/min] |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-status-can-kuehlmitteltemp-lesen"></a>
### STATUS_CAN_KUEHLMITTELTEMP_LESEN

DUAL PORT RAM des CAN-Controllers auslesen Kuehlmitteltemperatur u. Status der Kuehlmitteltemperaturleuchte ausgeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| STAT_KUEHLMITTELTEMP_WERT | long | Ausgabe der Kuehlmitteltemperatur in [Grad Celsius] |
| STAT_KUEHLMITTELTEMP_EINH | string | Einheit [Grad Celsius] |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-status-can-getriebeinfo-lesen"></a>
### STATUS_CAN_GETRIEBEINFO_LESEN

DUAL PORT RAM des CAN-Controllers auslesen Zielgang, Positionswaehlhebelanzeige, Programminformations- anzeige und Stoeranzeige ausgeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| STAT_GANG_INFO_WERT | int | gibt an in welchem Gang sich zur Zeit das Getriebe befindet |
| STAT_GANG_INFO_TEXT | string | gibt an in welchem Gang sich zur Zeit das Getriebe befindet |
| STAT_GANG_WHL_ANZ_WERT | int | gibt Waehlhebelposition an: 1,2,3,4,D,N,R,P,5,6,Zwischenstellung |
| STAT_GANG_WHL_ANZ_TEXT | string | gibt Waehlhebelposition an: 1,2,3,4,D,N,R,P,5,6,Zwischenstellung |
| STAT_PRG_INF_ANZ_WERT | int | gibt Programminfo aus: E,M,S,W,A,Anzeige aus |
| STAT_PRG_INF_ANZ_TEXT | string | gibt Programminfo aus: E,M,S,W,A,Anzeige aus |
| STAT_L_GETR_STEUERUNG_WERT | int | gibt Zustand der Getriebesteuerung an: Getriebenotprogramm ein |
| STAT_L_GETR_STEUERUNG_TEXT | string | gibt Zustand der Getriebesteuerung an: Getriebenotprogramm ein |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-status-can-einspritzmenge-lesen"></a>
### STATUS_CAN_EINSPRITZMENGE_LESEN

DUAL PORT RAM des CAN-Controllers auslesen und Einspritzmenge ausgeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| STAT_EINSPRITZMENGE_WERT | long | Ausgabe der Einspritzmenge in [ul] |
| STAT_EINSPRITZMENGE_EINH | string | Einheit [ul] |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-status-can-signale-lesen"></a>
### STATUS_CAN_SIGNALE_LESEN

DUAL PORT RAM des CAN-Controllers auslesen und Kontrollsignale ausgeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| TELEGRAMM1_ASC1 | binary | Telegramm an SG |
| SG_ANTWORT1_ASC1 | binary | Antworttelegramm vom SG |
| STAT_LAMPE_EBV_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_LAMPE_ASC_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| TELEGRAMM2_DME4_DDE4 | binary | Telegramm an SG |
| SG_ANTWORT2_DME4_DDE4 | binary | Antworttelegramm vom SG |
| STAT_VORGLUEHLAMPE_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_LAMPE_CHECK_ENGINE_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_LAMPE_TEMPOMAT_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_DDE_DIAGNOSELAMPE_EML_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_LAMPE_UEBERTEMPERATUR_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| TELEGRAMM3_INSTR2 | binary | Telegramm an SG |
| SG_ANTWORT3_INSTR2 | binary | Antworttelegramm vom SG |
| STAT_KILOMETERSTAND_WERT | long | gesamte Fahrleistung des Fahrzeugs in [km] |
| STAT_KILOMETERSTAND_EINH | string | [km] |
| TELEGRAMM4_INSTR3 | binary | Telegramm an SG |
| SG_ANTWORT4_INSTR3 | binary | Antworttelegramm vom SG |
| STAT_S_KLIMAKOMPRESSOR_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_S_KLIMABEREITSCHAFT_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |

<a id="job-sia-zeit-max-usa"></a>
### SIA_ZEIT_MAX_USA

Umkodierung der SIA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |

<a id="job-service-status"></a>
### SERVICE_STATUS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| ANZEIGE_VORGABE | string | Anzeigeinfo fuer Zeitinspektion |
| AKTUELLER_STAND | int | Aktueller Stand (Eiheit: Tage) |
| SUMME_TAGE | int | Tagessummenstand |
| KRAFTSTOFFMENGE | int | Verbrauchte Kraftstoffmenge (Einheit: Liter) |
| SERVICE | string | Naechste Serviceart |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (7 × 2)
- [LIEFERANTEN](#table-lieferanten) (30 × 2)
- [GETRIEBETYPEN](#table-getriebetypen) (3 × 2)
- [GANGINFO](#table-ganginfo) (9 × 2)
- [WAEHLHEBELINFO](#table-waehlhebelinfo) (12 × 2)
- [PROGRAMMINFO](#table-programminfo) (7 × 2)
- [FORTTEXTE](#table-forttexte) (19 × 2)
- [FARTTEXTE](#table-farttexte) (8 × 2)
- [KOMPONENTEN](#table-komponenten) (16 × 2)
- [SIARESET](#table-siareset) (5 × 2)
- [ZEITINSPINFO](#table-zeitinspinfo) (4 × 2)
- [SERVICEINFO](#table-serviceinfo) (3 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 7 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 30 rows × 2 columns

| LIEF_NR | LIEF_NAME |
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
| 0xFF | unbekannter Hersteller |

<a id="table-getriebetypen"></a>
### GETRIEBETYPEN

Dimensions: 3 rows × 2 columns

| GETRIEBEART | GETRIEBETEXT |
| --- | --- |
| 0x00 | Schaltgetriebe |
| 0x01 | Automatikgetriebe |
| 0xFF | unbekannte Getriebeart |

<a id="table-ganginfo"></a>
### GANGINFO

Dimensions: 9 rows × 2 columns

| GANGINFO | GANGTEXT |
| --- | --- |
| 0x00 | N oder P |
| 0x01 | 1. Gang |
| 0x02 | 2. Gang |
| 0x03 | 3. Gang |
| 0x04 | 4. Gang |
| 0x05 | 5. Gang |
| 0x06 | 6. Gang |
| 0x07 | Rueckwaertsgang |
| 0xFF | unbekannte Getriebeinfo |

<a id="table-waehlhebelinfo"></a>
### WAEHLHEBELINFO

Dimensions: 12 rows × 2 columns

| WAEHLHEBELINFO | WAEHLHEBELTEXT |
| --- | --- |
| 0x00 | Zwischenstellung |
| 0x01 | 1 |
| 0x02 | 2 |
| 0x03 | 3 |
| 0x04 | 4 |
| 0x05 | D |
| 0x06 | N |
| 0x07 | R |
| 0x08 | P |
| 0x09 | 5 |
| 0x0A | 6 |
| 0xFF | unbekannte Waehlhebelinfo |

<a id="table-programminfo"></a>
### PROGRAMMINFO

Dimensions: 7 rows × 2 columns

| PROGRAMMINFO | PROGRAMMTEXT |
| --- | --- |
| 0x00 | E |
| 0x01 | M |
| 0x02 | S |
| 0x03 | W |
| 0x04 | A |
| 0x05 | Anzeige aus |
| 0xFF | unbekannte Programminfo |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 19 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xC1 | Signal TWEG+ (Tacho) |
| 0xC3 | Signal TD (Drehzahl) |
| 0xD3 | Kuehlmitteltemperatur |
| 0xC7 | Tank-Hebelgeber_1 |
| 0x8F | Ueberspannung (U&gt;16V) |
| 0x8C | Klemme R |
| 0xCF | SIA-Reset |
| 0x8B | Gong_T3 |
| 0x3E | Messwerktreiber |
| 0x3F | Latch-Up Messwerktreiber |
| 0x83 | Tacho A |
| 0xF0 | CAN BUS OFF |
| 0xF4 | keine CAN ID |
| 0xF5 | keine CAN ID ASC1 |
| 0xF6 | keine CAN ID DME1 |
| 0xF7 | keine CAN ID DME2 |
| 0xF8 | keine CAN ID DME4 |
| 0xFB | keine CAN ID EGS1 |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 8 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen U-Batt |
| 0x02 | Kurzschluss gegen Masse |
| 0x03 | Leitungsunterbrechung |
| 0x04 | ungueltiger Arbeitsbereich |
| 0x05 | Fehler momentan vorhanden |
| 0x06 | sporadischer Fehler |
| 0xFF | unbekannte Fehlerart |

<a id="table-komponenten"></a>
### KOMPONENTEN

Dimensions: 16 rows × 2 columns

| ORT | BYTE |
| --- | --- |
| TACHO | 0x0A |
| Tacho | 0x0A |
| tacho | 0x0A |
| DREHZAHL | 0x0B |
| Drehzahl | 0x0B |
| drehzahl | 0x0B |
| TANKINHALT | 0x0C |
| Tankinhalt | 0x0C |
| tankinhalt | 0x0C |
| KUEHLMITTELTEMPERATUR | 0x0D |
| Kuehlmitteltemperatur | 0x0D |
| kuehlmitteltemperatur | 0x0D |
| ALLE | 0x20 |
| Alle | 0x20 |
| alle | 0x20 |
| FEHLER | 0xFF |

<a id="table-siareset"></a>
### SIARESET

Dimensions: 5 rows × 2 columns

| SELECTOR | RESET |
| --- | --- |
| OEL_RESET | 0x01 |
| INSPEKTION_RESET | 0x02 |
| ZEIT_RESET | 0x04 |
| GWSZ_RESET | 0x08 |
| FEHLER | 0x00 |

<a id="table-zeitinspinfo"></a>
### ZEITINSPINFO

Dimensions: 4 rows × 2 columns

| ZEITINFO | ZEITTEXT |
| --- | --- |
| 0x00 | Vorgezogene Zeitinspektion durchfuehren |
| 0x01 | Vorgezogene Zeitinspektion nicht durchfuehren |
| 0x02 | Keine Zeitinspektion durchfuehren |
| 0xFF | Unbekannte Anzeigevorgabe |

<a id="table-serviceinfo"></a>
### SERVICEINFO

Dimensions: 3 rows × 2 columns

| SINFO | STEXT |
| --- | --- |
| 0x00 | Oelservice |
| 0x01 | Inspektion |
| 0xFF | Unbekannte Serviceinfo |
