# IHKR36.prg

- Jobs: [13](#jobs)
- Tables: [1](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Integrierte Heiz- Klimaregelung E36 |
| ORIGIN | BMW ET-421 Drexel |
| REVISION | 1.05 |
| AUTHOR | BMW ET-421 Drexel |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Kommunikationsparameter fuer IHKR E36
- [IDENT](#job-ident) - Identifikation
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers
- [STATUS_DIGITAL](#job-status-digital) - Status lesen Digital Ein- Ausgaenge 
- [STATUS_ANALOG](#job-status-analog) - Status lesen Analog Ein- Ausgaenge 
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern der digitalen Ausgaenge
- [STEUERN_MOTOR](#job-steuern-motor) - Ansteuern der Schrittmotoren
- [STEUERN_VENTIL](#job-steuern-ventil) - Ansteuern der Wasserventile

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

Kommunikationsparameter fuer IHKR E36

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Identifikation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_GEN_NR | int | Generationsnummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_SW_NR | int | Softwarenummer |
| ID_PP_NR | int | Pruefplannummer |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| CODE | string | 4 Codierbytes in Hex |
| FAHRZEUGTYP | string | 'E34' 'E32' 'E31' 'E36' 'unbekannter Code' |
| LAENDERVARIANTE | string | 'ECE/US' 'Nordland' 'unbekannter Code' |
| AUSGANGSPEGEL_AC | string | 'DME-AC HIGH-aktiv' 'DME-AC LOW-aktiv' |
| AUSGANGSPEGEL_KO | string | 'DME-KO HIGH-aktiv' 'DME-KO LOW-aktiv' |
| ZYLINDERZAHL | string | '4-Zylinder' '6-Zylinder' '8-Zylinder' '12-Zylinder' |
| MOTORVARIANTE | string | 'Benzinmotor' 'Dieselmotor' 'Wasserstoffmotor' 'Elektromotor' 'unbekannter Code' |
| LENKUNG | string | 'Linkslenker' 'Rechtslenker' |
| AUC | string | 'ohne' 'digital' 'analog' 'unbekannter Code' |
| K_ZAHL | int |  |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_ART2_NR | int |  |
| F_ART2_TEXT | string |  |
| F_ART3_NR | int |  |
| F_ART3_TEXT | string |  |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int |  |
| ANZAHL | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Datenfeld |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status lesen Digital Ein- Ausgaenge 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TASTER_KLIMA_EIN | int |  |
| STAT_TASTER_UMLUFT_EIN | int |  |
| STAT_TASTER_HHS_EIN | int |  |
| STAT_LED_KLIMA_EIN | int |  |
| STAT_LED_UMLUFT_EIN | int |  |
| STAT_LED_HHS_EIN | int |  |
| STAT_RELAIS_HHS_EIN | int |  |
| STAT_KLAPPENSCHALTER_EIN | int |  |
| STAT_KLEMME_50_EIN | int |  |
| STAT_KLEMME_61_EIN | int |  |
| STAT_DME_AC_EIN | int |  |
| STAT_DME_KO_EIN | int |  |
| STAT_STANDLUEFTEN_EIN | int |  |
| STAT_STANDHEIZEN_EIN | int |  |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Status lesen Analog Ein- Ausgaenge 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_GEBLAESE | long | -30..190 [%] |
| STAT_GEBLAESE_TEXT | string |  |
| STAT_KLEMME_30 | long | 0.74..19.38 [Volt] |
| STAT_SCHICHTUNG | long | -157..324 [%] |
| STAT_SCHICHTUNG_TEXT | string |  |
| STAT_TAUSCHER_R | long | 0..90 [Grad Celsius] |
| STAT_TAUSCHER_L | long | 0..90 [Grad Celsius] |
| STAT_VERDAMPFER | long | -4.5..25.6 [Grad Celsius] |
| STAT_INNENTEMP | long | 10.0..40.0 [Grad Celsius] |
| STAT_AUSSENTEMP | long | -40.0..40.0 [Grad Celsius] |
| STAT_SOLL_R | long | 11.50..34.01 [Grad Celsius] |
| STAT_SOLL_L | long | 11.50..34.01 [Grad Celsius] |
| STAT_TACHO | long | 0..255 [km/h] |
| STAT_DREHZAHL | long | 0..3800 [1/min] |
| STAT_WV_R | long | 0..3600 [ms] |
| STAT_WV_L | long | 0..3600 [ms] |
| STAT_MOTOR_SCH | long | 0..100 [%] |
| STAT_MOTOR_UML | long | 0..100 [%] |
| STAT_MOTOR_FRI | long | 0..100 [%] |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern der digitalen Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LED_KLIMA | string |  |
| LED_UMLUFT | string |  |
| LED_HHS | string |  |
| RELAIS_HHS | string |  |
| DME_AC | string |  |
| DME_KO | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-motor"></a>
### STEUERN_MOTOR

Ansteuern der Schrittmotoren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FRISCHLUFT | int |  |
| UMLUFT | int |  |
| SCHICHTUNG | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-ventil"></a>
### STEUERN_VENTIL

Ansteuern der Wasserventile

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LINKS | int |  |
| RECHTS | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (22 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 22 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Geblaesepotentiometer |
| 0x02 | Schichtungspotentiometer |
| 0x03 | Waermetauscherfuehler rechts |
| 0x04 | Waermetauscherfuehler links |
| 0x05 | Verdampferfuehler |
| 0x06 | Innenraumtemperaturfuehler |
| 0x07 | Aussentemperaturfuehler |
| 0x08 | Sollwertsteller rechts |
| 0x09 | Sollwertsteller links |
| 0x0D | Standheizung / Standlueftung |
| 0x13 | Anlasser ( Klemme 50 ) |
| 0x15 | AUC |
| 0x19 | Schichtungsklappenmotor |
| 0x1A | Umluftklappenmotor |
| 0x1B | Frischluftklappenmotor |
| 0x1C | Wasserventil rechts |
| 0x1D | Wasserventil links |
| 0x20 | Innenfuehlergeblaese |
| 0x23 | DME / EPC |
| 0x24 | Heckscheibenheizung |
| 0x25 | Magnetkupplung |
| 0xFF | unbekannter Fehlerort |
