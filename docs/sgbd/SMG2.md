# SMG2.prg

- Jobs: [46](#jobs)
- Tables: [57](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Getriebesteuerung SMG MK II / M3 |
| ORIGIN | BMW TI-430 Gall |
| REVISION | 1.101 |
| AUTHOR | BMW-M ZS-E-53 Th.Gey, TI-430 Gall |
| COMMENT | Originalfile smg.b2s geaendert fuer SMG MK II |
| PACKAGE | 0.12 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer EGS
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Ident-Daten fuer EGS
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Auslesen des QUICK Fehlerspeichers
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen High-Konzept nach Lastenheft Codierung/Diagnose E39 Ausgabe 05
- [FS_SHADOW_LESEN](#job-fs-shadow-lesen) - Shadowspeicher lesen High-Konzept nach Lastenheft Codierung/Diagnose E39 Ausgabe 05
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen fuer EGS
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [STATUS_LESEN](#job-status-lesen) - Beliebige EPROM - Zellen auslesen
- [SPEICHER_LESEN](#job-speicher-lesen) - Speicher Lesen
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben von beliebigen Speicherzellen
- [ZIF](#job-zif) - Job ZIF
- [ZIF_BACKUP](#job-zif-backup) - Job ZIF_BACKUP
- [HERSTELLER_DATEN_LESEN](#job-hersteller-daten-lesen) - Herstellerdaten lesen (Kontrollbyte 53)
- [SG_RESET](#job-sg-reset) - Zuruecksetzen des SG Nur nach einer Neuprogrammierung durchführbar!
- [FLASH_LESEN](#job-flash-lesen) - Beliebige FLASH - Zellen auslesen
- [FLASH_LOESCHEN](#job-flash-loeschen) - Flash - Zellen loeschen
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Beliebige Flash Zellen mit 02 beschreiben
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Beliebige EPROM - Zellen auslesen
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [AIF_SCHREIBEN](#job-aif-schreiben) - Beschreiben des Anwender-Info-Feldes
- [STATUS_CODIER_CHECKSUMME](#job-status-codier-checksumme) - Codier - Checksumme abfragen
- [BAUDRATEN_LESEN](#job-baudraten-lesen) - Baudratentabelle auslesen
- [BAUDRATEN_UMSTELLUNG](#job-baudraten-umstellung) - Baudrate veraendern
- [EDIC_RESET](#job-edic-reset) - EDIC-Reset
- [SET_EDIC_BAUDRATE](#job-set-edic-baudrate) - EDIC-Parameter auf 125 KBd oder 9600Bd
- [BLOCKLAENGE_MAX](#job-blocklaenge-max) - maximale Blocklaenge
- [DATEN_REFERENZ](#job-daten-referenz) - Job DATEN-Referenz
- [HW_REFERENZ](#job-hw-referenz) - Job HW-Referenz
- [SEED_KEY](#job-seed-key) - Schutzmechanismus SEED_KEY
- [ANSTEUERUNG_VORBEREITEN](#job-ansteuerung-vorbereiten) - Vorbereiten STEUERN_STELLGLIED, (Zeit-Zaehler auf null setzen) Achtung: Fuer Anlasserfreigabe, Hydropumpe, Stoeranzeige und Shiftlock muss dieser Job vorab gesendet werden! (Steuergeraete-Timeout: 10s!) Wird die Diagnose zum nachtriggern des SG-Timeouts aufrechterhalten, so bleibt die Ansteuerung max. 60s erhalten. Diese Groessen werden ueber INAKTIV ausgeschaltet. Fuer ansteuerbare Groessen siehe immer aktuelles Lastenheft!
- [STEUERN_STELLGLIED](#job-steuern-stellglied) - Ansteuern der Stellglieder
- [TESTPRG_STOP](#job-testprg-stop) - Beenden eines laufenden Testprogrammes Muss VOR TESTPRG_STARTEN geschickt werden! (Steuergeraete-Timeout: 10s!)
- [TESTPRG_STARTEN](#job-testprg-starten) - Testprogramm starten Hinweis: Zuvor TESTPRG_STOP schicken!
- [CODIERDATEN_LESEN](#job-codierdaten-lesen) - Codierdaten lesen Kontrollbyte (0x08)
- [CODIERDATEN_SCHREIBEN](#job-codierdaten-schreiben) - Codierung schreiben
- [GETRIEBEDATEN_LESEN](#job-getriebedaten-lesen) - Abgleichwerte lesen (Kontrollbyte 0x40)  Getriebedaten lesen ohne Argument fuer VS-21 (vgl. ADAPTIONSWERTE_LESEN)
- [ADAPTIONSWERTE_LESEN](#job-adaptionswerte-lesen) - Adaptionswerte lesen Abgleichwerte lesen (Kontrollbyte 0x40)
- [ADAPTIONSWERTE_LOESCHEN](#job-adaptionswerte-loeschen) - Adaptionswerte loeschen (Kontrollbyte 0x43)
- [STATUS_HARDWARE_STATI_LESEN](#job-status-hardware-stati-lesen) - Hardwarestati SMG
- [STATUS_IO_LESEN](#job-status-io-lesen) - Status Eingaenge SMG
- [STATUS_IO_STATI_LESEN](#job-status-io-stati-lesen) - Status Eingaenge SMG
- [STATUS_FAHRZEUGTESTER_LESEN](#job-status-fahrzeugtester-lesen) - I/O Status lesen (Kontrollbyte 0x0B) Fahrzeugtester   (Auswahlbyte  0x05) Status der Ein- u. Ausgaenge GETRAG und VS21 spezifischer Job (Nicht fuer INPA gedacht.)

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job fuer EGS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

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

Ident-Daten fuer EGS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | string | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | string | Bus-Index |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |
| ID_LIEF_NR | string | Lieferanten-Nummer |
| ID_SW_NR | string | Softwarenummer |
| ID_SN_NR | string | Seriennummer |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Auslesen des QUICK Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_KM_AKT | real | km-Stand aktuell |
| F_KM_ALT | real | km-Stand beim letzten Loeschen |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen High-Konzept nach Lastenheft Codierung/Diagnose E39 Ausgabe 05

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ANZ_NR | int | Anzahl aller gespeicherter Fehler (max. 16) |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HEX_CODE | binary | Hexdumps eines der Fehlerdatums (Antworttelegramm eines Fehlers ohne Header und Pruefsumme) Beginnt hier mit Byte: 1     = FZ (Fehlerzaehler) 2     = FC (Fehlercode/Fehlerort) 3     = FA (Fehlerart) 4     = HZ (Fehler Haeufigkeitszaehler) 5 -24 = Umweltsatz 1, 1.Auftreten 25-44 = Umweltsatz 2, 2.Auftreten 45-65 = Umweltsatz 3, letztes Auftreten Ersten 6 Bytes jeden Satzes bestehen aus Kilometerstand Umgebungstemperatur Batteriespannnung |
| F_HEX_CODE_ALLER_FEHLER | binary | Beinhaltet nur Fehlerdaten aller Fehler (Ohne Header und Pruefsumme) (Fehlerdaten werden aus einzelnen Telegrammen zusammengesetzt.) Anforderung von VS-21 |
| F_HEX_CODE_FZ_BIS_HZ | binary | Ausplittung von F_HEX_CODE Antworttelegramm der Fehlerdaten bestehen nur aus 1     = FZ (Fehlerzaehler) 2     = FC (Fehlercode/Fehlerort) 3     = FA (Fehlerart) 4     = HZ (Fehler Haeufigkeitszaehler) |
| F_HEX_CODE_UMWELTSATZ1 | binary | Ausplittung von F_HEX_CODE Umweltsatz 1 |
| F_HEX_CODE_UMWELTSATZ2 | binary | Ausplittung von F_HEX_CODE Umweltsatz 2 |
| F_HEX_CODE_UMWELTSATZ3 | binary | Aufsplittung von F_HEX_CODE Umweltsatz 3 |
| F_HFK | int | Wertebereich 0 - 31 |
| F_ART_ANZ | int | immer 1 |
| F_ART1_NR | int | Index der Fehlernummer |
| F_ART1_TEXT | string | Fehlerart als Text |
| F_ART2_NR | int | Index der Fehlernummer |
| F_ART2_TEXT | string | Fehlerart als Text |
| F_ART3_NR | int | Index der Fehlernummer |
| F_ART3_TEXT | string | Fehlerart als Text |
| F_ART4_NR | int | Index der Fehlernummer |
| F_ART4_TEXT | string | Fehlerart als Text |
| F_ART5_NR | int | Index der Fehlernummer |
| F_ART5_TEXT | string | Fehlerart als Text |
| F_ART6_NR | int | Index der Fehlernummer |
| F_ART6_TEXT | string | Fehlerart als Text |
| F_ART7_NR | int | Index der Fehlernummer |
| F_ART7_TEXT | string | Fehlerart als Text |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen bei SMG immer 3 x 10 |
| F_UW_SATZ | int | UW-Satz Nummer |
| F_UW1_NR | int | Index der 1. Umweltbedingung, 1.Satz |
| F_UW1_TEXT | string | Text der 1. Umweltbedingung, 1.Satz |
| F_UW1_WERT | real | Wert der 1. Umweltbedingung, 1.Satz |
| F_UW1_EINH | string | Einheit |
| F_UW2_NR | int | Index der 2. Umweltbedingung, 1.Satz |
| F_UW2_TEXT | string | Text der 2. Umweltbedingung, 1.Satz |
| F_UW2_WERT | real | Wert der 2. Umweltbedingung, 1.Satz |
| F_UW2_EINH | string | Einheit |
| F_UW3_NR | int | Index der 3. Umweltbedingung, 1.Satz |
| F_UW3_TEXT | string | Text der 3. Umweltbedingung, 1.Satz |
| F_UW3_WERT | real | Wert der 3. Umweltbedingung, 1.Satz |
| F_UW3_EINH | string | Einheit |
| F_UW4_NR | int | Index der 4. Umweltbedingung, 1.Satz |
| F_UW4_TEXT | string | Text der 4. Umweltbedingung, 1.Satz |
| F_UW4_WERT | real | Wert der 4. Umweltbedingung, 1.Satz |
| F_UW4_EINH | string | Einheit |
| F_UW5_NR | int | Index der 5. Umweltbedingung, 1.Satz |
| F_UW5_TEXT | string | Text der 5. Umweltbedingung, 1.Satz |
| F_UW5_WERT | real | Wert der 5. Umweltbedingung, 1.Satz |
| F_UW5_EINH | string | Einheit |
| F_UW6_NR | int | Index der 6. Umweltbedingung, 1.Satz |
| F_UW6_TEXT | string | Text der 6. Umweltbedingung, 1.Satz |
| F_UW6_WERT | real | Wert der 6. Umweltbedingung, 1.Satz |
| F_UW6_EINH | string | Einheit |
| F_UW7_NR | int | Index der 7. Umweltbedingung, 1.Satz |
| F_UW7_TEXT | string | Text der 7. Umweltbedingung, 1.Satz |
| F_UW7_WERT | real | Wert der 7. Umweltbedingung, 1.Satz |
| F_UW7_EINH | string | Einheit |
| F_UW8_NR | int | Index der 8. Umweltbedingung, 1.Satz |
| F_UW8_TEXT | string | Text der 8. Umweltbedingung, 1.Satz |
| F_UW8_WERT | real | Wert der 8. Umweltbedingung, 1.Satz |
| F_UW8_EINH | string | Einheit |
| F_UW9_NR | int | Index der 9. Umweltbedingung, 1.Satz |
| F_UW9_TEXT | string | Text der 9. Umweltbedingung, 1.Satz |
| F_UW9_WERT | real | Wert der 9. Umweltbedingung, 1.Satz |
| F_UW9_EINH | string | Einheit |
| F_UW10_NR | int | Index der 10. Umweltbedingung, 1.Satz |
| F_UW10_TEXT | string | Text der 10. Umweltbedingung, 1.Satz |
| F_UW10_WERT | real | Wert der 10. Umweltbedingung, 1.Satz |
| F_UW10_EINH | string | Einheit |
| F_UW11_NR | int | Index der 1. Umweltbedingung, 2.Satz |
| F_UW11_TEXT | string | Text der 1. Umweltbedingung, 2.Satz |
| F_UW11_WERT | real | Wert der 1. Umweltbedingung, 2.Satz |
| F_UW11_EINH | string | Einheit |
| F_UW12_NR | int | Index der 2. Umweltbedingung, 2.Satz |
| F_UW12_TEXT | string | Text der 2. Umweltbedingung, 2.Satz |
| F_UW12_WERT | real | Wert der 2. Umweltbedingung, 2.Satz |
| F_UW12_EINH | string | Einheit |
| F_UW13_NR | int | Index der 3. Umweltbedingung, 2.Satz |
| F_UW13_TEXT | string | Text der 3. Umweltbedingung, 2.Satz |
| F_UW13_WERT | real | Wert der 3. Umweltbedingung, 2.Satz |
| F_UW13_EINH | string | Einheit |
| F_UW14_NR | int | Index der 4. Umweltbedingung, 2.Satz |
| F_UW14_TEXT | string | Text der 4. Umweltbedingung, 2.Satz |
| F_UW14_WERT | real | Wert der 4. Umweltbedingung, 2.Satz |
| F_UW14_EINH | string | Einheit |
| F_UW15_NR | int | Index der 5. Umweltbedingung, 2.Satz |
| F_UW15_TEXT | string | Text der 5. Umweltbedingung, 2.Satz |
| F_UW15_WERT | real | Wert der 5. Umweltbedingung, 2.Satz |
| F_UW15_EINH | string | Einheit |
| F_UW16_NR | int | Index der 6. Umweltbedingung, 2.Satz |
| F_UW16_TEXT | string | Text der 6. Umweltbedingung, 2.Satz |
| F_UW16_WERT | real | Wert der 6. Umweltbedingung, 2.Satz |
| F_UW16_EINH | string | Einheit |
| F_UW17_NR | int | Index der 7. Umweltbedingung, 2.Satz |
| F_UW17_TEXT | string | Text der 7. Umweltbedingung, 2.Satz |
| F_UW17_WERT | real | Wert der 7. Umweltbedingung, 2.Satz |
| F_UW17_EINH | string | Einheit |
| F_UW18_NR | int | Index der 8. Umweltbedingung, 2.Satz |
| F_UW18_TEXT | string | Text der 8. Umweltbedingung, 2.Satz |
| F_UW18_WERT | real | Wert der 8. Umweltbedingung, 2.Satz |
| F_UW18_EINH | string | Einheit |
| F_UW19_NR | int | Index der 9. Umweltbedingung, 2.Satz |
| F_UW19_TEXT | string | Text der 9. Umweltbedingung, 2.Satz |
| F_UW19_WERT | real | Wert der 9. Umweltbedingung, 2.Satz |
| F_UW19_EINH | string | Einheit |
| F_UW20_NR | int | Index der 10. Umweltbedingung, 2.Satz |
| F_UW20_TEXT | string | Text der 10. Umweltbedingung, 2.Satz |
| F_UW20_WERT | real | Wert der 10. Umweltbedingung, 2.Satz |
| F_UW20_EINH | string | Einheit |
| F_UW21_NR | int | Index der 1. Umweltbedingung, 3.Satz |
| F_UW21_TEXT | string | Text der 1. Umweltbedingung, 3.Satz |
| F_UW21_WERT | real | Wert der 1. Umweltbedingung, 3.Satz |
| F_UW21_EINH | string | Einheit |
| F_UW22_NR | int | Index der 2. Umweltbedingung, 3.Satz |
| F_UW22_TEXT | string | Text der 2. Umweltbedingung, 3.Satz |
| F_UW22_WERT | real | Wert der 2. Umweltbedingung, 3.Satz |
| F_UW22_EINH | string | Einheit |
| F_UW23_NR | int | Index der 3. Umweltbedingung, 3.Satz |
| F_UW23_TEXT | string | Text der 3. Umweltbedingung, 3.Satz |
| F_UW23_WERT | real | Wert der 3. Umweltbedingung, 3.Satz |
| F_UW23_EINH | string | Einheit |
| F_UW24_NR | int | Index der 4. Umweltbedingung, 3.Satz |
| F_UW24_TEXT | string | Text der 4. Umweltbedingung, 3.Satz |
| F_UW24_WERT | real | Wert der 4. Umweltbedingung, 3.Satz |
| F_UW24_EINH | string | Einheit |
| F_UW25_NR | int | Index der 5. Umweltbedingung, 3.Satz |
| F_UW25_TEXT | string | Text der 5. Umweltbedingung, 3.Satz |
| F_UW25_WERT | real | Wert der 5. Umweltbedingung, 3.Satz |
| F_UW25_EINH | string | Einheit |
| F_UW26_NR | int | Index der 6. Umweltbedingung, 3.Satz |
| F_UW26_TEXT | string | Text der 6. Umweltbedingung, 3.Satz |
| F_UW26_WERT | real | Wert der 6. Umweltbedingung, 3.Satz |
| F_UW26_EINH | string | Einheit |
| F_UW27_NR | int | Index der 7. Umweltbedingung, 3.Satz |
| F_UW27_TEXT | string | Text der 7. Umweltbedingung, 3.Satz |
| F_UW27_WERT | real | Wert der 7. Umweltbedingung, 3.Satz |
| F_UW27_EINH | string | Einheit |
| F_UW28_NR | int | Index der 8. Umweltbedingung, 3.Satz |
| F_UW28_TEXT | string | Text der 8. Umweltbedingung, 3.Satz |
| F_UW28_WERT | real | Wert der 8. Umweltbedingung, 3.Satz |
| F_UW28_EINH | string | Einheit |
| F_UW29_NR | int | Index der 9. Umweltbedingung, 3.Satz |
| F_UW29_TEXT | string | Text der 9. Umweltbedingung, 3.Satz |
| F_UW29_WERT | real | Wert der 9. Umweltbedingung, 3.Satz |
| F_UW29_EINH | string | Einheit |
| F_UW30_NR | int | Index der 10. Umweltbedingung, 3.Satz |
| F_UW30_TEXT | string | Text der 10. Umweltbedingung, 3.Satz |
| F_UW30_WERT | real | Wert der 10. Umweltbedingung, 3.Satz |
| F_UW30_EINH | string | Einheit |
| F_VORHANDEN | int | Fehler momentan vorhanden (Fehlerart) |
| _TEL_ANTWORT | binary | Beinhaltet immer nur den zuletzt gelesenen Fehler! |

<a id="job-fs-shadow-lesen"></a>
### FS_SHADOW_LESEN

Shadowspeicher lesen High-Konzept nach Lastenheft Codierung/Diagnose E39 Ausgabe 05

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ANZ_NR | int | Anzahl aller gespeicherter Fehler (max. 16) |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HEX_CODE | binary | Antworttelegramm der Fehlerdaten ohne Header und Pruefsumme Beginnt hier mit Byte: 1     = FZ (Fehlerzaehler) 2     = FC (Fehlercode/Fehlerort) 3     = FA (Fehlerart) 4     = HZ (Fehler Haeufigkeitszaehler) 5 -24 = Umweltsatz 1, 1.Auftreten 25-44 = Umweltsatz 2, 2.Auftreten 45-65 = Umweltsatz 3, letztes Auftreten Ersten 6 Bytes jeden Satzes bestehen aus Kilometerstand Umgebungstemperatur Batteriespannnung |
| F_HEX_CODE_ALLER_FEHLER | binary | Beinhaltet nur Fehlerdaten aller Fehler (Ohne Header und Pruefsumme) (Fehlerdaten werden aus einzelnen Telegrammen zusammengesetzt.) Anforderung von VS 22 |
| F_HEX_CODE_FZ_BIS_HZ | binary | Ausplittung von F_HEX_CODE Antworttelegramm der Fehlerdaten bestehen nur aus 1     = FZ (Fehlerzaehler) 2     = FC (Fehlercode/Fehlerort) 3     = FA (Fehlerart) 4     = HZ (Fehler Haeufigkeitszaehler) |
| F_HEX_CODE_UMWELTSATZ1 | binary | Ausplittung von F_HEX_CODE Umweltsatz 1 |
| F_HEX_CODE_UMWELTSATZ2 | binary | Ausplittung von F_HEX_CODE Umweltsatz 2 |
| F_HEX_CODE_UMWELTSATZ3 | binary | Ausplittung von F_HEX_CODE Umweltsatz 3 |
| F_HFK | int | Wertebereich 0 - 31 |
| F_ART_ANZ | int | immer 1 |
| F_ART1_NR | int | Index der Fehlernummer |
| F_ART1_TEXT | string | Fehlerart als Text |
| F_ART2_NR | int | Index der Fehlernummer |
| F_ART2_TEXT | string | Fehlerart als Text |
| F_ART3_NR | int | Index der Fehlernummer |
| F_ART3_TEXT | string | Fehlerart als Text |
| F_ART4_NR | int | Index der Fehlernummer |
| F_ART4_TEXT | string | Fehlerart als Text |
| F_ART5_NR | int | Index der Fehlernummer |
| F_ART5_TEXT | string | Fehlerart als Text |
| F_ART6_NR | int | Index der Fehlernummer |
| F_ART6_TEXT | string | Fehlerart als Text |
| F_ART7_NR | int | Index der Fehlernummer |
| F_ART7_TEXT | string | Fehlerart als Text |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen bei SMG immer 3 x 10 |
| F_UW_SATZ | int | UW-Satz Nummer |
| F_UW1_NR | int | Index der 1. Umweltbedingung, 1.Satz |
| F_UW1_TEXT | string | Text der 1. Umweltbedingung, 1.Satz |
| F_UW1_WERT | real | Wert der 1. Umweltbedingung, 1.Satz |
| F_UW1_EINH | string | Einheit |
| F_UW2_NR | int | Index der 2. Umweltbedingung, 1.Satz |
| F_UW2_TEXT | string | Text der 2. Umweltbedingung, 1.Satz |
| F_UW2_WERT | real | Wert der 2. Umweltbedingung, 1.Satz |
| F_UW2_EINH | string | Einheit |
| F_UW3_NR | int | Index der 3. Umweltbedingung, 1.Satz |
| F_UW3_TEXT | string | Text der 3. Umweltbedingung, 1.Satz |
| F_UW3_WERT | real | Wert der 3. Umweltbedingung, 1.Satz |
| F_UW3_EINH | string | Einheit |
| F_UW4_NR | int | Index der 4. Umweltbedingung, 1.Satz |
| F_UW4_TEXT | string | Text der 4. Umweltbedingung, 1.Satz |
| F_UW4_WERT | real | Wert der 4. Umweltbedingung, 1.Satz |
| F_UW4_EINH | string | Einheit |
| F_UW5_NR | int | Index der 5. Umweltbedingung, 1.Satz |
| F_UW5_TEXT | string | Text der 5. Umweltbedingung, 1.Satz |
| F_UW5_WERT | real | Wert der 5. Umweltbedingung, 1.Satz |
| F_UW5_EINH | string | Einheit |
| F_UW6_NR | int | Index der 6. Umweltbedingung, 1.Satz |
| F_UW6_TEXT | string | Text der 6. Umweltbedingung, 1.Satz |
| F_UW6_WERT | real | Wert der 6. Umweltbedingung, 1.Satz |
| F_UW6_EINH | string | Einheit |
| F_UW7_NR | int | Index der 7. Umweltbedingung, 1.Satz |
| F_UW7_TEXT | string | Text der 7. Umweltbedingung, 1.Satz |
| F_UW7_WERT | real | Wert der 7. Umweltbedingung, 1.Satz |
| F_UW7_EINH | string | Einheit |
| F_UW8_NR | int | Index der 8. Umweltbedingung, 1.Satz |
| F_UW8_TEXT | string | Text der 8. Umweltbedingung, 1.Satz |
| F_UW8_WERT | real | Wert der 8. Umweltbedingung, 1.Satz |
| F_UW8_EINH | string | Einheit |
| F_UW9_NR | int | Index der 9. Umweltbedingung, 1.Satz |
| F_UW9_TEXT | string | Text der 9. Umweltbedingung, 1.Satz |
| F_UW9_WERT | real | Wert der 9. Umweltbedingung, 1.Satz |
| F_UW9_EINH | string | Einheit |
| F_UW10_NR | int | Index der 10. Umweltbedingung, 1.Satz |
| F_UW10_TEXT | string | Text der 10. Umweltbedingung, 1.Satz |
| F_UW10_WERT | real | Wert der 10. Umweltbedingung, 1.Satz |
| F_UW10_EINH | string | Einheit |
| F_UW11_NR | int | Index der 1. Umweltbedingung, 2.Satz |
| F_UW11_TEXT | string | Text der 1. Umweltbedingung, 2.Satz |
| F_UW11_WERT | real | Wert der 1. Umweltbedingung, 2.Satz |
| F_UW11_EINH | string | Einheit |
| F_UW12_NR | int | Index der 2. Umweltbedingung, 2.Satz |
| F_UW12_TEXT | string | Text der 2. Umweltbedingung, 2.Satz |
| F_UW12_WERT | real | Wert der 2. Umweltbedingung, 2.Satz |
| F_UW12_EINH | string | Einheit |
| F_UW13_NR | int | Index der 3. Umweltbedingung, 2.Satz |
| F_UW13_TEXT | string | Text der 3. Umweltbedingung, 2.Satz |
| F_UW13_WERT | real | Wert der 3. Umweltbedingung, 2.Satz |
| F_UW13_EINH | string | Einheit |
| F_UW14_NR | int | Index der 4. Umweltbedingung, 2.Satz |
| F_UW14_TEXT | string | Text der 4. Umweltbedingung, 2.Satz |
| F_UW14_WERT | real | Wert der 4. Umweltbedingung, 2.Satz |
| F_UW14_EINH | string | Einheit |
| F_UW15_NR | int | Index der 5. Umweltbedingung, 2.Satz |
| F_UW15_TEXT | string | Text der 5. Umweltbedingung, 2.Satz |
| F_UW15_WERT | real | Wert der 5. Umweltbedingung, 2.Satz |
| F_UW15_EINH | string | Einheit |
| F_UW16_NR | int | Index der 6. Umweltbedingung, 2.Satz |
| F_UW16_TEXT | string | Text der 6. Umweltbedingung, 2.Satz |
| F_UW16_WERT | real | Wert der 6. Umweltbedingung, 2.Satz |
| F_UW16_EINH | string | Einheit |
| F_UW17_NR | int | Index der 7. Umweltbedingung, 2.Satz |
| F_UW17_TEXT | string | Text der 7. Umweltbedingung, 2.Satz |
| F_UW17_WERT | real | Wert der 7. Umweltbedingung, 2.Satz |
| F_UW17_EINH | string | Einheit |
| F_UW18_NR | int | Index der 8. Umweltbedingung, 2.Satz |
| F_UW18_TEXT | string | Text der 8. Umweltbedingung, 2.Satz |
| F_UW18_WERT | real | Wert der 8. Umweltbedingung, 2.Satz |
| F_UW18_EINH | string | Einheit |
| F_UW19_NR | int | Index der 9. Umweltbedingung, 2.Satz |
| F_UW19_TEXT | string | Text der 9. Umweltbedingung, 2.Satz |
| F_UW19_WERT | real | Wert der 9. Umweltbedingung, 2.Satz |
| F_UW19_EINH | string | Einheit |
| F_UW20_NR | int | Index der 10. Umweltbedingung, 2.Satz |
| F_UW20_TEXT | string | Text der 10. Umweltbedingung, 2.Satz |
| F_UW20_WERT | real | Wert der 10. Umweltbedingung, 2.Satz |
| F_UW20_EINH | string | Einheit |
| F_UW21_NR | int | Index der 1. Umweltbedingung, 3.Satz |
| F_UW21_TEXT | string | Text der 1. Umweltbedingung, 3.Satz |
| F_UW21_WERT | real | Wert der 1. Umweltbedingung, 3.Satz |
| F_UW21_EINH | string | Einheit |
| F_UW22_NR | int | Index der 2. Umweltbedingung, 3.Satz |
| F_UW22_TEXT | string | Text der 2. Umweltbedingung, 3.Satz |
| F_UW22_WERT | real | Wert der 2. Umweltbedingung, 3.Satz |
| F_UW22_EINH | string | Einheit |
| F_UW23_NR | int | Index der 3. Umweltbedingung, 3.Satz |
| F_UW23_TEXT | string | Text der 3. Umweltbedingung, 3.Satz |
| F_UW23_WERT | real | Wert der 3. Umweltbedingung, 3.Satz |
| F_UW23_EINH | string | Einheit |
| F_UW24_NR | int | Index der 4. Umweltbedingung, 3.Satz |
| F_UW24_TEXT | string | Text der 4. Umweltbedingung, 3.Satz |
| F_UW24_WERT | real | Wert der 4. Umweltbedingung, 3.Satz |
| F_UW24_EINH | string | Einheit |
| F_UW25_NR | int | Index der 5. Umweltbedingung, 3.Satz |
| F_UW25_TEXT | string | Text der 5. Umweltbedingung, 3.Satz |
| F_UW25_WERT | real | Wert der 5. Umweltbedingung, 3.Satz |
| F_UW25_EINH | string | Einheit |
| F_UW26_NR | int | Index der 6. Umweltbedingung, 3.Satz |
| F_UW26_TEXT | string | Text der 6. Umweltbedingung, 3.Satz |
| F_UW26_WERT | real | Wert der 6. Umweltbedingung, 3.Satz |
| F_UW26_EINH | string | Einheit |
| F_UW27_NR | int | Index der 7. Umweltbedingung, 3.Satz |
| F_UW27_TEXT | string | Text der 7. Umweltbedingung, 3.Satz |
| F_UW27_WERT | real | Wert der 7. Umweltbedingung, 3.Satz |
| F_UW27_EINH | string | Einheit |
| F_UW28_NR | int | Index der 8. Umweltbedingung, 3.Satz |
| F_UW28_TEXT | string | Text der 8. Umweltbedingung, 3.Satz |
| F_UW28_WERT | real | Wert der 8. Umweltbedingung, 3.Satz |
| F_UW28_EINH | string | Einheit |
| F_UW29_NR | int | Index der 9. Umweltbedingung, 3.Satz |
| F_UW29_TEXT | string | Text der 9. Umweltbedingung, 3.Satz |
| F_UW29_WERT | real | Wert der 9. Umweltbedingung, 3.Satz |
| F_UW29_EINH | string | Einheit |
| F_UW30_NR | int | Index der 10. Umweltbedingung, 3.Satz |
| F_UW30_TEXT | string | Text der 10. Umweltbedingung, 3.Satz |
| F_UW30_WERT | real | Wert der 10. Umweltbedingung, 3.Satz |
| F_UW30_EINH | string | Einheit |
| F_VORHANDEN | int | Fehler momentan vorhanden (Fehlerart) |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen fuer EGS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

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
| JOB_STATUS | string | OKAY, FEHLER |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Beliebige EPROM - Zellen auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| SG_STATUS | int |  |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Speicher Lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPEICHERART | string | Speicherart: FLASH, RAM, ROM, E2PROM --Speicherart kann beliebig angegeben werden-- --da laut Lastenh. keine Auswahl vorgesehen.-- --Auswahl aus Kompatibilitaetsgruenden beibehalten.-- |
| ADRESSE | long | Startadresse (dezimal eingeben) |
| ANZAHL | int | Anzahl zu lesender Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Inhalt der Speicherzellen |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Beschreiben von beliebigen Speicherzellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Programmierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| SPEICHER_SCHREIBEN_ANZAHL | int | Anzahl geschriebener Speicherzellen |

<a id="job-zif"></a>
### ZIF

Job ZIF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| ZIF_PROJEKT | string | Projektkennzeichnung |
| ZIF_PROGRAMM_STAND | string | Programmstand |
| ZIF_BMW_HW | string | BMW HW |
| ZIF_BMW_PST | string | BMW Programmstand |
| ZIF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-zif-backup"></a>
### ZIF_BACKUP

Job ZIF_BACKUP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_BACKUP_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| ZIF_BACKUP_PROJEKT | string | Projektkennzeichnung |
| ZIF_BACKUP_PROGRAMM_STAND | string | Programmstand |
| ZIF_BACKUP_BMW_HW | string | BMW HW |
| ZIF_BACKUP_BMW_PST | string | BMW Programmstand |
| ZIF_BACKUP_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-hersteller-daten-lesen"></a>
### HERSTELLER_DATEN_LESEN

Herstellerdaten lesen (Kontrollbyte 53)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SG_SW_RELEASE | binary | Hersteller spezifische Daten |
| TEST_PROOF | binary | Anfangsadresse FEP-Bereich |
| BMW_ZUS_NR_ADR | binary | Adresse cccccc: BMW Zusammenbaunummer |
| SIEMENS_HW_ADR | binary | Adresse dddddd: SIEMENS Hardwarenummer |
| BMW_HW_NR_ADR | binary | Adresse eeeeee: BMW Hardwarenummer |
| SIEMENS_SW_NR_GESAMT_ADR | binary | Adresse ffffff: |
| ID_SW_NR | binary | Adresse gggggg: SG Softwarenummer |
| SIEMENS_HERSTELLWOCHE_ADR | binary | Adresse hhhhhhh |
| SIEMENS_HERSTELLJAHR_ADR | binary | Adresse iiiiii |
| LIEFERANTEN_NR_ADR | binary | Adresse kkkkkk: Lieferantennummer |
| SW_NR_ADR | binary | Adresse llllll: DS2 Softwarenummer |
| AENDERUNGSINDEX_ADR | binary | Adresse nnnnnn: DS2 Aenderungsindex |
| SG_SERIEN_NR_ADR | binary | Adresse pppppp: Seriennummer (laufende Geraetenummer) |
| PROGRAMMIERSPANNUNG | binary | Direkt, keine Adresse |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-sg-reset"></a>
### SG_RESET

Zuruecksetzen des SG Nur nach einer Neuprogrammierung durchführbar!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-flash-lesen"></a>
### FLASH_LESEN

Beliebige FLASH - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low HEX |
| FLASH_LESEN_ANZAHL_BYTE | int | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_LESEN_WERT | binary | nichts |

<a id="job-flash-loeschen"></a>
### FLASH_LOESCHEN

Flash - Zellen loeschen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Programmierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_LOESCHEN_ADRESSE | binary |  |
| FLASH_LOESCHEN_STATUS | int |  |
| FLASH_LOESCHEN_ANZAHL | int |  |

<a id="job-flash-schreiben"></a>
### FLASH_SCHREIBEN

Beliebige Flash Zellen mit 02 beschreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Programmierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_SCHREIBEN_ADRESSE | binary |  |
| FLASH_SCHREIBEN_STATUS | int |  |
| FLASH_SCHREIBEN_ANZAHL | int |  |

<a id="job-flash-schreiben-ende"></a>
### FLASH_SCHREIBEN_ENDE

Beliebige EPROM - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Programmierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_SCHREIBEN_ENDE_ADRESSE | binary |  |
| FLASH_SCHREIBEN_ENDE_STATUS | int |  |
| FLASH_SCHREIBEN_ENDE_ANZAHL | int |  |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender-Info-Feldes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_NUMMER | int | Nummer des zu lesenden AIF's &gt;=1. 0 bedeutet aktuelles AIF, auf das ein freies AIF folgt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AIF_ADRESSE_HIGH | int | AIF Adresse, naechste (freie), high-word |
| AIF_ADRESSE_LOW | int | AIF Adresse, naechste (freie), low-word |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener (freier) AIF-Eintraege |
| AIF_FG_NR | string | Fahrgestellnummer |
| AIF_DATUM | string | Fertigungsdatum |
| AIF_AENDERUNGS_INDEX | string | Aenderungsindex |
| AIF_SW_NR | string | Softwarenummer |
| AIF_BEHOERDEN_NR | string | Behoerdennummer |
| AIF_ZB_NR | string | Zusammenbaunummer |
| AIF_SERIEN_NR | string | Seriennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_KM | string | Kilometerstand |
| AIF_PROG_NR | string | Programmstandsnummer |

<a id="job-aif-schreiben"></a>
### AIF_SCHREIBEN

Beschreiben des Anwender-Info-Feldes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_ADRESSE | string | AIF Adresse, naechste freie |
| AIF_FG_NR | string | Fahrgestellnummer |
| AIF_DATUM | string | Fertigungsdatum |
| AIF_AENDERUNGS_INDEX | string | Aenderungsindex |
| AIF_SW_NR | string | Softwarenummer |
| AIF_BEHOERDEN_NR | string | Behoerdennummer |
| AIF_ZB_NR | string | Zusammenbaunummer |
| AIF_SERIEN_NR | string | Seriennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_KM | string | Kilometerstand |
| AIF_PROG_NR | string | Programmstandsnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AIF_SCHREIBEN_ADRESSE | binary |  |
| AIF_SCHREIBEN_STATUS | int |  |
| AIF_SCHREIBEN_ANZAHL | int |  |

<a id="job-status-codier-checksumme"></a>
### STATUS_CODIER_CHECKSUMME

Codier - Checksumme abfragen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_CHECKSUMME_WERT | int | Ergebnis |

<a id="job-baudraten-lesen"></a>
### BAUDRATEN_LESEN

Baudratentabelle auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BAUDRATE_NUMMER | int | Nummer der zu lesenden Baudrate |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BAUDRATE | string | Baudrate 0....125000 "" heisst Tabellenende gelesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-baudraten-umstellung"></a>
### BAUDRATEN_UMSTELLUNG

Baudrate veraendern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BAUDRATE | long | Baudrate 0....125000 |
| BLOCKZWISCHENZEIT | int | 0... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-edic-reset"></a>
### EDIC_RESET

EDIC-Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-set-edic-baudrate"></a>
### SET_EDIC_BAUDRATE

EDIC-Parameter auf 125 KBd oder 9600Bd

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BAUDRATE | string | Baudrate "9600" oder "125000" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-blocklaenge-max"></a>
### BLOCKLAENGE_MAX

maximale Blocklaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| BLOCKLAENGE_MAX_WERT | int | Blocklaenge fuer Telegramm |

<a id="job-daten-referenz"></a>
### DATEN_REFERENZ

Job DATEN-Referenz

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| DATEN_REF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| DATEN_REF_PROJEKT | string | Projektkennzeichnung |
| DATEN_REF_PROGRAMM_STAND | string | Programmstand |
| DATEN_REF_DATENSATZ | string | Datensatzkennung |
| DATEN_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-hw-referenz"></a>
### HW_REFERENZ

Job HW-Referenz

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| HW_REF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| HW_REF_PROJEKT | string | Projektkennzeichnung |
| HW_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-seed-key"></a>
### SEED_KEY

Schutzmechanismus SEED_KEY

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SEED_KEY | binary | Rueckgabewert Status |
| Z_ZAHL | int | Zufallszahl |

<a id="job-ansteuerung-vorbereiten"></a>
### ANSTEUERUNG_VORBEREITEN

Vorbereiten STEUERN_STELLGLIED, (Zeit-Zaehler auf null setzen) Achtung: Fuer Anlasserfreigabe, Hydropumpe, Stoeranzeige und Shiftlock muss dieser Job vorab gesendet werden! (Steuergeraete-Timeout: 10s!) Wird die Diagnose zum nachtriggern des SG-Timeouts aufrechterhalten, so bleibt die Ansteuerung max. 60s erhalten. Diese Groessen werden ueber INAKTIV ausgeschaltet. Fuer ansteuerbare Groessen siehe immer aktuelles Lastenheft!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-steuern-stellglied"></a>
### STEUERN_STELLGLIED

Ansteuern der Stellglieder

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STELLGL | string | Anzusteuerndes Stellglied Argument siehe: table STELLGLIEDER  STELLGLIED aus Spalte: STELLGLIED Achtung: Fuer Anlasserfreigabe, Hydropumpe, Stoeranzeige und Shiftlock muss vorab ANSTEUERUNG_VORBEREITEN gesendet werden! Diese Groessen werden ueber INAKTIV ausgeschaltet. Fuer ansteuerbare Groessen siehe immer aktuelles Lastenheft! --ACHTUNG------------------------------------------------------------------ Hydropumpe schaltet nicht automatisch ab! Bei 100 bar oeffnet das Ueberdruckventil --Pumpe wird vorgeschaedigt, wenn mehrfach ueber Ventil abgeblasen wird.--- Wird Diagnose aufrechterhalten, wird die Pumpe maximal 60 sek. angesteuert!  (Steuergeraete-Timeout: 10s!)  --Fuer Soll-Ist-Vergleich z.B. bei MAGNETVENTIL_GANG_VOR------------------------ muss Job mehrfach angestossen werden, um endgueltige Position auszugeben (Z.B. einmaliges ausfuehren gibt nur momentane Pos. beim Einregeln zurueck) (Staendiges anstossen ist natuerlich auch moeglich.) (Sollposition=Adaptionswert) |
| STEUERART1 | string | Argument Steuerungsart: POSITIONSVORGABE STROMVORGABE INAKTIV AKTIV |
| STEUERART2 | int | Argument Steuerungsart: (dezimal eingeben) bei KOMBIANZEIGE_KOMFORTINDEX: 1-6 bei GANGANZEIGE_WAHLHEBEL: GANGANZEIGE: 0-9 WAHLHEBEL: 16,32,48,64,80,96,112,128,144,160,176,240 Fuer alle anderen ansteuerbare Groessen siehe immer aktuelles Lastenheft! (unter Ansteuerbyte 2) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_ANSTEUERUNG | int | Ansteuerergebnis 0 : Stellglied wird ordnungsgemaess angesteuert 1 : Ansteuerbedingungen nicht erfuellt |
| INFO_STATUS_BYTE | int | Infobyte (Ergebnisse der Ansteuerungen [Messwerte]) Infobyte -&gt;  Byte 4 (Lastenheft) |
| STAT_INFO_STATUS_WERT | real | Messwert des Infobyte (mit Quantisierung falls notwendig) bei Magnetventil: Kupplung, Gasse (Waehlwinkel), Gang (Schaltwegvor) Gang rueck (Schaltweg rueck) und Hydropumpe Bei allen anderen Ansteuerungen erfolgt kein Ausgabe |
| STAT_INFO_STATUS_EINH | string | Einheit des Infobyte, falls vorhanden Bei Magnetventil erfolgt Einheit abhaengig von gewaehlter Ansteuerung (mA oder Ink) |

<a id="job-testprg-stop"></a>
### TESTPRG_STOP

Beenden eines laufenden Testprogrammes Muss VOR TESTPRG_STARTEN geschickt werden! (Steuergeraete-Timeout: 10s!)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-testprg-starten"></a>
### TESTPRG_STARTEN

Testprogramm starten Hinweis: Zuvor TESTPRG_STOP schicken!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TESTPRG_NR | int | Argument: siehe: table Testprg  TESTPRG_NR TESTPRG_NAME aus Spalte: TESTPRG_NR |
| AUSWAHLBYTE | int | Argument: Nur fuer (Testprg:0x0A hex) bel. Gang einlegen: 0 = Neutral, 1-6 = Gang 1-6, 7 = Rueckwaertsgang Alle anderen Testprg benoetigen kein Auswahlbyte Siehe Lastenheft Spalte: -Auswahlbyte- (ob vorhanden) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| TEST_STATUS_BYTE | int | Status Testprogramm kann Wert 0, 1, 2 oder 3 annehmen siehe table StatTestTexte  STB TEST_STATUS_TEXT  HINWEIS: Job muss kontinuierlich angestossen werden, um z.B. den aktuellen Status beim Getriebe adaptieren zu erhalten. Job solange anstossen, bis dieses Result ungleich 1 liefert! (Steuergeraete-Timeout: 10s!) |
| TEST_STATUS | string | Status Testprogramm als Text kann Wert 0, 1, 2 oder 3 annehmen siehe table StatTestTexte  STB TEST_STATUS_TEXT |
| INFO_STATUS_BYTE | int | Infobyte 1 (Zustaende und Fehlermeldungen) Infobyte 1 -&gt; Byte 5 (Lastenheft) |
| INFO_STATUS | string | Infobyte 1 (Zustaende und Fehlermeldungen als Text) |
| INFO_STATUS_BYTE2 | int | Infobyte 2 (Ergebnisse der Testprogramme [Messwerte]) Infobyte 2 -&gt;  Byte 6 (Lastenheft) |
| STAT_INFO_STATUS2_WERT | real | Messwert des Infobyte 2 mit Quantisierung fuer TESTPRG=0x04/Speichervorspanndruck ermitteln bei allen anderen Ausgabe wie INFO_STATUS_BYTE2  Hinweis zu Speichervorspanndruck: Im Neuzustand   : Soll laut SACHS nicht gemessen werden, da kein Aussage moeglich. Werkstattbereich: 29-41 bar |
| STAT_INFO_STATUS2_EINH | string | Einheit des Infobyte 2, falls vorhanden Z.Z. nur Speichervorspanndruck |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-codierdaten-lesen"></a>
### CODIERDATEN_LESEN

Codierdaten lesen Kontrollbyte (0x08)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_ROLLENBETRIEB_AKTIV | int | Status Rollenbetrieb Nur fuer M-Gmbh (Nur Hinterachse in Rolle fuer Leistungspruefstand) Hinweis: Schaltet sich bei v=35 km/h wieder ab 0=inaktiv, 1=aktiv |
| STAT_RADABRISS_ABSCHALTUNG_AKTIV | int | Nur fuer Linie (um Geberrad einzulernen / DME) Status Radabrissfunktionsabschaltung aktiv Wieder Einschalten (Normalzustand) über Codierdaten schreiben oder Zuendung aus/ein 0=inaktiv, 1=aktiv |
| STAT_HA_CODE | int | Hinterachsuebersetzung 1..16 |
| STAT_HA_CODE_TEXT | string | Hinterachsuebersetzung 1..16 als Uebersetzungsverhaeltnis 1    = Standard: 1 : 3,64 2-16 = nicht definiert |
| TELEGRAMM_ANF0 | binary | Anforderungstelegramm allg. Codierdaten |
| TELEGRAMM_ANT0 | binary | Antworttelegramm allg. Codierdaten |
| TELEGRAMM_ANF1 | binary | Anforderungstelegramm Hinterachsuebersetzung |
| TELEGRAMM_ANT1 | binary | Antworttelegramm Hinterachsuebersetzung |

<a id="job-codierdaten-schreiben"></a>
### CODIERDATEN_SCHREIBEN

Codierung schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERUNG | string | Codierdaten fuer Auswahl: Argument: ROLLENBETRIEB oder    : RADABRISS  Rollenbetrieb (Nur Hinterachse in Rolle fuer Motorpruefstand) Hinweis: Schaltet sich bei v=35 km/h wieder ab Radabrissfunktionsabschaltung Bei Adaption des Geberrades (DME) in der Line kann es zum Radabriss kommen. Deshalb abschalten |
| AKTIVIERUNG | int | Argument: 0=inaktiv 1=aktiv |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |

<a id="job-getriebedaten-lesen"></a>
### GETRIEBEDATEN_LESEN

Abgleichwerte lesen (Kontrollbyte 0x40)  Getriebedaten lesen ohne Argument fuer VS-21 (vgl. ADAPTIONSWERTE_LESEN)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| HEX_GETRIEBEDATEN | binary | Getriebedaten als Hexdump |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-adaptionswerte-lesen"></a>
### ADAPTIONSWERTE_LESEN

Adaptionswerte lesen Abgleichwerte lesen (Kontrollbyte 0x40)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADAPTION_LESEN | int | Adaptionswerte Kupplung lesen, Argument: 0 Adaptionswerte Getriebe lesen, Argument: 1 Getriebedaten lesen,           Argument: 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Inhalt der Speicherzellen |
| KUPPL_SCHLEIF_PKT_WERT | unsigned int | Kupplungsschleifpunkt (GW) ohne Quantisierung/Umrechnung |
| KUPPL_SCHLEIF_PKT_INK_WERT | unsigned int | Kupplungsschleifpunkt (GW) als (Ink)rement mit Quantisierung/Umrechnung ---ACHTUNG------------------------------------ ---Wert nur bei erfolgreicher----------------- ---Kupplungsschleifpunkt-Adaption gueltig!!--- ---------------------------------------------- Min.: 72, Default: 97 Ink, Max.: 227 |
| I_NULL_VENT_KUPPL_WERT | unsigned int | Nullstrom Kupplungsventil Min.: 800, Default: 1002 mA, Max.: 1200 |
| UEBERDECKUNG_VENT_KUPPL_WERT | unsigned int | Ventilueberdeckung Kupplung Min.: 0, Default: 0 mA, Max.: 150 |
| POS_EINKUP_WERT | unsigned int | Einkuppelstellung (EK) Min.: 640, Default: 830 Ink, Max.: 1002 Hinweis: Differenz AK zu EK ist min.: 430 Ink, max.: 590 |
| POS_AUSKUP_WERT | unsigned int | Auskuppelstellung (AK) Min.: 146, Default: 400 Ink, Max.: 654 Hinweis: Differenz AK zu EK ist min. 430 Ink, max.590 |
| DIFF_V_ACHS_WERT | real | Geschwindigkeitsdifferenz der Achsen Min.: -15,875, Default: 0 km/h Max.: 15,875 |
| ZAHL_KUPPL_UEBERLAST_WERT | unsigned int | Anzahl der Kupplungsueberlastungen Min.: 0, Default: 0, Max.: 255 |
| M_KUPPL_MAX_WERT | unsigned int | max. uebertragbares Kupplungsmoment Min.: 1, Default: 700 Nm, Max.: 1020 Immer: 700 Nm |
| ADAPT_P0_WERT | unsigned int | Adaptionswert Kupplungslageregler P0 Min.: 0, Default: 50, Max.: 255 |
| ADAPT_P1_WERT | unsigned int | Adaptionswert Kupplungslageregler P1 Min.: 0, Default: 80, Max.: 255 |
| ADAPT_P2_WERT | unsigned int | Adaptionswert Kupplungslageregler P2 Min.: 0, Default: 100, Max.: 255 |
| ADAPT_P3_WERT | unsigned int | Adaptionswert Kupplungslageregler P3 Min.: 0, Default: 100, Max.: 255 |
| ADAPT_P4_WERT | unsigned int | Adaptionswert Kupplungslageregler P4 Min.: 0, Default: 80, Max.: 255 |
| ADAPT_P5_WERT | unsigned int | Adaptionswert Kupplungslageregler P5 Min.: 0, Default: 50, Max.: 255 |
| ADAPT_K1_WERT | unsigned int | Adaptionswert Kupplungskennlinie K1 Min.: 17, Default: 52, Max.: 114 |
| ADAPT_K2_WERT | unsigned int | Adaptionswert Kupplungskennlinie K2 Min.: 34, Default: 79, Max.: 182 |
| ADAPT_K3_WERT | unsigned int | Adaptionswert Kupplungskennlinie K3 Min.: 51, Default: 96, Max.: 229 |
| ADAPT_K4_WERT | unsigned int | Adaptionswert Kupplungskennlinie K4 Min.: 68, Default: 110, Max.: 244 |
| ADAPT_K5_WERT | unsigned int | Adaptionswert Kupplungskennlinie K5 Min.: 85, Default: 124, Max.: 246 |
| ADAPT_K6_WERT | unsigned int | Adaptionswert Kupplungskennlinie K6 Min.: 102, Default: 138, Max.: 248 |
| ADAPT_K7_WERT | unsigned int | Adaptionswert Kupplungskennlinie K7 Min.: 119, Default: 152, Max.: 249 |
| ADAPT_K8_WERT | unsigned int | Adaptionswert Kupplungskennlinie K8 Min.: 136, Default: 165, Max.: 250 |
| ADAPT_K9_WERT | unsigned int | Adaptionswert Kupplungskennlinie K9 Min.: 153, Default: 178, Max.: 251 |
| ADAPT_K10_WERT | unsigned int | Adaptionswert Kupplungskennlinie K10 Min.: 170, Default: 191, Max.: 252 |
| ADAPT_SMIN_WERT | unsigned int | Adaptionswert Nullstromkennlinie smin Min.: 0, Default: 0 mA, Max.: 65535 |
| ADAPT_SMAX_WERT | unsigned int | Adaptionswert Nullstromkennlinie smax Min.: 0, Default: 0 mA, Max.: 65535 |
| ADAPT_IMIN_WERT | unsigned int | Adaptionswert Nullstromkennlinie imin Min.: 0, Default: 0 mA, Max.: 65535 |
| ADAPT_IMAX_WERT | unsigned int | Adaptionswert Nullstromkennlinie imax Min.: 0, Default: 0 mA, Max.: 65535 |
| NULLPUNKT_KUPPL_POS_WERT | int | Nullpunkt der Kupplungsposition Min.: -10000, Default: -5600 Ink, Max.: -2000 |
| KUPPL_SCHLEIF_PKT_EINH | string | Einheit: keine |
| KUPPL_SCHLEIF_PKT_INK_EINH | string | Einheit: (Ink)remente |
| I_NULL_VENT_KUPPL_EINH | string | Einheit |
| UEBERDECKUNG_VENT_KUPPL_EINH | string | Einheit |
| POS_EINKUP_EINH | string | Einheit |
| POS_AUSKUP_EINH | string | Einheit |
| DIFF_V_ACHS_EINH | string | Einheit |
| ZAHL_KUPPL_UEBERLAST_EINH | string | Einheit |
| M_KUPPL_MAX_EINH | string | Einheit |
| ADAPT_P0_EINH | string | Einheit |
| ADAPT_P1_EINH | string | Einheit |
| ADAPT_P2_EINH | string | Einheit |
| ADAPT_P3_EINH | string | Einheit |
| ADAPT_P4_EINH | string | Einheit |
| ADAPT_P5_EINH | string | Einheit |
| ADAPT_K1_EINH | string | Einheit |
| ADAPT_K2_EINH | string | Einheit |
| ADAPT_K3_EINH | string | Einheit |
| ADAPT_K4_EINH | string | Einheit |
| ADAPT_K5_EINH | string | Einheit |
| ADAPT_K6_EINH | string | Einheit |
| ADAPT_K7_EINH | string | Einheit |
| ADAPT_K8_EINH | string | Einheit |
| ADAPT_K9_EINH | string | Einheit |
| ADAPT_K10_EINH | string | Einheit |
| ADAPT_SMIN_EINH | string | Einheit |
| ADAPT_SMAX_EINH | string | Einheit |
| ADAPT_IMIN_EINH | string | Einheit |
| ADAPT_IMAX_EINH | string | Einheit |
| NULLPUNKT_KUPPL_POS_EINH | string | Einheit |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |
| OFF_A_LONG_WERT | real | Offset Laengsbeschleunigungssensor Wert Default: 1800 mV, min: 1500 mV, max: 2100 mV |
| OFF_I_WW_WERT | unsigned int | Offsetstrom Waehlwinkel, Wert: unsigned 16 Bit Default: 1000 mA, min: 800 mA, max: 1200 mA |
| OFF_WWSPUR_1ZU2_WERT | int | Offsetstrom Waehlwinkelspur 1 zu Waehlwinkelspur 2 Default: 0 (Ink)remente, min: -180 Ink, max: 180 Ink |
| KORR_SW_EVEN_WERT | int | Korrekturfaktor SW Ende gerade, Wert: signed 8 Bit Default: 0 (Ink)remente |
| KORR_SW_ODD_WERT | int | Korrekturfaktor SW Ende ungerade, Wert: signed 8 Bit |
| KORR_WW_POS_WERT | int | Positiver Korrekturfaktor WW Regler, Wert: signed 8 Bit Default: 128  [--] |
| KORR_WW_NEG_WERT | int | Negativer Korrekturfaktor WW Regler, Wert: signed 8 Bit Default: 128 [--] |
| ANSCHLAG_SW_EVEN_WERT | int | Schaltweganschlag gerade Gaenge, Wert: signed 16 Bit Default: 207 (Ink)remente |
| ANSCHLAG_SW_ODD_WERT | int | Schaltweganschlag ungerade Gaenge, Wert: signed 16 Bit Default: 821 (Ink)remente |
| POS_SW_N_WERT | int | Schaltwegposition Neutral, Wert: signed 16 Bit Default: 500 (Ink)remente |
| WW_GASSE_1_2_WERT | int | Waehlwinkel Gasse 1/2, Wert: signed 16 Bit Default: 465 (Ink)remente |
| WW_GASSE_3_4_WERT | int | Waehlwinkel Gasse 3/4, Wert: signed 16 Bit Default: 580 (Ink)remente |
| WW_GASSE_5_6_WERT | int | Waehlwinkel Gasse 5/6, Wert: signed 16 Bit Default: 725 (Ink)remente |
| WW_GASSE_R_WERT | int | Waehlwinkel Gasse R, Wert: signed 16 Bit Default: 245 (Ink)remente |
| SW_GANG1_ROH1_WERT | int | Schaltweg 1.Gang Rohwert 1, Wert: signed 16 Bit |
| SW_GANG2_ROH1_WERT | int | Schaltweg 2.Gang Rohwert 1, Wert: signed 16 Bit |
| SW_GANG3_ROH1_WERT | int | Schaltweg 3.Gang Rohwert 1, Wert: signed 16 Bit |
| SW_GANG4_ROH1_WERT | int | Schaltweg 4.Gang Rohwert 1, Wert: signed 16 Bit |
| SW_GANG5_ROH1_WERT | int | Schaltweg 5.Gang Rohwert 1, Wert: signed 16 Bit |
| SW_GANG6_ROH1_WERT | int | Schaltweg 6.Gang Rohwert 1, Wert: signed 16 Bit |
| SW_GANGR_ROH1_WERT | int | Schaltweg Rueckwaertsgang Rohwert 1, Wert: signed 16 Bit |
| WW_TOUCH_R_GANG1_ROH1_WERT | int | Waehlwinkelanschlag rechts 1.Gang Rohwert 1, Wert: signed 16 Bit |
| WW_TOUCH_L_GANG1_ROH1_WERT | int | Waehlwinkelanschlag links 1.Gang Rohwert 1, Wert: signed 16 Bit |
| WW_TOUCH_R_GANG2_ROH1_WERT | int | Waehlwinkelanschlag rechts 2.Gang Rohwert 1, Wert: signed 16 Bit |
| WW_TOUCH_L_GANG2_ROH1_WERT | int | Waehlwinkelanschlag links 2.Gang Rohwert 1, Wert: signed 16 Bit |
| WW_TOUCH_R_GANG3_ROH1_WERT | int | Waehlwinkelanschlag rechts 3.Gang Rohwert 1, Wert: signed 16 Bit |
| WW_TOUCH_L_GANG3_ROH1_WERT | int | Waehlwinkelanschlag links 3.Gang Rohwert 1, Wert: signed 16 Bit |
| WW_TOUCH_R_GANG4_ROH1_WERT | int | Waehlwinkelanschlag rechts 4.Gang Rohwert 1, Wert: signed 16 Bit |
| WW_TOUCH_L_GANG4_ROH1_WERT | int | Waehlwinkelanschlag links 4.Gang Rohwert 1, Wert: signed 16 Bit |
| WW_TOUCH_R_GANG5_ROH1_WERT | int | Waehlwinkelanschlag rechts 5.Gang Rohwert 1, Wert: signed 16 Bit |
| WW_TOUCH_L_GANG5_ROH1_WERT | int | Waehlwinkelanschlag links 5.Gang Rohwert 1, Wert: signed 16 Bit |
| WW_TOUCH_R_GANG6_ROH1_WERT | int | Waehlwinkelanschlag rechts 6.Gang Rohwert 1, Wert: signed 16 Bit |
| WW_TOUCH_L_GANG6_ROH1_WERT | int | Waehlwinkelanschlag links 6.Gang Rohwert 1, Wert: signed 16 Bit |
| WW_TOUCH_R_GANGR_ROH1_WERT | int | Waehlwinkelanschlag rechts Rueckwaertsgang Rohwert 1, Wert: signed 16 Bit |
| WW_TOUCH_L_GANGR_ROH1_WERT | int | Waehlwinkelanschlag links Rueckwaertsgang Rohwert 1, Wert: signed 16 Bit |
| SW_GANG1_ROH2_WERT | int | Schaltweg 1.Gang Rohwert 2, Wert: signed 16 Bit |
| SW_GANG2_ROH2_WERT | int | Schaltweg 2.Gang Rohwert 2, Wert: signed 16 Bit |
| SW_GANG3_ROH2_WERT | int | Schaltweg 3.Gang Rohwert 2, Wert: signed 16 Bit |
| SW_GANG4_ROH2_WERT | int | Schaltweg 4.Gang Rohwert 2, Wert: signed 16 Bit |
| SW_GANG5_ROH2_WERT | int | Schaltweg 5.Gang Rohwert 2, Wert: signed 16 Bit |
| SW_GANG6_ROH2_WERT | int | Schaltweg 6.Gang Rohwert 2, Wert: signed 16 Bit |
| SW_GANGR_ROH2_WERT | int | Schaltweg Rueckwaertsgang Rohwert 2, Wert: signed 16 Bit |
| WW_TOUCH_R_GANG1_ROH2_WERT | int | Waehlwinkelanschlag rechts 1.Gang Rohwert 2, Wert: signed 16 Bit |
| WW_TOUCH_L_GANG1_ROH2_WERT | int | Waehlwinkelanschlag links 1.Gang Rohwert 2, Wert: signed 16 Bit |
| WW_TOUCH_R_GANG2_ROH2_WERT | int | Waehlwinkelanschlag rechts 2.Gang Rohwert 2, Wert: signed 16 Bit |
| WW_TOUCH_L_GANG2_ROH2_WERT | int | Waehlwinkelanschlag links 2.Gang Rohwert 2, Wert: signed 16 Bit |
| WW_TOUCH_R_GANG3_ROH2_WERT | int | Waehlwinkelanschlag rechts 3.Gang Rohwert 2, Wert: signed 16 Bit |
| WW_TOUCH_L_GANG3_ROH2_WERT | int | Waehlwinkelanschlag links 3.Gang Rohwert 2, Wert: signed 16 Bit |
| WW_TOUCH_R_GANG4_ROH2_WERT | int | Waehlwinkelanschlag rechts 4.Gang Rohwert 2, Wert: signed 16 Bit |
| WW_TOUCH_L_GANG4_ROH2_WERT | int | Waehlwinkelanschlag links 4.Gang Rohwert 2, Wert: signed 16 Bit |
| WW_TOUCH_R_GANG5_ROH2_WERT | int | Waehlwinkelanschlag rechts 5.Gang Rohwert 2, Wert: signed 16 Bit |
| WW_TOUCH_L_GANG5_ROH2_WERT | int | Waehlwinkelanschlag links 5.Gang Rohwert 2, Wert: signed 16 Bit |
| WW_TOUCH_R_GANG6_ROH2_WERT | int | Waehlwinkelanschlag rechts 6.Gang Rohwert 2, Wert: signed 16 Bit |
| WW_TOUCH_L_GANG6_ROH2_WERT | int | Waehlwinkelanschlag links 6.Gang Rohwert 2, Wert: signed 16 Bit |
| WW_TOUCH_R_GANGR_ROH2_WERT | int | Waehlwinkelanschlag rechts Rueckwaertsgang Rohwert 2, Wert: signed 16 Bit |
| WW_TOUCH_L_GANGR_ROH2_WERT | int | Waehlwinkelanschlag links Rueckwaertsgang Rohwert 2, Wert: signed 16 Bit |
| T_KL11_EK_ADAPT_1_WERT | unsigned int | Zeiten KL11 EK-Adaption 1.Gang, Wert: unsigned 16 Bit |
| T_KL11_EK_ADAPT_2_WERT | unsigned int | Zeiten KL11 EK-Adaption 2.Gang, Wert: unsigned 16 Bit |
| T_KL11_EK_ADAPT_3_WERT | unsigned int | Zeiten KL11 EK-Adaption 3.Gang, Wert: unsigned 16 Bit |
| T_KL11_EK_ADAPT_4_WERT | unsigned int | Zeiten KL11 EK-Adaption 4.Gang, Wert: unsigned 16 Bit |
| T_KL11_EK_ADAPT_5_WERT | unsigned int | Zeiten KL11 EK-Adaption 5.Gang, Wert: unsigned 16 Bit |
| T_KL11_EK_ADAPT_6_WERT | unsigned int | Zeiten KL11 EK-Adaption 6.Gang, Wert: unsigned 16 Bit |
| T_KL12_EK_ADAPT_1_WERT | unsigned int | Zeiten KL12 EK-Adaption 1.Gang, Wert: unsigned 16 Bit |
| T_KL12_EK_ADAPT_2_WERT | unsigned int | Zeiten KL12 EK-Adaption 2.Gang, Wert: unsigned 16 Bit |
| T_KL12_EK_ADAPT_3_WERT | unsigned int | Zeiten KL12 EK-Adaption 3.Gang, Wert: unsigned 16 Bit |
| T_KL12_EK_ADAPT_4_WERT | unsigned int | Zeiten KL12 EK-Adaption 4.Gang, Wert: unsigned 16 Bit |
| T_KL12_EK_ADAPT_5_WERT | unsigned int | Zeiten KL12 EK-Adaption 5.Gang, Wert: unsigned 16 Bit |
| T_KL12_EK_ADAPT_6_WERT | unsigned int | Zeiten KL12 EK-Adaption 6.Gang, Wert: unsigned 16 Bit |
| OFF_SCHALTWEGSPUR_1_ZU_2_WERT | int | Offset Schaltwegspur 1 zu Schaltwegspur 2, Wert: signed 16 Bit Default: 0 Ink, min: -180 Ink, max: 180 Ink |
| ANZ_RENNSTART_WERT | int | Anzahl Rennstarts |
| ANZ_SCHALT_FMAX_1_WERT | unsigned int | Anzahl Schaltungen mit maximaler Schaltkraft Gang 1 |
| ANZ_SCHALT_FMAX_2_WERT | unsigned int | Anzahl Schaltungen mit maximaler Schaltkraft Gang 2 |
| ANZ_SCHALT_FMAX_3_WERT | unsigned int | Anzahl Schaltungen mit maximaler Schaltkraft Gang 3 |
| ANZ_SCHALT_FMAX_4_WERT | unsigned int | Anzahl Schaltungen mit maximaler Schaltkraft Gang 4 |
| ANZ_SCHALT_FMAX_5_WERT | unsigned int | Anzahl Schaltungen mit maximaler Schaltkraft Gang 5 |
| ANZ_SCHALT_FMAX_6_WERT | unsigned int | Anzahl Schaltungen mit maximaler Schaltkraft Gang 6 |
| OFF_A_LONG_EINH | string | Offset Laengsbeschleunigungssensor Einheit |
| OFF_I_WW_EINH | string | Offsetstrom Waehlwinkel Einheit |
| OFF_WWSPUR_1ZU2_EINH | string | Offsetstrom Waehlwinkelspur 1 zu Waehlwinkelspur 2 Einheit: (Ink)remente |
| KORR_SW_EVEN_EINH | string | Korrekturfaktor SW Ende gerade Einheit Default: 0 (Ink)remente |
| KORR_SW_ODD_EINH | string | Korrekturfaktor SW Ende ungerade Einheit |
| KORR_WW_POS_EINH | string | Einheit |
| KORR_WW_NEG_EINH | string | Einheit |
| ANSCHLAG_SW_EVEN_EINH | string | Einheit |
| ANSCHLAG_SW_ODD_EINH | string | Einheit |
| POS_SW_N_EINH | string | Einheit |
| WW_GASSE_1_2_EINH | string | Einheit |
| WW_GASSE_3_4_EINH | string | Einheit |
| WW_GASSE_5_6_EINH | string | Einheit |
| WW_GASSE_R_EINH | string | Einheit |
| SW_GANG1_ROH1_EINH | string | Einheit |
| SW_GANG2_ROH1_EINH | string | Einheit |
| SW_GANG3_ROH1_EINH | string | Einheit |
| SW_GANG4_ROH1_EINH | string | Einheit |
| SW_GANG5_ROH1_EINH | string | Einheit |
| SW_GANG6_ROH1_EINH | string | Einheit |
| SW_GANGR_ROH1_EINH | string | Einheit |
| WW_TOUCH_R_GANG1_ROH1_EINH | string | Einheit |
| WW_TOUCH_L_GANG1_ROH1_EINH | string | Einheit |
| WW_TOUCH_R_GANG2_ROH1_EINH | string | Einheit |
| WW_TOUCH_L_GANG2_ROH1_EINH | string | Einheit |
| WW_TOUCH_R_GANG3_ROH1_EINH | string | Einheit |
| WW_TOUCH_L_GANG3_ROH1_EINH | string | Einheit |
| WW_TOUCH_R_GANG4_ROH1_EINH | string | Einheit |
| WW_TOUCH_L_GANG4_ROH1_EINH | string | Einheit |
| WW_TOUCH_R_GANG5_ROH1_EINH | string | Einheit |
| WW_TOUCH_L_GANG5_ROH1_EINH | string | Einheit |
| WW_TOUCH_R_GANG6_ROH1_EINH | string | Einheit |
| WW_TOUCH_L_GANG6_ROH1_EINH | string | Einheit |
| WW_TOUCH_R_GANGR_ROH1_EINH | string | Einheit |
| WW_TOUCH_L_GANGR_ROH1_EINH | string | Einheit |
| SW_GANG1_ROH2_EINH | string | Einheit |
| SW_GANG2_ROH2_EINH | string | Einheit |
| SW_GANG3_ROH2_EINH | string | Einheit |
| SW_GANG4_ROH2_EINH | string | Einheit |
| SW_GANG5_ROH2_EINH | string | Einheit |
| SW_GANG6_ROH2_EINH | string | Einheit |
| SW_GANGR_ROH2_EINH | string | Einheit |
| WW_TOUCH_R_GANG1_ROH2_EINH | string | Einheit |
| WW_TOUCH_L_GANG1_ROH2_EINH | string | Einheit |
| WW_TOUCH_R_GANG2_ROH2_EINH | string | Einheit |
| WW_TOUCH_L_GANG2_ROH2_EINH | string | Einheit |
| WW_TOUCH_R_GANG3_ROH2_EINH | string | Einheit |
| WW_TOUCH_L_GANG3_ROH2_EINH | string | Einheit |
| WW_TOUCH_R_GANG4_ROH2_EINH | string | Einheit |
| WW_TOUCH_L_GANG4_ROH2_EINH | string | Einheit |
| WW_TOUCH_R_GANG5_ROH2_EINH | string | Einheit |
| WW_TOUCH_L_GANG5_ROH2_EINH | string | Einheit |
| WW_TOUCH_R_GANG6_ROH2_EINH | string | Einheit |
| WW_TOUCH_L_GANG6_ROH2_EINH | string | Einheit |
| WW_TOUCH_R_GANGR_ROH2_EINH | string | Einheit |
| WW_TOUCH_L_GANGR_ROH2_EINH | string | Einheit |
| T_KL11_EK_ADAPT_1_EINH | string | Einheit |
| T_KL11_EK_ADAPT_2_EINH | string | Einheit |
| T_KL11_EK_ADAPT_3_EINH | string | Einheit |
| T_KL11_EK_ADAPT_4_EINH | string | Einheit |
| T_KL11_EK_ADAPT_5_EINH | string | Einheit |
| T_KL11_EK_ADAPT_6_EINH | string | Einheit |
| T_KL12_EK_ADAPT_1_EINH | string | Einheit |
| T_KL12_EK_ADAPT_2_EINH | string | Einheit |
| T_KL12_EK_ADAPT_3_EINH | string | Einheit |
| T_KL12_EK_ADAPT_4_EINH | string | Einheit |
| T_KL12_EK_ADAPT_5_EINH | string | Einheit |
| T_KL12_EK_ADAPT_6_EINH | string | Einheit |
| OFF_SCHALTWEGSPUR_1_ZU_2_EINH | string | Einheit |
| ANZ_RENNSTART_EINH | string | Einheit |
| ANZ_SCHALT_FMAX_1_EINH | string | Einheit |
| ANZ_SCHALT_FMAX_2_EINH | string | Einheit |
| ANZ_SCHALT_FMAX_3_EINH | string | Einheit |
| ANZ_SCHALT_FMAX_4_EINH | string | Einheit |
| ANZ_SCHALT_FMAX_5_EINH | string | Einheit |
| ANZ_SCHALT_FMAX_6_EINH | string | Einheit |

<a id="job-adaptionswerte-loeschen"></a>
### ADAPTIONSWERTE_LOESCHEN

Adaptionswerte loeschen (Kontrollbyte 0x43)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADAPTIONSWERT_LOESCHEN | int | Kupplungskennlinie loeschen, Argument: 0 Getriebedaten loeschen,      Argument: 1 Hinweis: Kupplungswerte werden auf Defaultwerte zurueckgesetzt Getriebedaten werden auf null gesetzt. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-status-hardware-stati-lesen"></a>
### STATUS_HARDWARE_STATI_LESEN

Hardwarestati SMG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_SHIFT_LOCK_EIN | int | Shift-Lock 0 oder 1 |
| STAT_SCHALTER_RUECK_EIN | int | Rueckfahrlichtschalter 0 oder 1 Lastenheft Eigendiagnose Stand 5, S.11: nicht im Steuergeraet verbaut!! |
| STAT_ANLASSER_EIN | int | Relais Anlasser 0 oder 1 |
| STAT_HYD_PUMP_EIN | int | Hydraulikpumpe 0 oder 1 |
| STAT_RESERVE_OUT_EIN | int | Reserve Output 0 oder 1 |
| STAT_TREIBER1_NOTANSTEUERUNG_EIN | int | Trouble Shot Down Driver 1 (kommt lowaktiv vom SG, in SGBD invertiert) 0 = aus, 1= ein (lowaktiv!) |
| STAT_TREIBER2_NOTANSTEUERUNG_EIN | int | Trouble Shot Down Driver 2 (kommt lowaktiv vom SG, in SGBD invertiert) 0 = aus, 1= ein |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Status Eingaenge SMG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_MOTORDREHZAHL_WERT | int |  |
| STAT_MOTORDREHZAHL_EINH | string |  |
| STAT_MOTORDREHZAHL_CAN_WERT | int | Motordrehzahl von CAN |
| STAT_MOTORDREHZAHL_CAN_EINH | string | Motordrehzahl von CAN |
| STAT_EINGANGSDREHZAHL_WERT | int | Getriebeeingangsdrehzahl |
| STAT_EINGANGSDREHZAHL_EINH | string | Getriebeeingangsdrehzahl |
| STAT_AUSGANGSDREHZAHL_WERT | int | Getriebeausgangsdrehzahl |
| STAT_AUSGANGSDREHZAHL_EINH | string | Getriebeausgangsdrehzahl |
| STAT_GESCHWINDIGKEIT_WERT | int | Fahrzeuggeschwindigkeit |
| STAT_GESCHWINDIGKEIT_EINH | string | Fahrzeuggeschwindigkeit |
| STAT_RADGESCHWINDIGKEIT_VL_WERT | int |  |
| STAT_RADGESCHWINDIGKEIT_VL_EINH | string |  |
| STAT_RADGESCHWINDIGKEIT_VR_WERT | int |  |
| STAT_RADGESCHWINDIGKEIT_VR_EINH | string |  |
| STAT_RADGESCHWINDIGKEIT_HL_WERT | int |  |
| STAT_RADGESCHWINDIGKEIT_HL_EINH | string |  |
| STAT_RADGESCHWINDIGKEIT_HR_WERT | int |  |
| STAT_RADGESCHWINDIGKEIT_HR_EINH | string |  |
| STAT_PWG_WERT | int | Fahrpedalwert |
| STAT_PWG_EINH | string | Fahrpedalwert |
| STAT_MOTORMOMENT_WERT | int | Motormoment |
| STAT_MOTORMOMENT_EINH | string | Motormoment |
| STAT_MOTORTEMPERATUR_WERT | int | MOTORTEMPERATUR (KUEHLWASSER) |
| STAT_MOTORTEMPERATUR_EINH | string | MOTORTEMPERATUR |
| STAT_HYDRAULIKTEMPERATUR_WERT | int | Hydrauliktemperatur |
| STAT_HYDRAULIKTEMPERATUR_EINH | string | Hydrauliktemperatur |
| STAT_GETRIEBETEMPERATUR_WERT | int | Getriebeoeltemperatur |
| STAT_GETRIEBETEMPERATUR_EINH | string | Getriebeoeltemperatur |
| STAT_UMGEBUNGSTEMPERATUR_WERT | int | Umgebungstemperatur |
| STAT_UMGEBUNGSTEMPERATUR_EINH | string | Umgebungstemperatur |
| STAT_POS_KUP_WERT | unsigned int | Ist-Kupplungsposition HINWEIS: Soll-Ist-Vergleich mit Adaptionswert Ein-Auskuppelstellung, Kupplungsschleifpunkt durchfuehren |
| STAT_POS_KUP_EINH | string | Ist-Kupplungsposition |
| STAT_POS1_GANG_WERT | unsigned int | Schaltwegpostion 1 (Position Gang) |
| STAT_POS1_GANG_EINH | string | Schaltwegpostion 1 (Position Gang) |
| STAT_POS1_GASSE_WERT | unsigned int | Waehlwinkelposition 1 (Position Gasse) |
| STAT_POS1_GASSE_EINH | string | Waehlwinkelposition 1 (Position Gasse) |
| STAT_POS2_GANG_WERT | unsigned int | Schaltwegpostion 2 (Position Gang) |
| STAT_POS2_GANG_EINH | string | Schaltwegpostion 2 (Position Gang) |
| STAT_POS2_GASSE_WERT | unsigned int | Waehlwinkelposition 2 (Position Gasse) |
| STAT_POS2_GASSE_EINH | string | Waehlwinkelposition 2 (Position Gasse) |
| STAT_STROM_KUP_WERT | unsigned int | Iststrom Magnetventil Kupplung |
| STAT_STROM_KUP_EINH | string | Iststrom Magnetventil Kupplung |
| STAT_STROM_WAEHLWINKEL_WERT | unsigned int | Iststrom Magnetventil Waehlwinkel |
| STAT_STROM_WAEHLWINKEL_EINH | string | Iststrom Magnetventil Waehlwinkel |
| STAT_STROM_SCHALTWEG_R_WERT | unsigned int | Iststrom Magnetventil Schaltweg Rueck |
| STAT_STROM_SCHALTWEG_R_EINH | string | Iststrom Magnetventil Schaltweg Rueck |
| STAT_STROM_SCHALTWEG_V_WERT | unsigned int | Iststrom Magnetventil Schaltweg Vor |
| STAT_STROM_SCHALTWEG_V_EINH | string | Iststrom Magnetventil Schaltweg Vor |
| STAT_UBAT_WERT | real | Batteriespannung (KL.30) |
| STAT_UBAT_EINH | string | Batteriespannung (KL.30) |
| STAT_USENSA_WERT | real | Sensorversorgungsspannung A |
| STAT_USENSA_EINH | string | Sensorversorgungsspannung A |
| STAT_USENSB_WERT | real | Sensorversorgungsspannung B |
| STAT_USENSB_EINH | string | Sensorversorgungsspannung B |
| STAT_PHYD_WERT | unsigned int | Hydraulikdruck |
| STAT_PHYD_EINH | string | Hydraulikdruck |
| STAT_AQUER_WERT | real | Querbeschleunigung von CAN |
| STAT_AQUER_EINH | string | Querbeschleunigung von CAN |
| STAT_ALAENGS_WERT | real | Laengsbeschleunigung (vom DSC) |
| STAT_ALAENGS_EINH | string | Laengsbeschleunigung (vom DSC) |
| STAT_LAENGS_G_CAN_WERT | real | Laengsbeschleunigung von CAN |
| STAT_LAENGS_G_CAN_EINH | string | Laengsbeschleunigung von CAN |
| STAT_ALAENGS_ROH_WERT | unsigned int | Laengsbeschleunigung |
| STAT_ALAENGS_ROH_EINH | string | Laengsbeschleunigung-Rohwert |
| STAT_EINGANGSDREHZAHL_ROH_WERT | unsigned int | Getriebeeingangsdrehzahl-Rohwert |
| STAT_EINGANGSDREHZAHL_ROH_EINH | string | Getriebeeingangsdrehzahl-Rohwert |
| STAT_MOTORDREHZAHL_ROH_WERT | unsigned int | Motordrehzahl-Rohwert |
| STAT_MOTORDREHZAHL_ROH_EINH | string | Motordrehzahl-Rohwert |
| STAT_POS_KUP_ROH_WERT | unsigned int | Position Kupplung-Rohwert, Inkrement Unsigned Integer |
| STAT_POS_KUP_ROH_EINH | string | Position Kupplung-Rohwert, Inkrement Unsigned Integer |
| STAT_GETRIEBETEMPERATUR_ROH_WERT | unsigned int | Getriebeoeltemperatur-Rohwert, Inkrement Unsigned Integer |
| STAT_GETRIEBETEMPERATUR_ROH_EINH | string | Getriebeoeltemperatur-Rohwert, Inkrement Unsigned Integer |
| STAT_HYDRAULIKTEMPERATUR_ROH_WERT | unsigned int | Hydrauliktemperatur-Rohwert, Inkrement Unsigned Integer |
| STAT_HYDRAULIKTEMPERATUR_ROH_EINH | string | Hydrauliktemperatur-Rohwert, Inkrement Unsigned Integer |
| STAT_SOLL_STROM_KUP_WERT | unsigned int | Sollstrom Magnetventil Kupplung |
| STAT_SOLL_STROM_KUP_EINH | string | Sollstrom Magnetventil Kupplung |
| STAT_SOLL_STROM_SCHALTWEG_R_WERT | unsigned int | Sollstrom Magnetventil Schaltweg Rueck |
| STAT_SOLL_STROM_SCHALTWEG_R_EINH | string | Sollstrom Magnetventil Schaltweg Rueck |
| STAT_SOLL_STROM_SCHALTWEG_V_WERT | unsigned int | Sollstrom Magnetventil Schaltweg Vor |
| STAT_SOLL_STROM_SCHALTWEG_V_EINH | string | Sollstrom Magnetventil Schaltweg Vor |
| STAT_SOLL_STROM_WAEHLWINKEL_WERT | unsigned int | Sollstrom Magnetventil Waehlwinkel |
| STAT_SOLL_STROM_WAEHLWINKEL_EINH | string | Sollstrom Magnetventil Waehlwinkel |
| STAT_SOLL_POS_KUP_WERT | int | Sollposition Kupplung, Inkrement Ist Reglergroesse, wenig sinnvoll mit anderen Groesse zu vergleichen HINWEIS: Soll-Ist-Vergleich mit Adaptionswert Ein-Auskuppelstellung mit STAT_POS_KUP_WERT durchfuehren |
| STAT_SOLL_POS_KUP_EINH | string | Sollposition Kupplung, Inkrement |
| STAT_SOLL_POS_SCHALTWEG_WERT | int | Sollposition Schaltweg, Inkrement |
| STAT_SOLL_POS_SCHALTWEG_EINH | string | Sollposition Schaltweg, Inkrement |
| STAT_SOLL_POS_WAEHLWINKEL_WERT | int | Sollposition Waehlwinkel, Inkrement |
| STAT_SOLL_POS_WAEHLWINKEL_EINH | string | Sollposition Waehlwinkel, Inkrement |
| STAT_IST_POS_SCHALTWEG_WERT | int | Istposition Schaltweg, Inkrement |
| STAT_IST_POS_SCHALTWEG_EINH | string | Istposition Schaltweg, Inkrement |
| STAT_IST_POS_WAEHLWINKEL_WERT | int | Istposition Waehlwinkel, Inkrement |
| STAT_IST_POS_WAEHLWINKEL_EINH | string | Istposition Waehlwinkel, Inkrement |
| STAT_GESCHWINDIGKEIT_HINTERACHSE_WERT | int | Hinterachsgeschwindigkeit |
| STAT_GESCHWINDIGKEIT_HINTERACHSE_EINH | string | Hinterachsgeschwindigkeit |
| STAT_KILOMETERSTAND_WERT | unsigned int | Kilometerstand ueber CAN |
| STAT_KILOMETERSTAND_EINH | string | Kilometerstand ueber CAN |
| STAT_MOTOROELTEMPERATUR_WERT | int | Motoroeltemperatur ueber CAN |
| STAT_MOTOROELTEMPERATUR_EINH | string | Motoroeltemperatur ueber CAN |
| STAT_PHYD_ROH_WERT | unsigned int | Hydraulikdruck-Rohwert, Inkrement |
| STAT_PHYD_ROH_EINH | string | Hydraulikdruck-Rohwert, Inkrement |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-io-stati-lesen"></a>
### STATUS_IO_STATI_LESEN

Status Eingaenge SMG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_WHS1_EIN | int | Waehlhebel Schalter S1 0 oder 1 |
| STAT_WHS2_EIN | int | Waehlhebel Schalter S2 0 oder 1 |
| STAT_WHE1_EIN | int | Waehlhebel Schalter E1 0 oder 1 |
| STAT_WHE2_EIN | int | Waehlhebel Schalter E2 0 oder 1 |
| STAT_WHN1_EIN | int | Waehlhebel Schalter N1 0 oder 1 |
| STAT_WHN2_EIN | int | Waehlhebel Schalter N2 0 oder 1 |
| STAT_WHR1_EIN | int | Waehlhebel Schalter R1 0 oder 1 |
| STAT_WHR2_EIN | int | Waehlhebel Schalter R2 0 oder 1 |
| STAT_ESTATE_EIN | int | ESTATE=Engine state, Erkennung ob Motor laueft 0=Motordrehzahl &lt; 200 1/min 1=Motordrehzahl &gt; 200 1/min |
| STAT_SPORT_ADD_EIN | int | Komfort-Schalter Sport+ 0 oder 1 |
| STAT_SPORT_SUB_EIN | int | Komfort-Schalter Sport- 0 oder 1 |
| STAT_MOTORHAUBE1_EIN | int | Motorhaubenkontakt 1 (links) 0=auf oder 1=zu |
| STAT_MOTORHAUBE2_EIN | int | Motorhaubenkontakt 2 (rechts) 0=auf oder 1=zu |
| STAT_VA_EIN | int | Verbraucherabschaltung 0 oder 1 |
| STAT_KL50_EIN | int | Zuendung Klemme 50 0 oder 1 |
| STAT_KLR_EIN | int | Zuendung Klemme R 0 oder 1 |
| STAT_KL15_EIN | int | Zuendung Klemme 15 0 oder 1 |
| STAT_FUELLSTAND_VORHANDEN | int | Fuellstand 0 oder 1 Lastenheft Eigendiagnose Stand 5, S.10: nicht im Steuergeraet verbaut!! |
| STAT_LENKRADTASTER_PLUS_AKTIV | int | 0 oder 1 |
| STAT_LENKRADTASTER_MINUS_AKTIV | int | 0 oder 1 |
| STAT_KUPPLUNG_WERT | int | Kupplungsstatus-Rohwert siehe table FUmweltTexte4  WERT UWTEXT |
| STAT_KUPPLUNG_EINH | string | Kupplungsstatus-Rohwert |
| STAT_KUPPLUNG_TEXT | string | Kupplungsstatus siehe table FUmweltTexte4  WERT UWTEXT |
| STAT_ISTGANG_WERT | int | Getriebeuebersetzung: 0,1,2,3,4,5,6,R- Rohwert siehe table FUmweltTexte1  WERT UWTEXT |
| STAT_ISTGANG_EINH | string | Getriebeuebersetzung: 0,1,2,3,4,5,6,R- Rohwert |
| STAT_ISTGANG_TEXT | string | Getriebeuebersetzung: 0,1,2,3,4,5,6,R siehe table FUmweltTexte1  WERT UWTEXT |
| STAT_GETRIEBE_WERT | int | Getriebestatus-Rohwert siehe table FUmweltTexte3  WERT UWTEXT |
| STAT_GETRIEBE_EINH | string | Getriebestatus-Rohwert |
| STAT_GETRIEBE_TEXT | string | Getriebestatus siehe table FUmweltTexte3  WERT UWTEXT |
| STAT_WAEHLHEBELSTELLUNG_WERT | int | Waehlhebelstellung: R,0,A,S,+,-,n.def. -Rohwert siehe table FUmweltTexte5  WERT UWTEXT |
| STAT_WAEHLHEBELSTELLUNG_EINH | string | Waehlhebelstellung: R,0,A,S,+,-,n.def. -Rohwert |
| STAT_WAEHLHEBELSTELLUNG_TEXT | string | Waehlhebelstellung: R,0,A,S,+,-,n.def. als Text siehe table FUmweltTexte5  WERT UWTEXT |
| STAT_FGR_WERT | int | Fahrgeschwingigkeitsregler (FGR) Status-Rohwert |
| STAT_FGR_EINH | string | Fahrgeschwindigkeitsregler (FGR) Status-Rohwert |
| STAT_FGR_TEXT | string | Fahrgeschwindigkeitsregler (FGR) Status |
| STAT_WARM_UP_CYCLE_ERFUELLT | int | Warm Up Cycle erfuellt |
| STAT_TRIP_ERFUELLT | int | Trip erfuellt |
| STAT_DRIVING_CYCLE_ON | int | Driving Cycle erfuellt bzw. begonnen |
| STAT_FREEZE_FRAME_REFERENZ_WERT | int | Freeze Frame-Rohwert wird verwaltet fuer siehe table FREEZE_FRAME_REFERENZ  WERT ANZEIGE_TEXT |
| STAT_FREEZE_FRAME_REFERENZ_EINH | string | Freeze Frame-Rohwert wird verwaltet fuer |
| STAT_FREEZE_FRAME_REFERENZ_TEXT | string | Freeze Frame wird verwaltet fuer siehe table FREEZE_FRAME_REFERENZ  WERT ANZEIGE_TEXT |
| STAT_KICK_DOWN_EIN | int | 0 oder 1 |
| STAT_BREMSLICHTSCHALTER_EIN | int | 0 oder 1 |
| STAT_BREMSLICHTTESTSCHALTER_EIN | int | 0 oder 1 |
| STAT_ANHAENGERBETRIEB_EIN | int | 0 oder 1 |
| STAT_HANDBREMSE_EIN | int | 0 oder 1 |
| STAT_TUER_ZU | int | Tuer 0=auf oder 1=zu |
| STAT_KUPPL_ADAPT_SPERRE_EIN | int | Sperren der Kupplungsadaption 0 oder 1 |
| STAT_GONG_AKTIV | int | 0 oder 1 |
| STAT_OBD_REL_FEHLER_ERFUELLT | int | 0 oder 1 |
| STAT_STOERANZEIGE_SMG_STEUERUNG_EIN | int | 0 oder 1 |
| STAT_SCHALTUNG_AKTIV | int | 0 oder 1 |
| STAT_ANLASSERFREIGABE_AKTIV | int | 0 oder 1 Kupplung und Getriebe geben Anlasserfreigabe an DME |
| STAT_FGR_ABSCHALTEN_AKTIV | int | 0 oder 1 |
| STAT_PROGRAMMINFO_WERT | int | 1. - 6. Programm-Rohwert Muss mit Anzahl der Balken im Kombi uebereinstimmen Wird ueber Taster vor Waehlhebel eingestellt siehe table PROGRAMMINFO  WERT ANZEIGE_TEXT |
| STAT_PROGRAMMINFO_EINH | string | 1. - 6. Programm-Rohwert |
| STAT_PROGRAMMINFO_TEXT | string | 1. - 6. Programm Muss mit Anzahl der Balken im Kombi uebereinstimmen Wird ueber Taster vor Waehlhebel eingestellt siehe table PROGRAMMINFO  WERT ANZEIGE_TEXT |
| STAT_KOMFORTINDEX_WERT | int | Komfortindex-Rohwert 0 - 12 Ausgabe abhängig von Gang und Fahrweise siehe table KOMFORTINDEX  WERT ANZEIGE_TEXT |
| STAT_KOMFORTINDEX_EINH | string | Komfortindex-Rohwert 0 - 12 |
| STAT_KOMFORTINDEX_TEXT | string | Komfortindex 0 - 12 Ausgabe abhängig von Gang und Fahrweise siehe table KOMFORTINDEX  WERT ANZEIGE_TEXT |
| STAT_GANGANZEIGE_WERT | int | Ganganzeige-Rohwert im Kombi siehe table GANGANZEIGE  WERT ANZEIGE_TEXT |
| STAT_GANGANZEIGE_EINH | string | Ganganzeige-Rohwert im Kombi |
| STAT_GANGANZEIGE_TEXT | string | Ganganzeige im Kombi als Text siehe table GANGANZEIGE  WERT ANZEIGE_TEXT |
| STAT_WAEHLHEBELANZEIGE_WERT | int | Waehlhebelanzeige-Rohwert im Kombi siehe table WAEHLHEBELANZEIGE  WERT ANZEIGE_TEXT |
| STAT_WAEHLHEBELANZEIGE_EINH | string | Waehlhebelanzeige-Rohwert im Kombi |
| STAT_WAEHLHEBELANZEIGE_TEXT | string | Waehlhebelanzeige im Kombi siehe table WAEHLHEBELANZEIGE  WERT ANZEIGE_TEXT |
| STAT_FAHRZUSTAND_WERT | int | Modulindex-Rohwert |
| STAT_FAHRZUSTAND_EINH | string | Fahzeugzustand-Rohwert |
| STAT_FAHRZUSTAND_TEXT | string | Fahzeugzustand Text table InfoTexteFahrzeugzustand  IB INFO_TEXT |
| STAT_GET_LOCAL_TRIP_ERREICHT | int | lokaler Trip erreicht oder nicht erreicht |
| STAT_FREEZE_FRAME_GESPEICHERT | int | Freeze Frame speichern oder loeschen |
| STAT_MIL_EIN | int | MIL ein oder aus |
| STAT_MIL_BLINK_EIN | int | MIL blink |
| STAT_LED_WERT | int | Rohwert: keine, 1.LED, 1. und 2. LED siehe table LED  WERT ANZEIGE_TEXT |
| STAT_LED_EINH | string | Rohwert: keine, 1.LED, 1. und 2. LED |
| STAT_LED_TEXT | string | keine, 1.LED, 1. und 2. LED siehe table LED  WERT ANZEIGE_TEXT |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-fahrzeugtester-lesen"></a>
### STATUS_FAHRZEUGTESTER_LESEN

I/O Status lesen (Kontrollbyte 0x0B) Fahrzeugtester   (Auswahlbyte  0x05) Status der Ein- u. Ausgaenge GETRAG und VS21 spezifischer Job (Nicht fuer INPA gedacht.)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_KICK_DOWN_EIN | int | 0 oder 1 |
| STAT_BREMSLICHTSCHALTER_EIN | int | 0 oder 1 |
| STAT_BREMSLICHTTESTSCHALTER_EIN | int | 0 oder 1 |
| STAT_ANHAENGERBETRIEB_EIN | int | 0 oder 1 |
| STAT_HANDBREMSE_EIN | int | 0 oder 1 |
| STAT_TUER_ZU | int | Tuer 0=auf oder 1=zu |
| STAT_KUPPL_ADAPT_SPERRE_EIN | int | Sperren der Kupplungsadaption 0 oder 1 |
| STAT_MOTORDREHZAHL_CAN_WERT | int | Motordrehzahl von CAN |
| STAT_MOTORDREHZAHL_CAN_EINH | string | Motordrehzahl von CAN |
| STAT_EINGANGSDREHZAHL_WERT | int | Getriebeeingangsdrehzahl |
| STAT_EINGANGSDREHZAHL_EINH | string | Getriebeeingangsdrehzahl |
| STAT_AUSGANGSDREHZAHL_WERT | int | Getriebeausgangsdrehzahl |
| STAT_AUSGANGSDREHZAHL_EINH | string | Getriebeausgangsdrehzahl |
| STAT_WAEHLHEBELSTELLUNG_WERT | int | Waehlhebelstellung: R,0,A,S,+,-,n.def. -Rohwert |
| STAT_WAEHLHEBELSTELLUNG_EINH | string | Waehlhebelstellung: R,0,A,S,+,-,n.def. -Rohwert |
| STAT_WAEHLHEBELSTELLUNG_TEXT | string | Waehlhebelstellung: R,0,A,S,+,-,n.def. als Text |
| STAT_WAEHLHEBELANZEIGE_WERT | int | Waehlhebelanzeige-Rohwert im Kombi |
| STAT_WAEHLHEBELANZEIGE_EINH | string | Waehlhebelanzeige-Rohwert im Kombi |
| STAT_WAEHLHEBELANZEIGE_TEXT | string | Waehlhebelanzeige im Kombi |
| STAT_RADGESCHWINDIGKEIT_VL_WERT | int |  |
| STAT_RADGESCHWINDIGKEIT_VL_EINH | string |  |
| STAT_RADGESCHWINDIGKEIT_VR_WERT | int |  |
| STAT_RADGESCHWINDIGKEIT_VR_EINH | string |  |
| STAT_RADGESCHWINDIGKEIT_HL_WERT | int |  |
| STAT_RADGESCHWINDIGKEIT_HL_EINH | string |  |
| STAT_RADGESCHWINDIGKEIT_HR_WERT | int |  |
| STAT_RADGESCHWINDIGKEIT_HR_EINH | string |  |
| STAT_FGR_WERT | int | Fahrgeschwingigkeitsregler (FGR) Status-Rohwert |
| STAT_FGR_EINH | string | Fahrgeschwindigkeitsregler (FGR) Status-Rohwert |
| STAT_FGR_TEXT | string | Fahrgeschwindigkeitsregler (FGR) Status |
| STAT_SHIFT_LOCK_EIN | int | Shift-Lock 0 oder 1 |
| STAT_SCHALTER_RUECK_EIN | int | Rueckfahrlichtschalter 0 oder 1 Lastenheft Eigendiagnose Stand 5, S.11: nicht im Steuergeraet verbaut!! |
| STAT_ANLASSER_EIN | int | Relais Anlasser 0 oder 1 |
| STAT_HYD_PUMP_EIN | int | Hydraulikpumpe 0 oder 1 |
| STAT_RESERVE_OUT_EIN | int | Reserve Output 0 oder 1 |
| STAT_TREIBER1_NOTANSTEUERUNG_EIN | int | Trouble Shot Down Driver 1 (kommt lowaktiv vom SG, in SGBD invertiert) 0 = aus, 1= ein (lowaktiv!) |
| STAT_TREIBER2_NOTANSTEUERUNG_EIN | int | Trouble Shot Down Driver 2 (kommt lowaktiv vom SG, in SGBD invertiert) 0 = aus, 1= ein |
| STAT_MOTORTEMPERATUR_WERT | int | MOTORTEMPERATUR (KUEHLWASSER) |
| STAT_MOTORTEMPERATUR_EINH | string | MOTORTEMPERATUR |
| STAT_GETRIEBETEMPERATUR_WERT | int | Getriebeoeltemperatur |
| STAT_GETRIEBETEMPERATUR_EINH | string | Getriebeoeltemperatur |
| STAT_HYDRAULIKTEMPERATUR_WERT | int | Hydrauliktemperatur |
| STAT_HYDRAULIKTEMPERATUR_EINH | string | Hydrauliktemperatur |
| STAT_UMGEBUNGSTEMPERATUR_WERT | int | Umgebungstemperatur |
| STAT_UMGEBUNGSTEMPERATUR_EINH | string | Umgebungstemperatur |
| STAT_I_VT_PS_CLUTCH_WERT | int | Kupplungsposition-Rohwert, (Ink)rement SIEMENS (I_VT_PS_CLUTCH) Dieser Wert ist "roher" als STAT_POS_KUP_ROH_WERT |
| STAT_I_VT_PS_CLUTCH_EINH | string | Kupplungsposition-Rohwert, (Ink)rement SIEMENS (I_VT_PS_CLUTCH) Dieser Wert ist "roher" als STAT_POS_KUP_ROH_WERT |
| STAT_POS1_GANG_WERT | unsigned int | Schaltwegpostion 1 (Position Gang) |
| STAT_POS1_GANG_EINH | string | Schaltwegpostion 1 (Position Gang) |
| STAT_POS1_GASSE_WERT | unsigned int | Waehlwinkelposition 1 (Position Gasse) |
| STAT_POS1_GASSE_EINH | string | Waehlwinkelposition 1 (Position Gasse) |
| STAT_POS2_GANG_WERT | unsigned int | Schaltwegpostion 2 (Position Gang) |
| STAT_POS2_GANG_EINH | string | Schaltwegpostion 2 (Position Gang) |
| STAT_POS2_GASSE_WERT | unsigned int | Waehlwinkelposition 2 (Position Gasse) |
| STAT_POS2_GASSE_EINH | string | Waehlwinkelposition 2 (Position Gasse) |
| STAT_STROM_KUP_WERT | unsigned int | Iststrom Magnetventil Kupplung |
| STAT_STROM_KUP_EINH | string | Iststrom Magnetventil Kupplung |
| STAT_STROM_WAEHLWINKEL_WERT | unsigned int | Iststrom Magnetventil Waehlwinkel |
| STAT_STROM_WAEHLWINKEL_EINH | string | Iststrom Magnetventil Waehlwinkel |
| STAT_STROM_SCHALTWEG_R_WERT | unsigned int | Iststrom Magnetventil Schaltweg Rueck |
| STAT_STROM_SCHALTWEG_R_EINH | string | Iststrom Magnetventil Schaltweg Rueck |
| STAT_STROM_SCHALTWEG_V_WERT | unsigned int | Iststrom Magnetventil Schaltweg Vor |
| STAT_STROM_SCHALTWEG_V_EINH | string | Iststrom Magnetventil Schaltweg Vor |
| STAT_UBAT_WERT | real | Batteriespannung (KL.30) |
| STAT_UBAT_EINH | string | Batteriespannung (KL.30) |
| STAT_USENSA_WERT | real | Sensorversorgungsspannung A |
| STAT_USENSA_EINH | string | Sensorversorgungsspannung A |
| STAT_USENSB_WERT | real | Sensorversorgungsspannung B |
| STAT_USENSB_EINH | string | Sensorversorgungsspannung B |
| STAT_PHYD_WERT | unsigned int | Hydraulikdruck |
| STAT_PHYD_EINH | string | Hydraulikdruck |
| STAT_AQUER_ROH_WERT | real | Querbeschleunigung von CAN Rohwert |
| STAT_AQUER_ROH_EINH | string | Querbeschleunigung von CAN Rohwert |
| STAT_ALAENGS_WERT | real | Laengsbeschleunigung (vom DSC) |
| STAT_ALAENGS_EINH | string | Laengsbeschleunigung (vom DSC) |
| STAT_LAENGS_G_CAN_ROH_WERT | real | Laengsbeschleunigung von CAN-Rohwert |
| STAT_LAENGS_G_CAN_ROH_EINH | string | Laengsbeschleunigung von CAN-Rohwert |
| STAT_ALAENGS_ROH_WERT | unsigned int | Laengsbeschleunigung-Rohwert |
| STAT_ALAENGS_ROH_EINH | string | Laengsbeschleunigung-Rohwert |
| STAT_EINGANGSDREHZAHL_ROH_WERT | unsigned int | Getriebeeingangsdrehzahl-Rohwert |
| STAT_EINGANGSDREHZAHL_ROH_EINH | string | Getriebeeingangsdrehzahl-Rohwert |
| STAT_MOTORDREHZAHL_ROH_WERT | unsigned int | Motordrehzahl-Rohwert |
| STAT_MOTORDREHZAHL_ROH_EINH | string | Motordrehzahl-Rohwert |
| STAT_POS_KUP_ROH_WERT | unsigned int | Ist-Position Kupplung-Rohwert, (Ink)rement Nur STAT_I_VT_PS_CLUTCH_WERT ist "roher"! |
| STAT_POS_KUP_ROH_EINH | string | Ist-Position Kupplung-Rohwert, (Ink)rement |
| STAT_GETRIEBETEMPERATUR_ROH_WERT | unsigned int | Getriebeoeltemperatur-Rohwert, (Ink)rement Unsigned Integer |
| STAT_GETRIEBETEMPERATUR_ROH_EINH | string | Getriebeoeltemperatur-Rohwert, (Ink)rement Unsigned Integer |
| STAT_HYDRAULIKTEMPERATUR_ROH_WERT | unsigned int | Hydrauliktemperatur-Rohwert, (Ink)rement Unsigned Integer |
| STAT_HYDRAULIKTEMPERATUR_ROH_EINH | string | Hydrauliktemperatur-Rohwert, (Ink)rement Unsigned Integer |
| STAT_SOLL_STROM_KUP_WERT | unsigned int | Sollstrom Magnetventil Kupplung |
| STAT_SOLL_STROM_KUP_EINH | string | Sollstrom Magnetventil Kupplung |
| STAT_SOLL_STROM_SCHALTWEG_R_WERT | unsigned int | Sollstrom Magnetventil Schaltweg Rueck |
| STAT_SOLL_STROM_SCHALTWEG_R_EINH | string | Sollstrom Magnetventil Schaltweg Rueck |
| STAT_SOLL_STROM_SCHALTWEG_V_WERT | unsigned int | Sollstrom Magnetventil Schaltweg Vor |
| STAT_SOLL_STROM_SCHALTWEG_V_EINH | string | Sollstrom Magnetventil Schaltweg Vor |
| STAT_SOLL_STROM_WAEHLWINKEL_WERT | unsigned int | Sollstrom Magnetventil Waehlwinkel |
| STAT_SOLL_STROM_WAEHLWINKEL_EINH | string | Sollstrom Magnetventil Waehlwinkel |
| STAT_SOLL_POS_KUP_WERT | unsigned int | Sollposition Kupplung, Inkrement  --Unsigned Integer!!!-- (Lastenh.: Integer) --&gt;gecastet!!!&lt;--  dadurch vergleichbar mit STAT_POS_KUP_ROH_WERT |
| STAT_SOLL_POS_KUP_EINH | string | Sollposition Kupplung, Inkrement |
| STAT_SOLL_POS_SCHALTWEG_WERT | int | Sollposition Schaltweg, Inkrement |
| STAT_SOLL_POS_SCHALTWEG_EINH | string | Sollposition Schaltweg, Inkrement |
| STAT_SOLL_POS_WAEHLWINKEL_WERT | int | Sollposition Waehlwinkel, Inkrement |
| STAT_SOLL_POS_WAEHLWINKEL_EINH | string | Sollposition Waehlwinkel, Inkrement |
| STAT_IST_POS_SCHALTWEG_WERT | int | Istposition Schaltweg, Inkrement |
| STAT_IST_POS_SCHALTWEG_EINH | string | Istposition Schaltweg, Inkrement |
| STAT_IST_POS_WAEHLWINKEL_WERT | int | Istposition Waehlwinkel, Inkrement |
| STAT_IST_POS_WAEHLWINKEL_EINH | string | Istposition Waehlwinkel, Inkrement |
| STAT_GEWUENSCHTER_GANG_WERT | int | Gewuenschter Gang 0=Neutral,1-6= Gang 1-6, 7=Rueckwaertsgang |
| STAT_GEWUENSCHTER_GANG_EINH | string | Gewuenschter Gang 0=Neutral,1-6= Gang 1-6, 7=Rueckwaertsgang |
| STAT_GEWUENSCHTER_GANG_TEXT | string | Gewuenschter Gang als Text 0=Neutral,1-6= Gang 1-6, 7=Rueckwaertsgang |
| STAT_FAHRTRICHTUNG_WERT | int | Fahrtrichtung 1=vorwaerts, 2=neutral, 3=rueckwaerts, 255=ungueltig |
| STAT_FAHRTRICHTUNG_EINH | int | Fahrtrichtung 1=vorwaerts, 2=neutral, 3=rueckwaerts, 255=ungueltig |
| STAT_FAHRTRICHTUNG_TEXT | string | Fahrtrichtung als Text 1=vorwaerts, 2=neutral, 3=rueckwaerts, 255=ungueltig |
| STAT_GESCHWINDIGKEIT_HINTERACHSE_WERT | int | Hinterachsgeschwindigkeit |
| STAT_GESCHWINDIGKEIT_HINTERACHSE_EINH | string | Hinterachsgeschwindigkeit |
| STAT_PWG_ROH_WERT | int | Fahrpedalwert von CAN, Rohwert |
| STAT_PWG_ROH_EINH | string | Fahrpedalwert von CAN, Rohwert |
| STAT_MOTOROELTEMPERATUR_WERT | int | Motoroeltemperatur ueber CAN |
| STAT_MOTOROELTEMPERATUR_EINH | string | Motoroeltemperatur ueber CAN |
| STAT_VAR_SI_KONZEPT | unsigned int | Variable Sicherheitskonzept |
| STAT_ERRVAR_ALIVE_DME10_EIN | unsigned int | Fehlervariable fuer CAN Botschaften Alivezaehler in DME10 |
| STAT_ERRVAR_ALIVE_DME11_EIN | unsigned int | Fehlervariable fuer CAN Botschaften Alivezaehler in DME11 |
| STAT_ERRVAR_ALIVE_DME12_EIN | unsigned int | Fehlervariable fuer CAN Botschaften Alivezaehler in DME12 |
| STAT_ERRVAR_ALIVE_DME13_EIN | unsigned int | Fehlervariable fuer CAN Botschaften Alivezaehler in DME13 |
| STAT_ERRVAR_ALIVE_DME14_EIN | unsigned int | Fehlervariable fuer CAN Botschaften Alivezaehler in DME14 |
| STAT_ERRVAR_ALIVE_DME15_EIN | unsigned int | Fehlervariable fuer CAN Botschaften Alivezaehler in DME15 |
| STAT_ERRVAR_SI_DME10_EIN | unsigned int | Fehlervariable fuer CAN Botschaften Sicherheitsvariable in DME10 |
| STAT_ERRVAR_SI_DME11_EIN | unsigned int | Fehlervariable fuer CAN Botschaften Sicherheitsvariable in DME11 |
| STAT_ERRVAR_SI_DME12_EIN | unsigned int | Fehlervariable fuer CAN Botschaften Sicherheitsvariable in DME12 |
| STAT_ERRVAR_SI_DME13_EIN | unsigned int | Fehlervariable fuer CAN Botschaften Sicherheitsvariable in DME13 |
| STAT_ERRVAR_SI_DME14_EIN | unsigned int | Fehlervariable fuer CAN Botschaften Sicherheitsvariable in DME14 |
| STAT_ERRVAR_SI_DME15_EIN | unsigned int | Fehlervariable fuer CAN Botschaften Sicherheitsvariable in DME15 |
| STAT_ZUENDUNGSSIGNAL_EIN | int | Zuendungssignal |
| STAT_GANGANZEIGE_WERT | int | Ganganzeige-Rohwert im Kombi |
| STAT_GANGANZEIGE_EINH | string | Ganganzeige-Rohwert im Kombi |
| STAT_GANGANZEIGE_TEXT | string | Ganganzeige im Kombi als Text |
| STAT_VAR_ABSCHALTEN | int | Variable fuer das Abschalten |
| STAT_VAR_INIT | int | Variable fuer das Initialisieren |
| STAT_ERRVAR_SI_KONZEPT_GETRIEBE | unsigned int | Fehlervariable Sicherheitskonzept Getriebe |
| STAT_ERRVAR_SI_KONZEPT_KUPPLUNG | unsigned int | Fehlervariable Sicherheitskonzept Kupplung |
| STAT_PHYD_ROH_WERT | unsigned int | Hydraulikdruck-Rohwert, Inkrement |
| STAT_PHYD_ROH_EINH | string | Hydraulikdruck-Rohwert, Inkrement |
| STAT_WHS1_EIN | int | Waehlhebel Schalter S1 0 oder 1 |
| STAT_WHS2_EIN | int | Waehlhebel Schalter S2 0 oder 1 |
| STAT_WHE1_EIN | int | Waehlhebel Schalter E1 0 oder 1 |
| STAT_WHE2_EIN | int | Waehlhebel Schalter E2 0 oder 1 |
| STAT_WHN1_EIN | int | Waehlhebel Schalter N1 0 oder 1 |
| STAT_WHN2_EIN | int | Waehlhebel Schalter N2 0 oder 1 |
| STAT_WHR1_EIN | int | Waehlhebel Schalter R1 0 oder 1 |
| STAT_WHR2_EIN | int | Waehlhebel Schalter R2 0 oder 1 |
| STAT_ESTATE_EIN | int | ESTATE=Engine state, Erkennung ob Motor laueft 0=Motordrehzahl &lt; 200 1/min 1=Motordrehzahl &gt; 200 1/min |
| STAT_SPORT_ADD_EIN | int | Schalter Sport+ 0 oder 1 |
| STAT_SPORT_SUB_EIN | int | Schalter Sport- 0 oder 1 |
| STAT_MOTORHAUBE1_EIN | int | Motorhaubenkontakt1 0 oder 1 |
| STAT_MOTORHAUBE2_EIN | int | Motorhaubenkontakt2 0 oder 1 |
| STAT_VA_EIN | int | Verbraucherabschaltung 0 oder 1 |
| STAT_KL50_EIN | int | Zuendung Klemme 50 0 oder 1 |
| STAT_KLR_EIN | int | Zuendung Klemme R 0 oder 1 |
| STAT_KL15_EIN | int | Zuendung Klemme 15 0 oder 1 |
| STAT_FUELLSTAND_VORHANDEN | int | Fuellstand 0 oder 1 Lastenheft Eigendiagnose Stand 5, S.10: nicht im Steuergeraet verbaut!! |
| STAT_LENKRADTASTER_PLUS_AKTIV | int | 0 oder 1 |
| STAT_LENKRADTASTER_MINUS_AKTIV | int | 0 oder 1 |
| STAT_KUPPLUNG_WERT | int | Kupplungsstatus-Rohwert siehe table FUmweltTexte4  WERT UWTEXT |
| STAT_KUPPLUNG_EINH | string | Kupplungsstatus-Rohwert |
| STAT_KUPPLUNG_TEXT | string | Kupplungsstatus siehe table FUmweltTexte4  WERT UWTEXT |
| STAT_ISTGANG_WERT | int | Getriebeuebersetzung: N,1,2,3,4,5,6,R- Rohwert siehe table FUmweltTexte1  WERT UWTEXT |
| STAT_ISTGANG_EINH | string | Getriebeuebersetzung: N,1,2,3,4,5,6,R- Rohwert |
| STAT_ISTGANG_TEXT | string | Getriebeuebersetzung: N,1,2,3,4,5,6,R siehe table FUmweltTexte1  WERT UWTEXT |
| STAT_GETRIEBE_WERT | int | Getriebestatus-Rohwert siehe table FUmweltTexte3  WERT UWTEXT |
| STAT_GETRIEBE_EINH | string | Getriebestatus-Rohwert |
| STAT_GETRIEBE_TEXT | string | Getriebestatus siehe table FUmweltTexte3  WERT UWTEXT |
| STAT_POS_WW1_SIEMENS_WERT | unsigned int | Waehlwinkelposition 1- Rohwert |
| STAT_POS_WW1_SIEMENS_EINH | string | Waehlwinkelposition 1- Rohwert |
| STAT_POS_WW2_SIEMENS_WERT | unsigned int | Waehlwinkelposition 2- Rohwert |
| STAT_POS_WW2_SIEMENS_EINH | string | Waehlwinkelposition 2- Rohwert |
| STAT_POS_SW1_SIEMENS_WERT | unsigned int | Schaltwegposition 1- Rohwert |
| STAT_POS_SW1_SIEMENS_EINH | string | Schaltwegposition 1- Rohwert |
| STAT_POS_SW2_SIEMENS_WERT | unsigned int | Schaltwegposition 2- Rohwert |
| STAT_POS_SW2_SIEMENS_EINH | string | Schaltwegposition 2- Rohwert |
| _TEL_ANTWORT | binary | Antworttelegramm |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [FORTTEXTE](#table-forttexte) (69 × 2)
- [FARTMATRIX](#table-fartmatrix) (1 × 15)
- [FUMWELTMATRIX](#table-fumweltmatrix) (69 × 13)
- [FUMWELTTEXTE](#table-fumwelttexte) (120 × 9)
- [FUMWELTTEXTE1](#table-fumwelttexte1) (9 × 2)
- [FUMWELTTEXTE2](#table-fumwelttexte2) (5 × 2)
- [FUMWELTTEXTE3](#table-fumwelttexte3) (12 × 2)
- [FUMWELTTEXTE4](#table-fumwelttexte4) (6 × 2)
- [FUMWELTTEXTE5](#table-fumwelttexte5) (8 × 2)
- [FUMWELTTEXTE6](#table-fumwelttexte6) (5 × 2)
- [FUMWELTTEXTE7](#table-fumwelttexte7) (17 × 2)
- [FUMWELTTEXTE8](#table-fumwelttexte8) (17 × 2)
- [FUMWELTTEXTE9](#table-fumwelttexte9) (5 × 2)
- [FUMWELTTEXTE15](#table-fumwelttexte15) (5 × 2)
- [FARTTEXTE](#table-farttexte) (10 × 2)
- [SPEICHER](#table-speicher) (4 × 2)
- [STELLGLIEDER](#table-stellglieder) (10 × 2)
- [TESTPRG](#table-testprg) (14 × 4)
- [STATTESTTEXTE](#table-stattesttexte) (5 × 2)
- [INFOTEXTE1A](#table-infotexte1a) (4 × 2)
- [INFOTEXTE1F](#table-infotexte1f) (5 × 2)
- [INFOTEXTE2A](#table-infotexte2a) (4 × 2)
- [INFOTEXTE2F](#table-infotexte2f) (8 × 2)
- [INFOTEXTE3A](#table-infotexte3a) (5 × 2)
- [INFOTEXTE3F](#table-infotexte3f) (9 × 2)
- [INFOTEXTE4A](#table-infotexte4a) (7 × 2)
- [INFOTEXTE4F](#table-infotexte4f) (7 × 2)
- [INFOTEXTE5A](#table-infotexte5a) (14 × 2)
- [INFOTEXTE5F](#table-infotexte5f) (8 × 2)
- [INFOTEXTE6A](#table-infotexte6a) (7 × 2)
- [INFOTEXTE6F](#table-infotexte6f) (11 × 2)
- [INFOTEXTE7A](#table-infotexte7a) (21 × 2)
- [INFOTEXTE7F](#table-infotexte7f) (38 × 2)
- [INFOTEXTE8A](#table-infotexte8a) (8 × 2)
- [INFOTEXTE8F](#table-infotexte8f) (5 × 2)
- [INFOTEXTE9A](#table-infotexte9a) (6 × 2)
- [INFOTEXTE9F](#table-infotexte9f) (10 × 2)
- [INFOTEXTE10A](#table-infotexte10a) (6 × 2)
- [INFOTEXTE10F](#table-infotexte10f) (5 × 2)
- [INFOTEXTE11A](#table-infotexte11a) (19 × 2)
- [INFOTEXTE11F](#table-infotexte11f) (38 × 2)
- [INFOTEXTE12A](#table-infotexte12a) (4 × 2)
- [INFOTEXTE12F](#table-infotexte12f) (8 × 2)
- [INFOTEXTE13A](#table-infotexte13a) (8 × 2)
- [INFOTEXTE13F](#table-infotexte13f) (11 × 2)
- [INFOTEXTE21A](#table-infotexte21a) (4 × 2)
- [INFOTEXTE21F](#table-infotexte21f) (8 × 2)
- [HINTERACHSUEBERSETZUNG](#table-hinterachsuebersetzung) (17 × 2)
- [INFOTEXTEFAHRZEUGZUSTAND](#table-infotextefahrzeugzustand) (48 × 2)
- [FGR](#table-fgr) (9 × 2)
- [FREEZE_FRAME_REFERENZ](#table-freeze-frame-referenz) (6 × 2)
- [PROGRAMMINFO](#table-programminfo) (7 × 2)
- [KOMFORTINDEX](#table-komfortindex) (14 × 2)
- [GANGANZEIGE](#table-ganganzeige) (12 × 2)
- [WAEHLHEBELANZEIGE](#table-waehlhebelanzeige) (15 × 2)
- [LED](#table-led) (4 × 2)

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 69 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x22 | Getriebetemperatur |
| 0x27 | Hydrauliktemperatur |
| 0x23 | Auswertung Hydraulikdrucksensor |
| 0x35 | Druckbandunterschreitung HE |
| 0x36 | Druckbandueberschreitung HE |
| 0x33 | Auswertung Motorhaubenkontakt im Fahrbetrieb |
| 0x34 | Auswertung Motorhaubenkontakt im Stand |
| 0x72 | Auswertung Waehlhebel |
| 0x24 | Auswertung Positionsgeber Waehlwinkel |
| 0x25 | Auswertung Positionsgeber Schaltweg |
| 0x26 | Auswertung Laengsbeschleunigung |
| 0x61 | Spannungsversorgung |
| 0x62 | Sensorspannungsversorgung A |
| 0x63 | Sensorspannungsversorgung B |
| 0x20 | Auswertung Getriebeeingangsdrehzahl |
| 0x21 | Auswertung Motordrehzahl (Sensor) |
| 0x96 | Auswertung Motordrehzahl (CAN) |
| 0x28 | Auswertung PLCD-Sensor fuer Kupplungsposition |
| 0x80 | Fehlerhafte CAN Botschaft / CAN Busfehler |
| 0x81 | CAN Fehler |
| 0x91 | Auswertung Geschwindigkeit hinten links |
| 0x92 | Auswertung Geschwindigkeit hinten rechts |
| 0x93 | Auswertung Geschwindigkeit vorne links |
| 0x94 | Auswertung Geschwindigkeit vorne rechts |
| 0x95 | Auswertung Geschwindigkeiten (mehr als ein Signal) |
| 0x97 | Auswertung Betriebsbremssignale ueber CAN |
| 0x9B | Auswertung Fahrpedalwert ueber CAN |
| 0x98 | Auswertung Lenkwinkel ueber CAN |
| 0x99 | Auswertung Querbeschleunigung ueber CAN |
| 0x9A | Auswertung Laengsbeschleunigung ueber CAN |
| 0x90 | Auswertung Tuerkontakt ueber CAN |
| 0x13 | Ansteuerung Shift Lock |
| 0x14 | Anlasserfreigabe |
| 0x15 | Ansteuerung Hydraulikpumpenrelais |
| 0x16 | Ansteuerung Rueckfahrlichtschalter |
| 0x10 | Ansteuerung Magnetventil Schaltweg Vor |
| 0x11 | Ansteuerung Magnetventil Schaltweg Rueck |
| 0x12 | Ansteuerung Magnetventil Waehlwinkel |
| 0x17 | Ansteuerung Magnetventil Kupplung |
| 0x50 | SMG Steuergeraet interner Fehler |
| 0xB0 | Sicherheitskonzept Ebene 2 Getriebe |
| 0xB1 | Sicherheitskonzept Ebene 2 Kupplung |
| 0xB2 | Sicherheitskonzept Ebene 3 |
| 0x53 | Getriebeadaption |
| 0x54 | Allgemeine Adaption |
| 0x55 | Adaption der Kupplung |
| 0x30 | Gang nicht einlegbar |
| 0x31 | Gangspringer |
| 0x32 | Waehlwinkel nicht einregelbar |
| 0x73 | Auswertung Verbraucherabschaltung VA |
| 0x74 | Auswertung Programmwahlschalter Plus |
| 0x75 | Auswertung Programmwahlschalter Minus |
| 0x76 | Auswertung Lenkradschalter + |
| 0x77 | Auswertung Lenkradschalter - |
| 0x37 | Einschalthaeufigkeit Hydraulikeinheit |
| 0x38 | Einschaltdauer Hydraulikeinheit |
| 0x39 | Missbrauch Hydraulikeinheit |
| 0x64 | Spannungsversorgung Magnetventile Schaltweg |
| 0x65 | Spannungsversorgung Magnetventile Kupplung und Waehlwinkel |
| 0x56 | Entlueftungen |
| 0x57 | Aktionsmodi |
| 0x78 | Auswertung Zuendschloss-Signal |
| 0x51 | Auswertung ESTATE |
| 0xB3 | Sicherheitskonzept Ebene 2 RAM |
| 0xB4 | Sicherheitskonzept Ebene 2 INPUT |
| 0x3A | Gang nicht auslegbar |
| 0x3B | Ansteuerung Kupplung |
| 0x58 | Adaptionswerte Getriebe |
| 0xFF | unbekannter Fehlerort |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 1 rows × 15 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xXY | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x07 | 0x00 | 0x08 |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 69 rows × 13 columns

| ORT | UW_ANZ | UW_SATZ | UW_1NR | UW_2NR | UW_3NR | UW_4NR | UW_5NR | UW_6NR | UW_7NR | UW_8NR | UW_9NR | UW_10NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x22 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x1D | 0x1E | 0x00 | 0x3E | 0x00 | 0x00 | 0x1F |
| 0x27 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x1D | 0x1E | 0x44 | 0x00 | 0x3F | 0x00 | 0x00 |
| 0x23 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x07 | 0x0C | 0x1E | 0x25 | 0x38 | 0x5B | 0x00 |
| 0x35 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x07 | 0x1E | 0x25 | 0x31 | 0x30 | 0x00 | 0x00 |
| 0x36 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x07 | 0x1E | 0x25 | 0x31 | 0x30 | 0x00 | 0x00 |
| 0x33 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x09 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x00 |
| 0x34 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x09 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x00 |
| 0x72 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x08 | 0x15 | 0x24 | 0x00 | 0x00 | 0x3B | 0x00 |
| 0x24 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x0B | 0x2D | 0x2E | 0x41 | 0x00 | 0x37 | 0x38 |
| 0x25 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x0B | 0x2B | 0x2C | 0x40 | 0x00 | 0x37 | 0x38 |
| 0x26 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x71 | 0x73 | 0x14 | 0x00 | 0x38 | 0x3A | 0x01 |
| 0x61 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x1B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x62 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x00 | 0x37 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x63 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x00 | 0x00 | 0x38 | 0x66 | 0x00 | 0x00 | 0x00 |
| 0x20 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x0B | 0x18 | 0x1B | 0x5F | 0x30 | 0x31 | 0x39 |
| 0x21 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x18 | 0x1A | 0x1B | 0x31 | 0x42 | 0x00 | 0x00 |
| 0x96 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x18 | 0x1A | 0x1B | 0x31 | 0x42 | 0x00 | 0x00 |
| 0x28 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x2A | 0x00 |
| 0x80 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x45 | 0x00 | 0x46 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x81 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x45 | 0x00 | 0x46 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x91 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x0B | 0x18 | 0x20 | 0x21 | 0x22 | 0x23 | 0x31 |
| 0x92 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x0B | 0x18 | 0x20 | 0x21 | 0x22 | 0x23 | 0x31 |
| 0x93 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x0B | 0x18 | 0x20 | 0x21 | 0x22 | 0x23 | 0x31 |
| 0x94 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x0B | 0x18 | 0x20 | 0x21 | 0x22 | 0x23 | 0x31 |
| 0x95 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x0B | 0x18 | 0x20 | 0x21 | 0x22 | 0x23 | 0x31 |
| 0x97 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x71 | 0x73 | 0x14 | 0x16 | 0x38 | 0x3A | 0x01 |
| 0x9B | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x00 | 0x49 | 0x00 | 0x1A | 0x00 | 0x00 | 0x00 |
| 0x98 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x45 | 0x00 | 0x46 | 0x00 | 0x00 | 0x00 | 0x5C |
| 0x99 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x45 | 0x00 | 0x46 | 0x00 | 0x00 | 0x02 | 0x00 |
| 0x9A | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x45 | 0x00 | 0x46 | 0x00 | 0x3D | 0x00 | 0x00 |
| 0x90 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x35 | 0x3A | 0x45 | 0x00 | 0x46 | 0x00 | 0x00 |
| 0x13 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x04 | 0x15 | 0x24 | 0x00 | 0x00 | 0x00 | 0x89 |
| 0x14 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x89 |
| 0x15 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x07 | 0x0C | 0x1E | 0x25 | 0x00 | 0x5B | 0x00 |
| 0x16 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x05 | 0x15 | 0x24 | 0x00 | 0x00 | 0x00 | 0x89 |
| 0x10 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x10 | 0x11 | 0x25 | 0x28 | 0x75 | 0x40 | 0x60 |
| 0x11 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x0E | 0x0F | 0x25 | 0x28 | 0x75 | 0x40 | 0x61 |
| 0x12 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x12 | 0x13 | 0x25 | 0x62 | 0x29 | 0x75 | 0x41 |
| 0x17 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x75 | 0x0C | 0x0D | 0x25 | 0x27 | 0x26 | 0x63 |
| 0x50 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x64 | 0x65 | 0x6A | 0x6B | 0x6C | 0x6D | 0x6E |
| 0xB0 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x72 | 0x76 | 0x77 | 0x85 | 0x79 | 0x80 | 0x81 |
| 0xB1 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x82 | 0x69 | 0x84 | 0x85 | 0x87 | 0x88 | 0x77 |
| 0xB2 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x59 | 0x5A | 0x67 | 0x68 | 0x79 | 0x77 | 0x76 |
| 0x53 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x32 | 0x33 | 0x34 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x54 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x32 | 0x33 | 0x34 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x55 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x32 | 0x33 | 0x34 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x30 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x26 | 0x40 | 0x28 | 0x41 | 0x29 | 0x3B | 0x1D |
| 0x31 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x26 | 0x40 | 0x28 | 0x41 | 0x29 | 0x3B | 0x1D |
| 0x32 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x26 | 0x40 | 0x28 | 0x41 | 0x29 | 0x3B | 0x1D |
| 0x73 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x56 |
| 0x74 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x54 | 0x00 | 0x24 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x75 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x55 | 0x00 | 0x24 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x76 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x00 | 0x00 | 0x24 | 0x00 | 0x00 | 0x00 | 0x52 |
| 0x77 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x00 | 0x00 | 0x24 | 0x00 | 0x00 | 0x00 | 0x53 |
| 0x37 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x07 | 0x1E | 0x25 | 0x31 | 0x30 | 0x1A | 0x38 |
| 0x38 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x07 | 0x1E | 0x25 | 0x31 | 0x30 | 0x1A | 0x38 |
| 0x39 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x07 | 0x1E | 0x25 | 0x31 | 0x30 | 0x1A | 0x38 |
| 0x64 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x75 | 0x25 | 0x0C | 0x12 | 0x0E | 0x10 | 0x2A |
| 0x65 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x75 | 0x25 | 0x0C | 0x12 | 0x0E | 0x10 | 0x2A |
| 0x56 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x32 | 0x33 | 0x34 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x57 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x32 | 0x33 | 0x34 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x78 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1B | 0x48 | 0x00 |
| 0x51 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x72 | 0x76 | 0x77 | 0x85 | 0x79 | 0x80 | 0x81 |
| 0xB3 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x72 | 0x76 | 0x77 | 0x85 | 0x79 | 0x80 | 0x81 |
| 0xB4 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x72 | 0x76 | 0x77 | 0x85 | 0x79 | 0x80 | 0x81 |
| 0x3A | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x26 | 0x40 | 0x28 | 0x41 | 0x29 | 0x3B | 0x1D |
| 0x3B | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x0C | 0x73 | 0x1E | 0x25 | 0x2A | 0x27 | 0x1A |
| 0x58 | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xXY | 10 | 3 | 0x17 | 0x1C | 0x36 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 120 rows × 9 columns

| UWNR | UWTEXT | UW_TYP | UW_EINH | MASK | NAME | UW_MULT | UW_DIV | UW_ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x00 | nicht relevant | sshort | - | -- | -- | 1 | 1 | 0 |
| 0x01 | Laengsbeschleunigung | sshort | g | -- | -- | 625 | 100000 | 0 |
| 0x02 | Querbeschleunigung (CAN) | sshort | m/s^2 | -- | -- | 48 | 1000 | -24.576 |
| 0x03 | Querbeschleunigung Rohwert | ushort | g | -- | -- | 625 | 100000 | 0 |
| 0x04 | Status Shift Lock | ushort | 0/1 | 0x0001 | -- | 1 | 1 | 0 |
| 0x05 | Status Rueckfahrlichtschalter | ushort | 0/1 | 0x0002 | -- | 1 | 1 | 0 |
| 0x06 | Status Anlasserfreigabe | ushort | 0/1 | 0x0080 | -- | 1 | 1 | 0 |
| 0x07 | Status Hydraulikpumpe | ushort | 0/1 | 0x0100 | -- | 1 | 1 | 0 |
| 0x08 | Waehlhebelsignale | ushort | 0/1 | 0x03FC | -- | 1 | 1 | 0 |
| 0x09 | Motorhaubenkontakte | ushort | 0-n | 0xC000 | FUmweltTexte15 | 1 | 1 | 0 |
| 0x0B | Aktueller Gang | ubyte | 0-n | -- | FUmweltTexte1 | 1 | 1 | 0 |
| 0x0C | Iststrom Magnetventil Kupplung | ushort | mA | -- | -- | 1 | 1 | 0 |
| 0x0D | Sollstrom Magnetventil Kupplung | ushort | mA | -- | -- | 1 | 1 | 0 |
| 0x0E | Iststrom Magnetventil Schaltweg Rueck | ushort | mA | -- | -- | 1 | 1 | 0 |
| 0x0F | Sollstrom Magnetventil Schaltweg Rueck | ushort | mA | -- | -- | 1 | 1 | 0 |
| 0x10 | Iststrom Magnetventil Schaltweg Vor | ushort | mA | -- | -- | 1 | 1 | 0 |
| 0x11 | Sollstrom Magnetventil Schaltweg Vor | ushort | mA | -- | -- | 1 | 1 | 0 |
| 0x12 | Iststrom Magnetventil Waehlwinkel | ushort | mA | -- | -- | 1 | 1 | 0 |
| 0x13 | Sollstrom Magnetventil Waehlwinkel | ushort | mA | -- | -- | 1 | 1 | 0 |
| 0x14 | Bremssignale | ubyte | 0-n | -- | FUmweltTexte6 | 1 | 1 | 0 |
| 0x15 | Fahrtrichtung | ubyte | 0-n | -- | FUmweltTexte2 | 1 | 1 | 0 |
| 0x16 | Fahrpedalwert | sshort | % | -- | -- | 1 | 10 | 0 |
| 0x17 | Kilometerstand | ushort | km | -- | -- | 10 | 1 | 0 |
| 0x18 | Getriebeeingangsdrehzahl | sshort | 1/min | -- | -- | 1 | 1 | 0 |
| 0x19 | Getriebeausgangsdrehzahl | sshort | 1/min | -- | -- | 1 | 1 | 0 |
| 0x1A | Motordrehzahl von CAN | sshort | 1/min | -- | -- | 1 | 1 | 0 |
| 0x1B | Motordrehzahl Istwert | sshort | 1/min | -- | -- | 1 | 1 | 0 |
| 0x1C | Umgebungstemperatur | ubyte | Grad C | -- | -- | 1 | 1 | -48 |
| 0x1D | Getriebetemperatur Istwert | ubyte | Grad C | -- | -- | 1 | 1 | -48 |
| 0x1E | Hydrauliktemperatur Istwert | ubyte | Grad C | -- | -- | 1 | 1 | -48 |
| 0x1F | Motoroeltemperatur von CAN | ubyte | Grad C | -- | -- | 1 | 1 | -48 |
| 0x20 | Radgeschwindigkeit hinten links | sshort | km/h | -- | -- | 1 | 16 | 0 |
| 0x21 | Radgeschwindigkeit hinten rechts | sshort | km/h | -- | -- | 1 | 16 | 0 |
| 0x22 | Radgeschwindigkeit vorne links | sshort | km/h | -- | -- | 1 | 16 | 0 |
| 0x23 | Radgeschwindigkeit vorne rechts | sshort | km/h | -- | -- | 1 | 16 | 0 |
| 0x24 | Waehlhebelposition | ubyte | 0-n | -- | FUmweltTexte5 | 1 | 1 | 0 |
| 0x25 | Hydraulikdruck Rohwert | ushort | bar | -- | -- | 0.122 | 1 | -12.481 |
| 0x26 | Kupplungsposition Istwert | sshort | Ink | -- | -- | 1 | 1 | 0 |
| 0x27 | Sollposition Kupplung | sshort | Ink | -- | -- | 1 | 1 | 0 |
| 0x28 | Sollposition Schaltweg | sshort | Ink | -- | -- | 1 | 1 | 0 |
| 0x29 | Sollposition Waehlwinkel | sshort | Ink | -- | -- | 1 | 1 | 0 |
| 0x2A | Kupplungsposition Rohwert | ushort | Ink | -- | -- | 1 | 1 | 0 |
| 0x2B | Schaltwegposition 1 Rohwert | ushort | Ink | -- | -- | 1 | 1 | 0 |
| 0x2C | Schaltwegposition 2 Rohwert | ushort | Ink | -- | -- | 1 | 1 | 0 |
| 0x2D | Waehlwinkelposition 1 Rohwert | ushort | Ink | -- | -- | 1 | 1 | 0 |
| 0x2E | Waehlwinkelposition 2 Rohwert | ushort | Ink | -- | -- | 1 | 1 | 0 |
| 0x30 | Getriebestatus | ubyte | 0-n | -- | FUmweltTexte3 | 1 | 1 | 0 |
| 0x31 | Kupplungsstatus | ubyte | 0-n | -- | FUmweltTexte4 | 1 | 1 | 0 |
| 0x32 | Adaptions- bzw. Testprogramm-Nr. | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x33 | Fehlermeldung der Adaption | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x34 | Adaptionszustand | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x35 | Tuerkontakt | ushort | 0/1 | 0x0080 | -- | 1 | 1 | 0 |
| 0x36 | Spannungsversorgung Ubatt | ushort | V | -- | -- | 25 | 1000 | 0 |
| 0x37 | Sensorversorgung A Rohwert | ushort | V | -- | -- | 9766 | 1000000 | 0 |
| 0x38 | Sensorversorgung B Rohwert | ushort | V | -- | -- | 9766 | 1000000 | 0 |
| 0x39 | Radgeschwindigkeit der Hinterachse | sshort | km/h | -- | -- | 1 | 16 | 0 |
| 0x3A | Fahrzeuggeschwindigkeit | sshort | km/h | -- | -- | 1 | 16 | 0 |
| 0x3B | Gewuenschter Gang | ubyte | 0-n | -- | FUmweltTexte1 | 1 | 1 | 0 |
| 0x3C | Variablen Sicherheitskonzept Getriebe | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x3D | Laengsbeschleunigung von CAN | sshort | m/s^2 | -- | -- | 1 | 10 | -12.7 |
| 0x3E | Getriebetemperatur Rohwert | ushort | Ink | -- | -- | 1 | 1 | 0 |
| 0x3F | Hydrauliktemperatur | ushort | Ink | -- | -- | 1 | 1 | 0 |
| 0x40 | Schaltwegposition Istwert | sshort | Ink | -- | -- | 1 | 1 | 0 |
| 0x41 | Waehlwinkelposition Istwert | sshort | Ink | -- | -- | 1 | 1 | 0 |
| 0x42 | Motordrehzahl Rohwert | ushort | 1/min | -- | -- | 1 | 1 | 0 |
| 0x44 | Motortemperatur (Kuehlwasser) | ubyte | Grad C | -- | -- | 1 | 1 | -48 |
| 0x45 | Byte - CAN-Botschaft-Fehler | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x46 | Byte - CAN-Empfangs-Sende-Fehler | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x48 | Zuendungssignale | ubyte | 0-n | -- | FUmweltTexte9 | 1 | 1 | 0 |
| 0x49 | Fahrpedalwert (CAN) | sshort | % | -- | -- | 1 | 10 | 0 |
| 0x52 | Lenkradschalter SH + | ushort | 0/1 | 0x0020 | -- | 1 | 1 | 0 |
| 0x53 | Lenkradschalter SH - | ushort | 0/1 | 0x0080 | -- | 1 | 1 | 0 |
| 0x54 | Programmwahlschalter + | ushort | 0/1 | 0x0800 | -- | 1 | 1 | 0 |
| 0x55 | Programmwahlschalter - | ushort | 0/1 | 0x1000 | -- | 1 | 1 | 0 |
| 0x56 | Status VA | ushort | 0/1 | 0x0001 | -- | 1 | 1 | 0 |
| 0x57 | Status Anlasser KL50 | ushort | 0/1 | 0x0002 | -- | 1 | 1 | 0 |
| 0x58 | Status KL15 | ushort | 0/1 | 0x0008 | -- | 1 | 1 | 0 |
| 0x59 | Fehlercode MU | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x5A | Fehlercode MC | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x5B | Hydraulikdruck AD-Wert | ushort | Ink | -- | -- | 1 | 1 | 0 |
| 0x5C | Lenkwinkel (CAN) | sshort | Grad | -- | -- | 1 | 1 | -2047 |
| 0x5D | Gradient Motordrehzahl | sshort | 1/min | -- | -- | 1 | 1 | 0 |
| 0x5E | Gradient Getriebeeingangsdrehzahl | sshort | 1/min | -- | -- | 1 | 1 | 0 |
| 0x5F | Getriebeeingangsdrehzahl Rohwert | ushort | 1/min | -- | -- | 1 | 1 | 0 |
| 0x60 | Duty Cycle Ventil Schaltweg Vor | ushort | % | -- | -- | 1 | 100 | 0 |
| 0x61 | Duty Cycle Ventil Schaltweg Rueck | ushort | % | -- | -- | 1 | 100 | 0 |
| 0x62 | Duty Cycle Ventil Waehlwinkel | ushort | % | -- | -- | 1 | 100 | 0 |
| 0x63 | Duty Cycle Ventil Kupplung | ushort | % | -- | -- | 1 | 100 | 0 |
| 0x64 | Duty Cycle Signal OSC_IN | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x65 | Periodendauer Signal OSC_IN | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x66 | Port 7 | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x67 | Reset-Counter MC | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x68 | Reset-Counter MU | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x69 | Variablen Sicherheitskonzept Kupplung | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x6A | SPI Timeout | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x6B | SPI Hardwarefehler | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x6C | Status BIOS SW | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x6D | Variable fuers Abschalten | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x6E | Variable fuers Initialisieren | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x6F | Lifetime-Zaehler SG obere 2 Bytes | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x70 | Lifetime-Zaehler SG untere 2 Bytes | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x71 | Laengsbeschleunigung Rohwert | ushort | Ink | -- | -- | 1 | 1 | 0 |
| 0x72 | Byte - Digitaleingang 1 | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x73 | Bremssignale Rohwert | ubyte | 0-n | -- | FUmweltTexte6 | 1 | 1 | 0 |
| 0x74 | Statusbyte Digitalausgang 2 | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x75 | Statusbyte Digitalausgang | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x76 | Motordrehzahl Rohwert im resetfesten Bereich | ushort | 1/min | -- | -- | 1 | 1 | 0 |
| 0x77 | Byte - Gewuenschter und aktueller Gang im resetfesten Bereich | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x78 | Radgeschwindigkeit im resetfesten Bereich | sshort | km/h | -- | -- | 1 | 16 | 0 |
| 0x79 | Byte - Betriebsbremse und Getriebestatus im resetfesten Bereich | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x80 | Byte - Fehlervariable des Sicherheitskonzept Getriebe | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x81 | Resetzaehler Sicherheitskonzept Getriebe | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x82 | Byte - Fehlerursache Sicherheitskonzept Kupplung | ubyte | - | -- | -- | 1 | 1 | 0 |
| 0x83 | Byte - Umgebungsvariable | ushort | - | -- | -- | 1 | 1 | 0 |
| 0x84 | Radgeschwindigkeit der Vorderachse im resetfesten Bereich | sshort | km/h | -- | -- | 1 | 16 | 0 |
| 0x85 | Radgeschwindigkeit der Hinterachse im resetfesten Bereich | sshort | km/h | -- | -- | 1 | 16 | 0 |
| 0x87 | Sollposition der Kupplung im resetfesten Bereich | sshort | Ink | -- | -- | 1 | 1 | 0 |
| 0x88 | Istposition der Kupplung im resetfesten Bereich | sshort | Ink | -- | -- | 1 | 1 | 0 |
| 0x89 | Byte - Digitaleingang 2 | ushort | - | -- | -- | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | - | XY | -- | -- | 1 | 1 | 0 |

<a id="table-fumwelttexte1"></a>
### FUMWELTTEXTE1

Dimensions: 9 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 0/Neutral |
| 0x01 | 1.Gang |
| 0x02 | 2.Gang |
| 0x03 | 3.Gang |
| 0x04 | 4.Gang |
| 0x05 | 5.Gang |
| 0x06 | 6.Gang |
| 0x07 | Rueckwaertsgang |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte2"></a>
### FUMWELTTEXTE2

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | vorwaerts |
| 0x02 | neutral |
| 0x03 | rueckwaerts |
| 0xFF | ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte3"></a>
### FUMWELTTEXTE3

Dimensions: 12 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | geschaltet |
| 0x01 | aktiv |
| 0x02 | Zwischenkuppeln |
| 0x03 | Synchronisation |
| 0x04 | Schaltweg Neutral |
| 0x05 | Waehlwinkel einregeln |
| 0x06 | Vorspannen |
| 0x07 | Waehlwinkel ablegen aus |
| 0x08 | Getriebe init aktiv |
| 0x09 | Synchronisation fertig |
| 0x0A | vor Synchronisation |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte4"></a>
### FUMWELTTEXTE4

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | offen |
| 0x01 | geschlossen |
| 0x02 | oeffnet |
| 0x03 | schliesst |
| 0x04 | Zwischenkuppeln aktiv |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte5"></a>
### FUMWELTTEXTE5

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Waehlhebel in P (Parken) |
| 0x02 | Waehlhebel in R (Rueckwaerts) |
| 0x03 | Waehlhebel in 0 (Neutral) |
| 0x04 | Waehlhebel in A (Automatik) |
| 0x05 | Waehlhebel in S (Sequentiell) |
| 0x06 | Waehlhebel in + (Gang hoch) |
| 0x07 | Waehlhebel in - (Gang runter) |
| 0xFF | Waehlhebelposition nicht definiert |

<a id="table-fumwelttexte6"></a>
### FUMWELTTEXTE6

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Bremse nicht betätigt |
| 0x01 | Bremslichtschalter |
| 0x02 | Bremslichttestschalter |
| 0x03 | Bremslicht- und -test-schalter |
| 0xFF | nicht definiert |

<a id="table-fumwelttexte7"></a>
### FUMWELTTEXTE7

Dimensions: 17 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | CAN Alivezaehler DME 10 nicht korrekt |
| 0x01 | CAN Alivezaehler DME 11 nicht korrekt |
| 0x02 | CAN Alivezaehler DME 12 nicht korrekt |
| 0x03 | CAN Alivezaehler DME 13 nicht korrekt |
| 0x04 | CAN Alivezaehler DME 14 nicht korrekt |
| 0x05 | CAN Alivezaehler DME 15 nicht korrekt |
| 0x06 | nicht belegt |
| 0x07 | nicht belegt |
| 0x08 | CAN Sicherheitsvariable DME 10 nicht korrekt |
| 0x09 | CAN Sicherheitsvariable DME 11 nicht korrekt |
| 0x0A | CAN Sicherheitsvariable DME 12 nicht korrekt |
| 0x0B | CAN Sicherheitsvariable DME 13 nicht korrekt |
| 0x0C | CAN Sicherheitsvariable DME 14 nicht korrekt |
| 0x0D | CAN Sicherheitsvariable DME 15 nicht korrekt |
| 0x0E | nicht belegt |
| 0x0F | nicht belegt |
| 0xFF | nicht definiert |

<a id="table-fumwelttexte8"></a>
### FUMWELTTEXTE8

Dimensions: 17 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Nachricht SMG 10 nicht korrekt gesendet |
| 0x01 | Nachricht SMG 11 nicht korrekt gesendet |
| 0x02 | Nachricht SMG 12 nicht korrekt gesendet |
| 0x03 | nicht belegt |
| 0x04 | nicht belegt |
| 0x05 | nicht belegt |
| 0x06 | nicht belegt |
| 0x07 | nicht belegt |
| 0x08 | Nachricht DME 10 nicht korrekt empfangen |
| 0x09 | Nachricht DME 11 nicht korrekt empfangen |
| 0x0A | Nachricht DME 12 nicht korrekt empfangen |
| 0x0B | Nachricht DME 13 nicht korrekt empfangen |
| 0x0C | Nachricht DME 14 nicht korrekt empfangen |
| 0x0D | Nachricht DME 15 nicht korrekt empfangen |
| 0x0E | Nachricht DME 16 nicht korrekt empfangen |
| 0x0F | nicht belegt |
| 0xFF | nicht definiert |

<a id="table-fumwelttexte9"></a>
### FUMWELTTEXTE9

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Zuendung aus |
| 0x01 | Radio Ein-Stellung |
| 0x02 | Fahrtstellung |
| 0x03 | Anlassen |
| 0xFF | nicht definiert |

<a id="table-fumwelttexte15"></a>
### FUMWELTTEXTE15

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | geschlossen |
| 0x4000 | (1) links offen |
| 0x8000 | (2) rechts offen |
| 0xC000 | (1+2) links + rechts offen |
| 0xFFFF | nicht definiert |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 10 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | KS gegen UBatt |
| 0x02 | KS gegen Masse |
| 0x03 | Leitungsunterbrechung |
| 0x04 | unplausibler Wert |
| 0x05 | SG spezifisch |
| 0x06 | SG spezifisch |
| 0x07 | Fehler momentan vorhanden |
| 0x08 | sporadischer Fehler |
| 0xFF | unbekannte Fehlerart |

<a id="table-speicher"></a>
### SPEICHER

Dimensions: 4 rows × 2 columns

| SPEICHER | WERT |
| --- | --- |
| FLASH | 0x00 |
| RAM | 0x00 |
| ROM | 0x00 |
| E2PROM | 0x00 |

<a id="table-stellglieder"></a>
### STELLGLIEDER

Dimensions: 10 rows × 2 columns

| STELLGLIED | PIN |
| --- | --- |
| MAGNETVENTIL_KUPPLUNG | 0x0A |
| MAGNETVENTIL_GASSE | 0x28 |
| MAGNETVENTIL_GANG_VOR | 0x48 |
| MAGNETVENTIL_GANG_R | 0x4C |
| ANLASSER_FREIGABE | 0x08 |
| HYDROPUMPE | 0x05 |
| STOERANZEIGE | 0x3E |
| SHIFTLOCK | 0x3F |
| GANG_WAHLHEBEL_ANZEIGE | 0x42 |
| KOMBIANZEIGE_KOMFORTINDEX | 0x43 |

<a id="table-testprg"></a>
### TESTPRG

Dimensions: 14 rows × 4 columns

| TESTPRG_NR | TESTPRG_NAME | DAUER TYP. | DAUER MAX. |
| --- | --- | --- | --- |
| 0x01 | Entlueftung Kuppl.-Nehmerzyl./Hydraulikleit. | 2 min | 2 min |
| 0x02 | Kupplungsschleifpunkt einlernen | 5 sek | 10 sek |
| 0x03 | Kupplungsventilkennwerte einlernen | 1 min | 2 min |
| 0x04 | Speichervorspanndruck ermitteln | 8 sek | 30 sek |
| 0x05 | Entlueftung Getriebeakuator | 16 min | 16 min |
| 0x06 | Stromoffset Waehlwinkel (Gasse) einlernen |  |  |
| 0x07 | Getriebe komplett adaptieren | 2,30 min | 3,0 min |
| 0x08 | Offset Laengsbeschleunigungssensor einlernen | 5 sek | 20 sek |
| 0x09 | Schaltwegmittellage positionieren |  |  |
| 0x0A | Beliebigen Gang einlegen |  |  |
| 0x0B | Getriebe einlernen |  |  |
| 0x0C | Schaltwegmitte und Waehlwinkelsenor testen |  |  |
| 0x0D | Gangerkennung Waehlwinkel einlernen |  |  |
| 0x15 | Startbedingungen fuer Motor herstellen |  |  |

<a id="table-stattesttexte"></a>
### STATTESTTEXTE

Dimensions: 5 rows × 2 columns

| STB | TEST_STATUS_TEXT |
| --- | --- |
| 0x00 | Testbedingung nicht erfuellt |
| 0x01 | Testprogramm laeuft |
| 0x02 | Testprogramm beendet |
| 0x03 | Testprogramm nicht ordnungsgemaess beendet |
| 0xFF | Unbekannter Status |

<a id="table-infotexte1a"></a>
### INFOTEXTE1A

Dimensions: 4 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm Initialisierung |
| 0x01 | Kupplungsentlueftung |
| 0x7F | Entlueftung beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte1f"></a>
### INFOTEXTE1F

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Nehmerzylinder-Mindesthub nicht erreicht |
| 0x7F | Abbruch durch Benutzer |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft, oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte2a"></a>
### INFOTEXTE2A

Dimensions: 4 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm Initialisierung und Pruefung der Eintrittsbedingungen |
| 0x01 | Adaption Kupplungsschleifpunkt |
| 0x7F | Schleifpunktadaption beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte2f"></a>
### INFOTEXTE2F

Dimensions: 8 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler erkannt |
| 0x24 | Getriebedrehzahl beim Anfahren des Einlernbereichs oder Schleifpunkt zu niedrig |
| 0x25 | Keine Getriebedrehzahl bei geschlossener Kupplung |
| 0x26 | Interner Ablauffehler |
| 0x27 | Getriebedrehzahl nach Kupplungsoeffnen nicht in der geforderten Zeit auf Null |
| 0x7F | Abbruch durch Benutzer |
| 0xA0 | Testbedingung nicht erfuellt (Motor ist aus, Gang eingelegt oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte3a"></a>
### INFOTEXTE3A

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm Initialisierung und Pruefung der Eintrittsbedingungen |
| 0x01 | Ermittlung Ventilkennwerte |
| 0x02 | Ermittlung Kupplungs-Lagereglerverstaerkung |
| 0x7F | Adaption Kupplungskennwerte beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte3f"></a>
### INFOTEXTE3F

Dimensions: 9 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler erkannt |
| 0x7F | Abbruch durch Benutzer |
| 0x81 | Einkuppelposition ausserhalb der zulaessigen Toleranz |
| 0x82 | Auskuppelposition ausserhalb der zulaessigen Toleranz |
| 0x83 | Kupplungsventil-Nullstrom ausserhalb der zulaessigen Toleranz |
| 0x84 | Zeitueberschreitung bei Ermittlung der Ventilueberdeckung |
| 0x85 | Ventilueberdeckung ausserhalb der zulaessigen Toleranz |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte4a"></a>
### INFOTEXTE4A

Dimensions: 7 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm Initialisierung |
| 0x01 | Speicher leeren |
| 0x02 | Speicher geleert |
| 0x03 | Speicher befuellen |
| 0x04 | Vorspanndruck bestimmen |
| 0x7F | Vorspanndruchermittlung beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte4f"></a>
### INFOTEXTE4F

Dimensions: 7 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | HE-Temperatur bei Vorspanndruckermittlung ausserhalb der zulaessigen Grenzen |
| 0x02 | Druck beim Speicher leeren nicht in der vorgeschriebenen Zeit unter Mindestschwelle |
| 0x03 | Druck beim Pumpen nicht in der vorgesehenen Zeit ueber Abschaltschwelle |
| 0x7F | Abbruch durch Benutzer |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte5a"></a>
### INFOTEXTE5A

Dimensions: 14 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x14 | Druckaufbau fuer den Ventiltest |
| 0x15 | Es werden die Schaltventile getestet, ob der noetige Strom zum spuelen der Hydraulikleitungen fliessen kann |
| 0x16 | Ermittlung des Leckagedruckabfalls |
| 0x17 | Verringern des Hydraulikdrucks |
| 0x18 | Getriebe in Endlage (5. Gang) bringen |
| 0x19 | Druckaufbau fuer die Waehlwinkelentlueftung |
| 0x1A | Waehlwinkel entlueften |
| 0x1B | Druckaufbau fuer die Schaltwegentlueftung |
| 0x1D | Wartezeit verbringen um Oelverschaeumung abklingen zu lassen |
| 0x1E | Verschlusspruefung des Druckbegrenzungsventils am Waehlwinkelzylinder |
| 0x20 | Schaltwegzylinder fuellen |
| 0x21 | Entlueftung beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte5f"></a>
### INFOTEXTE5F

Dimensions: 8 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Der Ablauf des Automatismus ist nicht korrekt |
| 0x0F | Kein oder zu geringer Hydraulikdruck |
| 0x16 | Hydraulikdruck zu hoch |
| 0x17 | Druckregelventile sind zu warm und der fuer die Entlueftung notwendige Strom kann nicht fliessen |
| 0x18 | Die Endlage (5.Gang) ist nicht einlegbar |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte6a"></a>
### INFOTEXTE6A

Dimensions: 7 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x01 | Kupplung oeffnen |
| 0x28 | Schaltwegmittellage einregeln |
| 0x29 | Schaltwegmittellage ueberpruefen |
| 0x2A | Schaltwegmittellage einlegen beendet |
| 0x02 | Waehlwinkeloffsetstromadaption |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte6f"></a>
### INFOTEXTE6F

Dimensions: 11 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Der Ablauf des Automatismus ist nicht korrekt |
| 0x46 | Die Schaltwegmittellage laesst sich nicht einregeln |
| 0x47 | Der Waehlwinkel laesst sich nicht vom rechten zum linken Anschlag bewegen |
| 0x48 | Der minimale Abstand zwischen linker und rechter Endstellung des Waehlwinkels ist unterschritten |
| 0x49 | Der Wert des WW-Hauptsensors liegt ausserhalb des erlaubten elektrischen Bereiches |
| 0x4A | Der Wert des redundanten WW-Sensors liegt ausserhalb des erlaubten elektrischen Bereiches |
| 0x4C | Grenzwert fuer Wiederholgenauigkeit der WW-Sensoren ueberschritten |
| 0x1E | Kein gueltiger Waehlwinkeloffsetstrom eingelernt |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte7a"></a>
### INFOTEXTE7A

Dimensions: 21 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x01 | Kupplung oeffnen |
| 0x28 | Schaltwegmittellage einregeln |
| 0x29 | Schaltwegmittellage ueberpruefen |
| 0x2A | Schaltwegmittellage einlegen beendet |
| 0x02 | Waehlwinkeloffsetstromadaption |
| 0x03 | Waehlwinkelregler adaptieren |
| 0x04 | Gang 1 ausmessen |
| 0x05 | Gang 2 ausmessen |
| 0x06 | Gang 3 ausmessen |
| 0x07 | Gang 4 ausmessen |
| 0x08 | Gang 5 ausmessen |
| 0x09 | Gang 6 ausmessen |
| 0x0A | Gang R ausmessen |
| 0x0B | Neutralstellung einnehmen |
| 0x0C | In NV-RAM schreiben |
| 0x0D | Einlegehaenger nachbearbeiten |
| 0x0E | Getriebeparameter verarbeiten |
| 0x0F | Getriebe einlernen beenden |
| 0x10 | Gangerkennungssensor adaptieren |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte7f"></a>
### INFOTEXTE7F

Dimensions: 38 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Fehler im Ablauf |
| 0x28 | Die Schaltwegendstellungen der geraden Gaenge sind zu unterschiedlich |
| 0x29 | Die Schaltwegendstellungen der ungeraden Gaenge sind zu unterschiedlich |
| 0x2A | Die Schaltwegendstellung des Rueckwaertsganges zu den anderen ungeraden Gaengen ist zu unterschiedlich |
| 0x2B | Die minimale Fenstergroesse des Rueckeaertsganges wurde unterschritten |
| 0x2C | Die minimale Fenstergroesse des 6.Ganges wurde unterschritten |
| 0x2D | Die minimale Fenstergroesse des 5.Ganges wurde unterschritten |
| 0x2E | Die minimale Fenstergroesse des 4.Ganges wurde unterschritten |
| 0x2F | Die minimale Fenstergroesse des 3.Ganges wurde unterschritten |
| 0x30 | Die minimale Fenstergroesse des 2.Ganges wurde unterschritten |
| 0x31 | Die minimale Fenstergroesse des 1.Ganges wurde unterschritten |
| 0x32 | Die Zeit zum Einregeln der Waehlwinkelmitte ist ueberschritten |
| 0x33 | Minimaler Abstand zwischen Schaltweg gerade Gaenge und ungerade Gaenge ist unterschritten |
| 0x34 | Der Hydraulikdruck ist zu gering |
| 0x35 | Einlegehaenger erkannt |
| 0x36 | Einlegehaenger in Gang 1 vorhanden / Werte wurden substituiert |
| 0x37 | Einlegehaenger in Gang 2 vorhanden / Werte wurden substituiert |
| 0x38 | Einlegehaenger in Gang 3 vorhanden / Werte wurden substituiert |
| 0x39 | Einlegehaenger in Gang 4 vorhanden / Werte wurden substituiert |
| 0x3A | Einlegehaenger in Gang 5 vorhanden / Werte wurden substituiert |
| 0x3B | Einlegehaenger in Gang 6 vorhanden / Werte wurden substituiert |
| 0x3C | Einlegehaenger in Rueckwaertsgang vorhanden / Werte wurden substituiert |
| 0x3D | Mindestens einer der eingelernten Parameter liegt ausserhalb des erlaubten Toleranzbereiches |
| 0x3E | Schaltweg zu weit ausgerueckt |
| 0x40 | Der SW-Hauptsensor liegt ausserhalb des erlaubten elektrischen Bereiches |
| 0x41 | Der redundante SW-Sensor liegt ausserhalb des erlaubten elektrischen Bereiches |
| 0x46 | Die Schaltwegmitte laesst sich nicht einregeln |
| 0x47 | Der Waehlwinkel laesst sich nicht vom rechten zum linken Anschlag bewegen |
| 0x48 | Der minimale Abstand zwischen linker und rechter Endstellung des Waehlwinkels ist unterschritten |
| 0x49 | Der WW-Wert des Hauptsensors liegt ausserhalb des erlaubten elektrischen Bereiches |
| 0x4A | Der WW-Wert des redundanten Hauptsensors liegt ausserhalb des erlaubten elektrischen Bereiches |
| 0x4C | Grenzwerte fuer Wiederholgenaugikeit der WW-Sensoren ueberschritten |
| 0x64 | Bereichsfehler des gemittelten Deltas zwischen den Schaltwegspuren |
| 0x65 | Deltafehler zwischen den Waehlwinkelspuren |
| 0x66 | Bereichsfehler des gemittelten Deltas zwischen den Schaltwegspuren |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte8a"></a>
### INFOTEXTE8A

Dimensions: 8 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x01 | Initialisierung |
| 0x02 | Ersten Wert ermitteln |
| 0x03 | Zeit zwischen zwei Werten abwarten |
| 0x04 | Folgewerte mit 1. Wert vergleichen |
| 0x05 | Offset berechnen |
| 0x06 | Offsetermittlung beenden |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte8f"></a>
### INFOTEXTE8F

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x5A | Eingelernter Wert ausserhalb des fuer Laengsbeschleunigung zulaessigen Bereichs |
| 0x5B | Offset des Laengsbeschleunigungssensors in vorgesehener Zeit nicht erfolgreich eingelernt |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte9a"></a>
### INFOTEXTE9A

Dimensions: 6 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x01 | Kupplung oeffnen |
| 0x28 | Schaltwegmittellage einregeln |
| 0x29 | Schaltwegmittellage ueberpruefen |
| 0x2A | Schaltwegmittellage einlegen beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte9f"></a>
### INFOTEXTE9F

Dimensions: 10 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Der Ablauf des Automatismus ist nicht korrekt |
| 0x46 | Die Schaltwegmittellage laesst sich nicht einregeln |
| 0x47 | Der Waehlwinkel laesst sich nicht vom rechten zum linken Anschlag bewegen |
| 0x48 | Der minimale Abstand zwischen linker und rechter Endstellung des Waehlwinkels ist unterschritten |
| 0x49 | Der WW-Wert des Hauptsensors liegt ausserhalb des erlaubten elektrischen Bereiches |
| 0x4A | Der WW-Wert des redundanten Sensors liegt ausserhalb des erlaubten elektrischen Bereiches |
| 0x4C | Grenzwerte fuer Wiederholgenaugikeit der WW-Sensoren ueberschritten |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte10a"></a>
### INFOTEXTE10A

Dimensions: 6 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x3D | Initialisierung der Funktion |
| 0x3E | Gewuenschten Gang als Zielgang setzen |
| 0x3F | Zeit zum Gangeinlegen abwarten |
| 0x40 | Beliebigen Gang einlegen ist beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte10f"></a>
### INFOTEXTE10F

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x50 | Das Einlegen des gewuenschten Ganges ist gescheitert |
| 0x51 | Ungueltige Gangvorgabe |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte11a"></a>
### INFOTEXTE11A

Dimensions: 19 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x01 | Kupplung oeffnen |
| 0x28 | Schaltwegmittellage einregeln |
| 0x29 | Schaltwegmittellage ueberpruefen |
| 0x2A | Schaltwegmittellage einlegen beendet |
| 0x04 | Gang 1 ausmessen |
| 0x05 | Gang 2 ausmessen |
| 0x06 | Gang 3 ausmessen |
| 0x07 | Gang 4 ausmessen |
| 0x08 | Gang 5 ausmessen |
| 0x09 | Gang 6 ausmessen |
| 0x0A | Gang R ausmessen |
| 0x0B | Neutralstellung einnehmen |
| 0x0C | Adaptionswerte in NV-RAM schreiben |
| 0x0D | Einlegehaenger nachbearbeiten |
| 0x0E | Getriebeparameter verarbeiten |
| 0x0F | Getriebe einlernen beenden |
| 0x10 | Gangerkennungssensor adaptieren |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte11f"></a>
### INFOTEXTE11F

Dimensions: 38 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Fehler im Ablauf |
| 0x28 | Die Schaltwegendstellungen der geraden Gaenge sind zu unterschiedlich |
| 0x29 | Die Schaltwegendstellungen der ungeraden Gaenge sind zu unterschiedlich |
| 0x2A | Die Schaltwegendstellung des Rueckwaertsganges zu den anderen ungeraden Gaengen ist zu unterschiedlich |
| 0x2B | Die minimale Fenstergroesse des Rueckeaertsganges wurde unterschritten |
| 0x2C | Die minimale Fenstergroesse des 6.Ganges wurde unterschritten |
| 0x2D | Die minimale Fenstergroesse des 5.Ganges wurde unterschritten |
| 0x2E | Die minimale Fenstergroesse des 4.Ganges wurde unterschritten |
| 0x2F | Die minimale Fenstergroesse des 3.Ganges wurde unterschritten |
| 0x30 | Die minimale Fenstergroesse des 2.Ganges wurde unterschritten |
| 0x31 | Die minimale Fenstergroesse des 1.Ganges wurde unterschritten |
| 0x32 | Die Zeit zum Einregeln der Waehlwinkelmitte ist ueberschritten |
| 0x33 | Minimaler Abstand zwischen Schaltweg gerade Gaenge und ungerade Gaenge ist unterschritten |
| 0x34 | Der Hydraulikdruck ist zu gering |
| 0x35 | Einlegehaenger erkannt |
| 0x36 | Einlegehaenger in Gang 1 vorhanden / Werte wurden substituiert |
| 0x37 | Einlegehaenger in Gang 2 vorhanden / Werte wurden substituiert |
| 0x38 | Einlegehaenger in Gang 3 vorhanden / Werte wurden substituiert |
| 0x39 | Einlegehaenger in Gang 4 vorhanden / Werte wurden substituiert |
| 0x3A | Einlegehaenger in Gang 5 vorhanden / Werte wurden substituiert |
| 0x3B | Einlegehaenger in Gang 6 vorhanden / Werte wurden substituiert |
| 0x3C | Einlegehaenger in Rueckwartsgang vorhanden / Werte wurden substituiert |
| 0x3D | Mindestens einer der eingelernten Parameter liegt ausserhalb des erlaubten Toleranzbereiches |
| 0x3E | Schaltweg zu weit ausgerueckt |
| 0x40 | Schaltweg Haupsensorwert ausserhalb der Grenze fuer elektrischen Bereich |
| 0x41 | Schaltweg red. Sensorwert ausserhalb der Grenze fuer elektrischen Bereich |
| 0x46 | Die Schaltwegmitte laesst sich nicht einregeln |
| 0x47 | Der Waehlwinkel laesst sich nicht vom rechten zum linken Anschlag bewegen |
| 0x48 | Der Minimale Abstand zwischen linker und rechter Endstellung des Waehlwinkels ist unterschritten |
| 0x49 | Waehlwinkel Hauptsensorwert ausserhalb der Grenze fuer elektrischen Bereich |
| 0x4A | Waehlwinkel red. Sensorwert ausserhalb der Grenze fuer elektrischen Bereich |
| 0x4C | Potiwerte Waehlwinkel Haupt- und red. Sensor passen nich zueinander |
| 0x64 | 0x64 Fehler einlernen Gangerkennungs Sensor |
| 0x65 | 0x65 Fehler einlernen Gangerkennungs Sensor |
| 0x66 | Bereichsfehler des gemittelten Deltas zwischen den Schaltwegspuren |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte12a"></a>
### INFOTEXTE12A

Dimensions: 4 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x29 | Schaltwegmittellage ueberpruefen |
| 0x2A | Schaltwegmittellage ueberpruefen beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte12f"></a>
### INFOTEXTE12F

Dimensions: 8 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Fehler im Ablauf |
| 0x48 | Abstand zw. Waehlwinkelanschlag links und rechts zu klein |
| 0x49 | Der WW-Wert des Hauptsensors liegt ausserhalb des erlaubten elektrischen Bereiches |
| 0x4A | WW-Wert des redundanten Sensors liegt ausserhalb des erlaubten elektrischen Bereiches |
| 0x4C | Grenzwert fuer Wiederholgenauigkeit der WW-Sensoren ueberschritten |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte13a"></a>
### INFOTEXTE13A

Dimensions: 8 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x01 | Kupplung oeffnen |
| 0x28 | Schaltwegmittellage einregeln |
| 0x29 | Schaltwegmittellage ueberpruefen |
| 0x2A | Schaltwegmittellage ueberpruefen beendet |
| 0x10 | Gangerkennung Waehlwinkel einregeln |
| 0x11 | Gangerkennung Waehlwinkel einregeln Ende |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte13f"></a>
### INFOTEXTE13F

Dimensions: 11 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Der Ablauf des Automatismus ist nicht korrekt |
| 0x46 | Die Schaltwegmittellage laesst sich nicht einregeln |
| 0x47 | Der Waehlwinkel laesst sich nicht vom rechten zum linken Anschlag bewegen |
| 0x48 | Der minimale Abstand zwischen linker und rechter Endstellung des Waehlwinkels ist unterschritten |
| 0x49 | Der WW-Wert des Hauptsensors liegt ausserhalb des erlaubten elektrischen Bereiches |
| 0x4A | Der WW-Wert des redundanten Sensors liegt ausserhalb des erlaubten elektrischen Bereiches |
| 0x4C | Grenzwert fuer Wiederholgenauigkeit der WW-Sensoren ueberschritten |
| 0x64 | Bereichsfehler des gemittelten Deltas zwischen den Waehlwinkelspuren |
| 0x65 | Deltafehler zwischen den Waehlwinkelspuren |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte21a"></a>
### INFOTEXTE21A

Dimensions: 4 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm Initialisierung und Pruefung der Eintrittsbedingungen |
| 0x01 | Ermittlung Ventilkennwerte |
| 0x7F | Adaption Kupplungskennwerte beendet, Startbedingung fuer Motor hergestellt |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte21f"></a>
### INFOTEXTE21F

Dimensions: 8 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x81 | Einkuppelposition ausserhalb der zulaessigen Toleranz |
| 0x82 | Auskuppelposition ausserhalb der zulaessigen Toleranz |
| 0x83 | Kupplungsventil-Nullstrom ausserhalb der zulaessigen Toleranz |
| 0x84 | Zeitueberschreitung bei Ermittlung der Ventilueberdeckung |
| 0x85 | Ventilueberdeckung ausserhalb der zulaessigen Toleranz |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-hinterachsuebersetzung"></a>
### HINTERACHSUEBERSETZUNG

Dimensions: 17 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Hinterachsuebersetzung 1; Standard: 1:3,64 |
| 0x01 | Hinterachsuebersetzung 2 |
| 0x02 | Hinterachsuebersetzung 3 |
| 0x03 | Hinterachsuebersetzung 4 |
| 0x04 | Hinterachsuebersetzung 5 |
| 0x05 | Hinterachsuebersetzung 6 |
| 0x06 | Hinterachsuebersetzung 7 |
| 0x07 | Hinterachsuebersetzung 8 |
| 0x08 | Hinterachsuebersetzung 9 |
| 0x09 | Hinterachsuebersetzung 10 |
| 0x0A | Hinterachsuebersetzung 11 |
| 0x0B | Hinterachsuebersetzung 12 |
| 0x0C | Hinterachsuebersetzung 13 |
| 0x0D | Hinterachsuebersetzung 14 |
| 0x0E | Hinterachsuebersetzung 15 |
| 0x0F | Hinterachsuebersetzung 16 |
| 0xXY | nicht definiert |

<a id="table-infotextefahrzeugzustand"></a>
### INFOTEXTEFAHRZEUGZUSTAND

Dimensions: 48 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Keine Systemfreigabe |
| 0x01 | Motor aus, Fahrzeug steht |
| 0x02 | Eingekuppelt |
| 0x03 | Abwuergen |
| 0x04 | Anhalten |
| 0x05 | Anschleppen |
| 0x06 | Abschalten |
| 0x07 | Antiblockiersystem |
| 0x08 | Antriebsschlupfregelung |
| 0x09 | Nebenantrieb |
| 0x0A | Keine Druckluft |
| 0x0B | Starten |
| 0x0C | Abschalten ohne Systemfreigabe |
| 0x10 | Einkuppeln, Schub |
| 0x11 | Einkuppeln, Zug |
| 0x12 | Einkuppeln, Synchron |
| 0x13 | Einkuppeln, Ueberdrehzahl |
| 0x14 | Einkuppeln, Zug, Sport |
| 0x15 | Einkuppeln, Schub, Sport |
| 0x16 | Einkuppeln, Radabriss |
| 0x17 | Einkuppeln, Schub, Eingriff |
| 0x18 | Einkuppeln, Eingriff |
| 0x20 | Anfahren, Vorweg |
| 0x21 | Anfahren, Normal |
| 0x22 | Anfahren, Kick Down |
| 0x23 | Anfahren, Synchron |
| 0x24 | Anfahren, Rennstart |
| 0x25 | Anfahrhilfe |
| 0x26 | Rennstart vorbereiten |
| 0x27 | Anfahren, Moment |
| 0x30 | Schalten |
| 0x40 | Neutral ohne Einlernen, GW |
| 0x41 | Neutral Einlernen, GW |
| 0x42 | Neutral Einlernen GW beendet |
| 0x43 | Neutral, Fahrzeug steht |
| 0x50 | Verschalten, Zug Normal |
| 0x51 | Verschalten, Zug Extrem |
| 0x52 | Verschalten, Zug Synchron |
| 0x60 | Anrollen |
| 0x70 | Notfahr FP Kuppeln |
| 0x71 | Notfahr N Mot Kuppeln |
| 0x72 | System abschalten |
| 0x80 | Schlupf |
| 0x90 | Ansynchronisieren |
| 0x91 | Ansynchronisieren beendet |
| 0xA0 | KKL Einlernen |
| 0xA1 | KKL Einlernen beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-fgr"></a>
### FGR

Dimensions: 9 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | FGR passiv |
| 0x01 | FGR aktiv, Konstantfahrt |
| 0x02 | ACC-Regelung Standard |
| 0x03 | FGR aktiv, Wiederaufnahme |
| 0x04 | ACC-Regelung erhoehte Dynamik |
| 0x05 | FGR aktiv, Setzen/Beschleunigen |
| 0x06 | FGR/ACC-Abschaltung |
| 0x07 | FGR aktiv, Verzoegern |
| 0xXY | nicht definiert |

<a id="table-freeze-frame-referenz"></a>
### FREEZE_FRAME_REFERENZ

Dimensions: 6 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Kein Freeze Frame gespeichert |
| 0x01 | Freeze Frame wird verwaltet fuer DME (Master) |
| 0x02 | Freeze Frame wird verwaltet fuer EGS od. SMG |
| 0x03 | Freeze Frame wird verwaltet fuer EML |
| 0x04 | Freeze Frame wird verwaltet fuer DME links |
| 0xXY | nicht definiert |

<a id="table-programminfo"></a>
### PROGRAMMINFO

Dimensions: 7 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x01 | 1. Programm |
| 0x02 | 2. Programm |
| 0x03 | 3. Programm |
| 0x04 | 4. Programm |
| 0x05 | 5. Programm |
| 0x06 | 6. Programm |
| 0xXY | nicht definiert |

<a id="table-komfortindex"></a>
### KOMFORTINDEX

Dimensions: 14 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | komfortabel |
| 0x01 | komfortabel+1 |
| 0x02 | komfortabel+2 |
| 0x03 | komfortabel+3 |
| 0x04 | komfortabel+4 |
| 0x05 | komfortabel+5 |
| 0x06 | normal |
| 0x07 | sportiv-5 |
| 0x08 | sportiv-4 |
| 0x09 | sportiv-3 |
| 0x0A | sportive-2 |
| 0x0B | sportiv-1 |
| 0x0C | sportiv |
| 0xXY | nicht definiert |

<a id="table-ganganzeige"></a>
### GANGANZEIGE

Dimensions: 12 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | 0/Neutral |
| 0x01 | 1.Gang |
| 0x02 | 2.Gang |
| 0x03 | 3.Gang |
| 0x04 | 4.Gang |
| 0x05 | 5.Gang |
| 0x06 | 6.Gang |
| 0x07 | Rueckwaertsgang |
| 0x08 | Anzeige dunkel |
| 0x09 | Automat |
| 0x0F | Testfunktion (alle an) |
| 0xFF | nicht definiert |

<a id="table-waehlhebelanzeige"></a>
### WAEHLHEBELANZEIGE

Dimensions: 15 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Anzeige dunkel |
| 0x01 | 0 |
| 0x02 | R |
| 0x03 | A+ |
| 0x04 | A- |
| 0x05 | A+/- |
| 0x06 | S+ |
| 0x07 | S- |
| 0x08 | S+/- |
| 0x09 | + |
| 0x0A | - |
| 0x0B | +/- |
| 0x0C | A (Automat) |
| 0x0F | Testfunktion (alle an) |
| 0xFF | nicht definiert |

<a id="table-led"></a>
### LED

Dimensions: 4 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Keine LED |
| 0x01 | 1. LED |
| 0x02 | 1. und 2. LED |
| 0xXY | nicht definiert |
