# fas_64.prg

- Jobs: [17](#jobs)
- Tables: [9](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Gateway SZM&lt;-&gt;SM(E46) |
| ORIGIN | BMW EE-52 Lueddeke |
| REVISION | 0.07 |
| AUTHOR | DELPHI/IEB/B.Burkhart |
| COMMENT | Gateway SZM E64 |
| PACKAGE | 1.18 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Fahrersitz (E46) identifizieren KWP2000: $A5 unpackDS2ServiceRequest Id   Modus  : all
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [SG_STATUS_LESEN](#job-sg-status-lesen) - auslesen der Systemstati aus dem Steuergeraet
- [FERNBEDIENUNG_POSITIONEN_LESEN](#job-fernbedienung-positionen-lesen) - 4 zur Fernbedienung zugeordnete Positionen aus EEPROM auslesen
- [POSITIONEN_LESEN](#job-positionen-lesen) - 3 Speicher- und aktuelle Position aus EEPROM auslesen
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des internen Speichers
- [STEUERN_IO](#job-steuern-io) - Ansteuern eines digitalen Einganges
- [CODIERDATEN_LESEN](#job-codierdaten-lesen) - Daten der Individualisierung lesen
- [CODIERDATEN_SCHREIBEN](#job-codierdaten-schreiben) - Daten der Individualisierung schreiben
- [VARIANTE_LESEN](#job-variante-lesen) - SG-Variante aus Zelle 0x0124 auslesen
- [STATUS_1_LESEN](#job-status-1-lesen) - Stati des SM46_C
- [STATUS_2_LESEN](#job-status-2-lesen) - Stati des SM46
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen

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

Fahrersitz (E46) identifizieren KWP2000: $A5 unpackDS2ServiceRequest Id   Modus  : all

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_BUS_INDEX | int | Bus Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_DATUM_JAHR | int | Herstelldatum (Jahr) |
| ID_DATUM_WOCHE | int | Herstelldatum (Woche) |
| ID_DATUM | string | Herstelldatum (WW/JJ) |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-sg-status-lesen"></a>
### SG_STATUS_LESEN

auslesen der Systemstati aus dem Steuergeraet

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| SOFTSTOP_FAND_STATT | int | bei letzter Verstellung fand Softstop statt |
| BLOCKABSCHALTUNG_FAND_STATT | int | bei letzter Verstellung fand Blockabschaltung statt |
| TIPPTASTEN_BETRIEB_MOEGLICH | int |  |
| SLEEPMODE_MOEGLICH | int |  |
| BEIFAHRERTUER_OFFEN | int |  |
| FAHRERTUER_OFFEN | int |  |
| KLEMME_15_AKTIV | int |  |
| KLEMME_R_AKTIV | int |  |

<a id="job-fernbedienung-positionen-lesen"></a>
### FERNBEDIENUNG_POSITIONEN_LESEN

4 zur Fernbedienung zugeordnete Positionen aus EEPROM auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| FB_POS_1_SITZLAENGE_WERT | long | gespeicherte Sitzlaengenposition 1 |
| FB_POS_2_SITZLAENGE_WERT | long | gespeicherte Sitzlaengenposition 2 |
| FB_POS_3_SITZLAENGE_WERT | long | gespeicherte Sitzlaengenposition 3 |
| FB_POS_4_SITZLAENGE_WERT | long | gespeicherte Sitzlaengenposition 4 |
| FB_POS_1_SITZHOEHE_WERT | long | gespeicherte Sitzhoehenposition 1 |
| FB_POS_2_SITZHOEHE_WERT | long | gespeicherte Sitzhoehenposition 2 |
| FB_POS_3_SITZHOEHE_WERT | long | gespeicherte Sitzhoehenposition 3 |
| FB_POS_4_SITZHOEHE_WERT | long | gespeicherte Sitzhoehenposition 4 |
| FB_POS_1_SITZNEIGUNG_WERT | long | gespeicherte Sitzneigungsposition 1 |
| FB_POS_2_SITZNEIGUNG_WERT | long | gespeicherte Sitzneigungsposition 2 |
| FB_POS_3_SITZNEIGUNG_WERT | long | gespeicherte Sitzneigungsposition 3 |
| FB_POS_4_SITZNEIGUNG_WERT | long | gespeicherte Sitzneigungsposition 4 |
| FB_POS_1_LEHNENNEIGUNG_WERT | long | gespeicherte Lehnenneigungsposition 1 |
| FB_POS_2_LEHNENNEIGUNG_WERT | long | gespeicherte Lehnenneigungsposition 2 |
| FB_POS_3_LEHNENNEIGUNG_WERT | long | gespeicherte Lehnenneigungsposition 3 |
| FB_POS_4_LEHNENNEIGUNG_WERT | long | gespeicherte Lehnenneigungsposition 4 |

<a id="job-positionen-lesen"></a>
### POSITIONEN_LESEN

3 Speicher- und aktuelle Position aus EEPROM auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| POS_1_SITZLAENGE_WERT | long | gespeicherte Sitzlaengenposition 1 |
| POS_2_SITZLAENGE_WERT | long | gespeicherte Sitzlaengenposition 2 |
| POS_3_SITZLAENGE_WERT | long | gespeicherte Sitzlaengenposition 3 |
| POS_AKTUELL_SITZLAENGE_WERT | long | gespeicherte aktuelle Sitzlaengenposition |
| POS_1_SITZHOEHE_WERT | long | gespeicherte Sitzhoehenposition 1 |
| POS_2_SITZHOEHE_WERT | long | gespeicherte Sitzhoehenposition 2 |
| POS_3_SITZHOEHE_WERT | long | gespeicherte Sitzhoehenposition 3 |
| POS_AKTUELL_SITZHOEHE_WERT | long | gespeicherte aktuelle Sitzhoehenposition |
| POS_1_SITZNEIGUNG_WERT | long | gespeicherte Sitzneigungsposition 1 |
| POS_2_SITZNEIGUNG_WERT | long | gespeicherte Sitzneigungsposition 2 |
| POS_3_SITZNEIGUNG_WERT | long | gespeicherte Sitzneigungsposition 3 |
| POS_AKTUELL_SITZNEIGUNG_WERT | long | gespeicherte aktuelle Sitzneigungsposition |
| POS_1_LEHNENNEIGUNG_WERT | long | gespeicherte Lehnenneigungsposition 1 |
| POS_2_LEHNENNEIGUNG_WERT | long | gespeicherte Lehnenneigungsposition 2 |
| POS_3_LEHNENNEIGUNG_WERT | long | gespeicherte Lehnenneigungsposition 3 |
| POS_AKTUELL_LEHNENNEIGUNG_WERT | long | gespeicherte aktuelle Lehnenneigungsposition |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE_HIGH | int |  |
| ADRESSE_LOW | int |  |
| ANZAHL | int | 1 bis 16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| DATENFELD | binary | Ergebnisfeld mit 1 bis 16 Bytes |
| _TEL_ANTWORT | binary |  |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Beschreiben des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int |  |
| ZELLE | int | immer nur 1 Speicherzelle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-io"></a>
### STEUERN_IO

Ansteuern eines digitalen Einganges

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT1 | string | gewuenschte Komponente |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-codierdaten-lesen"></a>
### CODIERDATEN_LESEN

Daten der Individualisierung lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| CODIER_BYTE | unsigned char | Datenbyte der Infividualisierung |
| KENNF_FREI | int | Bit7: Kennfeldsteuerung 1: aktiviert 0: nicht aktiv |
| KSSE_FREI | int | Bit6: Kopfstuetze Sicherheitseinstellung 1: keine Funktionsmerkmale 0: Kopfstuetze bei Bedarf auffahren |
| LVK_FREI | int | Bit5: Lehnenverriegelungskontakt Kontrolle 1: LVK Statusausgang laut Definition 0: keine Funktionsmerkmale |
| EHMZB | int | Bit4: Einstiegshilfe mit Zusatzbedingungen 1: EH nur, wenn T�r offen und Fzg. steht 0: EH auch ohne K-Bus m”glich |
| EHMHG | int | Bit3: Einstiegshilfe mit hoher Geschwindigkeit 1: bei EH Anforderung DK-Motor aktivieren (Softstop bekannt) 0: normaler SLV-Antrieb |
| TTB_FR | int | Bit2: Tipptastenbetrieb frei 1: TT-Betrieb m”glich 0: nur Dauertasten |
| PERS | int | Bit1: Personalisierung 1: keine Reaktion auf FB Telegramme 0: Abruf der Funkschl�sselpositionen |
| ARV | int | Bit0: Abrufvariante 1: Sitz verf„hrt erst nach ”ffnen der T�r 0: sofort nach Empfang des FB-Telegramms |
| _TEL_ANTWORT | binary |  |

<a id="job-codierdaten-schreiben"></a>
### CODIERDATEN_SCHREIBEN

Daten der Individualisierung schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_BYTE | unsigned char | Datenbyte der Infividualisierung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-variante-lesen"></a>
### VARIANTE_LESEN

SG-Variante aus Zelle 0x0124 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| SG_VARIANTE | string | Variante im Klartext |
| _TEL_ANTWORT | binary |  |

<a id="job-status-1-lesen"></a>
### STATUS_1_LESEN

Stati des SM46_C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_SCHALTER_SLV_VOR_EIN | int |  |
| STAT_SCHALTER_SLV_ZURUECK_EIN | int |  |
| STAT_SCHALTER_SHV_AUF_EIN | int |  |
| STAT_SCHALTER_SHV_AB_EIN | int |  |
| STAT_SCHALTER_SNV_AUF_EIN | int |  |
| STAT_SCHALTER_SNV_AB_EIN | int |  |
| STAT_SCHALTER_LEHNE_VOR_EIN | int |  |
| STAT_SCHALTER_LEHNE_ZURUECK_EIN | int |  |
| STAT_SCHALTER_KHV_AUF_EIN | int |  |
| STAT_SCHALTER_KHV_AB_EIN | int |  |
| STAT_TASTE_MEM_EIN | int |  |
| STAT_TASTE_POS1_EIN | int |  |
| STAT_TASTE_POS2_EIN | int |  |
| STAT_TASTE_POS3_EIN | int |  |
| STAT_EHV_EIN | int |  |
| STAT_EHZ_EIN | int |  |
| STAT_EE_SCHALTER_POS | int | 0=aus,1=vor,2=zurueck |
| STAT_RS_EIN | int |  |
| STAT_BC_EIN | int |  |
| STAT_KL30_EIN | int |  |
| STAT_LVK_EIN | int |  |
| STAT_LED_EIN | int |  |
| STAT_POS_SLV_WERT | long |  |
| STAT_POS_SHV_WERT | long |  |
| STAT_POS_SNV_WERT | long |  |
| STAT_POS_LNV_WERT | long |  |
| STAT_POS_KHV_WERT | long |  |
| STAT_SCHALTER_SITZLAENGE | int | 0=aus,1=vor,2=zurueck |
| STAT_SCHALTER_SITZHOEHE | int | 0=aus,1=auf,2=ab |
| STAT_SCHALTER_NEIGUNG | int | 0=aus,1=auf,2=ab |
| STAT_SCHALTER_SITZLEHNE | int | 0=aus,1=vor,2=zurueck |
| STAT_SCHALTER_KOPFSTUETZE | int | 0=aus,1=auf,2=ab |
| STAT_MEMORYSCHALTER | int | bitcodiert, Werte zwischen 0 und 15! bit 0=MEM-Taste bit 1=Taste 1 bit 2=Taste 2 bit 3=Taste 3 |

<a id="job-status-2-lesen"></a>
### STATUS_2_LESEN

Stati des SM46

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_SPANNUNG_HALLS_LNV_WERT | real | Spannung am Hallsensor |
| STAT_SPANNUNG_HALLS_SHV_WERT | real | Spannung am Hallsensor |
| STAT_SPANNUNG_HALLS_SNV_WERT | real | Spannung am Hallsensor |
| STAT_SPANNUNG_HALLS_SLV_WERT | real | Spannung am Hallsensor |
| STAT_SPANNUNG_HALLS_KHV_WERT | real | Spannung am Hallsensor |
| STAT_SPANNUNG_HALLS_LVK_WERT | real | Spannung am Hallsensor |
| STAT_SPANNUNG_KL30_WERT | real | Batterie-Spannung am SG |
| STAT_SPANNUNGEN_EINH | string | Einheit der Spannung |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ANZ | int | Gesamtzahl Fehler |
| F_ORT_NR | int | identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int |  |
| F_ART_ANZ | int | immer 1 |
| F_ART1_NR | int | momentan identisch Art-Bit |
| F_ART1_TEXT | string | Fehlerart als Text table FArtTexteSM ARTTEXT |
| F_UW_ANZ | int | immer 0 |
| F_HEX_CODE | binary | Hexdaten des Fehlers (2 Bytes) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (23 × 2)
- [FARTTEXTESM](#table-farttextesm) (3 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [STEUERN](#table-steuern) (20 × 4)
- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (67 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 23 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Hallsensor Lehnenneigung, Kurzschluss nach Masse |
| 0x01 | Hallsensor Lehnenneigung, Unterbrechung |
| 0x02 | Hallsensor Lehnenneigung, Kurzschluss nach Ubatt |
| 0x03 | Hallsensor Sitzhoehe, Kurzschluss nach Masse |
| 0x04 | Hallsensor Sitzhoehe, Unterbrechung |
| 0x05 | Hallsensor Sitzhoehe, Kurzschluss nach Ubatt |
| 0x06 | Hallsensor Sitzneigung, Kurzschluss nach Masse |
| 0x07 | Hallsensor Sitzneigung, Unterbrechung |
| 0x08 | Hallsensor Sitzneigung, Kurzschluss nach Ubatt |
| 0x09 | Hallsensor Sitzschlitten, Kurzschluss nach Masse |
| 0x0A | Hallsensor Sitzschlitten, Unterbrechung |
| 0x0B | Hallsensor Sitzschlitten, Kurzschluss nach Ubatt |
| 0x0C | Hallsensor Kopfstuetze, Kurzschluss nach Masse |
| 0x0D | Hallsensor Kopfstuetze, Unterbrechung |
| 0x0E | Hallsensor Kopfstuetze, Kurzschluss nach Ubatt |
| 0x0F | Hallsensor Lehnenverriegelung, Kurzschluss nach Masse |
| 0x10 | Hallsensor Lehnenverriegelung, Unterbrechung |
| 0x11 | Hallsensor Lehnenverriegelung, Kurzschluss nach Ubatt |
| 0x12 | Hallsensor ST2 nicht aufgesteckt, Kurzschluss nach Masse |
| 0x13 | Steuergeraetefehler, Motorbruecke defekt |
| 0x14 | Sitzbedienschalter, Kurzschluss nach Ubatt |
| 0x15 | Sitzbedienschalter, Kurzschluss nach Masse |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttextesm"></a>
### FARTTEXTESM

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0xXY | unbekannte Fehlerart |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 20 rows × 4 columns

| STEUER_I_O | BYTE1 | BYTE2 | BYTE3 |
| --- | --- | --- | --- |
| STOP | 0x01 | 0x00 | 0x00 |
| SLV_VOR | 0x01 | 0x01 | 0x00 |
| SLV_ZUR | 0x01 | 0x02 | 0x00 |
| SHV_AUF | 0x01 | 0x04 | 0x00 |
| SHV_AB | 0x01 | 0x08 | 0x00 |
| SNV_AUF | 0x01 | 0x10 | 0x00 |
| SNV_AB | 0x01 | 0x20 | 0x00 |
| LNV_VOR | 0x01 | 0x40 | 0x00 |
| LNV_ZUR | 0x01 | 0x80 | 0x00 |
| KHV_AB | 0x01 | 0x00 | 0x02 |
| KHV_AUF | 0x01 | 0x00 | 0x01 |
| POS_1 | 0x02 | 0x01 | 0x00 |
| POS_2 | 0x02 | 0x02 | 0x00 |
| POS_3 | 0x02 | 0x04 | 0x00 |
| LED_AN | 0x03 | 0x01 | 0x00 |
| LED_AUS | 0x03 | 0x00 | 0x00 |
| EH_STOP | 0x04 | 0x00 | 0x00 |
| EH_VOR | 0x04 | 0x01 | 0x00 |
| EH_ZUR | 0x04 | 0x02 | 0x00 |
| XXX | Y | Z | Z |

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

Dimensions: 67 rows × 2 columns

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
