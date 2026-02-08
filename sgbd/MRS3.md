# MRS3.prg

- Jobs: [21](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MRS3 |
| ORIGIN | BMW TI-433 Winkler H.-J. |
| REVISION | 2.08 |
| AUTHOR | BMW TI-433 Winkler |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer AIRBAG MRS3
- [IDENT](#job-ident) - Ident-Daten fuer AIRBAG MRS3
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Quicktest High-Konzept nach Lastenheft
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [SPEICHER_LESEN](#job-speicher-lesen) - Speicher lesen
- [AUSSTATTUNG_LESEN](#job-ausstattung-lesen) - Ausstattung lesen
- [HERSTELLERDATEN_LESEN](#job-herstellerdaten-lesen) - Kodierte KFZ-Herstellerdaten lesen
- [TYP_LESEN](#job-typ-lesen) - Lesen des Fahrzeugtyps (Baureihe)
- [PARAMETER_LESEN](#job-parameter-lesen) - 16 Byte aus Parametersatz 1 lesen
- [BMW_SERIENNUMMER_LESEN](#job-bmw-seriennummer-lesen) - Lesen der BMW-Seriennummer
- [STATUS_LESEN](#job-status-lesen) - Status des MRS3 lesen
- [VERRIEGELUNG_LESEN](#job-verriegelung-lesen) - Auslesen der Verriegelung (= Pruefstempel)
- [VERRIEGELUNG_SCHREIBEN](#job-verriegelung-schreiben) - Verriegelungsbytes setzen
- [CONTROLLER_RESET](#job-controller-reset) - Zuruecksetzen des Controllers
- [SG_LOGIN](#job-sg-login) - Berechtigung fuer EEPROM-Zugriffe
- [DIAGNOSE_ERHALTEN](#job-diagnose-erhalten) - Diagnose aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [AUSSTATTUNG_LESEN_EWS](#job-ausstattung-lesen-ews) - Ausstattung lesen
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Lesen des Pruefcodes, besteht aus Identifikationsdaten, Ausstattungsdaten und dem FS-Inhalt, jedes Telegrammpaket ist durch ein 0x00 abgeschlossen

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

Init-Job fuer AIRBAG MRS3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer AIRBAG MRS3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferant |
| ID_SW_NR | int | Softwarenummer |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Quicktest High-Konzept nach Lastenheft

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ANZ | int | Anzahl Fehler |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_HEX_CODE | binary | Hex-Fehlerdaten je Fehler |
| F_ORT_NR | int | identisch Fehlerbytemaske |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten (hier: immer 8) |
| F_ART1_NR | int | Index der 1. Fehlerart |
| F_ART1_TEXT | string | 1. Fehlerart als Text |
| F_ART2_NR | int | Index der 2. Fehlerart |
| F_ART2_TEXT | string | 2. Fehlerart als Text |
| F_ART3_NR | int | Index der 3. Fehlerart |
| F_ART3_TEXT | string | 3. Fehlerart als Text |
| F_ART4_NR | int | Index der 4. Fehlerart |
| F_ART4_TEXT | string | 4. Fehlerart als Text |
| F_ART5_NR | int | Index der 5. Fehlerart |
| F_ART5_TEXT | string | 5. Fehlerart als Text |
| F_ART6_NR | int | Index der 6. Fehlerart |
| F_ART6_TEXT | string | 6. Fehlerart als Text |
| F_ART7_NR | int | Index der 7. Fehlerart |
| F_ART7_TEXT | string | 7. Fehlerart als Text |
| F_ART8_NR | int | Index der 8. Fehlerart |
| F_ART8_TEXT | string | 8. Fehlerart als Text |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen (hier: immer 2) |
| F_UW_SATZ | int | Anzahl der Umweltsaetze (hier: immer 1) |
| F_UW1_NR | int | Index der 1. Umweltbedingung (hier: immer 1) |
| F_UW1_TEXT | string | Text zur 1. Umweltbedingung (hier: immer Beginnfehleruhr) |
| F_UW1_WERT | long | Wert der 1. Umweltbedingung |
| F_UW1_EINH | string | Einheit der 1. Umweltbedingung (hier: immer Sek.) |
| F_UW2_NR | int | Index der 2. Umweltbedingung (hier: immer 2) |
| F_UW2_TEXT | string | Text zur 2. Umweltbedingung (hier: immer Endefehleruhr) |
| F_UW2_WERT | long | Wert der 2. Umweltbedingung |
| F_UW2_EINH | string | Einheit der 2. Umweltbedingung (hier: immer Sek.) |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Speicher lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| H_ADR | string | Startadresse High-Byte (0x00-0xFF) |
| L_ADR | string | Startadresse Low-Byte (0x00-0xFF) |
| ANZ_BYTE | string | Anzahl der zu lesenden Bytes (&lt;=16) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Speicherinhalt |

<a id="job-ausstattung-lesen"></a>
### AUSSTATTUNG_LESEN

Ausstattung lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| BYTE_1 | int | Byte 1 der 4/5 Ausstattungsbytes |
| BYTE_2 | int | Byte 2 der 4/5 Ausstattungsbytes |
| BYTE_3 | int | Byte 3 der 4/5 Ausstattungsbytes |
| BYTE_4 | int | Byte 4 der 4/5 Ausstattungsbytes |
| BYTE_5 | int | Byte 5 der 4/5 Ausstattungsbytes -1 wenn Byte 5 nicht existent |
| AB_F_VERBAUT | int | Airbag Fahrer verbaut (ZK0) --&gt; 1 |
| GS_F_VERBAUT | int | Gurtstrammer Fahrer verbaut (ZK1) --&gt; 1 |
| GS_BF_VERBAUT | int | Gurtstrammer Beifahrer verbaut (ZK2) --&gt; 1 |
| AB_BF_VERBAUT | int | Airbag Beifahrer verbaut (ZK3) --&gt; 1 |
| AB_SEITE_VORNE_LINKS | int | Airbag Seite vorne links verbaut (ZK4) --&gt; 1 |
| AB_SEITE_VORNE_RECHTS | int | Airbag Seite vorne rechts verbaut (ZK5) --&gt; 1 |
| AB_SEITE_HINTEN_LINKS | int | Airbag Seite hinten links verbaut (ZK6) --&gt; 1 |
| AB_SEITE_HINTEN_RECHTS | int | Airbag Seite hinten rechts verbaut (ZK7) --&gt; 1 |
| AB_KOPF_VORNE_LINKS | int | Airbag Kopf vorne links verbaut (ZK8) --&gt; 1 |
| AB_KOPF_VORNE_RECHTS | int | Airbag Kopf vorne rechts verbaut (ZK9) --&gt; 1 |
| AB_BATTERIE_1 | int | Batterie-Plus-Abtrennung-1 verbaut (ZK10) --&gt; 1 |
| AB_BF2_VERBAUT | int | Airbag Beifahrer Stufe 2 verbaut (ZK11) --&gt; 1 |
| AB_F2_VERBAUT | int | Airbag Fahrer Stufe 2 verbaut (ZK12) --&gt; 1 |
| AB_KOPF_HINTEN_LINKS | int | Airbag Kopf hinten links verbaut (ZK13) --&gt; 1 |
| AB_KOPF_HINTEN_RECHTS | int | Airbag Kopf hinten rechts verbaut (ZK14) --&gt; 1 |
| AB_BATTERIE_2 | int | Batterie-Plus-Abtrennung-2 verbaut (ZK15) --&gt; 1 |
| SCHLOSS_F_VERBAUT | int | Gurtschloss Fahrer verbaut --&gt; 1 |
| SCHLOSS_BF_VERBAUT | int | Gurtschloss Beifahrer verbaut --&gt; 1 |
| SCHLOSS_STROM_VERBAUT | int | Gurtschloesser Stromschnittstelle verbaut --&gt; 1 |
| SCHLOSS_SPANNUNG_VERBAUT | int | Gurtschloesser Spannungsschnittstelle verbaut --&gt; 1 |
| FM_VERBAUT | int | Fond-Modul verbaut --&gt; 1 |
| SBE_VERBAUT | int | Sitzbelegungserkennung verbaut --&gt; 1 |
| SBE2_VERBAUT | int | Sitzbelegungserkennung 2 verbaut --&gt; 1 |
| SITZ_ERKENNUNG_VERBAUT | int | Veroderung der Results SBE_VERBAUT und SBE2_VERBAUT Notwendig ausschliesslich fuer ELDI-Job E3_SIV!!! |
| UERS_VERBAUT | int | Ueberrollsensor verbaut --&gt; 1 |
| SAT_VORNE_VERBAUT | int | Frontsatelliten verbaut --&gt; 1 |
| SAT_HINTEN_VERBAUT | int | Fondsatelliten verbaut --&gt; 1 |
| KBUS | int | K-BUS-Anbindung --&gt; 1 / D-Bus-Anbindung --&gt; 0 |
| HWL | int | Hinweisleuchte brennt bei KSE --&gt; 1 |
| ZAE2_EMULATION | int | ZAE2-Emulation aktiv --&gt; 1 |
| MRS1_EMULATION | int | MRS1-Emulation aktiv --&gt; 1 |
| TRIGGERSCHALTER_VERBAUT | int | Triggerschalter verbaut --&gt; 1 |
| US_VERSION | int | USA-Version --&gt; 1 |
| LEHNE_F_VERBAUT | int | Sitzlehnenverriegelung Fahrer verbaut --&gt; 1 |
| LEHNE_BF_VERBAUT | int | Sitzlehnenverriegelung Beifahrer verbaut --&gt; 1 |
| LINKSLENKER | int | Rechtslenker --&gt; 0, Linkslenker --&gt; 1 |

<a id="job-herstellerdaten-lesen"></a>
### HERSTELLERDATEN_LESEN

Kodierte KFZ-Herstellerdaten lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| TYP | string | Baureihe z.B: E31 / 03h , E34 / 01h ... |
| CODIERDATUM | string | z.B: 21.4.93 ... |
| WERKSKENNUNG | string | 4-stellige Dezimalzahl als String |
| HAENDLERKENNUNG | string | 5-stellige Dezimalzahl als String |
| FGNUMMER | string | Kurze Fahrgestellnummer |
| DATEN | binary | Antworttelegramm |
| DATEN1 | binary | Antworttelegramm |

<a id="job-typ-lesen"></a>
### TYP_LESEN

Lesen des Fahrzeugtyps (Baureihe)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| TYP | string | Baureihe z.B: E31 / 03h , E34 / 01h ... |

<a id="job-parameter-lesen"></a>
### PARAMETER_LESEN

16 Byte aus Parametersatz 1 lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCKNR | int | (0 &lt;= BLOCKNR &lt;= 9) --&gt; 16 Parameterbytes ab Byte (16*BLOCKNR) werden angefordert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Spezifizierte Parameterdaten |

<a id="job-bmw-seriennummer-lesen"></a>
### BMW_SERIENNUMMER_LESEN

Lesen der BMW-Seriennummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Antworttelegramm |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Status des MRS3 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_ZK0 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK1 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK2 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK3 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK4 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK5 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK6 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK7 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK8 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK9 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK10 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK11 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK12 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK13 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK14 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK15 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_SBE | int | 0 = belegt, 1 = unbelegt |
| STAT_GURTSCHLOSS_F | int | 0 = (nicht da, nicht gesteckt oder defekt), 1 = gesteckt |
| STAT_GURTSCHLOSS_BF | int | 0 = (nicht da, nicht gesteckt oder defekt), 1 = gesteckt |
| STAT_SBE_X_FEHLER | int | 0 = fehlerhaft, 1 = fehlerfrei |
| STAT_SACSR_FEHLER | int | 0 = fehlerhaft, 1 = fehlerfrei |
| STAT_SACSL_FEHLER | int | 0 = fehlerhaft, 1 = fehlerfrei |
| STAT_SBE2_KIND | int | 0 = Kindersitz, 1 = kein Kindersitz |
| STAT_SBE2_OOP | int | 0 = OOP, 1 = nicht OOP |
| STAT_F_LEHNE_NV | int | -1 = Information nicht verfuegbar 0 = Fahrerlehne verriegelt oder n.i.O. 1 = Fahrerlehne nicht verriegelt |
| STAT_F_LEHNE_V | int | -1 = Information nicht verfuegbar 0 = Fahrerlehne nicht verriegelt oder n.i.O. 1 = Fahrerlehne verriegelt |
| STAT_F_LEHNE_MODUL_FEHLER | int | -1 = Information nicht verfuegbar 0 = n.i.O., 1 = i.O. |
| STAT_F_LEHNE_SYSTEM_FEHLER | int | -1 = Information nicht verfuegbar 0 = n.i.O., 1 = i.O. |
| STAT_BF_LEHNE_NV | int | -1 = Information nicht verfuegbar 0 = Beifahrerlehne verriegelt oder n.i.O. 1 = Beifahrerlehne nicht verriegelt |
| STAT_BF_LEHNE_V | int | -1 = Information nicht verfuegbar 0 = Beifahrerlehne nicht verriegelt oder n.i.O. 1 = Beifahrerlehne verriegelt |
| STAT_BF_LEHNE_MODUL_FEHLER | int | -1 = Information nicht verfuegbar 0 = n.i.O., 1 = i.O. |
| STAT_BF_LEHNE_SYSTEM_FEHLER | int | -1 = Information nicht verfuegbar 0 = n.i.O., 1 = i.O. |

<a id="job-verriegelung-lesen"></a>
### VERRIEGELUNG_LESEN

Auslesen der Verriegelung (= Pruefstempel)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| BYTE1 | int | Datenbyte 1 |
| BYTE2 | int | Datenbyte 2 |
| BYTE3 | int | Datenbyte 3 |

<a id="job-verriegelung-schreiben"></a>
### VERRIEGELUNG_SCHREIBEN

Verriegelungsbytes setzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| ERROR_CODE | string | Bei NIO Fehlertext, sonst Leerstring |

<a id="job-controller-reset"></a>
### CONTROLLER_RESET

Zuruecksetzen des Controllers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-sg-login"></a>
### SG_LOGIN

Berechtigung fuer EEPROM-Zugriffe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-diagnose-erhalten"></a>
### DIAGNOSE_ERHALTEN

Diagnose aufrechterhalten

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

<a id="job-ausstattung-lesen-ews"></a>
### AUSSTATTUNG_LESEN_EWS

Ausstattung lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| AUSSTATTUNG | string | x Ausstattungsbytes als String |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Lesen des Pruefcodes, besteht aus Identifikationsdaten, Ausstattungsdaten und dem FS-Inhalt, jedes Telegrammpaket ist durch ein 0x00 abgeschlossen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| PRUEFCODE | binary | Daten in Hex-Format |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (6 × 2)
- [LIEFERANTEN](#table-lieferanten) (31 × 2)
- [FORTTEXTE](#table-forttexte) (50 × 2)
- [FARTMATRIX](#table-fartmatrix) (50 × 17)
- [FARTTEXTE](#table-farttexte) (28 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (2 × 3)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 6 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNKTION |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 31 rows × 2 columns

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
| 0x30 | NEC |
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 50 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Zuendkreis ZK0 -&gt; Airbag Fahrer |
| 0x02 | Zuendkreis ZK1 -&gt; Gurtstrammer Fahrer |
| 0x03 | Zuendkreis ZK2 -&gt; Gurtstrammer Beifahrer |
| 0x04 | Zuendkreis ZK3 -&gt; Airbag Beifahrer |
| 0x05 | Zuendkreis ZK4 -&gt; Seitenairbag vorne links |
| 0x06 | Zuendkreis ZK5 -&gt; Seitenairbag vorne rechts |
| 0x07 | Zuendkreis ZK6 -&gt; Seitenairbag hinten links |
| 0x08 | Zuendkreis ZK7 -&gt; Seitenairbag hinten rechts |
| 0x09 | Zuendkreis ZK8 -&gt; Kopfairbag (ITS) vorne links |
| 0x0A | Zuendkreis ZK9 -&gt; Kopfairbag (ITS) vorne rechts |
| 0x0B | Zuendkreis ZK10 -&gt; Batterie Pluspoltrennung 1 |
| 0x0C | Zuendkreis ZK11 -&gt; Airbag Beifahrer Stufe 2 |
| 0x0D | Zuendkreis ZK12 -&gt; Airbag Fahrer Stufe 2 |
| 0x0E | Zuendkreis ZK13 -&gt; Kopfairbag hinten links |
| 0x0F | Zuendkreis ZK14 -&gt; Kopfairbag hinten rechts |
| 0x10 | Zuendkreis ZK15 -&gt; Batterie Pluspoltrennung 2 |
| 0x11 | Versorgungsspannung |
| 0x12 | Fehlerlampe (AWL) |
| 0x13 | Hinweislampe (HWL) |
| 0x14 | Gurtschloss Fahrer |
| 0x15 | Gurtschloss Beifahrer |
| 0x16 | MRSA vorne links |
| 0x17 | MRSA vorne rechts |
| 0x18 | Externer Ueberrollsensor (UERS) |
| 0x19 | Sitzbelegungserkennung 2 (SBE2) |
| 0x1A | Sitzbelegungserkennung 1 (SBE1) |
| 0x1B | Crashtelegrammspeicher |
| 0x1C | Verkopplung in Zuendkreis ZK0 -&gt; Airbag Fahrer |
| 0x1D | Verkopplung in Zuendkreis ZK1 -&gt; Gurtstrammer Fahrer |
| 0x1E | Verkopplung in Zuendkreis ZK2 -&gt; Gurtstrammer Beifahrer |
| 0x1F | Verkopplung in Zuendkreis ZK3 -&gt; Airbag Beifahrer |
| 0x20 | Verkopplung in Zuendkreis ZK4 -&gt; Seitenairbag vorne links |
| 0x21 | Verkopplung in Zuendkreis ZK5 -&gt; Seitenairbag vorne rechts |
| 0x22 | Verkopplung in Zuendkreis ZK6 -&gt; Seitenairbag hinten links |
| 0x23 | Verkopplung in Zuendkreis ZK7 -&gt; Seitenairbag hinten rechts |
| 0x24 | Verkopplung in Zuendkreis ZK8 -&gt; Kopfairbag (ITS) vorne links |
| 0x25 | Verkopplung in Zuendkreis ZK9 -&gt; Kopfairbag (ITS) vorne rechts |
| 0x26 | Verkopplung in Zuendkreis ZK10 -&gt; Batterie Pluspoltrennung 1 |
| 0x27 | Verkopplung in Zuendkreis ZK11 -&gt; Airbag Beifahrer Stufe 2 |
| 0x28 | Verkopplung in Zuendkreis ZK12 -&gt; Airbag Fahrer Stufe 2 |
| 0x29 | Verkopplung in Zuendkreis ZK13 -&gt; Kopfairbag hinten links |
| 0x2A | Verkopplung in Zuendkreis ZK14 -&gt; Kopfairbag hinten rechts |
| 0x2B | Verkopplung in Zuendkreis ZK15 -&gt; Batterie Pluspoltrennung 2 |
| 0x2C | Checksumme Codierdaten |
| 0x2D | MRSA vorne (links und rechts) |
| 0x2E | Sitzlehnenverriegelung Fahrer |
| 0x2F | Sitzlehnenverriegelung Beifahrer |
| 0x30 | Sitzlehnenverriegelung K-Bus |
| 0xF0 | Interner Steuergeraetefehler |
| 0xFF | unbekannter Fehlerort |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 50 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x02 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x03 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x04 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x05 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x06 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x07 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x08 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x09 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0A | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0B | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0C | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0D | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0E | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0F | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x10 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x11 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x13 | 0x08 | 0x09 |
| 0x12 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x14 | 0xFF | 0x15 | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x13 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x14 | 0xFF | 0x15 | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x14 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0A | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x0B | 0xFF | 0x0C | 0x08 | 0x09 |
| 0x15 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0A | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x0B | 0xFF | 0x0C | 0x08 | 0x09 |
| 0x16 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x0E | 0xFF | 0x0F | 0xFF | 0x17 | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x17 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x0E | 0xFF | 0x0F | 0xFF | 0x17 | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x18 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x0E | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x19 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x0E | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x1A | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x10 | 0xFF | 0x11 | 0x08 | 0x09 |
| 0x1B | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x12 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x1C | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x1D | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x1E | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x1F | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x20 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x21 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x22 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x23 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x24 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x25 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x26 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x27 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x28 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x29 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x2A | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x2B | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x16 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x2C | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x18 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x2D | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x19 | 0xFF | 0x0F | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x2E | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x0E | 0xFF | 0x1A | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x2F | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x0E | 0xFF | 0x1A | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x30 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0xF0 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF |
| 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 28 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Plausibilitaetsfehler |
| 0x01 | Fehler zur Zeit nicht aktiv |
| 0x02 | Fehler zur Zeit aktiv |
| 0x03 | Unterbrechung |
| 0x04 | Masseschluss |
| 0x05 | Batterieschluss |
| 0x06 | Widerstand zu klein |
| 0x07 | Widerstand zu gross |
| 0x08 | Fehler ist nicht sporadisch |
| 0x09 | Fehler ist sporadisch |
| 0x0A | Widerstand nicht definiert oder Graubereich |
| 0x0B | Masseschluss / Widerstand zu klein |
| 0x0C | Batterieschluss / Unterbrechung / Widerstand zu gross |
| 0x0D | Kommunikationsfehler |
| 0x0E | Modul sendet Fehlersignal |
| 0x0F | Falsche Algorithmusparameter |
| 0x10 | Unterbrechung Sitzmatte |
| 0x11 | Kurzschluss Sitzmatte |
| 0x12 | Crashtelegramm(e) gespeichert |
| 0x13 | Unterspannung |
| 0x14 | Masseschluss / Unterbrechung |
| 0x15 | Batterieschluss / Ansteuerung defekt |
| 0x16 | Verkopplung mit einem anderen Zuendkreis |
| 0x17 | Falscher Typ |
| 0x18 | Checksummen-Fehler beim Schreiben der Daten |
| 0x19 | Unterschiedliche Typen |
| 0x1A | Mind. ein Modul inaktiv |
| 0xFF | -- |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW_ANZ | UW_SATZ | UW1_NR | UW2_NR |
| --- | --- | --- | --- | --- |
| 0xFF | 0x02 | 0x01 | 0x01 | 0x02 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 2 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x01 | Beginnfehleruhr | Sek. |
| 0x02 | Endefehleruhr | Sek. |
