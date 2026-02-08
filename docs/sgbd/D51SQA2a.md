# D51SQA2a.prg

- Jobs: [81](#jobs)
- Tables: [555](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | DDE 5.1 fuer M67 |
| ORIGIN | BMW ZM-E-33 Lexmueller |
| REVISION | 0.1 |
| AUTHOR | BMW ZM-E-33 Lexmueller |
| COMMENT | SGBD fuer DDE50/M47TUE |
| PACKAGE | 0.95 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INTERFACETYPE](#job-interfacetype) - Interface-Typ bestimmen und ausgeben Es wird der Name des Interfaces übergeben Wichtig für Baudratenumschaltung weil bei ADS, EADS und OBD sind nur 115200 Baud möglich, bei EDIC nur 125000 Baud möglich
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [DIAGNOSEPROTOKOLL_SETZEN](#job-diagnoseprotokoll-setzen) - Wählt ein Diagnoseprotokoll aus
- [DIAGNOSEPROTOKOLL_LESEN](#job-diagnoseprotokoll-lesen) - Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück
- [IDENT](#job-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [AIF_SCHREIBEN](#job-aif-schreiben) - Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [FS_LESEN_LANG](#job-fs-lesen-lang) - Auslesen des Fehlerspeichers
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [TEL_ROH](#job-tel-roh) - Rohtelegramm ohne Header lesen
- [ABGLEICH_IMA_LESEN_HEX](#job-abgleich-ima-lesen-hex) - IMA Abgleichwerte und Ausgabe im HEX Format KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier LID: $BB
- [ABGLEICH_IMA_LESEN](#job-abgleich-ima-lesen) - IMA Abgleichwerte Ausgabe zylinderspezifisch im Injektor Format KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier LID: $BB
- [ABGLEICH_PROGRAMMIEREN_IMA_HEX](#job-abgleich-programmieren-ima-hex) - Programmieren der IMA Abgleichwerte und Eingabe im HEX Format - Alle Zylinder KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier LID: $BB
- [ABGLEICH_PROGRAMMIEREN_IMA](#job-abgleich-programmieren-ima) - Programmieren der IMA Abgleichwerte und Eingabe im HEX Format - Alle Zylinder KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier LID: $BB
- [ABGLEICH_PROGRAMMIEREN_IMA_ZYL_HEX](#job-abgleich-programmieren-ima-zyl-hex) - IMA Abgleichwert Programmierrn im HEX Format KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier LID: $B5 - $B5
- [ABGLEICH_PROGRAMMIEREN_IMA_ZYL](#job-abgleich-programmieren-ima-zyl) - IMA Abgleichwert Programmierrn im Injektor aufgedruckten Format KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier LID: $B5 - $B5
- [ABGLEICH_IMA_ABGLEICHFLAG_LESEN](#job-abgleich-ima-abgleichflag-lesen) - Lesen des IMA Abgleichflags - muss 1x beschrieben sein KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier LID: $BC
- [ABGLEICH_IMA_ABGLEICHFLAG_VORGEBEN](#job-abgleich-ima-abgleichflag-vorgeben) - Vorgeben des IMA Abgleichflags - muss 1x beschrieben sein KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [ABGLEICH_IMA_ABGLEICHFLAG_PROGRAMMIEREN](#job-abgleich-ima-abgleichflag-programmieren) - Programmieren des IMA Abgleichflags - muss 1x beschrieben sein KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [FS_SELEKTIV_LOESCHEN](#job-fs-selektiv-loeschen) - Auslesen des Fehlerspeichers KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [ABGLEICH_VERSTELLEN](#job-abgleich-verstellen) - Verstellen eines EEPROM Abgleichwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [ABGLEICH_VERSTELLEN_X](#job-abgleich-verstellen-x) - Verstellen eines Abgleichwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [ABGLEICH_LESEN](#job-abgleich-lesen) - Veines Abgleichwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [ABGLEICH_LESEN_X](#job-abgleich-lesen-x) - Veines Abgleichwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [ABGLEICH_PROG](#job-abgleich-prog) - Programmieren eines Abgleichwertes mittels Kurzbezeichner aus dem EEPROM KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [ABGLEICH_PROG_X](#job-abgleich-prog-x) - Programmieren eines Abgleichwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [ABGLEICHWERTE_SCHREIBEN](#job-abgleichwerte-schreiben) - Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten
- [ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - Lesen der Motorabgleichwerte
- [ABGLEICHFLAG_SCHREIBEN](#job-abgleichflag-schreiben) - Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten
- [ABGLEICHFLAG_LESEN](#job-abgleichflag-lesen) - Lesen des EEPROM-Speichers ab Adresse 0x0032
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [STEUERN_SELECTIV](#job-steuern-selectiv) - Verstellen eines Stellerwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [STEUERN_SELECTIV_X](#job-steuern-selectiv-x) - Verstellen eines Stellerwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [STEUERN_ENDE_SELECTIV](#job-steuern-ende-selectiv) - Beenden von Verstellen eines Stellerwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [STEUERN_ENDE_SELECTIV_X](#job-steuern-ende-selectiv-x) - Beenden von Verstellen eines Stellerwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [STEUERN_WERT_LESEN_X](#job-steuern-wert-lesen-x) - Lesen des Vorgegebenen Stellerwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [STEUERN_WERT_LESEN](#job-steuern-wert-lesen) - Lesen des Vorgegebenen Stellerwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [STEUERN_ZUHEIZER](#job-steuern-zuheizer) - Vorgeben eines Stellerwertes fuer Zuheizer KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier Verstellwert 5 - 95 %
- [STEUERN_ZUHEIZER_AUS](#job-steuern-zuheizer-aus) - Beenden von Vorgeben von Zuheizer ansteuern KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - Vorgeben eines Stellerwertes fuer E - Luefter KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier Verstellwert 5 - 90 %
- [STEUERN_E_LUEFTER_AUS](#job-steuern-e-luefter-aus) - Beenden von Vorgeben von E-Luefter ansteuern KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [STEUERN_VFP](#job-steuern-vfp) - Vorgeben eines Stellerwertes fuer Vorfoerderpumpe KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier Verstellwert 5 - 95 %
- [STEUERN_VFP_AUS](#job-steuern-vfp-aus) - Beenden von Vorgeben von Vorfoerderpumpe ansteuern KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier
- [MW_SELECT_LESEN_NORM](#job-mw-select-lesen-norm) - Messwerteblock selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [MW_SELECT_LESEN_NORM2](#job-mw-select-lesen-norm2) - Messwerteblock selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [MW_SELECT_LESEN_NORM3](#job-mw-select-lesen-norm3) - Messwerteblock selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_UBATT](#job-status-ubatt) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_LMM_MASSE](#job-status-lmm-masse) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_AN_LUFTTEMPERATUR](#job-status-an-lufttemperatur) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_PWG_POTI_SPANNUNG](#job-status-pwg-poti-spannung) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_PEDALWERTGEBER_POTI_2](#job-status-pedalwertgeber-poti-2) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_ATMOSPHAERENDRUCK](#job-status-atmosphaerendruck) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_KUEHLMITTELTEMPERATUR](#job-status-kuehlmitteltemperatur) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_LADEDRUCK_IST](#job-status-ladedruck-ist) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_ANSAUGLUFTTEMPERATUR](#job-status-ansauglufttemperatur) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_LUFTMASSE_IST](#job-status-luftmasse-ist) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_PEDALWERTGEBER_POTI_1](#job-status-pedalwertgeber-poti-1) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_LUTTEMPERATUR](#job-status-luttemperatur) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_LUFTMASSE_SOLL](#job-status-luftmasse-soll) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_LADEDRUCK_SOLL](#job-status-ladedruck-soll) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_KILOMETERSTAND](#job-status-kilometerstand) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_BETRIEBSSTUNDENZAEHLER](#job-status-betriebsstundenzaehler) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_RAILDRUCK_IST](#job-status-raildruck-ist) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [STATUS_RAILDRUCK_SOLL](#job-status-raildruck-soll) - Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 
- [EWS_STARTWERT](#job-ews-startwert) - EWS-Empfangsstatus auslesen KWP2000: $21 DefineDataByLocalIdentifier 
- [EWS_EMPFANG](#job-ews-empfang) - EWS-Empfangsstatus auslesen KWP2000: $21 DefineDataByLocalIdentifier 
- [STATUS_MFL_KLI_VARIANTE_LESEN](#job-status-mfl-kli-variante-lesen) - Auslesen ob MFL oder KLI verbaut $30 InputOutputControlByLocalIndentifierer
- [LOESCHEN_KLI_FGR_VARIANTE](#job-loeschen-kli-fgr-variante) - Loeschen der Varianten
- [STATUS_DIGITAL](#job-status-digital)
- [STATUS_LAUFUNRUHE_LLR_MENGE](#job-status-laufunruhe-llr-menge) - Auslesen selektive Mengenkorrektur
- [STATUS_LAUFUNRUHE_DREHZAHL](#job-status-laufunruhe-drehzahl) - Auslesen selektive Mengenkorrektur
- [START_SYSTEMCHECK_ZYL](#job-start-systemcheck-zyl) - Starten der Drehungleichfouermigleitsmessung LLR_AUS Starten der Laufruhe - Mengen Messung
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Indentifikation, FS_Codes ShadowFS_Codes, ShadowFS_lang, AIF

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

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-interfacetype"></a>
### INTERFACETYPE

Interface-Typ bestimmen und ausgeben Es wird der Name des Interfaces übergeben Wichtig für Baudratenumschaltung weil bei ADS, EADS und OBD sind nur 115200 Baud möglich, bei EDIC nur 125000 Baud möglich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| INTERFACE_TYP | string | Rueckmeldung des Interface-Typs |

<a id="job-diagnose-mode"></a>
### DIAGNOSE_MODE

SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter Diagnose-Modus table DiagMode MODE MODE_TEXT Defaultwert: DEFAULT (DefaultMode) |
| BAUDRATE | string | optionaler Parameter fuer die gewuenschte Baudrate table BaudRate BAUD |
| SPEZIFISCHE_BAUDRATE_WERT | long | Parameter nur fuer BAUDRATE = 'SB' ( spezifische Baudrate ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnoseprotokoll-setzen"></a>
### DIAGNOSEPROTOKOLL_SETZEN

Wählt ein Diagnoseprotokoll aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_PROT | string | Diagnoseprotokoll table KONZEPT_TABELLE KONZEPT_TEXT |
| DIAG_ADR | string | Diagnoseadresse  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |

<a id="job-diagnoseprotokoll-lesen"></a>
### DIAGNOSEPROTOKOLL_LESEN

Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_DIAG_PROT |
| DIAG_PROT_IST | string | Gibt das aktuelle gewählte Protokoll aus table KONZEPT_TABELLE KONZEPT_TEXT |
| DIAG_PROT_ANZAHL | int | Anzahl der Diagnoseprotokolle |
| DIAG_PROT_NR1 | string | Alle möglichen Diagnose-Protokolle Falls mehrere Protokolle möglich sind werden die entsprechenden Results DIAG_PROT_NRx dynamisch erzeugt |

<a id="job-ident"></a>
### IDENT

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_VAR_INDEX | int | Varianten-Index |
| ID_DATUM_JAHR | int | Herstelldatum (Jahr) |
| ID_DATUM_MONAT | int | Herstelldatum (Monat) |
| ID_DATUM_TAG | int | Herstelldatum (Tag) |
| ID_DATUM | string | Herstelldatum (TT.MM.JJJJ) |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR_MCV | string | Softwarenummer (message catalogue version) |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| ID_SW_NR_OSV | string | Softwarenummer (operating system version) |
| ID_SW_NR_RES | string | Softwarenummer (reserved - currently unused) |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_NUMMER | int | ==0 : aktuelles AIF &gt; 0 : Nummer des zu lesenden AIF default = 0 : aktuelles AIF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_ADRESSE_HIGH | int | AIF Adresse des AIF, High-Word |
| AIF_ADRESSE_LOW | int | AIF Adresse des AIF, Low-Word |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_SW_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_SERIEN_NR | string | Tester Seriennummer |
| AIF_KM | long | km-Stand bei der Programmierung |
| AIF_PROG_NR | string | Programmstandsnummer |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge |
| AIF_ANZ_DATEN | int | Groesse des AIF-Eintrags |
| AIF_GROESSE | int | Groesse des AIF |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-aif-schreiben"></a>
### AIF_SCHREIBEN

Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig oder 17-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ oder TTMMJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_SW_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_SERIEN_NR | string | Tester Seriennummer |
| AIF_KM | long | km-Stand bei der Programmierung |
| AIF_PROG_NR | string | Programmstandsnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| AIF_NUMMER | int | Nummer des geschreibenen AIF |
| AIF_DATEN | binary | AIF Hex-Daten |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG AIF lesen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG AIF lesen |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG AIF schreiben |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG AIF schreiben |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-lang"></a>
### FS_LESEN_LANG

Auslesen des Fehlerspeichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SHADOW | string | Umschalten auf Shadowfehlerspeicher |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_ORT_NR | int | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_LZ | int | Fehlerlogistikzaehler |
| F_ART_ANZ | int | Anzahl der Fehlerarten des SG |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_ART1_NR | int | Fehlerart 1 Index |
| F_ART1_TEXT | string | Fehlerart 1 Text |
| F_ART2_NR | int | Fehlerart 2 Index |
| F_ART2_TEXT | string | Fehlerart 2 Text |
| F_ART3_NR | int | Fehlerart 3 Index |
| F_ART3_TEXT | string | Fehlerart 3 Text |
| F_ART4_NR | int | Fehlerart 4 Index |
| F_ART4_TEXT | string | Fehlerart 4 Text |
| F_ART7_NR | int | Fehlerart 7 Index |
| F_ART7_TEXT | string | Fehlerart 7 Text |
| F_VORHANDEN | int | Statusbit Fehler vorhanden |
| F_UW1_NR | int | Umweltbedingung 1 Index |
| F_UW1_TEXT | string | Umweltbedingung 1 Text |
| F_UW1_EINH | string | Umweltbedingung 1 Text |
| F_UW1_WERT | real | Umweltbedingung 1 Wert |
| F_UW2_NR | int | Umweltbedingung 2 Index |
| F_UW2_TEXT | string | Umweltbedingung 2 Text |
| F_UW2_EINH | string | Umweltbedingung 2 Einheit |
| F_UW2_WERT | real | Umweltbedingung 2 Wert |
| F_UW3_NR | int | Umweltbedingung 3 Index |
| F_UW3_TEXT | string | Umweltbedingung 3 Text |
| F_UW3_EINH | string | Umweltbedingung 3 Einheit |
| F_UW3_WERT | real | Umweltbedingung 3 Wert |
| F_UW4_NR | int | Umweltbedingung 4 Index |
| F_UW4_TEXT | string | Umweltbedingung 4 Text |
| F_UW4_EINH | string | Umweltbedingung 4 EINH |
| F_UW4_WERT | real | Umweltbedingung 4  Wert |
| F_UW5_NR | int | Umweltbedingung 5 Index |
| F_UW5_TEXT | string | Umweltbedingung 5 Text |
| F_UW5_EINH | string | Umweltbedingung 5 EINH |
| F_UW5_WERT | real | Umweltbedingung 5  Wert |
| F_UW6_NR | int | Umweltbedingung 6 Index |
| F_UW6_TEXT | string | Umweltbedingung 6 Text |
| F_UW6_EINH | string | Umweltbedingung 6 EINH |
| F_UW6_WERT | real | Umweltbedingung 6  Wert |
| F_UW7_NR | int | Umweltbedingung 7 Index |
| F_UW7_TEXT | string | Umweltbedingung 7 Text |
| F_UW7_EINH | string | Umweltbedingung 7 EINH |
| F_UW7_WERT | real | Umweltbedingung 7  Wert |
| F_UW8_NR | int | Umweltbedingung 8 Index |
| F_UW8_TEXT | string | Umweltbedingung 8 Text |
| F_UW8_EINH | string | Umweltbedingung 8 EINH |
| F_UW8_WERT | real | Umweltbedingung 8  Wert |
| F_UW9_NR | int | Umweltbedingung 9 Index |
| F_UW9_TEXT | string | Umweltbedingung 9 Text |
| F_UW9_EINH | string | Umweltbedingung 9 EINH |
| F_UW9_WERT | real | Umweltbedingung 9  Wert |
| F_UW10_NR | int | Umweltbedingung 10 Index |
| F_UW10_TEXT | string | Umweltbedingung 10 Text |
| F_UW10_EINH | string | Umweltbedingung 10 EINH |
| F_UW10_WERT | real | Umweltbedingung 10  Wert |
| F_UW11_NR | int | Umweltbedingung 11 Index |
| F_UW11_TEXT | string | Umweltbedingung 11 Text |
| F_UW11_EINH | string | Umweltbedingung 11 EINH |
| F_UW11_WERT | real | Umweltbedingung 11  Wert |
| F_UW12_NR | int | Umweltbedingung 12 Index |
| F_UW12_TEXT | string | Umweltbedingung 12 Text |
| F_UW12_EINH | string | Umweltbedingung 12 EINH |
| F_UW12_WERT | real | Umweltbedingung 12  Wert |
| F_UW13_NR | int | Umweltbedingung 13 Index |
| F_UW13_TEXT | string | Umweltbedingung 13 Text |
| F_UW13_EINH | string | Umweltbedingung 13 EINH |
| F_UW13_WERT | real | Umweltbedingung 13  Wert |
| F_UW14_NR | int | Umweltbedingung 14 Index |
| F_UW14_TEXT | string | Umweltbedingung 14 Text |
| F_UW14_EINH | string | Umweltbedingung 14 EINH |
| F_UW14_WERT | real | Umweltbedingung 14  Wert |
| F_UW15_NR | int | Umweltbedingung 15 Index |
| F_UW15_TEXT | string | Umweltbedingung 15 Text |
| F_UW15_EINH | string | Umweltbedingung 15 EINH |
| F_UW15_WERT | real | Umweltbedingung 15  Wert |
| F_UW16_NR | int | Umweltbedingung 16 Index |
| F_UW16_TEXT | string | Umweltbedingung 16 Text |
| F_UW16_EINH | string | Umweltbedingung 16 EINH |
| F_UW16_WERT | real | Umweltbedingung 16  Wert |
| F_UW17_NR | int | Umweltbedingung 17 Index |
| F_UW17_TEXT | string | Umweltbedingung 17 Text |
| F_UW17_EINH | string | Umweltbedingung 17 EINH |
| F_UW17_WERT | real | Umweltbedingung 17  Wert |
| F_UW18_NR | int | Umweltbedingung 18 Index |
| F_UW18_TEXT | string | Umweltbedingung 18 Text |
| F_UW18_EINH | string | Umweltbedingung 18 EINH |
| F_UW18_WERT | real | Umweltbedingung 18  Wert |
| F_UW19_NR | int | Umweltbedingung 19 Index |
| F_UW19_TEXT | string | Umweltbedingung 19 Text |
| F_UW19_EINH | string | Umweltbedingung 19 EINH |
| F_UW19_WERT | real | Umweltbedingung 19  Wert |
| F_UW20_NR | int | Umweltbedingung 20 Index |
| F_UW20_TEXT | string | Umweltbedingung 20 Text |
| F_UW20_EINH | string | Umweltbedingung 20 EINH |
| F_UW20_WERT | real | Umweltbedingung 20  Wert |
| F_UW21_NR | int | Umweltbedingung 21 Index |
| F_UW21_TEXT | string | Umweltbedingung 21 Text |
| F_UW21_EINH | string | Umweltbedingung 21 EINH |
| F_UW21_WERT | real | Umweltbedingung 21  Wert |
| F_UW22_NR | int | Umweltbedingung 22 Index |
| F_UW22_TEXT | string | Umweltbedingung 22 Text |
| F_UW22_EINH | string | Umweltbedingung 22 EINH |
| F_UW22_WERT | real | Umweltbedingung 22  Wert |
| F_CODEHEX | binary | Hexdump des Fehlersatzes |
| F_HEX_CODE | binary | Hexdump des Fehlersatzes |
| F_UW_SATZ | int | Anzahl der Umweltsaetze , Steuerung der Anzeige in der Applikation |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-fs-lesen-detail"></a>
### FS_LESEN_DETAIL

Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Fehlercode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_PCODE | unsigned int | optional / Pflicht fuer abgasrelevante SG Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_PCODE7 | unsigned int | optional / fuer abgasrelevante SG Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE7_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE7_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_LZ | int | Logistikzaehler als Zahl Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| F_ART_ANZ | int | Anzahl der zusaetzlichen Fehlerarten Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_ARTi_NR   Index der i. Fehlerart (string) F_ARTi_TEXT Text  zur i. Fehlerart |
| F_UW_KM | long | Umweltbedingung Kilometerstand Wertebereich: 0 - 524280 km |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-tel-roh"></a>
### TEL_ROH

Rohtelegramm ohne Header lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REQUEST | binary | Daten ohne Header |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| RESPONSE | binary | Daten ohne Header |

<a id="job-abgleich-ima-lesen-hex"></a>
### ABGLEICH_IMA_LESEN_HEX

IMA Abgleichwerte und Ausgabe im HEX Format KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier LID: $BB

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| ABGLEICH_IMA_WERT | binary | Hex-Antwort von SG |

<a id="job-abgleich-ima-lesen"></a>
### ABGLEICH_IMA_LESEN

IMA Abgleichwerte Ausgabe zylinderspezifisch im Injektor Format KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier LID: $BB

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| ABGLEICH_IMA_WERT_ZYL1 | string | Antwort von SG im Format wie auf Injektor |
| ABGLEICH_IMA_WERT_ZYL2 | string | Antwort von SG im Format wie auf Injektor |
| ABGLEICH_IMA_WERT_ZYL3 | string | Antwort von SG im Format wie auf Injektor |
| ABGLEICH_IMA_WERT_ZYL4 | string | Antwort von SG im Format wie auf Injektor |
| ABGLEICH_IMA_WERT_ZYL5 | string | Antwort von SG im Format wie auf Injektor |
| ABGLEICH_IMA_WERT_ZYL6 | string | Antwort von SG im Format wie auf Injektor |

<a id="job-abgleich-programmieren-ima-hex"></a>
### ABGLEICH_PROGRAMMIEREN_IMA_HEX

Programmieren der IMA Abgleichwerte und Eingabe im HEX Format - Alle Zylinder KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier LID: $BB

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_IMA | binary | gesamter Hex-Wert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-programmieren-ima"></a>
### ABGLEICH_PROGRAMMIEREN_IMA

Programmieren der IMA Abgleichwerte und Eingabe im HEX Format - Alle Zylinder KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier LID: $BB

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_IMA_ZYL1 | string |  |
| ABGLEICH_VERSTELLEN_IMA_ZYL2 | string |  |
| ABGLEICH_VERSTELLEN_IMA_ZYL3 | string |  |
| ABGLEICH_VERSTELLEN_IMA_ZYL4 | string |  |
| ABGLEICH_VERSTELLEN_IMA_ZYL5 | string |  |
| ABGLEICH_VERSTELLEN_IMA_ZYL6 | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-programmieren-ima-zyl-hex"></a>
### ABGLEICH_PROGRAMMIEREN_IMA_ZYL_HEX

IMA Abgleichwert Programmierrn im HEX Format KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier LID: $B5 - $B5

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_IMA_IDENT | int | Identifier zylinderspezifisch B5 - BA |
| ABGLEICH_VERSTELLEN_IMA_HEX | binary |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-programmieren-ima-zyl"></a>
### ABGLEICH_PROGRAMMIEREN_IMA_ZYL

IMA Abgleichwert Programmierrn im Injektor aufgedruckten Format KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier LID: $B5 - $B5

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_IMA_IDENT | int | Identifier zylinderspezifisch B5 - BA |
| ABGLEICH_VERSTELLEN_IMA_ZYL | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-ima-abgleichflag-lesen"></a>
### ABGLEICH_IMA_ABGLEICHFLAG_LESEN

Lesen des IMA Abgleichflags - muss 1x beschrieben sein KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier LID: $BC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| IMA_FLAG | int | Ima Flag - Ima Kennfeld programmiert |

<a id="job-abgleich-ima-abgleichflag-vorgeben"></a>
### ABGLEICH_IMA_ABGLEICHFLAG_VORGEBEN

Vorgeben des IMA Abgleichflags - muss 1x beschrieben sein KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-ima-abgleichflag-programmieren"></a>
### ABGLEICH_IMA_ABGLEICHFLAG_PROGRAMMIEREN

Programmieren des IMA Abgleichflags - muss 1x beschrieben sein KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-selektiv-loeschen"></a>
### FS_SELEKTIV_LOESCHEN

Auslesen des Fehlerspeichers KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FEHLER_0 | int | 0-65535 |
| FEHLER_1 | int | 0-65535 |
| FEHLER_2 | int | 0-65535 |
| FEHLER_3 | int | 0-65535 |
| FEHLER_4 | int | 0-65535 |
| FEHLER_5 | int | 0-65535 |
| FEHLER_6 | int | 0-65535 |
| FEHLER_7 | int | 0-65535 |
| FEHLER_8 | int | 0-65535 |
| FEHLER_9 | int | 0-65535 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-verstellen"></a>
### ABGLEICH_VERSTELLEN

Verstellen eines EEPROM Abgleichwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IDENTIFIER_ABGLEICH | string | Local Identifier |
| ABGLEICH_VERSTELLEN_WERT | real | Neuer Verstellwert |
| ABGLEICH_VERSTELLEN_WERT2 | real | Neuer Verstellwert 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-verstellen-x"></a>
### ABGLEICH_VERSTELLEN_X

Verstellen eines Abgleichwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IDENTIFIER_ABGLEICH | int | Local Identifier |
| ABGLEICH_VERSTELLEN_WERT | real | Neuer Verstellwert |
| ABGLEICH_VERSTELLEN_WERT2 | real | Neuer Verstellwert 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-abgleich-lesen"></a>
### ABGLEICH_LESEN

Veines Abgleichwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IDENTIFIER_ABGLEICH | string | Local Identifier |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| ABGLEICH_LESEN_WERT | real | Neuer Verstellwert |
| ABGLEICH_LESEN_WERT2 | real | Neuer Verstellwert 2 |

<a id="job-abgleich-lesen-x"></a>
### ABGLEICH_LESEN_X

Veines Abgleichwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IDENTIFIER_ABGLEICH | int | Local Identifier |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| ABGLEICH_LESEN_WERT | real | Neuer Verstellwert |
| ABGLEICH_LESEN_WERT2 | real | Neuer Verstellwert 2 |

<a id="job-abgleich-prog"></a>
### ABGLEICH_PROG

Programmieren eines Abgleichwertes mittels Kurzbezeichner aus dem EEPROM KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IDENTIFIER_ABGLEICH | string | Local Identifier |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-prog-x"></a>
### ABGLEICH_PROG_X

Programmieren eines Abgleichwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IDENTIFIER_ABGLEICH | int | Local Identifier |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleichwerte-schreiben"></a>
### ABGLEICHWERTE_SCHREIBEN

Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_SCHREIBEN_ANZAHL | int | Anzahl der zu schreibenden Abgleichdatenbytes ohne die Pruefziffer |
| ABGLEICHWERTE_SCHREIBEN_DATEN | string | Abgleichdaten in folgendem Format |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_SCHREIBEN_ABGLEICHDATEN | string | Abgleichdaten zum Steuergeraet |
| ABGLEICHWERTE_SCHREIBEN_PRUEFZEICHEN | string | das im Job berechnete Pruefzeichen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleichwerte-lesen"></a>
### ABGLEICHWERTE_LESEN

Lesen der Motorabgleichwerte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_LESEN_ANZAHL | int | Anzahl der zu lesenden Bytes, =12 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_LESEN_DATEN | string | aus dem Steuergeraet ausgelesene Daten im Format z.B.: "01 A5 FE" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_..., wenn argument nicht uebergeben oder ausser Bereich |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleichflag-schreiben"></a>
### ABGLEICHFLAG_SCHREIBEN

Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHFLAG_SCHREIBEN_FLAG | string | ABGLEICH_IO : 0x01 ABGLEICH_NIO: 0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_..., wenn argument nicht uebergeben oder ausser Bereich |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleichflag-lesen"></a>
### ABGLEICHFLAG_LESEN

Lesen des EEPROM-Speichers ab Adresse 0x0032

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHFLAG_LESEN_WERT | string | 0x01 --&gt; ABGLEICH_IO 0xFF --&gt; ABGLEICH_NIO |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_..., wenn argument nicht uebergeben oder ausser Bereich |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-selectiv"></a>
### STEUERN_SELECTIV

Verstellen eines Stellerwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IDENTIFIER_STELLER | string | Local Identifier |
| TASTVERHAELTNIS | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-selectiv-x"></a>
### STEUERN_SELECTIV_X

Verstellen eines Stellerwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IDENTIFIER_STELLER | int | Local Identifier |
| TASTVERHAELTNIS | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-selectiv"></a>
### STEUERN_ENDE_SELECTIV

Beenden von Verstellen eines Stellerwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IDENTIFIER_STELLER | string | Local Identifier |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-selectiv-x"></a>
### STEUERN_ENDE_SELECTIV_X

Beenden von Verstellen eines Stellerwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IDENTIFIER_STELLER | int | Local Identifier |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-wert-lesen-x"></a>
### STEUERN_WERT_LESEN_X

Lesen des Vorgegebenen Stellerwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IDENTIFIER_STELLER | int | Local Identifier |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STEUERN_LESEN_WERT | real | Verstellwert von SG |

<a id="job-steuern-wert-lesen"></a>
### STEUERN_WERT_LESEN

Lesen des Vorgegebenen Stellerwertes KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IDENTIFIER_STELLER | string | Local Identifier |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STEUERN_LESEN_WERT | real | Verstellwert von SG |

<a id="job-steuern-zuheizer"></a>
### STEUERN_ZUHEIZER

Vorgeben eines Stellerwertes fuer Zuheizer KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier Verstellwert 5 - 95 %

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zuheizer-aus"></a>
### STEUERN_ZUHEIZER_AUS

Beenden von Vorgeben von Zuheizer ansteuern KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

Vorgeben eines Stellerwertes fuer E - Luefter KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier Verstellwert 5 - 90 %

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-e-luefter-aus"></a>
### STEUERN_E_LUEFTER_AUS

Beenden von Vorgeben von E-Luefter ansteuern KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vfp"></a>
### STEUERN_VFP

Vorgeben eines Stellerwertes fuer Vorfoerderpumpe KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier Verstellwert 5 - 95 %

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vfp-aus"></a>
### STEUERN_VFP_AUS

Beenden von Vorgeben von Vorfoerderpumpe ansteuern KWP2000 / KWP2000*: $30 InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-mw-select-lesen-norm"></a>
### MW_SELECT_LESEN_NORM

Messwerteblock selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MW_SELECT_LESEN_MNR | binary | Message Nummern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-mw-select-lesen-norm2"></a>
### MW_SELECT_LESEN_NORM2

Messwerteblock selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MW_SELECT_LESEN_MNR | binary | Message Namen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-mw-select-lesen-norm3"></a>
### MW_SELECT_LESEN_NORM3

Messwerteblock selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MW_SELECT_LESEN_MNR | binary | Message Nummern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_UBATT_WERT | real | Ergebnis |
| STAT_UBATT_EINH | string | Einheit |

<a id="job-status-lmm-masse"></a>
### STATUS_LMM_MASSE

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_LMM_MASSE_WERT | real | Ergebnis |
| STAT_LMM_MASSE_EINH | string | Einheit |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_MOTORTEMPERATUR_WERT | real | Ergebnis |
| STAT_MOTORTEMPERATUR_EINH | string | Einheit |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_MOTORDREHZAHL_WERT | real | Ergebnis |
| STAT_MOTORDREHZAHL_EINH | string | Einheit |

<a id="job-status-an-lufttemperatur"></a>
### STATUS_AN_LUFTTEMPERATUR

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_AN_LUFTTEMPERATUR_WERT | real | Ergebnis |
| STAT_AN_LUFTTEMPERATUR_EINH | string | Einheit |

<a id="job-status-pwg-poti-spannung"></a>
### STATUS_PWG_POTI_SPANNUNG

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_PWG_POTI_SPANNUNG_WERT | real | Ergebnis |
| STAT_PWG_POTI_SPANNUNG_EINH | string | Einheit |

<a id="job-status-pedalwertgeber-poti-2"></a>
### STATUS_PEDALWERTGEBER_POTI_2

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_PEDALWERTGEBER_POTI_2_WERT | real | Ergebnis |
| STAT_PEDALWERTGEBER_POTI_2_EINH | string | Einheit |

<a id="job-status-atmosphaerendruck"></a>
### STATUS_ATMOSPHAERENDRUCK

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_ATMOSPHAERENDRUCK_WERT | real | Ergebnis |
| STAT_ATMOSPHAERENDRUCK_EINH | string | Einheit |

<a id="job-status-kuehlmitteltemperatur"></a>
### STATUS_KUEHLMITTELTEMPERATUR

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_KUEHLMITTELTEMPERATUR_WERT | real | Ergebnis |
| STAT_KUEHLMITTELTEMPERATUR_EINH | string | Einheit |

<a id="job-status-ladedruck-ist"></a>
### STATUS_LADEDRUCK_IST

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_LADEDRUCK_IST_WERT | real | Ergebnis |
| STAT_LADEDRUCK_IST_EINH | string | Einheit |

<a id="job-status-ansauglufttemperatur"></a>
### STATUS_ANSAUGLUFTTEMPERATUR

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_ANSAUGLUFTTEMPERATUR_WERT | real | Ergebnis |
| STAT_ANSAUGLUFTTEMPERATUR_EINH | string | Einheit |

<a id="job-status-luftmasse-ist"></a>
### STATUS_LUFTMASSE_IST

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_LUFTMASSE_IST_WERT | real | Ergebnis |
| STAT_LUFTMASSE_IST_EINH | string | Einheit |

<a id="job-status-pedalwertgeber-poti-1"></a>
### STATUS_PEDALWERTGEBER_POTI_1

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_PEDALWERTGEBER_POTI_1_WERT | real | Ergebnis |
| STAT_PEDALWERTGEBER_POTI_1_EINH | string | Einheit |

<a id="job-status-luttemperatur"></a>
### STATUS_LUTTEMPERATUR

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_LUTTEMPERATUR_WERT | real | Ergebnis |
| STAT_LUTTEMPERATUR_EINH | string | Einheit |

<a id="job-status-luftmasse-soll"></a>
### STATUS_LUFTMASSE_SOLL

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_LUFTMASSE_SOLL_WERT | real | Ergebnis |
| STAT_LUFTMASSE_SOLL_EINH | string | Einheit |

<a id="job-status-ladedruck-soll"></a>
### STATUS_LADEDRUCK_SOLL

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_LADEDRUCK_SOLL_WERT | real | Ergebnis |
| STAT_LADEDRUCK_SOLL_EINH | string | Einheit |

<a id="job-status-kilometerstand"></a>
### STATUS_KILOMETERSTAND

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_KILOMETERSTAND_WERT | real | Ergebnis |
| STAT_KILOMETERSTAND_EINH | string | Einheit |

<a id="job-status-betriebsstundenzaehler"></a>
### STATUS_BETRIEBSSTUNDENZAEHLER

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_BETRIEBSSTUNDENZAEHLER_WERT | real | Ergebnis |
| STAT_BETRIEBSSTUNDENZAEHLER_EINH | string | Einheit |

<a id="job-status-raildruck-ist"></a>
### STATUS_RAILDRUCK_IST

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_RAILDRUCK_IST_WERT | real | Ergebnis |
| STAT_RAILDRUCK_IST_EINH | string | Einheit |

<a id="job-status-raildruck-soll"></a>
### STATUS_RAILDRUCK_SOLL

Messwert selectiv lesen KWP2000: $2C DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_RAILDRUCK_SOLL_WERT | real | Ergebnis |
| STAT_RAILDRUCK_SOLL_EINH | string | Einheit |

<a id="job-ews-startwert"></a>
### EWS_STARTWERT

EWS-Empfangsstatus auslesen KWP2000: $21 DefineDataByLocalIdentifier 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARAMETER | int | Parameter zur Initialisierung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| EWS_STATUS | string | Rueckgabestatus bei der Startwertinitialisierung |
| STAT_EWS_WERT | int | Rueckgabestatus bei der Startwertinitialisierung |

<a id="job-ews-empfang"></a>
### EWS_EMPFANG

EWS-Empfangsstatus auslesen KWP2000: $21 DefineDataByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| EWS_EMPFANGSSTATUS | string | Rueckgabestatus bei der Startwertinitialisierung |
| EWS_STATUS_VALUE | int | Rueckgabestatus bei der Startwertinitialisierung |

<a id="job-status-mfl-kli-variante-lesen"></a>
### STATUS_MFL_KLI_VARIANTE_LESEN

Auslesen ob MFL oder KLI verbaut $30 InputOutputControlByLocalIndentifierer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_MFL_EIN | int | Multfunktionslenkrad vorhanden |
| STAT_KLI_EIN | int | Klimakompressor vorhanden |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| ID_SG_ADR | long | Steuergeraeteadresse |

<a id="job-loeschen-kli-fgr-variante"></a>
### LOESCHEN_KLI_FGR_VARIANTE

Loeschen der Varianten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_VARIANTE_LOESCHEN | string | gibt bei OKAY an, ob loeschen erfolgreich war |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| ID_SG_ADR | long | Steuergeraeteadresse |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TABELLE | string | Ausgabe mit/ohne Text |
| TEXTDIGITAL | string | Ausgabe mit/ohne Text |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_DIGITAL_BEDINGUNG | string | Der Ort der Abschaltursache |
| STAT_DIGITAL_ERGEBNIS | string | Text in Abhängigkeit vom Ergebnis |
| STAT_BLS_EIN | int | Zustand des untersuchten Bits |
| STAT_BLTS_EIN | int | Zustand des untersuchten Bits |
| STAT_KUP_EIN | int | Zustand des untersuchten Bits |
| STAT_GETRIEBEART_HAND_EIN | int | Zustand des untersuchten Bits |
| STAT_AC_EIN | int | Zustand des untersuchten Bits |
| STAT_ODS_EIN | int | Zustand des untersuchten Bits |
| STAT_KO_EIN | int | Zustand des untersuchten Bits |
| STAT_MFLEINP_EIN | int | Zustand des untersuchten Bits |
| STAT_MFLEINM_EIN | int | Zustand des untersuchten Bits |
| STAT_MFLWA_EIN | int | Zustand des untersuchten Bits |
| STAT_MFLAUS_EIN | int | Zustand des untersuchten Bits |

<a id="job-status-laufunruhe-llr-menge"></a>
### STATUS_LAUFUNRUHE_LLR_MENGE

Auslesen selektive Mengenkorrektur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_LAUFUNRUHE_LLR_MENGE_ZYL1_WERT | real |  |
| STAT_LAUFUNRUHE_LLR_MENGE_ZYL2_WERT | real |  |
| STAT_LAUFUNRUHE_LLR_MENGE_ZYL3_WERT | real |  |
| STAT_LAUFUNRUHE_LLR_MENGE_ZYL4_WERT | real |  |
| STAT_LAUFUNRUHE_LLR_MENGE_ZYL5_WERT | real |  |
| STAT_LAUFUNRUHE_LLR_MENGE_ZYL6_WERT | real |  |
| STAT_LAUFUNRUHE_LLR_MENGE_EINH | string |  |

<a id="job-status-laufunruhe-drehzahl"></a>
### STATUS_LAUFUNRUHE_DREHZAHL

Auslesen selektive Mengenkorrektur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_LAUFUNRUHE_DREHZAHL_ZYL1_WERT | real |  |
| STAT_LAUFUNRUHE_DREHZAHL_ZYL2_WERT | real |  |
| STAT_LAUFUNRUHE_DREHZAHL_ZYL3_WERT | real |  |
| STAT_LAUFUNRUHE_DREHZAHL_ZYL4_WERT | real |  |
| STAT_LAUFUNRUHE_DREHZAHL_ZYL5_WERT | real |  |
| STAT_LAUFUNRUHE_DREHZAHL_ZYL6_WERT | real |  |
| STAT_LAUFUNRUHE_DREHZAHL_EINH | string |  |

<a id="job-start-systemcheck-zyl"></a>
### START_SYSTEMCHECK_ZYL

Starten der Drehungleichfouermigleitsmessung LLR_AUS Starten der Laufruhe - Mengen Messung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SWITCH_MENGEN_DREHZAHL | string | LLR_AUS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Indentifikation, FS_Codes ShadowFS_Codes, ShadowFS_lang, AIF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| PRUEFCODE | binary | Indentifikation, AIF, FS_Codes ShadowFS_Codes, ShadowFS_lang |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (4 × 2)
- [LIEFERANTEN](#table-lieferanten) (56 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [ABGLEICH](#table-abgleich) (26 × 6)
- [STELLER](#table-steller) (12 × 6)
- [DIG_MFL](#table-dig-mfl) (4 × 10)
- [DIG_FGR_AUS](#table-dig-fgr-aus) (23 × 10)
- [DIG_KWH_AUS](#table-dig-kwh-aus) (11 × 10)
- [DIG_AGR_AUS](#table-dig-agr-aus) (20 × 10)
- [DIG_MFLKLI](#table-dig-mflkli) (2 × 4)
- [DIG_ALLG](#table-dig-allg) (11 × 10)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (12 × 3)
- [BETRIEBSWTAB](#table-betriebswtab) (215 × 17)
- [FORTTEXTE](#table-forttexte) (532 × 12)
- [FUMWELTTEXTE](#table-fumwelttexte) (35 × 9)
- [FARTMATRIX](#table-fartmatrix) (531 × 17)
- [FARTTEXTE_ERW](#table-farttexte-erw) (251 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (531 × 5)
- [ANALOG0](#table-analog0) (1 × 8)
- [ANALOG1](#table-analog1) (1 × 8)
- [ANALOG2](#table-analog2) (1 × 8)
- [ANALOG3](#table-analog3) (1 × 8)
- [ANALOG4](#table-analog4) (1 × 8)
- [ANALOG5](#table-analog5) (1 × 8)
- [ANALOG6](#table-analog6) (1 × 8)
- [ANALOG7](#table-analog7) (1 × 8)
- [ANALOG8](#table-analog8) (1 × 8)
- [ANALOG9](#table-analog9) (1 × 8)
- [ANALOG10](#table-analog10) (1 × 8)
- [ANALOG11](#table-analog11) (1 × 8)
- [ANALOG12](#table-analog12) (1 × 8)
- [ANALOG13](#table-analog13) (1 × 8)
- [ANALOG14](#table-analog14) (1 × 8)
- [ANALOG15](#table-analog15) (1 × 8)
- [ANALOG16](#table-analog16) (1 × 8)
- [ANALOG17](#table-analog17) (1 × 8)
- [ANALOG18](#table-analog18) (1 × 8)
- [ANALOG19](#table-analog19) (1 × 8)
- [ANALOG20](#table-analog20) (1 × 8)
- [ANALOG21](#table-analog21) (1 × 8)
- [ANALOG22](#table-analog22) (1 × 8)
- [ANALOG23](#table-analog23) (1 × 8)
- [ANALOG24](#table-analog24) (1 × 8)
- [ANALOG25](#table-analog25) (1 × 8)
- [ANALOG26](#table-analog26) (1 × 8)
- [ANALOG27](#table-analog27) (1 × 8)
- [ANALOG28](#table-analog28) (1 × 8)
- [ANALOG29](#table-analog29) (1 × 8)
- [ANALOG30](#table-analog30) (1 × 8)
- [ANALOG31](#table-analog31) (1 × 8)
- [ANALOG32](#table-analog32) (1 × 8)
- [ANALOG33](#table-analog33) (1 × 8)
- [ANALOG34](#table-analog34) (1 × 8)
- [ANALOG35](#table-analog35) (1 × 8)
- [ANALOG36](#table-analog36) (1 × 8)
- [ANALOG37](#table-analog37) (1 × 8)
- [ANALOG38](#table-analog38) (1 × 8)
- [ANALOG39](#table-analog39) (1 × 8)
- [ANALOG40](#table-analog40) (1 × 8)
- [ANALOG41](#table-analog41) (1 × 8)
- [ANALOG42](#table-analog42) (1 × 8)
- [ANALOG43](#table-analog43) (1 × 8)
- [ANALOG44](#table-analog44) (1 × 8)
- [ANALOG45](#table-analog45) (1 × 8)
- [ANALOG46](#table-analog46) (1 × 8)
- [ANALOG47](#table-analog47) (1 × 8)
- [ANALOG48](#table-analog48) (1 × 8)
- [ANALOG49](#table-analog49) (1 × 8)
- [ANALOG50](#table-analog50) (1 × 8)
- [ANALOG51](#table-analog51) (1 × 8)
- [ANALOG52](#table-analog52) (1 × 8)
- [ANALOG53](#table-analog53) (1 × 8)
- [ANALOG54](#table-analog54) (1 × 8)
- [ANALOG55](#table-analog55) (1 × 8)
- [ANALOG56](#table-analog56) (1 × 8)
- [ANALOG57](#table-analog57) (1 × 8)
- [ANALOG58](#table-analog58) (1 × 8)
- [ANALOG59](#table-analog59) (1 × 8)
- [ANALOG60](#table-analog60) (1 × 8)
- [ANALOG61](#table-analog61) (1 × 8)
- [ANALOG62](#table-analog62) (1 × 8)
- [ANALOG63](#table-analog63) (1 × 8)
- [ANALOG64](#table-analog64) (1 × 8)
- [ANALOG65](#table-analog65) (1 × 8)
- [ANALOG66](#table-analog66) (1 × 8)
- [ANALOG67](#table-analog67) (1 × 8)
- [ANALOG68](#table-analog68) (1 × 8)
- [ANALOG69](#table-analog69) (1 × 8)
- [ANALOG70](#table-analog70) (1 × 8)
- [ANALOG71](#table-analog71) (1 × 8)
- [ANALOG72](#table-analog72) (1 × 8)
- [ANALOG73](#table-analog73) (1 × 8)
- [ANALOG74](#table-analog74) (1 × 8)
- [ANALOG75](#table-analog75) (1 × 8)
- [ANALOG76](#table-analog76) (1 × 8)
- [ANALOG77](#table-analog77) (1 × 8)
- [ANALOG78](#table-analog78) (1 × 8)
- [ANALOG79](#table-analog79) (1 × 8)
- [ANALOG80](#table-analog80) (1 × 8)
- [ANALOG81](#table-analog81) (1 × 8)
- [ANALOG82](#table-analog82) (1 × 8)
- [ANALOG83](#table-analog83) (1 × 8)
- [ANALOG84](#table-analog84) (1 × 8)
- [ANALOG85](#table-analog85) (1 × 8)
- [ANALOG86](#table-analog86) (1 × 8)
- [ANALOG87](#table-analog87) (1 × 8)
- [ANALOG88](#table-analog88) (1 × 8)
- [ANALOG89](#table-analog89) (1 × 8)
- [ANALOG90](#table-analog90) (1 × 8)
- [ANALOG91](#table-analog91) (1 × 8)
- [ANALOG92](#table-analog92) (1 × 8)
- [ANALOG93](#table-analog93) (1 × 8)
- [ANALOG94](#table-analog94) (1 × 8)
- [ANALOG95](#table-analog95) (1 × 8)
- [ANALOG96](#table-analog96) (1 × 8)
- [ANALOG97](#table-analog97) (1 × 8)
- [ANALOG98](#table-analog98) (1 × 8)
- [ANALOG99](#table-analog99) (1 × 8)
- [ANALOG100](#table-analog100) (1 × 8)
- [ANALOG101](#table-analog101) (1 × 8)
- [ANALOG102](#table-analog102) (1 × 8)
- [ANALOG103](#table-analog103) (1 × 8)
- [ANALOG104](#table-analog104) (1 × 8)
- [ANALOG105](#table-analog105) (1 × 8)
- [ANALOG106](#table-analog106) (1 × 8)
- [ANALOG107](#table-analog107) (1 × 8)
- [ANALOG108](#table-analog108) (1 × 8)
- [ANALOG109](#table-analog109) (1 × 8)
- [ANALOG110](#table-analog110) (1 × 8)
- [ANALOG111](#table-analog111) (1 × 8)
- [ANALOG112](#table-analog112) (1 × 8)
- [ANALOG113](#table-analog113) (1 × 8)
- [ANALOG114](#table-analog114) (1 × 8)
- [ANALOG115](#table-analog115) (1 × 8)
- [ANALOG116](#table-analog116) (1 × 8)
- [ANALOG117](#table-analog117) (1 × 8)
- [ANALOG118](#table-analog118) (1 × 8)
- [ANALOG119](#table-analog119) (1 × 8)
- [ANALOG120](#table-analog120) (1 × 8)
- [ANALOG121](#table-analog121) (1 × 8)
- [ANALOG122](#table-analog122) (1 × 8)
- [ANALOG123](#table-analog123) (1 × 8)
- [ANALOG124](#table-analog124) (1 × 8)
- [ANALOG125](#table-analog125) (1 × 8)
- [ANALOG126](#table-analog126) (1 × 8)
- [ANALOG127](#table-analog127) (1 × 8)
- [ANALOG128](#table-analog128) (1 × 8)
- [ANALOG129](#table-analog129) (1 × 8)
- [ANALOG130](#table-analog130) (1 × 8)
- [ANALOG131](#table-analog131) (1 × 8)
- [ANALOG132](#table-analog132) (1 × 8)
- [ANALOG133](#table-analog133) (1 × 8)
- [ANALOG134](#table-analog134) (1 × 8)
- [ANALOG135](#table-analog135) (1 × 8)
- [ANALOG136](#table-analog136) (1 × 8)
- [ANALOG137](#table-analog137) (1 × 8)
- [ANALOG138](#table-analog138) (1 × 8)
- [ANALOG139](#table-analog139) (1 × 8)
- [ANALOG140](#table-analog140) (1 × 8)
- [ANALOG141](#table-analog141) (1 × 8)
- [ANALOG142](#table-analog142) (1 × 8)
- [ANALOG143](#table-analog143) (1 × 8)
- [ANALOG144](#table-analog144) (1 × 8)
- [ANALOG145](#table-analog145) (1 × 8)
- [ANALOG146](#table-analog146) (1 × 8)
- [ANALOG147](#table-analog147) (1 × 8)
- [ANALOG148](#table-analog148) (1 × 8)
- [ANALOG149](#table-analog149) (1 × 8)
- [ANALOG150](#table-analog150) (1 × 8)
- [ANALOG151](#table-analog151) (1 × 8)
- [ANALOG152](#table-analog152) (1 × 8)
- [ANALOG153](#table-analog153) (1 × 8)
- [ANALOG154](#table-analog154) (1 × 8)
- [ANALOG155](#table-analog155) (1 × 8)
- [ANALOG156](#table-analog156) (1 × 8)
- [ANALOG157](#table-analog157) (1 × 8)
- [ANALOG158](#table-analog158) (1 × 8)
- [ANALOG159](#table-analog159) (1 × 8)
- [ANALOG160](#table-analog160) (1 × 8)
- [ANALOG161](#table-analog161) (1 × 8)
- [ANALOG162](#table-analog162) (1 × 8)
- [ANALOG163](#table-analog163) (1 × 8)
- [ANALOG164](#table-analog164) (1 × 8)
- [ANALOG165](#table-analog165) (1 × 8)
- [ANALOG166](#table-analog166) (1 × 8)
- [ANALOG167](#table-analog167) (1 × 8)
- [ANALOG168](#table-analog168) (1 × 8)
- [ANALOG169](#table-analog169) (1 × 8)
- [ANALOG170](#table-analog170) (1 × 8)
- [ANALOG171](#table-analog171) (1 × 8)
- [ANALOG172](#table-analog172) (1 × 8)
- [ANALOG173](#table-analog173) (1 × 8)
- [ANALOG174](#table-analog174) (1 × 8)
- [ANALOG175](#table-analog175) (1 × 8)
- [ANALOG176](#table-analog176) (1 × 8)
- [ANALOG177](#table-analog177) (1 × 8)
- [ANALOG178](#table-analog178) (1 × 8)
- [ANALOG179](#table-analog179) (1 × 8)
- [ANALOG180](#table-analog180) (1 × 8)
- [ANALOG181](#table-analog181) (1 × 8)
- [ANALOG182](#table-analog182) (1 × 8)
- [ANALOG183](#table-analog183) (1 × 8)
- [ANALOG184](#table-analog184) (1 × 8)
- [ANALOG185](#table-analog185) (1 × 8)
- [ANALOG186](#table-analog186) (1 × 8)
- [ANALOG187](#table-analog187) (1 × 8)
- [ANALOG188](#table-analog188) (1 × 8)
- [ANALOG189](#table-analog189) (1 × 8)
- [ANALOG190](#table-analog190) (1 × 8)
- [ANALOG191](#table-analog191) (1 × 8)
- [ANALOG192](#table-analog192) (1 × 8)
- [ANALOG193](#table-analog193) (1 × 8)
- [ANALOG194](#table-analog194) (1 × 8)
- [ANALOG195](#table-analog195) (1 × 8)
- [ANALOG196](#table-analog196) (1 × 8)
- [ANALOG197](#table-analog197) (1 × 8)
- [ANALOG198](#table-analog198) (1 × 8)
- [ANALOG199](#table-analog199) (1 × 8)
- [ANALOG200](#table-analog200) (1 × 8)
- [ANALOG201](#table-analog201) (1 × 8)
- [ANALOG202](#table-analog202) (1 × 8)
- [ANALOG203](#table-analog203) (1 × 8)
- [ANALOG204](#table-analog204) (1 × 8)
- [ANALOG205](#table-analog205) (1 × 8)
- [ANALOG206](#table-analog206) (1 × 8)
- [ANALOG207](#table-analog207) (1 × 8)
- [ANALOG208](#table-analog208) (1 × 8)
- [ANALOG209](#table-analog209) (1 × 8)
- [ANALOG210](#table-analog210) (1 × 8)
- [ANALOG211](#table-analog211) (1 × 8)
- [ANALOG212](#table-analog212) (1 × 8)
- [ANALOG213](#table-analog213) (1 × 8)
- [ANALOG214](#table-analog214) (1 × 8)
- [ANALOG215](#table-analog215) (1 × 8)
- [ANALOG216](#table-analog216) (1 × 8)
- [ANALOG217](#table-analog217) (1 × 8)
- [ANALOG218](#table-analog218) (1 × 8)
- [ANALOG219](#table-analog219) (1 × 8)
- [ANALOG220](#table-analog220) (1 × 8)
- [ANALOG221](#table-analog221) (1 × 8)
- [ANALOG222](#table-analog222) (1 × 8)
- [ANALOG223](#table-analog223) (1 × 8)
- [ANALOG224](#table-analog224) (1 × 8)
- [ANALOG225](#table-analog225) (1 × 8)
- [ANALOG226](#table-analog226) (1 × 8)
- [ANALOG227](#table-analog227) (1 × 8)
- [ANALOG228](#table-analog228) (1 × 8)
- [ANALOG229](#table-analog229) (1 × 8)
- [ANALOG230](#table-analog230) (1 × 8)
- [ANALOG231](#table-analog231) (1 × 8)
- [ANALOG232](#table-analog232) (1 × 8)
- [ANALOG233](#table-analog233) (1 × 8)
- [ANALOG234](#table-analog234) (1 × 8)
- [ANALOG235](#table-analog235) (1 × 8)
- [ANALOG236](#table-analog236) (1 × 8)
- [ANALOG237](#table-analog237) (1 × 8)
- [ANALOG238](#table-analog238) (1 × 8)
- [ANALOG239](#table-analog239) (1 × 8)
- [ANALOG240](#table-analog240) (1 × 8)
- [ANALOG241](#table-analog241) (1 × 8)
- [ANALOG242](#table-analog242) (1 × 8)
- [ANALOG243](#table-analog243) (1 × 8)
- [ANALOG244](#table-analog244) (1 × 8)
- [ANALOG245](#table-analog245) (1 × 8)
- [ANALOG246](#table-analog246) (1 × 8)
- [ANALOG247](#table-analog247) (1 × 8)
- [ANALOG248](#table-analog248) (1 × 8)
- [ANALOG249](#table-analog249) (1 × 8)
- [ANALOG250](#table-analog250) (1 × 8)
- [ANALOG251](#table-analog251) (1 × 8)
- [ANALOG252](#table-analog252) (1 × 8)
- [ANALOG253](#table-analog253) (1 × 8)
- [ANALOG254](#table-analog254) (1 × 8)
- [ANALOG255](#table-analog255) (1 × 8)
- [ANALOG256](#table-analog256) (1 × 8)
- [ANALOG257](#table-analog257) (1 × 8)
- [ANALOG258](#table-analog258) (1 × 8)
- [ANALOG259](#table-analog259) (1 × 8)
- [ANALOG260](#table-analog260) (1 × 8)
- [ANALOG261](#table-analog261) (1 × 8)
- [ANALOG262](#table-analog262) (1 × 8)
- [ANALOG263](#table-analog263) (1 × 8)
- [ANALOG264](#table-analog264) (1 × 8)
- [ANALOG265](#table-analog265) (1 × 8)
- [ANALOG266](#table-analog266) (1 × 8)
- [ANALOG267](#table-analog267) (1 × 8)
- [ANALOG268](#table-analog268) (1 × 8)
- [ANALOG269](#table-analog269) (1 × 8)
- [ANALOG270](#table-analog270) (1 × 8)
- [ANALOG271](#table-analog271) (1 × 8)
- [ANALOG272](#table-analog272) (1 × 8)
- [ANALOG273](#table-analog273) (1 × 8)
- [ANALOG274](#table-analog274) (1 × 8)
- [ANALOG275](#table-analog275) (1 × 8)
- [ANALOG276](#table-analog276) (1 × 8)
- [ANALOG277](#table-analog277) (1 × 8)
- [ANALOG278](#table-analog278) (1 × 8)
- [ANALOG279](#table-analog279) (1 × 8)
- [ANALOG280](#table-analog280) (1 × 8)
- [ANALOG281](#table-analog281) (1 × 8)
- [ANALOG282](#table-analog282) (1 × 8)
- [ANALOG283](#table-analog283) (1 × 8)
- [ANALOG284](#table-analog284) (1 × 8)
- [ANALOG285](#table-analog285) (1 × 8)
- [ANALOG286](#table-analog286) (1 × 8)
- [ANALOG287](#table-analog287) (1 × 8)
- [ANALOG288](#table-analog288) (1 × 8)
- [ANALOG289](#table-analog289) (1 × 8)
- [ANALOG290](#table-analog290) (1 × 8)
- [ANALOG291](#table-analog291) (1 × 8)
- [ANALOG292](#table-analog292) (1 × 8)
- [ANALOG293](#table-analog293) (1 × 8)
- [ANALOG294](#table-analog294) (1 × 8)
- [ANALOG295](#table-analog295) (1 × 8)
- [ANALOG296](#table-analog296) (1 × 8)
- [ANALOG297](#table-analog297) (1 × 8)
- [ANALOG298](#table-analog298) (1 × 8)
- [ANALOG299](#table-analog299) (1 × 8)
- [ANALOG300](#table-analog300) (1 × 8)
- [ANALOG301](#table-analog301) (1 × 8)
- [ANALOG302](#table-analog302) (1 × 8)
- [ANALOG303](#table-analog303) (1 × 8)
- [ANALOG304](#table-analog304) (1 × 8)
- [ANALOG305](#table-analog305) (1 × 8)
- [ANALOG306](#table-analog306) (1 × 8)
- [ANALOG307](#table-analog307) (1 × 8)
- [ANALOG308](#table-analog308) (1 × 8)
- [ANALOG309](#table-analog309) (1 × 8)
- [ANALOG310](#table-analog310) (1 × 8)
- [ANALOG311](#table-analog311) (1 × 8)
- [ANALOG312](#table-analog312) (1 × 8)
- [ANALOG313](#table-analog313) (1 × 8)
- [ANALOG314](#table-analog314) (1 × 8)
- [ANALOG315](#table-analog315) (1 × 8)
- [ANALOG316](#table-analog316) (1 × 8)
- [ANALOG317](#table-analog317) (1 × 8)
- [ANALOG318](#table-analog318) (1 × 8)
- [ANALOG319](#table-analog319) (1 × 8)
- [ANALOG320](#table-analog320) (1 × 8)
- [ANALOG321](#table-analog321) (1 × 8)
- [ANALOG322](#table-analog322) (1 × 8)
- [ANALOG323](#table-analog323) (1 × 8)
- [ANALOG324](#table-analog324) (1 × 8)
- [ANALOG325](#table-analog325) (1 × 8)
- [ANALOG326](#table-analog326) (1 × 8)
- [ANALOG327](#table-analog327) (1 × 8)
- [ANALOG328](#table-analog328) (1 × 8)
- [ANALOG329](#table-analog329) (1 × 8)
- [ANALOG330](#table-analog330) (1 × 8)
- [ANALOG331](#table-analog331) (1 × 8)
- [ANALOG332](#table-analog332) (1 × 8)
- [ANALOG333](#table-analog333) (1 × 8)
- [ANALOG334](#table-analog334) (1 × 8)
- [ANALOG335](#table-analog335) (1 × 8)
- [ANALOG336](#table-analog336) (1 × 8)
- [ANALOG337](#table-analog337) (1 × 8)
- [ANALOG338](#table-analog338) (1 × 8)
- [ANALOG339](#table-analog339) (1 × 8)
- [ANALOG340](#table-analog340) (1 × 8)
- [ANALOG341](#table-analog341) (1 × 8)
- [ANALOG342](#table-analog342) (1 × 8)
- [ANALOG343](#table-analog343) (1 × 8)
- [ANALOG344](#table-analog344) (1 × 8)
- [ANALOG345](#table-analog345) (1 × 8)
- [ANALOG346](#table-analog346) (1 × 8)
- [ANALOG347](#table-analog347) (1 × 8)
- [ANALOG348](#table-analog348) (1 × 8)
- [ANALOG349](#table-analog349) (1 × 8)
- [ANALOG350](#table-analog350) (1 × 8)
- [ANALOG351](#table-analog351) (1 × 8)
- [ANALOG352](#table-analog352) (1 × 8)
- [ANALOG353](#table-analog353) (1 × 8)
- [ANALOG354](#table-analog354) (1 × 8)
- [ANALOG355](#table-analog355) (1 × 8)
- [ANALOG356](#table-analog356) (1 × 8)
- [ANALOG357](#table-analog357) (1 × 8)
- [ANALOG358](#table-analog358) (1 × 8)
- [ANALOG359](#table-analog359) (1 × 8)
- [ANALOG360](#table-analog360) (1 × 8)
- [ANALOG361](#table-analog361) (1 × 8)
- [ANALOG362](#table-analog362) (1 × 8)
- [ANALOG363](#table-analog363) (1 × 8)
- [ANALOG364](#table-analog364) (1 × 8)
- [ANALOG365](#table-analog365) (1 × 8)
- [ANALOG366](#table-analog366) (1 × 8)
- [ANALOG367](#table-analog367) (1 × 8)
- [ANALOG368](#table-analog368) (1 × 8)
- [ANALOG369](#table-analog369) (1 × 8)
- [ANALOG370](#table-analog370) (1 × 8)
- [ANALOG371](#table-analog371) (1 × 8)
- [ANALOG372](#table-analog372) (1 × 8)
- [ANALOG373](#table-analog373) (1 × 8)
- [ANALOG374](#table-analog374) (1 × 8)
- [ANALOG375](#table-analog375) (1 × 8)
- [ANALOG376](#table-analog376) (1 × 8)
- [ANALOG377](#table-analog377) (1 × 8)
- [ANALOG378](#table-analog378) (1 × 8)
- [ANALOG379](#table-analog379) (1 × 8)
- [ANALOG380](#table-analog380) (1 × 8)
- [ANALOG381](#table-analog381) (1 × 8)
- [ANALOG382](#table-analog382) (1 × 8)
- [ANALOG383](#table-analog383) (1 × 8)
- [ANALOG384](#table-analog384) (1 × 8)
- [ANALOG385](#table-analog385) (1 × 8)
- [ANALOG386](#table-analog386) (1 × 8)
- [ANALOG387](#table-analog387) (1 × 8)
- [ANALOG388](#table-analog388) (1 × 8)
- [ANALOG389](#table-analog389) (1 × 8)
- [ANALOG390](#table-analog390) (1 × 8)
- [ANALOG391](#table-analog391) (1 × 8)
- [ANALOG392](#table-analog392) (1 × 8)
- [ANALOG393](#table-analog393) (1 × 8)
- [ANALOG394](#table-analog394) (1 × 8)
- [ANALOG395](#table-analog395) (1 × 8)
- [ANALOG396](#table-analog396) (1 × 8)
- [ANALOG397](#table-analog397) (1 × 8)
- [ANALOG398](#table-analog398) (1 × 8)
- [ANALOG399](#table-analog399) (1 × 8)
- [ANALOG400](#table-analog400) (1 × 8)
- [ANALOG401](#table-analog401) (1 × 8)
- [ANALOG402](#table-analog402) (1 × 8)
- [ANALOG403](#table-analog403) (1 × 8)
- [ANALOG404](#table-analog404) (1 × 8)
- [ANALOG405](#table-analog405) (1 × 8)
- [ANALOG406](#table-analog406) (1 × 8)
- [ANALOG407](#table-analog407) (1 × 8)
- [ANALOG408](#table-analog408) (1 × 8)
- [ANALOG409](#table-analog409) (1 × 8)
- [ANALOG410](#table-analog410) (1 × 8)
- [ANALOG411](#table-analog411) (1 × 8)
- [ANALOG412](#table-analog412) (1 × 8)
- [ANALOG413](#table-analog413) (1 × 8)
- [ANALOG414](#table-analog414) (1 × 8)
- [ANALOG415](#table-analog415) (1 × 8)
- [ANALOG416](#table-analog416) (1 × 8)
- [ANALOG417](#table-analog417) (1 × 8)
- [ANALOG418](#table-analog418) (1 × 8)
- [ANALOG419](#table-analog419) (1 × 8)
- [ANALOG420](#table-analog420) (1 × 8)
- [ANALOG421](#table-analog421) (1 × 8)
- [ANALOG422](#table-analog422) (1 × 8)
- [ANALOG423](#table-analog423) (1 × 8)
- [ANALOG424](#table-analog424) (1 × 8)
- [ANALOG425](#table-analog425) (1 × 8)
- [ANALOG426](#table-analog426) (1 × 8)
- [ANALOG427](#table-analog427) (1 × 8)
- [ANALOG428](#table-analog428) (1 × 8)
- [ANALOG429](#table-analog429) (1 × 8)
- [ANALOG430](#table-analog430) (1 × 8)
- [ANALOG431](#table-analog431) (1 × 8)
- [ANALOG432](#table-analog432) (1 × 8)
- [ANALOG433](#table-analog433) (1 × 8)
- [ANALOG434](#table-analog434) (1 × 8)
- [ANALOG435](#table-analog435) (1 × 8)
- [ANALOG436](#table-analog436) (1 × 8)
- [ANALOG437](#table-analog437) (1 × 8)
- [ANALOG438](#table-analog438) (1 × 8)
- [ANALOG439](#table-analog439) (1 × 8)
- [ANALOG440](#table-analog440) (1 × 8)
- [ANALOG441](#table-analog441) (1 × 8)
- [ANALOG442](#table-analog442) (1 × 8)
- [ANALOG443](#table-analog443) (1 × 8)
- [ANALOG444](#table-analog444) (1 × 8)
- [ANALOG445](#table-analog445) (1 × 8)
- [ANALOG446](#table-analog446) (1 × 8)
- [ANALOG447](#table-analog447) (1 × 8)
- [ANALOG448](#table-analog448) (1 × 8)
- [ANALOG449](#table-analog449) (1 × 8)
- [ANALOG450](#table-analog450) (1 × 8)
- [ANALOG451](#table-analog451) (1 × 8)
- [ANALOG452](#table-analog452) (1 × 8)
- [ANALOG453](#table-analog453) (1 × 8)
- [ANALOG454](#table-analog454) (1 × 8)
- [ANALOG455](#table-analog455) (1 × 8)
- [ANALOG456](#table-analog456) (1 × 8)
- [ANALOG457](#table-analog457) (1 × 8)
- [ANALOG458](#table-analog458) (1 × 8)
- [ANALOG459](#table-analog459) (1 × 8)
- [ANALOG460](#table-analog460) (1 × 8)
- [ANALOG461](#table-analog461) (1 × 8)
- [ANALOG462](#table-analog462) (1 × 8)
- [ANALOG463](#table-analog463) (1 × 8)
- [ANALOG464](#table-analog464) (1 × 8)
- [ANALOG465](#table-analog465) (1 × 8)
- [ANALOG466](#table-analog466) (1 × 8)
- [ANALOG467](#table-analog467) (1 × 8)
- [ANALOG468](#table-analog468) (1 × 8)
- [ANALOG469](#table-analog469) (1 × 8)
- [ANALOG470](#table-analog470) (1 × 8)
- [ANALOG471](#table-analog471) (1 × 8)
- [ANALOG472](#table-analog472) (1 × 8)
- [ANALOG473](#table-analog473) (1 × 8)
- [ANALOG474](#table-analog474) (1 × 8)
- [ANALOG475](#table-analog475) (1 × 8)
- [ANALOG476](#table-analog476) (1 × 8)
- [ANALOG477](#table-analog477) (1 × 8)
- [ANALOG478](#table-analog478) (1 × 8)
- [ANALOG479](#table-analog479) (1 × 8)
- [ANALOG480](#table-analog480) (1 × 8)
- [ANALOG481](#table-analog481) (1 × 8)
- [ANALOG482](#table-analog482) (1 × 8)
- [ANALOG483](#table-analog483) (1 × 8)
- [ANALOG484](#table-analog484) (1 × 8)
- [ANALOG485](#table-analog485) (1 × 8)
- [ANALOG486](#table-analog486) (1 × 8)
- [ANALOG487](#table-analog487) (1 × 8)
- [ANALOG488](#table-analog488) (1 × 8)
- [ANALOG489](#table-analog489) (1 × 8)
- [ANALOG490](#table-analog490) (1 × 8)
- [ANALOG491](#table-analog491) (1 × 8)
- [ANALOG492](#table-analog492) (1 × 8)
- [ANALOG493](#table-analog493) (1 × 8)
- [ANALOG494](#table-analog494) (1 × 8)
- [ANALOG495](#table-analog495) (1 × 8)
- [ANALOG496](#table-analog496) (1 × 8)
- [ANALOG497](#table-analog497) (1 × 8)
- [ANALOG498](#table-analog498) (1 × 8)
- [ANALOG499](#table-analog499) (1 × 8)
- [ANALOG500](#table-analog500) (1 × 8)
- [ANALOG501](#table-analog501) (1 × 8)
- [ANALOG502](#table-analog502) (1 × 8)
- [ANALOG503](#table-analog503) (1 × 8)
- [ANALOG504](#table-analog504) (1 × 8)
- [ANALOG505](#table-analog505) (1 × 8)
- [ANALOG506](#table-analog506) (1 × 8)
- [ANALOG507](#table-analog507) (1 × 8)
- [ANALOG508](#table-analog508) (1 × 8)
- [ANALOG509](#table-analog509) (1 × 8)
- [ANALOG510](#table-analog510) (1 × 8)
- [ANALOG511](#table-analog511) (1 × 8)
- [ANALOG512](#table-analog512) (1 × 8)
- [ANALOG513](#table-analog513) (1 × 8)
- [ANALOG514](#table-analog514) (1 × 8)
- [ANALOG515](#table-analog515) (1 × 8)
- [ANALOG516](#table-analog516) (1 × 8)
- [ANALOG517](#table-analog517) (1 × 8)
- [ANALOG518](#table-analog518) (1 × 8)
- [ANALOG519](#table-analog519) (1 × 8)
- [ANALOG520](#table-analog520) (1 × 8)
- [ANALOG521](#table-analog521) (1 × 8)
- [ANALOG522](#table-analog522) (1 × 8)
- [ANALOG523](#table-analog523) (1 × 8)
- [ANALOG524](#table-analog524) (1 × 8)
- [ANALOG525](#table-analog525) (1 × 8)
- [ANALOG526](#table-analog526) (1 × 8)
- [ANALOG527](#table-analog527) (1 × 8)
- [ANALOG528](#table-analog528) (1 × 8)
- [ANALOG529](#table-analog529) (1 × 8)
- [ANALOG530](#table-analog530) (1 × 8)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [EWSEMPFANGSSTATUS](#table-ewsempfangsstatus) (12 × 2)
- [EWSSTART](#table-ewsstart) (5 × 2)
- [JOBRESULT](#table-jobresult) (86 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 4 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0D | KWP2000* |
| 0x0C | KWP2000 |
| 0x06 | DS2 |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 56 rows × 2 columns

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
| 0x55 | BHTC |
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

<a id="table-abgleich"></a>
### ABGLEICH

Dimensions: 26 rows × 6 columns

| LABEL | TEXT | LID | BYTES | FACT_A | FACT_B |
| --- | --- | --- | --- | --- | --- |
| AGR | Abgasrueckfuehrung | 0xA4 | 2 | 0,1 | 0,0 |
| BEG | Begrenzungsmoment | 0xA2 | 2 | 0,01220703125 | 0,0 |
| FGRKLI | FGR/Klimaanlage | 0xCC | 1 | 1,0 | 0,0 |
| FGRMAIN | FGR/Mainswitch | 0xA8 | 1 | 1,0 | 0,0 |
| HFMKORR | HFM-Luftmasse nach korr. | 0xAD | 2 | 0,1 | 0,0 |
| HFMLASTGRENZ | HFM-Last Grenzwert | 0xBE | 2 | 0,1 | 0,0 |
| HFMLAST | HFM-Lastabgleich | 0xAF | 2 | 1,220703125 | 0,0 |
| HFMLLGRENZ | HFM Leerlauf Grenzwert | 0xBF | 2 | 0,1 | 0,0 |
| HFMLL | HFM Leerlaufabgleich | 0xAE | 2 | 1,220703125 | 0,0 |
| RDR | Hochdruckregelungs-Modos | 0xBD | 1 | 1,0 | 0,0 |
| IMAALLE | IMA Alle Injektoren | 0xBB | 20 | 0,0 | 0,0 |
| IMA1 | IMA Injektor 1 | 0xB5 | 5 | 0,0 | 0,0 |
| IMA2 | IMA Injektor 2 | 0xB6 | 5 | 0,0 | 0,0 |
| IMA3 | IMA Injektor 3 | 0xB7 | 5 | 0,0 | 0,0 |
| IMA4 | IMA Injektor 4 | 0xB8 | 5 | 0,0 | 0,0 |
| IMA5 | IMA Injektor 5 | 0xB9 | 5 | 0,0 | 0,0 |
| IMA6 | IMA Injektor 6 | 0xBA | 5 | 0,0 | 0,0 |
| IMAFLAG | IMA Programmiert Flag | 0xBC | 1 | 1,0 | 0,0 |
| KLIMA | Klimakompressorabgleich | 0xB1 | 2 | 0,01220703125 | 0,0 |
| LLA | Leerlaufdrehzahl | 0xA3 | 2 | 1,0 | 0,0 |
| MEN48 | Mengenabgleich 48 Pkt. | 0xAA | 48 | 0,01 | 0,0 |
| MENDRIFT | Mengendriftkompensation | 0xA6 | 2 | 0,01 | 0,0 |
| SER | Serviceabgleich | 0xA5 | 2 | 0,01220703125 | 0,0 |
| STA | Startmoment | 0xA1 | 2 | 0,01 | 0,0 |
| VER | Verbrauchskennlinie | 0xB0 | 2 | 0,01220703125 | 0,0 |
| -- |  | 0x00 | 0 | 0,0 | 0,0 |

<a id="table-steller"></a>
### STELLER

Dimensions: 12 rows × 6 columns

| LABEL | TEXT | LID | BYTES | FACT_A | FACT_B |
| --- | --- | --- | --- | --- | --- |
| AGR | Abgasrueckfuehrung | 0xC2 | 2 | 0,01 | 0,0 |
| ADD | Additivdosierpumpe | 0xC9 | 1 | 1,0 | 0,0 |
| DRA | Drallklappe | 0xCE | 2 | 0,01 | 0,0 |
| GLU | Gluehrelais | 0xC4 | 1 | 1,0 | 0,0 |
| KLI | Klimakompressor | 0xC5 | 1 | 1,0 | 0,0 |
| DRV | Kraftstoffdruck-Regelventil | 0xD0 | 2 | 0,01 | 0,0 |
| LDS | Ladedruckstelle | 0xC6 | 2 | 0,01 | 0,0 |
| ELU | Motorluefter | 0xC7 | 2 | 0,01 | 0,0 |
| VFP | Vorfoederpumpe | 0xC3 | 1 | 1,0 | 0,0 |
| MRV | Zumesseinheit | 0xCF | 2 | 0,01 | 0,0 |
| ZUH | Zusatzheizer | 0xCB | 2 | 0,01 | 0,0 |
| -- |  | 0x00 | 0 | 0,0 | 0,0 |

<a id="table-dig-mfl"></a>
### DIG_MFL

Dimensions: 4 rows × 10 columns

| TELNAME | TELEGRAMM | NAME | ERGEBNIS | BYTE | MASK | VALUE | LNAME | TEXT_1 | TEXT_0 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CrCCD_stKey | 00D0 | S_MFLEINP | STAT_MFLEINP_WERT | 3 | 0x01 | 0x01 | MFL Bedienteil Taste + | betaetigt | nicht betaetigt |
| CrCCD_stKey | 00D0 | S_MFLEINM | STAT_MFLEINM_WERT | 3 | 0x02 | 0x02 | MFL Bedienteil Taste - | betaetigt | nicht betaetigt |
| CrCCD_stKey | 00D0 | S_MFLWA | STAT_MFLWA_WERT | 3 | 0x04 | 0x04 | MFL Bedienteil Taste Wiederaufnahme | betaetigt | nicht betaetigt |
| CrCCD_stKey | 00D0 | S_MFLAUS | STAT_MFLAUS_WERT | 3 | 0x08 | 0x08 | MFL Bedienteil Taste AUS | betaetigt | nicht betaetigt |

<a id="table-dig-fgr-aus"></a>
### DIG_FGR_AUS

Dimensions: 23 rows × 10 columns

| TELNAME | TELEGRAMM | NAME | ERGEBNIS | BYTE | MASK | VALUE | LNAME | TEXT_1 | TEXT_0 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CrCtl_stShutOffCode1_mp | 00F000F2 | S_RFGRABS | STAT_RFGRABS_WERT | 3 | 0x01 | 0x01 | Ausschalter aktiv  (Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode1_mp | 00F0 | S_RFGRGNRA | STAT_RFGRGNRA_WERT | 3 | 0x02 | 0x02 | zu grosse neg. Regelabweichung (Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode1_mp | 00F0 | S_RFGRLNLA | STAT_RFGRLNLA_WERT | 3 | 0x04 | 0x04 | zu lange neg. Regelabweichung (Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode1_mp | 00F0 | S_RFGRPRA | STAT_RFGRPRA_WERT | 3 | 0x08 | 0x08 | zu grosse pos. Regelabweichung (Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode1_mp | 00F0 | S_RFGRVMN | STAT_RFGRVMN_WERT | 3 | 0x10 | 0x10 | Geschwindigkeit zu klein (Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode1_mp | 00F0 | S_RFGRBRK | STAT_RFGRBRK_WERT | 3 | 0x01 | 0x01 | Bremse betaetigt (Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode1_mp | 00F0 | S_RFGRKUP | STAT_RFGRKUP_WERT | 2 | 0x02 | 0x02 | Kupplung betaetigt (Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode1_mp | 00F0 | S_RFGRNMAX | STAT_RFGRNMAX_WERT | 2 | 0x04 | 0x04 | Drehzahlgrenze überschritten (Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode1_mp | 00F0 | S_RFGRNMIN | STAT_RFGRNMIN_WERT | 2 | 0x08 | 0x08 | Drehzahlgrenze unterschritten (Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode1_mp | 00F0 | S_RFGRUEB | STAT_RFGRUEB_WERT | 2 | 0x10 | 0x10 | Geschwindigkeit zu gross (Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode1_mp | 00F0 | S_RFGRGNG | STAT_RFGRGNG_WERT | 2 | 0x20 | 0x20 | kein gueltiger Gang (Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode1_mp | 00F0 | S_RFGRMOT | STAT_RFGRMOT_WERT | 2 | 0x40 | 0x40 | Motorzustand nicht normal (Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode1_mp | 00F0 | S_RFGRSCH | STAT_RFGRSCH_WERT | 2 | 0x80 | 0x80 | v/n Änderung gegenüber Start(Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode2_mp | 00F2 | S_RFGRVNM | STAT_RFGRVNM_WERT | 5 | 0x01 | 0x01 | durch Hochdrehen(Schlupf)(Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode2_mp | 00F2 | S_RFGRBRE | STAT_RFGRBRE_WERT | 5 | 0x02 | 0x02 | Bremsüberprüfung (Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode2_mp | 00F2 | S_RFGRAQUA | STAT_RFGRAQUA_WERT | 5 | 0x04 | 0x04 | Aquaplaning(Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode2_mp | 00F2 | S_RFGRDSC | STAT_RFGRDSC_WERT | 5 | 0x08 | 0x08 | Bremseingriff DSC (Reversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode2_mp | 00F2 | S_IOPT | STAT_IOPT_WERT | 4 | 0x01 | 0x01 | FGR n. variantencodiert/verbaut (Irreversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode2_mp | 00F2 | S_IKOMPO | STAT_IKOMPO_WERT | 4 | 0x02 | 0x02 | Komponentendefekt (Irreversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode2_mp | 00F2 | S_IBUMM | STAT_IBUMM_WERT | 4 | 0x04 | 0x04 | Aufprall erkannt (Irreversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode2_mp | 00F2 | S_IBREMAX | STAT_IBREMAX_WERT | 4 | 0x08 | 0x08 | starkes Bremsen (Irreversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode2_mp | 00F2 | S_IAMAX | STAT_IAMAX_WERT | 4 | 0x10 | 0x10 | starke Beschleunigung (Irreversible Abschaltbdg) | aktiv | nicht aktiv |
| CrCtl_stShutOffCode2_mp | 00F2 | S_IFGRAUS | STAT_IFGRAUS_WERT | 4 | 0x80 | 0x80 | Irreversible Abschaltbdg | aktiv | nicht aktiv |

<a id="table-dig-kwh-aus"></a>
### DIG_KWH_AUS

Dimensions: 11 rows × 10 columns

| TELNAME | TELEGRAMM | NAME | ERGEBNIS | BYTE | MASK | VALUE | LNAME | TEXT_1 | TEXT_0 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AOHt_stShutOff_mp | 0099 | S_KWH_WTF | STAT_KWH_WTF_WERT | 3 | 0x01 | 0x01 | Wassertemperatur ausreichend (Abschaltbdg. AOHt) | aktiv | nicht aktiv |
| AOHt_stShutOff_mp | 0099 | S_KWH_GEN | STAT_KWH_GEN_WERT | 3 | 0x02 | 0x02 | Generatorfehler (Abschaltbdg. AOHt) | aktiv | nicht aktiv |
| AOHt_stShutOff_mp | 0099 | S_KWH_UBATT | STAT_KWH_UBATT_WERT | 3 | 0x04 | 0x04 | Batteriespannung zu niedrig (Abschaltbdg. AOHt) | aktiv | nicht aktiv |
| AOHt_stShutOff_mp | 0099 | S_KWH_N | STAT_KWH_N_WERT | 3 | 0x08 | 0x08 | Motordrehzahl zu niedrig (Abschaltbdg. AOHt) | aktiv | nicht aktiv |
| AOHt_stShutOff_mp | 0099 | S_KWH_START | STAT_KWH_A_WERT | 3 | 0x10 | 0x10 | Startverzoegerung aktiv (Abschaltbdg. AOHt) | aktiv | nicht aktiv |
| AOHt_stShutOff_mp | 0099 | S_KWH_SENSDEF | STAT_KWH_SENSDEF_WERT | 13 | 0x20 | 0x20 | WTF, UTF oder Endstufe defekt (Abschaltbdg. AOHt) | aktiv | nicht aktiv |
| AOHt_stShutOff_mp | 0099 | S_KWH_STEU | STAT_KWH_STEU_WERT | 3 | 0x40 | 0x40 | k. Anforderung von Steuerung (Abschaltbdg. AOHt) | aktiv | nicht aktiv |
| AOHt_stShutOff_mp | 0099 | S_KWH_AC | STAT_KWH_AC_WERT | 3 | 0x80 | 0x80 | k. Anforderung von AC (Abschaltbdg. AOHt) | aktiv | nicht aktiv |
| AOHt_stShutOff_mp | 0099 | S_KWH_ANF | STAT_KWH_ANF_WERT | 2 | 0x01 | 0x01 | Anfahrvorgang (Abschaltbdg. AOHt) | aktiv | nicht aktiv |
| AOHt_stShutOff_mp | 0099 | S_KWH_BE | STAT_KWH_BE_WERT | 2 | 0x02 | 0x02 | Beschleunugungswunsch (Abschaltbdg. AOHt) | aktiv | nicht aktiv |
| AOHt_stShutOff_mp | 0099 | S_KWH_SWT | STAT_KWH_SWT_WERT | 2 | 0x80 | 0x80 | Schalter AOHt_swtHtgActive=0 (Abschaltbdg. AOHt) | aktiv | nicht aktiv |

<a id="table-dig-agr-aus"></a>
### DIG_AGR_AUS

Dimensions: 20 rows × 10 columns

| TELNAME | TELEGRAMM | NAME | ERGEBNIS | BYTE | MASK | VALUE | LNAME | TEXT_1 | TEXT_0 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AirCtl_stAirCtlBits1_mp | 00410043003D | S_AGR_UKN | STAT_AGR_UKN_WERT | 15 | 0x01 | 0x01 | keine bestimmte Ursache (Abschaltursache AGR) | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_SUB | STAT_AGR_SUB_WERT | 3 | 0x02 | 0x02 | Schubbetrieb | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_SAL | STAT_AGR_SAL_WERT | 3 | 0x04 | 0x04 | Schaltvorgang | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_LL | STAT_AGR_LL_WERT | 3 | 0x08 | 0x08 | langer Leerlauf | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_REG | STAT_AGR_REG_WERT | 3 | 0x10 | 0x10 | Regeneration EGT | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_SYS | STAT_AGR_SYS_WERT | 3 | 0x20 | 0x20 | Systemfehler | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_RA | STAT_AGR_RA_WERT | 3 | 0x40 | 0x40 | bleibende Regelabweichung | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_NAT | STAT_AGR_NAT_WERT | 3 | 0x80 | 0x80 | zu niedriger Atmosphärendruck | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_NWT | STAT_AGR_NWT_WERT | 3 | 0x01 | 0x01 | zu niedrige Kühlwassertemperatur | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_HWT | STAT_AGR_HWT_WERT | 2 | 0x02 | 0x02 | zu hohe Kühlwassertemperatur | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_BAT | STAT_AGR_BAT_WERT | 2 | 0x04 | 0x04 | zu niedrige Batteriespannung | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_QMX | STAT_AGR_QMX_WERT | 2 | 0x08 | 0x08 | große Einspritzmenge | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_KLT | STAT_AGR_KLT_WERT | 2 | 0x10 | 0x10 | Kaltstart | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_NLT | STAT_AGR_NLT_WERT | 2 | 0x20 | 0x20 | zu niedrige Lufttemperatur | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_HLT | STAT_AGR_HLT_WERT | 2 | 0x40 | 0x40 | zu hohe Lufttemperatur | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits1_mp | 0041 | S_AGR_NIN | STAT_AGR_MIN_WERT | 2 | 0x80 | 0x80 | zu kleine Drehzahl | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits2_mp | 0043 | S_AGR_NMX | STAT_AGR_NMX_WERT | 5 | 0x01 | 0x01 | zu hohe Drehzahl | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits2_mp | 0043 | S_AGR_HFM | STAT_AGR_HFM_WERT | 5 | 0x02 | 0x02 | HFM Abgleich aktiv | aktiv | Abschaltbedingung nicht aktiv |
| AirCtl_stAirCtlBits2_mp | 0043 | S_AGR_KOO | STAT_AGR_KOO_WERT | 5 | 0x04 | 0x04 | Abschaltkoordinationsanforderung | aktiv | Abschaltbedingung nicht aktiv |
| ACCtl_stLogicOut | 003D | S_KLIMA_S | STAT_KLIMA_S_WERT | 7 | 0x01 | 0x01 | Klimakompressor AN / AUS | AUS | AN |

<a id="table-dig-mflkli"></a>
### DIG_MFLKLI

Dimensions: 2 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| B_MFL | 3 | 0x02 | 0x02 |
| B_KLI | 3 | 0x01 | 0x01 |

<a id="table-dig-allg"></a>
### DIG_ALLG

Dimensions: 11 rows × 10 columns

| TELNAME | TELEGRAMM | NAME | ERGEBNIS | BYTE | MASK | VALUE | LNAME | TEXT_0 | TEXT_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BrkCD_stMnSwtRawVal | 005C005D00C900CA005E00A000AF00D0 | S_BRL | STAT_BLS_EIN | 3 | 0x01 | 0x01 | Eingang Bremslichtschalter | Pedal nicht betaetigt (Masse) | Pedal betaetigt (Ubatt) |
| BrkCD_stRedSwtRawVal | 005C005D00C900CA005E00A000AF00D0 | S_BRT | STAT_BLTS_EIN | 5 | 0x01 | 0x01 | Eingang Bremslichttestschalter | Pedal nicht betaetigt (Masse) | Pedal betaetigt (Ubatt) |
| FrmMng_swtAC_mp | 005C005D00C900CA005E00A000AF00D0 | S_KO | STAT_KO_EIN | 7 | 0x01 | 0x01 | Schalter Klimaanforderung KO (CAN) | Oeldruck io (Ubatt) | Oeldruck zu niedrig (Masse) |
| FrmMng_swtACComp_mp | 005C005D00C900CA005E00A000AF00D0 | S_AC | STAT_AC_EIN | 9 | 0x01 | 0x01 | Schalter Klimabereitschaft AC (CAN) | nicht betaetigt | betaetigt |
| ConvCD_stRawVal | 005C005D00C900CA005E00A000AF00D0 | S_KUP | STAT_KUP_EIN | 11 | 0x01 | 0x01 | Eingang Kupplungsschalter | Pedal nicht betaetigt (Masse) | Pedal betaetigt (Ubatt) |
| Gearbx_swtType | 005C005D00C900CA005E00A000AF00D0 | S_EGS | STAT_GETRIEBEART_HAND_EIN | 13 | 0x01 | 0x01 | Getriebe | Handschalter | Automatik |
| OPSCD_stSigOut | 005C005D00C900CA005E00A000AF00D0 | S_ODS | STAT_ODS_EIN | 15 | 0x01 | 0x01 | Eingang Oeldruckschalter | Oeldruck io (Ubatt) | Oeldruck zu niedrig (Masse) |
| CrCCD_stKey | 005C005D00C900CA005E00A000AF00D0 | S_MFLEINP | STAT_MFLEINP_EIN | 17 | 0x01 | 0x01 | MFL Bedienteil Taste + | betaetigt | nicht betaetigt |
| CrCCD_stKey | 005C005D00C900CA005E00A000AF00D0 | S_MFLEINM | STAT_MFLEINM_EIN | 17 | 0x02 | 0x02 | MFL Bedienteil Taste - | betaetigt | nicht betaetigt |
| CrCCD_stKey | 005C005D00C900CA005E00A000AF00D0 | S_MFLWA | STAT_MFLWA_EIN | 17 | 0x04 | 0x04 | MFL Bedienteil Taste Wiederaufnahme | betaetigt | nicht betaetigt |
| CrCCD_stKey | 005C005D00C900CA005E00A000AF00D0 | S_MFLAUS | STAT_MFLAUS_EIN | 17 | 0x08 | 0x08 | MFL Bedienteil Taste AUS | betaetigt | nicht betaetigt |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 12 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxxx0 | 10 | --                                                                    |
| xxxxxxx1 | 11 | Diagnose aktiv            |
| xxxxxx0x | 20 | --                                                                    |
| xxxxxx1x | 21 | Diagnose gestoppt         |
| xxxxx0xx | 30 | --                                                                    |
| xxxxx1xx | 31 | Zyklus-Flag gesetzt       |
| xxxx0xxx | 40 | --                                                                    |
| xxxx1xxx | 41 | Error-Flag gesetzt        |
| xxx0xxxx | 50 | --                                                                    |
| xxx1xxxx | 51 | MIL ein                   |
| xx0xxxxx | 60 | --                                                                    |
| xx1xxxxx | 61 | Fehler in Entprellphase   |

<a id="table-betriebswtab"></a>
### BETRIEBSWTAB

Dimensions: 215 rows × 17 columns

| NAME | TELEGRAM | POS_ADR | LEN_ADR | ADR | BYTE | DATA_TYPE | COMPU_TYPE | FACT_A | FACT_B | MASK | VALUE | ANZ | MEAS | RANGE | JOBNAME | LNAME |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CoEng_rTrq | B812F1042C100000 | 07 | 1 | 0x04 | 06 | 5 | -- | 3.11E-02 | 0 | 0 | 0 | 6.2f | % |  | CoEng_rTrq | Verhältnis aktuelles Moment zu Maximalmoment |
| CTSCD_tClntLin | B812F1042C100000 | 07 | 1 | 0x05 | 06 | 5 | -- | 1.00 | -41.0 | 0 | 0 | 6.2f | deg C |  | CTSCD_tClntLin | linearisierter Wert aus HWK vorm Aufruf der Übergangsfunktion |
| BPSCD_pLin | B812F1042C100000 | 07 | 1 | 0x0B | 06 | 5 | -- | 9.84 | 0 | 0 | 0 | 6.2f | hPa |  | BPSCD_pLin | Mittelere Ladedruck-Wert (liniarisiert) |
| Eng_nAvrg | B812F1042C100000 | 07 | 1 | 0x0C | 06 | 5 | -- | 4 | 0 | 0 | 0 | 6.2f | rpm |  | Eng_nAvrg | mittlere Motordrehzahl |
| VSSCD_v | B812F1042C100000 | 07 | 1 | 0x0D | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | km/h |  | VSSCD_v | Fahrzeuggeschwindigkeit |
| IATSCD_tAirLin | B812F1042C100000 | 07 | 1 | 0x0F | 06 | 5 | -- | 1.00 | -41.0 | 0 | 0 | 6.2f | deg C |  | IATSCD_tAirLin | linearisierter Wert aus HWK vorm Aufruf der Übergangsfunktion |
| AFSCD_dmAirRawPerTime | B812F1042C100000 | 07 | 1 | 0x10 | 06 | 5 | -- | 9.99 | 0 | 0 | 0 | 6.2f | Kg/h |  | AFSCD_dmAirRawPerTime | LMM Luftmassenmesser HFM |
| Signals_PID0x1C_C | B812F1042C100000 | 07 | 1 | 0x1C | 06 | 5 | -- | 0 | 0 | 0 | 0 | 6.2f | - |  | Signals_PID0x1C_C | Info für Generic Scan Tool (OBD-Tester) für welche Vorschrift das Fahrzeug appliziert wurde |
| DSM_stSysLamp | B812F1042C100000 | 07 | 1 | 0x29 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | DSM_stSysLamp | DSM System Lampen Anforderungsstatus (1 = kontinuierlich) |
| DSM_stMIL | B812F1042C100000 | 07 | 1 | 0x2A | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | DSM_stMIL | DSM Mil Anforderungsstatus (1 = kontinuierlich, 2 blinkend) |
| CTSCD_uRaw | B812F1042C100000 | 07 | 1 | 0x2B | 06 | 5 | -- | 0.610 | 0 | 0 | 0 | 6.2f | mV |  | CTSCD_uRaw | Wassertemperatur Spannungsrohwert |
| CTSCD_tClnt | B812F1042C100000 | 07 | 1 | 0x2C | 06 | 5 | -- | 0.016 | -50.1 | 0 | 0 | 6.2f | deg C |  | CTSCD_tClnt | Kühlmitteltemperatur |
| Eng_nAvrg | B812F1042C100000 | 07 | 1 | 0x2D | 06 | 5 | -- | 0.125 | 0 | 0 | 0 | 6.2f | rpm |  | Eng_nAvrg | mittlere Motordrehzahl |
| AFSCD_dmAirPerTime | B812F1042C100000 | 07 | 1 | 0x2E | 06 | 5 | -- | 4.88E-02 | -1599. | 0 | 0 | 6.2f | Kg/h |  | AFSCD_dmAirPerTime | MLt Luftmassenstrom n. Liniarisierung + Mittelung |
| BattCD_u | B812F1042C100000 | 07 | 1 | 0x2F | 06 | 5 | -- | 0.00245 | 0 | 0 | 0 | 6.2f | V |  | BattCD_u | Batteriespannung |
| LIGov_nSetpoint | B812F1042C100000 | 07 | 1 | 0x31 | 06 | 5 | -- | 0.125 | 0 | 0 | 0 | 6.2f | rpm |  | LIGov_nSetpoint | Leerlauf Solldrehzahl |
| VSSCD_v | B812F1042C100000 | 07 | 1 | 0x32 | 06 | 5 | -- | 3.81E-03 | 0 | 0 | 0 | 6.2f | km/h |  | VSSCD_v | Fahrzeuggeschwindigkeit |
| VSSCD_a | B812F1042C100000 | 07 | 1 | 0x33 | 06 | 5 | -- | 3.05E-04 | -9.99 | 0 | 0 | 6.2f | m/s^2 |  | VSSCD_a | Fahrbeschleunigung |
| InjCtl_qSet | B812F1042C100000 | 07 | 1 | 0x34 | 06 | 5 | -- | 3.05E-03 | -99.9 | 0 | 0 | 6.2f | mg/cyc |  | InjCtl_qSet | Einspritzmenge Sollwert |
| Rail_dvolMeUnSet | B812F1042C100000 | 07 | 1 | 0x35 | 06 | 5 | -- | 10 | 0 | 0 | 0 | 6.2f | mm3/s |  | Rail_dvolMeUnSet | Sollwert (Volumenstrom) von der Raildruckregelung |
| IATSCD_tAirCats | B812F1042C100000 | 07 | 1 | 0x36 | 06 | 5 | -- | 0.016 | -50.1 | 0 | 0 | 6.2f | deg C |  | IATSCD_tAirCats | Ladelufttemperatur nach Ladeluftkühler |
| IATSCD_uRaw | B812F1042C100000 | 07 | 1 | 0x37 | 06 | 5 | -- | 0.610 | 0 | 0 | 0 | 6.2f | mV |  | IATSCD_uRaw | Lufttemperatur Spannungsrohwert |
| IATSCD_tAir | B812F1042C100000 | 07 | 1 | 0x38 | 06 | 5 | -- | 0.016 | -50.1 | 0 | 0 | 6.2f | deg C |  | IATSCD_tAir | Ansauglufttemperatur |
| BPSCD_uRawVal | B812F1042C100000 | 07 | 1 | 0x39 | 06 | 5 | -- | 0.610 | 0 | 0 | 0 | 6.2f | mV |  | BPSCD_uRawVal | Spannungsrohwert des Ladedrucksensors |
| BPSCD_pOutVal | B812F1042C100000 | 07 | 1 | 0x3A | 06 | 5 | -- | 0.125 | 0 | 0 | 0 | 6.2f | hPa |  | BPSCD_pOutVal | Ladedruckwert |
| T15CD_stWakeUpRawVal_mp | B812F1042C100000 | 07 | 1 | 0x3B | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | T15CD_stWakeUpRawVal_mp | Rohwert des Wake Up Signals aus der HWE |
| AccPed_trqDes | B812F1042C100000 | 07 | 1 | 0x3C | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | AccPed_trqDes | Fahrerwunsch Rohwert |
| AccPed_trqDes | B812F1042C100000 | 07 | 1 | 0x3D | 06 | 5 | -- | 0.228 | -5000. | 0 | 0 | 6.2f | Nm |  | AccPed_trqDes | Fahrerwunsch Rohwert |
| AddPCD_stCo_mp | B812F1042C100000 | 07 | 1 | 0x3E | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | AddPCD_stCo_mp | Status Additivpumpen-Komponententreiber |
| AddPCD_volAddTotFine_mp | B812F1042C100000 | 07 | 1 | 0x3F | 06 | 5 | -- | 0.001 | 0 | 0 | 0 | 6.2f | ml |  | AddPCD_volAddTotFine_mp | Eingespritztes Gesamt-Additivvolumen (feine Auflösung) |
| AddPmp_volAddTotDem | B812F1042C100000 | 07 | 1 | 0x40 | 06 | 5 | -- | 1.25E-02 | 0 | 0 | 0 | 6.2f | ml |  | AddPmp_volAddTotDem | Angefordertes Gesamt-Additivvolumen |
| AirCtl_stAirCtlBits1_mp | B812F1042C100000 | 07 | 1 | 0x41 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | AirCtl_stAirCtlBits1_mp | AirCtl_stAirCtlBits_mp LowByte (-&gt;Signals) |
| AirCtl_stAirCtlBits1_mp | B812F1042C100000 | 07 | 1 | 0x42 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | AirCtl_stAirCtlBits1_mp | AirCtl_stAirCtlBits_mp LowByte (-&gt;Signals) |
| AirCtl_stAirCtlBits2_mp | B812F1042C100000 | 07 | 1 | 0x43 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | AirCtl_stAirCtlBits2_mp | AirCtl_stAirCtlBits_mp HighByte (-&gt;Signals) |
| AirCtl_stAirCtlBits2_mp | B812F1042C100000 | 07 | 1 | 0x44 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | AirCtl_stAirCtlBits2_mp | AirCtl_stAirCtlBits_mp HighByte (-&gt;Signals) |
| MeUn_iSet_mp | B812F1042C100000 | 07 | 1 | 0x45 | 06 | 5 | -- | 0.228 | 0 | 0 | 0 | 6.2f | mA |  | MeUn_iSet_mp | Sollstrom für die Zumesseinheit |
| ACCtl_stShutOff_mp | B812F1042C100000 | 07 | 1 | 0x46 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | ACCtl_stShutOff_mp | letzter Abschalgrund Klimakompressor |
| ACCtl_stShutOff_mp | B812F1042C100000 | 07 | 1 | 0x47 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | ACCtl_stShutOff_mp | letzter Abschalgrund Klimakompressor |
| APPCD_rLinAPP1 | B812F1042C100000 | 07 | 1 | 0x48 | 06 | 5 | -- | 3.05E-03 | 0 | 0 | 0 | 6.2f | % |  | APPCD_rLinAPP1 | linearisierter APP1 |
| APPCD_rLinAPP2 | B812F1042C100000 | 07 | 1 | 0x49 | 06 | 5 | -- | 3.05E-03 | 0 | 0 | 0 | 6.2f | % |  | APPCD_rLinAPP2 | Linearisierter APP2 |
| FlSys_volDetRefuel | B812F1042C100000 | 07 | 1 | 0x4A | 06 | 5 | -- | 0.05 | 0 | 0 | 0 | 6.2f | l |  | FlSys_volDetRefuel | Nachgetankte Kraftstoffmenge |
| FlSys_volTotalRef_mp | B812F1042C100000 | 07 | 1 | 0x4C | 06 | 5 | -- | 0.05 | 0 | 0 | 0 | 6.2f | l |  | FlSys_volTotalRef_mp | Referenzsignal des Tankfüllstands |
| PCR_stMonitor | B812F1042C100000 | 07 | 1 | 0x4D | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | PCR_stMonitor | Statusangabe bei Abschaltung der Regelung |
| PFlt_dvol | B812F1042C100000 | 07 | 1 | 0x4E | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | m^3/h |  | PFlt_dvol | berechneter Abgasvolumsstrom |
| PFlt_facMltCor_mp | B812F1042C100000 | 07 | 1 | 0x4F | 06 | 5 | -- | 0.000 | 0 | 0 | 0 | 6.2f | - |  | PFlt_facMltCor_mp | Korrekturfaktor Additivasche |
| AFSCD_mAirPerCyl | B812F1042C100000 | 07 | 1 | 0x50 | 06 | 5 | -- | 4.88E-02 | -1599. | 0 | 0 | 6.2f | mg/Hub |  | AFSCD_mAirPerCyl | angesaugte Luftmasse pro Zylinder |
| AFSCD_dmAirNorm | B812F1042C100000 | 07 | 1 | 0x52 | 06 | 5 | -- | 4.88E-02 | -1599. | 0 | 0 | 6.2f | Kg/h |  | AFSCD_dmAirNorm | Normalisierte Luftmasse |
| PFlt_lSum_mp | B812F1042C100000 | 07 | 1 | 0x53 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | m |  | PFlt_lSum_mp | ges. gefahrene Strecke bei der letzten erfolgr. Regeneration |
| PFlt_pDiff | B812F1042C100000 | 07 | 1 | 0x54 | 06 | 5 | -- | 0.125 | 0 | 0 | 0 | 6.2f | hPa |  | PFlt_pDiff | Differenzdruck über Partikelfilter |
| InjCtl_qCurr | B812F1042C100000 | 07 | 1 | 0x55 | 06 | 5 | -- | 3.05E-03 | -99.9 | 0 | 0 | 6.2f | mg/cyc |  | InjCtl_qCurr | Einspritzmenge aktueller Wert |
| AirCtl_mGvnrDvt | B812F1042C100000 | 07 | 1 | 0x56 | 06 | 5 | -- | 4.88E-02 | -1599. | 0 | 0 | 6.2f | mg/Hub |  | AirCtl_mGvnrDvt | Regelabweichung |
| AirCtl_rEGR | B812F1042C100000 | 07 | 1 | 0x57 | 06 | 5 | -- | 3.05E-03 | 0 | 0 | 0 | 6.2f | % |  | AirCtl_rEGR | Stellgröße für das ARF-Ventil |
| IndSys_rVSA | B812F1042C100000 | 07 | 1 | 0x58 | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | % |  | IndSys_rVSA | Sollposition für Einlaßkanalabschaltung |
| PCR_rBPA | B812F1042C100000 | 07 | 1 | 0x59 | 06 | 5 | -- | 3.05E-03 | 0 | 0 | 0 | 6.2f | % |  | PCR_rBPA | Stellgröße für den Ladedrucksteller |
| OTSCD_tEngOil | B812F1042C100000 | 07 | 1 | 0x5A | 06 | 5 | -- | 0.016 | -50.1 | 0 | 0 | 6.2f | deg C |  | OTSCD_tEngOil | Motoröltemperatur |
| FTSCD_tFuel | B812F1042C100000 | 07 | 1 | 0x5B | 06 | 5 | -- | 0.016 | -50.1 | 0 | 0 | 6.2f | deg C |  | FTSCD_tFuel | Kraftstofftemperatur |
| BrkCD_stMnSwtRawVal | B812F1042C100000 | 07 | 1 | 0x5C | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | BrkCD_stMnSwtRawVal | Rohwert Bremskontakt nicht entprellt |
| BrkCD_stRedSwtRawVal | B812F1042C100000 | 07 | 1 | 0x5D | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | BrkCD_stRedSwtRawVal | Rohwert redundanter Bremskontakt nicht entprellt |
| ConvCD_stRawVal | B812F1042C100000 | 07 | 1 | 0x5E | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | ConvCD_stRawVal | Kupplungssignal Rohwert |
| GlwCtl_stLampOut | B812F1042C100000 | 07 | 1 | 0x61 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | GlwCtl_stLampOut | Zustand der Glühanzeige |
| EBAFCD_stSigOut | B812F1042C100000 | 07 | 1 | 0x62 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | EBAFCD_stSigOut | Airwalvecontrol |
| PFlt_stEngPOp5_mp | B812F1042C100000 | 07 | 1 | 0x63 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | PFlt_stEngPOp5_mp | Motorbetriebspunkt berechnet in Check Range 5 |
| APPCD_uRawAPP1 | B812F1042C100000 | 07 | 1 | 0x64 | 06 | 5 | -- | 0.000610 | 0 | 0 | 0 | 6.2f | V |  | APPCD_uRawAPP1 | Fahrpedal 1 Position Rohwert |
| APPCD_uRawAPP2 | B812F1042C100000 | 07 | 1 | 0x65 | 06 | 5 | -- | 0.000610 | 0 | 0 | 0 | 6.2f | V |  | APPCD_uRawAPP2 | Fahrpedal 2 Position Rohwert |
| APPCD_rFlt | B812F1042C100000 | 07 | 1 | 0x66 | 06 | 5 | -- | 3.05E-03 | 0 | 0 | 0 | 6.2f | % |  | APPCD_rFlt | gefiltertes Pedalwertgebersignal |
| APPCD_rAPP1UnFlt | B812F1042C100000 | 07 | 1 | 0x67 | 06 | 5 | -- | 3.05E-03 | 0 | 0 | 0 | 6.2f | % |  | APPCD_rAPP1UnFlt | Fahrpedal 1 position ungefilterter Rohwert |
| PFlt_mSot | B812F1042C100000 | 07 | 1 | 0x68 | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | g |  | PFlt_mSot | Rußmasse im Partikelfilter |
| PFlt_mSotMeas_mp | B812F1042C100000 | 07 | 1 | 0x69 | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | g |  | PFlt_mSotMeas_mp | Partikelmasse additivkorrigiert |
| PFlt_mSotMeasRaw_mp | B812F1042C100000 | 07 | 1 | 0x6A | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | g |  | PFlt_mSotMeasRaw_mp | Strömungswdst. in Partikelmasse umgerechnet |
| PFlt_mSotSim_mp | B812F1042C100000 | 07 | 1 | 0x6B | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | g |  | PFlt_mSotSim_mp | simulierte Partikelmasse |
| PFlt_mAsh_mp | B812F1042C100000 | 07 | 1 | 0x6C | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | g |  | PFlt_mAsh_mp | Aschen-Masse |
| PFlt_numEngPOp_mp | B812F1042C100000 | 07 | 1 | 0x6D | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | PFlt_numEngPOp_mp | Regeneriermaßnahme aufgrund PFlt- und Motorzustand |
| APSCD_pVal | B812F1042C100000 | 07 | 1 | 0x6E | 06 | 5 | -- | 0.125 | 0 | 0 | 0 | 6.2f | hPa |  | APSCD_pVal | Atmosphärendruck |
| APSCD_uRaw | B812F1042C100000 | 07 | 1 | 0x6F | 06 | 5 | -- | 0.610 | 0 | 0 | 0 | 6.2f | mV |  | APSCD_uRaw | Rohspannung ADC-Signal Atmosphärendruck |
| PFlt_numRgn_mp | B812F1042C100000 | 07 | 1 | 0x70 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | PFlt_numRgn_mp | gesamte Regenerationsanforderung |
| PFlt_tPreFlt_mp | B812F1042C100000 | 07 | 1 | 0x71 | 06 | 5 | -- | 0.016 | -50.1 | 0 | 0 | 6.2f | deg C |  | PFlt_tPreFlt_mp | PFlt_tPre PT1 gefiltert |
| PFlt_vVehFlt_mp | B812F1042C100000 | 07 | 1 | 0x72 | 06 | 5 | -- | 3.81E-03 | 0 | 0 | 0 | 6.2f | km/h |  | PFlt_vVehFlt_mp | VSSCD_v PT1 gefiltert |
| HWEMon_numRecovery | B812F1042C100000 | 07 | 1 | 0x73 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | HWEMon_numRecovery | Herkunft des letzten Reset ( &gt;0 = Recovery ) |
| Clg_tiDynTst | B812F1042C100000 | 07 | 1 | 0x74 | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | s |  | Clg_tiDynTst | Abgelaufene Zeit, seit der der dynamische plausibilitätstest aktiv ist |
| Clg_dtDynTst | B812F1042C100000 | 07 | 1 | 0x75 | 06 | 5 | -- | 1.00 | 232. | 0 | 0 | 6.2f | deg C |  | Clg_dtDynTst | Ansteig der Wassertemperatur seit start |
| Clg_tiMaxDynTst | B812F1042C100000 | 07 | 1 | 0x76 | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | s |  | Clg_tiMaxDynTst | Maximal zulässige Testzeit des dynamischen Plausibilitätstest |
| Clg_tEndDynTst | B812F1042C100000 | 07 | 1 | 0x77 | 06 | 5 | -- | 1.00 | -41.0 | 0 | 0 | 6.2f | deg C |  | Clg_tEndDynTst | CTSCD_tClnt am Ende des Tests |
| EGRCD_rOut | B812F1042C100000 | 07 | 1 | 0x7A | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | % |  | EGRCD_rOut | Tastverhältnis zür Endstufenansteuerung |
| BPACD_rOut | B812F1042C100000 | 07 | 1 | 0x7B | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | % |  | BPACD_rOut | Tastverhältnis zür Endstufenansteuerung |
| GlwCtl_rPwrOut | B812F1042C100000 | 07 | 1 | 0x7C | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | GlwCtl_rPwrOut | Glühanforderung |
| ACCD_dcycPres | B812F1042C100000 | 07 | 1 | 0x7D | 06 | 5 | -- | 3.05E-03 | 0 | 0 | 0 | 6.2f | % |  | ACCD_dcycPres | AC Druck für PWM Eingang |
| PFlt_qFl_mp | B812F1042C100000 | 07 | 1 | 0x7E | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | l |  | PFlt_qFl_mp | verbrauchter Treibstoff seit der letzten erfolgreichen Regeneration |
| AOHt_rHtgOut | B812F1042C100000 | 07 | 1 | 0x7F | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | % |  | AOHt_rHtgOut | Heizleitungsanforderung, Zuheizer (Tastverhältnis) |
| FanCD_dcyc | B812F1042C100000 | 07 | 1 | 0x80 | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | % |  | FanCD_dcyc | duty cycle to be passed to the powerstage (without diagnosis access) |
| PSPCD_dvolOut | B812F1042C100000 | 07 | 1 | 0x81 | 06 | 5 | -- | 0.208 | -6830. | 0 | 0 | 6.2f | l/h |  | PSPCD_dvolOut | Output fuel consumption quantity from PSPCD |
| AltCD_rAltLoad | B812F1042C100000 | 07 | 1 | 0x82 | 06 | 5 | -- | 3.05E-03 | 0 | 0 | 0 | 6.2f | % |  | AltCD_rAltLoad | Linearisiertes und fehlerentprelltes Generatorlastsignals |
| CrCtl_vDes | B812F1042C100000 | 07 | 1 | 0x83 | 06 | 5 | -- | 3.81E-03 | 0 | 0 | 0 | 6.2f | km/h |  | CrCtl_vDes | Sollgeschwindigkeit FGR |
| VehDa_rVn | B812F1042C100000 | 07 | 1 | 0x84 | 06 | 5 | -- | 1.52E-06 | 0 | 0 | 0 | 6.2f | (km/h)/rpm |  | VehDa_rVn | Verhältnis von Fahrgeschwindigkeit zur Motordrehzahl |
| CrSCD_nCurr | B812F1042C100000 | 07 | 1 | 0x85 | 06 | 5 | -- | 0.125 | 0 | 0 | 0 | 6.2f | rpm |  | CrSCD_nCurr | aktuelle Motordrehzahl aus der letzten Segmentperiode |
| FBC_qDvtCyl | B812F1042C100000 | 07 | 1 | 0x86 | 06 | 5 | -- | 3.05E-03 | -99.9 | 0 | 0 | 6.2f | mg/hub |  | FBC_qDvtCyl | aktuelle zylinderindividuelle Korrekturmenge: I-Anteil |
| AirCtl_mDesStat_mp | B812F1042C100000 | 07 | 1 | 0x87 | 06 | 5 | -- | 4.88E-02 | -1599. | 0 | 0 | 6.2f | mg/Hub |  | AirCtl_mDesStat_mp | stationärer Luftmassensollwert |
| AirCtl_mDesVal | B812F1042C100000 | 07 | 1 | 0x88 | 06 | 5 | -- | 4.88E-02 | -1599. | 0 | 0 | 6.2f | mg/Hub |  | AirCtl_mDesVal | Luftmassensollwert |
| BPSCD_pFltVal | B812F1042C100000 | 07 | 1 | 0x89 | 06 | 5 | -- | 0.125 | 0 | 0 | 0 | 6.2f | hPa |  | BPSCD_pFltVal | gefilterter Wert des Ladedrucks |
| PCR_pDesVal | B812F1042C100000 | 07 | 1 | 0x8A | 06 | 5 | -- | 0.125 | 0 | 0 | 0 | 6.2f | hPa |  | PCR_pDesVal | Ladedrucksollwert |
| BPA_rBPACD | B812F1042C100000 | 07 | 1 | 0x8B | 06 | 5 | -- | 3.05E-03 | 0 | 0 | 0 | 6.2f | % |  | BPA_rBPACD | Stellgröße für Ladedrucksteller (Stellerkoordinatorausgang) |
| PFlt_resFlow | B812F1042C100000 | 07 | 1 | 0x8C | 06 | 5 | -- | 0.001 | 0 | 0 | 0 | 6.2f | hPa/(m^3/h) |  | PFlt_resFlow | Strömungswiderstand |
| CrCtl_numGear | B812F1042C100000 | 07 | 1 | 0x8D | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | CrCtl_numGear | Gang FGR |
| CoEng_stShutOff | B812F1042C100000 | 07 | 1 | 0x8E | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | CoEng_stShutOff | Typ der wirksamen Abschaltursache (0: Nachlauf; 1: reversibel; 2: irreversibel) |
| CoEng_trqInrLtd | B812F1042C100000 | 07 | 1 | 0x8F | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | CoEng_trqInrLtd | inneres Moment Sollwert nach Begrenzung, vor Eingriff ARD-Störungsregler |
| StSys_trqStrt | B812F1042C100000 | 07 | 1 | 0x90 | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | StSys_trqStrt | inneres Moment Startwert |
| CrCtl_trqDes | B812F1042C100000 | 07 | 1 | 0x91 | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | CrCtl_trqDes | Momentenanforderung FGR |
| Prp_trqRaw | B812F1042C100000 | 07 | 1 | 0x92 | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | Prp_trqRaw | Vortriebsmomentwunsch vor Führungsformer |
| FrmMng_trqDCS | B812F1042C100000 | 07 | 1 | 0x93 | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | FrmMng_trqDCS | vom MSR gefordertes Getriebeausgangsmoment |
| CoEng_trqLimMin_mp | B812F1042C100000 | 07 | 1 | 0x94 | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | CoEng_trqLimMin_mp | Begrenzungsmoment, falls kein momentenbegrenzender Systemfehler vorliegt (Minimum aus Rauchgrenze un Motormech.schutz) |
| CoVM_trqPrpDes | B812F1042C100000 | 07 | 1 | 0x95 | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | CoVM_trqPrpDes | Wunsch Vortriebsmoment |
| FMTC_trqInr | B812F1042C100000 | 07 | 1 | 0x96 | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | FMTC_trqInr | aktuelles rückgerechnetes inneres Motormoment |
| LIGov_trq | B812F1042C100000 | 07 | 1 | 0x97 | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | LIGov_trq | Leerlaufreglermoment |
| CrCtl_st | B812F1042C100000 | 07 | 1 | 0x98 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | CrCtl_st | Status FGR |
| AOHt_stShutOff_mp | B812F1042C100000 | 07 | 1 | 0x99 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | AOHt_stShutOff_mp | Überblick auf alle Abschaltbedingungen |
| FrmMng_lSum | B812F1042C100000 | 07 | 1 | 0x9A | 06 | 5 | -- | 8 | 0 | 0 | 0 | 6.2f | km |  | FrmMng_lSum | Kilometerstand des Fahrzeugs |
| OxiCCD_tPre | B812F1042C100000 | 07 | 1 | 0x9B | 06 | 5 | -- | 0.016 | -50.1 | 0 | 0 | 6.2f | deg C |  | OxiCCD_tPre | Abgastemperatur vor Oxidationskatalysator |
| RailCD_pAct_mp | B812F1042C100000 | 07 | 1 | 0x9C | 06 | 5 | -- | 3.05E-02 | 0 | 0 | 0 | 6.2f | bar |  | RailCD_pAct_mp | aktueller Kraftstoffdruck |
| PFltCD_tPre | B812F1042C100000 | 07 | 1 | 0x9D | 06 | 5 | -- | 0.016 | -50.1 | 0 | 0 | 6.2f | deg C |  | PFltCD_tPre | Abgastemp. vor Partikelfilter erster Sensor |
| PCVCD_iActVal | B812F1042C100000 | 07 | 1 | 0x9E | 06 | 5 | -- | 0.228 | 0 | 0 | 0 | 6.2f | mA |  | PCVCD_iActVal | Analogeingang Strom-Istwert |
| VehDa_tiEngOn | B812F1042C100000 | 07 | 1 | 0x9F | 06 | 5 | -- | 99.9 | 0 | 0 | 0 | 6.2f | s |  | VehDa_tiEngOn | Erfassung der aktuellen Betriebszeit |
| Gearbx_swtType | B812F1042C100000 | 07 | 1 | 0xA0 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | Gearbx_swtType | Getriebetyp (0: manuell; 1: automatisch) |
| InjVlv_nCyl1 | B812F1042C100000 | 07 | 1 | 0xA1 | 06 | 5 | -- | 0.125 | 0 | 0 | 0 | 6.2f | rpm |  | InjVlv_nCyl1 | Zylinderspezifische Drehzahl für Zylinder 1 |
| InjVlv_nCyl2 | B812F1042C100000 | 07 | 1 | 0xA2 | 06 | 5 | -- | 0.125 | 0 | 0 | 0 | 6.2f | rpm |  | InjVlv_nCyl2 | Zylinderspezifische Drehzahl für Zylinder 2 |
| InjVlv_nCyl3 | B812F1042C100000 | 07 | 1 | 0xA3 | 06 | 5 | -- | 0.125 | 0 | 0 | 0 | 6.2f | rpm |  | InjVlv_nCyl3 | Zylinderspezifische Drehzahl für Zylinder 3 |
| InjVlv_nCyl4 | B812F1042C100000 | 07 | 1 | 0xA4 | 06 | 5 | -- | 0.125 | 0 | 0 | 0 | 6.2f | rpm |  | InjVlv_nCyl4 | Zylinderspezifische Drehzahl für Zylinder 4 |
| InjVlv_nCyl5 | B812F1042C100000 | 07 | 1 | 0xA5 | 06 | 5 | -- | 0.125 | 0 | 0 | 0 | 6.2f | rpm |  | InjVlv_nCyl5 | Zylinderspezifische Drehzahl für Zylinder 5 |
| InjVlv_nCyl6 | B812F1042C100000 | 07 | 1 | 0xA6 | 06 | 5 | -- | 0.125 | 0 | 0 | 0 | 6.2f | rpm |  | InjVlv_nCyl6 | Zylinderspezifische Drehzahl für Zylinder 6 |
| InjVlv_qFBCCyl1 | B812F1042C100000 | 07 | 1 | 0xA7 | 06 | 5 | -- | 3.05E-03 | -99.9 | 0 | 0 | 6.2f | mg/hub |  | InjVlv_qFBCCyl1 | Zylinderselektive FBC-Mengenkorrektur für Zylinder 1 |
| InjVlv_qFBCCyl2 | B812F1042C100000 | 07 | 1 | 0xA8 | 06 | 5 | -- | 3.05E-03 | -99.9 | 0 | 0 | 6.2f | mg/hub |  | InjVlv_qFBCCyl2 | Zylinderselektive FBC-Mengenkorrektur für Zylinder 2 |
| InjVlv_qFBCCyl3 | B812F1042C100000 | 07 | 1 | 0xA9 | 06 | 5 | -- | 3.05E-03 | -99.9 | 0 | 0 | 6.2f | mg/hub |  | InjVlv_qFBCCyl3 | Zylinderselektive FBC-Mengenkorrektur für Zylinder 3 |
| InjVlv_qFBCCyl4 | B812F1042C100000 | 07 | 1 | 0xAA | 06 | 5 | -- | 3.05E-03 | -99.9 | 0 | 0 | 6.2f | mg/hub |  | InjVlv_qFBCCyl4 | Zylinderselektive FBC-Mengenkorrektur für Zylinder 4 |
| InjVlv_qFBCCyl5 | B812F1042C100000 | 07 | 1 | 0xAB | 06 | 5 | -- | 3.05E-03 | -99.9 | 0 | 0 | 6.2f | mg/hub |  | InjVlv_qFBCCyl5 | Zylinderselektive FBC-Mengenkorrektur für Zylinder 5 |
| InjVlv_qFBCCyl6 | B812F1042C100000 | 07 | 1 | 0xAC | 06 | 5 | -- | 3.05E-03 | -99.9 | 0 | 0 | 6.2f | mg/hub |  | InjVlv_qFBCCyl6 | Zylinderselektive FBC-Mengenkorrektur für Zylinder 6 |
| PFlt_resFlowOfs | B812F1042C100000 | 07 | 1 | 0xAD | 06 | 5 | -- | 0.001 | 0 | 0 | 0 | 6.2f | hPa/(m^3/h) |  | PFlt_resFlowOfs | Strömungswiderstandoffset |
| AddPCD_volAddTot | B812F1042C100000 | 07 | 1 | 0xAE | 06 | 5 | -- | 1.25E-02 | 0 | 0 | 0 | 6.2f | ml |  | AddPCD_volAddTot | Eingespritztes Gesamt-Additivvolumen (grobe Auflösung) |
| OPSCD_stSigOut | B812F1042C100000 | 07 | 1 | 0xAF | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | OPSCD_stSigOut | Ausgangssignal Öldruckschalter |
| EngM_stSync | B812F1042C100000 | 07 | 1 | 0xB0 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | EngM_stSync | Meta-Status der KW- und NW-Ereignisverwaltung (Motorpositions-Management) |
| InjCrv_phiPiI1Des | B812F1042C100000 | 07 | 1 | 0xB1 | 06 | 5 | -- | 2.92E-03 | -90.3 | 0 | 0 | 6.2f | deg CrS |  | InjCrv_phiPiI1Des | gewünschter Winkelkomponente Ansteuerbeginn PiI1 |
| InjCrv_phiPiI2Des | B812F1042C100000 | 07 | 1 | 0xB2 | 06 | 5 | -- | 2.92E-03 | -90.3 | 0 | 0 | 6.2f | deg CrS |  | InjCrv_phiPiI2Des | gewünschte Winkelkomponente Ansteuerbeginn PiI2 |
| InjCrv_phiPiI3Des | B812F1042C100000 | 07 | 1 | 0xB3 | 06 | 5 | -- | 2.92E-03 | -90.3 | 0 | 0 | 6.2f | deg CrS |  | InjCrv_phiPiI3Des | gewünschte Winkelkomponente Ansteuerbeginn PiI3 |
| InjVCD_tiPiI1ET_mp | B812F1042C100000 | 07 | 1 | 0xB4 | 06 | 5 | -- | 0.152 | 0 | 0 | 0 | 6.2f | us |  | InjVCD_tiPiI1ET_mp | Ansteuerdauer der Voreinspritzung 1 |
| InjVCD_tiPiI2ET_mp | B812F1042C100000 | 07 | 1 | 0xB5 | 06 | 5 | -- | 0.152 | 0 | 0 | 0 | 6.2f | us |  | InjVCD_tiPiI2ET_mp | Ansteuerdauer der Voreinspritzung 2 |
| InjVCD_tiPiI3ET_mp | B812F1042C100000 | 07 | 1 | 0xB6 | 06 | 5 | -- | 0.152 | 0 | 0 | 0 | 6.2f | us |  | InjVCD_tiPiI3ET_mp | Ansteuerdauer der Voreinspritzung 3 |
| InjCrv_qPiI1Des | B812F1042C100000 | 07 | 1 | 0xB7 | 06 | 5 | -- | 1.52E-03 | 0 | 0 | 0 | 6.2f | mg/inj |  | InjCrv_qPiI1Des | gewünschte Einspritzmenge PiI 1 |
| InjCrv_qPiI2Des | B812F1042C100000 | 07 | 1 | 0xB8 | 06 | 5 | -- | 1.52E-03 | 0 | 0 | 0 | 6.2f | mg/inj |  | InjCrv_qPiI2Des | gewünschte Einspritzmenge PiI 2 |
| InjCrv_qPiI3Des | B812F1042C100000 | 07 | 1 | 0xB9 | 06 | 5 | -- | 1.52E-03 | 0 | 0 | 0 | 6.2f | mg/inj |  | InjCrv_qPiI3Des | gewünschte Einspritzmenge PiI 3 |
| InjCrv_stPiI1_mp | B812F1042C100000 | 07 | 1 | 0xBA | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | InjCrv_stPiI1_mp | Freigabestatus PiI1 |
| InjCrv_stPiI2_mp | B812F1042C100000 | 07 | 1 | 0xBB | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | InjCrv_stPiI2_mp | Freigabestatus PiI2 |
| InjVCD_tiMI1ET_mp | B812F1042C100000 | 07 | 1 | 0xBC | 06 | 5 | -- | 0.152 | 0 | 0 | 0 | 6.2f | us |  | InjVCD_tiMI1ET_mp | Ansteuerdauer der Haupteinspritzung 1 |
| InjCrv_qPiI1Bas_mp | B812F1042C100000 | 07 | 1 | 0xBD | 06 | 5 | -- | 1.52E-03 | 0 | 0 | 0 | 6.2f | mg/inj |  | InjCrv_qPiI1Bas_mp | Einspritzmenge PiI1 Grundwert |
| InjCrv_qPiI2Bas_mp | B812F1042C100000 | 07 | 1 | 0xBE | 06 | 5 | -- | 1.52E-03 | 0 | 0 | 0 | 6.2f | mg/inj |  | InjCrv_qPiI2Bas_mp | Einspritzmenge PiI2 Grundwert |
| InjCrv_phiMI1Des | B812F1042C100000 | 07 | 1 | 0xBF | 06 | 5 | -- | 2.92E-03 | -90.3 | 0 | 0 | 6.2f | deg CrS |  | InjCrv_phiMI1Des | gewünschter Bezugswinkel für Beginn der MI1 |
| InjCrv_tiMI1ET | B812F1042C100000 | 07 | 1 | 0xC0 | 06 | 5 | -- | 0.152 | 0 | 0 | 0 | 6.2f | us |  | InjCrv_tiMI1ET | geschätzte Ansteuerdauer MI1 |
| InjCrv_qMI1Des | B812F1042C100000 | 07 | 1 | 0xC1 | 06 | 5 | -- | 1.52E-03 | 0 | 0 | 0 | 6.2f | mg/inj |  | InjCrv_qMI1Des | Sollmenge Haupteinspritzung |
| RailCD_pPeak | B812F1042C100000 | 07 | 1 | 0xC2 | 06 | 5 | -- | 3.05E-02 | 0 | 0 | 0 | 6.2f | bar |  | RailCD_pPeak | maximaler Raildruck der letzten 10ms |
| Rail_pSetPoint | B812F1042C100000 | 07 | 1 | 0xC3 | 06 | 5 | -- | 3.05E-02 | 0 | 0 | 0 | 6.2f | bar |  | Rail_pSetPoint | Raildruck-sollwert |
| InjCrv_phiPoI1Des | B812F1042C100000 | 07 | 1 | 0xC4 | 06 | 5 | -- | 2.92E-03 | -90.3 | 0 | 0 | 6.2f | deg CrS |  | InjCrv_phiPoI1Des | gewünschter Bezugswinkel für Beginn der PoI1 |
| InjCrv_phiPoI2Des | B812F1042C100000 | 07 | 1 | 0xC5 | 06 | 5 | -- | 2.92E-03 | -90.3 | 0 | 0 | 6.2f | deg CrS |  | InjCrv_phiPoI2Des | gewünschter Bezugswinkel für Beginn der PoI2 |
| InjVCD_tiPoI1ET_mp | B812F1042C100000 | 07 | 1 | 0xC6 | 06 | 5 | -- | 0.152 | 0 | 0 | 0 | 6.2f | us |  | InjVCD_tiPoI1ET_mp | Ansteuerdauer Nacheinspritzung 1 |
| InjVCD_tiPoI2ET_mp | B812F1042C100000 | 07 | 1 | 0xC7 | 06 | 5 | -- | 0.152 | 0 | 0 | 0 | 6.2f | us |  | InjVCD_tiPoI2ET_mp | Ansteuerdauer der Nacheinspritzung 2 |
| APPCD_stKickDown | B812F1042C100000 | 07 | 1 | 0xC8 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | APPCD_stKickDown | Kick Down Zustand des Fahrpedals |
| FrmMng_swtAC_mp | B812F1042C100000 | 07 | 1 | 0xC9 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | FrmMng_swtAC_mp | Schalter Klimakompressor |
| CoEng_voltotFlConsum | B812F1042C100000 | 07 | 1 | 0xCB | 06 | 5 | -- | 20.8 | -683021. | 0 | 0 | 6.2f | ul |  | CoEng_voltotFlConsum | Absoluter Kraftstoffverbrauch |
| PFlt_resFlowRaw_mp | B812F1042C100000 | 07 | 1 | 0xCC | 06 | 5 | -- | 0.001 | 0 | 0 | 0 | 6.2f | hPa/(m^3/h) |  | PFlt_resFlowRaw_mp | Strömungswiderstand Rohwert |
| PrpBrk_trqDes | B812F1042C100000 | 07 | 1 | 0xCD | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | PrpBrk_trqDes | Vortriebsmomentwunsch der Längsbewegung |
| EngM_trqFrc | B812F1042C100000 | 07 | 1 | 0xCE | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | EngM_trqFrc | aktuelles Reibmoment |
| FrmMng_nFan | B812F1042C100000 | 07 | 1 | 0xCF | 06 | 5 | -- | 1.14E-02 | 0 | 0 | 0 | 6.2f | 1/min |  | FrmMng_nFan | Lüfterdrehzahl |
| CrCCD_stKey | B812F1042C100000 | 07 | 1 | 0xD0 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | CrCCD_stKey | Rückgabewert  |
| CrCtl_stLampOut | B812F1042C100000 | 07 | 1 | 0xD1 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | CrCtl_stLampOut | Status der CrCtl-Lampe (wird über CAN versendet) |
| PFlt_stEngPOp | B812F1042C100000 | 07 | 1 | 0xD2 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | PFlt_stEngPOp | Motorbetriebspunkt |
| RailCD_uPeakRaw | B812F1042C100000 | 07 | 1 | 0xD3 | 06 | 5 | -- | 0.610 | 0 | 0 | 0 | 6.2f | mV |  | RailCD_uPeakRaw | Rohwert des Raildrucks |
| FTSCD_uRaw | B812F1042C100000 | 07 | 1 | 0xD4 | 06 | 5 | -- | 0.610 | 0 | 0 | 0 | 6.2f | mV |  | FTSCD_uRaw | Spannungsrohwert der Kraftstoffstemperatur |
| OxiCCD_uRawTempPre | B812F1042C100000 | 07 | 1 | 0xD5 | 06 | 5 | -- | 0.610 | 0 | 0 | 0 | 6.2f | mV |  | OxiCCD_uRawTempPre | Abgastemperatur vor Oxidationskatalysator Rohwert |
| PFltCD_uRawTempPre | B812F1042C100000 | 07 | 1 | 0xD6 | 06 | 5 | -- | 0.610 | 0 | 0 | 0 | 6.2f | mV |  | PFltCD_uRawTempPre | Spannungsrohwert der Abgastemperatur vor dem Partikelfilter |
| BattCD_uRaw | B812F1042C100000 | 07 | 1 | 0xD7 | 06 | 5 | -- | 0.610 | 0 | 0 | 0 | 6.2f | mV |  | BattCD_uRaw | Rohwert ADC-Signalspannung für Batteriespannung |
| OTSCD_uRaw | B812F1042C100000 | 07 | 1 | 0xD8 | 06 | 5 | -- | 0.610 | 0 | 0 | 0 | 6.2f | mV |  | OTSCD_uRaw | Rohwert des OTF-Sensors |
| FBC_q | B812F1042C100000 | 07 | 1 | 0xD9 | 06 | 5 | -- | 1.52E-02 | 0 | 0 | 0 | 6.2f | mg/hub |  | FBC_q | Ausgangsmenge der Mengenausgleichsregelung |
| CoEng_trqSetASDdc_mp | B812F1042C100000 | 07 | 1 | 0xDA | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | CoEng_trqSetASDdc_mp | Sollmoment nach Eingriff Ruckeldämfer vor zweiter Begrenzung (mit Offset) |
| ASDrf_trqInr | B812F1042C100000 | 07 | 1 | 0xDB | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | ASDrf_trqInr | ARD Führungsformer Momentausgang (inneres Moment) |
| ASDdc_trq | B812F1042C100000 | 07 | 1 | 0xDC | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | ASDdc_trq | Momentforderung Aktiver Ruckeldämpfer (Störungsregler) |
| PFlt_stEngPOp1_mp | B812F1042C100000 | 07 | 1 | 0xDD | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | PFlt_stEngPOp1_mp | Motorbetriebspunkt berechnet in Check Range 1 |
| PFlt_stEngPOp2_mp | B812F1042C100000 | 07 | 1 | 0xDE | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | PFlt_stEngPOp2_mp | Motorbetriebspunkt berechnet in Check Range 2 |
| LIGov_trqI | B812F1042C100000 | 07 | 1 | 0xDF | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | LIGov_trqI | Wert des I-Anteils des LLR |
| LIGov_trqP | B812F1042C100000 | 07 | 1 | 0xE0 | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | LIGov_trqP | Wert des P-Anteils des LLR |
| LIGov_trqD_mp | B812F1042C100000 | 07 | 1 | 0xE1 | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | LIGov_trqD_mp | Messpunkt für den Wert des D-Anteils des LLR |
| LIGov_st | B812F1042C100000 | 07 | 1 | 0xE2 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | LIGov_st | Zustand des Leerlaufreglers |
| FrmMng_tEnv | B812F1042C100000 | 07 | 1 | 0xE3 | 06 | 5 | -- | 0.016 | -50.1 | 0 | 0 | 6.2f | deg C |  | FrmMng_tEnv | Umgebungstemperatur |
| FrmMng_stACHtgReq | B812F1042C100000 | 07 | 1 | 0xE4 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | FrmMng_stACHtgReq | Heizleistungsanforderung über CAN |
| ACCD_stACPresent | B812F1042C100000 | 07 | 1 | 0xE5 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | ACCD_stACPresent | Klimaanlage im Auto vorhanden |
| GlwCD_rHWEActrOut_mp | B812F1042C100000 | 07 | 1 | 0xE6 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | GlwCD_rHWEActrOut_mp | Glühausgang |
| ACCD_rDigOut_mp | B812F1042C100000 | 07 | 1 | 0xE7 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | ACCD_rDigOut_mp | AC digital output value to the hardware |
| FanCD_dcycCorr_mp | B812F1042C100000 | 07 | 1 | 0xE8 | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | % |  | FanCD_dcycCorr_mp | dutycycle Ubatt-corrected |
| AOHtCD_rOut_mp | B812F1042C100000 | 07 | 1 | 0xE9 | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | % |  | AOHtCD_rOut_mp | Meßpunkt fuer korrigiertes Tastverhaeltnis der Zuheizeransteuerung |
| TVACD_rOut | B812F1042C100000 | 07 | 1 | 0xEA | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | % |  | TVACD_rOut | Tastverhältnis zür Endstufenansteuerung |
| VSACD_rOut | B812F1042C100000 | 07 | 1 | 0xEB | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | % |  | VSACD_rOut | Tastverhältnis zür Endstufenansteuerung |
| MeUnCD_dcycOut_mp | B812F1042C100000 | 07 | 1 | 0xEC | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | % |  | MeUnCD_dcycOut_mp | Ausgangstastverhältnis |
| PCVCD_dcycOut_mp | B812F1042C100000 | 07 | 1 | 0xED | 06 | 5 | -- | 0.01 | 0 | 0 | 0 | 6.2f | % |  | PCVCD_dcycOut_mp | Ausgangstastverhältnis |
| ACCD_trqLim | B812F1042C100000 | 07 | 1 | 0xEE | 06 | 5 | -- | 0.114 | -2500. | 0 | 0 | 6.2f | Nm |  | ACCD_trqLim | Externally controlled regulator for AC compressor |
| PFlt_stEngPOp4_mp | B812F1042C100000 | 07 | 1 | 0xEF | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | PFlt_stEngPOp4_mp | Motorbetriebspunkt berechnet in Check Range 4 |
| CrCtl_stShutOffCode1_mp | B812F1042C100000 | 07 | 1 | 0xF0 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | CrCtl_stShutOffCode1_mp | Low Byte von CrCtl_shutOffCode (Verwendung als Signal) |
| CrCtl_stShutOffCode1_mp | B812F1042C100000 | 07 | 1 | 0xF1 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | CrCtl_stShutOffCode1_mp | Low Byte von CrCtl_shutOffCode (Verwendung als Signal) |
| CrCtl_stShutOffCode2_mp | B812F1042C100000 | 07 | 1 | 0xF2 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | CrCtl_stShutOffCode2_mp | Low Byte von CrCtl_shutOffCode (Verwendung als Signal) |
| CrCtl_stShutOffCode2_mp | B812F1042C100000 | 07 | 1 | 0xF3 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | CrCtl_stShutOffCode2_mp | Low Byte von CrCtl_shutOffCode (Verwendung als Signal) |
| CrCtl_stShutOffFrz1_mp | B812F1042C100000 | 07 | 1 | 0xF4 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | CrCtl_stShutOffFrz1_mp | Shutoff code Frz |
| CrCtl_stShutOffFrz1_mp | B812F1042C100000 | 07 | 1 | 0xF5 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | CrCtl_stShutOffFrz1_mp | Shutoff code Frz |
| CrCtl_stShutOffFrz2_mp | B812F1042C100000 | 07 | 1 | 0xF6 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | CrCtl_stShutOffFrz2_mp | Shutoff code Frz |
| CrCtl_stShutOffFrz2_mp | B812F1042C100000 | 07 | 1 | 0xF7 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | CrCtl_stShutOffFrz2_mp | Shutoff code Frz |
| BrkCD_tiDebTmrPlaus_mp | B812F1042C100000 | 07 | 1 | 0xF8 | 06 | 5 | -- | 10 | 0 | 0 | 0 | 6.2f | ms |  | BrkCD_tiDebTmrPlaus_mp | Entprelltimer für Bremssignal-Plausibilitaets-Check |
| PFlt_st1_mp | B812F1042C100000 | 07 | 1 | 0xF9 | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | PFlt_st1_mp | Status des Partikelfilters  LowByte (-&gt;Signals) |
| PFlt_st1_mp | B812F1042C100000 | 07 | 1 | 0xFA | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | PFlt_st1_mp | Status des Partikelfilters  LowByte (-&gt;Signals) |
| PFlt_st2_mp | B812F1042C100000 | 07 | 1 | 0xFB | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | PFlt_st2_mp | Status des Partikelfilters  HighByte (-&gt;Signals) |
| PFlt_st2_mp | B812F1042C100000 | 07 | 1 | 0xFC | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | PFlt_st2_mp | Status des Partikelfilters  HighByte (-&gt;Signals) |
| Dummy_recLocLow_mp | B812F1042C100000 | 07 | 1 | 0xFD | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | Dummy_recLocLow_mp | LowAdresse recovery-location |
| Dummy_recLocLow_mp | B812F1042C100000 | 07 | 1 | 0xFE | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | Dummy_recLocLow_mp | LowAdresse recovery-location |
| Dummy_recLocHigh_mp | B812F1042C100000 | 07 | 1 | 0xFF | 06 | 5 | -- | 1 | 0 | 0 | 0 | 6.2f | - |  | Dummy_recLocHigh_mp | HighAdresse recovery-location |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 532 rows × 12 columns

| ORT | ORTTEXT | UW_1 | UW_2 | UW_3 | UW_4 | UW_5 | UW_6 | UW_7 | UW_8 | UW_9 | UW_10 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4820 | 4820 (0) Klimaleistungsausgang | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4821 | 4821 (0) Klimaleistungsausgang | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4822 | 4822 (0) Klimaleistungsausgang | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4823 | 4823 (0) Klimaleistungsausgang | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x40B0 | 40B0 (0) Fault path 1 for air condition pressure (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x40B1 | 40B1 (0) Fault path 1 for air condition pressure (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x40B2 | 40B2 (0) Fault path 1 for air condition pressure (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x40B3 | 40B3 (0) Fault path 1 for air condition pressure (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x40C0 | 40C0 (0) Fault path 2 for air condition pressure (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x40C1 | 40C1 (0) Fault path 2 for air condition pressure (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x40D0 | 40D0 (0) Fault path for analog air condition pressure (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x40D1 | 40D1 (0) Fault path for analog air condition pressure (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4112 | 4112 (0) Fault path of air condition power stage (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4113 | 4113 (0) Fault path of air condition power stage (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4780 | 4780 (0) Steuergeraet intern 15 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4781 | 4781 (0) Steuergeraet intern 15 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4782 | 4782 (0) Steuergeraet intern 15 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4783 | 4783 (0) Steuergeraet intern 15 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4170 | 4170 (0) Additiv-Dosierpumpe (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4171 | 4171 (0) Additiv-Dosierpumpe (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4172 | 4172 (0) Additiv-Dosierpumpe (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4173 | 4173 (0) Additiv-Dosierpumpe (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4370 | 4370 (0) error path for plausibility check of the airmasses from the two air systems | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4830 | 4830 (0) error path for signal range check of duty cycle of air temparature signal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4831 | 4831 (0) error path for signal range check of duty cycle of air temparature signal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3E95 | 3E95 (0) 2nd HFM:  error path for signal range check of dutay cycle of air temparature sig | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3E96 | 3E96 (0) 2nd HFM:  error path for signal range check of dutay cycle of air temparature sig | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3FE0 | 3FE0 (0) Luftmassenmesser (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3FE1 | 3FE1 (0) Luftmassenmesser (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3EB5 | 3EB5 (0) 2nd HFM:  error path for plausibility check of offset drift of airmass | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3EB6 | 3EB6 (0) 2nd HFM:  error path for plausibility check of offset drift of airmass | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3FF0 | 3FF0 (0) Luftmassenmesser (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3FF1 | 3FF1 (0) Luftmassenmesser (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4CA5 | 4CA5 (0) 2nd HFM:  fault path for plausibility check of sensitivity drift of airmass | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4CA6 | 4CA6 (0) 2nd HFM:  fault path for plausibility check of sensitivity drift of airmass | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4BA0 | 4BA0 (0) error path for signal range check of air temparature | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x4BA1 | 4BA1 (0) error path for signal range check of air temparature | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x3EA5 | 3EA5 (0) 2nd HFM:  error path for signal range check of air temparature | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x3EA6 | 3EA6 (0) 2nd HFM:  error path for signal range check of air temparature | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x4BB0 | 4BB0 (0) error path for signal range check of battery voltage | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x4BB1 | 4BB1 (0) error path for signal range check of battery voltage | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x4C75 | 4C75 (0) 2nd HFM:  error path for signal range check of battery voltage | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x4C76 | 4C76 (0) 2nd HFM:  error path for signal range check of battery voltage | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x4BB5 | 4BB5 (0) error path for signal range check of corrected airmass signal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x4BB6 | 4BB6 (0) error path for signal range check of corrected airmass signal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x3ED5 | 3ED5 (0) 2nd HFM:  error path for signal range check of corrected airmass signal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x3ED6 | 3ED6 (0) 2nd HFM:  error path for signal range check of corrected airmass signal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x4BC0 | 4BC0 (0) error path for signal range check of raw airmasssignal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x4BC1 | 4BC1 (0) error path for signal range check of raw airmasssignal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x4BC2 | 4BC2 (0) error path for signal range check of raw airmasssignal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x3EE5 | 3EE5 (0) 2nd HFM:  error path for signal range check of raw airmasssignal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x3EE6 | 3EE6 (0) 2nd HFM:  error path for signal range check of raw airmasssignal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x3EE7 | 3EE7 (0) 2nd HFM:  error path for signal range check of raw airmasssignal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x4BC5 | 4BC5 (0) error path for signal range check of reference signal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x4BC6 | 4BC6 (0) error path for signal range check of reference signal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x4BC7 | 4BC7 (0) error path for signal range check of reference signal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x3EF5 | 3EF5 (0) 2nd HFM:  error path for signal range check of reference signal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x3EF6 | 3EF6 (0) 2nd HFM:  error path for signal range check of reference signal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x3EF7 | 3EF7 (0) 2nd HFM:  error path for signal range check of reference signal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |
| 0x43F0 | 43F0 (0) Elektrischer Zuheizer | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |
| 0x43F1 | 43F1 (0) Elektrischer Zuheizer | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |
| 0x43F2 | 43F2 (0) Elektrischer Zuheizer | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |
| 0x43F3 | 43F3 (0) Elektrischer Zuheizer | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |
| 0x4AB0 | 4AB0 (0) Elektrischer Zuheizer | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |
| 0x4AB2 | 4AB2 (0) Elektrischer Zuheizer | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |
| 0x4AC0 | 4AC0 (0) Elektrischer Zuheizer 2 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |
| 0x4AC2 | 4AC2 (0) Elektrischer Zuheizer 2 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |
| 0x4AD0 | 4AD0 (0) Elektrischer Zuheizer 3 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |
| 0x4AD2 | 4AD2 (0) Elektrischer Zuheizer 3 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |
| 0x3F10 | 3F10 (0) Pedalwertgeber | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x49 |
| 0x3F11 | 3F11 (0) Pedalwertgeber | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x49 |
| 0x3F13 | 3F13 (0) Pedalwertgeber | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x49 |
| 0x3F20 | 3F20 (0) Pedalwertgeber PGS | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x49 |
| 0x3F21 | 3F21 (0) Pedalwertgeber PGS | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x49 |
| 0x3F23 | 3F23 (0) Pedalwertgeber PGS | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x49 |
| 0x4060 | 4060 (8745) Atmosphaerendruckfuehler (im Steuergeraet verbaut) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x6F | 0x2F | 0x32 | 0x6E |
| 0x4061 | 4061 (8744) Atmosphaerendruckfuehler (im Steuergeraet verbaut) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x6F | 0x2F | 0x32 | 0x6E |
| 0x4063 | 4063 (0) Atmosphaerendruckfuehler (im Steuergeraet verbaut) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x6F | 0x2F | 0x32 | 0x6E |
| 0x4BD2 | 4BD2 (0) Fault path for ARS | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4093 | 4093 (0) Error path for AccPed and Brake Plausibility (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C71 | 4C71 (0) fault path for the additive tank  component driver | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4501 | 4501 (1025) Abgasrueckfuehr-Regelung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x7A | 0x7B | 0x6E |
| 0x4841 | 4841 (0) AirCtl permanent governor2 negative deviation | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x7A | 0x7B | 0x6E |
| 0x4507 | 4507 (1026) Abgasrueckfuehr-Regelung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x7A | 0x7B | 0x6E |
| 0x4850 | 4850 (0) AirCtl permanent governor2 positive deviation | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x7A | 0x7B | 0x6E |
| 0x40E0 | 40E0 (0) Generator | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3F57 | 3F57 (0) error path 1 of boost pressure actuator diagnosis | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |
| 0x3F67 | 3F67 (0) fault path for diagnostic window one for BPA power stage | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |
| 0x3F77 | 3F77 (0) error path 2 of boost pressure actuator diagnosis | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |
| 0x3F87 | 3F87 (0) fault path for diagnostic window two for BPA power stage | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |
| 0x3F97 | 3F97 (0) error path 3 of boost pressure actuator diagnosis | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |
| 0x3FA7 | 3FA7 (0) fault path for diagnostic window three for BPA power stage | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |
| 0x4180 | 4180 (4624) Ladedrucksteller KS B+ | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |
| 0x4550 | 4550 (0) xxx Short Circuit Battery | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |
| 0x4191 | 4191 (4625) Ladedrucksteller KS B- | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |
| 0x4D81 | 4D81 (0) fault path for short circuit to ground for the second BPA power stage | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |
| 0x41A2 | 41A2 (4626) Ladedrucksteller UeT Unt | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x41A3 | 41A3 (4627) Ladedrucksteller UeT Unt | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A22 | 4A22 (0) fault path for no load and excess temparature for the second BPA power stage | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A23 | 4A23 (0) fault path for no load and excess temparature for the second BPA power stage | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3F00 | 3F00 (568) Ladedruckfuehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x39 | 0x2F | 0x32 | 0x6E |
| 0x3F01 | 3F01 (567) Ladedruckfuehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x39 | 0x2F | 0x32 | 0x6E |
| 0x3F02 | 3F02 (565) Ladedruckfuehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x39 | 0x2F | 0x32 | 0x6E |
| 0x3F03 | 3F03 (566) Ladedruckfuehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x39 | 0x2F | 0x32 | 0x6E |
| 0x4660 | 4660 (0) Versorgungsspannung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4661 | 4661 (0) Versorgungsspannung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4082 | 4082 (0) Bremslicht- / Bremstestschalter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4083 | 4083 (0) Bremslicht- / Bremstestschalter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A10 | 4A10 (0) Bitserielle Datenschnittstelle BSD | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A13 | 4A13 (0) Bitserielle Datenschnittstelle BSD | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3EE0 | 3EE0 (280) Kuehlmitteltemperaturfuehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x2B | 0x2F | 0x32 | 0x6E |
| 0x3EE1 | 3EE1 (279) Kuehlmitteltemperaturfuehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x2B | 0x2F | 0x32 | 0x6E |
| 0x3EE2 | 3EE2 (277) Kuehlmitteltemperaturfuehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x2B | 0x2F | 0x32 | 0x6E |
| 0x3EE3 | 3EE3 (0) Kuehlmitteltemperaturfuehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x2B | 0x2F | 0x32 | 0x6E |
| 0x3EF3 | 3EF3 (0) Kuehlmitteltemperaturfuehler Plaus (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4880 | 4880 (0) xxx number of recognized misfire events above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4890 | 4890 (0) xxx number of recognized misfire events above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4930 | 4930 (0) xxx number of recognized misfire events above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4940 | 4940 (0) xxx number of recognized misfire events above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4950 | 4950 (0) xxx number of recognized misfire events above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4960 | 4960 (0) xxx number of recognized misfire events above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4870 | 4870 (0) xxx number of recognized misfire events above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x47A0 | 47A0 (0) MFC error path for Misfire cylinder 0 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x47B0 | 47B0 (0) MFC error path for Misfire cylinder 1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x47C0 | 47C0 (0) MFC error path for Misfire cylinder 2 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x47D0 | 47D0 (0) MFC error path for Misfire cylinder 3 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x47E0 | 47E0 (0) MFC error path for Misfire cylinder 4 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x47F0 | 47F0 (0) MFC error path for Misfire cylinder 5 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C80 | 4C80 (0) MFC error path for Misfire cylinder 6 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C90 | 4C90 (0) MFC error path for Misfire cylinder 7 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D92 | 4D92 (0) Torque Monitoring | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D93 | 4D93 (0) Torque Monitoring | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4900 | 4900 (0) Momenteneingriff (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4072 | 4072 (0) Kupplungsschalter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4073 | 4073 (0) Kupplungsschalter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A30 | 4A30 (0) Multifunktionsschalter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A31 | 4A31 (0) Multifunktionsschalter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A32 | 4A32 (0) Multifunktionsschalter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A33 | 4A33 (0) Multifunktionsschalter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3F80 | 3F80 (115) Umgebungstemperaturfuehler (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3F81 | 3F81 (114) Umgebungstemperaturfuehler (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3F82 | 3F82 (0) Umgebungstemperaturfuehler (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x41C0 | 41C0 (0) Abluftklappenansteuerung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x62 |
| 0x41C1 | 41C1 (0) Abluftklappenansteuerung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x62 |
| 0x41C2 | 41C2 (0) Abluftklappenansteuerung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x62 |
| 0x41C3 | 41C3 (0) Abluftklappenansteuerung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x62 |
| 0x4AE0 | 4AE0 (0) E-Boxluefter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4AE1 | 4AE1 (0) E-Boxluefter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4AE2 | 4AE2 (0) E-Boxluefter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4AE3 | 4AE3 (0) E-Boxluefter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4AF0 | 4AF0 (0) Steuergeraetetemperaturfuehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4AF1 | 4AF1 (0) Steuergeraetetemperaturfuehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4B00 | 4B00 (0) Steuergeraetetemperatur | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x38 | 0x32 | 0x6E |
| 0x41B0 | 41B0 (8514) Abgasrueckfuehrsteller KS B+ | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |
| 0x4DB0 | 4DB0 (8514) xxx Short Circuit Battery | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |
| 0x41D1 | 41D1 (8513) Abgasrueckfuehrsteller KS B- | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |
| 0x4DC1 | 4DC1 (8513) fault path for short circuit to ground for 2nd EGR power stage | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |
| 0x41E2 | 41E2 (1159) Abgasrueckfuehrsteller Unt Ueb | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |
| 0x41E3 | 41E3 (0) Abgasrueckfuehrsteller Unt Ueb | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |
| 0x4DD2 | 4DD2 (1159) fault path for no load and excess temparature for 2nd EGR power stage | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |
| 0x4DD3 | 4DD3 (0) fault path for no load and excess temparature for 2nd EGR power stage | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |
| 0x3EC0 | 3EC0 (0) Nockenwellengeber | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |
| 0x3EC1 | 3EC1 (0) Nockenwellengeber | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |
| 0x3ED0 | 3ED0 (0) Nockenwellengeber | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |
| 0x3ED1 | 3ED1 (0) Nockenwellengeber | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |
| 0x3E90 | 3E90 (0) Drehzahlgeber Kurbelwelle | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |
| 0x3E91 | 3E91 (0) Drehzahlgeber Kurbelwelle | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |
| 0x3EA0 | 3EA0 (0) Drehzahlgeber Kurbelwelle | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |
| 0x3EA1 | 3EA1 (0) Drehzahlgeber Kurbelwelle | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |
| 0x4BD5 | 4BD5 (0) xxx Short Circuit to Battery | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4BD6 | 4BD6 (0) xxx Short Circuit to Battery | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4BD7 | 4BD7 (0) xxx Short Circuit to Battery | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4BD8 | 4BD8 (0) xxx Short Circuit to Battery | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4B10 | 4B10 (4630) Laufruheregler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x97 |
| 0x4B11 | 4B11 (4631) Laufruheregler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x97 |
| 0x4A70 | 4A70 (0) Kennfeld FMTC_trq2qBas_MAP falsch | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x96 |
| 0x4000 | 4000 (0) Fuel Temperature sensor (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0xD4 | 0x2F | 0x32 | 0x6E |
| 0x4001 | 4001 (0) Fuel Temperature sensor (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0xD4 | 0x2F | 0x32 | 0x6E |
| 0x41F0 | 41F0 (0) Elektroluefter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |
| 0x41F1 | 41F1 (0) Elektroluefter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |
| 0x41F2 | 41F2 (0) Elektroluefter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |
| 0x41F3 | 41F3 (0) Elektroluefter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |
| 0x4B20 | 4B20 (0) Elektroluefter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |
| 0x4B22 | 4B22 (0) Elektroluefter | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |
| 0x4B30 | 4B30 (0) Elektroluefter 2 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |
| 0x4B32 | 4B32 (0) Elektroluefter 2 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |
| 0x4B40 | 4B40 (0) Elektroluefter 3 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |
| 0x4B42 | 4B42 (0) Elektroluefter 3 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |
| 0x4A80 | 4A80 (0) Ladedruckregelung (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4040 | 4040 (0) DFP for SRC error of Tank 1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4041 | 4041 (0) DFP for SRC error of Tank 1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4042 | 4042 (0) DFP for SRC error of Tank 1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4BE2 | 4BE2 (0) CAN Botschaftsueberwachung GEARBX_DATA | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4BE7 | 4BE7 (0) CAN Botschaftsueberwachung GEARBX_DATA2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4BF2 | 4BF2 (0) CAN Botschaftsueberwachung HEAT_AC | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4BF7 | 4BF7 (0) CAN Botschaftsueberwachung MILEAGE_RANGE | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C00 | 4C00 (0) CAN Botschaftsueberwachung OP_CRCTLACC | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C01 | 4C01 (0) CAN Botschaftsueberwachung OP_CRCTLACC | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C02 | 4C02 (0) CAN Botschaftsueberwachung OP_CRCTLACC | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4CA2 | 4CA2 (0) CAN Botschaftsueberwachung POWERMANAGMENT_BATTERYVOLTAGE | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4CB2 | 4CB2 (0) CAN Botschaftsueberwachung PWRMNG_LOADV | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C06 | 4C06 (0) CAN Botschaftsueberwachung STAT_ARS | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C07 | 4C07 (0) CAN Botschaftsueberwachung STAT_ARS | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C12 | 4C12 (0) CAN Botschaftsueberwachung STAT_DSC | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C15 | 4C15 (0) CAN Botschaftsueberwachung TERMINAL | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C16 | 4C16 (0) CAN Botschaftsueberwachung TERMINAL | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C17 | 4C17 (0) CAN Botschaftsueberwachung TERMINAL | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C20 | 4C20 (0) CAN Botschaftsueberwachung TORQUE_DSC | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C21 | 4C21 (0) CAN Botschaftsueberwachung TORQUE_DSC | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C22 | 4C22 (0) CAN Botschaftsueberwachung TORQUE_DSC | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4DF0 | 4DF0 (0) CAN Botschaftsueberwachung TORQUE_GEARBX | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4DF1 | 4DF1 (0) CAN Botschaftsueberwachung TORQUE_GEARBX | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4DF2 | 4DF2 (0) CAN Botschaftsueberwachung TORQUE_GEARBX | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C27 | 4C27 (0) CAN Botschaftsueberwachung VELOCITY | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C30 | 4C30 (0) CAN Botschaftsausfall (FRM1) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C31 | 4C31 (0) CAN Botschaftsausfall (FRM1) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C32 | 4C32 (0) CAN Botschaftsausfall (FRM1) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C33 | 4C33 (0) CAN Botschaftsausfall (FRM1) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C35 | 4C35 (0) CAN Botschaftsausfall (FRM2) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C36 | 4C36 (0) CAN Botschaftsausfall (FRM2) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C37 | 4C37 (0) CAN Botschaftsausfall (FRM2) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C38 | 4C38 (0) CAN Botschaftsausfall (FRM2) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4970 | 4970 (0) CAN Botschaftsausfall (FRM3) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4971 | 4971 (0) CAN Botschaftsausfall (FRM3) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4972 | 4972 (0) CAN Botschaftsausfall (FRM3) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4973 | 4973 (0) CAN Botschaftsausfall (FRM3) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4CC0 | 4CC0 (0) CAN Botschaftsausfall (FRM4) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4920 | 4920 (0) Momenteneingriff Getriebe (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4203 | 4203 (1648) Gluehsteuergeraet | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4211 | 4211 (1649) Gluehkerze an Zylinder 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4212 | 4212 (1649) Gluehkerze an Zylinder 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4213 | 4213 (1649) Gluehkerze an Zylinder 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4221 | 4221 (1650) Gluehkerze an Zylinder 2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4222 | 4222 (1650) Gluehkerze an Zylinder 2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4223 | 4223 (1650) Gluehkerze an Zylinder 2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4231 | 4231 (1651) Gluehkerze an Zylinder 3 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4232 | 4232 (1651) Gluehkerze an Zylinder 3 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4233 | 4233 (1651) Gluehkerze an Zylinder 3 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4241 | 4241 (1652) Gluehkerze an Zylinder 4 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4242 | 4242 (1652) Gluehkerze an Zylinder 4 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4243 | 4243 (1652) Gluehkerze an Zylinder 4 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4251 | 4251 (0) Gluehkerze an Zylinder 5 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4252 | 4252 (0) Gluehkerze an Zylinder 5 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4253 | 4253 (0) Gluehkerze an Zylinder 5 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4261 | 4261 (0) Gluehkerze an Zylinder 6 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4262 | 4262 (0) Gluehkerze an Zylinder 6 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4263 | 4263 (0) Gluehkerze an Zylinder 6 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4271 | 4271 (0) Gluehkerze an Zylinder 7 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4272 | 4272 (0) Gluehkerze an Zylinder 7 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4273 | 4273 (0) Gluehkerze an Zylinder 7 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4281 | 4281 (0) Gluehkerze an Zylinder 8 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4282 | 4282 (0) Gluehkerze an Zylinder 8 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x4283 | 4283 (0) Gluehkerze an Zylinder 8 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x42A0 | 42A0 (0) Gluehrelais (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x42A1 | 42A1 (0) Gluehrelais (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x42A2 | 42A2 (0) Gluehrelais (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x42A3 | 42A3 (0) Gluehrelais (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x42B1 | 42B1 (0) Gluehrelais (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x42B2 | 42B2 (0) Gluehrelais (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |
| 0x46C0 | 46C0 (0) Steuergeraet intern 3 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x46D0 | 46D0 (0) Steuergeraet intern 4 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x46D1 | 46D1 (0) Steuergeraet intern 4 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x46D2 | 46D2 (0) Steuergeraet intern 4 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x46D3 | 46D3 (0) Steuergeraet intern 4 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4293 | 4293 (0) error path for Recovery which is locked | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x73 |
| 0x4403 | 4403 (0) error path for Recovery which is suppressed | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x73 |
| 0x4473 | 4473 (0) error path for Recovery which is visible | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x73 |
| 0x4480 | 4480 (0) xxx internal supply voltage upper limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4491 | 4491 (0) error state supply voltage CJ940 lower limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3F70 | 3F70 (275) Ansauglufttemperaturfuehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x37 | 0x2F | 0x32 | 0x6E |
| 0x3F71 | 3F71 (274) Ansauglufttemperaturfuehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x37 | 0x2F | 0x32 | 0x6E |
| 0x4390 | 4390 (4677) Ladelufttemperaturfuehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4391 | 4391 (4678) Ladelufttemperaturfuehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A41 | 4A41 (0) EWS Schnittstellenfehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A42 | 4A42 (0) EWS Schnittstellenfehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A43 | 4A43 (0) EWS Schnittstellenfehler | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A50 | 4A50 (0) EWS EEPROM Wechselcodeablage fehlerhaft | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A51 | 4A51 (0) EWS EEPROM Wechselcodeablage fehlerhaft | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A60 | 4A60 (0) EWS Manupulation | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A61 | 4A61 (0) EWS Manupulation | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A62 | 4A62 (0) EWS Manupulation | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A63 | 4A63 (0) EWS Manupulation | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44C0 | 44C0 (0) xxx Number of injections limited by charge balance | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44C1 | 44C1 (0) xxx Number of injections limited by charge balance | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44C2 | 44C2 (0) xxx Number of injections limited by charge balance | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4B50 | 4B50 (0) Mengenabgleich | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4B60 | 4B60 (0) Mengendriftkompensation | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44A0 | 44A0 (512) Injektoren Bank 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44A1 | 44A1 (512) Injektoren Bank 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44A2 | 44A2 (0) Injektoren Bank 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44A3 | 44A3 (512) Injektoren Bank 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44AA | 44AA (0) Injektoren Bank 1_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44AB | 44AB (0) Injektoren Bank 1_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44AC | 44AC (512) Injektoren Bank 1_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44AD | 44AD (0) Injektoren Bank 1_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44B0 | 44B0 (0) Injektoren Bank 2 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44B1 | 44B1 (0) Injektoren Bank 2 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44B2 | 44B2 (0) Injektoren Bank 2 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44B3 | 44B3 (0) Injektoren Bank 2 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44BA | 44BA (0) Injektoren Bank 2_1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44BB | 44BB (0) Injektoren Bank 2_1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44BC | 44BC (0) Injektoren Bank 2_1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x44BD | 44BD (0) Injektoren Bank 2_1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x46A0 | 46A0 (512) Steuergeraet intern 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x46A1 | 46A1 (512) Steuergeraet intern 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x46A2 | 46A2 (512) Steuergeraet intern 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x46A3 | 46A3 (512) Steuergeraet intern 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x46B0 | 46B0 (512) Steuergeraet intern 2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x46B1 | 46B1 (512) Steuergeraet intern 2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x46B2 | 46B2 (512) Steuergeraet intern 2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x46B3 | 46B3 (512) Steuergeraet intern 2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4410 | 4410 (513) Injektor Zylinder 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4411 | 4411 (513) Injektor Zylinder 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4412 | 4412 (513) Injektor Zylinder 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4413 | 4413 (513) Injektor Zylinder 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x441A | 441A (0) Injektor Zylinder 1_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x441B | 441B (0) Injektor Zylinder 1_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x441C | 441C (513) Injektor Zylinder 1_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x441D | 441D (0) Injektor Zylinder 1_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4420 | 4420 (514) Injektor Zylinder 2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4421 | 4421 (514) Injektor Zylinder 2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4422 | 4422 (514) Injektor Zylinder 2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4423 | 4423 (514) Injektor Zylinder 2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x442A | 442A (0) Injektor Zylinder 2_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x442B | 442B (0) Injektor Zylinder 2_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x442C | 442C (514) Injektor Zylinder 2_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x442D | 442D (0) Injektor Zylinder 2_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4430 | 4430 (515) Injektor Zylinder 3 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4431 | 4431 (515) Injektor Zylinder 3 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4432 | 4432 (515) Injektor Zylinder 3 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4433 | 4433 (515) Injektor Zylinder 3 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x443A | 443A (0) Injektor Zylinder 3_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x443B | 443B (0) Injektor Zylinder 3_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x443C | 443C (515) Injektor Zylinder 3_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x443D | 443D (0) Injektor Zylinder 3_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4440 | 4440 (516) Injektor Zylinder 4 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4441 | 4441 (516) Injektor Zylinder 4 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4442 | 4442 (516) Injektor Zylinder 4 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4443 | 4443 (516) Injektor Zylinder 4 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x444A | 444A (0) Injektor Zylinder 4_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x444B | 444B (0) Injektor Zylinder 4_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x444C | 444C (516) Injektor Zylinder 4_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x444D | 444D (0) Injektor Zylinder 4_1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4450 | 4450 (517) Injektor Zylinder 5 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4451 | 4451 (517) Injektor Zylinder 5 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4452 | 4452 (517) Injektor Zylinder 5 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4453 | 4453 (517) Injektor Zylinder 5 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x445A | 445A (0) Injektor Zylinder 5_1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x445B | 445B (0) Injektor Zylinder 5_1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x445C | 445C (517) Injektor Zylinder 5_1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x445D | 445D (0) Injektor Zylinder 5_1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4460 | 4460 (518) Injektor Zylinder 6 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4461 | 4461 (518) Injektor Zylinder 6 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4462 | 4462 (518) Injektor Zylinder 6 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4463 | 4463 (518) Injektor Zylinder 6 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x446A | 446A (0) Injektor Zylinder 6_1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x446B | 446B (0) Injektor Zylinder 6_1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x446C | 446C (518) Injektor Zylinder 6_1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x446D | 446D (0) Injektor Zylinder 6_1 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x42D0 | 42D0 (1616) Power Stage fault status for MIL (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x42D1 | 42D1 (1616) Power Stage fault status for MIL (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x42D2 | 42D2 (1616) Power Stage fault status for MIL (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x42D3 | 42D3 (1616) Power Stage fault status for MIL (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4120 | 4120 (5782) DDE-Hauptrelais | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4121 | 4121 (5782) DDE-Hauptrelais | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4DE0 | 4DE0 (0) xxx not used | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4DE1 | 4DE1 (0) xxx not used | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4DE2 | 4DE2 (0) xxx not used | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4DE3 | 4DE3 (0) xxx not used | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3FB5 | 3FB5 (0) faultpath for task counter and OvR state consistency error | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3FB6 | 3FB6 (0) faultpath for task counter and OvR state consistency error | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3FB7 | 3FB7 (0) faultpath for task counter and OvR state consistency error | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3FC5 | 3FC5 (0) faultpath for irreversible faults | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3FE5 | 3FE5 (0) faultpath for irreversible faults | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3FF5 | 3FF5 (0) faultpath for irreversible faults | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4005 | 4005 (0) faultpath for shut off Vehicle | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4015 | 4015 (0) faultpath for reversible faults | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4025 | 4025 (0) faultpath for reversible faults | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4035 | 4035 (0) faultpath for reversible faults | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4045 | 4045 (0) faultpath for errors with priority 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4055 | 4055 (0) faultpath for errors with priority 2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4065 | 4065 (0) faultpath for private CAN | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4075 | 4075 (0) faultpath for Mil Lamp | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4085 | 4085 (0) faultpath for SysLamp | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4095 | 4095 (0) faultpath for fuel quantity limitation | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x40A5 | 40A5 (0) faultpath for coordination drive train | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x40B5 | 40B5 (0) faultpath for coordination vehicle | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x40C5 | 40C5 (0) faultpath for external desired torque | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x40D5 | 40D5 (0) faultpath for torque limitation | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x40E5 | 40E5 (0) faultpath for torque limitation | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x40F5 | 40F5 (0) faultpath for torque limitation | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x45E3 | 45E3 (0) error path for ECU-Selection [CAN-Communication] | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3EC7 | 3EC7 (0) error path for ECU-Selection | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x45F2 | 45F2 (0) error path for ECU-Selection Begin and Ini | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x45F3 | 45F3 (0) error path for ECU-Selection Begin and Ini | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4792 | 4792 (0) error path for ECU-Selection | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4793 | 4793 (0) error path for ECU-Selection | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4107 | 4107 (0) faultpath MS software comparison between master and slave | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4108 | 4108 (0) faultpath MS software comparison between master and slave | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4118 | 4118 (0) faultpath MS software comparison between master and slave, difference in eeprom | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4302 | 4302 (4752) Mengenregelventil Uet Unt | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |
| 0x4303 | 4303 (4753) Mengenregelventil Uet Unt | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |
| 0x4310 | 4310 (4754) Mengenregelventil KS B+ | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |
| 0x4321 | 4321 (4755) Mengenregelventil KS B- | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |
| 0x4730 | 4730 (4756) Mengenregelventil Stromregelung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |
| 0x4731 | 4731 (4757) Mengenregelventil Stromregelung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |
| 0x4732 | 4732 (4758) Mengenregelventil Stromregelung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |
| 0x4397 | 4397 (4759) Mengenregelventil Stellertest | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |
| 0x4703 | 4703 (0) Steuergeraet intern 7 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0xCD87 | CD87 (0) CAN Bus | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x48F2 | 48F2 (0) CAN Bus | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x48F3 | 48F3 (0) CAN Bus | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4910 | 4910 (0) faultpath CAN B (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4912 | 4912 (0) faultpath CAN B (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4913 | 4913 (0) faultpath CAN B (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x42C0 | 42C0 (0) Oeldruckkontrolllampe | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xAF |
| 0x42C1 | 42C1 (0) Oeldruckkontrolllampe | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xAF |
| 0x42C2 | 42C2 (0) Oeldruckkontrolllampe | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xAF |
| 0x42C3 | 42C3 (0) Oeldruckkontrolllampe | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xAF |
| 0x3F90 | 3F90 (0) Oeldruckfuehler (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3F91 | 3F91 (0) Oeldruckfuehler (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3FA0 | 3FA0 (0) error path of oil temperature sensor (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3FA1 | 3FA1 (0) error path of oil temperature sensor (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3FA2 | 3FA2 (0) error path of oil temperature sensor (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3FA3 | 3FA3 (0) error path of oil temperature sensor (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4740 | 4740 (0) Steuergeraet intern 11 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3EB0 | 3EB0 (0) Drehzahlberechnung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4030 | 4030 (0) Abgastemperaturfuehler vor Katalysator (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4031 | 4031 (0) Abgastemperaturfuehler vor Katalysator (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4CD3 | 4CD3 (0) Oxidation catalyst implausible | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4DA3 | 4DA3 (0) difference in air masses in balance governor | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4521 | 4521 (4629) Ladedruckregelung neg | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x7A | 0x7B | 0x6E |
| 0x4530 | 4530 (4628) Ladedruckregelung pos | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x7A | 0x7B | 0x6E |
| 0x4332 | 4332 (144) Raildruckregelventil Unt Uet | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |
| 0x4333 | 4333 (145) Raildruckregelventil Unt Uet | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |
| 0x4340 | 4340 (146) Raildruckregelventil KS B+ | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |
| 0x4351 | 4351 (145) Raildruckregelventil KS B- | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |
| 0x4360 | 4360 (4213) Raildruckregelventil Stromregelung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |
| 0x4361 | 4361 (4214) Raildruckregelventil Stromregelung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |
| 0x4362 | 4362 (4215) Raildruckregelventil Stromregelung | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |
| 0x4382 | 4382 (4728) Raildruckregelventil Stellertest | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |
| 0x4378 | 4378 (137) Raildruckregelventil Test (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |
| 0x4C40 | 4C40 (0) xxx Short Circuit Battery | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C41 | 4C41 (0) xxx Short Circuit Battery | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C42 | 4C42 (0) xxx Short Circuit Battery | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4C43 | 4C43 (0) xxx Short Circuit Battery | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4010 | 4010 (0) Abgasgegendruckfuehler vor Partikelfilter (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4011 | 4011 (0) Abgasgegendruckfuehler vor Partikelfilter (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4020 | 4020 (0) Abgastemperaturfuehler vor Partikelfilter (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4021 | 4021 (0) Abgastemperaturfuehler vor Partikelfilter (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4CE0 | 4CE0 (0) xxx Diffrential pressure above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4CF3 | 4CF3 (0) dynamics of diffrential pressure signal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D00 | 4D00 (0) xxx pressure  above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D01 | 4D01 (0) xxx pressure  above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D03 | 4D03 (0) xxx pressure  above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D13 | 4D13 (0) hose line defective | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D23 | 4D23 (0) pressure sensor blocked | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D30 | 4D30 (0) xxx Flow resistance above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D31 | 4D31 (0) xxx Flow resistance above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D40 | 4D40 (0) xxx permanent regeneration | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D53 | 4D53 (0) plausibility of temp sensors oxidation catalyst | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D60 | 4D60 (0) xxx temperature ahead PFlt above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D61 | 4D61 (0) xxx temperature ahead PFlt above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D63 | 4D63 (0) xxx temperature ahead PFlt above limit | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4D73 | 4D73 (0) plausibility check of general temp sensors | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4750 | 4750 (0) Steuergeraet intern 12 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4753 | 4753 (0) Steuergeraet intern 12 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3F30 | 3F30 (403) Raildrucksensor | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xD3 |
| 0x3F31 | 3F31 (402) Raildrucksensor | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xD3 |
| 0x3F40 | 3F40 (0) Raildrucksensor Offsmaxmin (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0xD3 | 0x2F | 0x32 | 0x5B |
| 0x3F41 | 3F41 (0) Raildrucksensor Offsmaxmin (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0xD3 | 0x2F | 0x32 | 0x5B |
| 0x4B90 | 4B90 (0) Raildruckueberwachung Start | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x42F2 | 42F2 (0) Umschaltung Raildruckregelung MeUn | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x42E2 | 42E2 (0) Umschaltung Raildruckregelung PCV | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4560 | 4560 (4224) Raildruck-Plausibilitaet mengengeregelt Maxpos | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xEC |
| 0x4570 | 4570 (0) Raildruck-Plausibilitaet mengengeregelt Maxposfuelflow | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xEC |
| 0x4580 | 4580 (4226) Raildruck-Plausibilitaet mengengeregelt Neg | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xEC |
| 0x4590 | 4590 (135) Raildruck-Plausibilitaet mengengeregelt Minpres | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xEC |
| 0x45A0 | 45A0 (136) Raildruck-Plausibilitaet mengengeregelt Maxpres | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xEC |
| 0x45C0 | 45C0 (0) Raildruck-Plausibilitaet mengengeregelt setmetov (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xEC |
| 0x4B80 | 4B80 (0) Raildruck-Plausibilitaet mengengeregelt panicpress (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xEC |
| 0x4600 | 4600 (4240) Raildruck-Plausibilitaet druckgeregelt posdev | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xED |
| 0x4610 | 4610 (0) Raildruck-Plausibilitaet druckgeregelt posdevTV | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xED |
| 0x4620 | 4620 (4242) Raildruck-Plausibilitaet druckgeregelt negdevclosPCV | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xED |
| 0x4630 | 4630 (135) Raildruck-Plausibilitaet druckgeregelt MinP | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xED |
| 0x4640 | 4640 (136) Raildruck-Plausibilitaet druckgeregelt MaxP | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xED |
| 0x4650 | 4650 (0) Raildruck-Plausibilitaet druckgeregelt PlausP/I (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xED |
| 0x44F0 | 44F0 (0) xxx panic pressure test limit exceeded | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xED |
| 0x4711 | 4711 (0) Steuergeraet intern 8 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4712 | 4712 (0) Steuergeraet intern 8 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4713 | 4713 (0) Steuergeraet intern 8 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4670 | 4670 (0) Speisespannung 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4671 | 4671 (0) Speisespannung 1 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4680 | 4680 (1603) Speisespannung 2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4681 | 4681 (1602) Speisespannung 2 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4690 | 4690 (0) Speisespannung 3 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4691 | 4691 (0) Speisespannung 3 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4125 | 4125 (0) sensor supply voltage 4 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4125 | 4125 (0) sensor supply voltage 4 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4135 | 4135 (0) sensor supply voltage 5 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4135 | 4135 (0) sensor supply voltage 5 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4145 | 4145 (0) sensor supply voltage 6 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4145 | 4145 (0) sensor supply voltage 6 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4B71 | 4B71 (0) ZMS Pulsation | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4763 | 4763 (0) Steuergeraet intern 13 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x43A0 | 43A0 (0) Error path for the starter relay actuator (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x43A1 | 43A1 (0) Error path for the starter relay actuator (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x43A2 | 43A2 (0) Error path for the starter relay actuator (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x43A3 | 43A3 (0) Error path for the starter relay actuator (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x43B0 | 43B0 (0) Power Stage fault status for System lamp (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x43B1 | 43B1 (0) Power Stage fault status for System lamp (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x43B2 | 43B2 (0) Power Stage fault status for System lamp (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x43B3 | 43B3 (0) Power Stage fault status for System lamp (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A02 | 4A02 (0) Klemme 15 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4A03 | 4A03 (0) Klemme 15 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4772 | 4772 (0) Steuergeraet intern 14 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4773 | 4773 (0) Steuergeraet intern 14 (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x43C0 | 43C0 (0) fault path for short circuit to battery for TVA power stage (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEA |
| 0x43D1 | 43D1 (0) fault path for short circuit to ground for TVA power stage (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEA |
| 0x43E2 | 43E2 (0) fault path for no load and excess temparature for TVA power stage (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEA |
| 0x43E3 | 43E3 (0) fault path for no load and excess temparature for TVA power stage (nv) | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEA |
| 0x4130 | 4130 (5141) Drallklappe KS B+ | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEB |
| 0x4141 | 4141 (5142) Drallklappe KS B- | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEB |
| 0x4152 | 4152 (5143) Drallklappe Uet Untbr | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEB |
| 0x4153 | 4153 (5144) Drallklappe Uet Untbr | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEB |
| 0x3F50 | 3F50 (0) Fahrgeschwindigkeitssignal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3F51 | 3F51 (0) Fahrgeschwindigkeitssignal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3F52 | 3F52 (0) Fahrgeschwindigkeitssignal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3F53 | 3F53 (0) Fahrgeschwindigkeitssignal | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x3F62 | 3F62 (1280) Fahrgeschwindigkeitssignal ueber CAN | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x4723 | 4723 (0) Steuergeraet intern 9 | 0x2D | 0x2C | 0xC2 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |
| 0x0000 | XXXX Unbekannter Fehlerort | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 35 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x2B | Wassertemperatur Spannungsrohwert | mV | - | unsigned char | - | 21.6 | 1 | 0 |
| 0x2C | Kühlmitteltemperatur | deg C | - | unsigned char | - | 1.00 | 1 | -50.2 |
| 0x2D | mittlere Motordrehzahl | rpm | - | unsigned char | - | 27.5 | 1 | 0 |
| 0x2F | Batteriespannung | mV | - | unsigned char | - | 162. | 1 | 0 |
| 0x32 | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 0.986 | 1 | 0 |
| 0x34 | Einspritzmenge Sollwert | mg/cyc | - | unsigned char | - | 0.393 | 1 | 0 |
| 0x37 | Lufttemperatur Spannungsrohwert | mV | - | unsigned char | - | 21.6 | 1 | 0 |
| 0x38 | Ansauglufttemperatur | deg C | - | unsigned char | - | 1.00 | 1 | -50.2 |
| 0x39 | Spannungsrohwert des Ladedrucksensors | mV | - | unsigned char | - | 21.6 | 1 | 0 |
| 0x3A | Ladedruckwert | hPa | - | unsigned char | - | 9.84 | 1 | 0 |
| 0x48 | linearisierter APP1 | % | - | unsigned char | - | 0.787 | 1 | 0 |
| 0x49 | Linearisierter APP2 | % | - | unsigned char | - | 0.787 | 1 | 0 |
| 0x50 | angesaugte Luftmasse pro Zylinder | mg/Hub | - | unsigned char | - | 6.30 | 1 | 0 |
| 0x5B | Kraftstofftemperatur | deg C | - | unsigned char | - | 1.00 | 1 | -50.2 |
| 0x61 | Zustand der Glühanzeige | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x62 | Airwalvecontrol | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x6E | Atmosphärendruck | hPa | - | unsigned char | - | 9.84 | 1 | 0 |
| 0x6F | Rohspannung ADC-Signal Atmosphärendruck | mV | - | unsigned char | - | 21.6 | 1 | 0 |
| 0x73 | Herkunft des letzten Reset ( &gt;0 = Recovery ) | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x7A | Tastverhältnis zür Endstufenansteuerung | % | - | unsigned char | - | 0.787 | 1 | 0 |
| 0x7B | Tastverhältnis zür Endstufenansteuerung | % | - | unsigned char | - | 0.787 | 1 | 0 |
| 0x96 | aktuelles rückgerechnetes inneres Motormoment | Nm | - | unsigned char | - | 29.2 | 1 | -2486. |
| 0x97 | Leerlaufreglermoment | Nm | - | unsigned char | - | 29.2 | 1 | -2486. |
| 0xAF | Ausgangssignal Öldruckschalter | - | - | unsigned char | - | 1 | 1 | 0 |
| 0xB0 | Meta-Status der KW- und NW-Ereignisverwaltung | - | - | unsigned char | - | 1 | 1 | 0 |
| 0xC2 | maximaler Raildruck der letzten 10ms | bar | - | unsigned char | - | 7.87 | 1 | 0 |
| 0xC3 | Raildruck-sollwert | bar | - | unsigned char | - | 7.87 | 1 | 0 |
| 0xD3 | Rohwert des Raildrucks | mV | - | unsigned char | - | 21.6 | 1 | 0 |
| 0xD4 | Spannungsrohwert der Kraftstoffstemperatur | mV | - | unsigned char | - | 21.6 | 1 | 0 |
| 0xE8 | dutycycle Ubatt-corrected | % | - | unsigned char | - | 0.787 | 1 | 0 |
| 0xE9 | Zusatzheizer Tastverhaeltnis | % | - | unsigned char | - | 0.787 | 1 | 0 |
| 0xEA | Tastverhältnis zür Endstufenansteuerung | % | - | unsigned char | - | 0.787 | 1 | 0 |
| 0xEB | Tastverhältnis zür Endstufenansteuerung | % | - | unsigned char | - | 0.787 | 1 | 0 |
| 0xEC | Tastverhaeltnis Mengenregelungsventil | % | - | unsigned char | - | 0.787 | 1 | 0 |
| 0xED | Tastverhaeltnis Druckregelventil | % | - | unsigned char | - | 0.787 | 1 | 0 |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 531 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4820 | 0x00 | 0x03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4821 | 0x00 | 0x00 | 0x00 | 0x04 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4822 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4823 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40B0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40B1 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40B2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40B3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40C0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40C1 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40D0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40D1 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4112 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x08 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4113 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x08 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4780 | 0x00 | 0x09 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4781 | 0x00 | 0x00 | 0x00 | 0x0A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4782 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x0B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4783 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x0C | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4170 | 0x00 | 0x03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4171 | 0x00 | 0x00 | 0x00 | 0x04 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4172 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4173 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4370 | 0x00 | 0x0D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4830 | 0x00 | 0x0E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4831 | 0x00 | 0x00 | 0x00 | 0x0F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3E95 | 0x00 | 0x0E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3E96 | 0x00 | 0x00 | 0x00 | 0x0F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FE0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FE1 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EB5 | 0x00 | 0x10 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EB6 | 0x00 | 0x00 | 0x00 | 0x11 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FF0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FF1 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4CA5 | 0x00 | 0x12 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4CA6 | 0x00 | 0x00 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BA0 | 0x00 | 0x14 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BA1 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EA5 | 0x00 | 0x14 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EA6 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BB0 | 0x00 | 0x16 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BB1 | 0x00 | 0x00 | 0x00 | 0x17 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C75 | 0x00 | 0x16 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C76 | 0x00 | 0x00 | 0x00 | 0x17 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BB5 | 0x00 | 0x18 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BB6 | 0x00 | 0x00 | 0x00 | 0x19 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3ED5 | 0x00 | 0x18 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3ED6 | 0x00 | 0x00 | 0x00 | 0x19 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BC0 | 0x00 | 0x18 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BC1 | 0x00 | 0x00 | 0x00 | 0x19 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BC2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EE5 | 0x00 | 0x18 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EE6 | 0x00 | 0x00 | 0x00 | 0x19 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EE7 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BC5 | 0x00 | 0x1B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BC6 | 0x00 | 0x00 | 0x00 | 0x1C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BC7 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EF5 | 0x00 | 0x1B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EF6 | 0x00 | 0x00 | 0x00 | 0x1C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EF7 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43F0 | 0x00 | 0x03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43F1 | 0x00 | 0x00 | 0x00 | 0x04 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43F2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43F3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4AB0 | 0x00 | 0x1E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4AB2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4AC0 | 0x00 | 0x1F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4AC2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4AD0 | 0x00 | 0x20 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4AD2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x20 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F10 | 0x00 | 0x21 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F11 | 0x00 | 0x00 | 0x00 | 0x22 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F13 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x23 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F20 | 0x00 | 0x21 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F21 | 0x00 | 0x00 | 0x00 | 0x22 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F23 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x23 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4060 | 0x00 | 0x21 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4061 | 0x00 | 0x00 | 0x00 | 0x22 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4063 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x24 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BD2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4093 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x26 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C71 | 0x00 | 0x00 | 0x00 | 0x27 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4501 | 0x00 | 0x00 | 0x00 | 0x28 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4841 | 0x00 | 0x00 | 0x00 | 0x29 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4507 | 0x00 | 0x2A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4850 | 0x00 | 0x2B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40E0 | 0x00 | 0x2C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F57 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x2D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F67 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x2D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F77 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x2D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F87 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x2D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F97 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x2D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FA7 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x2D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4180 | 0x00 | 0x03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4550 | 0x00 | 0x2E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4191 | 0x00 | 0x00 | 0x00 | 0x04 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D81 | 0x00 | 0x00 | 0x00 | 0x2F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x41A2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x41A3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A22 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A23 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x30 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F00 | 0x00 | 0x21 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F01 | 0x00 | 0x00 | 0x00 | 0x22 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F02 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x31 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x32 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4660 | 0x00 | 0x33 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4661 | 0x00 | 0x00 | 0x00 | 0x34 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4082 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x35 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4083 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x36 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A10 | 0x00 | 0x37 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A13 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EE0 | 0x00 | 0x38 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EE1 | 0x00 | 0x00 | 0x00 | 0x39 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EE2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EE3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3B | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EF3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4880 | 0x00 | 0x3C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4890 | 0x00 | 0x3C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4930 | 0x00 | 0x3C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4940 | 0x00 | 0x3C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4950 | 0x00 | 0x3C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4960 | 0x00 | 0x3C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4870 | 0x00 | 0x3C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x47A0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x47B0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x47C0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x47D0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x47E0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x47F0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C80 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C90 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D92 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D93 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3E | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4900 | 0x00 | 0x3F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4072 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x40 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4073 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x41 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A30 | 0x00 | 0x42 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A31 | 0x00 | 0x00 | 0x00 | 0x43 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A32 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x44 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A33 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x43 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F80 | 0x00 | 0x38 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F81 | 0x00 | 0x00 | 0x00 | 0x39 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F82 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x45 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x41C0 | 0x00 | 0x03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x41C1 | 0x00 | 0x00 | 0x00 | 0x04 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x41C2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x41C3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4AE0 | 0x00 | 0x03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4AE1 | 0x00 | 0x00 | 0x00 | 0x04 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4AE2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4AE3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4AF0 | 0x00 | 0x21 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4AF1 | 0x00 | 0x00 | 0x00 | 0x22 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4B00 | 0x00 | 0x46 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x41B0 | 0x00 | 0x03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4DB0 | 0x00 | 0x2E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x41D1 | 0x00 | 0x00 | 0x00 | 0x04 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4DC1 | 0x00 | 0x00 | 0x00 | 0x2F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x41E2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x41E3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x47 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4DD2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4DD3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x30 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EC0 | 0x00 | 0x48 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EC1 | 0x00 | 0x00 | 0x00 | 0x40 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3ED0 | 0x00 | 0x49 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3ED1 | 0x00 | 0x00 | 0x00 | 0x4A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3E90 | 0x00 | 0x48 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3E91 | 0x00 | 0x00 | 0x00 | 0x40 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EA0 | 0x00 | 0x49 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EA1 | 0x00 | 0x00 | 0x00 | 0x4A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BD5 | 0x00 | 0x4B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BD6 | 0x00 | 0x00 | 0x00 | 0x4C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BD7 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BD8 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x4D | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4B10 | 0x00 | 0x4E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4B11 | 0x00 | 0x00 | 0x00 | 0x4F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A70 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x50 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4000 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4001 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x41F0 | 0x00 | 0x03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x41F1 | 0x00 | 0x00 | 0x00 | 0x04 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x41F2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x41F3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4B20 | 0x00 | 0x51 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4B22 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x51 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4B30 | 0x00 | 0x52 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4B32 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x52 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4B40 | 0x00 | 0x53 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4B42 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x53 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A80 | 0x00 | 0x54 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4040 | 0x00 | 0x55 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4041 | 0x00 | 0x00 | 0x00 | 0x56 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4042 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x57 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BE2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BE7 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4BF7 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C00 | 0x00 | 0x59 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C01 | 0x00 | 0x00 | 0x00 | 0x5A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C02 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4CA2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4CB2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C06 | 0x00 | 0x00 | 0x00 | 0x5A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C12 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C15 | 0x00 | 0x59 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C16 | 0x00 | 0x00 | 0x00 | 0x5A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C17 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C20 | 0x00 | 0x59 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C21 | 0x00 | 0x00 | 0x00 | 0x5A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C22 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4DF0 | 0x00 | 0x59 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4DF1 | 0x00 | 0x00 | 0x00 | 0x5A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4DF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C27 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C30 | 0x00 | 0x5B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C31 | 0x00 | 0x00 | 0x00 | 0x5C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C32 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x5D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C33 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x5E | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C35 | 0x00 | 0x5F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C36 | 0x00 | 0x00 | 0x00 | 0x60 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C37 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x61 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C38 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x62 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4970 | 0x00 | 0x63 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4971 | 0x00 | 0x00 | 0x00 | 0x64 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4972 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x65 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4973 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x66 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4CC0 | 0x00 | 0x67 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4920 | 0x00 | 0x68 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4203 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x69 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4211 | 0x00 | 0x00 | 0x00 | 0x6A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4212 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x6B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4213 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4221 | 0x00 | 0x00 | 0x00 | 0x6A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4222 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x6B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4223 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4231 | 0x00 | 0x00 | 0x00 | 0x6A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4232 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x6B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4233 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4241 | 0x00 | 0x00 | 0x00 | 0x6A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4242 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x6B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4243 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4251 | 0x00 | 0x00 | 0x00 | 0x6A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4252 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x6B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4253 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4261 | 0x00 | 0x00 | 0x00 | 0x6A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4262 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x6B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4263 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4271 | 0x00 | 0x00 | 0x00 | 0x6A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4272 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x6B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4273 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4281 | 0x00 | 0x00 | 0x00 | 0x6A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4282 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x6B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4283 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42A0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42A1 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42A2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42A3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42B1 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42B2 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x46C0 | 0x00 | 0x6C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x46D0 | 0x00 | 0x6D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x46D1 | 0x00 | 0x00 | 0x00 | 0x6E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x46D2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x6F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x46D3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x70 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4293 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x71 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4403 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x71 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4473 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x71 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4480 | 0x00 | 0x72 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4491 | 0x00 | 0x00 | 0x00 | 0x73 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F70 | 0x00 | 0x38 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F71 | 0x00 | 0x00 | 0x00 | 0x39 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4390 | 0x00 | 0x38 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4391 | 0x00 | 0x00 | 0x00 | 0x39 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A41 | 0x00 | 0x00 | 0x00 | 0x74 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A42 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x48 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A43 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x75 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A50 | 0x00 | 0x76 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A51 | 0x00 | 0x00 | 0x00 | 0x77 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A60 | 0x00 | 0x78 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A61 | 0x00 | 0x00 | 0x00 | 0x79 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A62 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x7A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A63 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x7B | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44C0 | 0x00 | 0x7C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44C1 | 0x00 | 0x00 | 0x00 | 0x7D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44C2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x7E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4B50 | 0x00 | 0x7F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4B60 | 0x00 | 0x7F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44A0 | 0x00 | 0x80 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44A1 | 0x00 | 0x00 | 0x00 | 0x81 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44A2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44A3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x82 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44AA | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44AB | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44AC | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x83 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44AD | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x84 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44B0 | 0x00 | 0x80 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44B1 | 0x00 | 0x00 | 0x00 | 0x81 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44B2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44B3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x82 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44BA | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44BB | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44BC | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x83 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44BD | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x46A0 | 0x00 | 0x85 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x46A1 | 0x00 | 0x00 | 0x00 | 0x86 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x46A2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x87 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x46A3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x88 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x46B0 | 0x00 | 0x89 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x46B1 | 0x00 | 0x00 | 0x00 | 0x8A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x46B2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x8B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x46B3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x8C | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4410 | 0x00 | 0x8D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4411 | 0x00 | 0x00 | 0x00 | 0x8E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4412 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x8F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4413 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x82 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x441A | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x441B | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x441C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x90 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x441D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4420 | 0x00 | 0x8D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4421 | 0x00 | 0x00 | 0x00 | 0x8E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4422 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x8F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4423 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x82 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x442A | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x442B | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x442C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x90 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x442D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4430 | 0x00 | 0x8D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4431 | 0x00 | 0x00 | 0x00 | 0x8E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4432 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x8F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4433 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x82 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x443A | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x443B | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x443C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x90 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x443D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4440 | 0x00 | 0x8D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4441 | 0x00 | 0x00 | 0x00 | 0x8E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4442 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x8F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4443 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x82 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x444A | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x444B | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x444C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x90 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x444D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4450 | 0x00 | 0x8D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4451 | 0x00 | 0x00 | 0x00 | 0x8E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4452 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x8F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4453 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x82 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x445A | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x445B | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x445C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x90 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x445D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4460 | 0x00 | 0x8D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4461 | 0x00 | 0x00 | 0x00 | 0x8E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4462 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x8F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4463 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x82 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x446A | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x446B | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x446C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x90 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x446D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42D0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42D1 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42D2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42D3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4120 | 0x00 | 0x91 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4121 | 0x00 | 0x00 | 0x00 | 0x92 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4DE0 | 0x00 | 0x93 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4DE1 | 0x00 | 0x00 | 0x00 | 0x93 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4DE2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x94 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4DE3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x93 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FB5 | 0x00 | 0x95 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FB6 | 0x00 | 0x00 | 0x00 | 0x96 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FB7 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x97 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FC5 | 0x00 | 0x98 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FE5 | 0x00 | 0x99 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FF5 | 0x00 | 0x9A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4005 | 0x00 | 0x9B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4015 | 0x00 | 0x9C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4025 | 0x00 | 0x9D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4035 | 0x00 | 0x9E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4045 | 0x00 | 0x9F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4055 | 0x00 | 0xA0 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4065 | 0x00 | 0xA1 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4075 | 0x00 | 0xA2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4085 | 0x00 | 0xA3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4095 | 0x00 | 0xA4 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40A5 | 0x00 | 0xA5 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40B5 | 0x00 | 0xA6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40C5 | 0x00 | 0xA7 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40D5 | 0x00 | 0xA8 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40E5 | 0x00 | 0xA9 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x40F5 | 0x00 | 0xAA | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x45E3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xAB | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EC7 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xAC | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x45F2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xAD | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x45F3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xAE | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4792 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xAC | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4793 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xAF | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4107 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x2D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4108 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xB0 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4118 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xB0 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4302 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4303 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4310 | 0x00 | 0x03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4321 | 0x00 | 0x00 | 0x00 | 0x04 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4730 | 0x00 | 0xB1 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4731 | 0x00 | 0x00 | 0x00 | 0xB2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4732 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xB3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4397 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xB4 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4703 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xB5 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0xCD87 | 0x00 | 0xB6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x48F2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xB7 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x48F3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xB8 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4910 | 0x00 | 0xB6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4912 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xB7 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4913 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xB8 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42C0 | 0x00 | 0x03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42C1 | 0x00 | 0x00 | 0x00 | 0x04 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42C2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42C3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F90 | 0x00 | 0x21 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F91 | 0x00 | 0x00 | 0x00 | 0x39 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FA0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FA1 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FA2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xB9 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3FA3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4740 | 0x00 | 0xBA | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3EB0 | 0x00 | 0xBB | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4030 | 0x00 | 0x21 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4031 | 0x00 | 0x00 | 0x00 | 0x22 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4CD3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xBC | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4DA3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xBD | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4521 | 0x00 | 0x00 | 0x00 | 0xBE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4530 | 0x00 | 0xBF | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4332 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4333 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4340 | 0x00 | 0x03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4351 | 0x00 | 0x00 | 0x00 | 0x04 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4360 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4361 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4362 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xB3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4382 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xC0 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4378 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xC1 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C40 | 0x00 | 0x2E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C41 | 0x00 | 0x00 | 0x00 | 0x2F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C42 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4C43 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x30 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4010 | 0x00 | 0x21 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4011 | 0x00 | 0x00 | 0x00 | 0x22 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4020 | 0x00 | 0x21 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4021 | 0x00 | 0x00 | 0x00 | 0x22 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4CE0 | 0x00 | 0xC2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4CF3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xC3 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D00 | 0x00 | 0xC4 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D01 | 0x00 | 0x00 | 0x00 | 0xC5 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xC6 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D13 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xC7 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D23 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xC8 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D30 | 0x00 | 0xC9 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D31 | 0x00 | 0x00 | 0x00 | 0xCA | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D40 | 0x00 | 0xCB | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D53 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xCC | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D60 | 0x00 | 0xCD | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D61 | 0x00 | 0x00 | 0x00 | 0xCE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D63 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xCC | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4D73 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xCC | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4750 | 0x00 | 0xCF | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4753 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xD0 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F30 | 0x00 | 0x38 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F31 | 0x00 | 0x00 | 0x00 | 0x39 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F40 | 0x00 | 0xD1 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F41 | 0x00 | 0x00 | 0x00 | 0xD2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4B90 | 0x00 | 0xD3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42F2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xD4 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x42E2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xD5 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4560 | 0x00 | 0xD6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4570 | 0x00 | 0xD7 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4580 | 0x00 | 0xD8 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4590 | 0x00 | 0xD9 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x45A0 | 0x00 | 0xDA | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x45C0 | 0x00 | 0xDB | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4B80 | 0x00 | 0xDC | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4600 | 0x00 | 0xD6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4610 | 0x00 | 0xDD | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4620 | 0x00 | 0xDE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4630 | 0x00 | 0xD9 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4640 | 0x00 | 0xDA | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4650 | 0x00 | 0xDF | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x44F0 | 0x00 | 0xE0 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4711 | 0x00 | 0x00 | 0x00 | 0xE1 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4712 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xE2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4713 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xE3 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4670 | 0x00 | 0x37 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4671 | 0x00 | 0x00 | 0x00 | 0xE4 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4680 | 0x00 | 0x37 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4681 | 0x00 | 0x00 | 0x00 | 0xE4 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4690 | 0x00 | 0x37 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4691 | 0x00 | 0x00 | 0x00 | 0xE4 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4125 | 0x00 | 0xE5 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4125 | 0x00 | 0x00 | 0x00 | 0x16 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4135 | 0x00 | 0xE6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4135 | 0x00 | 0x00 | 0x00 | 0x16 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4145 | 0x00 | 0xE7 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4145 | 0x00 | 0x00 | 0x00 | 0x16 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4B71 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xE8 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4763 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xE9 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43A0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43A1 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43A2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43A3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43B0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43B1 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43B2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43B3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A02 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEA | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4A03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4772 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEC | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4773 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xED | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43C0 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43D1 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43E2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x43E3 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x07 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4130 | 0x00 | 0x03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4141 | 0x00 | 0x00 | 0x00 | 0x04 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4152 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4153 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F50 | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F51 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F52 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x31 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F53 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEF | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x3F62 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF0 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |
| 0x4723 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF1 | 0x00 | 0x00 | 0x00 | 0x00 | 0xFA | 0xFC | 0x00 | 0x00 |

<a id="table-farttexte-erw"></a>
### FARTTEXTE_ERW

Dimensions: 251 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | - |
| 0x01 | ??? |
| 0x03 | Ansteuerung Kurzschluss nach B+ |
| 0x04 | Ansteuerung Kurzschluss nach B- |
| 0x05 | Ansteuerung Unterbrechung |
| 0x06 | Endstufe Uebertemperatur |
| 0x07 | nicht verwendet |
| 0x08 | CAN nicht verwendet |
| 0x09 | Analog-/Digital-Wandler Spannung zu hoch |
| 0x0A | Analog-/Digital-Wandler Spannung zu niedrig |
| 0x0B | Analog-/Digital-Wandler Testimpuls-Fehler |
| 0x0C | Analog-/Digital-Wandler Interner Fehler |
| 0x0D | the difference in the two air flows is biger than max. allowed |
| 0x0E | SRC max error for the duty cycle |
| 0x0F | SRC min error for the duty cycle |
| 0x10 | airmass ADC raw value &gt; threshold high |
| 0x11 | airmass ADC raw value &lt; threshold low |
| 0x12 | airmass ratio is higher then threshold high |
| 0x13 | airmass ratio is lower then threshold low |
| 0x14 | air temparature above upper Limit |
| 0x15 | air temparature below lower Limit |
| 0x16 | Voltage above upper Limit |
| 0x17 | Voltage below lower Limit |
| 0x18 | Signal range check high error |
| 0x19 | Signal range check low error |
| 0x1A | raw air mass signal out side the range |
| 0x1B | SRC max error for the time period |
| 0x1C | SRC min error for the time period |
| 0x1D | reference signal out side the range |
| 0x1E | Uebertemperaturerkennung im Zuheizer |
| 0x1F | Fehler Zuheizer 2 |
| 0x20 | Fehler Zuheizer 3 |
| 0x21 | Signal Kurzschluss nach B+ |
| 0x22 | Signal Unterbrechung oder Kurzschluss nach B- |
| 0x23 | Plausibilitaet zwischen Poti 1 und 2 verletzt |
| 0x24 | Plausibilitaet mit Ladedruckfuehler bei Leerlauf |
| 0x25 | No load |
| 0x26 | BRE nicht verwendet |
| 0x27 | additive tank is  - empty - |
| 0x28 | Negative Regelabweichung / Luftmasse zu hoch |
| 0x29 | negative governor2 deviation below limit |
| 0x2A | Positive Regelabweichung / Luftmasse zu niedrig |
| 0x2B | positive governor2 deviation above limit |
| 0x2C | Ladekontrolleuchte an |
| 0x2D | Signal fault |
| 0x2E | Short Circuit Battery |
| 0x2F | Short Circuit Ground |
| 0x30 | Excess Temperature |
| 0x31 | Signal fehlerhaft |
| 0x32 | Plausibilitaet mit Atmosphaerendruckfuehler bei Leerlauf |
| 0x33 | Versorgungsspannung DDE ueberschritten |
| 0x34 | Versorgungsspannung DDE unterschritten |
| 0x35 | brake signal is defective |
| 0x36 | Plausibilitaet der Bremssignale im Fahrbetrieb |
| 0x37 | Kurzschluss nach B+ |
| 0x38 | Signal Unterbrechung oder Kurzschluss nach B+ |
| 0x39 | Signal Kurzschluss nach B- |
| 0x3A | CAN Wert nicht plausibel |
| 0x3B | plausibility defect between OTS and CTS |
| 0x3C | number of recognized misfire events above limit |
| 0x3D | Lead Diff |
| 0x3E | Des Diff |
| 0x3F | Unplausibler Eingriff |
| 0x40 | falsches Signal |
| 0x41 | Plausibilitaet mit Gangwechsel |
| 0x42 | kein Signal oder MFL nicht verbaut |
| 0x43 | falsches Signal von MFL |
| 0x44 | kein Signal von MFL |
| 0x45 | Signal error from CAN |
| 0x46 | Temperatur zu hoch |
| 0x47 | Ansteuerung Endstufe Uebertemperatur |
| 0x48 | kein Signal |
| 0x49 | kurzzeitig kein Signal |
| 0x4A | kurzzeitig falsches Signal |
| 0x4B | Short Circuit to Battery |
| 0x4C | Short Circuit to Gnd |
| 0x4D | High Temperature |
| 0x4E | Korrekturmenge zu hoch |
| 0x4F | Korrekturmenge zu niedrig |
| 0x50 | Kennfeldwerte nicht plausibel |
| 0x51 | Blockiererkennung |
| 0x52 | Elektroluefter 2 |
| 0x53 | Elektroluefter 3 |
| 0x54 | Ladeluftschlauch abgefallen |
| 0x55 | Maximum fault |
| 0x56 | Minimum fault |
| 0x57 | CAN Message value defect |
| 0x58 | ungültige Signale |
| 0x59 | Checksummenfehler |
| 0x5A | Alivecounterfehler |
| 0x5B | Botschaft von ARS ausgefallen (STAT_ARS) |
| 0x5C | Botschaft von DSC ausgefallen (STAT_DSC) |
| 0x5D | Botschaft von DSC ausgefallen (TORQUE_DSC) |
| 0x5E | Botschaft von DSC ausgefallen (VELOCITY) |
| 0x5F | Botschaft von EGS ausgefallen (GEARBX_DATA) |
| 0x60 | Botschaft von EGS ausgefallen (TORQUE_GEARBX) |
| 0x61 | Botschaft von CAS ausgefallen (TERMINAL) |
| 0x62 | Botschaft von IHK ausgefallen (HEAT_AC) |
| 0x63 | Botschaft von Kombi ausgefallen (MILEAGE_RANGE) |
| 0x64 | Botschaft von EGS ausgefallen (GEARBX_DATA2) |
| 0x65 | Botschaft von SZL ausgefallen (OP_CRCTLACC) |
| 0x66 | Botschaft von Power-Modul ausgefallen (POWERMANAGMENT_BATTERYVOLTAGE) |
| 0x67 | Botschaft von Power-Modul ausgefallen (PWRMNG_LOADV) |
| 0x68 | Eingriff unplausibel |
| 0x69 | keine Kommunikation ueber BSD-Schnittstelle |
| 0x6A | Kurzschluss nach B- |
| 0x6B | Unterbrechung |
| 0x6C | communication error of CJ940 |
| 0x6D | EEP Fehler beim Lesen oder Schreiben |
| 0x6E | EEP Fehler beim Lesen |
| 0x6F | EEP Fehler beim Schreiben |
| 0x70 | EEP Neutral - Werte benutzt |
| 0x71 | a recovery has occurred |
| 0x72 | internal supply voltage upper limit |
| 0x73 | internal supply voltage lower limit |
| 0x74 | Signal gestoert (Frame oder Stopbiterror) |
| 0x75 | Signal gestoert (parity error) |
| 0x76 | Fehler bei Lesen des Wechselcodes aus EEPROM |
| 0x77 | Wechselcodeablage fehlerhaft |
| 0x78 | Startwert nicht erkennbar beim Ruecksetzen |
| 0x79 | kein Startwert programmiert (DDE jungfraeulich) |
| 0x7A | falscher Startwert (falsche EWS oder gleiche Zufallszahl beim Ruecksetzen) |
| 0x7B | falscher Wechselcode |
| 0x7C | Number of injections limited by charge balance |
| 0x7D | Number of injections limited by quantity balance |
| 0x7E | Number of injections limited by software |
| 0x7F | Checksumme falsch |
| 0x80 | High Side Ansteuerung Kurzschluss nach B+ |
| 0x81 | High Side Ansteuerung Kurzschluss nach B- |
| 0x82 | unbekannter Fehler |
| 0x83 | High Side Ansteuerung Unterbrechung |
| 0x84 | icht verwendet |
| 0x85 | SG CY33X internal reset / clockloss / undervoltage |
| 0x86 | SG CY33X is unlocked / CY33X init error |
| 0x87 | SG CY33X is in Testmode |
| 0x88 | SG CY33X SPI communication error /checksum/readback |
| 0x89 | SG CY33X internal parity error |
| 0x8A | SG CY33X internal program flow error |
| 0x8B | SG CY33X check of inv. YSEL during ON failed |
| 0x8C | SG CY33X ON timeout for at least 1 cylinder |
| 0x8D | Low Side Ansteuerung Kurzschluss nach B+ |
| 0x8E | Low Side Ansteuerung Kurzschluss nach B- |
| 0x8F | Low Side Ansteuerung Kurzschluss nach High Side |
| 0x90 | Low Side Ansteuerung Unterbrechung |
| 0x91 | Relais schaltet zu spaet ab |
| 0x92 | Relais schaltet zu frueh ab |
| 0x93 | not used |
| 0x94 | signal error |
| 0x95 | OvRMon_stOvR does not match complement |
| 0x96 | error in slave task counter detected by master |
| 0x97 | error in task counter |
| 0x98 | BIT2 is set in status byte 2 |
| 0x99 | BIT3 is set in status byte 2 |
| 0x9A | BIT0 is set in status byte 2 |
| 0x9B | BIT4 is set in status byte 2 |
| 0x9C | BIT5 is set in status byte 2 |
| 0x9D | BIT6 is set in status byte 2 |
| 0x9E | BIT1 is set in status byte 2 |
| 0x9F | torque switch off |
| 0xA0 | torque is limited |
| 0xA1 | BIT7 is set in status byte 2 |
| 0xA2 | Mil Lamp activation |
| 0xA3 | SysLamp activation |
| 0xA4 | BIT7 is set in status byte |
| 0xA5 | BIT5 is set in status byte |
| 0xA6 | BIT6 is set in status byte |
| 0xA7 | BIT4 is set in status byte |
| 0xA8 | BIT0 is set in status byte |
| 0xA9 | BIT1 is set in status byte |
| 0xAA | BIT2 is set in status byte |
| 0xAB | ECU-Selection CAN private not plausible |
| 0xAC | ECU-Pin No load |
| 0xAD | ECU-Selection ECU Begin |
| 0xAE | ECU-Selection ECU CHANGE |
| 0xAF | ECU-Selection not plausible |
| 0xB0 | Not plausible fault |
| 0xB1 | ADC signal range check high error of metering unit AD-channel |
| 0xB2 | ADC signal range check low error of metering unit AD-channel |
| 0xB3 | Strommessung defekt (SG intern) |
| 0xB4 | MeUnCD Mengenregelventil wurde durch Diagnose angesteuert |
| 0xB5 | SG watch dog counter limit exceeded |
| 0xB6 | Bus off |
| 0xB7 | Hardwaredefekt im Betrieb |
| 0xB8 | Hardwarefehler in Initialisierung |
| 0xB9 | signal error for CAN |
| 0xBA | Schubueberwachung |
| 0xBB | Drehzahlberechnung im Steuergeraet fehlerhaft |
| 0xBC | Oxidation catalyst non plausible |
| 0xBD | plausibility check for airmass difference |
| 0xBE | negative Regelabweichung / Ladedruck zu hoch |
| 0xBF | positive Regelabweichung / Ladedruck zu niedrig |
| 0xC0 | Raildruckregelventil wurde durch Diagnose angesteuert |
| 0xC1 | Raildruckregelventil defekt |
| 0xC2 | Diffrential pressure above limit |
| 0xC3 | dynamics of diffrential pressure signal is not plausible |
| 0xC4 | pressure  above limit |
| 0xC5 | pressure  below limit |
| 0xC6 | pressure  value non plausible |
| 0xC7 | hose line defective so signal is not plausible |
| 0xC8 | pressure sensor blocked so signal is not plausible |
| 0xC9 | Flow resistance above limit |
| 0xCA | Flow resistance below limit |
| 0xCB | permanent regeneration |
| 0xCC | temperature value non plausible |
| 0xCD | temperature ahead PFlt above limit |
| 0xCE | temperature ahead PFlt below limit |
| 0xCF | runtime of a task is exceeded |
| 0xD0 | System overload |
| 0xD1 | Offset Maximum ueberschritten |
| 0xD2 | Offset Minimum unterschritten |
| 0xD3 | Raildruck bei Motorstart zu niedrig |
| 0xD4 | Raildruckregelung wurde durch Diagnose auf Mengenregelung umgeschaltet MeUn |
| 0xD5 | Raildruckregelung wurde durch Diagnose auf Druckregelung umgeschaltet PCV |
| 0xD6 | positive Regelabweichung/Raildruck zu niedrig |
| 0xD7 | positive Regelabweichung/Raildruck zu niedrig und Stellgroesse zu hoch |
| 0xD8 | Raildruck zu hoch bei Maximalansteuerung Mengenregelventil (RA negativ) |
| 0xD9 | Minimaldruck unterschritten |
| 0xDA | Maximaldruck ueberschritten |
| 0xDB | Stellgroesse von Mengenregelventil im Schub nicht plausibel |
| 0xDC | Raildruckueberhoehung |
| 0xDD | positive Regelabweichung/Raildruck zu niedrig und Ansteuerung DRV zu hoch |
| 0xDE | negative Regelabweichung/Raildruck zu hoch bei Minimalansteuerung Druckregelventil |
| 0xDF | Verhaeltnis von Raildruck zu Ansteuerstrom Druckregelventil unplausibel |
| 0xE0 | panic pressure test limit exceeded |
| 0xE1 | Watch dog Abschaltung |
| 0xE2 | Interne Spannung zu hoch |
| 0xE3 | Interne Spannung zu niedrig |
| 0xE4 | Unterbrechung oder Kurzschluss nach B- |
| 0xE5 | or supply voltage 4 |
| 0xE6 | or supply voltage 5 |
| 0xE7 | or supply voltage 6 |
| 0xE8 | Pulsation |
| 0xE9 | Signal Klemme 50 fehlerhaft |
| 0xEA | Wake Up evaluation circuit defective |
| 0xEB | Wake Up has short circuit to ground |
| 0xEC | Timeout of TPU generated Interrupt |
| 0xED | Deviation between System timer and TPU time |
| 0xEE | Geschwindigkeit zu gross |
| 0xEF | Plausibilitaet mit Einspritzmenge und Motordrehzahl |
| 0xF0 | Signal nicht gueltig |
| 0xF1 | Watchdog |
| 0xF7 | Testbedingungen erfuellt |
| 0xF8 | Testbedingungen noch nicht erfuellt |
| 0xF9 | Fehler bisher nicht aufgetreten |
| 0xFA | Fehler momentan nicht vorhanden |
| 0xFB | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0xFC | Fehler momentan vorhanden |
| 0xFD | Fehler wuerde kein Aufleuchten einer Warnlampe verursachen |
| 0xFE | Fehler wuerde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |
| 0xXY | kein passendes Fehlersymptom |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 531 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x4820 | 0x2D | 0x2C | 0xC2 | ANALOG0 |
| 0x4821 | 0x2D | 0x2C | 0xC2 | ANALOG1 |
| 0x4822 | 0x2D | 0x2C | 0xC2 | ANALOG2 |
| 0x4823 | 0x2D | 0x2C | 0xC2 | ANALOG3 |
| 0x40B0 | 0x2D | 0x2C | 0xC2 | ANALOG4 |
| 0x40B1 | 0x2D | 0x2C | 0xC2 | ANALOG5 |
| 0x40B2 | 0x2D | 0x2C | 0xC2 | ANALOG6 |
| 0x40B3 | 0x2D | 0x2C | 0xC2 | ANALOG7 |
| 0x40C0 | 0x2D | 0x2C | 0xC2 | ANALOG8 |
| 0x40C1 | 0x2D | 0x2C | 0xC2 | ANALOG9 |
| 0x40D0 | 0x2D | 0x2C | 0xC2 | ANALOG10 |
| 0x40D1 | 0x2D | 0x2C | 0xC2 | ANALOG11 |
| 0x4112 | 0x2D | 0x2C | 0xC2 | ANALOG12 |
| 0x4113 | 0x2D | 0x2C | 0xC2 | ANALOG13 |
| 0x4780 | 0x2D | 0x2C | 0xC2 | ANALOG14 |
| 0x4781 | 0x2D | 0x2C | 0xC2 | ANALOG15 |
| 0x4782 | 0x2D | 0x2C | 0xC2 | ANALOG16 |
| 0x4783 | 0x2D | 0x2C | 0xC2 | ANALOG17 |
| 0x4170 | 0x2D | 0x2C | 0xC2 | ANALOG18 |
| 0x4171 | 0x2D | 0x2C | 0xC2 | ANALOG19 |
| 0x4172 | 0x2D | 0x2C | 0xC2 | ANALOG20 |
| 0x4173 | 0x2D | 0x2C | 0xC2 | ANALOG21 |
| 0x4370 | 0x2D | 0x2C | 0xC2 | ANALOG22 |
| 0x4830 | 0x2D | 0x2C | 0xC2 | ANALOG23 |
| 0x4831 | 0x2D | 0x2C | 0xC2 | ANALOG24 |
| 0x3E95 | 0x2D | 0x2C | 0xC2 | ANALOG25 |
| 0x3E96 | 0x2D | 0x2C | 0xC2 | ANALOG26 |
| 0x3FE0 | 0x2D | 0x2C | 0xC2 | ANALOG27 |
| 0x3FE1 | 0x2D | 0x2C | 0xC2 | ANALOG28 |
| 0x3EB5 | 0x2D | 0x2C | 0xC2 | ANALOG29 |
| 0x3EB6 | 0x2D | 0x2C | 0xC2 | ANALOG30 |
| 0x3FF0 | 0x2D | 0x2C | 0xC2 | ANALOG31 |
| 0x3FF1 | 0x2D | 0x2C | 0xC2 | ANALOG32 |
| 0x4CA5 | 0x2D | 0x2C | 0xC2 | ANALOG33 |
| 0x4CA6 | 0x2D | 0x2C | 0xC2 | ANALOG34 |
| 0x4BA0 | 0x2D | 0x2C | 0xC2 | ANALOG35 |
| 0x4BA1 | 0x2D | 0x2C | 0xC2 | ANALOG36 |
| 0x3EA5 | 0x2D | 0x2C | 0xC2 | ANALOG37 |
| 0x3EA6 | 0x2D | 0x2C | 0xC2 | ANALOG38 |
| 0x4BB0 | 0x2D | 0x2C | 0xC2 | ANALOG39 |
| 0x4BB1 | 0x2D | 0x2C | 0xC2 | ANALOG40 |
| 0x4C75 | 0x2D | 0x2C | 0xC2 | ANALOG41 |
| 0x4C76 | 0x2D | 0x2C | 0xC2 | ANALOG42 |
| 0x4BB5 | 0x2D | 0x2C | 0xC2 | ANALOG43 |
| 0x4BB6 | 0x2D | 0x2C | 0xC2 | ANALOG44 |
| 0x3ED5 | 0x2D | 0x2C | 0xC2 | ANALOG45 |
| 0x3ED6 | 0x2D | 0x2C | 0xC2 | ANALOG46 |
| 0x4BC0 | 0x2D | 0x2C | 0xC2 | ANALOG47 |
| 0x4BC1 | 0x2D | 0x2C | 0xC2 | ANALOG48 |
| 0x4BC2 | 0x2D | 0x2C | 0xC2 | ANALOG49 |
| 0x3EE5 | 0x2D | 0x2C | 0xC2 | ANALOG50 |
| 0x3EE6 | 0x2D | 0x2C | 0xC2 | ANALOG51 |
| 0x3EE7 | 0x2D | 0x2C | 0xC2 | ANALOG52 |
| 0x4BC5 | 0x2D | 0x2C | 0xC2 | ANALOG53 |
| 0x4BC6 | 0x2D | 0x2C | 0xC2 | ANALOG54 |
| 0x4BC7 | 0x2D | 0x2C | 0xC2 | ANALOG55 |
| 0x3EF5 | 0x2D | 0x2C | 0xC2 | ANALOG56 |
| 0x3EF6 | 0x2D | 0x2C | 0xC2 | ANALOG57 |
| 0x3EF7 | 0x2D | 0x2C | 0xC2 | ANALOG58 |
| 0x43F0 | 0x2D | 0x2C | 0xC2 | ANALOG59 |
| 0x43F1 | 0x2D | 0x2C | 0xC2 | ANALOG60 |
| 0x43F2 | 0x2D | 0x2C | 0xC2 | ANALOG61 |
| 0x43F3 | 0x2D | 0x2C | 0xC2 | ANALOG62 |
| 0x4AB0 | 0x2D | 0x2C | 0xC2 | ANALOG63 |
| 0x4AB2 | 0x2D | 0x2C | 0xC2 | ANALOG64 |
| 0x4AC0 | 0x2D | 0x2C | 0xC2 | ANALOG65 |
| 0x4AC2 | 0x2D | 0x2C | 0xC2 | ANALOG66 |
| 0x4AD0 | 0x2D | 0x2C | 0xC2 | ANALOG67 |
| 0x4AD2 | 0x2D | 0x2C | 0xC2 | ANALOG68 |
| 0x3F10 | 0x2D | 0x2C | 0xC2 | ANALOG69 |
| 0x3F11 | 0x2D | 0x2C | 0xC2 | ANALOG70 |
| 0x3F13 | 0x2D | 0x2C | 0xC2 | ANALOG71 |
| 0x3F20 | 0x2D | 0x2C | 0xC2 | ANALOG72 |
| 0x3F21 | 0x2D | 0x2C | 0xC2 | ANALOG73 |
| 0x3F23 | 0x2D | 0x2C | 0xC2 | ANALOG74 |
| 0x4060 | 0x2D | 0x2C | 0xC2 | ANALOG75 |
| 0x4061 | 0x2D | 0x2C | 0xC2 | ANALOG76 |
| 0x4063 | 0x2D | 0x2C | 0xC2 | ANALOG77 |
| 0x4BD2 | 0x2D | 0x2C | 0xC2 | ANALOG78 |
| 0x4093 | 0x2D | 0x2C | 0xC2 | ANALOG79 |
| 0x4C71 | 0x2D | 0x2C | 0xC2 | ANALOG80 |
| 0x4501 | 0x2D | 0x2C | 0xC2 | ANALOG81 |
| 0x4841 | 0x2D | 0x2C | 0xC2 | ANALOG82 |
| 0x4507 | 0x2D | 0x2C | 0xC2 | ANALOG83 |
| 0x4850 | 0x2D | 0x2C | 0xC2 | ANALOG84 |
| 0x40E0 | 0x2D | 0x2C | 0xC2 | ANALOG85 |
| 0x3F57 | 0x2D | 0x2C | 0xC2 | ANALOG86 |
| 0x3F67 | 0x2D | 0x2C | 0xC2 | ANALOG87 |
| 0x3F77 | 0x2D | 0x2C | 0xC2 | ANALOG88 |
| 0x3F87 | 0x2D | 0x2C | 0xC2 | ANALOG89 |
| 0x3F97 | 0x2D | 0x2C | 0xC2 | ANALOG90 |
| 0x3FA7 | 0x2D | 0x2C | 0xC2 | ANALOG91 |
| 0x4180 | 0x2D | 0x2C | 0xC2 | ANALOG92 |
| 0x4550 | 0x2D | 0x2C | 0xC2 | ANALOG93 |
| 0x4191 | 0x2D | 0x2C | 0xC2 | ANALOG94 |
| 0x4D81 | 0x2D | 0x2C | 0xC2 | ANALOG95 |
| 0x41A2 | 0x2D | 0x2C | 0xC2 | ANALOG96 |
| 0x41A3 | 0x2D | 0x2C | 0xC2 | ANALOG97 |
| 0x4A22 | 0x2D | 0x2C | 0xC2 | ANALOG98 |
| 0x4A23 | 0x2D | 0x2C | 0xC2 | ANALOG99 |
| 0x3F00 | 0x2D | 0x2C | 0xC2 | ANALOG100 |
| 0x3F01 | 0x2D | 0x2C | 0xC2 | ANALOG101 |
| 0x3F02 | 0x2D | 0x2C | 0xC2 | ANALOG102 |
| 0x3F03 | 0x2D | 0x2C | 0xC2 | ANALOG103 |
| 0x4660 | 0x2D | 0x2C | 0xC2 | ANALOG104 |
| 0x4661 | 0x2D | 0x2C | 0xC2 | ANALOG105 |
| 0x4082 | 0x2D | 0x2C | 0xC2 | ANALOG106 |
| 0x4083 | 0x2D | 0x2C | 0xC2 | ANALOG107 |
| 0x4A10 | 0x2D | 0x2C | 0xC2 | ANALOG108 |
| 0x4A13 | 0x2D | 0x2C | 0xC2 | ANALOG109 |
| 0x3EE0 | 0x2D | 0x2C | 0xC2 | ANALOG110 |
| 0x3EE1 | 0x2D | 0x2C | 0xC2 | ANALOG111 |
| 0x3EE2 | 0x2D | 0x2C | 0xC2 | ANALOG112 |
| 0x3EE3 | 0x2D | 0x2C | 0xC2 | ANALOG113 |
| 0x3EF3 | 0x2D | 0x2C | 0xC2 | ANALOG114 |
| 0x4880 | 0x2D | 0x2C | 0xC2 | ANALOG115 |
| 0x4890 | 0x2D | 0x2C | 0xC2 | ANALOG116 |
| 0x4930 | 0x2D | 0x2C | 0xC2 | ANALOG117 |
| 0x4940 | 0x2D | 0x2C | 0xC2 | ANALOG118 |
| 0x4950 | 0x2D | 0x2C | 0xC2 | ANALOG119 |
| 0x4960 | 0x2D | 0x2C | 0xC2 | ANALOG120 |
| 0x4870 | 0x2D | 0x2C | 0xC2 | ANALOG121 |
| 0x47A0 | 0x2D | 0x2C | 0xC2 | ANALOG122 |
| 0x47B0 | 0x2D | 0x2C | 0xC2 | ANALOG123 |
| 0x47C0 | 0x2D | 0x2C | 0xC2 | ANALOG124 |
| 0x47D0 | 0x2D | 0x2C | 0xC2 | ANALOG125 |
| 0x47E0 | 0x2D | 0x2C | 0xC2 | ANALOG126 |
| 0x47F0 | 0x2D | 0x2C | 0xC2 | ANALOG127 |
| 0x4C80 | 0x2D | 0x2C | 0xC2 | ANALOG128 |
| 0x4C90 | 0x2D | 0x2C | 0xC2 | ANALOG129 |
| 0x4D92 | 0x2D | 0x2C | 0xC2 | ANALOG130 |
| 0x4D93 | 0x2D | 0x2C | 0xC2 | ANALOG131 |
| 0x4900 | 0x2D | 0x2C | 0xC2 | ANALOG132 |
| 0x4072 | 0x2D | 0x2C | 0xC2 | ANALOG133 |
| 0x4073 | 0x2D | 0x2C | 0xC2 | ANALOG134 |
| 0x4A30 | 0x2D | 0x2C | 0xC2 | ANALOG135 |
| 0x4A31 | 0x2D | 0x2C | 0xC2 | ANALOG136 |
| 0x4A32 | 0x2D | 0x2C | 0xC2 | ANALOG137 |
| 0x4A33 | 0x2D | 0x2C | 0xC2 | ANALOG138 |
| 0x3F80 | 0x2D | 0x2C | 0xC2 | ANALOG139 |
| 0x3F81 | 0x2D | 0x2C | 0xC2 | ANALOG140 |
| 0x3F82 | 0x2D | 0x2C | 0xC2 | ANALOG141 |
| 0x41C0 | 0x2D | 0x2C | 0xC2 | ANALOG142 |
| 0x41C1 | 0x2D | 0x2C | 0xC2 | ANALOG143 |
| 0x41C2 | 0x2D | 0x2C | 0xC2 | ANALOG144 |
| 0x41C3 | 0x2D | 0x2C | 0xC2 | ANALOG145 |
| 0x4AE0 | 0x2D | 0x2C | 0xC2 | ANALOG146 |
| 0x4AE1 | 0x2D | 0x2C | 0xC2 | ANALOG147 |
| 0x4AE2 | 0x2D | 0x2C | 0xC2 | ANALOG148 |
| 0x4AE3 | 0x2D | 0x2C | 0xC2 | ANALOG149 |
| 0x4AF0 | 0x2D | 0x2C | 0xC2 | ANALOG150 |
| 0x4AF1 | 0x2D | 0x2C | 0xC2 | ANALOG151 |
| 0x4B00 | 0x2D | 0x2C | 0xC2 | ANALOG152 |
| 0x41B0 | 0x2D | 0x2C | 0xC2 | ANALOG153 |
| 0x4DB0 | 0x2D | 0x2C | 0xC2 | ANALOG154 |
| 0x41D1 | 0x2D | 0x2C | 0xC2 | ANALOG155 |
| 0x4DC1 | 0x2D | 0x2C | 0xC2 | ANALOG156 |
| 0x41E2 | 0x2D | 0x2C | 0xC2 | ANALOG157 |
| 0x41E3 | 0x2D | 0x2C | 0xC2 | ANALOG158 |
| 0x4DD2 | 0x2D | 0x2C | 0xC2 | ANALOG159 |
| 0x4DD3 | 0x2D | 0x2C | 0xC2 | ANALOG160 |
| 0x3EC0 | 0x2D | 0x2C | 0xC2 | ANALOG161 |
| 0x3EC1 | 0x2D | 0x2C | 0xC2 | ANALOG162 |
| 0x3ED0 | 0x2D | 0x2C | 0xC2 | ANALOG163 |
| 0x3ED1 | 0x2D | 0x2C | 0xC2 | ANALOG164 |
| 0x3E90 | 0x2D | 0x2C | 0xC2 | ANALOG165 |
| 0x3E91 | 0x2D | 0x2C | 0xC2 | ANALOG166 |
| 0x3EA0 | 0x2D | 0x2C | 0xC2 | ANALOG167 |
| 0x3EA1 | 0x2D | 0x2C | 0xC2 | ANALOG168 |
| 0x4BD5 | 0x2D | 0x2C | 0xC2 | ANALOG169 |
| 0x4BD6 | 0x2D | 0x2C | 0xC2 | ANALOG170 |
| 0x4BD7 | 0x2D | 0x2C | 0xC2 | ANALOG171 |
| 0x4BD8 | 0x2D | 0x2C | 0xC2 | ANALOG172 |
| 0x4B10 | 0x2D | 0x2C | 0xC2 | ANALOG173 |
| 0x4B11 | 0x2D | 0x2C | 0xC2 | ANALOG174 |
| 0x4A70 | 0x2D | 0x2C | 0xC2 | ANALOG175 |
| 0x4000 | 0x2D | 0x2C | 0xC2 | ANALOG176 |
| 0x4001 | 0x2D | 0x2C | 0xC2 | ANALOG177 |
| 0x41F0 | 0x2D | 0x2C | 0xC2 | ANALOG178 |
| 0x41F1 | 0x2D | 0x2C | 0xC2 | ANALOG179 |
| 0x41F2 | 0x2D | 0x2C | 0xC2 | ANALOG180 |
| 0x41F3 | 0x2D | 0x2C | 0xC2 | ANALOG181 |
| 0x4B20 | 0x2D | 0x2C | 0xC2 | ANALOG182 |
| 0x4B22 | 0x2D | 0x2C | 0xC2 | ANALOG183 |
| 0x4B30 | 0x2D | 0x2C | 0xC2 | ANALOG184 |
| 0x4B32 | 0x2D | 0x2C | 0xC2 | ANALOG185 |
| 0x4B40 | 0x2D | 0x2C | 0xC2 | ANALOG186 |
| 0x4B42 | 0x2D | 0x2C | 0xC2 | ANALOG187 |
| 0x4A80 | 0x2D | 0x2C | 0xC2 | ANALOG188 |
| 0x4040 | 0x2D | 0x2C | 0xC2 | ANALOG189 |
| 0x4041 | 0x2D | 0x2C | 0xC2 | ANALOG190 |
| 0x4042 | 0x2D | 0x2C | 0xC2 | ANALOG191 |
| 0x4BE2 | 0x2D | 0x2C | 0xC2 | ANALOG192 |
| 0x4BE7 | 0x2D | 0x2C | 0xC2 | ANALOG193 |
| 0x4BF2 | 0x2D | 0x2C | 0xC2 | ANALOG194 |
| 0x4BF7 | 0x2D | 0x2C | 0xC2 | ANALOG195 |
| 0x4C00 | 0x2D | 0x2C | 0xC2 | ANALOG196 |
| 0x4C01 | 0x2D | 0x2C | 0xC2 | ANALOG197 |
| 0x4C02 | 0x2D | 0x2C | 0xC2 | ANALOG198 |
| 0x4CA2 | 0x2D | 0x2C | 0xC2 | ANALOG199 |
| 0x4CB2 | 0x2D | 0x2C | 0xC2 | ANALOG200 |
| 0x4C06 | 0x2D | 0x2C | 0xC2 | ANALOG201 |
| 0x4C07 | 0x2D | 0x2C | 0xC2 | ANALOG202 |
| 0x4C12 | 0x2D | 0x2C | 0xC2 | ANALOG203 |
| 0x4C15 | 0x2D | 0x2C | 0xC2 | ANALOG204 |
| 0x4C16 | 0x2D | 0x2C | 0xC2 | ANALOG205 |
| 0x4C17 | 0x2D | 0x2C | 0xC2 | ANALOG206 |
| 0x4C20 | 0x2D | 0x2C | 0xC2 | ANALOG207 |
| 0x4C21 | 0x2D | 0x2C | 0xC2 | ANALOG208 |
| 0x4C22 | 0x2D | 0x2C | 0xC2 | ANALOG209 |
| 0x4DF0 | 0x2D | 0x2C | 0xC2 | ANALOG210 |
| 0x4DF1 | 0x2D | 0x2C | 0xC2 | ANALOG211 |
| 0x4DF2 | 0x2D | 0x2C | 0xC2 | ANALOG212 |
| 0x4C27 | 0x2D | 0x2C | 0xC2 | ANALOG213 |
| 0x4C30 | 0x2D | 0x2C | 0xC2 | ANALOG214 |
| 0x4C31 | 0x2D | 0x2C | 0xC2 | ANALOG215 |
| 0x4C32 | 0x2D | 0x2C | 0xC2 | ANALOG216 |
| 0x4C33 | 0x2D | 0x2C | 0xC2 | ANALOG217 |
| 0x4C35 | 0x2D | 0x2C | 0xC2 | ANALOG218 |
| 0x4C36 | 0x2D | 0x2C | 0xC2 | ANALOG219 |
| 0x4C37 | 0x2D | 0x2C | 0xC2 | ANALOG220 |
| 0x4C38 | 0x2D | 0x2C | 0xC2 | ANALOG221 |
| 0x4970 | 0x2D | 0x2C | 0xC2 | ANALOG222 |
| 0x4971 | 0x2D | 0x2C | 0xC2 | ANALOG223 |
| 0x4972 | 0x2D | 0x2C | 0xC2 | ANALOG224 |
| 0x4973 | 0x2D | 0x2C | 0xC2 | ANALOG225 |
| 0x4CC0 | 0x2D | 0x2C | 0xC2 | ANALOG226 |
| 0x4920 | 0x2D | 0x2C | 0xC2 | ANALOG227 |
| 0x4203 | 0x2D | 0x2C | 0xC2 | ANALOG228 |
| 0x4211 | 0x2D | 0x2C | 0xC2 | ANALOG229 |
| 0x4212 | 0x2D | 0x2C | 0xC2 | ANALOG230 |
| 0x4213 | 0x2D | 0x2C | 0xC2 | ANALOG231 |
| 0x4221 | 0x2D | 0x2C | 0xC2 | ANALOG232 |
| 0x4222 | 0x2D | 0x2C | 0xC2 | ANALOG233 |
| 0x4223 | 0x2D | 0x2C | 0xC2 | ANALOG234 |
| 0x4231 | 0x2D | 0x2C | 0xC2 | ANALOG235 |
| 0x4232 | 0x2D | 0x2C | 0xC2 | ANALOG236 |
| 0x4233 | 0x2D | 0x2C | 0xC2 | ANALOG237 |
| 0x4241 | 0x2D | 0x2C | 0xC2 | ANALOG238 |
| 0x4242 | 0x2D | 0x2C | 0xC2 | ANALOG239 |
| 0x4243 | 0x2D | 0x2C | 0xC2 | ANALOG240 |
| 0x4251 | 0x2D | 0x2C | 0xC2 | ANALOG241 |
| 0x4252 | 0x2D | 0x2C | 0xC2 | ANALOG242 |
| 0x4253 | 0x2D | 0x2C | 0xC2 | ANALOG243 |
| 0x4261 | 0x2D | 0x2C | 0xC2 | ANALOG244 |
| 0x4262 | 0x2D | 0x2C | 0xC2 | ANALOG245 |
| 0x4263 | 0x2D | 0x2C | 0xC2 | ANALOG246 |
| 0x4271 | 0x2D | 0x2C | 0xC2 | ANALOG247 |
| 0x4272 | 0x2D | 0x2C | 0xC2 | ANALOG248 |
| 0x4273 | 0x2D | 0x2C | 0xC2 | ANALOG249 |
| 0x4281 | 0x2D | 0x2C | 0xC2 | ANALOG250 |
| 0x4282 | 0x2D | 0x2C | 0xC2 | ANALOG251 |
| 0x4283 | 0x2D | 0x2C | 0xC2 | ANALOG252 |
| 0x42A0 | 0x2D | 0x2C | 0xC2 | ANALOG253 |
| 0x42A1 | 0x2D | 0x2C | 0xC2 | ANALOG254 |
| 0x42A2 | 0x2D | 0x2C | 0xC2 | ANALOG255 |
| 0x42A3 | 0x2D | 0x2C | 0xC2 | ANALOG256 |
| 0x42B1 | 0x2D | 0x2C | 0xC2 | ANALOG257 |
| 0x42B2 | 0x2D | 0x2C | 0xC2 | ANALOG258 |
| 0x46C0 | 0x2D | 0x2C | 0xC2 | ANALOG259 |
| 0x46D0 | 0x2D | 0x2C | 0xC2 | ANALOG260 |
| 0x46D1 | 0x2D | 0x2C | 0xC2 | ANALOG261 |
| 0x46D2 | 0x2D | 0x2C | 0xC2 | ANALOG262 |
| 0x46D3 | 0x2D | 0x2C | 0xC2 | ANALOG263 |
| 0x4293 | 0x2D | 0x2C | 0xC2 | ANALOG264 |
| 0x4403 | 0x2D | 0x2C | 0xC2 | ANALOG265 |
| 0x4473 | 0x2D | 0x2C | 0xC2 | ANALOG266 |
| 0x4480 | 0x2D | 0x2C | 0xC2 | ANALOG267 |
| 0x4491 | 0x2D | 0x2C | 0xC2 | ANALOG268 |
| 0x3F70 | 0x2D | 0x2C | 0xC2 | ANALOG269 |
| 0x3F71 | 0x2D | 0x2C | 0xC2 | ANALOG270 |
| 0x4390 | 0x2D | 0x2C | 0xC2 | ANALOG271 |
| 0x4391 | 0x2D | 0x2C | 0xC2 | ANALOG272 |
| 0x4A41 | 0x2D | 0x2C | 0xC2 | ANALOG273 |
| 0x4A42 | 0x2D | 0x2C | 0xC2 | ANALOG274 |
| 0x4A43 | 0x2D | 0x2C | 0xC2 | ANALOG275 |
| 0x4A50 | 0x2D | 0x2C | 0xC2 | ANALOG276 |
| 0x4A51 | 0x2D | 0x2C | 0xC2 | ANALOG277 |
| 0x4A60 | 0x2D | 0x2C | 0xC2 | ANALOG278 |
| 0x4A61 | 0x2D | 0x2C | 0xC2 | ANALOG279 |
| 0x4A62 | 0x2D | 0x2C | 0xC2 | ANALOG280 |
| 0x4A63 | 0x2D | 0x2C | 0xC2 | ANALOG281 |
| 0x44C0 | 0x2D | 0x2C | 0xC2 | ANALOG282 |
| 0x44C1 | 0x2D | 0x2C | 0xC2 | ANALOG283 |
| 0x44C2 | 0x2D | 0x2C | 0xC2 | ANALOG284 |
| 0x4B50 | 0x2D | 0x2C | 0xC2 | ANALOG285 |
| 0x4B60 | 0x2D | 0x2C | 0xC2 | ANALOG286 |
| 0x44A0 | 0x2D | 0x2C | 0xC2 | ANALOG287 |
| 0x44A1 | 0x2D | 0x2C | 0xC2 | ANALOG288 |
| 0x44A2 | 0x2D | 0x2C | 0xC2 | ANALOG289 |
| 0x44A3 | 0x2D | 0x2C | 0xC2 | ANALOG290 |
| 0x44AA | 0x2D | 0x2C | 0xC2 | ANALOG291 |
| 0x44AB | 0x2D | 0x2C | 0xC2 | ANALOG292 |
| 0x44AC | 0x2D | 0x2C | 0xC2 | ANALOG293 |
| 0x44AD | 0x2D | 0x2C | 0xC2 | ANALOG294 |
| 0x44B0 | 0x2D | 0x2C | 0xC2 | ANALOG295 |
| 0x44B1 | 0x2D | 0x2C | 0xC2 | ANALOG296 |
| 0x44B2 | 0x2D | 0x2C | 0xC2 | ANALOG297 |
| 0x44B3 | 0x2D | 0x2C | 0xC2 | ANALOG298 |
| 0x44BA | 0x2D | 0x2C | 0xC2 | ANALOG299 |
| 0x44BB | 0x2D | 0x2C | 0xC2 | ANALOG300 |
| 0x44BC | 0x2D | 0x2C | 0xC2 | ANALOG301 |
| 0x44BD | 0x2D | 0x2C | 0xC2 | ANALOG302 |
| 0x46A0 | 0x2D | 0x2C | 0xC2 | ANALOG303 |
| 0x46A1 | 0x2D | 0x2C | 0xC2 | ANALOG304 |
| 0x46A2 | 0x2D | 0x2C | 0xC2 | ANALOG305 |
| 0x46A3 | 0x2D | 0x2C | 0xC2 | ANALOG306 |
| 0x46B0 | 0x2D | 0x2C | 0xC2 | ANALOG307 |
| 0x46B1 | 0x2D | 0x2C | 0xC2 | ANALOG308 |
| 0x46B2 | 0x2D | 0x2C | 0xC2 | ANALOG309 |
| 0x46B3 | 0x2D | 0x2C | 0xC2 | ANALOG310 |
| 0x4410 | 0x2D | 0x2C | 0xC2 | ANALOG311 |
| 0x4411 | 0x2D | 0x2C | 0xC2 | ANALOG312 |
| 0x4412 | 0x2D | 0x2C | 0xC2 | ANALOG313 |
| 0x4413 | 0x2D | 0x2C | 0xC2 | ANALOG314 |
| 0x441A | 0x2D | 0x2C | 0xC2 | ANALOG315 |
| 0x441B | 0x2D | 0x2C | 0xC2 | ANALOG316 |
| 0x441C | 0x2D | 0x2C | 0xC2 | ANALOG317 |
| 0x441D | 0x2D | 0x2C | 0xC2 | ANALOG318 |
| 0x4420 | 0x2D | 0x2C | 0xC2 | ANALOG319 |
| 0x4421 | 0x2D | 0x2C | 0xC2 | ANALOG320 |
| 0x4422 | 0x2D | 0x2C | 0xC2 | ANALOG321 |
| 0x4423 | 0x2D | 0x2C | 0xC2 | ANALOG322 |
| 0x442A | 0x2D | 0x2C | 0xC2 | ANALOG323 |
| 0x442B | 0x2D | 0x2C | 0xC2 | ANALOG324 |
| 0x442C | 0x2D | 0x2C | 0xC2 | ANALOG325 |
| 0x442D | 0x2D | 0x2C | 0xC2 | ANALOG326 |
| 0x4430 | 0x2D | 0x2C | 0xC2 | ANALOG327 |
| 0x4431 | 0x2D | 0x2C | 0xC2 | ANALOG328 |
| 0x4432 | 0x2D | 0x2C | 0xC2 | ANALOG329 |
| 0x4433 | 0x2D | 0x2C | 0xC2 | ANALOG330 |
| 0x443A | 0x2D | 0x2C | 0xC2 | ANALOG331 |
| 0x443B | 0x2D | 0x2C | 0xC2 | ANALOG332 |
| 0x443C | 0x2D | 0x2C | 0xC2 | ANALOG333 |
| 0x443D | 0x2D | 0x2C | 0xC2 | ANALOG334 |
| 0x4440 | 0x2D | 0x2C | 0xC2 | ANALOG335 |
| 0x4441 | 0x2D | 0x2C | 0xC2 | ANALOG336 |
| 0x4442 | 0x2D | 0x2C | 0xC2 | ANALOG337 |
| 0x4443 | 0x2D | 0x2C | 0xC2 | ANALOG338 |
| 0x444A | 0x2D | 0x2C | 0xC2 | ANALOG339 |
| 0x444B | 0x2D | 0x2C | 0xC2 | ANALOG340 |
| 0x444C | 0x2D | 0x2C | 0xC2 | ANALOG341 |
| 0x444D | 0x2D | 0x2C | 0xC2 | ANALOG342 |
| 0x4450 | 0x2D | 0x2C | 0xC2 | ANALOG343 |
| 0x4451 | 0x2D | 0x2C | 0xC2 | ANALOG344 |
| 0x4452 | 0x2D | 0x2C | 0xC2 | ANALOG345 |
| 0x4453 | 0x2D | 0x2C | 0xC2 | ANALOG346 |
| 0x445A | 0x2D | 0x2C | 0xC2 | ANALOG347 |
| 0x445B | 0x2D | 0x2C | 0xC2 | ANALOG348 |
| 0x445C | 0x2D | 0x2C | 0xC2 | ANALOG349 |
| 0x445D | 0x2D | 0x2C | 0xC2 | ANALOG350 |
| 0x4460 | 0x2D | 0x2C | 0xC2 | ANALOG351 |
| 0x4461 | 0x2D | 0x2C | 0xC2 | ANALOG352 |
| 0x4462 | 0x2D | 0x2C | 0xC2 | ANALOG353 |
| 0x4463 | 0x2D | 0x2C | 0xC2 | ANALOG354 |
| 0x446A | 0x2D | 0x2C | 0xC2 | ANALOG355 |
| 0x446B | 0x2D | 0x2C | 0xC2 | ANALOG356 |
| 0x446C | 0x2D | 0x2C | 0xC2 | ANALOG357 |
| 0x446D | 0x2D | 0x2C | 0xC2 | ANALOG358 |
| 0x42D0 | 0x2D | 0x2C | 0xC2 | ANALOG359 |
| 0x42D1 | 0x2D | 0x2C | 0xC2 | ANALOG360 |
| 0x42D2 | 0x2D | 0x2C | 0xC2 | ANALOG361 |
| 0x42D3 | 0x2D | 0x2C | 0xC2 | ANALOG362 |
| 0x4120 | 0x2D | 0x2C | 0xC2 | ANALOG363 |
| 0x4121 | 0x2D | 0x2C | 0xC2 | ANALOG364 |
| 0x4DE0 | 0x2D | 0x2C | 0xC2 | ANALOG365 |
| 0x4DE1 | 0x2D | 0x2C | 0xC2 | ANALOG366 |
| 0x4DE2 | 0x2D | 0x2C | 0xC2 | ANALOG367 |
| 0x4DE3 | 0x2D | 0x2C | 0xC2 | ANALOG368 |
| 0x3FB5 | 0x2D | 0x2C | 0xC2 | ANALOG369 |
| 0x3FB6 | 0x2D | 0x2C | 0xC2 | ANALOG370 |
| 0x3FB7 | 0x2D | 0x2C | 0xC2 | ANALOG371 |
| 0x3FC5 | 0x2D | 0x2C | 0xC2 | ANALOG372 |
| 0x3FE5 | 0x2D | 0x2C | 0xC2 | ANALOG373 |
| 0x3FF5 | 0x2D | 0x2C | 0xC2 | ANALOG374 |
| 0x4005 | 0x2D | 0x2C | 0xC2 | ANALOG375 |
| 0x4015 | 0x2D | 0x2C | 0xC2 | ANALOG376 |
| 0x4025 | 0x2D | 0x2C | 0xC2 | ANALOG377 |
| 0x4035 | 0x2D | 0x2C | 0xC2 | ANALOG378 |
| 0x4045 | 0x2D | 0x2C | 0xC2 | ANALOG379 |
| 0x4055 | 0x2D | 0x2C | 0xC2 | ANALOG380 |
| 0x4065 | 0x2D | 0x2C | 0xC2 | ANALOG381 |
| 0x4075 | 0x2D | 0x2C | 0xC2 | ANALOG382 |
| 0x4085 | 0x2D | 0x2C | 0xC2 | ANALOG383 |
| 0x4095 | 0x2D | 0x2C | 0xC2 | ANALOG384 |
| 0x40A5 | 0x2D | 0x2C | 0xC2 | ANALOG385 |
| 0x40B5 | 0x2D | 0x2C | 0xC2 | ANALOG386 |
| 0x40C5 | 0x2D | 0x2C | 0xC2 | ANALOG387 |
| 0x40D5 | 0x2D | 0x2C | 0xC2 | ANALOG388 |
| 0x40E5 | 0x2D | 0x2C | 0xC2 | ANALOG389 |
| 0x40F5 | 0x2D | 0x2C | 0xC2 | ANALOG390 |
| 0x45E3 | 0x2D | 0x2C | 0xC2 | ANALOG391 |
| 0x3EC7 | 0x2D | 0x2C | 0xC2 | ANALOG392 |
| 0x45F2 | 0x2D | 0x2C | 0xC2 | ANALOG393 |
| 0x45F3 | 0x2D | 0x2C | 0xC2 | ANALOG394 |
| 0x4792 | 0x2D | 0x2C | 0xC2 | ANALOG395 |
| 0x4793 | 0x2D | 0x2C | 0xC2 | ANALOG396 |
| 0x4107 | 0x2D | 0x2C | 0xC2 | ANALOG397 |
| 0x4108 | 0x2D | 0x2C | 0xC2 | ANALOG398 |
| 0x4118 | 0x2D | 0x2C | 0xC2 | ANALOG399 |
| 0x4302 | 0x2D | 0x2C | 0xC2 | ANALOG400 |
| 0x4303 | 0x2D | 0x2C | 0xC2 | ANALOG401 |
| 0x4310 | 0x2D | 0x2C | 0xC2 | ANALOG402 |
| 0x4321 | 0x2D | 0x2C | 0xC2 | ANALOG403 |
| 0x4730 | 0x2D | 0x2C | 0xC2 | ANALOG404 |
| 0x4731 | 0x2D | 0x2C | 0xC2 | ANALOG405 |
| 0x4732 | 0x2D | 0x2C | 0xC2 | ANALOG406 |
| 0x4397 | 0x2D | 0x2C | 0xC2 | ANALOG407 |
| 0x4703 | 0x2D | 0x2C | 0xC2 | ANALOG408 |
| 0xCD87 | 0x2D | 0x2C | 0xC2 | ANALOG409 |
| 0x48F2 | 0x2D | 0x2C | 0xC2 | ANALOG410 |
| 0x48F3 | 0x2D | 0x2C | 0xC2 | ANALOG411 |
| 0x4910 | 0x2D | 0x2C | 0xC2 | ANALOG412 |
| 0x4912 | 0x2D | 0x2C | 0xC2 | ANALOG413 |
| 0x4913 | 0x2D | 0x2C | 0xC2 | ANALOG414 |
| 0x42C0 | 0x2D | 0x2C | 0xC2 | ANALOG415 |
| 0x42C1 | 0x2D | 0x2C | 0xC2 | ANALOG416 |
| 0x42C2 | 0x2D | 0x2C | 0xC2 | ANALOG417 |
| 0x42C3 | 0x2D | 0x2C | 0xC2 | ANALOG418 |
| 0x3F90 | 0x2D | 0x2C | 0xC2 | ANALOG419 |
| 0x3F91 | 0x2D | 0x2C | 0xC2 | ANALOG420 |
| 0x3FA0 | 0x2D | 0x2C | 0xC2 | ANALOG421 |
| 0x3FA1 | 0x2D | 0x2C | 0xC2 | ANALOG422 |
| 0x3FA2 | 0x2D | 0x2C | 0xC2 | ANALOG423 |
| 0x3FA3 | 0x2D | 0x2C | 0xC2 | ANALOG424 |
| 0x4740 | 0x2D | 0x2C | 0xC2 | ANALOG425 |
| 0x3EB0 | 0x2D | 0x2C | 0xC2 | ANALOG426 |
| 0x4030 | 0x2D | 0x2C | 0xC2 | ANALOG427 |
| 0x4031 | 0x2D | 0x2C | 0xC2 | ANALOG428 |
| 0x4CD3 | 0x2D | 0x2C | 0xC2 | ANALOG429 |
| 0x4DA3 | 0x2D | 0x2C | 0xC2 | ANALOG430 |
| 0x4521 | 0x2D | 0x2C | 0xC2 | ANALOG431 |
| 0x4530 | 0x2D | 0x2C | 0xC2 | ANALOG432 |
| 0x4332 | 0x2D | 0x2C | 0xC2 | ANALOG433 |
| 0x4333 | 0x2D | 0x2C | 0xC2 | ANALOG434 |
| 0x4340 | 0x2D | 0x2C | 0xC2 | ANALOG435 |
| 0x4351 | 0x2D | 0x2C | 0xC2 | ANALOG436 |
| 0x4360 | 0x2D | 0x2C | 0xC2 | ANALOG437 |
| 0x4361 | 0x2D | 0x2C | 0xC2 | ANALOG438 |
| 0x4362 | 0x2D | 0x2C | 0xC2 | ANALOG439 |
| 0x4382 | 0x2D | 0x2C | 0xC2 | ANALOG440 |
| 0x4378 | 0x2D | 0x2C | 0xC2 | ANALOG441 |
| 0x4C40 | 0x2D | 0x2C | 0xC2 | ANALOG442 |
| 0x4C41 | 0x2D | 0x2C | 0xC2 | ANALOG443 |
| 0x4C42 | 0x2D | 0x2C | 0xC2 | ANALOG444 |
| 0x4C43 | 0x2D | 0x2C | 0xC2 | ANALOG445 |
| 0x4010 | 0x2D | 0x2C | 0xC2 | ANALOG446 |
| 0x4011 | 0x2D | 0x2C | 0xC2 | ANALOG447 |
| 0x4020 | 0x2D | 0x2C | 0xC2 | ANALOG448 |
| 0x4021 | 0x2D | 0x2C | 0xC2 | ANALOG449 |
| 0x4CE0 | 0x2D | 0x2C | 0xC2 | ANALOG450 |
| 0x4CF3 | 0x2D | 0x2C | 0xC2 | ANALOG451 |
| 0x4D00 | 0x2D | 0x2C | 0xC2 | ANALOG452 |
| 0x4D01 | 0x2D | 0x2C | 0xC2 | ANALOG453 |
| 0x4D03 | 0x2D | 0x2C | 0xC2 | ANALOG454 |
| 0x4D13 | 0x2D | 0x2C | 0xC2 | ANALOG455 |
| 0x4D23 | 0x2D | 0x2C | 0xC2 | ANALOG456 |
| 0x4D30 | 0x2D | 0x2C | 0xC2 | ANALOG457 |
| 0x4D31 | 0x2D | 0x2C | 0xC2 | ANALOG458 |
| 0x4D40 | 0x2D | 0x2C | 0xC2 | ANALOG459 |
| 0x4D53 | 0x2D | 0x2C | 0xC2 | ANALOG460 |
| 0x4D60 | 0x2D | 0x2C | 0xC2 | ANALOG461 |
| 0x4D61 | 0x2D | 0x2C | 0xC2 | ANALOG462 |
| 0x4D63 | 0x2D | 0x2C | 0xC2 | ANALOG463 |
| 0x4D73 | 0x2D | 0x2C | 0xC2 | ANALOG464 |
| 0x4750 | 0x2D | 0x2C | 0xC2 | ANALOG465 |
| 0x4753 | 0x2D | 0x2C | 0xC2 | ANALOG466 |
| 0x3F30 | 0x2D | 0x2C | 0xC2 | ANALOG467 |
| 0x3F31 | 0x2D | 0x2C | 0xC2 | ANALOG468 |
| 0x3F40 | 0x2D | 0x2C | 0xC2 | ANALOG469 |
| 0x3F41 | 0x2D | 0x2C | 0xC2 | ANALOG470 |
| 0x4B90 | 0x2D | 0x2C | 0xC2 | ANALOG471 |
| 0x42F2 | 0x2D | 0x2C | 0xC2 | ANALOG472 |
| 0x42E2 | 0x2D | 0x2C | 0xC2 | ANALOG473 |
| 0x4560 | 0x2D | 0x2C | 0xC2 | ANALOG474 |
| 0x4570 | 0x2D | 0x2C | 0xC2 | ANALOG475 |
| 0x4580 | 0x2D | 0x2C | 0xC2 | ANALOG476 |
| 0x4590 | 0x2D | 0x2C | 0xC2 | ANALOG477 |
| 0x45A0 | 0x2D | 0x2C | 0xC2 | ANALOG478 |
| 0x45C0 | 0x2D | 0x2C | 0xC2 | ANALOG479 |
| 0x4B80 | 0x2D | 0x2C | 0xC2 | ANALOG480 |
| 0x4600 | 0x2D | 0x2C | 0xC2 | ANALOG481 |
| 0x4610 | 0x2D | 0x2C | 0xC2 | ANALOG482 |
| 0x4620 | 0x2D | 0x2C | 0xC2 | ANALOG483 |
| 0x4630 | 0x2D | 0x2C | 0xC2 | ANALOG484 |
| 0x4640 | 0x2D | 0x2C | 0xC2 | ANALOG485 |
| 0x4650 | 0x2D | 0x2C | 0xC2 | ANALOG486 |
| 0x44F0 | 0x2D | 0x2C | 0xC2 | ANALOG487 |
| 0x4711 | 0x2D | 0x2C | 0xC2 | ANALOG488 |
| 0x4712 | 0x2D | 0x2C | 0xC2 | ANALOG489 |
| 0x4713 | 0x2D | 0x2C | 0xC2 | ANALOG490 |
| 0x4670 | 0x2D | 0x2C | 0xC2 | ANALOG491 |
| 0x4671 | 0x2D | 0x2C | 0xC2 | ANALOG492 |
| 0x4680 | 0x2D | 0x2C | 0xC2 | ANALOG493 |
| 0x4681 | 0x2D | 0x2C | 0xC2 | ANALOG494 |
| 0x4690 | 0x2D | 0x2C | 0xC2 | ANALOG495 |
| 0x4691 | 0x2D | 0x2C | 0xC2 | ANALOG496 |
| 0x4125 | 0x2D | 0x2C | 0xC2 | ANALOG497 |
| 0x4125 | 0x2D | 0x2C | 0xC2 | ANALOG498 |
| 0x4135 | 0x2D | 0x2C | 0xC2 | ANALOG499 |
| 0x4135 | 0x2D | 0x2C | 0xC2 | ANALOG500 |
| 0x4145 | 0x2D | 0x2C | 0xC2 | ANALOG501 |
| 0x4145 | 0x2D | 0x2C | 0xC2 | ANALOG502 |
| 0x4B71 | 0x2D | 0x2C | 0xC2 | ANALOG503 |
| 0x4763 | 0x2D | 0x2C | 0xC2 | ANALOG504 |
| 0x43A0 | 0x2D | 0x2C | 0xC2 | ANALOG505 |
| 0x43A1 | 0x2D | 0x2C | 0xC2 | ANALOG506 |
| 0x43A2 | 0x2D | 0x2C | 0xC2 | ANALOG507 |
| 0x43A3 | 0x2D | 0x2C | 0xC2 | ANALOG508 |
| 0x43B0 | 0x2D | 0x2C | 0xC2 | ANALOG509 |
| 0x43B1 | 0x2D | 0x2C | 0xC2 | ANALOG510 |
| 0x43B2 | 0x2D | 0x2C | 0xC2 | ANALOG511 |
| 0x43B3 | 0x2D | 0x2C | 0xC2 | ANALOG512 |
| 0x4A02 | 0x2D | 0x2C | 0xC2 | ANALOG513 |
| 0x4A03 | 0x2D | 0x2C | 0xC2 | ANALOG514 |
| 0x4772 | 0x2D | 0x2C | 0xC2 | ANALOG515 |
| 0x4773 | 0x2D | 0x2C | 0xC2 | ANALOG516 |
| 0x43C0 | 0x2D | 0x2C | 0xC2 | ANALOG517 |
| 0x43D1 | 0x2D | 0x2C | 0xC2 | ANALOG518 |
| 0x43E2 | 0x2D | 0x2C | 0xC2 | ANALOG519 |
| 0x43E3 | 0x2D | 0x2C | 0xC2 | ANALOG520 |
| 0x4130 | 0x2D | 0x2C | 0xC2 | ANALOG521 |
| 0x4141 | 0x2D | 0x2C | 0xC2 | ANALOG522 |
| 0x4152 | 0x2D | 0x2C | 0xC2 | ANALOG523 |
| 0x4153 | 0x2D | 0x2C | 0xC2 | ANALOG524 |
| 0x3F50 | 0x2D | 0x2C | 0xC2 | ANALOG525 |
| 0x3F51 | 0x2D | 0x2C | 0xC2 | ANALOG526 |
| 0x3F52 | 0x2D | 0x2C | 0xC2 | ANALOG527 |
| 0x3F53 | 0x2D | 0x2C | 0xC2 | ANALOG528 |
| 0x3F62 | 0x2D | 0x2C | 0xC2 | ANALOG529 |
| 0x4723 | 0x2D | 0x2C | 0xC2 | ANALOG530 |

<a id="table-analog0"></a>
### ANALOG0

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog1"></a>
### ANALOG1

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog2"></a>
### ANALOG2

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog3"></a>
### ANALOG3

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog4"></a>
### ANALOG4

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog5"></a>
### ANALOG5

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog6"></a>
### ANALOG6

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog7"></a>
### ANALOG7

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog8"></a>
### ANALOG8

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog9"></a>
### ANALOG9

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog10"></a>
### ANALOG10

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog11"></a>
### ANALOG11

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog12"></a>
### ANALOG12

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog13"></a>
### ANALOG13

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog14"></a>
### ANALOG14

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog15"></a>
### ANALOG15

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog16"></a>
### ANALOG16

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog17"></a>
### ANALOG17

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog18"></a>
### ANALOG18

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog19"></a>
### ANALOG19

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog20"></a>
### ANALOG20

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog21"></a>
### ANALOG21

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog22"></a>
### ANALOG22

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog23"></a>
### ANALOG23

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog24"></a>
### ANALOG24

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog25"></a>
### ANALOG25

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog26"></a>
### ANALOG26

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog27"></a>
### ANALOG27

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog28"></a>
### ANALOG28

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog29"></a>
### ANALOG29

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog30"></a>
### ANALOG30

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog31"></a>
### ANALOG31

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog32"></a>
### ANALOG32

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog33"></a>
### ANALOG33

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog34"></a>
### ANALOG34

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog35"></a>
### ANALOG35

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog36"></a>
### ANALOG36

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog37"></a>
### ANALOG37

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog38"></a>
### ANALOG38

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog39"></a>
### ANALOG39

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog40"></a>
### ANALOG40

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog41"></a>
### ANALOG41

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog42"></a>
### ANALOG42

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog43"></a>
### ANALOG43

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog44"></a>
### ANALOG44

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog45"></a>
### ANALOG45

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog46"></a>
### ANALOG46

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog47"></a>
### ANALOG47

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog48"></a>
### ANALOG48

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog49"></a>
### ANALOG49

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog50"></a>
### ANALOG50

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog51"></a>
### ANALOG51

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog52"></a>
### ANALOG52

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog53"></a>
### ANALOG53

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog54"></a>
### ANALOG54

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog55"></a>
### ANALOG55

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog56"></a>
### ANALOG56

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog57"></a>
### ANALOG57

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog58"></a>
### ANALOG58

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x38 | 0x6E |

<a id="table-analog59"></a>
### ANALOG59

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |

<a id="table-analog60"></a>
### ANALOG60

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |

<a id="table-analog61"></a>
### ANALOG61

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |

<a id="table-analog62"></a>
### ANALOG62

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |

<a id="table-analog63"></a>
### ANALOG63

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |

<a id="table-analog64"></a>
### ANALOG64

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |

<a id="table-analog65"></a>
### ANALOG65

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |

<a id="table-analog66"></a>
### ANALOG66

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |

<a id="table-analog67"></a>
### ANALOG67

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |

<a id="table-analog68"></a>
### ANALOG68

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE9 |

<a id="table-analog69"></a>
### ANALOG69

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x49 |

<a id="table-analog70"></a>
### ANALOG70

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x49 |

<a id="table-analog71"></a>
### ANALOG71

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x49 |

<a id="table-analog72"></a>
### ANALOG72

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x49 |

<a id="table-analog73"></a>
### ANALOG73

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x49 |

<a id="table-analog74"></a>
### ANALOG74

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x49 |

<a id="table-analog75"></a>
### ANALOG75

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x6F | 0x2F | 0x32 | 0x6E |

<a id="table-analog76"></a>
### ANALOG76

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x6F | 0x2F | 0x32 | 0x6E |

<a id="table-analog77"></a>
### ANALOG77

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x6F | 0x2F | 0x32 | 0x6E |

<a id="table-analog78"></a>
### ANALOG78

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog79"></a>
### ANALOG79

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog80"></a>
### ANALOG80

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog81"></a>
### ANALOG81

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x7A | 0x7B | 0x6E |

<a id="table-analog82"></a>
### ANALOG82

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x7A | 0x7B | 0x6E |

<a id="table-analog83"></a>
### ANALOG83

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x7A | 0x7B | 0x6E |

<a id="table-analog84"></a>
### ANALOG84

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x7A | 0x7B | 0x6E |

<a id="table-analog85"></a>
### ANALOG85

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog86"></a>
### ANALOG86

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |

<a id="table-analog87"></a>
### ANALOG87

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |

<a id="table-analog88"></a>
### ANALOG88

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |

<a id="table-analog89"></a>
### ANALOG89

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |

<a id="table-analog90"></a>
### ANALOG90

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |

<a id="table-analog91"></a>
### ANALOG91

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |

<a id="table-analog92"></a>
### ANALOG92

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |

<a id="table-analog93"></a>
### ANALOG93

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |

<a id="table-analog94"></a>
### ANALOG94

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |

<a id="table-analog95"></a>
### ANALOG95

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7B |

<a id="table-analog96"></a>
### ANALOG96

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog97"></a>
### ANALOG97

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog98"></a>
### ANALOG98

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog99"></a>
### ANALOG99

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog100"></a>
### ANALOG100

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x39 | 0x2F | 0x32 | 0x6E |

<a id="table-analog101"></a>
### ANALOG101

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x39 | 0x2F | 0x32 | 0x6E |

<a id="table-analog102"></a>
### ANALOG102

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x39 | 0x2F | 0x32 | 0x6E |

<a id="table-analog103"></a>
### ANALOG103

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x39 | 0x2F | 0x32 | 0x6E |

<a id="table-analog104"></a>
### ANALOG104

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog105"></a>
### ANALOG105

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog106"></a>
### ANALOG106

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog107"></a>
### ANALOG107

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog108"></a>
### ANALOG108

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog109"></a>
### ANALOG109

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog110"></a>
### ANALOG110

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x2B | 0x2F | 0x32 | 0x6E |

<a id="table-analog111"></a>
### ANALOG111

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x2B | 0x2F | 0x32 | 0x6E |

<a id="table-analog112"></a>
### ANALOG112

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x2B | 0x2F | 0x32 | 0x6E |

<a id="table-analog113"></a>
### ANALOG113

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x2B | 0x2F | 0x32 | 0x6E |

<a id="table-analog114"></a>
### ANALOG114

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog115"></a>
### ANALOG115

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog116"></a>
### ANALOG116

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog117"></a>
### ANALOG117

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog118"></a>
### ANALOG118

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog119"></a>
### ANALOG119

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog120"></a>
### ANALOG120

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog121"></a>
### ANALOG121

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog122"></a>
### ANALOG122

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog123"></a>
### ANALOG123

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog124"></a>
### ANALOG124

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog125"></a>
### ANALOG125

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog126"></a>
### ANALOG126

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog127"></a>
### ANALOG127

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog128"></a>
### ANALOG128

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog129"></a>
### ANALOG129

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog130"></a>
### ANALOG130

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog131"></a>
### ANALOG131

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog132"></a>
### ANALOG132

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog133"></a>
### ANALOG133

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog134"></a>
### ANALOG134

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog135"></a>
### ANALOG135

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog136"></a>
### ANALOG136

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog137"></a>
### ANALOG137

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog138"></a>
### ANALOG138

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog139"></a>
### ANALOG139

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog140"></a>
### ANALOG140

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog141"></a>
### ANALOG141

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog142"></a>
### ANALOG142

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x62 |

<a id="table-analog143"></a>
### ANALOG143

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x62 |

<a id="table-analog144"></a>
### ANALOG144

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x62 |

<a id="table-analog145"></a>
### ANALOG145

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x62 |

<a id="table-analog146"></a>
### ANALOG146

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog147"></a>
### ANALOG147

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog148"></a>
### ANALOG148

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog149"></a>
### ANALOG149

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog150"></a>
### ANALOG150

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog151"></a>
### ANALOG151

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog152"></a>
### ANALOG152

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x38 | 0x32 | 0x6E |

<a id="table-analog153"></a>
### ANALOG153

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |

<a id="table-analog154"></a>
### ANALOG154

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |

<a id="table-analog155"></a>
### ANALOG155

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |

<a id="table-analog156"></a>
### ANALOG156

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |

<a id="table-analog157"></a>
### ANALOG157

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |

<a id="table-analog158"></a>
### ANALOG158

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |

<a id="table-analog159"></a>
### ANALOG159

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |

<a id="table-analog160"></a>
### ANALOG160

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x7A |

<a id="table-analog161"></a>
### ANALOG161

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |

<a id="table-analog162"></a>
### ANALOG162

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |

<a id="table-analog163"></a>
### ANALOG163

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |

<a id="table-analog164"></a>
### ANALOG164

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |

<a id="table-analog165"></a>
### ANALOG165

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |

<a id="table-analog166"></a>
### ANALOG166

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |

<a id="table-analog167"></a>
### ANALOG167

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |

<a id="table-analog168"></a>
### ANALOG168

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xB0 |

<a id="table-analog169"></a>
### ANALOG169

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog170"></a>
### ANALOG170

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog171"></a>
### ANALOG171

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog172"></a>
### ANALOG172

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog173"></a>
### ANALOG173

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x97 |

<a id="table-analog174"></a>
### ANALOG174

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x97 |

<a id="table-analog175"></a>
### ANALOG175

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x96 |

<a id="table-analog176"></a>
### ANALOG176

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0xD4 | 0x2F | 0x32 | 0x6E |

<a id="table-analog177"></a>
### ANALOG177

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0xD4 | 0x2F | 0x32 | 0x6E |

<a id="table-analog178"></a>
### ANALOG178

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |

<a id="table-analog179"></a>
### ANALOG179

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |

<a id="table-analog180"></a>
### ANALOG180

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |

<a id="table-analog181"></a>
### ANALOG181

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |

<a id="table-analog182"></a>
### ANALOG182

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |

<a id="table-analog183"></a>
### ANALOG183

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |

<a id="table-analog184"></a>
### ANALOG184

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |

<a id="table-analog185"></a>
### ANALOG185

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |

<a id="table-analog186"></a>
### ANALOG186

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |

<a id="table-analog187"></a>
### ANALOG187

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xE8 |

<a id="table-analog188"></a>
### ANALOG188

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog189"></a>
### ANALOG189

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog190"></a>
### ANALOG190

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog191"></a>
### ANALOG191

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog192"></a>
### ANALOG192

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog193"></a>
### ANALOG193

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog194"></a>
### ANALOG194

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog195"></a>
### ANALOG195

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog196"></a>
### ANALOG196

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog197"></a>
### ANALOG197

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog198"></a>
### ANALOG198

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog199"></a>
### ANALOG199

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog200"></a>
### ANALOG200

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog201"></a>
### ANALOG201

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog202"></a>
### ANALOG202

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog203"></a>
### ANALOG203

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog204"></a>
### ANALOG204

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog205"></a>
### ANALOG205

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog206"></a>
### ANALOG206

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog207"></a>
### ANALOG207

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog208"></a>
### ANALOG208

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog209"></a>
### ANALOG209

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog210"></a>
### ANALOG210

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog211"></a>
### ANALOG211

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog212"></a>
### ANALOG212

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog213"></a>
### ANALOG213

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog214"></a>
### ANALOG214

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog215"></a>
### ANALOG215

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog216"></a>
### ANALOG216

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog217"></a>
### ANALOG217

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog218"></a>
### ANALOG218

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog219"></a>
### ANALOG219

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog220"></a>
### ANALOG220

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog221"></a>
### ANALOG221

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog222"></a>
### ANALOG222

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog223"></a>
### ANALOG223

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog224"></a>
### ANALOG224

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog225"></a>
### ANALOG225

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog226"></a>
### ANALOG226

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog227"></a>
### ANALOG227

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog228"></a>
### ANALOG228

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog229"></a>
### ANALOG229

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog230"></a>
### ANALOG230

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog231"></a>
### ANALOG231

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog232"></a>
### ANALOG232

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog233"></a>
### ANALOG233

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog234"></a>
### ANALOG234

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog235"></a>
### ANALOG235

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog236"></a>
### ANALOG236

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog237"></a>
### ANALOG237

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog238"></a>
### ANALOG238

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog239"></a>
### ANALOG239

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog240"></a>
### ANALOG240

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog241"></a>
### ANALOG241

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog242"></a>
### ANALOG242

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog243"></a>
### ANALOG243

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog244"></a>
### ANALOG244

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog245"></a>
### ANALOG245

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog246"></a>
### ANALOG246

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog247"></a>
### ANALOG247

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog248"></a>
### ANALOG248

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog249"></a>
### ANALOG249

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog250"></a>
### ANALOG250

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog251"></a>
### ANALOG251

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog252"></a>
### ANALOG252

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog253"></a>
### ANALOG253

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog254"></a>
### ANALOG254

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog255"></a>
### ANALOG255

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog256"></a>
### ANALOG256

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog257"></a>
### ANALOG257

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog258"></a>
### ANALOG258

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x61 |

<a id="table-analog259"></a>
### ANALOG259

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog260"></a>
### ANALOG260

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog261"></a>
### ANALOG261

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog262"></a>
### ANALOG262

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog263"></a>
### ANALOG263

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog264"></a>
### ANALOG264

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x73 |

<a id="table-analog265"></a>
### ANALOG265

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x73 |

<a id="table-analog266"></a>
### ANALOG266

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x73 |

<a id="table-analog267"></a>
### ANALOG267

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog268"></a>
### ANALOG268

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog269"></a>
### ANALOG269

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x37 | 0x2F | 0x32 | 0x6E |

<a id="table-analog270"></a>
### ANALOG270

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x37 | 0x2F | 0x32 | 0x6E |

<a id="table-analog271"></a>
### ANALOG271

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog272"></a>
### ANALOG272

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog273"></a>
### ANALOG273

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog274"></a>
### ANALOG274

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog275"></a>
### ANALOG275

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog276"></a>
### ANALOG276

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog277"></a>
### ANALOG277

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog278"></a>
### ANALOG278

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog279"></a>
### ANALOG279

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog280"></a>
### ANALOG280

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog281"></a>
### ANALOG281

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog282"></a>
### ANALOG282

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog283"></a>
### ANALOG283

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog284"></a>
### ANALOG284

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog285"></a>
### ANALOG285

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog286"></a>
### ANALOG286

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog287"></a>
### ANALOG287

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog288"></a>
### ANALOG288

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog289"></a>
### ANALOG289

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog290"></a>
### ANALOG290

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog291"></a>
### ANALOG291

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog292"></a>
### ANALOG292

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog293"></a>
### ANALOG293

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog294"></a>
### ANALOG294

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog295"></a>
### ANALOG295

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog296"></a>
### ANALOG296

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog297"></a>
### ANALOG297

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog298"></a>
### ANALOG298

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog299"></a>
### ANALOG299

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog300"></a>
### ANALOG300

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog301"></a>
### ANALOG301

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog302"></a>
### ANALOG302

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog303"></a>
### ANALOG303

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog304"></a>
### ANALOG304

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog305"></a>
### ANALOG305

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog306"></a>
### ANALOG306

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog307"></a>
### ANALOG307

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog308"></a>
### ANALOG308

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog309"></a>
### ANALOG309

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog310"></a>
### ANALOG310

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog311"></a>
### ANALOG311

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog312"></a>
### ANALOG312

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog313"></a>
### ANALOG313

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog314"></a>
### ANALOG314

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog315"></a>
### ANALOG315

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog316"></a>
### ANALOG316

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog317"></a>
### ANALOG317

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog318"></a>
### ANALOG318

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog319"></a>
### ANALOG319

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog320"></a>
### ANALOG320

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog321"></a>
### ANALOG321

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog322"></a>
### ANALOG322

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog323"></a>
### ANALOG323

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog324"></a>
### ANALOG324

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog325"></a>
### ANALOG325

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog326"></a>
### ANALOG326

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog327"></a>
### ANALOG327

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog328"></a>
### ANALOG328

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog329"></a>
### ANALOG329

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog330"></a>
### ANALOG330

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog331"></a>
### ANALOG331

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog332"></a>
### ANALOG332

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog333"></a>
### ANALOG333

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog334"></a>
### ANALOG334

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog335"></a>
### ANALOG335

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog336"></a>
### ANALOG336

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog337"></a>
### ANALOG337

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog338"></a>
### ANALOG338

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog339"></a>
### ANALOG339

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog340"></a>
### ANALOG340

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog341"></a>
### ANALOG341

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog342"></a>
### ANALOG342

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog343"></a>
### ANALOG343

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog344"></a>
### ANALOG344

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog345"></a>
### ANALOG345

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog346"></a>
### ANALOG346

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog347"></a>
### ANALOG347

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog348"></a>
### ANALOG348

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog349"></a>
### ANALOG349

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog350"></a>
### ANALOG350

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog351"></a>
### ANALOG351

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog352"></a>
### ANALOG352

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog353"></a>
### ANALOG353

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog354"></a>
### ANALOG354

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog355"></a>
### ANALOG355

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog356"></a>
### ANALOG356

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog357"></a>
### ANALOG357

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog358"></a>
### ANALOG358

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog359"></a>
### ANALOG359

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog360"></a>
### ANALOG360

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog361"></a>
### ANALOG361

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog362"></a>
### ANALOG362

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog363"></a>
### ANALOG363

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog364"></a>
### ANALOG364

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog365"></a>
### ANALOG365

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog366"></a>
### ANALOG366

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog367"></a>
### ANALOG367

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog368"></a>
### ANALOG368

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog369"></a>
### ANALOG369

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog370"></a>
### ANALOG370

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog371"></a>
### ANALOG371

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog372"></a>
### ANALOG372

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog373"></a>
### ANALOG373

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog374"></a>
### ANALOG374

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog375"></a>
### ANALOG375

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog376"></a>
### ANALOG376

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog377"></a>
### ANALOG377

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog378"></a>
### ANALOG378

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog379"></a>
### ANALOG379

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog380"></a>
### ANALOG380

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog381"></a>
### ANALOG381

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog382"></a>
### ANALOG382

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog383"></a>
### ANALOG383

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog384"></a>
### ANALOG384

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog385"></a>
### ANALOG385

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog386"></a>
### ANALOG386

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog387"></a>
### ANALOG387

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog388"></a>
### ANALOG388

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog389"></a>
### ANALOG389

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog390"></a>
### ANALOG390

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog391"></a>
### ANALOG391

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog392"></a>
### ANALOG392

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog393"></a>
### ANALOG393

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog394"></a>
### ANALOG394

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog395"></a>
### ANALOG395

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog396"></a>
### ANALOG396

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog397"></a>
### ANALOG397

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog398"></a>
### ANALOG398

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog399"></a>
### ANALOG399

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog400"></a>
### ANALOG400

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |

<a id="table-analog401"></a>
### ANALOG401

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |

<a id="table-analog402"></a>
### ANALOG402

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |

<a id="table-analog403"></a>
### ANALOG403

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |

<a id="table-analog404"></a>
### ANALOG404

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |

<a id="table-analog405"></a>
### ANALOG405

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |

<a id="table-analog406"></a>
### ANALOG406

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |

<a id="table-analog407"></a>
### ANALOG407

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEC |

<a id="table-analog408"></a>
### ANALOG408

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog409"></a>
### ANALOG409

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog410"></a>
### ANALOG410

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog411"></a>
### ANALOG411

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog412"></a>
### ANALOG412

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog413"></a>
### ANALOG413

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog414"></a>
### ANALOG414

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog415"></a>
### ANALOG415

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xAF |

<a id="table-analog416"></a>
### ANALOG416

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xAF |

<a id="table-analog417"></a>
### ANALOG417

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xAF |

<a id="table-analog418"></a>
### ANALOG418

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xAF |

<a id="table-analog419"></a>
### ANALOG419

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog420"></a>
### ANALOG420

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog421"></a>
### ANALOG421

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog422"></a>
### ANALOG422

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog423"></a>
### ANALOG423

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog424"></a>
### ANALOG424

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog425"></a>
### ANALOG425

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog426"></a>
### ANALOG426

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog427"></a>
### ANALOG427

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog428"></a>
### ANALOG428

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog429"></a>
### ANALOG429

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog430"></a>
### ANALOG430

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog431"></a>
### ANALOG431

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x7A | 0x7B | 0x6E |

<a id="table-analog432"></a>
### ANALOG432

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x7A | 0x7B | 0x6E |

<a id="table-analog433"></a>
### ANALOG433

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |

<a id="table-analog434"></a>
### ANALOG434

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |

<a id="table-analog435"></a>
### ANALOG435

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |

<a id="table-analog436"></a>
### ANALOG436

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |

<a id="table-analog437"></a>
### ANALOG437

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |

<a id="table-analog438"></a>
### ANALOG438

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |

<a id="table-analog439"></a>
### ANALOG439

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |

<a id="table-analog440"></a>
### ANALOG440

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |

<a id="table-analog441"></a>
### ANALOG441

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xED |

<a id="table-analog442"></a>
### ANALOG442

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog443"></a>
### ANALOG443

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog444"></a>
### ANALOG444

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog445"></a>
### ANALOG445

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog446"></a>
### ANALOG446

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog447"></a>
### ANALOG447

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog448"></a>
### ANALOG448

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog449"></a>
### ANALOG449

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog450"></a>
### ANALOG450

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog451"></a>
### ANALOG451

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog452"></a>
### ANALOG452

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog453"></a>
### ANALOG453

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog454"></a>
### ANALOG454

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog455"></a>
### ANALOG455

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog456"></a>
### ANALOG456

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog457"></a>
### ANALOG457

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog458"></a>
### ANALOG458

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog459"></a>
### ANALOG459

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog460"></a>
### ANALOG460

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog461"></a>
### ANALOG461

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog462"></a>
### ANALOG462

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog463"></a>
### ANALOG463

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog464"></a>
### ANALOG464

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog465"></a>
### ANALOG465

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog466"></a>
### ANALOG466

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog467"></a>
### ANALOG467

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xD3 |

<a id="table-analog468"></a>
### ANALOG468

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xD3 |

<a id="table-analog469"></a>
### ANALOG469

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0xD3 | 0x2F | 0x32 | 0x5B |

<a id="table-analog470"></a>
### ANALOG470

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0xD3 | 0x2F | 0x32 | 0x5B |

<a id="table-analog471"></a>
### ANALOG471

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog472"></a>
### ANALOG472

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog473"></a>
### ANALOG473

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog474"></a>
### ANALOG474

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xEC |

<a id="table-analog475"></a>
### ANALOG475

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xEC |

<a id="table-analog476"></a>
### ANALOG476

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xEC |

<a id="table-analog477"></a>
### ANALOG477

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xEC |

<a id="table-analog478"></a>
### ANALOG478

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xEC |

<a id="table-analog479"></a>
### ANALOG479

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xEC |

<a id="table-analog480"></a>
### ANALOG480

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xEC |

<a id="table-analog481"></a>
### ANALOG481

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xED |

<a id="table-analog482"></a>
### ANALOG482

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xED |

<a id="table-analog483"></a>
### ANALOG483

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xED |

<a id="table-analog484"></a>
### ANALOG484

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xED |

<a id="table-analog485"></a>
### ANALOG485

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xED |

<a id="table-analog486"></a>
### ANALOG486

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xED |

<a id="table-analog487"></a>
### ANALOG487

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0xC3 | 0x32 | 0xED |

<a id="table-analog488"></a>
### ANALOG488

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog489"></a>
### ANALOG489

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog490"></a>
### ANALOG490

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog491"></a>
### ANALOG491

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog492"></a>
### ANALOG492

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog493"></a>
### ANALOG493

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog494"></a>
### ANALOG494

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog495"></a>
### ANALOG495

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog496"></a>
### ANALOG496

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog497"></a>
### ANALOG497

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog498"></a>
### ANALOG498

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog499"></a>
### ANALOG499

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog500"></a>
### ANALOG500

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog501"></a>
### ANALOG501

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog502"></a>
### ANALOG502

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog503"></a>
### ANALOG503

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog504"></a>
### ANALOG504

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog505"></a>
### ANALOG505

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog506"></a>
### ANALOG506

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog507"></a>
### ANALOG507

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog508"></a>
### ANALOG508

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog509"></a>
### ANALOG509

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog510"></a>
### ANALOG510

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog511"></a>
### ANALOG511

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog512"></a>
### ANALOG512

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog513"></a>
### ANALOG513

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog514"></a>
### ANALOG514

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog515"></a>
### ANALOG515

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog516"></a>
### ANALOG516

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog517"></a>
### ANALOG517

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEA |

<a id="table-analog518"></a>
### ANALOG518

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEA |

<a id="table-analog519"></a>
### ANALOG519

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEA |

<a id="table-analog520"></a>
### ANALOG520

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEA |

<a id="table-analog521"></a>
### ANALOG521

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEB |

<a id="table-analog522"></a>
### ANALOG522

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEB |

<a id="table-analog523"></a>
### ANALOG523

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEB |

<a id="table-analog524"></a>
### ANALOG524

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0xEB |

<a id="table-analog525"></a>
### ANALOG525

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog526"></a>
### ANALOG526

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog527"></a>
### ANALOG527

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog528"></a>
### ANALOG528

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog529"></a>
### ANALOG529

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-analog530"></a>
### ANALOG530

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x34 | 0x50 | 0x3A | 0x48 | 0x2F | 0x32 | 0x6E |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | 11220333 |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-ewsempfangsstatus"></a>
### EWSEMPFANGSSTATUS

Dimensions: 12 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Startwertprogrammierung bzw. -ruecksetzen war erfolgreich |
| 0x01 | falscher Startwert beim Ruecksetzen (EWS u. DDE passen ni. zusammen) |
| 0x02 | Telegramminhalt war kein Startwert (event. Wechselcode) |
| 0x03 | Schnittstellenfehler DWA: Frame o. Parity oder kein Signal (Timeout) |
| 0x04 | Prozess laeuft |
| 0x05 | Programmierung bzw. Ruecksetzen im Fahrzyklus noch nicht ausgefuehrt |
| 0x06 | gleiche Zufallszahl wie bei vorherigem Ruecksetzen trotz Weiterschaltung |
| 0x07 | noch kein Startwert programmiert |
| 0x10 | Startwert nicht korrekt in Flash programmiert |
| 0x11 | Wechselcode nicht korrekt in EEPROM-Spiegel programmiert |
| 0x21 | 2-aus-3-Startwertablage im Flash nicht in Ordnung |
| 0xXY | Fehlerhafter Status |

<a id="table-ewsstart"></a>
### EWSSTART

Dimensions: 5 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | DDE bereit, Startwert zu empfangen |
| 0x01 | kein freier Startwert mit Freigabe vorhanden |
| 0x02 | noch kein Startwert gespeichert |
| 0x03 | Startwert nicht plausibel |
| 0xXY | Fehlerhafter Status |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 86 rows × 2 columns

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
| ?A0? | ERROR_DIAG_PROT |
| ?A1? | ERROR_SG_ADRESSE |
| ?A2? | ERROR_SG_MAXANZAHL_AIF |
| ?A3? | ERROR_SG_GROESSE_AIF |
| ?A4? | ERROR_SG_ENDEKENNUNG_AIF |
| ?A5? | ERROR_SG_AUTHENTISIERUNG |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-diagmode"></a>
### DIAGMODE

Dimensions: 14 rows × 3 columns

| NR | MODE | MODE_TEXT |
| --- | --- | --- |
| 0x81 | DEFAULT | DefaultMode |
| 0x82 | PT | PeriodicTransmissions |
| 0x84 | EOLSSM | EndOfLineSystemSupplierMode |
| 0x85 | ECUPM | ECUProgrammingMode |
| 0x86 | ECUDM | ECUDevelopmentMode |
| 0x87 | ECUAM | ECUAdjustmentMode |
| 0x88 | ECUVCM | ECUVariantCodingMode |
| 0x89 | ECUSM | ECUSafetyMode |
| 0xFA | SSS_A | SystemSupplierSpecific (A) |
| 0xFB | SSS_B | SystemSupplierSpecific (B) |
| 0xFC | SSS_C | SystemSupplierSpecific (C) |
| 0xFD | SSS_D | SystemSupplierSpecific (D) |
| 0xFE | SSS_E | SystemSupplierSpecific (E) |
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-baudrate"></a>
### BAUDRATE

Dimensions: 7 rows × 3 columns

| NR | BAUD | BAUD_TEXT |
| --- | --- | --- |
| 0x01 | PC9600 | Baudrate 9.6 kBaud |
| 0x02 | PC19200 | Baudrate 19.2 kBaud |
| 0x03 | PC38400 | Baudrate 38.4 kBaud |
| 0x04 | PC57600 | Baudrate 57.6 kBaud |
| 0x05 | PC115200 | Baudrate 115.2 kBaud |
| 0x06 | SB | Specific Baudrate |
| 0xXY | -- | unbekannte Baudrate |
