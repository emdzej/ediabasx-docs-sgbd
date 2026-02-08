# VM5IBUS.prg

- Jobs: [34](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Videomodul VM5IBus VM_Hybrid_Ibus VM5_IBus_Cam |
| ORIGIN | BMW EE-41 Lamberty |
| REVISION | 1.04 |
| AUTHOR | Lear DCS Bayreuther,BMW TI-431 Rochal, |
| COMMENT | Videomodul VM5IBUS VM_HYBRID_IBUS VM5_IBUS_CAM |
| PACKAGE | 1.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [POWERDOWN_MODE](#job-powerdown-mode) - SG in PowerDown-Mode versetzen
- [INITIALISIERUNG](#job-initialisierung) - Init-Job Videomodul TV-Teil
- [IDENT](#job-ident) - Ident-Daten fuer Videomodul TV-Teil
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low Konzept ohne Umweltbedingung
- [IS_LESEN](#job-is-lesen) - Shadowspeicher lesen
- [Pruefstempel_lesen](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Daten in den Pruefstempel schreiben
- [Speicher_lesen](#job-speicher-lesen) - Lesen, welche Parameter geladen sind
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen im Videomodul TV-Teil
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - Selbsttest des Videomoduls Uebergabe eines Arguments nur bei VM5IBus ab SW12 und VM_HYBRID_IBUS Bei VM_HYBRID_IBUS und bei VM5IBUS ab SW16 (VM5_IBUS_CAM) sind waehrend diesen Tests weitere Diagnosefunktionen moeglich.
- [SG_STATUS_LESEN](#job-sg-status-lesen) - Stati lesen am Videomodul TV-Teil
- [STEUERN_EINZELTEST_ANTENNEN](#job-steuern-einzeltest-antennen) - Job nur fuer VM_HYBRID_IBUS Pruefung der Fernspeisung des Videomoduls Pruefung des Antennenstroms  des Videomoduls
- [SG_STATUS_EINZELTEST_ANTENNEN](#job-sg-status-einzeltest-antennen) - Job nur fuer VM_HYBRID_IBUS Ergebnis des Antennentests
- [SG_ST_MESSWERTE_LESEN](#job-sg-st-messwerte-lesen) - SG Lesen der aktuellen Messwerte nach Selbsttest
- [SG_VORGABE_ANALOG_TV_KANAL](#job-sg-vorgabe-analog-tv-kanal) - Umschalten eines analogen Kanals und dessen Norm Job fuer VM5Ibus ab SW 11 und VM_HYBRID_IBUS Argument_1 Kanal (Bereich von 1 bis 99) Argument_2 Norm  (Bereich von 2 bis 21)  Wird Argument 2 (Norm) nicht uebergeben, dann ist automatisch PAL BG eingestellt. Es muss vor Aufruf des Jobs auf TV umgeschaltet werden. Jetzt darf das VM_Hybrid_IBus nicht auf einem digitalen Kanal stehen, da mit diesem Job nur analoge Kanaele umgeschaltet werden koennen.  Argument 1  Kanal 1..99 Argument 2  TV-Norm 2     NTSC_M 3     NTSC JAPAN 4     PAL_BG 5     PAL_BG (default) 6     PAL_I 7     PAL_M 8     PAL_N 9     PAL_DK 10    PAL AUSTRALIA 11    PAL ITALIA 12    PAL MOROCCO 13    PAL_DK OIRT 14    PAL NEWZEALAND 15    PAL CHINA 16    SECAM_BG 17    SECAM_DK 18    SECAM_K1 19    SECAM_L FRANCE 20    SECAM MOROCCO 21    PAL_BG OIRT 
- [STEUERN_CHANNEL_SET](#job-steuern-channel-set) - Aufschalten eines analogen oder digitalen Kanals Job nur fuer VM_HYBRID_IBUS ab SW 18 Kanal (Bereich von 1 bis 99)  Hinweis: kann bis zu mehreren Sekunden andauern mit STATUS_CHANNEL_SET abfragen ob Abstimmung fertig Argument Kanal 1..99
- [STATUS_CHANNEL_SET](#job-status-channel-set) - Abfrage Tunerabstimmung Job nur fuer VM_HYBRID_IBUS ab SW 18
- [STATUS_BITERROR_RATE](#job-status-biterror-rate) - Abfrage BER nach Viterbi Job nur fuer VM_HYBRID_IBUS ab SW 18 Die Ausgabe erfolgt in 4 Empfangsstufen VM muss auf einen digitalem Kanal eingestellt werden BER-Werte nur für Digitalempfang
- [STEUERN_TESTBILD](#job-steuern-testbild) - Job fuer VM_HYBRID_IBUS ab SW18 und fuer VM5IBUS (VM5_IBUS_CAM) ab SW 16 Starten des Testbilds fuer 1..30 Sekunden Valid Time Argument: Argument: 0 = Testbild aus Argument: 1...30  = Testbild 1...30 Sekunden
- [CODIERUNG_LAENDERVARIANTE_LESEN](#job-codierung-laendervariante-lesen) - Speicher lesen EEPROM
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [C_S_AUFTRAG](#job-c-s-auftrag) - Codierdaten schreiben und verifizieren
- [C_S_LESEN](#job-c-s-lesen) - Codierdaten lesen
- [CS_BILDEN](#job-cs-bilden)
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen des Pruefstempels und Interpretation als FG-Nummer
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Beschreiben des Pruefstempels mit der FG-Nummer
- [MODUL_INFO](#job-modul-info) - MODUL-Info-Daten fuer Videomodul TV-Teil
- [NEC_MONITOR_TYP_BASISBETRIEB](#job-nec-monitor-typ-basisbetrieb) - NEC-Monitor-Typ Umschaltung (4:3 Monitor). Job nur bei Anzeigeproblemen mit GT-BASIS-Konfiguration. Bei Problemen wg. Helligkeitspumpen und Ruecklauflinien im Hauptmenue
- [STEUERN_JMC_BLANKING](#job-steuern-jmc-blanking) - Schwarzes Fenster links oder rechts des Bildes Kamera muss zugeschaltet sein Job nur fuer VM5IBUS (VM5_IBUS_CAM) ab SW 16  Argument1: schwarzer Balken links erhoehen    = 1 Argument1: schwarzer Balken links verringern  = 2 Argument1: schwarzer Balken rechts erhoehen   = 3 Argument1: schwarzer Balken rechts verringern = 4 Argument1: Normalstellung links               = 5 Argument1: Normalstellung rechts              = 6
- [STEUERN_JMC_SETTINGS](#job-steuern-jmc-settings) - Aendern von Kontrast, Helligkeit, Farbe oder Tint Job nur fuer VM5IBUS (VM5_IBUS_CAM) ab SW 16 JMC muss eingeschaltet sein Argument1: Kontrast           = 1 Argument1: Helligkeit         = 2 Argument1: Farbe              = 3 Argument1: Tint (bei NTSC)    = 4 Argument1: Werte lesen        = 5 ( Kein Argument2 notwendig) Argument1: Grundeinstellung   = 6 ( Kein Argument2 notwendig) Argument2: Bereich von 1 bis 100 Prozent
- [STEUERN_JMCTEST](#job-steuern-jmctest) - MirrorCam-Test des Videomoduls Uebergabe eines Arguments Abfrage der Ergebnisse mit STATUS_JMCTEST Job nur fuer VM5IBUS (VM5_IBUS_CAM) ab SW16
- [STATUS_JMCTEST](#job-status-jmctest) - Job nur fuer VM5IBUS (VM5_IBUS_CAM) ab SW 16 Ergebnisse des MirrorCam-Tests STEUERN_JMCTEST oder STEUERN_SELBSTTEST muss vorher gesendet werden

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

<a id="job-energiesparmode"></a>
### ENERGIESPARMODE

Einstellen des Energiesparmodes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PRODUKTIONSMODE | string | "ein" -&gt; Produktions Mode ein "aus" -&gt; Produktions Mode aus table DigitalArgument TEXT Default: "aus" |
| TRANSPORTMODE | string | "ein" -&gt; Transport Mode ein "aus" -&gt; Transport Mode aus table DigitalArgument TEXT Default: "aus" |
| WERKSTATTMODE | string | "ein" -&gt; Werkstatt Mode ein "aus" -&gt; Werkstatt Mode aus table DigitalArgument TEXT Default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-powerdown-mode"></a>
### POWERDOWN_MODE

SG in PowerDown-Mode versetzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | real | Zeit nach der das Steuergerät einschläft Bereich   : 0.5 bis 20.0 [Sekunden] Auflösung : 0.5 [Sekunden] =&gt; zeitgesteuerter Power-Down (0x9B) wird aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job Videomodul TV-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer Videomodul TV-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Normalerweise "OKAY" |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | string | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | string | Bus-Index |
| ID_DATUM_KW | string | Herstelldatum: Woche |
| ID_DATUM_JAHR | string | Herstelldatum: Jahr |
| ID_LIEF_NR | string | Lieferant-Nummer |
| ID_LIEF_TEXT | string | Lieferant im Klartext |
| ID_SW_NR | string | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low Konzept ohne Umweltbedingung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ORT_NR | int | Ausgabe Fehlernummer |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingen, hier 0 |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-is-lesen"></a>
### IS_LESEN

Shadowspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ORT_NR | int | Ausgabe Fehlernummer |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingen, hier 0 |
| _TEL_ANTWORT | binary | Telegramm anzeigen |

<a id="job-pruefstempel-lesen"></a>
### Pruefstempel_lesen

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Daten in den Pruefstempel schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise "OKAY" |
| _TEL_SENDE | binary |  |

<a id="job-speicher-lesen"></a>
### Speicher_lesen

Lesen, welche Parameter geladen sind

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT_AUSWAHL | int | Angabe, welches Speichermedium ausgelesen werden soll |
| START_ADRESSE_HIGH | int | Startadresse high als Hexwert |
| START_ADRESSE_MIDDLE | int | Startadresse middle als Hexwert |
| START_ADRESSE_LOW | int | Startadresse low als Hexwert |
| ANZAHL_BYTE | int | Angabe, wieviele Bytes ausgelesen werden sollen maximale Anzahl 27 Byte, entspricht 1B Hex |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise "OKAY" |
| SEGMENT_TEXT | string | Text Segmentauswahl |
| DATEN | binary | angeforderter Datenblock |
| BYTE_ANZAHL | int | Eingabe, wieviel Byte ausgelesen werden sollen |
| EINGABEFEHLER | string | Fehlertextausgabe bei Eingabe &gt;27 Byte |
| _TEL_SENDE | binary | gesendetes Telegramm |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen im Videomodul TV-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

Selbsttest des Videomoduls Uebergabe eines Arguments nur bei VM5IBus ab SW12 und VM_HYBRID_IBUS Bei VM_HYBRID_IBUS und bei VM5IBUS ab SW16 (VM5_IBUS_CAM) sind waehrend diesen Tests weitere Diagnosefunktionen moeglich.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_1 | int | 0 = Rueckgabe des Acknowledge vor Testbeginn (Test 0) 1 = Rueckgabe des Acknowledge nach Testende (Test 1) wenn kein Argument uebergeben wird, wird Test 0 durchgefuehrt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_ANTWORT | binary |  |
| _TEL_SENDE | binary |  |

<a id="job-sg-status-lesen"></a>
### SG_STATUS_LESEN

Stati lesen am Videomodul TV-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweiser OKAY |
| STAT_ROT_OUT | string | Ausgabe Testergebnis |
| STAT_ROT_OUT_WERT | int | Ausgabe Testergebnis |
| STAT_GRUEN_OUT | string | Ausgabe Testergebnis |
| STAT_GRUEN_OUT_WERT | int | Ausgabe Testergebnis |
| STAT_BLAU_OUT | string | Ausgabe Testergebnis |
| STAT_BLAU_OUT_WERT | int | Ausgabe Testergebnis |
| STAT_ROT_IN | string | Ausgabe Testergebnis |
| STAT_ROT_IN_WERT | int | Ausgabe Testergebnis |
| STAT_GRUEN_IN | string | Ausgabe Testergebnis |
| STAT_GRUEN_IN_WERT | int | Ausgabe Testergebnis |
| STAT_BLAU_IN | string | Ausgabe Testergebnis |
| STAT_BLAU_IN_WERT | int | Ausgabe Testergebnis |
| STAT_FS | string |  |
| STAT_FS_WERT | int |  |
| STAT_XSYNC | string |  |
| STAT_XSYNC_WERT | int |  |
| STAT_CVBS_FOND | string |  |
| STAT_CVBS_FOND_WERT | int |  |
| STAT_CVBS_CAM | string |  |
| STAT_CVBS_CAM_WERT | int |  |
| STAT_CVBS_VCR | string |  |
| STAT_CVBS_VCR_WERT | int |  |
| STAT_CVBS_TUNER | string |  |
| STAT_CVBS_TUNER_WERT | int |  |
| STAT_AF_FOND | string |  |
| STAT_AF_FOND_WERT | int |  |
| STAT_AF_VCR | string |  |
| STAT_AF_VCR_WERT | int |  |
| STAT_AF_RADIO | string |  |
| STAT_AF_RADIO_WERT | int |  |
| STAT_AF_NAV | string |  |
| STAT_AF_NAV_WERT | int |  |
| STAT_ANTENNE1 | string | nur VM_HYBRID_IBUS |
| STAT_ANTENNE1_WERT | int | nur VM_HYBRID_IBUS |
| STAT_ANTENNE2 | string | nur VM_HYBRID_IBUS |
| STAT_ANTENNE2_WERT | int | nur VM_HYBRID_IBUS |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-einzeltest-antennen"></a>
### STEUERN_EINZELTEST_ANTENNEN

Job nur fuer VM_HYBRID_IBUS Pruefung der Fernspeisung des Videomoduls Pruefung des Antennenstroms  des Videomoduls

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_1 | int | 0 = Fernspeisespannung / -Strom  Ackn. vor Testbeginn 1 = Fernspeisespannung / -Strom  Ackn. nach Testende bei Test 0 erfolgt bei Messbeginn ein Acknowledge bei Test 1 erfolgt nach Messende ein Acknowledge wenn kein Argument uebergeben wird, wird Test 0 durchgefuehrt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_ANTWORT | binary |  |
| _TEL_SENDE | binary |  |

<a id="job-sg-status-einzeltest-antennen"></a>
### SG_STATUS_EINZELTEST_ANTENNEN

Job nur fuer VM_HYBRID_IBUS Ergebnis des Antennentests

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweiser OKAY |
| STAT_FS | string | nur VM_HYBRID_IBUS |
| STAT_ANTENNE1 | string | nur VM_HYBRID_IBUS |
| STAT_FS_WERT | int | nur VM_HYBRID_IBUS |
| STAT_ANTENNE1_WERT | int | nur VM_HYBRID_IBUS |
| STAT_ANTENNE2 | string | nur VM_HYBRID_IBUS |
| STAT_ANTENNE2_WERT | int | nur VM_HYBRID_IBUS |
| _TEL_ANTWORT | binary |  |

<a id="job-sg-st-messwerte-lesen"></a>
### SG_ST_MESSWERTE_LESEN

SG Lesen der aktuellen Messwerte nach Selbsttest

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TESTAUSWAHL | int | Testauswahl 0x91 oder 145 dezimal = RGB Messwerte Testauswahl 0x92 oder 146 dezimal = CVBS Messwerte Testauswahl 0x93 oder 147 dezimal = TON Messwerte Testauswahl 0x94 oder 148 dezimal = FSU/I Messwerte (nur Hybrid) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sg-vorgabe-analog-tv-kanal"></a>
### SG_VORGABE_ANALOG_TV_KANAL

Umschalten eines analogen Kanals und dessen Norm Job fuer VM5Ibus ab SW 11 und VM_HYBRID_IBUS Argument_1 Kanal (Bereich von 1 bis 99) Argument_2 Norm  (Bereich von 2 bis 21)  Wird Argument 2 (Norm) nicht uebergeben, dann ist automatisch PAL BG eingestellt. Es muss vor Aufruf des Jobs auf TV umgeschaltet werden. Jetzt darf das VM_Hybrid_IBus nicht auf einem digitalen Kanal stehen, da mit diesem Job nur analoge Kanaele umgeschaltet werden koennen.  Argument 1  Kanal 1..99 Argument 2  TV-Norm 2     NTSC_M 3     NTSC JAPAN 4     PAL_BG 5     PAL_BG (default) 6     PAL_I 7     PAL_M 8     PAL_N 9     PAL_DK 10    PAL AUSTRALIA 11    PAL ITALIA 12    PAL MOROCCO 13    PAL_DK OIRT 14    PAL NEWZEALAND 15    PAL CHINA 16    SECAM_BG 17    SECAM_DK 18    SECAM_K1 19    SECAM_L FRANCE 20    SECAM MOROCCO 21    PAL_BG OIRT 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_1 | int | Argument entspricht dem einzustellenden Kanal zulaessiger Bereich von 1 bis 99 |
| ARGUMENT_2 | int | Argument entspricht der länderabhängigen Norm zulaessiger Bereich von 2 bis 21 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_ANTWORT | binary |  |
| _TEL_SENDE | binary |  |

<a id="job-steuern-channel-set"></a>
### STEUERN_CHANNEL_SET

Aufschalten eines analogen oder digitalen Kanals Job nur fuer VM_HYBRID_IBUS ab SW 18 Kanal (Bereich von 1 bis 99)  Hinweis: kann bis zu mehreren Sekunden andauern mit STATUS_CHANNEL_SET abfragen ob Abstimmung fertig Argument Kanal 1..99

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_1 | int | Argument entspricht dem einzustellenden Kanal zulaessiger Bereich von 1 bis 99 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_SENDE | binary | Sendetelegramm |

<a id="job-status-channel-set"></a>
### STATUS_CHANNEL_SET

Abfrage Tunerabstimmung Job nur fuer VM_HYBRID_IBUS ab SW 18

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CODE | int | Fehlercode |
| STAT_CODE_TXT | string | Fehlercode |
| STAT_CHANNEL | int | eingestellter Kanal |
| STAT_ANALOG_DIGITAL | int | Analog oder Digitalkanal |
| STAT_ANALOG_DIGITAL_TXT | string | Analog oder Digital |
| _TEL_ANTWORT | binary |  |

<a id="job-status-biterror-rate"></a>
### STATUS_BITERROR_RATE

Abfrage BER nach Viterbi Job nur fuer VM_HYBRID_IBUS ab SW 18 Die Ausgabe erfolgt in 4 Empfangsstufen VM muss auf einen digitalem Kanal eingestellt werden BER-Werte nur für Digitalempfang

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_VBER_TXT | string | Info |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-testbild"></a>
### STEUERN_TESTBILD

Job fuer VM_HYBRID_IBUS ab SW18 und fuer VM5IBUS (VM5_IBUS_CAM) ab SW 16 Starten des Testbilds fuer 1..30 Sekunden Valid Time Argument: Argument: 0 = Testbild aus Argument: 1...30  = Testbild 1...30 Sekunden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TIME | int | value 00 to 30 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SENDE | binary | Sendetelegramm |

<a id="job-codierung-laendervariante-lesen"></a>
### CODIERUNG_LAENDERVARIANTE_LESEN

Speicher lesen EEPROM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| COD_LAENDERVARIANTE_TEXT | string | ECE, GB , US oder unbekannt |
| COD_LAENDERVARIANTE_WERT | int |  |
| ID_COD_INDEX | int | aus Id-lesen |
| _TEL_ANTWORT | binary |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY" |

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

<a id="job-c-s-lesen"></a>
### C_S_LESEN

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

<a id="job-cs-bilden"></a>
### CS_BILDEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

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

<a id="job-modul-info"></a>
### MODUL_INFO

MODUL-Info-Daten fuer Videomodul TV-Teil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Normalerweise "OKAY" |
| VM_SW_NR_EXTERNAL | string | Externe Softwarenummer |
| VM_SW_NR_INTERNAL | string | Interne Softwarenummer |
| VM_SW_NR_INTERNAL_INT | int | Interne Softwarenummer als INTEGER |
| VM_IDENTIFICATION | string | Videomodulkennung |
| VM_IDENTIFICATION_NAME | string | Videomodulname falls bekannt |
| VM_EEPROM_LAYOUT | string | EE-Layoutkennung |
| VM_EEPROM_INDEX | string | EE-Layout-Index |
| _TEL_ANTWORT | binary |  |

<a id="job-nec-monitor-typ-basisbetrieb"></a>
### NEC_MONITOR_TYP_BASISBETRIEB

NEC-Monitor-Typ Umschaltung (4:3 Monitor). Job nur bei Anzeigeproblemen mit GT-BASIS-Konfiguration. Bei Problemen wg. Helligkeitspumpen und Ruecklauflinien im Hauptmenue

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TYPE | int | Type: 00  = Neuer Monitor (Default-Einstellung) Type: 01  = Alter Monitor |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise "OKAY" |
| _TEL_SENDE | binary |  |

<a id="job-steuern-jmc-blanking"></a>
### STEUERN_JMC_BLANKING

Schwarzes Fenster links oder rechts des Bildes Kamera muss zugeschaltet sein Job nur fuer VM5IBUS (VM5_IBUS_CAM) ab SW 16  Argument1: schwarzer Balken links erhoehen    = 1 Argument1: schwarzer Balken links verringern  = 2 Argument1: schwarzer Balken rechts erhoehen   = 3 Argument1: schwarzer Balken rechts verringern = 4 Argument1: Normalstellung links               = 5 Argument1: Normalstellung rechts              = 6

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_1 | int | Argument EINSTELLUNG Bereich von 1 bis 6 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-steuern-jmc-settings"></a>
### STEUERN_JMC_SETTINGS

Aendern von Kontrast, Helligkeit, Farbe oder Tint Job nur fuer VM5IBUS (VM5_IBUS_CAM) ab SW 16 JMC muss eingeschaltet sein Argument1: Kontrast           = 1 Argument1: Helligkeit         = 2 Argument1: Farbe              = 3 Argument1: Tint (bei NTSC)    = 4 Argument1: Werte lesen        = 5 ( Kein Argument2 notwendig) Argument1: Grundeinstellung   = 6 ( Kein Argument2 notwendig) Argument2: Bereich von 1 bis 100 Prozent

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_1 | int | Argument EINSTELLUNG Bereich von 1 bis 6 |
| ARGUMENT_2 | int | Argument Wert in Prozent Bereich von 1 bis 100 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JMC_CONTRAST | int | aktuelle Kontrasteinstellung |
| JMC_BRIGHTNESS | int | aktuelle Helligkeitseinstellung |
| JMC_COLOR | int | aktuelle Farbeinstellung |
| JMC_TINT | int | aktuelle Tinteinstellung |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_SENDE | binary | Sendetelegramm |

<a id="job-steuern-jmctest"></a>
### STEUERN_JMCTEST

MirrorCam-Test des Videomoduls Uebergabe eines Arguments Abfrage der Ergebnisse mit STATUS_JMCTEST Job nur fuer VM5IBUS (VM5_IBUS_CAM) ab SW16

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_1 | int | 0 = Rueckgabe des Acknowledge vor Testbeginn (Test 0) 1 = Rueckgabe des Acknowledge nach Testende (Test 1) wenn kein Argument uebergeben wird, wird Test 0 durchgeführt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_ANTWORT | binary |  |
| _TEL_SENDE | binary |  |

<a id="job-status-jmctest"></a>
### STATUS_JMCTEST

Job nur fuer VM5IBUS (VM5_IBUS_CAM) ab SW 16 Ergebnisse des MirrorCam-Tests STEUERN_JMCTEST oder STEUERN_SELBSTTEST muss vorher gesendet werden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_FINISH_INT | int | Selbsttest Status als INTEGER Wert 0 = Fertig 1 = Messung aktiv 2 = noch keine Messung durchgefuehrt 255 = Ergebniss ungueltig |
| STAT_FINISH | string | Selbsttest Status als Ausgabestring |
| STAT_JMCCODE_INT | int | Codierung als INTEGER Wert 0 = JMC nicht codiert 1 = JMC 4:3 codiert 2 = JMC 16:9 codiert 3 = JMC 16:9 ZOOM codiert x = Kodierfehler |
| STAT_JMCCODE | string | eingestellte Codierung 4:3, 16:9 oder Zoom |
| STAT_JMCSPEED | int | Kodierte Abschaltgeschwindigkeit |
| STAT_JMCVOLTAGE_READ | int | gemessener Spannungswert |
| STAT_JMCVOLTAGE_INT | int | Ergebnis der Spannungspruefung als INTEGER Wert 0 = JMC Spannung OK 1 = JMC Spannung zu hoch oder Kurzschluss 2 = JMC Spannung zu klein oder Kurzschluss 255 = Ergebniss ungueltig Voraussetzung fuer Kurzschlusspruefung gegen UBatt: JMC muss angeschlossen sein |
| STAT_JMCVOLTAGE | string | Spannungspruefung fuer JMC |
| STAT_JMCSIGNAL_INT | int | Ergebnis der Eingangspruefung als INTERGER Wert 0 = JMC Signal OK 1 = JMC nicht angeschlossen oder defekt 2 = JMC nicht angeschlossen oder Kurzschluss 255 = Ergebniss ungueltig |
| STAT_JMCSIGNAL | string | FBAS Signal der JMC |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [LIEFERANTEN](#table-lieferanten) (76 × 2)
- [SEGMENTAUSWAHL](#table-segmentauswahl) (6 × 2)
- [FORTTEXTE](#table-forttexte) (4 × 2)
- [IORTTEXTE](#table-iorttexte) (14 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)

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

<a id="table-segmentauswahl"></a>
### SEGMENTAUSWAHL

Dimensions: 6 rows × 2 columns

| SEGMENT | AUSWAHLTEXT |
| --- | --- |
| 0x02 | EPROM |
| 0x03 | EEPROM |
| 0x04 | internes RAM DATA |
| 0x05 | externes RAM XDATA |
| 0x0B | internes RAM IDATA |
| 0xXY | Unbekanntes Segment |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 4 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | IBus Dauerhigh Abschaltung |
| 0x02 | Watchdog ausgeloest |
| 0x03 | FeTraWe aktiviert |
| 0xXY | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 14 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | IBus-Pufferueberlauf |
| 0x02 | I2C Fehler zum Graphikteil |
| 0x03 | I2C Fehler vom Graphikteil |
| 0x04 | Uebertemperatur im Videomodul |
| 0x05 | Audio-Fehler |
| 0x06 | RGB-Fehler |
| 0x07 | Video-Fehler |
| 0x08 | Sonstige-Fehler |
| 0x09 | EEPROM read Fehler |
| 0x0A | EEPROM write Fehler |
| 0x0B | EEPROM Checksumfehler |
| 0x0C | EEPROM Neuinitialisierung |
| 0x0D | TV-Tunerinitialisierungs-Fehler |
| 0xXY | unbekannte Fehlerart |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler nicht aktiv |
| 0x20 | Fehler aktiv |
| 0xXY | unbekannte Fehlerart |
