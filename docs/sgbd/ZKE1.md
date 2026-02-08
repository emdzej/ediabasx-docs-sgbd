# ZKE1.prg

- Jobs: [20](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Zentrale Karosserie-Elektronik I |
| ORIGIN | BMW ET-421 Gerd Huber |
| REVISION | 1.13 |
| AUTHOR | Softing Taubert, BMW ET-421 Gerd Huber |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer ZKE I automatischer Aufruf beim ersten Zugriff auf SGBD
- [IDENT](#job-ident) - Ident-Daten fuer ZKE I
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [STATUS_EINGAENGE_0](#job-status-eingaenge-0) - Status der digitalen Eingaenge des GM I (Gruppe 0)
- [STATUS_EINGAENGE_1](#job-status-eingaenge-1) - Status der digitalen Eingaenge des GM I (Gruppe 1)
- [STATUS_EINGAENGE_2](#job-status-eingaenge-2) - Status der digitalen Eingaenge des GM I (Gruppe 2)
- [STATUS_EINGAENGE_3](#job-status-eingaenge-3) - Status der digitalen Eingaenge des GM I (Gruppe 3)
- [STATUS_EINGAENGE_4](#job-status-eingaenge-4) - Status der digitalen Eingaenge des GM I (Gruppe 4)
- [STATUS_EINGAENGE_5](#job-status-eingaenge-5) - Status der digitalen Eingaenge des GM I (Gruppe 5)
- [STATUS_EINGAENGE_6](#job-status-eingaenge-6) - Status der digitalen Eingaenge des GM I (Gruppe 6)
- [STATUS_EINGAENGE_7](#job-status-eingaenge-7) - Status der digitalen Eingaenge des GM I (Gruppe 7)
- [STATUS_EINGAENGE_8](#job-status-eingaenge-8) - Status der digitalen Eingaenge des GM I (Gruppe 8)
- [STATUS_AUSGAENGE_0](#job-status-ausgaenge-0) - Status der digitalen Ausgaenge des GM I (Gruppe 0)
- [STATUS_AUSGAENGE_1](#job-status-ausgaenge-1) - Status der digitalen Ausgaenge des GM I (Gruppe 1)
- [STATUS_AUSGAENGE_2](#job-status-ausgaenge-2) - Status der digitalen Ausgaenge des GM I (Gruppe 2)
- [STEUERN_EINGANG](#job-steuern-eingang) - Ansteuern eines digitalen Eingangs v. GM1 !!! ACHTUNG: Die ZKE1 antwortet nicht !!!
- [STEUERN_AUSGANG](#job-steuern-ausgang) - Ansteuern eines digitalen Ausgangs v. GM1 !!! ACHTUNG: Die ZKE1 antwortet nicht !!!

<a id="job-info"></a>
### INFO

Info fuer Anwender

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergerat im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Namen aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch / english |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job fuer ZKE I automatischer Aufruf beim ersten Zugriff auf SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer ZKE I

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_NACK |
| ID_IDENT | int | Indentifikation alt/neu  (0/1) |
| ID_HW_NR | int | Hardwarestand |
| ID_SW_NR | int | Softwarestand |
| ID_PROGSPEICHER | int | Programmspeicher ROM/EPROM (0/1) |
| ID_AUSSTATTUNG | int | Scheibenwischersteuerung       (Bit 0 = 1) Anpressdruckverstellung        (Bit 1 = 1) Scheibenwischerreinigung       (Bit 2 = 1) Zentralverriegelung            (Bit 3 = 1) Tuerschl.heizung u. Innenlicht (Bit 4 = 1) Fensterheber u. Schiebedach    (Bit 5 = 1) Elektr. Sicherung              (Bit 6 = 1) |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_NACK, ERROR_TABELLE |
| F_ORT_NR | int | Fehlerort als Index |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_ART_ANZ | int | immer 1 |
| F_UW_ANZ | int | immer 0 |
| F_ART1_NR | int | Fehlerart 1 des einzelnen Fehlers als Index |
| F_ART1_TEXT | string | Fehlerart 1 des einzelnen Fehlers als Text table FArtTexte ARTTEXT |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-status-eingaenge-0"></a>
### STATUS_EINGAENGE_0

Status der digitalen Eingaenge des GM I (Gruppe 0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_VR1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_VR3_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_VR2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ER_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ZS1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ZS2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_VR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-eingaenge-1"></a>
### STATUS_EINGAENGE_1

Status der digitalen Eingaenge des GM I (Gruppe 1)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_INT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_WASCH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_WI1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_KL15_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_KLR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_NSW_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SW_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-eingaenge-2"></a>
### STATUS_EINGAENGE_2

Status der digitalen Eingaenge des GM I (Gruppe 2)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_TKBT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_TKFT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_TKH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_TGK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ES_34_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ES_60_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_NS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-eingaenge-3"></a>
### STATUS_EINGAENGE_3

Status der digitalen Eingaenge des GM I (Gruppe 3)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_HK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ZV_TYP_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_LA1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_KL50_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_LA2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SIR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-eingaenge-4"></a>
### STATUS_EINGAENGE_4

Status der digitalen Eingaenge des GM I (Gruppe 4)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_DADV_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_DSWR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_DFHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_DZS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_DZV_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_DFHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_DTSH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-eingaenge-5"></a>
### STATUS_EINGAENGE_5

Status der digitalen Eingaenge des GM I (Gruppe 5)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_SSHDH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SSHDZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SSHDA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHFHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHBTA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHFTA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHBHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-eingaenge-6"></a>
### STATUS_EINGAENGE_6

Status der digitalen Eingaenge des GM I (Gruppe 6)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_FHFHE_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHBHE_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHBTE_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHFTE_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHBHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHFHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHFTZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHBTZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-eingaenge-7"></a>
### STATUS_EINGAENGE_7

Status der digitalen Eingaenge des GM I (Gruppe 7)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_CS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_RSK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SHD_EH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SHD_EV_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-eingaenge-8"></a>
### STATUS_EINGAENGE_8

Status der digitalen Eingaenge des GM I (Gruppe 8)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ADV_LSB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ADV_MID_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ADV_MSB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-ausgaenge-0"></a>
### STATUS_AUSGAENGE_0

Status der digitalen Ausgaenge des GM I (Gruppe 0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_TSH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHBTZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHBTA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SHDMOTP_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHBHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHFHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHFTA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FHFTZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-ausgaenge-1"></a>
### STATUS_AUSGAENGE_1

Status der digitalen Ausgaenge des GM I (Gruppe 1)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_WI1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_WP_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SRA_SW_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SRA_NS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IL_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ES_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ADVP_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ADVM_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-ausgaenge-2"></a>
### STATUS_AUSGAENGE_2

Status der digitalen Ausgaenge des GM I (Gruppe 2)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_MZVP_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_MZVM_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_MZS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_QZV_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_FST_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_WB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-eingang"></a>
### STEUERN_EINGANG

Ansteuern eines digitalen Eingangs v. GM1 !!! ACHTUNG: Die ZKE1 antwortet nicht !!!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table EINGANG NAME TEXT |
| EIN | int | '1', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | immer OKAY |
| _TEL1_AN_SG | binary |  |
| _TEL1_ANTWORT | binary |  |
| _TEL2_AN_SG | binary |  |

<a id="job-steuern-ausgang"></a>
### STEUERN_AUSGANG

Ansteuern eines digitalen Ausgangs v. GM1 !!! ACHTUNG: Die ZKE1 antwortet nicht !!!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table AUSGANG NAME TEXT |
| EIN | int | '1', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | immer OKAY |
| _TEL1_AN_SG | binary |  |
| _TEL1_ANTWORT | binary |  |
| _TEL2_AN_SG | binary |  |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (21 × 3)
- [FARTTEXTE](#table-farttexte) (2 × 2)
- [EINGANG](#table-eingang) (29 × 4)
- [AUSGANG](#table-ausgang) (17 × 4)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 21 rows × 3 columns

| ORT | SA | ORTTEXT |
| --- | --- | --- |
| 0x00 | 0x00 | unbekannter Fehlerort |
| 0x01 | 0x01 | SWS01 Stufe 1 u.Intervall |
| 0x02 | 0x01 | SWS03 Blockierschutz aktiv |
| 0x03 | 0x02 | ADV01 Blockierschutz aktiv |
| 0x04 | 0x02 | ADV02 ADV-Relais, Sicher. |
| 0x05 | 0x08 | ZV_01 ZV-Relais Sicherung |
| 0x06 | 0x08 | ZV_02 ZV-Relais Verriegel |
| 0x07 | 0x08 | ZV_03 ZV-Relais Entriegel |
| 0x08 | 0x10 | TSH   Tuerschlossheizung |
| 0x09 | 0x20 | SHD01 Rel-FH.Beift u S.hi |
| 0x0a | 0x20 | SHD02 Rel-FH.Beiftuer |
| 0x0b | 0x20 | SHD03 Rel-SHD |
| 0x0c | 0x20 | SHD04 Rel-FH.Beif.seite hi |
| 0x0d | 0x20 | SHD05 Rel-FH.Fahrerseite hi |
| 0x0e | 0x20 | SHD06 Rel-FH.Fahrertuer |
| 0x0f | 0x20 | SHD07 Rel-FH.Fahrerseite hi |
| 0x10 | 0x20 | SHD08 FH Fahrt Weg/Zeit |
| 0x11 | 0x20 | SHD09 FH Beift Weg/Zeit |
| 0x12 | 0x20 | SHD10 FH Beifs hi Weg/Zeit |
| 0x13 | 0x20 | SHD11 FH Fahrs hi Weg/Zeit |
| 0x14 | 0x20 | SHD12 SHD Weg/Zeit |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 2 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0 | Fehler momentan nicht vorhanden |
| 1 | Fehler momentan vorhanden |

<a id="table-eingang"></a>
### EINGANG

Dimensions: 29 rows × 4 columns

| NAME | BYTE | MASK | TEXT |
| --- | --- | --- | --- |
| VR1 | 0xE0 | 0x01 | Stiftkontakt VR1 |
| VR3 | 0xE0 | 0x02 | Stiftkontakt VR3 |
| VR2 | 0xE0 | 0x04 | Stiftkontakt VR2 |
| ER | 0xE0 | 0x08 | Stiftkontakt ER |
| ZS1 | 0xE0 | 0x10 | Schlosskontakt ZS1 |
| ZS2 | 0xE0 | 0x20 | Schlosskontakt ZS2 |
| VR | 0xE0 | 0x40 | Schlosskontakt VR |
| INT | 0xE1 | 0x01 | Intervallwischen |
| WASCH | 0xE1 | 0x02 | Waschen |
| WI1 | 0xE1 | 0x04 | Wischerstufe1 |
| KL15 | 0xE1 | 0x10 | Klemme 15 |
| KLR | 0xE1 | 0x20 | Klemme R |
| NSW | 0xE1 | 0x40 | Nebelscheinwerfer |
| SW | 0xE1 | 0x80 | Scheinwerfer |
| TKBT | 0xE2 | 0x01 | Tuerkontakt BT |
| TKFT | 0xE2 | 0x02 | Tuerkontakt FT |
| TKH | 0xE2 | 0x04 | Tuerkontakt hinten |
| TGK | 0xE2 | 0x08 | Tuergriffkontakt |
| KL50 | 0xE3 | 0x08 | Klemme 50 |
| SIR | 0xE3 | 0x80 | Scheibenintensiv-Reinigung |
| FHFHA | 0xE5 | 0x10 | Schalter FH-FH Auf |
| FHBTA | 0xE5 | 0x20 | Schalter FH-BT Auf |
| FHFTA | 0xE5 | 0x40 | Schalter FH-FT Auf |
| FHBHA | 0xE5 | 0x80 | Schalter FH-BH Auf |
| FHBHZ | 0xE6 | 0x10 | Schalter FH-BH |
| FHFHZ | 0xE6 | 0x20 | Schalter FH-FH |
| FHFTZ | 0xE6 | 0x40 | Schalter FH-FT |
| FHBTZ | 0xE6 | 0x80 | Schalter FH-BT |
| XY | 0xXY | 0xXY | nicht definiertes Signal |

<a id="table-ausgang"></a>
### AUSGANG

Dimensions: 17 rows × 4 columns

| NAME | BYTE | MASK | TEXT |
| --- | --- | --- | --- |
| TSH | 0xF0 | 0x01 | Tuerschlossheizung |
| FHBTZ | 0xF0 | 0x02 | FH-BT, FH-BH Zu |
| FHBTA | 0xF0 | 0x04 | FH-BT Auf |
| FHBHA | 0xF0 | 0x10 | FH-BH Auf |
| FHFHA | 0xF0 | 0x20 | FH-FH Auf |
| FHFTA | 0xF0 | 0x40 | FH-FT Auf |
| WI1 | 0xF1 | 0x01 | Wischerstufe 1 |
| WP | 0xF1 | 0x02 | Waschpumpe |
| SRA_SW | 0xF1 | 0x04 | SRA-Pumpe Scheinwerfer |
| SRA_NS | 0xF1 | 0x08 | SRA-Pumpe Nebelscheinwerfer |
| IL | 0xF1 | 0x10 | Innenlicht |
| MZV+ | 0xF2 | 0x01 | Motor ZV+ |
| MZV- | 0xF2 | 0x02 | Motor ZV- |
| MZS | 0xF2 | 0x04 | Motor ZS |
| FST | 0xF2 | 0x40 | Signal 'Fahrzeug steht' |
| WB | 0xF2 | 0x80 | Warnblinker |
| XY | 0xXY | 0xXY | nicht definiertes Signal |
