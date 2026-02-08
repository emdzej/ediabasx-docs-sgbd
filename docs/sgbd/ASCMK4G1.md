# ASCMK4G1.prg

- Jobs: [12](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Antiblockier- u. Aut.-Stabilitaets-Controll MK4G E36 K1 Protokoll |
| ORIGIN | BMW EF-73 Kusch |
| REVISION | 1.10 |
| AUTHOR | BMW TP-421 Hirsch, BMW TP-423 Pollmann, BMW EF-73 Kusch |
| COMMENT | Keine Diagnose bei V &gt; 2.5 km/h |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer ABS_ASC_MK4G m. K1 Prot.
- [IDENT](#job-ident) - Ident-Daten fuer ABS_ASC_MK4G m. K1 Prot.
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen fuer ABS_ASC_MK4G m. K1 Prot.
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen fuer ABS_ASC_MK4G m. K1 Prot.
- [STATUS_IO_LESEN](#job-status-io-lesen) - Status Eingaenge ABS_ASC_MK4G m. K1 Prot.
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern mehrerer digitaler Ausgaenge
- [STEUERN_ANALOG](#job-steuern-analog) - Ansteuern Drosselklappe
- [ABS_REGELSIMULATION](#job-abs-regelsimulation) - Ansteuern mehrerer digitaler Ausgaenge
- [ASC](#job-asc) - Steuern_Digital Drehzahlabsenkung
- [ASC_SIM_HA](#job-asc-sim-ha) - Steuern_Digital ansteueren u. halten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden

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

Init-Job fuer ABS_ASC_MK4G m. K1 Prot.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer ABS_ASC_MK4G m. K1 Prot.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_SW_NR | int | BMW-Softwarenummer |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen fuer ABS_ASC_MK4G m. K1 Prot.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ORT_NR | int | momentan identisch Fehlerbytemaske |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_ART_ANZ | int | Anzahl der Fehlerarten bei ABS_ASC_MK4G m. K1 Prot. = 0 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen bei ABS_ASC_MK4G m. K1 Prot. = 0 |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen fuer ABS_ASC_MK4G m. K1 Prot.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Status Eingaenge ABS_ASC_MK4G m. K1 Prot.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_RAD_GESCHW_VL_WERT | long | Radgeschwindigkeit vorne links |
| STAT_RAD_GESCHW_VR_WERT | long | Radgeschwindigkeit vorne rechts |
| STAT_RAD_GESCHW_HL_WERT | long | Radgeschwindigkeit hinten links |
| STAT_RAD_GESCHW_HR_WERT | long | Radgeschwindigkeit hinten rechts |
| STAT_RAD_GESCHW_EINH | string | Einheit = km/h |
| STAT_BREMSLICHT_SCHALTER_EIN | int | 0 oder 1 |
| STAT_MOTORDREHZAHL_WERT_500 | int | 0 oder 1 (groesser oder kleiner 500 1/min) |
| STAT_MOTORDREHZAHL_EINH | string | Einheit = 1/min |
| STAT_DROSSELKLAPPEN_IST_WERT | int | Momentane Drosselklappenstellung |
| STAT_DROSSELKLAPPEN_EINH | string | Einheit = Winkelgrad |
| STAT_GETRIEBEVARIANTE_TEXT | string | Handschalter od. Automatik |
| STAT_MOTORDREHZAHL_WERT | int | Momentane Motordrehzahl in 1/min |
| STAT_MOTORVARIANTE_TEXT | string | Codiervariante Motortyp |
| TAKTZAEHLER_GRENZ_WERT | long |  |
| TAKTZAEHLER_IST_WERT | long | Wert der Triggerschwelle |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern mehrerer digitaler Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| ORT1 | string | gewuenschte Komponente 1 |
| ORT2 | string | gewuenschte Komponente 2 |
| ORT3 | string | gewuenschte Komponente 3 |
| ORT4 | string | gewuenschte Komponente 4 |
| ORT5 | string | gewuenschte Komponente 5 |
| ORT6 | string | gewuenschte Komponente 6 |
| ORT7 | string | gewuenschte Komponente 7 |
| ORT8 | string | gewuenschte Komponente 8 |
| ORT9 | string | gewuenschte Komponente 9 |
| ORT10 | string | gewuenschte Komponente 10 |
| ORT11 | string | gewuenschte Komponente 11 |
| ORT12 | string | gewuenschte Komponente 12 |
| ORT13 | string | gewuenschte Komponente 13 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-steuern-analog"></a>
### STEUERN_ANALOG

Ansteuern Drosselklappe

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| WINKEL | int | gewuenschte Drosselklappenstellung in Winkelgrad |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-abs-regelsimulation"></a>
### ABS_REGELSIMULATION

Ansteuern mehrerer digitaler Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL_WARTESCHLEIFEN | int | Anzahl Warteschleifen, wenn nicht angegeben == 3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-asc"></a>
### ASC

Steuern_Digital Drehzahlabsenkung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-asc-sim-ha"></a>
### ASC_SIM_HA

Steuern_Digital ansteueren u. halten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [FORTTEXTE](#table-forttexte) (47 × 2)
- [STEUERN](#table-steuern) (13 × 3)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0xFA | ERROR_ECU_FUNCTION |
| 0xFB | ERROR_ECU_FUNCTION |
| 0xF7 | ERROR_ECU_FUNCTION |
| 0xF8 | ERROR_ECU_FUNCTION |
| 0xF2 | ERROR_ECU_FUNCTION |
| 0x0A | ERROR_ECU_NACK |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 47 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x11 | ABS Ventil Einlass vorne links |
| 0x12 | ABS Ventil Auslass vorne links |
| 0x14 | ABS Ventil Einlass vorne rechts |
| 0x18 | ABS Ventil Auslass vorne rechts |
| 0x21 | ABS Ventil Einlass hinten links |
| 0x22 | ABS Ventil Auslass hinten links |
| 0x24 | ABS Ventil Einlass hinten rechts |
| 0x28 | ABS Ventil Auslass hinten rechts |
| 0x31 | Alle ABS Ventile |
| 0x38 | ASC-Trennventil |
| 0x32 | Drosselklappensteller oder Stellmechanismus |
| 0x41 | Bus od. Busprozessor |
| 0x42 | TD-Leitung |
| 0x44 | Bus od. Busprozessor |
| 0x48 | Interner IC-Fehler Motor-Control |
| 0x51 | Drehzahlfuehler Fehler VL, Triggersignal |
| 0x52 | Drehzahlfuehler Fehler VR, Triggersignal |
| 0x54 | Drehzahlfuehler Fehler HL, Triggersignal |
| 0x58 | Drehzahlfuehler Fehler HR, Triggersignal |
| 0x61 | Drehzahlfuehler Fehler VL, Kontinuitaet |
| 0x62 | Drehzahlfuehler Fehler VR, Kontinuitaet |
| 0x64 | Drehzahlfuehler Fehler HL, Kontinuitaet |
| 0x68 | Drehzahlfuehler Fehler HR, Kontinuitaet |
| 0x71 | Drehzahlfuehler Fehler VL, Anfahrerkennung |
| 0x72 | Drehzahlfuehler Fehler VR, Anfahrerkennung |
| 0x74 | Drehzahlfuehler Fehler HL, Anfahrerkennung |
| 0x78 | Drehzahlfuehler Fehler HR, Anfahrerkennung |
| 0x81 | Leitung DKG |
| 0x82 | DME Drosselklappenpoti |
| 0x91 | Pumpenmotor oder Kabelbaum |
| 0x92 | Fehlerhafte Codierung |
| 0x94 | Relais, Pumpenmotor, Zaehlerstand oder Taktzaehler |
| 0x98 | Bremslichtschalter |
| 0xA1 | ABS Ventil Auslass vorne links Hydraulik/Kabelbaum |
| 0xA2 | ABS Ventil Auslass vorne rechts Hydraulik/Kabelbaum |
| 0xA4 | ABS Ventil Auslass hinten links Hydraulik/Kabelbaum |
| 0xA8 | ABS Ventil Auslass hinten rechts Hydraulik/Kabelbaum |
| 0xC1 | UBatt. oder ZA-Leitung |
| 0xC2 | UBatt. oder ZWV-Leitung |
| 0xC3 | UBatt. |
| 0xC4 | MSR-Leitung |
| 0xC8 | ASCA-Leitung oder NVRAM |
| 0xD1 | ASC-Drosselklappenpotentiometer oder -leitung |
| 0xD4 | Drosselklappensteller oder -leitung |
| 0xD8 | Drosselklappe, Drosselklappensteller, Bowdenzug oder Kabelbaum |
| 0xFF | NV-RAM |
| 0xXY | unbekannter Fehlerort |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 13 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| EVVL | 0 | 0x01 |
| AVVL | 0 | 0x02 |
| EVVR | 0 | 0x04 |
| AVVR | 0 | 0x08 |
| EVHL | 0 | 0x10 |
| AVHL | 0 | 0x20 |
| EVHR | 0 | 0x40 |
| AVHR | 0 | 0x80 |
| Pumpe | 1 | 0x01 |
| EVASC | 1 | 0x04 |
| ZA | 1 | 0x08 |
| ZWV | 1 | 0x10 |
| XYZ | 2 | 0xFF |
