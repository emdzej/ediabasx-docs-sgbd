# C_GM5.prg

- Jobs: [11](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | C_SGBD GM 5 |
| ORIGIN | BMW TI-433 Mario Spoljarec |
| REVISION | 1.05 |
| AUTHOR | BMW TI-433 Mario Spoljarec, BMW TI-433 Arnold Pollmann |
| COMMENT | Verifiziert |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer Grundmodul V automatischer Aufruf beim ersten Zugriff auf SGBD
- [IDENT](#job-ident) - Ident-Daten fuer GM V
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen des Pruefstempels und Interpretation als FG-Nummer
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Beschreiben des Pruefstempels mit der FG-Nummer
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [STATUS_DIGITAL](#job-status-digital) - Status der Digitalsignale des GM V (Ein-/Ausgaenge) Der Wertebereich ist bei fast allen Results: Bereich: 0, wenn FALSE / 1, wenn TRUE Andernfalls ist der Bereich gezielt spezifiziert.
- [STATUS_FUNKSCHLUESSEL](#job-status-funkschluessel) - Auslesen der Funkschluesseldaten aus dem internen Speicher der ZKE V
- [STATUS_KEY_MEMORY](#job-status-key-memory) - Auslesen der Nummer des Funkschluessels, mit dem zuletzt entriegelt wurde

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

Init-Job fuer Grundmodul V automatischer Aufruf beim ersten Zugriff auf SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer GM V

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR | int | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Auslesen des Pruefstempels und Interpretation als FG-Nummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| FG_NR | string | Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Beschreiben des Pruefstempels mit der FG-Nummer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status der Digitalsignale des GM V (Ein-/Ausgaenge) Der Wertebereich ist bei fast allen Results: Bereich: 0, wenn FALSE / 1, wenn TRUE Andernfalls ist der Bereich gezielt spezifiziert.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SIB | int | Eingang: Schalter Innenbeleuchtung |
| STAT_TOEHK | int | Eingang: Taster Entriegeln Heckklappe |
| STAT_TZV | int | Eingang: Taster Centerlock |
| STAT_TOEHS | int | Eingang: Taster Entriegeln Heckscheibe |
| STAT_TOEHKI | int | Eingang: Taster Entriegeln Heckklappe innen |
| STAT_HKK | int | Eingang: Heckklappen-Kontakt |
| STAT_ERHK | int | Eingang: Entriegeln Heckklappe |
| STAT_RSK | int | Eingang: Rueckstellkontakt Wischer |
| STAT_SFFA | int | Eingang: Schalter Fensterheber Fahrer auf |
| STAT_SFFZ | int | Eingang: Schalter Fensterheber Fahrer zu |
| STAT_SFBA | int | Eingang: Schalter Fensterheber Beifahrer auf |
| STAT_SFBZ | int | Eingang: Schalter Fensterheber Beifahrer zu |
| STAT_SW2 | int | Eingang: Wischerschalter 2 |
| STAT_KISI | int | Eingang: Kindersicherung Fensterheber hinten |
| STAT_MHK | int | Eingang: Motorhauben-Kontakt |
| STAT_HFK | int | Eingang: Handschuhfach-Kontakt |
| STAT_HSK | int | Eingang: Heckscheiben-Kontakt |
| STAT_INRS | int | Eingang: Innenraumschutz |
| STAT_NG | int | Eingang: Neigungsgeber |
| STAT_INRS2 | int | Eingang: Innenraumschutz 2 |
| STAT_KL_R_HW | int | Eingang: Klemme R (Hardware) |
| STAT_REE1 | int | Eingang: Reserve 1 |
| STAT_REE3 | int | Eingang: Reserve 3 |
| STAT_CS | int | Eingang: Crash-Sensor |
| STAT_KL30BTS | int | Eingang: Versorgung fuer IB, WP, MERHK und VA |
| STAT_KL30ZV | int | Eingang: Versorgung fuer Zentralverriegelung |
| STAT_KL30FHV | int | Eingang: Versorgung fuer Klemme 30 Fensterheber vorne |
| STAT_SFFHA | int | Eingang: Schalter Fensterheber Fahrer hinten auf |
| STAT_SFFHZ | int | Eingang: Schalter Fensterheber Fahrer hinten zu |
| STAT_SFBHA | int | Eingang: Schalter Fensterheber Beifahrer hinten auf |
| STAT_SFBHZ | int | Eingang: Schalter Fensterheber Beifahrer hinten zu |
| STAT_SFFHA2 | int | Eingang: Schalter 2 Fensterheber Fahrer hinten auf |
| STAT_SFFHZ2 | int | Eingang: Schalter 2 Fensterheber Fahrer hinten zu |
| STAT_SFBHA2 | int | Eingang: Schalter 2 Fensterheber Beifahrer hinten auf |
| STAT_SFBHZ2 | int | Eingang: Schalter 2 Fensterheber Beifahrer hinten zu |
| STAT_REE2 | int | Eingang: Reserve 2 |
| STAT_VRHK | int | Eingang: Verriegeln Heckklappe |
| STAT_SWA | int | Eingang: Schalter Waschen |
| STAT_SW1 | int | Eingang: Schalter Wischerstufe 1 |
| STAT_DMVR | int | Eingang: Diagnose Verriegeln |
| STAT_DMER | int | Eingang: Diagnose Entriegeln |
| STAT_DMZS | int | Eingang: Diagnose Sichern |
| STAT_DMVRFT | int | Eingang: Diagnose Verriegeln Fahrertuer |
| STAT_TKFT | int | Eingang: Tuerkontakt Fahrertuer |
| STAT_TKBT | int | Eingang: Tuerkontakt Beifahrertuer |
| STAT_TKFH | int | Eingang: Tuerkontakt Fahrertuer hinten |
| STAT_TKBH | int | Eingang: Tuerkontakt Beifahrertuer hinten |
| STAT_VRFT | int | Eingang: Verriegeln Fahrertuer |
| STAT_ERFT | int | Eingang: Entriegeln Fahrertuer |
| STAT_VRBT | int | Eingang: Verriegeln Beifahrertuer |
| STAT_ERBT | int | Eingang: Entriegeln Beifahrertuer |
| STAT_DSTDWA | int | Eingang: Diagnose Status DWA |
| STAT_FZV | int | Eingang: Funkfernbedienung Zentralverriegelung |
| STAT_DERHK | int | Eingang: Diagnose Entriegeln Heckklappe |
| STAT_DWP | int | Eingang: Diagnose Waschpumpe |
| STAT_DVA | int | Eingang: Diagnose Verbraucherabschaltung |
| STAT_DIB | int | Eingang: Diagnose Innenbeleuchtung |
| STAT_SFF | int | Schalter Fensterheber Fahrer moegliche Werte: 0=AUS, 1=AUF, 2=ZU, 3=AUTOMATIK |
| STAT_SFF_TEXT | string | Schalter Fensterheber Fahrer moegliche Texte: AUS, AUF, ZU, AUTOMATIK |
| STAT_SFB | int | Schalter Fensterheber Beifahrer moegliche Werte: 0=AUS, 1=AUF, 2=ZU, 3=AUTOMATIK |
| STAT_SFB_TEXT | string | Schalter Fensterheber Beifahrer moegliche Texte: AUS, AUF, ZU, AUTOMATIK |
| STAT_SFFH | int | Schalter Fensterheber Fahrer hinten moegliche Werte: 0=AUS, 1=AUF, 2=ZU, 3=AUTOMATIK |
| STAT_SFFH_TEXT | string | Schalter Fensterheber Fahrer hinten moegliche Texte: AUS, AUF, ZU, AUTOMATIK |
| STAT_SFBH | int | Schalter Fensterheber Beifahrer hinten moegliche Werte: 0=AUS, 1=AUF, 2=ZU, 3=AUTOMATIK |
| STAT_SFBH_TEXT | string | Schalter Fensterheber Beifahrer hinten moegliche Texte: AUS, AUF, ZU, AUTOMATIK |
| STAT_SFFH2 | int | Schalter 2 Fensterheber Fahrer hinten moegliche Werte: 0=AUS, 1=AUF, 2=ZU, 3=AUTOMATIK |
| STAT_SFFH2_TEXT | string | Schalter 2 Fensterheber Fahrer hinten moegliche Texte: AUS, AUF, ZU, AUTOMATIK |
| STAT_SFBH2 | int | Schalter 2 Fensterheber Beifahrer hinten moegliche Werte: 0=AUS, 1=AUF, 2=ZU, 3=AUTOMATIK |
| STAT_SFBH2_TEXT | string | Schalter 2 Fensterheber Beifahrer hinten moegliche Texte: AUS, AUF, ZU, AUTOMATIK |
| STAT_SW | int | Schalter Wischer moegliche Werte: 0=AUS, 1=INTERVALL, 2=STUFE1, 3=STUFE2 |
| STAT_SW_TEXT | string | Schalter Wischer moegliche Texte: AUS, INTERVALL, STUFE1, STUFE2 |
| STAT_VERFT | int | Verriegeln / Entriegeln Fahrertuer moegliche Werte: 0=RUHE, 1=VERRIEGELN, 2=ENTRIEGELN, 3=FEHLER |
| STAT_VERFT_TEXT | string | Verriegeln / Entriegeln Fahrertuer moegliche Texte: RUHE, ENTRIEGELN, VERRIEGELN, FEHLER |
| STAT_VERBT | int | Verriegeln / Entriegeln Beifahrertuer moegliche Werte: 0=RUHE, 1=VERRIEGELN, 2=ENTRIEGELN, 3=FEHLER |
| STAT_VERBT_TEXT | string | Verriegeln / Entriegeln Beifahrertuer moegliche Texte: RUHE, ENTRIEGELN, VERRIEGELN, FEHLER |
| STAT_MFFHA | int | Ausgang: Motor Fensterheber Fahrer hinten auf |
| STAT_MFFHZ | int | Ausgang: Motor Fensterheber Fahrer hinten zu |
| STAT_MFBHZ | int | Ausgang: Motor Fensterheber Beifahrer hinten zu |
| STAT_MFBHA | int | Ausgang: Motor Fensterheber Beifahrer hinten auf |
| STAT_MER | int | Ausgang: Motor Entriegeln |
| STAT_MZS | int | Ausgang: Motor Sichern |
| STAT_MVRFT | int | Ausgang: Motor Verriegeln Fahrertuer |
| STAT_REA3 | int | Ausgang: Reserve 3 |
| STAT_WI1 | int | Ausgang: Wischerrelais Stufe 1 |
| STAT_WI2 | int | Ausgang: Wischerrelais Stufe 2 |
| STAT_SRA | int | Ausgang: Relais Scheinwerferreinigung |
| STAT_RERHS | int | Ausgang: Relais Entriegeln Heckscheibe |
| STAT_SIRENE | int | Ausgang: Sirene bzw. Alarmhorn |
| STAT_DWAL | int | Ausgang: DWA-LED |
| STAT_MVR | int | Ausgang: Motor Verriegeln |
| STAT_MFFA | int | Ausgang: Motor Fensterheber Fahrer auf |
| STAT_MFFZ | int | Ausgang: Motor Fensterheber Fahrer zu |
| STAT_MFBA | int | Ausgang: Motor Fensterheber Beifahrer auf |
| STAT_MFBZ | int | Ausgang: Motor Fensterheber Beifahrer zu |
| STAT_STDWA | int | Ausgang: Status Diebstahlwarnanlage |
| STAT_ENEKS | int | Ausgang: Einklemmschutz-Versorgung aktiv |
| STAT_ENPU | int | Ausgang: Enable Pull Up |
| STAT_REA1 | int | Ausgang: Reserve 1 |
| STAT_REA2 | int | Ausgang: Reserve 2 |
| STAT_ENANGR1 | int | Ausgang: Enable Analogsignale Gruppe 1 |
| STAT_IB | int | Ausgang: Innenbeleuchtung |
| STAT_VA | int | Ausgang: Verbraucherabschaltung EIN |
| STAT_WP | int | Ausgang: Waschpumpe |
| STAT_MERHK | int | Ausgang: Motor Entriegeln Heckklappe |
| STAT_KL_R | int | K-Bus: Klemme R |
| STAT_KL15 | int | K-Bus: Klemme 15 |
| STAT_KL58 | int | K-Bus: Klemme 58 |
| STAT_EWS_FREE | int | K-Bus: EWS freigeschaltet |
| STAT_EWS_KEY | int | K-Bus: gueltiger Schluessel steckt |
| STAT_CSMODE | int | K-Bus: System im Crash-Mode |
| STAT_DIAGMOD | int | K-Bus: System im Diagnosemode |
| STAT_ZV | int | K-Bus: ZV ist verriegelt |
| STAT_ZS | int | K-Bus: ZV ist gesichert |
| STAT_SER | int | K-Bus: Selektiv entriegelt |
| STAT_WB | int | K-Bus: Crash-Warnblinken, DWA-Quittierung |
| STAT_OA | int | K-Bus: Optischer Alarm |
| STAT_ES | int | K-Bus: ZV ist entsichert |
| STAT_QFFZ | int | K-Bus: Quittierung Fensterheber Fahrer ist zu |
| STAT_QFBZ | int | K-Bus: Quittierung Fensterheber Beifahrer ist zu |
| STAT_QFFHZ | int | K-Bus: Quittierung Fensterheber Fahrer hinten ist zu |
| STAT_QFBHZ | int | K-Bus: Quittierung Fensterheber Beifahrer hinten ist zu |
| STAT_SOFTON | int | K-Bus: IB-Lampe ist an oder Ansteuerung laeuft |
| STAT_KB_FSHD | int | K-Bus: Schiebe-Hebedach-Handbedienung |
| STAT_KB_KOE | int | K-Bus: Komfortfunktion Oeffnen |
| STAT_KB_KS | int | K-Bus: Komfortfunktion Schliessen |
| STAT_FB_BAT | int | K-Bus: Fernbedien-Sender Batterie schwach |
| STAT_FB_NR | int | K-Bus: Gueltige FB-Nr. liegt vor (Personalisierung) |
| STAT_FB_SEND_L | int | K-Bus: Sender-Nr. Low-Bit, bei dem zuletzt ER-Taste gedrueckt |
| STAT_FB_SEND_H | int | K-Bus: Sender-Nr. High-Bit, bei dem zuletzt ER-Taste gedrueckt |
| STAT_FB_VR | int | K-Bus: VR-Taste gedrueckt |
| STAT_FB_ER | int | K-Bus: ER-Taste gedrueckt |
| STAT_FB_HK | int | K-Bus: HK-Taste gedrueckt |
| STAT_SEND_L | int | Eingang Funk: Sender-Nummer (Low-Bit) |
| STAT_SEND_H | int | Eingang Funk: Sender-Nummer (High-Bit) |
| STAT_FZVSIG | int | Eingang Funk: Funksignal empfangen |
| STAT_FZVKEY | int | Eingang Funk: Funkschluesselsignale empfangen |
| STAT_TASTE1 | int | Eingang Funk: Fernbedienung Taste 1 betaetigt |
| STAT_TASTE2 | int | Eingang Funk: Fernbedienung Taste 2 betaetigt |
| STAT_TASTE3 | int | Eingang Funk: Fernbedienung Taste 3 betaetigt |
| STAT_FUINIT | int | Eingang Funk: Initialisierung Funkschluessel moeglich |
| STAT_LOBAT1 | int | Eingang Funk: Schluessel Sender 1 Batterie schwach |
| STAT_LOBAT2 | int | Eingang Funk: Schluessel Sender 2 Batterie schwach |
| STAT_LOBAT3 | int | Eingang Funk: Schluessel Sender 3 Batterie schwach |
| STAT_LOBAT4 | int | Eingang Funk: Schluessel Sender 4 Batterie schwach |
| STAT_FSIB | int | Eingang Funk: FS IB-Befehl |
| STAT_FSAHK | int | Eingang Funk: Heckklappentaste Entriegeln Heckklappe |
| STAT_ZV1FS | int | Eingang Funk: ZV-Befehl entriegeln |
| STAT_ZV0FS | int | Eingang Funk: ZV-Befehl verriegeln |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-funkschluessel"></a>
### STATUS_FUNKSCHLUESSEL

Auslesen der Funkschluesseldaten aus dem internen Speicher der ZKE V

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NR_AKTUELL_CODE | int | Zahlencode der momentan eingelesenen Schluesselnummer Bereich: 0 bis 255 (Zufallszahl) Wenn der momentane Schluessel zum Fahrzeug gehoert, muss dieser Wert identisch mit einem der Werte STAT_NR_n sein. |
| STAT_NR_AKTUELL | int | momentan eingelesene Schluesselnummer Bereich: IO  (Schluessel gehoert zum FZG)      : 1 bis 4 NIO (Schluessel gehoert NICHT zum FZG): 0 |
| STAT_INIT_ANZ | int | Anzahl der initialisierten Schluessel Bereich: 0 bis 4 |
| STAT_NR_1 | int | Speicher von Schluesselnummer 1 (auf ZKE V initialisiert) Bereich: 0 bis 255 |
| STAT_NR_2 | int | Speicher von Schluesselnummer 2 (auf ZKE V initialisiert) Bereich: 0 bis 255 |
| STAT_NR_3 | int | Speicher von Schluesselnummer 3 (auf ZKE V initialisiert) Bereich: 0 bis 255 |
| STAT_NR_4 | int | Speicher von Schluesselnummer 4 (auf ZKE V initialisiert) Bereich: 0 bis 255 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-key-memory"></a>
### STATUS_KEY_MEMORY

Auslesen der Nummer des Funkschluessels, mit dem zuletzt entriegelt wurde

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NR | int | 0   : ungueltig ! (z.B.: mechanisch entriegelt) 1-4 : Nr. des Funkschluessels, mit dem entriegelt wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (7 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 7 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNKTION |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 27 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen |
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
| 0xXY | unbekannter Hersteller |
