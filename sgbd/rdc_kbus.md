# rdc_kbus.prg

- Jobs: [33](#jobs)
- Tables: [15](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Reifendruck Control (RDC)  |
| ORIGIN | BMW TI-431 Weber |
| REVISION | 2.001 |
| AUTHOR | Beru_Electronics_GmbH BES Rapp, 3SOFT - Knop, IVM_Automotive_GmbH IE12 Trinkberger, BMW TI-431 Weber |
| COMMENT | RDC-SGBD fuer E83, E85, R52 |
| PACKAGE | 1.03 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [POWER_DOWN_MODE](#job-power-down-mode) - Versetzt das SG in den Power Down Mode
- [INIT_EEPROM](#job-init-eeprom) - Init - Datensatz ins EEProm laden !!!Nach Ausfuehrung macht das RDC einen Reset!!!
- [IDENT_SCHREIBEN](#job-ident-schreiben) - Beschreiben der Ident-Daten (nur Herstelldatum) fuer RDC
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen der Herstelldaten
- [HERSTELLDATEN_SCHREIBEN](#job-herstelldaten-schreiben) - Beschreiben der Herstelldaten
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten
- [CODIERUNG_SCHREIBEN](#job-codierung-schreiben) - Beschreiben der Codierdaten
- [STEUERN_DIGITAL](#job-steuern-digital) - Aktiviert/Deaktiviert spezielle Dienste (Set == 1)  && ( Reset == 0 ) =&gt; Set (Set == 0)  && ( Reset == 1 ) =&gt; Reset
- [STATUS_HS_INAKTIVEREIGNIS1_LESEN](#job-status-hs-inaktivereignis1-lesen) - Auslesen eines Inaktiveignisses des Historienspeichers
- [STATUS_HS_INAKTIVEREIGNIS2_LESEN](#job-status-hs-inaktivereignis2-lesen) - Auslesen eines Inaktiveignisses des Historienspeichers
- [STATUS_HS_KALIBRIEREREIGNIS1_LESEN](#job-status-hs-kalibrierereignis1-lesen) - Auslesen eines Kalibrierereignisses des Historienspeichers
- [STATUS_HS_KALIBRIEREREIGNIS2_LESEN](#job-status-hs-kalibrierereignis2-lesen) - Auslesen eines Kalibrierereignisses des Historienspeichers
- [STATUS_HS_WARNEREIGNIS1_LESEN](#job-status-hs-warnereignis1-lesen) - Auslesen eines Pannenereignisses des Historienspeichers
- [STATUS_HS_WARNEREIGNIS2_LESEN](#job-status-hs-warnereignis2-lesen) - Auslesen eines Pannenereignisses des Historienspeichers
- [STATUS_HS_WARNUNGSZAEHLER_LESEN](#job-status-hs-warnungszaehler-lesen) - Auslesen der Warnungszaehler des Historienspeichers
- [STATUS_MESSDATEN_BLOCK1_LESEN](#job-status-messdaten-block1-lesen) - Auslesen der Rad-Daten
- [STATUS_MESSDATEN_BLOCK2_LESEN](#job-status-messdaten-block2-lesen) - Auslesen der Rad-Daten
- [STATUS_MESSDATEN_BLOCK3_LESEN](#job-status-messdaten-block3-lesen) - Auslesen der Rad-Daten
- [STATUS_MESSDATEN_BLOCK4_LESEN](#job-status-messdaten-block4-lesen) - Auslesen der Rad-Daten
- [STATUS_MESSDATEN_BLOCK5_LESEN](#job-status-messdaten-block5-lesen) - Auslesen der Rad-Daten
- [STEUERN_RADELEKTRONIK_VORGEBEN](#job-steuern-radelektronik-vorgeben) - Beschreiben der Rad-Kennung
- [STATUS_IO_LESEN](#job-status-io-lesen) - Auslesen der Statusbytes
- [_FS_LESEN_OHNE_AUSB](#job-fs-lesen-ohne-ausb) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

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
| TELEGRAMM | binary | Antworttelegramm |

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

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FEHLER_ANZAHL | int | Anzahl der Fehler im Fehlerspeicher |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Fehlerort momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Verlernzaehler Bereich: 0 - 31 |
| F_ART_ANZ | int | Anzahl der Fehlerarten Bereich: immer 1 |
| F_ART1_NR | int | Index der 1. (einzigen) Fehlerart Bereich: 0, 1 |
| F_ART1_TEXT | string | 1. (einzige) Fehlerart als Text table FArtTexte ARTTEXT |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Bereich: immer 1 |
| F_UW_SATZ | int | Anzahl der Umweltsaetze Bereich: immer 1 |
| F_UW1_NR | int | Index der 1. (einzigen) Umweltbedingung Bereich: 0, 1 |
| F_UW1_TEXT | string | 1. (einzige) Umweltbedingung als Text |
| F_UW1_WERT | int | Wert der 1. (einzigen) Umweltbedingung |
| F_UW1_EINH | string | Einheit der 1. (einzigen) Umweltbedingung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-power-down-mode"></a>
### POWER_DOWN_MODE

Versetzt das SG in den Power Down Mode

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WARTEZEIT | int | Zeit in 500ms Schritten Zeitintervall 2..20 Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-init-eeprom"></a>
### INIT_EEPROM

Init - Datensatz ins EEProm laden !!!Nach Ausfuehrung macht das RDC einen Reset!!!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-schreiben"></a>
### IDENT_SCHREIBEN

Beschreiben der Ident-Daten (nur Herstelldatum) fuer RDC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ID_DATUM_KW | int | Herstelldatum KW Eingabeformat: Dezimal Wertebereich:  1 ... 53 Beispiel:      fuer KW15 ist 15 einzugeben |
| ID_DATUM_JAHR | int | Herstelldatum Jahr Eingabeformat: Dezimal Wertebereich:  0 ... 99 Beispiel:      fuer Jahr 2028 ist 28 einzugeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | int | Speichersegmente HCS12 Mikrocontroller gueltige Bereiche : 0x00 bis 0x0A Bereich: 0x00 Registerbank ( Adresse 0x3000 .. 0x329F ) Bereich: 0x01 RAM          ( Adresse 0x0000 .. 0x1FFF ) Bereich: 0x02 EEPROM       ( Adresse 0x3800 .. 0x3FFF ) Adresse in den Flash Pages ( Adresse 0x8000 .. 0xBFFF ) Bereich: 0x03 FLASH Page 0x38 Bereich: 0x04 FLASH Page 0x39 Bereiche 0x05 bis Bereich: 0x0A FLASH Page 0x3F |
| ADRESSE | long | Speicheradresse Bereich: 0x0000-0xFFFF |
| ANZAHL | int | Anzahl der Daten Bereich: 1 bis 16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DATEN | binary | ausgelesene Hex-Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Auslesen der Herstelldaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE4 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE5 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE6 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE7 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE8 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE9 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstelldaten-schreiben"></a>
### HERSTELLDATEN_SCHREIBEN

Beschreiben der Herstelldaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bereich: 0-9 bzw. 0x00-0x09 |
| BYTE2 | int | Bereich: 0-9 bzw. 0x00-0x09 |
| BYTE3 | int | Bereich: 0-9 bzw. 0x00-0x09 |
| BYTE4 | int | Bereich: 0-9 bzw. 0x00-0x09 |
| BYTE5 | int | Bereich: 0-9 bzw. 0x00-0x09 |
| BYTE6 | int | Bereich: 0-9 bzw. 0x00-0x09 |
| BYTE7 | int | Bereich: 0-9 bzw. 0x00-0x09 |
| BYTE8 | int | Bereich: 0-9 bzw. 0x00-0x09 |
| BYTE9 | int | Bereich: 0-9 bzw. 0x00-0x09 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AREACODE | int | Gebiet Wertebereich: 0 =&gt; RDW / 1 =&gt; USA |
| STAT_REIFENTYP | int | Reifentyp Wertebereich: 0 =&gt; Standard Load / 1 =&gt; Extra Load |
| STAT_FREQVARIANTE | int | Frequenzvariante Wertebereich: 0 =&gt; 433MHz / 2 =&gt; 315MHz |
| STAT_MDOFFSET | real | Offset auf Mindestdruck Wertebereich: 0 bis 60 (x 0,025 bar =&gt; entspricht 0 bis 1,5 bar) |
| STAT_MDOFFSET_EINH | string | Einheit fuer Offset des Mindestdruck |
| STAT_BAUREIHE | int | Baureihe Wertebereich: 0 =&gt; E83, E85, R52 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierung-schreiben"></a>
### CODIERUNG_SCHREIBEN

Beschreiben der Codierdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AREACODE | int | Gebiet Wertebereich: 0 =&gt; RDW / 1 =&gt; USA |
| REIFENTYP | int | Reifentyp Wertebereich: 0 =&gt; Standard Load / 1 =&gt; Extra Load |
| FREQUENZVARIANTE | int | Frequenzvariante Wertebereich: 0 =&gt; 433MHz / 2 =&gt; 315MHz |
| MDOFFSET | int | Offset auf Mindestdruck Wertebereich: 0 bis 60 (x 0,025 bar =&gt; entspricht 0 bis 1,5 bar) |
| BAUREIHE | int | Baureihe Wertebereich: 0 =&gt; E83, E85, R52 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Aktiviert/Deaktiviert spezielle Dienste (Set == 1)  && ( Reset == 0 ) =&gt; Set (Set == 0)  && ( Reset == 1 ) =&gt; Reset

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_BANDMODE | unsigned char | 0: Bandmode unveraendert 1: Bandmode setzen |
| RESET_BANDMODE | unsigned char | 0: Bandmode unveraendert 1: Bandmode ruecksetzen |
| SET_ER_FAHRT | unsigned char | 0: Eigenraderkennung bei Fahrt unveraendert 1: Eigenraderkennung bei Fahrt setzen |
| RESET_ER_FAHRT | unsigned char | 0: Eigenraderkennung bei Fahrt unveraendert 1: Eigenraderkennung bei Fahrt ruecksetzen |
| SET_ER_STAND | unsigned char | 0: Eigenraderkennung im Stand unveraendert 1: Eigenraderkennung im Stand setzen |
| RESET_ER_STAND | unsigned char | 0: Eigenraderkennung im Stand unveraendert 1: Eigenraderkennung im Stand ruecksetzen |
| SET_CAL_REQUEST | unsigned char | 0: Kalibrieranforderung unveraendert 1: Kalibrieranforderung setzen |
| RESET_CAL_REQUEST | unsigned char | 0: Kalibrieranforderung unveraendert 1: Kalibrieranforderung ruecksetzen |
| SET_TEST_ER_FAHRT | unsigned char | 0: Empfang der Eigenraeder waehrend der Fahrt pruefen unveraendert 1: Empfang der Eigenraeder waehrend der Fahrt pruefen setzen |
| RESET_TEST_ER_FAHRT | unsigned char | 0: Empfang der Eigenraeder waehrend der Fahrt pruefen unveraendert 1: Empfang der Eigenraeder waehrend der Fahrt pruefen ruecksetzen |
| SET_RDCBUS_DIAG | unsigned char | 0: Stromdiagnose LIN-Teilnehmer unveraendert 1: Stromdiagnose LIN-Teilnehmer setzen |
| RESET_RDCBUS_DIAG | unsigned char | 0: Stromdiagnose LIN-Teilnehmer unveraendert 1: Stromdiagnose LIN-Teilnehmer ruecksetzen |
| SET_SOLLDRUCK_UEBERNEHMEN | unsigned char | 0: Solldruck unveraendert 1: Solldruckuebernahme setzen |
| RESET_SOLLDRUCK_UEBERNEHMEN | unsigned char | 0: Solldruck unveraendert 1: Solldruckuebernahme ruecksetzen |
| SET_TEST_ER_STAND | unsigned char | 0: Empfang der Eigenraeder im Stand pruefen unveraendert 1: Empfang der Eigenraeder im Stand pruefen setzen |
| RESET_TEST_ER_STAND | unsigned char | 0: Empfang der Eigenraeder im Stand pruefen unveraendert 1: Empfang der Eigenraeder im Stand pruefen ruecksetzen |
| SET_TASTER | unsigned char | 0: Reset-Taster unveraendert 1: Reset-Taster gedrückt |
| RESET_TASTER | unsigned char | 0: Reset-Taster unveraendert 1: Reset-Taster nicht gedrückt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-inaktivereignis1-lesen"></a>
### STATUS_HS_INAKTIVEREIGNIS1_LESEN

Auslesen eines Inaktiveignisses des Historienspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) |
| STAT_DATUM_EINH | string | JJ.MM.TT |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_HF_UEBERDECKUNG | unsigned char | HF Ueberdeckung |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_INTERNER_FEHLERCODE | int | SG-interner Fehlercode |
| STAT_FEHLERCODE | int | Fehlercode BMW |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Grad C |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |
| _TEL_AN_SG_1 | binary | Hex-Auftrag an SG (Teil 1) |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG (Teil 1) |
| _TEL_AN_SG_2 | binary | Hex-Auftrag an SG (Teil 2) |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG (Teil 2) |

<a id="job-status-hs-inaktivereignis2-lesen"></a>
### STATUS_HS_INAKTIVEREIGNIS2_LESEN

Auslesen eines Inaktiveignisses des Historienspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) |
| STAT_DATUM_EINH | string | JJ.MM.TT |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_HF_UEBERDECKUNG | unsigned char | HF Ueberdeckung |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_INTERNER_FEHLERCODE | int | SG-interner Fehlercode |
| STAT_FEHLERCODE | int | Fehlercode BMW |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Grad C |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |
| _TEL_AN_SG_1 | binary | Hex-Auftrag an SG (Teil 1) |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG (Teil 1) |
| _TEL_AN_SG_2 | binary | Hex-Auftrag an SG (Teil 2) |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG (Teil 2) |

<a id="job-status-hs-kalibrierereignis1-lesen"></a>
### STATUS_HS_KALIBRIEREREIGNIS1_LESEN

Auslesen eines Kalibrierereignisses des Historienspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) |
| STAT_DATUM_EINH | string | JJ.MM.TT |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Grad C |
| STAT_RADID_RE0 | unsigned long | ID der Radelektronik auf Listenplatz 0 |
| STAT_RADPOS_RE0 | string | Radposition |
| STAT_RADELEKTRONIK_STATUS_RE0 | unsigned int | Radelektronik-Status der RE0 |
| STAT_SOLLDRUCKWERT_RE0_WERT | real | Solldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE0_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE0_WERT | char | Bezugstemperatur fuer Solldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE0_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE0 | int | Restlebensdauer der Radelektronik RE0 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RADID_RE1 | unsigned long | ID der Radelektronik auf Listenplatz 1 |
| STAT_RADPOS_RE1 | string | Radposition |
| STAT_RADELEKTRONIK_STATUS_RE1 | unsigned int | Radelektronik-Status der RE1 |
| STAT_SOLLDRUCKWERT_RE1_WERT | real | Solldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE1_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE1_WERT | char | Bezugstemperatur fuer Solldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE1_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE1 | int | Restlebensdauer der Radelektronik RE1 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RADID_RE2 | unsigned long | ID der Radelektronik auf Listenplatz 2 |
| STAT_RADPOS_RE2 | string | Radposition |
| STAT_RADELEKTRONIK_STATUS_RE2 | unsigned int | Radelektronik-Status der RE2 |
| STAT_SOLLDRUCKWERT_RE2_WERT | real | Solldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE2_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE2_WERT | char | Bezugstemperatur fuer Solldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE2_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE2 | int | Restlebensdauer der Radelektronik RE2 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RADID_RE3 | unsigned long | ID der Radelektronik auf Listenplatz 3 |
| STAT_RADPOS_RE3 | string | Radposition |
| STAT_RADELEKTRONIK_STATUS_RE3 | unsigned int | Radelektronik-Status der RE3 |
| STAT_SOLLDRUCKWERT_RE3_WERT | real | Solldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE3_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE3_WERT | char | Bezugstemperatur fuer Solldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE3_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE3 | int | Restlebensdauer der Radelektronik RE3 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |
| _TEL_AN_SG_1 | binary | Hex-Auftrag an SG (Teil 1) |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG (Teil 1) |
| _TEL_AN_SG_2 | binary | Hex-Auftrag an SG (Teil 2) |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG (Teil 2) |
| _TEL_AN_SG_3 | binary | Hex-Auftrag an SG (Teil 3) |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG (Teil 3) |
| _TEL_AN_SG_4 | binary | Hex-Auftrag an SG (Teil 4) |
| _TEL_ANTWORT_4 | binary | Hex-Antwort von SG (Teil 4) |

<a id="job-status-hs-kalibrierereignis2-lesen"></a>
### STATUS_HS_KALIBRIEREREIGNIS2_LESEN

Auslesen eines Kalibrierereignisses des Historienspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) |
| STAT_DATUM_EINH | string | JJ.MM.TT |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Grad C |
| STAT_RADID_RE0 | unsigned long | ID der Radelektronik auf Listenplatz 0 |
| STAT_RADPOS_RE0 | string | Radposition |
| STAT_RADELEKTRONIK_STATUS_RE0 | unsigned int | Radelektronik-Status der RE0 |
| STAT_SOLLDRUCKWERT_RE0_WERT | real | Solldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE0_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE0_WERT | char | Bezugstemperatur fuer Solldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE0_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE0 | int | Restlebensdauer der Radelektronik RE0 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RADID_RE1 | unsigned long | ID der Radelektronik auf Listenplatz 1 |
| STAT_RADPOS_RE1 | string | Radposition |
| STAT_RADELEKTRONIK_STATUS_RE1 | unsigned int | Radelektronik-Status der RE1 |
| STAT_SOLLDRUCKWERT_RE1_WERT | real | Solldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE1_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE1_WERT | char | Bezugstemperatur fuer Solldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE1_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE1 | int | Restlebensdauer der Radelektronik RE1 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RADID_RE2 | unsigned long | ID der Radelektronik auf Listenplatz 2 |
| STAT_RADPOS_RE2 | string | Radposition |
| STAT_RADELEKTRONIK_STATUS_RE2 | unsigned int | Radelektronik-Status der RE2 |
| STAT_SOLLDRUCKWERT_RE2_WERT | real | Solldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE2_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE2_WERT | char | Bezugstemperatur fuer Solldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE2_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE2 | int | Restlebensdauer der Radelektronik RE2 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RADID_RE3 | unsigned long | ID der Radelektronik auf Listenplatz 3 |
| STAT_RADPOS_RE3 | string | Radposition |
| STAT_RADELEKTRONIK_STATUS_RE3 | unsigned int | Radelektronik-Status der RE3 |
| STAT_SOLLDRUCKWERT_RE3_WERT | real | Solldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE3_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE3_WERT | char | Bezugstemperatur fuer Solldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE3_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE3 | int | Restlebensdauer der Radelektronik RE3 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |
| _TEL_AN_SG_1 | binary | Hex-Auftrag an SG (Teil 1) |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG (Teil 1) |
| _TEL_AN_SG_2 | binary | Hex-Auftrag an SG (Teil 2) |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG (Teil 2) |
| _TEL_AN_SG_3 | binary | Hex-Auftrag an SG (Teil 3) |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG (Teil 3) |
| _TEL_AN_SG_4 | binary | Hex-Auftrag an SG (Teil 4) |
| _TEL_ANTWORT_4 | binary | Hex-Antwort von SG (Teil 4) |

<a id="job-status-hs-warnereignis1-lesen"></a>
### STATUS_HS_WARNEREIGNIS1_LESEN

Auslesen eines Pannenereignisses des Historienspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) |
| STAT_DATUM_EINH | string | JJ.MM.TT |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Grad C |
| STAT_RADID_RE0 | unsigned long | ID der Radelektronik auf Listenplatz 0 |
| STAT_REIFENDRUCKWERT_RE0_WERT | real | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE0_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE0_WERT | char | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE0 | int | Radelektronik-Status der RE0 |
| STAT_RADPOS_RE0 | string | Radposition |
| STAT_SOLLDRUCKWERT_RE0_WERT | real | Solldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE0_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE0_WERT | char | Bezugstemperatur fuer Solldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE0_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE0 | int | Restlebensdauer der Radelektronik RE0 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RADID_RE1 | unsigned long | ID der Radelektronik auf Listenplatz 1 |
| STAT_REIFENDRUCKWERT_RE1_WERT | real | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE1_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE1_WERT | char | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE1 | int | Radelektronik-Status der RE1 |
| STAT_RADPOS_RE1 | string | Radposition |
| STAT_SOLLDRUCKWERT_RE1_WERT | real | Solldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE1_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE1_WERT | char | Bezugstemperatur fuer Solldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE1_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE1 | int | Restlebensdauer der Radelektronik RE1 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RADID_RE2 | unsigned long | ID der Radelektronik auf Listenplatz 2 |
| STAT_REIFENDRUCKWERT_RE2_WERT | real | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE2_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE2_WERT | char | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE2 | int | Radelektronik-Status der RE2 |
| STAT_RADPOS_RE2 | string | Radposition |
| STAT_SOLLDRUCKWERT_RE2_WERT | real | Solldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE2_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE2_WERT | char | Bezugstemperatur fuer Solldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE2_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE2 | int | Restlebensdauer der Radelektronik RE2 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RADID_RE3 | unsigned long | ID der Radelektronik auf Listenplatz 3 |
| STAT_REIFENDRUCKWERT_RE3_WERT | real | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE3_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE3_WERT | char | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE3 | int | Radelektronik-Status der RE3 |
| STAT_RADPOS_RE3 | string | Radposition |
| STAT_SOLLDRUCKWERT_RE3_WERT | real | Solldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE3_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE3_WERT | char | Bezugstemperatur fuer Solldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE3_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE3 | int | Restlebensdauer der Radelektronik RE3 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |
| _TEL_AN_SG_1 | binary | Hex-Auftrag an SG (Teil 1) |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG (Teil 1) |
| _TEL_AN_SG_2 | binary | Hex-Auftrag an SG (Teil 2) |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG (Teil 2) |
| _TEL_AN_SG_3 | binary | Hex-Auftrag an SG (Teil 3) |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG (Teil 3) |
| _TEL_AN_SG_4 | binary | Hex-Auftrag an SG (Teil 4) |
| _TEL_ANTWORT_4 | binary | Hex-Antwort von SG (Teil 4) |
| _TEL_AN_SG_5 | binary | Hex-Auftrag an SG (Teil 5) |
| _TEL_ANTWORT_5 | binary | Hex-Antwort von SG (Teil 5) |

<a id="job-status-hs-warnereignis2-lesen"></a>
### STATUS_HS_WARNEREIGNIS2_LESEN

Auslesen eines Pannenereignisses des Historienspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) |
| STAT_DATUM_EINH | string | JJ.MM.TT |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Grad C |
| STAT_RADID_RE0 | unsigned long | ID der Radelektronik auf Listenplatz 0 |
| STAT_REIFENDRUCKWERT_RE0_WERT | real | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE0_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE0_WERT | char | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE0 | int | Radelektronik-Status der RE0 |
| STAT_RADPOS_RE0 | string | Radposition |
| STAT_SOLLDRUCKWERT_RE0_WERT | real | Solldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE0_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE0_WERT | char | Bezugstemperatur fuer Solldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE0_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE0 | int | Restlebensdauer der Radelektronik RE0 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RADID_RE1 | unsigned long | ID der Radelektronik auf Listenplatz 1 |
| STAT_REIFENDRUCKWERT_RE1_WERT | real | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE1_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE1_WERT | char | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE1 | int | Radelektronik-Status der RE1 |
| STAT_RADPOS_RE1 | string | Radposition |
| STAT_SOLLDRUCKWERT_RE1_WERT | real | Solldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE1_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE1_WERT | char | Bezugstemperatur fuer Solldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE1_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE1 | int | Restlebensdauer der Radelektronik RE1 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RADID_RE2 | unsigned long | ID der Radelektronik auf Listenplatz 2 |
| STAT_REIFENDRUCKWERT_RE2_WERT | real | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE2_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE2_WERT | char | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE2 | int | Radelektronik-Status der RE2 |
| STAT_RADPOS_RE2 | string | Radposition |
| STAT_SOLLDRUCKWERT_RE2_WERT | real | Solldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE2_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE2_WERT | char | Bezugstemperatur fuer Solldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE2_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE2 | int | Restlebensdauer der Radelektronik RE2 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RADID_RE3 | unsigned long | ID der Radelektronik auf Listenplatz 3 |
| STAT_REIFENDRUCKWERT_RE3_WERT | real | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE3_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE3_WERT | char | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE3 | int | Radelektronik-Status der RE3 |
| STAT_RADPOS_RE3 | string | Radposition |
| STAT_SOLLDRUCKWERT_RE3_WERT | real | Solldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE3_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE3_WERT | char | Bezugstemperatur fuer Solldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE3_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE3 | int | Restlebensdauer der Radelektronik RE3 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |
| _TEL_AN_SG_1 | binary | Hex-Auftrag an SG (Teil 1) |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG (Teil 1) |
| _TEL_AN_SG_2 | binary | Hex-Auftrag an SG (Teil 2) |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG (Teil 2) |
| _TEL_AN_SG_3 | binary | Hex-Auftrag an SG (Teil 3) |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG (Teil 3) |
| _TEL_AN_SG_4 | binary | Hex-Auftrag an SG (Teil 4) |
| _TEL_ANTWORT_4 | binary | Hex-Antwort von SG (Teil 4) |
| _TEL_AN_SG_5 | binary | Hex-Auftrag an SG (Teil 5) |
| _TEL_ANTWORT_5 | binary | Hex-Antwort von SG (Teil 5) |

<a id="job-status-hs-warnungszaehler-lesen"></a>
### STATUS_HS_WARNUNGSZAEHLER_LESEN

Auslesen der Warnungszaehler des Historienspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZAEHLER_HARTE_WARNUNG_VL | int | Zaehler der harten Warnungen vorne links |
| STAT_ZAEHLER_HARTE_WARNUNG_VR | int | Zaehler der harten Warnungen vorne rechts |
| STAT_ZAEHLER_HARTE_WARNUNG_HL | int | Zaehler der harten Warnungen hinten links |
| STAT_ZAEHLER_HARTE_WARNUNG_HR | int | Zaehler der harten Warnungen hinten rechts |
| STAT_ZAEHLER_HARTE_WARNUNG_XX | int | Zaehler der harten Warnungen waehrend ER Verlust |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdaten-block1-lesen"></a>
### STATUS_MESSDATEN_BLOCK1_LESEN

Auslesen der Rad-Daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RE_IDENTIFIER | unsigned long | Radelektronik-Identifier |
| STAT_RAD_POSITION | string | Radposition |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | real | Letzter Reifendruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_LETZTER_REIFENDRUCKWERT_EINH | string | bar |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | char | Letzter Reifentemperaturwert der ID Bereich: -40 bis 120 Grad C |
| STAT_LETZTER_REIFENTEMPERATURWERT_EINH | string | Grad C |
| STAT_SOLLDRUCK_WERT | real | Solldruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_SOLLDRUCK_EINH | string | bar |
| STAT_GUTEMPFAENGE | unsigned int | Anzahl gut empfangener Telegramme der ID |
| STAT_AUSBEUTE_WERT | unsigned int | Ausbeute der ID Bereich: 0 bis 100 |
| STAT_AUSBEUTE_EINH | string | Prozent |
| STAT_RSSI_PEGEL | unsigned int | RSSI-Pegel der ID Bereich. 0 bis 255 |
| STAT_RESTLEBENSDAUER_WERT | unsigned int | Restlebensdauer der ID Bereich: 0 bis 120 Monate |
| STAT_RESTLEBENSDAUER_EINH | string | Monate |
| STAT_RADELEKTRONIK_STATUS | unsigned int | Radelektronik-Status der ID |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdaten-block2-lesen"></a>
### STATUS_MESSDATEN_BLOCK2_LESEN

Auslesen der Rad-Daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RE_IDENTIFIER | unsigned long | Radelektronik-Identifier |
| STAT_RAD_POSITION | string | Radposition |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | real | Letzter Reifendruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_LETZTER_REIFENDRUCKWERT_EINH | string | bar |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | char | Letzter Reifentemperaturwert der ID Bereich: -40 bis 120 Grad C |
| STAT_LETZTER_REIFENTEMPERATURWERT_EINH | string | Grad C |
| STAT_SOLLDRUCK_WERT | real | Solldruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_SOLLDRUCK_EINH | string | bar |
| STAT_GUTEMPFAENGE | unsigned int | Anzahl gut empfangener Telegramme der ID |
| STAT_AUSBEUTE_WERT | unsigned int | Ausbeute der ID Bereich: 0 bis 100 |
| STAT_AUSBEUTE_EINH | string | Prozent |
| STAT_RSSI_PEGEL | unsigned int | RSSI-Pegel der ID Bereich. 0 bis 255 |
| STAT_RESTLEBENSDAUER_WERT | unsigned int | Restlebensdauer der ID Bereich: 0 bis 120 Monate |
| STAT_RESTLEBENSDAUER_EINH | string | Monate |
| STAT_RADELEKTRONIK_STATUS | unsigned int | Radelektronik-Status der ID |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdaten-block3-lesen"></a>
### STATUS_MESSDATEN_BLOCK3_LESEN

Auslesen der Rad-Daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RE_IDENTIFIER | unsigned long | Radelektronik-Identifier |
| STAT_RAD_POSITION | string | Radposition |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | real | Letzter Reifendruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_LETZTER_REIFENDRUCKWERT_EINH | string | bar |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | char | Letzter Reifentemperaturwert der ID Bereich: -40 bis 120 Grad C |
| STAT_LETZTER_REIFENTEMPERATURWERT_EINH | string | Grad C |
| STAT_SOLLDRUCK_WERT | real | Solldruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_SOLLDRUCK_EINH | string | bar |
| STAT_GUTEMPFAENGE | unsigned int | Anzahl gut empfangener Telegramme der ID |
| STAT_AUSBEUTE_WERT | unsigned int | Ausbeute der ID Bereich: 0 bis 100 |
| STAT_AUSBEUTE_EINH | string | Prozent |
| STAT_RSSI_PEGEL | unsigned int | RSSI-Pegel der ID Bereich. 0 bis 255 |
| STAT_RESTLEBENSDAUER_WERT | unsigned int | Restlebensdauer der ID Bereich: 0 bis 120 Monate |
| STAT_RESTLEBENSDAUER_EINH | string | Monate |
| STAT_RADELEKTRONIK_STATUS | unsigned int | Radelektronik-Status der ID |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdaten-block4-lesen"></a>
### STATUS_MESSDATEN_BLOCK4_LESEN

Auslesen der Rad-Daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RE_IDENTIFIER | unsigned long | Radelektronik-Identifier |
| STAT_RAD_POSITION | string | Radposition |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | real | Letzter Reifendruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_LETZTER_REIFENDRUCKWERT_EINH | string | bar |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | char | Letzter Reifentemperaturwert der ID Bereich: -40 bis 120 Grad C |
| STAT_LETZTER_REIFENTEMPERATURWERT_EINH | string | Grad C |
| STAT_SOLLDRUCK_WERT | real | Solldruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_SOLLDRUCK_EINH | string | bar |
| STAT_GUTEMPFAENGE | unsigned int | Anzahl gut empfangener Telegramme der ID |
| STAT_AUSBEUTE_WERT | unsigned int | Ausbeute der ID Bereich: 0 bis 100 |
| STAT_AUSBEUTE_EINH | string | Prozent |
| STAT_RSSI_PEGEL | unsigned int | RSSI-Pegel der ID Bereich. 0 bis 255 |
| STAT_RESTLEBENSDAUER_WERT | unsigned int | Restlebensdauer der ID Bereich: 0 bis 120 Monate |
| STAT_RESTLEBENSDAUER_EINH | string | Monate |
| STAT_RADELEKTRONIK_STATUS | unsigned int | Radelektronik-Status der ID |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdaten-block5-lesen"></a>
### STATUS_MESSDATEN_BLOCK5_LESEN

Auslesen der Rad-Daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RE_IDENTIFIER | unsigned long | Radelektronik-Identifier |
| STAT_RAD_POSITION | string | Radposition |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | real | Letzter Reifendruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_LETZTER_REIFENDRUCKWERT_EINH | string | bar |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | char | Letzter Reifentemperaturwert der ID Bereich: -40 bis 120 Grad C |
| STAT_LETZTER_REIFENTEMPERATURWERT_EINH | string | Grad C |
| STAT_SOLLDRUCK_WERT | real | Solldruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_SOLLDRUCK_EINH | string | bar |
| STAT_GUTEMPFAENGE | unsigned int | Anzahl gut empfangener Telegramme der ID |
| STAT_AUSBEUTE_WERT | unsigned int | Ausbeute der ID Bereich: 0 bis 100 |
| STAT_AUSBEUTE_EINH | string | Prozent |
| STAT_RSSI_PEGEL | unsigned int | RSSI-Pegel der ID Bereich. 0 bis 255 |
| STAT_RESTLEBENSDAUER_WERT | unsigned int | Restlebensdauer der ID Bereich: 0 bis 120 Monate |
| STAT_RESTLEBENSDAUER_EINH | string | Monate |
| STAT_RADELEKTRONIK_STATUS | unsigned int | Radelektronik-Status der ID |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-radelektronik-vorgeben"></a>
### STEUERN_RADELEKTRONIK_VORGEBEN

Beschreiben der Rad-Kennung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RE_ID | string | RE-Kennung RE-Kennung = 0 bewirkt eine komplette Loeschung der ZOM (Schnellloeschung) |
| RE_POS | int | 1. Radpos 1-5  ( VL, VR, HL, HR, RR ) 2. Radpos 6-10 ( ZOM-Spaltenposition ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Auslesen der Statusbytes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EIGENRAEDER_BEKANNT | int | Alle Eigenräder sind bekannt |
| STAT_RADPOS_ER_BEKANNT | int | Radpositionen aller Eigenraeder sind bekannt |
| STAT_RADPOS_UEBERPRUEFT_BESTAETIGT | int | Alle Radpositionen sind ueberprueft und bestaetigt |
| STAT_DTC_INACTIVE | int | Aktiver Fehler mit Warnlampe im Fehlerspeicher |
| STAT_KAL_ANFORDERUNG | int | Kalibrieranforderung steht an |
| STAT_LIN_ON | int | LIN aktiv |
| STAT_RAD_ZUORDNUNG_TIMEOUT | int | Radzuordnung konnte nicht abgeschlossen werden |
| STAT_BANDMODE | int | RDC ist im Bandmode |
| STAT_ER_ERKENNUNG_STAND | int | Eigenraderkennung im Stand wurde gestartet |
| STAT_ER_ERKENNUNG_FAHRT | int | Eigenraderkennung waehrend der Fahrt wurde gestartet |
| STAT_TEST_EIGENRAD | int | Test-Eigenraderkennung waehrend der Fahrt wurde gestartet |
| STAT_BUS_DIAGNOSE | int | LIN Bus Diagnose wurde gestartet |
| STAT_ER_FAHRT_VTHRS | int | Geschwindigkeitsschwelle fuer Eigenraderkennung bei Fahrt aktiviert |
| STAT_BM_TIMEOUT_ACTIVE | int | Bandmode Timeout laeuft |
| STAT_TEST_ER_STAND | int | Test-Eigenraderkennung im Stand wurde gestartet |
| STAT_HARTE_WARNUNG_UNSPEZIFISCH | int | Harte Warnung unspezifisch |
| STAT_HARTE_WARNUNG_VL | int | Harte Warnung VL |
| STAT_HARTE_WARNUNG_VR | int | Harte Warnung VR |
| STAT_HARTE_WARNUNG_HL | int | Harte Warnung HL |
| STAT_HARTE_WARNUNG_HR | int | Harte Warnung HR |
| STAT_KL15_EIN | int | Klemme 15 Ein |
| STAT_MOTOR_LAEUFT_EIN | int | Motor dreht |
| STAT_FZG_FAEHRT | int | Fahrzeug faehrt |
| STAT_ER_ALLE_TEL_RE | int | Alle Radelektroniken erkannt |
| STAT_ER_ZUVIELE_RE | int | Zu viele Radelektroniken erkannt |
| STAT_STOERSENDER_SCI | int | Funkstoerung vorhanden |
| STAT_STOERSENDER_FF_SCI | int | Funkstoerung hat zu mehrfachen Telegrammausfaellen |
| STAT_STOERSENDER_ZEIT_SCI | int | Funkstoerung ist laenger als die erlaubte Totzeit vorhanden |
| STAT_POS_CHANGED_VL | int | RE auf der Radposition VL hat sich geaendert |
| STAT_POS_CHANGED_VR | int | RE auf der Radposition VR hat sich geaendert |
| STAT_POS_CHANGED_HL | int | RE auf der Radposition HL hat sich geaendert |
| STAT_POS_CHANGED_HR | int | RE auf der Radposition HR hat sich geaendert |
| STAT_POS_CHANGED_RR | int | RE auf der Radposition RR hat sich geaendert |
| STAT_ANT_UEBER_STROM_AKT | int | Ueberstromabschaltung aktiviert |
| STAT_ANT_UEBER_SPANN_AKT | int | Ueberspannungsabschaltung aktiviert |
| STAT_RESET_KEY_STATE | int | Zustand des Initialisierungstasters 0: Taster nicht betaetigt - 1: Taster gedrueckt |
| STAT_OVERHEAT_VL | int | Ueberhitzung vorne links |
| STAT_OVERHEAT_VR | int | Ueberhitzung vorne rechts |
| STAT_OVERHEAT_HL | int | Ueberhitzung hinten links |
| STAT_OVERHEAT_HR | int | Ueberhitzung vorne rechts |
| STAT_METROLOGY | int | Messschnittstelle CCP ein/aus |
| STAT_CCP_FREE_RUNNING | int | ASAP Free Running Mode (AFR) ein/aus |
| STAT_STAND_ALONE | int | Stand Alone Mode (SAM) ein/aus |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-ohne-ausb"></a>
### _FS_LESEN_OHNE_AUSB

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FEHLER_ANZAHL | int | Anzahl der Fehler im Fehlerspeicher |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Fehlerort momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Verlernzaehler Bereich: 0 - 31 |
| F_ART_ANZ | int | Anzahl der Fehlerarten Bereich: immer 1 |
| F_ART1_NR | int | Index der 1. (einzigen) Fehlerart Bereich: 0, 1 |
| F_ART1_TEXT | string | 1. (einzige) Fehlerart als Text table FArtTexte ARTTEXT |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Bereich: immer 1 |
| F_UW_SATZ | int | Anzahl der Umweltsaetze Bereich: immer 1 |
| F_UW1_NR | int | Index der 1. (einzigen) Umweltbedingung Bereich: 0, 1 |
| F_UW1_TEXT | string | 1. (einzige) Umweltbedingung als Text |
| F_UW1_WERT | int | Wert der 1. (einzigen) Umweltbedingung |
| F_UW1_EINH | string | Einheit der 1. (einzigen) Umweltbedingung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (100 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (3 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [FORTTEXTE](#table-forttexte) (57 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (2 × 9)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [REPOSITION](#table-reposition) (5 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 4)
- [TFORTIGNORE](#table-tfortignore) (1 × 2)

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

Dimensions: 100 rows × 2 columns

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
| 0x72 | AISIN AW CO.LTD |
| 0x73 | Shorlock |
| 0x74 | Schrader |
| 0x75 | BERU Electronics GmbH |
| 0x76 | CEL |
| 0x77 | Audio Mobil |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia Automotive GmbH |
| 0x81 | Tyco Electronics |
| 0x82 | Paragon AG |
| 0x83 | IEE S.A |
| 0x84 | TEMIC AUTOMOTIVE of NA |
| 0x85 | AKsys GmbH |
| 0x86 | META System |
| 0x87 | Hülsbeck & Fürst GmbH & Co KG |
| 0x88 | Mann & Hummel Automotive GmbH |
| 0x89 | Brose Fahrzeugteile GmbH & Co |
| 0x90 | Keihin |
| 0x91 | Vimercati S.p.A. |
| 0x92 | CRH |
| 0x93 | TPO Display Corp. |
| 0x94 | KÜSTER Automotive Control |
| 0x95 | Hitachi Automotive |
| 0x96 | Continental Automotive |
| 0x97 | TI-Automotive |
| 0x98 | Hydro |
| 0x99 | Johnson Controls |
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

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 3 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | nein |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 57 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x000 | Betriebsspannung AD-Wandler defekt |
| 0x002 | Schutzschaltung aktiv: Ueberspannung Antennen |
| 0x003 | Lernvorgang bei externer HF-Stoerung nicht moeglich |
| 0x004 | Eigenradstatus nicht erreicht |
| 0x007 | Hardwaredefekt: Speichercheck RAM |
| 0x009 | Hardwaredefekt: R/W-Check EEPROM |
| 0x00b | Hardwaredefekt: Speichercheck ROM |
| 0x00d | Hardwaredefekt: EEPROM-Fehler Kategorie A |
| 0x00f | Hardwaredefekt: EEPROM-Fehler Kategorie E |
| 0x027 | KBUS Timeout |
| 0x02a | Unterspannung Kl.30 |
| 0x02b | Ueberspannung Kl.30 |
| 0x02d | RE VL defekt: Sensorfehler |
| 0x02e | RE VL defekt: Kein Empfang |
| 0x030 | RE VR defekt: Sensorfehler |
| 0x031 | RE VR defekt: Kein Empfang |
| 0x033 | RE HL defekt: Sensorfehler |
| 0x034 | RE HL defekt: Kein Empfang |
| 0x036 | RE HR defekt: Sensorfehler |
| 0x037 | RE HR defekt: Kein Empfang |
| 0x03c | RE defekt: Sensorfehler |
| 0x03d | RE defekt: Kein Empfang |
| 0x065 | Externe HF-Stoerung |
| 0x073 | Kalibrierungszuordnung nicht moeglich |
| 0x07c | Bandmode aktiviert |
| 0x080 | Strom-Diagnose Kanal VL |
| 0x081 | Kurzschluß auf Kanal VL |
| 0x082 | TSS-Bus VL: Verbindungsaufbau gescheitert |
| 0x083 | Strom-Diagnose Kanal VR |
| 0x084 | Kurzschluß auf Kanal VR |
| 0x085 | TSS-Bus VR: Verbindungsaufbau gescheitert |
| 0x086 | Strom-Diagnose Kanal HL |
| 0x087 | Kurzschluß auf Kanal HL |
| 0x088 | TSS-Bus HL: Verbindungsaufbau gescheitert |
| 0x089 | Strom-Diagnose Kanal HR |
| 0x08a | Kurzschluß auf Kanal HR |
| 0x08b | TSS-Bus HR: Verbindungsaufbau gescheitert |
| 0x08c | Strom-Diagnose Kanal Ant |
| 0x08d | Kurzschluß auf Kanal Ant |
| 0x08e | TSS-Bus Ant: Verbindungsaufbau gescheitert |
| 0x08f | Trigger VL defekt: RAM-Fehler |
| 0x090 | Trigger VL defekt: ROM-Fehler |
| 0x095 | Trigger VR defekt: RAM-Fehler |
| 0x096 | Trigger VR defekt: ROM-Fehler |
| 0x09b | Trigger HL defekt: RAM-Fehler |
| 0x09c | Trigger HL defekt: ROM-Fehler |
| 0x0a1 | Trigger HR defekt: RAM-Fehler |
| 0x0a2 | Trigger HR defekt: ROM-Fehler |
| 0x0a7 | Digitalantenne defekt: RAM-Fehler |
| 0x0a8 | Digitalantenne defekt: ROM-Fehler |
| 0x0ad | Kanal VL: falsche Komponente |
| 0x0ae | Kanal VR: falsche Komponente |
| 0x0af | Kanal HL: falsche Komponente |
| 0x0b0 | Kanal HR: falsche Komponente |
| 0x0b1 | Kanal Digitalantenne: falsche Komponente |
| 0x0f0 | CRC HF-Telegramm n.i.O. (inkompatible Digitalantenne) |
| 0xXY | unbekannter Fehlerort |

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

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 2 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Geschwindigkeit | km/h | high | unsigned int | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0xXY | unbekannte Fehlerart |

<a id="table-reposition"></a>
### REPOSITION

Dimensions: 5 rows × 2 columns

| NAME | WERT |
| --- | --- |
| VL | 0x00 |
| VR | 0x01 |
| HL | 0x02 |
| HR | 0x03 |
| RR | 0x04 |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 4 columns

| ORT | UW_ANZ | UW_SATZ | UW1_NR |
| --- | --- | --- | --- |
| 0xFF | 0x01 | 0x01 | 0x01 |

<a id="table-tfortignore"></a>
### TFORTIGNORE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x027 | KBUS Timeout |
