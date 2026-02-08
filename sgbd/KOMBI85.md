# KOMBI85.prg

- Jobs: [47](#jobs)
- Tables: [16](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | KOMBI E85  |
| ORIGIN | BMW EE-42 Ramboeck |
| REVISION | 2.200 |
| AUTHOR | BMW EI-42 Ramboeck, BMW TI-431 Dennert, Volke EI-42 Angerer, IAV EI-42 Wallmann |
| COMMENT | N/A |
| PACKAGE | 1.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [IDENT](#job-ident) - Identdaten
- [IDENT_SW](#job-ident-sw) - Identdaten Software
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicherinhalt aus SG lesen
- [STATUS_GWSZ_OFFSET_LESEN](#job-status-gwsz-offset-lesen) - OFFSET-Wert des GWSZ aus EEPROM lesen
- [STEUERN_GWSZ_OFFSET_SCHREIBEN](#job-steuern-gwsz-offset-schreiben) - OFFSET-Wert des GWSZ in EEPROM schreiben
- [STATUS_KALIBRIERFAKTOR_VERBRAUCH_LESEN](#job-status-kalibrierfaktor-verbrauch-lesen) - Kalibrierfaktor Verbrauch aus EEPROM W-Adr. 1B lesen
- [STEUERN_KALIBRIERFAKTOR_VERBRAUCH_SCHREIBEN](#job-steuern-kalibrierfaktor-verbrauch-schreiben) - Kalibrierfaktor Verbrauch in EEPROM W-Adr. 1B schreiben
- [STEUERN_SIA_KORREKTUR_SCHREIBEN](#job-steuern-sia-korrektur-schreiben) - Toggeln der SIA Inspektions- bzw. Oelservices
- [STEUERN_ZEITINSPEKTION_DEAKTIVIEREN](#job-steuern-zeitinspektion-deaktivieren) - Vorziehen der Zeitinspection vor der Zeitgrenze
- [STEUERN_ZEITINSPEKTIONSDATUM_SCHREIBEN](#job-steuern-zeitinspektionsdatum-schreiben) - Beschreiben des Monats- u. Jahres-Bytes im EEPROM
- [STATUS_ZEITINSPEKTIONSDATUM_LESEN](#job-status-zeitinspektionsdatum-lesen) - Monats- u. Jahres-Byte des Zeitinspektionsdatums aus EEPROM WortAdr. 1C
- [SOFTWARE_RESET](#job-software-reset) - Kombi loest selbststaendig einen Reset aus
- [STEUERN_SIA_RESET](#job-steuern-sia-reset) - Ruecksetzen der Service-Intervall-Anzeige
- [GWSZ_RESET](#job-gwsz-reset) - GWSZ zuruecksetzen, nur moeglich wenn Km-Stand &lt; 255
- [STATUS_AIF_GWSZ_LESEN](#job-status-aif-gwsz-lesen) - Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen
- [STATUS_AIF_FG_NR_LESEN](#job-status-aif-fg-nr-lesen) - Auslesen der Fahrgestellnummer
- [STATUS_AIF_SIA_DATEN_LESEN](#job-status-aif-sia-daten-lesen) - Anwenderinfofeld Block 3 auslesen
- [STATUS_AIF_TANKDATEN_LESEN](#job-status-aif-tankdaten-lesen) - Tankdaten aus Anwenderinfofeld auslesen
- [STATUS_AIF_AUSSENTEMP_LESEN](#job-status-aif-aussentemp-lesen) - Tankdaten aus Anwenderinfofeld auslesen
- [STATUS_AIF_DATUM_UHRZEIT_LESEN](#job-status-aif-datum-uhrzeit-lesen) - Eingestelltes Datum und Uhrzeit aus Anwenderinfofeld auslesen
- [STATUS_AIF_V_KMT_DZ_CON_LESEN](#job-status-aif-v-kmt-dz-con-lesen) - Auslesen von Fahrgeschwindigkeit, Kuehlmitteltemperatur, Drehzahl und Verbrauch aus dem Anwenderinfofeld
- [STATUS_TACHO_ENDWERT_LESEN](#job-status-tacho-endwert-lesen) - Auslesen des Tacho-Endausschlags aus dem EEPROM
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - SG - Selbsttest ausloesen
- [STEUERN_ANZEIGE](#job-steuern-anzeige) - Anzeigenkomponenten steuern
- [STEUERN_PIEZO](#job-steuern-piezo) - interner Piezo ansteuern
- [STEUERN_LEUCHTE](#job-steuern-leuchte) - Details zur SW-Version mit JOB_IDENT_SW auslesen. Leuchten in der Anzeigeeinheit ansteuern. Zum Aufruf 4 Parameter in Folge mit Semikolon getrennt und ohne Leerzeichen i.d. Form dez (0..255), hex (0x00..0xFF) oder bin (0y00000000..0y11111111) uebergeben. Die Belegung der Datenbytes ist separat beschrieben. 
- [STATUS_IO_LESEN](#job-status-io-lesen) - Eingangs- und Ausgangsstati lesen
- [STATUS_ANALOG_LESEN](#job-status-analog-lesen) - Spezielle analoge Eingaenge lesen
- [RAM_LESEN](#job-ram-lesen) - Internen RAM-Speicher auslesen
- [EEPROM_LESEN](#job-eeprom-lesen) - EEPROM-Speicher auslesen
- [STATUS_KOMBI_VERRIEGELT](#job-status-kombi-verriegelt)
- [C_FA_LESEN](#job-c-fa-lesen) - Fahrzeugauftrag lesen Gueltiger Adressbereich: 0x100 - 0x1BF (384 Bytes, 192 words)
- [C_FA_AUFTRAG](#job-c-fa-auftrag) - Fahrzeugauftrag schreiben Fahrzeugauftrag lesen Gueltiger Adressbereich: 0x100 - 0x1BF (384 Bytes)
- [C_S_AUFTRAG](#job-c-s-auftrag) - Codierdaten schreiben und verifizieren
- [C_S_SCHREIBEN](#job-c-s-schreiben) - Codierdaten schreiben
- [C_S_LESEN](#job-c-s-lesen) - Codierdaten schreiben und verifizieren
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen der Fahrgestellnummer
- [C_CHECKSUM](#job-c-checksum) - Berechnung und Speicherung der Checksumme
- [STEUERN_BREMSLICHT](#job-steuern-bremslicht) - Steuern des Bremslichtes ueber Diagnose Nach Ausfuehren des Jobs wird das Bremslicht ueber K-Line im Lichtschaltzentrum angesteuert

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

Initialisierung und Kommunikationsparameter DS2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_ARGUMENT, wenn Argumente nicht uebergeben oder ausser Bereich |

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

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode aufrechterhalten

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

<a id="job-ident"></a>
### IDENT

Identdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| ID_CAN_INDEX | int | CAN-Index |
| ID_AENDERUNGSINDEX | int | Aenderungsindex |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-ident-sw"></a>
### IDENT_SW

Identdaten Software

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_SW_NR_LIEF | string | Softwarenummer (Full software number) |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicherinhalt aus SG lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status-FS: OKAY, ERROR_.. |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zum Fehlerort |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_ART1_NR | int | Fehlerart-Nr |
| F_ART1_TEXT | string | Fehlerart-Text |
| F_ART2_NR | int | Fehlerart-Nr |
| F_ART2_TEXT | string | Fehlerart-Text |
| F_ART3_NR | int | Fehlerart-Nr |
| F_ART3_TEXT | string | Fehlerart-Text |
| F_ART4_NR | int | Fehlerart-Nr |
| F_ART4_TEXT | string | Fehlerart-Text |
| F_ART5_NR | int | Fehlerart-Nr |
| F_ART5_TEXT | string | Fehlerart-Text |
| F_ART6_NR | int | Fehlerart-Nr |
| F_ART6_TEXT | string | Fehlerart-Text |
| F_ART7_NR | int | Fehlerart-Nr |
| F_ART7_TEXT | string | Fehlerart-Text |
| F_UW_ANZ | int | immer 0 |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| STAT_ANTWORT_EEPROM | string | Job-Status EEPROM lesen: OKAY, ERROR_.. |
| STAT_GWSZ_AIRBAG | string | km-Stand beim auftreten des Airbagfehlers |

<a id="job-status-gwsz-offset-lesen"></a>
### STATUS_GWSZ_OFFSET_LESEN

OFFSET-Wert des GWSZ aus EEPROM lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_GWSZ_OFFSET_WERT | int | absoluter Offset-Wert des GWSZ (0-255) |
| STAT_GWSZ_OFFSET_EINH | string | Einheit des Offset- Wertes |

<a id="job-steuern-gwsz-offset-schreiben"></a>
### STEUERN_GWSZ_OFFSET_SCHREIBEN

OFFSET-Wert des GWSZ in EEPROM schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GWSZ_OFFSET_WERT | int | absoluter Offset-Wert des GWSZ |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |

<a id="job-status-kalibrierfaktor-verbrauch-lesen"></a>
### STATUS_KALIBRIERFAKTOR_VERBRAUCH_LESEN

Kalibrierfaktor Verbrauch aus EEPROM W-Adr. 1B lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KALIBRIERFAKTOR_WERT | int | Kalibrierfaktor Verbrauch |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| _ANTWORT | binary | Antworttelegramm von SG |

<a id="job-steuern-kalibrierfaktor-verbrauch-schreiben"></a>
### STEUERN_KALIBRIERFAKTOR_VERBRAUCH_SCHREIBEN

Kalibrierfaktor Verbrauch in EEPROM W-Adr. 1B schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KALIBRIERFAKTOR_WERT | long | Kalibrierfaktor Verbrauch (0-1000) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-steuern-sia-korrektur-schreiben"></a>
### STEUERN_SIA_KORREKTUR_SCHREIBEN

Toggeln der SIA Inspektions- bzw. Oelservices

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |

<a id="job-steuern-zeitinspektion-deaktivieren"></a>
### STEUERN_ZEITINSPEKTION_DEAKTIVIEREN

Vorziehen der Zeitinspection vor der Zeitgrenze

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATUM_MONAT | int | Monatsangabe [1-12], aktuelles Datum |
| DATUM_JAHR | int | Jahresangabe [0-99], akuelles Datum |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM_1_ZEITGRENZE_LESEN | binary | Telegramm an SG: Zeitgrenze lesen |
| SG_ANTWORT_1_ZEITGRENZE_LESEN | binary | Antworttelegramm von SG: Zeitgrenze lesen |
| TELEGRAMM_2_ZEITGRENZE_SCHREIBEN | binary | Telegramm an SG: Zeitgrenze schreiben |
| SG_ANTWORT_2_ZEITGRENZE_SCHREIBEN | binary | Antworttelegramm von SG: Zeitgrenze schreiben |
| TELEGRAMM_3_ZEITINSPEKTION_LESEN | binary | Telegramm an SG: Zeitinspektionsdatum lesen |
| SG_ANTWORT_3_ZEITINSPEKTION_LESEN | binary | Antworttelegramm von SG: Zeitinspektionsdatum lesen |
| TELEGRAMM_4_ZEITINSPEKTION_SCHREIBEN | binary | Telegramm an SG: Zeitinspektionsdatum schreiben |
| SG_ANTWORT_4_ZEITINSPEKTION_SCHREIBEN | binary | Antworttelegramm von SG: Zeitinspektionsdatum schreiben |
| TELEGRAMM_5_CS_LESEN | binary | Telegramm an SG: Checksum lesen |
| SG_ANTWORT_5_CS_LESEN | binary | Antworttelegramm von SG: Checksum lesen |
| TELEGRAMM_6_CS_SCHREIBEN | binary | Telegramm an SG: Checksum schreiben |
| SG_ANTWORT_6_CS_SCHREIBEN | binary | Antworttelegramm von SG: Checksum schreiben |
| TELEGRAMM_7_SW_RESET | binary | Telegramm an SG: Software-Reset ausfuehren |
| SG_ANTWORT_7_SW_RESET | binary | Antworttelegramm von SG: Software-Reset ausfuehren |
| TELEGRAMM_8_ZEITINSPEKTIONS_RESET | binary | Telegramm an SG: Zeitinspektionsreset ausfuehren |
| SG_ANTWORT_8_ZEITINSPEKTIONS_RESET | binary | Antworttelegramm von SG: Zeitinspektionsreset ausfuehren |
| TELEGRAMM_9_ZEITGRENZE_SCHREIBEN | binary | Telegramm an SG: Zeitinspektionsgrenze schreiben |
| SG_ANTWORT_9_ZEITGRENZE_SCHREIBEN | binary | Antworttelegramm von SG: Zeitinspektionsdatum schreiben |
| TELEGRAMM_10_CS_SCHREIBEN | binary | Telegramm an SG: Checksum schreiben |
| SG_ANTWORT_10_CS_SCHREIBEN | binary | Antworttelegramm von SG: Checksum schreiben |
| TELEGRAMM_11_SW_RESET | binary | Telegramm an SG: Software-Reset ausfuehren |
| SG_ANTWORT_11_SW_RESET | binary | Antworttelegramm von SG: Software-Reset ausfuehren |

<a id="job-steuern-zeitinspektionsdatum-schreiben"></a>
### STEUERN_ZEITINSPEKTIONSDATUM_SCHREIBEN

Beschreiben des Monats- u. Jahres-Bytes im EEPROM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEITINSPEKTION_MONAT | int | Monatsangabe [1-12] |
| ZEITINSPEKTION_JAHR | int | Jahresangabe [0-99] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-status-zeitinspektionsdatum-lesen"></a>
### STATUS_ZEITINSPEKTIONSDATUM_LESEN

Monats- u. Jahres-Byte des Zeitinspektionsdatums aus EEPROM WortAdr. 1C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZEITINSPEKTION_MONAT | int | Monatsangabe [1-12] |
| STAT_ZEITINSPEKTION_JAHR | int | Jahresangabe [0-99] |
| STAT_SERVICE_INTERVALL | int | 0 = US, 1 = Japan, 2 = ECE |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| _ANTWORT | binary | Antworttelegramm von SG |

<a id="job-software-reset"></a>
### SOFTWARE_RESET

Kombi loest selbststaendig einen Reset aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |

<a id="job-steuern-sia-reset"></a>
### STEUERN_SIA_RESET

Ruecksetzen der Service-Intervall-Anzeige

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | moegliche Uebergabeparameter: Oel_Reset, Weg_Reset, Zeit_Reset, Liter_Reset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-gwsz-reset"></a>
### GWSZ_RESET

GWSZ zuruecksetzen, nur moeglich wenn Km-Stand &lt; 255

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |

<a id="job-status-aif-gwsz-lesen"></a>
### STATUS_AIF_GWSZ_LESEN

Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_GWSZ_WERT | long | Gesamtwegstreckenzaehler |
| STAT_GWSZ_EINH | string | Einheit des GWSZ [km] |
| KM_STATUS | string | Absoluter Kilometerstand grösser oder kleiner als 255 km |
| _ANTWORT | binary | Antworttelegramm von SG |

<a id="job-status-aif-fg-nr-lesen"></a>
### STATUS_AIF_FG_NR_LESEN

Auslesen der Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_AIF_FG_NR | string | Fahrgestellnummer |
| _ANTWORT | binary | Antworttelegramm von SG |

<a id="job-status-aif-sia-daten-lesen"></a>
### STATUS_AIF_SIA_DATEN_LESEN

Anwenderinfofeld Block 3 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_MOTORTYP_NR | int | 0 = Benzinmotor, 1 = Dieselmotor |
| STAT_MOTORTYP_TEXT | string | "Benzinmotor", "Dieselmotor" |
| STAT_GETRIEBE_NR | int | 0 = Schaltgetriebe, 1 = Automatikgetriebe, (siehe table Getriebetypen) |
| STAT_GETRIEBE_TEXT | string | "Schaltgetriebe", "Automatikgetriebe", (siehe table Getriebetypen) |
| STAT_ZEITINSPEKTION | int | keine Zeitinspektion = 0 |
| STAT_VORGEZOGENE_ZEITINSPEKTION | int | 1 wenn vorgezogene Zeitinspektion moeglich |
| STAT_INSPEKTIONSGRENZE_WERT | int | Inspektionsgrenze |
| STAT_INSPEKTIONSGRENZE_EINH | string | Einheit "Liter" |
| STAT_ZEITGRENZE_WERT | int | Zeitgrenze |
| STAT_ZEITGRENZE_EINH | string | Einheit "Tage" |
| STAT_KRAFTSTOFFMENGE_WERT | int | verbrauchte SI-Kraftstoffmenge |
| STAT_KRAFTSTOFFMENGE_EINH | string | Einheit "Liter" |
| STAT_ZEIT_INSP_ZAEHLER_WERT | int | Zeitinspektionszaehler |
| STAT_ZEIT_INSP_ZAEHLER_EINH | string | Einheit "Tage" |
| STAT_SERVICE_ART | int | Art des letzten Service: 0 = Inspektion, 1 = Oelservice |
| STAT_SERVICE_TEXT | string | "Inspektion", "Oelservice" |
| _ANTWORT | binary | Antworttelegramm von SG |

<a id="job-status-aif-tankdaten-lesen"></a>
### STATUS_AIF_TANKDATEN_LESEN

Tankdaten aus Anwenderinfofeld auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_TANKINHALT_HEBEL1_WERT | real | Tankinhalt Hebelgeber1 in Liter |
| STAT_TANKINHALT_HEBEL2_WERT | real | Tankinhalt Hebelgeber2 in Liter |
| STAT_TANKINHALT_UNGEF_WERT | real | Tankinhaltanzeige gesamt in Liter (ungefiltert) |
| STAT_TANKINHALT_GEF_WERT | real | Tankinhaltanzeige gesamt in Liter (gefiltert) |
| STAT_TANKINHALT_HEBEL1_EINH | string | Einheit Tankinhalt Hebelgeber1: "Liter" |
| STAT_TANKINHALT_HEBEL2_EINH | string | Einheit Tankinhalt Hebelgeber2: "Liter" |
| STAT_TANKINHALT_UNGEF_EINH | string | Einheit Tankanzeigewert gesamt (ungefiltert): "Liter" |
| STAT_TANKINHALT_GEF_EINH | string | Einheit Tankanzeigewert gesamt (gefiltert): "Liter" |
| STAT_RESERVE | string | Tankreserve erreicht ("EIN" oder "AUS") |

<a id="job-status-aif-aussentemp-lesen"></a>
### STATUS_AIF_AUSSENTEMP_LESEN

Tankdaten aus Anwenderinfofeld auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_AUSSENTEMP_GEF_WERT | real | Aussentemperatur in "Grad Celsius" (gefiltert) |
| STAT_AUSSENTEMP_GEF_EINH | string | Einheit Aussentemperatur: "Grad Celsius" (gefiltert) |
| STAT_AUSSENTEMP_UNGEF_WERT | real | Aussentemperatur in "Grad Celsius" (ungefiltert) |
| STAT_AUSSENTEMP_UNGEF_EINH | string | Einheit Aussentemperatur: "Grad Celsius" (ungefiltert) |

<a id="job-status-aif-datum-uhrzeit-lesen"></a>
### STATUS_AIF_DATUM_UHRZEIT_LESEN

Eingestelltes Datum und Uhrzeit aus Anwenderinfofeld auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_DATUM_UHRZEIT | string | Datum und Uhrzeit |

<a id="job-status-aif-v-kmt-dz-con-lesen"></a>
### STATUS_AIF_V_KMT_DZ_CON_LESEN

Auslesen von Fahrgeschwindigkeit, Kuehlmitteltemperatur, Drehzahl und Verbrauch aus dem Anwenderinfofeld

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_FAHRGESCHWINDIGKEIT_WERT | int | Fahrgeschwindigkeit in km/h, Aufloesung: 1 km |
| STAT_FAHRGESCHWINDIGKEIT_EINH | string | Einheit Aussentemperatur: "km/h" |
| STAT_KUEHLMITTELTEMP_WERT | int | Kuehlmitteltemperatur in "Grad Celsius" |
| STAT_KUEHLMITTELTEMP_EINH | string | Einheit Kuehlmitteltemperatur: "Grad Celsius" |
| STAT_MOTORDREHZAHL_WERT | int | DREHZAHL in "1/min" |
| STAT_MOTORDREHZAHL_EINH | string | Einheit Drehzahl: "1/min" |
| STAT_MOMENTANVERBRAUCH_WERT | real | DREHZAHL in "Liter" |
| STAT_MOMENTANVERBRAUCH_EINH | string | Einheit Verbrauch: "Liter" |

<a id="job-status-tacho-endwert-lesen"></a>
### STATUS_TACHO_ENDWERT_LESEN

Auslesen des Tacho-Endausschlags aus dem EEPROM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| STAT_TACHO_ENDWERT_CODE_WERT | string | gibt den Codierwert zum Tachoendwert als String aus |
| STAT_TACHO_ENDWERT_CODE_EINH | string | gibt die Einheit zum Tachoendwert als String aus 197 Winkelgrade = 260 km/h |
| _ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

SG - Selbsttest ausloesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |

<a id="job-steuern-anzeige"></a>
### STEUERN_ANZEIGE

Anzeigenkomponenten steuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | Zu steuernde Komponente, siehe table Komponenten moegliche Uebergabeparamter: TACHO, DREHZAHL, TANKINHALT, .                            KUEHLMITTELTEMPERATUR |
| WERT | int | Winkelgrade im Bereich von (10-195) Grad, Mit Spruengen beaufschlagt werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-steuern-piezo"></a>
### STEUERN_PIEZO

interner Piezo ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-steuern-leuchte"></a>
### STEUERN_LEUCHTE

Details zur SW-Version mit JOB_IDENT_SW auslesen. Leuchten in der Anzeigeeinheit ansteuern. Zum Aufruf 4 Parameter in Folge mit Semikolon getrennt und ohne Leerzeichen i.d. Form dez (0..255), hex (0x00..0xFF) oder bin (0y00000000..0y11111111) uebergeben. Die Belegung der Datenbytes ist separat beschrieben. 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Belegung 1. Datenbytes: (0..0xFF) Bit0: Kuehlmittelstand Bit1: Reifenluftdruck Bit2: Reifenpanne Bit3: Nebelschlussleuchte Bit4: EGS-Notprogramm Bit5: EPS Bit6: ASC_DSC Bit7: Kuehlmitteltbertemperatur |
| BYTE2 | int | Belegung 2. Datenbytes: (0..0xFF) Bit0: Check Control Bit1: Tank-Reserve Bit2: EML Bit3: E83/E85 SW&lt;=7.1  --&gt; nicht belegt, Reserve 1 .             SW&gt;=7.52 --&gt; Tueren-/Klappenstatus Bit4: E83              --&gt; nicht belegt, Reserve 2 .         E85 SW&gt;=7.1  --&gt; DTC Bit5: Tankdeckel offen Bit6: Service Engine Soon (MIL) Bit7: Bremswarnleuchte |
| BYTE3 | int | Belegung 3. Datenbytes: (0..0xFF) Bit0: Airbag Bit1: Ladekontrolle Bit2: DBC Bit3: Fernlicht Bit4: Sicherheitsgurt Bit5: Oelstand Bit6: Bremsbelagverschleiss Bit7: Oeldruck |
| BYTE4 | int | Belegung 4. Datenbytes: (0..0xFF) Bit0: Blinker links Bit1: Blinker rechts Bit2: Nebelscheinwerfer Bit3: Tempomat Bit4: frei Bit5: frei Bit6: frei Bit7: frei |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Eingangs- und Ausgangsstati lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_OELDRUCK_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_RUECKFAHRSIGNAL_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_BREMSFLUESSIGKEIT_EIN | int | 1, wenn "TRUE" , 0, wenn "FALSE" |
| STAT_HANDBREMSE_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KUEHLMITTELSTAND_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_WASCHWASSER_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_TASTE_LINKS_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_TASTE_RECHTS_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_LSS_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KBUS_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KLR_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KL15_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_POWER_FAIL_EIN | int | 1 = TRUE bei Ausfall Versorgungsspannung |
| STAT_KL50_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_ANTWORT_SG | binary | Antworttelegramm von SG |
| STAT_DIAG_INDEX | int | Diagnose-Index |
| STAT_ANTWORT_DIAG | string | Job-Status Diagnose-Index: OKAY, ERROR_.. |
| STAT_HW_VERSION | string | alter µC (bis HW06)/ neuer µC (ab HW07) |

<a id="job-status-analog-lesen"></a>
### STATUS_ANALOG_LESEN

Spezielle analoge Eingaenge lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_HEBELGEBER1_WERT | int | AD - Kanal 1, Wert des 1. Hebelgebers (links) |
| STAT_HEBELGEBER1_EINH | string | Einheit [ADC-Wert] |
| STAT_HEBELGEBER2_WERT | int | AD - Kanal 2, Wert des 2. Hebelgebers (rechts) |
| STAT_HEBELGEBER2_EINH | string | Einheit [ADC-Wert] |
| STAT_BORDNETZSPANNUNG_WERT | int | Wert AD - Kanal 4, Wert des Bremsbelagverschleisses2 |
| STAT_BORDNETZSPANNUNG_EINH | string | Einheit [ADC-Wert] |
| STAT_AUSSENTEMP_WERT | int | Wert AD - Kanal 7, Wert der Aussen`temperatur |
| STAT_AUSSENTEMP_EINH | string | Einheit [ADC-Wert] |
| STAT_BREMSVERSCHLEISS1_WERT | int | Wert AD - Kanal 6, Wert des Bremsbelagverschleisses1 |
| STAT_BREMSVERSCHLEISS1_EINH | string | Einheit [ADC-Wert] |
| STAT_5V_WERT | int | AD - Kanal 0, 5V fixe Spannung |
| STAT_5V_EINH | string | Einheit [ADC-Wert] |
| _ANTWORT | binary | Antworttelegramm von SG |

<a id="job-ram-lesen"></a>
### RAM_LESEN

Internen RAM-Speicher auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x000-0xFFF) der Adresse ,ab der das Ram gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der Bytes (max. 32 !) die ausgelesen werden sollen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| DATEN | binary | Datenfeld |

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

EEPROM-Speicher auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x00-0x3FF) der WortAdresse ,ab der das EEPROM gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der 2-Byte-Worte (max. 16 Worte = 32 Bytes), die ausgelesen werden koennen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| DATEN | binary | Datenfeld |

<a id="job-status-kombi-verriegelt"></a>
### STATUS_KOMBI_VERRIEGELT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_VERRIEGELUNG_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |

<a id="job-c-fa-lesen"></a>
### C_FA_LESEN

Fahrzeugauftrag lesen Gueltiger Adressbereich: 0x100 - 0x1BF (384 Bytes, 192 words)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string | Daten des Fahrzeugauftrages |
| SPEICHER_STATUS | string | BELEGT bzw. UNBELEGT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-fa-auftrag"></a>
### C_FA_AUFTRAG

Fahrzeugauftrag schreiben Fahrzeugauftrag lesen Gueltiger Adressbereich: 0x100 - 0x1BF (384 Bytes)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-s-auftrag"></a>
### C_S_AUFTRAG

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-s-schreiben"></a>
### C_S_SCHREIBEN

Codierdaten schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-s-lesen"></a>
### C_S_LESEN

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Auslesen der Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| FG_NR | string | Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-c-checksum"></a>
### C_CHECKSUM

Berechnung und Speicherung der Checksumme

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CHECKSUM | binary | berechnete Checksumme |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-steuern-bremslicht"></a>
### STEUERN_BREMSLICHT

Steuern des Bremslichtes ueber Diagnose Nach Ausfuehren des Jobs wird das Bremslicht ueber K-Line im Lichtschaltzentrum angesteuert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (76 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FORTTEXTE](#table-forttexte) (27 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [SIARESET](#table-siareset) (4 × 2)
- [FARTTEXTE](#table-farttexte) (8 × 2)
- [FARTTEXTEERWEITERT_AIRBAG](#table-farttexteerweitert-airbag) (5 × 3)
- [GETRIEBETYPEN](#table-getriebetypen) (4 × 2)
- [GANGINFO](#table-ganginfo) (11 × 2)
- [PROGRAMMINFO](#table-programminfo) (7 × 2)
- [KOMPONENTEN](#table-komponenten) (5 × 2)
- [OELINFO](#table-oelinfo) (7 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)

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

Dimensions: 76 rows × 2 columns

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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 27 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x11 | Oelstandssensor defekt |
| 0x20 | Airbag |
| 0x21 | SMG |
| 0x83 | Tacho A |
| 0x87 | K-Bus |
| 0x8C | Klemme R |
| 0x8F | Ueberspannung (U&gt;16V) |
| 0xBB | KOMBI-EEPROM Checksumme 2 falsch |
| 0xBE | Lichtmodul-EEPROM-Fehler |
| 0xBF | KOMBI-EEPROM Checksumme 1 falsch, Codierung unvollstaendig |
| 0xC1 | Signal TWEG+ (Tacho) |
| 0xC7 | Tank-Hebelgeber_links |
| 0xCE | Aussentemperatur |
| 0xCF | SIA-Zaehlerstaende nicht plausibel |
| 0xD7 | Tank-Hebelgeber_rechts |
| 0xF0 | CAN BUS OFF |
| 0xF4 | keine CAN ID |
| 0xF5 | keine CAN ID ASC1 |
| 0xF6 | keine CAN ID DME1_DDE1 |
| 0xF7 | keine CAN ID DME2_DDE2 |
| 0xF8 | keine CAN ID DME4_DDE4 |
| 0xF9 | keine CAN ID ASC3 |
| 0xFA | keine CAN ID EPS1 |
| 0xFB | keine CAN ID EGS1 |
| 0xFC | keine CAN ID SMG1 |
| 0xFD | keine CAN ID DME3_DDE3 |
| 0xFF | unbekannter Fehlerort |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-siareset"></a>
### SIARESET

Dimensions: 4 rows × 2 columns

| SELECTOR | RESET |
| --- | --- |
| OEL_RESET | 0x01 |
| WEG_RESET | 0x02 |
| ZEIT_RESET | 0x04 |
| LITER_RESET | 0x08 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 8 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen U-Batt |
| 0x02 | Kurzschluss gegen Masse |
| 0x03 | Leitungsunterbrechung |
| 0x04 | ungültiger Arbeitsbereich |
| 0x05 | Fehler momentan vorhanden |
| 0x06 | sporadischer Fehler |
| 0xFF | unbekannte Fehlerart |

<a id="table-farttexteerweitert-airbag"></a>
### FARTTEXTEERWEITERT_AIRBAG

Dimensions: 5 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xx00xxxx | 0x00 | unbekannte Fehlerart (Maske 00) |
| xx01xxxx | 0x10 | Alive-Counter steht (Maske 01) |
| xx10xxxx | 0x20 | K-Bus Telegramm 70h ausgefallen (Maske 10) |
| xx11xxxx | 0x30 | Airbag-SG sendet waehrend Betrieb 'LED ein' (Maske 11) |
| xxxxxxxx | 0x00 | -- |

<a id="table-getriebetypen"></a>
### GETRIEBETYPEN

Dimensions: 4 rows × 2 columns

| GETRIEBEART | GETRIEBETEXT |
| --- | --- |
| 0x00 | Schaltgetriebe |
| 0x02 | Automatikgetriebe |
| 0x03 | SMG Getriebe |
| 0xFF | unbekannte Getriebeart |

<a id="table-ganginfo"></a>
### GANGINFO

Dimensions: 11 rows × 2 columns

| GANGINFO | GANGTEXT |
| --- | --- |
| 0x01 | 1. Gang |
| 0x02 | 2. Gang |
| 0x03 | 3. Gang |
| 0x04 | 4. Gang |
| 0x05 | D |
| 0x06 | N |
| 0x07 | Rueckwaertsgang |
| 0x08 | P |
| 0x09 | 5. Gang |
| 0x0A | 6. Gang |
| 0xFF | unbekannte Getriebeinfo |

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

<a id="table-komponenten"></a>
### KOMPONENTEN

Dimensions: 5 rows × 2 columns

| ORT | BYTE |
| --- | --- |
| TACHO | 0x0A |
| DREHZAHL | 0x0B |
| TANKINHALT | 0x0C |
| KUEHLMITTELTEMPERATUR | 0x0D |
| unbekannt | 0xFF |

<a id="table-oelinfo"></a>
### OELINFO

Dimensions: 7 rows × 2 columns

| MASKE | INFOTEXT |
| --- | --- |
| 0x00 | Oelsensor i.O. |
| 0x01 | Oel unter Normalstand |
| 0x02 | Oelniveau Minimum |
| 0x03 | Oelniveau Minimum |
| 0x04 | Oelsensor defekt |
| 0x05 | Oelniveau i.O. |
| 0xFF | unbekannte Oelinfo |

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
