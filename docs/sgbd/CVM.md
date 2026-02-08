# CVM.prg

- Jobs: [17](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Cabrio-Verdeck-Modul E36 |
| ORIGIN | BMW TP-422 Teepe |
| REVISION | 2.01 |
| AUTHOR | BMW TP-422 Teepe |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [IDENT](#job-ident) - Auslesen der Identifikationsdaten
- [BMW_NR_LESEN](#job-bmw-nr-lesen) - Auslesen der BMW-Teilenummer
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [CRASH_AUSLOESEN](#job-crash-ausloesen) - Ausloesung des UERSS durch Crash-Telegramm
- [MOTOR_FAHREN](#job-motor-fahren) - Ansteuerung der Verdeckmotoren
- [TIPP_FUNKTION](#job-tipp-funktion) - Ansteuerung des Verdeckzyklus ueber Tippfunktion
- [AUSGAENGE_SCHALTEN](#job-ausgaenge-schalten) - Ansteuerung des Verdeckzyklus ueber Tippfunktion
- [REFERENZLAUF_EINSCHALTEN](#job-referenzlauf-einschalten) - Ausloesung des Recferenzlaufes
- [STATUS_LESEN](#job-status-lesen) - Ausloesung des Recferenzlaufes
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierung des SG
- [SG_SELBSTTEST](#job-sg-selbsttest) - Ausfuehren des SG-Selbsttests
- [ZAEHLERSTAENDE_LESEN](#job-zaehlerstaende-lesen) - Auslesen der Zaehlerstaende
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Speicherinhaltes
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose

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

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

<a id="job-ident"></a>
### IDENT

Auslesen der Identifikationsdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| ID_GEN_NR | int | Generationsnummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_SW_NR | int | Softwarenummer |
| ID_COD_INDEX | int | Codierindex |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |

<a id="job-bmw-nr-lesen"></a>
### BMW_NR_LESEN

Auslesen der BMW-Teilenummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| BMW_NR | string | BMW-Teilenummer |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| F_ORT_NR | int | Nr des Fehlers (entspricht dem Fehlercode) |
| F_ORT_TEXT | string | Fehlertext |
| F_ART_ANZ | int | Anzahl der Fehlerarten (immer 1) |
| F_ART1_NR | int | Textindex fuer Fehlerart 1 |
| F_ART1_TEXT | string | Text fuer Fehlerart 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen (hier immer 0) |
| F_ANZ | int | Anzahl der Fehler |
| F_HFK | int | Haeufigkeit des Einzelfehler |
| F_HEX_CODE | binary | Hex-Werte des Fehlers |
| TEL_0 | binary | Antworttelegramm 0 |
| TEL_1 | binary | Antworttelegramme auf Speicherlesen |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-crash-ausloesen"></a>
### CRASH_AUSLOESEN

Ausloesung des UERSS durch Crash-Telegramm

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STATUS_ANTWORT | string | Liefert: ANSTEUERUNG_ERFOLGT, ANSTEUERUNG_UNMOEGLICH |

<a id="job-motor-fahren"></a>
### MOTOR_FAHREN

Ansteuerung der Verdeckmotoren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MOTOR | string | anzusteuernder Motor (KLAPPE_AUF/ZU, VERDECK_AUF/ZU, UERSS_AUF/ZU, ALLE_AUS) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-tipp-funktion"></a>
### TIPP_FUNKTION

Ansteuerung des Verdeckzyklus ueber Tippfunktion

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTION | string | anzufuehrender Zyklus (VERDECK_OEFFNEN, VERDECK_SCHLIESSEN, VERDECK_HALT) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-ausgaenge-schalten"></a>
### AUSGAENGE_SCHALTEN

Ansteuerung des Verdeckzyklus ueber Tippfunktion

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTION | string | anzufuehrende Funktion(FH_AUF, FH_ZU, LAMPE_EIN, RESERVE, STOP) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-referenzlauf-einschalten"></a>
### REFERENZLAUF_EINSCHALTEN

Ausloesung des Recferenzlaufes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Ausloesung des Recferenzlaufes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_SCHALTER_VERDECK_AUF_EIN | int | Liefert: 0 oder 1 |
| STAT_SCHALTER_VERDECK_ZU_EIN | int | Liefert: 0 oder 1 |
| STAT_SCHALTER_UERSS_AUF_EIN | int | Liefert: 0 oder 1 |
| STAT_SCHALTER_UERSS_ZU_EIN | int | Liefert: 0 oder 1 |
| STAT_VERDECK_POSITION1_EIN | int | Liefert: 0 oder 1 |
| STAT_VERDECK_POSITION2_EIN | int | Liefert: 0 oder 1 |
| STAT_VERDECK_POSITION3_EIN | int | Liefert: 0 oder 1 |
| STAT_MIKROSCHALTER_WINDLAUF_ZU_EIN | int | Liefert: 0 oder 1 |
| STAT_MIKROSCHALTER_VERDECK_UEBERSTRECKT_EIN | int | Liefert: 0 oder 1 |
| STAT_MIKROSCHALTER_HARDTOP_VERBAUT_EIN | int | Liefert: 0 oder 1 |
| STAT_MIKROSCHALTER_HECKKLAPPE_GESCHLOSSEN_EIN | int | Liefert: 0 oder 1 |
| STAT_MIKROSCHALTER_CRASHAUSLOESUNG_RECHTS_EIN | int | Liefert: 0 oder 1 |
| STAT_MIKROSCHALTER_CRASHAUSLOESUNG_LINKS_EIN | int | Liefert: 0 oder 1 |
| STAT_GURTSCHLOSS_HINTEN_EIN | int | Liefert: 0 oder 1 |
| STAT_MOTOR_KLAPPE1_EIN | int | Liefert: 0 oder 1 |
| STAT_MOTOR_KLAPPE2_VERDECK1_EIN | int | Liefert: 0 oder 1 |
| STAT_MOTOR_VERDECK2_URB1_EIN | int | Liefert: 0 oder 1 |
| STAT_MOTOR_URB1_VERR1_EIN | int | Liefert: 0 oder 1 |
| STAT_MOTOR_VERR2_EIN | int | Liefert: 0 oder 1 |
| STAT_MIKROSCHALTER_ENTRIEGELT_EIN | int | Liefert: 0 oder 1, nur bei automatischem Verdeck! |
| STAT_SIGNAL_SPANNUNGSREGLER_EIN | int | Liefert: 0 oder 1 |
| STAT_AUSLOESESIGNAL_EIN | int | Liefert: 0 oder 1 |
| STAT_SENSORFEHLER_SIGNAL_EIN | int | Liefert: 0 oder 1 |
| STAT_KLEMME_15_EIN | int | Liefert: 0 oder 1 |
| STAT_KLEMME_R_EIN | int | Liefert: 0 oder 1 |
| STAT_AUSGANG_ALLE_MOTOREN_AUS | int | Liefert: 0 bis 1 |
| STAT_AUSGANG_MOTOR_VERDECKKLAPPE_OEFFNEN_EIN | int | Liefert: 0 bis 1 |
| STAT_AUSGANG_MOTOR_VERDECKKLAPPE_SCHLIESSEN_EIN | int | Liefert: 0 bis 1 |
| STAT_AUSGANG_MOTOR_VERDECK_SCHLIESSEN_EIN | int | Liefert: 0 bis 1 |
| STAT_AUSGANG_MOTOR_VERDECK_OEFFNEN_EIN | int | Liefert: 0 bis 1 |
| STAT_AUSGAENGE_0_BIS_7 | int | Liefert: 0 bis 255 |
| STAT_AUSGAENGE_8_BIS_15 | int | Liefert: 0 bis 255 |
| STAT_GESCHWINDIGKEIT_WERT | int | Liefert: 0 bis 255 |
| STAT_GESCHWINDIGKEIT_EINH | string | Liefert: "ms" |
| STAT_POSITION_VERDECKKLAPPE | string | Liefert: offen, geschlossen, auf Block, Zwischenlage |
| STAT_POSITION_UERSS | string | Liefert: ganz unten, Komfortstellung, Crashstellung |
| STAT_GESAMTSTROM_WERT | int | Liefert: 0 bis 25,5 |
| STAT_GESAMTSTROM_EINH | string | Liefert: "A" |
| _ANTWORT | binary | Liefert: Antworttelegramm 1 |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierung des SG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| COD_VERDECK_VERBAUT | int | Liefert: 0 oder 1 |
| COD_AUTO_VERDECK_VERBAUT | int | Liefert: 0 oder 1 |
| COD_2_TABELLE_AKTIV | int | Liefert: 0 oder 1, bei 1 Verdeckmotor auf Block, wenn Klappe oeffnet |
| COD_UERSS_VERBAUT | int | Liefert: 0 oder 1 |
| COD_FERNBEDIENUNG_AKTIV | int | Liefert: 0 oder 1 |
| COD_EICHLAUF_BEI_KL15_UND_SCHALTER_AKTIV | int | Liefert: 0 oder 1 |
| COD_EICHLAUF_BEI_8_BETAETIGUNG_KLAPPE_AKTIV | int | Liefert: 0 oder 1 |
| _ANTWORT | binary | Liefert: Antworttelegramm 1 |

<a id="job-sg-selbsttest"></a>
### SG_SELBSTTEST

Ausfuehren des SG-Selbsttests

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-zaehlerstaende-lesen"></a>
### ZAEHLERSTAENDE_LESEN

Auslesen der Zaehlerstaende

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| _ANTWORT | binary | Liefert: Antworttelegramm 1 |
| _ANTWORT1 | binary | Liefert: Antworttelegramm 2 |
| _ANTWORT2 | binary | Liefert: Antworttelegramm 3 |
| ZAEHLER_EINH | string | Liefert: "" |
| ZAEHLER_VERDECK_GEOEFFNET_WERT | int | Liefert: 0 bis 65535 |
| ZAEHLER_VERDECK_GESCHLOSSEN_WERT | int | Liefert: 0 bis 65535 |
| ZAEHLER_UERSS_OBEN_WERT | int | Liefert: 0 bis 65535 |
| ZAEHLER_UERSS_UNTEN_WERT | int | Liefert: 0 bis 65535 |
| ZAEHLER_SENSORAUSLOESUNGEN_UERSS_WERT | int | Liefert: 0 bis 255 |
| ZAEHLER_SENSORAUSLOESUNGEN_UERSS_SEIT_LETZTER_DIAG_AUSLOESUNG_WERT | int | Liefert: 0 bis 255 |
| ZAEHLER_POWER_UP_WERT | int | Liefert: 0 bis 255 |
| ZAEHLER_RESET_PROZESSOR_WERT | int | Liefert: 0 bis 255 |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Auslesen des Speicherinhaltes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZAHL | int | 1 bis 24 |
| HIGH | int | 0 = RAM, 1 = ROM |
| LOW | int | range = 0x90 bis 0xCF bei RAM und 0x01 bis 0xFF bei ROM |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| ANZAHL_BYTES | int | 1 bis 24 |
| START_ADRESSE_HIGH_BYTE | int | 0 = RAM, 1 = ROM |
| START_ADRESSE_LOW_BYTE | int | range = 0x90 bis 0xCF bei RAM und 0x01 bis 0xFF bei ROM |
| DATEN | binary | Hexdump des gewuenschten Speicherbereiches |
| _ANTWORT | binary | Antworttelegramm |
| _SENDEN | binary | Sendetelegramm |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (36 × 3)
- [STEUERN](#table-steuern) (18 × 3)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 36 rows × 3 columns

| HILFE | ORT | ORTTEXT |
| --- | --- | --- |
| 0x01 | 0x01 | Klappenmotor 1 |
| 0x02 | 0x02 | Klappenmotor 2 oder Verdeckmotor 1 |
| 0x03 | 0x12 | Verdeckmotor 2 oder Verriegelungsmotor 1 |
| 0x04 | 0x03 | Verdeckmotor 2 |
| 0x05 | 0x13 | Verriegelungsmotor 2 |
| 0x06 | 0x04 | Mikroschalter Verdeckklappe |
| 0x07 | 0x05 | Mikroschalter Position 1 oder 2 |
| 0x08 | 0x06 | Mikroschalter Position 1 oder 3 |
| 0x00 | 0x07 | Mikroschalter Position 2 |
| 0x10 | 0x08 | Mikroschalter Position 3 |
| 0x46 | 0x09 | Klappenmotor |
| 0x4E | 0x0A | Klappenmotor |
| 0x3A | 0x0A | Klappenmotor |
| 0x3E | 0x0A | Klappenmotor |
| 0x35 | 0x0A | Klappenmotor |
| 0x3D | 0x0A | Klappenmotor |
| 0x49 | 0x0A | Klappenmotor |
| 0x4D | 0x0A | Klappenmotor |
| 0x0A | 0x0B | Mikroschalter Position 1 oder Verdeckmotor |
| 0x16 | 0x0B | Mikroschalter Position 1 oder Verdeckmotor |
| 0x05 | 0x0B | Mikroschalter Position 1 oder Verdeckmotor |
| 0x19 | 0x0B | Mikroschalter Position 1 oder Verdeckmotor |
| 0x1A | 0x0C | Mikroschalter Position 2 oder Verdeckmotor |
| 0x36 | 0x0C | Mikroschalter Position 2 oder Verdeckmotor |
| 0x15 | 0x0C | Mikroschalter Position 2 oder Verdeckmotor |
| 0x39 | 0x0C | Mikroschalter Position 2 oder Verdeckmotor |
| 0x4A | 0x0D | Mikroschalter Position 3 oder Verdeckmotor |
| 0x09 | 0x0D | Mikroschalter Position 3 oder Verdeckmotor |
| 0x32 | 0x0B | Mikroschalter Position 1 oder Verdeckmotor |
| 0x24 | 0x0C | Mikroschalter Position 2 oder Verdeckmotor |
| 0x51 | 0x0D | Mikroschalter Position 3 oder Verdeckmotor |
| 0x52 | 0x0E | Stack Fehler |
| 0x53 | 0x0F | Gesamtstrom zu gross (&gt;11A) |
| 0x54 | 0x10 | Eintraege im EEPROM sind ungleich |
| 0x55 | 0x11 | Fehler Ueberrollsensor |
| 0xFF | 0xFF | unbekannter Fehlerort |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 18 rows × 3 columns

| BYTE1 | ANTRIEB | BYTE2 |
| --- | --- | --- |
| 0xA9 | KLAPPE_AUF | 0x02 |
| 0x56 | KLAPPE_ZU | 0x01 |
| 0xA5 | VERDECK_AUF | 0x02 |
| 0x5A | VERDECK_ZU | 0x01 |
| 0x95 | UERSS_AUF | 0x02 |
| 0x6A | UERSS_ZU | 0x01 |
| 0xAA | ALLE_AUS | 0x02 |
| 0x08 | VERDECK_OEFFNEN | 0x01 |
| 0x08 | VERDECK_SCHLIESSEN | 0x02 |
| 0x08 | VERDECK_HALT | 0x04 |
| 0x10 | FH_AUF | 0x01 |
| 0x10 | FH_ZU | 0x02 |
| 0x10 | LAMPE_EIN | 0x04 |
| 0x55 | VERRIEGELN | 0x02 |
| 0xAA | ENTRIEGELN | 0x01 |
| 0x10 | RESERVE | 0x08 |
| 0x10 | STOP | 0x00 |
| 0xFF | ERROR | 0x00 |
