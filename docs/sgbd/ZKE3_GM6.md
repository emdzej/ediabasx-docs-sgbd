# ZKE3_GM6.prg

- Jobs: [33](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ZKE III: GM3 Redesign E53 (incl. SCA) |
| ORIGIN | BMW TI-430 Gerd Huber |
| REVISION | 1.02 |
| AUTHOR | Softing AEC Thomas Wischer |
| COMMENT | Ansteuern nur bei entsichertem Fahrzeug! |
| PACKAGE | 1.03 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [IDENT](#job-ident) - Ident-Daten fuer GM III
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen der Herstelldaten
- [COD_LESEN_ALLGEMEIN](#job-cod-lesen-allgemein) - Auslesen der allgemeinen Codierdaten des GM III (Block 0)
- [COD_LESEN_SERVOTRONIK](#job-cod-lesen-servotronik) - Auslesen der Codierdaten des GM III (Block 1 und 2)
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen Info-Speicher ist im Aufbau identisch dem Fehlerspeicher Low-Konzept nach Lastenheft Codierung/Diagnose
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers der ZKE III Als Argumente werden die Anzahl, das Segment und die Adresse der Datenbytes uebergeben.
- [SPEICHER_LESEN_STRING](#job-speicher-lesen-string) - Lesen des internen Speichers der ZKE III Als Argumente werden die Anzahl, das Segment und die Adresse der Datenbytes uebergeben.
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [STATUS_DIGITAL_GM3_EA](#job-status-digital-gm3-ea) - Status der Digitalsignale des GM III E53 Signalart: Ein-/Ausgaenge
- [STATUS_DIGITAL_GM3_KP](#job-status-digital-gm3-kp) - Status der Digitalsignale des GM III E53 Signalart: K-Bus bzw. P-Bus
- [STATUS_DIGITAL_GM3_INT](#job-status-digital-gm3-int) - Status der Digitalsignale des GM III E53 Signalart: interne Signale
- [STATUS_ANALOG_GM3](#job-status-analog-gm3) - Status der Analogsignale des GM III E53
- [STEUERN_DIGITAL_GM3](#job-steuern-digital-gm3) - Ansteuern eines digitalen Ein- oder Ausgangs v. GM3
- [STEUERN_ANALOG_GM3](#job-steuern-analog-gm3) - Ansteuern eines analogen Ein- oder Ausgangs v. GM3
- [STEUERN_GENERIC_GM3](#job-steuern-generic-gm3) - Ansteuern eines Statussignals
- [STEUERN_SIMULTAN_GM3](#job-steuern-simultan-gm3) - Gleichzeitiges Ansteuern maximal 5 digitaler Signale des GM3 !!! ACHTUNG: ZKE III antwortet nicht !!!
- [STATUS_BYTES_GM3](#job-status-bytes-gm3) - Status der Digitalsignale des GM III Signalart: BYTE-weise, d.h. ohne Interpretation
- [STATUS_FH_HINTEN](#job-status-fh-hinten) - Status der FH-Signale hinten (GM3)
- [STATUS_INRS](#job-status-inrs) - 1.) Ansteuern: NGAG - 2.) Status lesen: INRS
- [STATUS_KEY_MEMORY](#job-status-key-memory) - Auslesen der Nummer des Funkschluessels, mit dem zuletzt entriegelt wurde
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen des Pruefstempels und Interpretation als FG-Nummer
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Beschreiben des Pruefstempels mit der FG-Nummer

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

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 if done |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer GM III

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

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Wertebereich 0 - 31 |
| F_ART_ANZ | int | immer 1 |
| F_UW_ANZ | int | immer 0 |
| F_ART1_NR | int | momentan identisch Art-Bit |
| F_ART1_TEXT | string | Fehlerart als Text table FArtTexte ARTTEXT |
| _TEL_ANTWORT0 | binary |  |
| _TEL_ANTWORT1 | binary |  |
| _TEL_ANTWORT2 | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
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

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Auslesen der Herstelldaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| BYTE4 | int | kann beliebig verwendet werden |
| _TEL_ANTWORT | binary |  |

<a id="job-cod-lesen-allgemein"></a>
### COD_LESEN_ALLGEMEIN

Auslesen der allgemeinen Codierdaten des GM III (Block 0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_MIT_SIR | int | Scheibenintensivreinigung |
| COD_MIT_SRA | int | Scheinwerferreinigung |
| COD_MIT_SERVO | int | Servotronik SVT |
| COD_WI_OHNE_POTI | int | Wischerintervall ohne Potentiometer (mit Regensensor) |
| COD_MIT_SP_EINKLAPPEN | int | Spiegel einklappen |
| COD_MIT_SP_HEIZUNG | int | Spiegel-Heizung |
| COD_MIT_SP_MEMORY | int | Spiegel-Memory |
| COD_MIT_SCA_HK | int | Soft-Close-Automatik Heckklappe |
| COD_MIT_FHH | int | elektrische Fensterheber hinten |
| COD_MIT_LSM | int | Lenksaeulenmemory LSM |
| COD_MIT_GLAS_SHD | int | Glasdach |
| COD_IL_OHNE_SOFT | int | ohne Soft On/Off bei Innenlicht |
| COD_OEH | int | integrierte optische Einstiegshilfe OEH |
| COD_BC_WS_IGNORIEREN | int | Bord Computer (BC) Wegfahrsicherung (WFS) nicht ausführen |
| COD_WI_INT_STILL | string | mit Wischerintervall kurz, Intervallzeit bei Stillstand 0: 5 Sekunden 1: 3 Sekunden |
| COD_MIT_SPZ | int | mit Spezialwaschprogramm (SPZ) nur im E53 |
| COD_MIT_SRA_L322 | int | mit Scheinwerferreinigung nur für L322 |
| COD_IB_LEIST_KONF_WERT | real | IB-Leistung Konfiguration (Default Wert: 80%) Bereich: 0 bis 100 |
| COD_IB_LEIST_KONF_EINH | string | Einheit: 'Prozent' |
| COD_OEH_LEIST_KONF_WERT | real | OEH-Leistung Konfiguration (Default Wert: 80%) Bereich: 0 bis 100 |
| COD_OEH_LEIST_KONF_EINH | string | Einheit: 'Prozent' |
| COD_MIT_SHD | int | Schiebehebedach SHD verbaut |
| COD_MIT_SM | int | Sitzmemory FT verbaut |
| COD_MIT_SMBF | int | Sitzmemory BT verbaut |
| COD_MIT_SB_FOND | int | Schalterblock Fond verbaut |
| COD_K_FS_UNL_300MS | int | 1 = Auf dem K-Bus wird das FS-Unlock-Telegramm 300ms verzögert |
| COD_P_FS_UNL_300MS | int | 1 = Auf dem P-Bus wird das FS-Unlock-Telegramm 300ms verzögert |
| COD_IB_CRASH_0KMH | int | nur im Crashfall: mit Innenbeleuchtung "Ein" erst bei 0 KMH |
| COD_RDC_ALARM_HFK | int | mit RDC-DWA Trigger über HFK |
| COD_RDC_ALARM_KBUS | int | mit RDC-DWA Trigger über K-Bus |
| COD_MIT_DWA | int | 1, wenn Diebstahlwarnanlage aktiviert |
| COD_NG_AKTIV | int | 1, wenn Neigungsgeber aktiviert |
| COD_INRS_AKTIV | int | 1, wenn Innenraumschutz aktiviert |
| COD_S_E_MIT_FERNBED | int | 1, wenn Schaerfen u. Entschaerfen nur ueber Fernbedienung |
| COD_AKK_ALARM | string | Intervallton oder Dauerton |
| COD_OPT_ALARM_WARNBL | int | 1, wenn optischer Alarm mit Warnblinkern |
| COD_OPT_ALARM_ABBLLI | int | 1, wenn optischer Alarm mit Abblendlicht |
| COD_OPT_ALARM_FERNLI | int | 1, wenn optischer Alarm mit Fernlicht |
| COD_MIT_SIRENE | int | 1, wenn mit Notstromsirene |
| COD_QS_WARNBL | int | 1, wenn Quittierungssignal beim Schaerfen mit Warnblinker |
| COD_QS_HORN | int | 1, wenn Quit.-sign. beim Schaerfen mit DWA-Horn |
| COD_QE_WARNBL | int | 1, wenn Quittierungssignal beim Entschaerfen mit Warnblinker |
| COD_QE_HORN | int | 1, wenn Quit.-sign. beim Entschaerfen mit DWA-Horn |
| COD_OHNE_NOTENTSCHAERFEN | int | 1, wenn Entfall Notentschaerfen |
| COD_AUTO_WS | int | 1, wenn automatische Wegfahrsperre |
| COD_SUEFV_DEAKTIV | int | Scheibenueberwachung Fahrertuere vorne deaktiv |
| COD_SUEFH_DEAKTIV | int | COD_Scheibenueberwachung Fahrertuere hinten deaktiv |
| COD_SUEBV_DEAKTIV | int | Scheibenueberwachung Beifahrertuere vorne deaktiv |
| COD_SUEBH_DEAKTIV | int | Scheibenueberwachung Beifahrertuere hinten deaktiv |
| COD_HSUE_DEAKTIV | int | Heckscheibenueberwachung deaktiv |
| COD_MIT_FUNK_IRS_H | int | Funkinnenraumschutz hinten |
| COD_TKV_AN_GM | string | Tuerkontakt vorne an Grundmodul angeschlossen |
| COD_LOGIK_TK | string | Logik Tuerkontakte invertiert |
| COD_FH_LA_AB | string | Laendervariante der Fensterheber-Abschaltung |
| COD_FH_KFO_INAKTIV | int | Komfortoeffnung bei Fensterheber inaktiv |
| COD_FH_KFS_INAKTIV | int | Komfortschliessung bei Fensterheber inaktiv |
| COD_REVERS_LANG | int | langes FH Reversieren |
| COD_SERVOTRONIC_KW | int | Servotronik Ventil Korrekturwert Bereich: 0 bis 255 |
| COD_ZV_AGG_TYP | string | ZV Aggregate Typ: 1 = E53, 0 = E39 |
| COD_MIT_ZV_BS_BT | int | mit ZV über Bedienstelle Beifahrertüre |
| COD_MIT_AUTO_ZV_8KMH | int | mit geschwindigkeitsabhängiger (automatischer) ZV |
| COD_MIT_HK_NICHT_ENTSICHERN | int | ohne Heckklappe entsichern |
| COD_MIT_SEL_ZV | int | selektive Zentralverriegelung |
| COD_FB_MIT_AUTO_ZV | int | mit automatischem Verriegeln nach 2min |
| COD_FB_MIT_ENTRIEGELN_KLR | int | mit automatischem Entriegeln bei KL.R an, innerhalb 30s nach verriegeln |
| COD_FB_ZV_ENTRIEGELN_SCHLUESSEL | int | ZV entriegeln über Schlüssel, auch wenn DWA nicht entschärft wird |
| COD_MIT_CRASHTIMER_HKOE | int | mit Crashtimer HK Öffnen erst nach 10sec |
| COD_FB_MIT_KFO | int | mit Komfortoeffnung |
| COD_FB_MIT_KFS | int | mit Komfortschliessung |
| COD_FB_MIT_PANIK | int | mit Panik-Mode |
| COD_FB_MIT_IL | int | mit Innenlicht an bei mehrmaligem Verriegeln |
| COD_FB_KBUS_SPERREN | int | mit interner FZV, d.h. K-Bus Fernbedienung sperren |
| COD_MIT_IRF_BT | int | mit IR-FB an PM-BT fuer Hongkong |
| COD_DEB_TIM_CS_WERT | real | Debounce Time Crash-Sensor (Default Wert:100d = 1ms) Bereich: 0 bis 2.55 |
| COD_DEB_TIM_CS_EINH | string | Einheit: 'ms' |
| COD_FZG_TYP | string | Fahrzeugtyp: E38, E39, E39/2 (HK, HS Funktion), E53, L30 / L322 |
| COD_E39_2_HECK_FKT | int | E39/2: Heckklappen-, Heckscheibenfunktion |
| COD_MIT_ADV | int | Anpressdruckverstellung ADV verbaut |
| COD_PASS_DWA_HORN | int | passives DWA Horn E38 |
| COD_DWAH_PIN_C17 | int | DWAH auf Pin C17 |
| COD_VA_2 | int | 2. VA bei E53 mit SCA |
| COD_BLOCK_0 | binary | Codierdaten im Block 0 |
| DATENSICHERUNG_BLOCK_0 | string | Datensicherungsbyte fuer Block 0 |
| CHECKSUMME_BLOCK_0 | int | Checksumme fuer Block 0 |
| _TEL_ANTWORT | binary |  |

<a id="job-cod-lesen-servotronik"></a>
### COD_LESEN_SERVOTRONIK

Auslesen der Codierdaten des GM III (Block 1 und 2)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_BLOCK_1 | binary | Codierdaten im Block 1 |
| DATENSICHERUNG_BLOCK_1 | string | Datensicherungsbyte fuer Block 1 |
| CHECKSUMME_BLOCK_1 | int | Checksumme fuer Block 1 |
| COD_BLOCK_2 | binary | Codierdaten im Block 2 |
| DATENSICHERUNG_BLOCK_2 | string | Datensicherungsbyte fuer Block 2 |
| CHECKSUMME_BLOCK_2 | int | Checksumme fuer Block 2 |
| _TEL_ANTWORT1 | binary |  |
| _TEL_ANTWORT2 | binary |  |

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen Info-Speicher ist im Aufbau identisch dem Fehlerspeicher Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table IOrtTexte ORTTEXT |
| F_HFK | int | Wertebereich 0 - 31 |
| F_ART_ANZ | int | immer 1 |
| F_UW_ANZ | int | immer 0 |
| F_ART1_NR | int | momentan identisch Art-Bit |
| F_ART1_TEXT | string | Fehlerart als Text table FArtTexte ARTTEXT |
| _TEL_ANTWORT0 | binary |  |
| _TEL_ANTWORT1 | binary |  |
| _TEL_ANTWORT2 | binary |  |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers der ZKE III Als Argumente werden die Anzahl, das Segment und die Adresse der Datenbytes uebergeben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL | int | 1 - 32 |
| SEGMENT | int | 0x00 - 0xFF |
| ADRESSE | long | 0x000000 - 0xFFFFFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-speicher-lesen-string"></a>
### SPEICHER_LESEN_STRING

Lesen des internen Speichers der ZKE III Als Argumente werden die Anzahl, das Segment und die Adresse der Datenbytes uebergeben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL | int | 1 - 32 |
| SEGMENT | int | 0x00 - 0xFF |
| ADRESSE | long | 0x000000 - 0xFFFFFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | int | 0x00 - 0xFF |
| ADRESSE | long | 0x000000 - 0xFFFFFF |
| ANZAHL | int | 1 - n ( max. 26 ) |
| DATEN | string | zu schreibende Daten (Anzahl siehe oben) z.B. 1,2,03,0x04,0x05... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-gm3-ea"></a>
### STATUS_DIGITAL_GM3_EA

Status der Digitalsignale des GM III E53 Signalart: Ein-/Ausgaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_E_TKFH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TKBH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TKFT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TKBT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_VORA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_ZRS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MHK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_RDC_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_HKK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SIB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_INRS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_NGEG_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_THKU_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_KLR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_KL30_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_CS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_WS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TOEHKI_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_REE2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_REE1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TZV_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TOEHK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SW1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SW2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SWP_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SPZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_RSK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MFBHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MFBHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MFFHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MFFHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SCAO_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_SIRENE_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_VA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_WP_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_MVR_GH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_MVR_GL_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_MER_GH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_MER_GL_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_MZS_GH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_MZS_GL_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_MERHK_GH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_MERHK_GL_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MHKER_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_OEH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_IB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_PRELAY_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_XC7_H1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_XC7_L1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_XC16_H2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_XC16_L2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_WI1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_WI2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_SRA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_DWAL_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_NGAG_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_XB21_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_OUT_XB22_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IFN_FTOFFEN_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IFN_BTOFFEN_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_ANLE_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_RERHS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_RERHK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT0 | binary |  |
| _TEL_ANTWORT1 | binary |  |
| _TEL_ANTWORT2 | binary |  |

<a id="job-status-digital-gm3-kp"></a>
### STATUS_DIGITAL_GM3_KP

Status der Digitalsignale des GM III E53 Signalart: K-Bus bzw. P-Bus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_K_KLR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_K_KL15_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_K_KL50_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_K_KL58_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_PS_TKFT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_PS_TKBT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-digital-gm3-int"></a>
### STATUS_DIGITAL_GM3_INT

Status der Digitalsignale des GM III E53 Signalart: interne Signale

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_IFN_ZV_VERRIEGELT | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IFN_ZV_GESICHERT | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IFN_FTOFFEN_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IFN_BTOFFEN_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-gm3"></a>
### STATUS_ANALOG_GM3

Status der Analogsignale des GM III E53

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_TACHOA_WERT | real | aktuelle Geschwindigkeit ueber Tacho-A-Eingang Bereich: 0 bis 255 |
| STAT_TACHOA_EINH | string | Einheit: 'km/h' |
| STAT_KMH_WERT | real | Geschwindigkeit ueber K-Bus Bereich: 0 bis 255 |
| STAT_KMH_EINH | string | Einheit: 'km/h' |
| STAT_TEMP_WERT | real | Aussentemperatur ueber K-Bus Bereich: -128 bis 127 |
| STAT_TEMP_EINH | string | Einheit: 'Grad Celsius' |
| STAT_ISERV_WERT | real | Strom im Servoventil Bereich: 0 bis 897 |
| STAT_ISERV_EINH | string | Einheit: 'Milli-Ampere' |
| STAT_ASERV_WERT | real | PWM-Ansteuerung Servoventil Bereich: 0 bis 100 |
| STAT_ASERV_EINH | string | Einheit: 'Prozent' |
| STAT_AIB_WERT | real | PWM-Ansteuerung Innenlicht Bereich: 0 bis 100 |
| STAT_AIB_EINH | string | Einheit: 'Prozent' |
| STAT_VAL_OEH_WERT | real | PWM-Ansteuerung Optische Einstiegshilfe Bereich: 0 bis 100 |
| STAT_VAL_OEH_EINH | string | Einheit: 'Prozent' |
| STAT_VAL_GPL_WERT | real | PWM-Ansteuerung Gepaeckraumleuchte Bereich: 0 bis 100 |
| STAT_VAL_GPL_EINH | string | Einheit: 'Prozent' |
| STAT_VAL_VA_WERT | real | PWM-Ansteuerung Verbraucherabschaltung Bereich: 0 bis 100 |
| STAT_VAL_VA_EINH | string | Einheit: 'Prozent' |
| STAT_DA_IB_WERT | real | Aktueller Wert IB, Diagnose Feedback Bereich: 0 bis 100 |
| STAT_DA_IB_EINH | string | Einheit: 'Prozent' |
| STAT_DA_OEH_WERT | real | Aktueller Wert OEH, Diagnose Feedback Bereich: 0 bis 100 |
| STAT_DA_OEH_EINH | string | Einheit: 'Prozent' |
| STAT_DA_VA_WERT | real | Aktueller Wert VA, Diagnose Feedback Bereich: 0 bis 6 |
| STAT_DA_VA_EINH | string | Einheit: 'Ampere' |
| STAT_IFHBH_WERT | real | mom. Strom FH-Antrieb BT hinten Bereich: 0 bis 49,7 |
| STAT_IFHBH_EINH | string | Einheit: 'Ampere' |
| STAT_IFHFH_WERT | real | mom. Strom FH-Antrieb FT hinten Bereich: 0 bis 49,7 |
| STAT_IFHFH_EINH | string | Einheit: 'Ampere' |
| STAT_DA_WP_WERT | real | Diagnose Feedback Wasch Pumpe Bereich: 0 bis 255 |
| STAT_DA_WP_EINH | string | Einheit: '1' |
| STAT_SERV_FEEDBACK_WERT | real | Diagnose Feedback Servotronic Bereich: 0 bis 255 |
| STAT_SERV_FEEDBACK_EINH | string | Einheit: '1' |
| STAT_U30L1_WERT | real | Spannung am Laststromkreis 1 Bereich: 0 bis 28,4 |
| STAT_U30L1_EINH | string | Einheit: 'Volt' |
| STAT_U30L2_WERT | real | Spannung am Laststromkreis 2 Bereich: 0 bis 28,4 |
| STAT_U30L2_EINH | string | Einheit: 'Volt' |
| STAT_UWIINT_WERT | real | Spannung am Wischerpotentiometer Bereich: 0 bis 5 |
| STAT_UWIINT_EINH | string | Einheit: 'Volt' |
| STAT_UEKSBH_WERT | real | Spannung an der Einklemmschutzleiste BH Bereich: 0 bis 5 |
| STAT_UEKSBH_EINH | string | Einheit: 'Volt' |
| STAT_UEKSFH_WERT | real | Spannung an der Einklemmschutzleiste FH Bereich: 0 bis 5 |
| STAT_UEKSFH_EINH | string | Einheit: 'Volt' |
| STAT_C17_PWM_WERT | real | PWM Ansteuerung C17 Bereich: 0 bis 100 |
| STAT_C17_PWM_EINH | string | Einheit: 'Prozent' |
| STAT_C16_PWM_WERT | real | PWM Ansteuerung C16 Bereich: 0 bis 100 |
| STAT_C16_PWM_EINH | string | Einheit: 'Prozent' |
| STAT_DA_MERHK_WERT | real | Aktueller Wert MERHK, Diagnose Feedback Bereich: 0 bis 255 |
| STAT_DA_MERHK_EINH | string | Einheit: '1' |
| STAT_IBHMAX_WERT | real | max. Strom FH-Antrieb BT hinten Bereich: 0 bis 49,7 |
| STAT_IBHMAX_EINH | string | Einheit: 'Ampere' |
| STAT_IFHMAX_WERT | real | max. Strom FH-Antrieb FT hinten Bereich: 0 bis 49,7 |
| STAT_IFHMAX_EINH | string | Einheit: 'Ampere' |
| STAT_GKL_WERT | real | aktuelle Geschwindigkeitsklasse Bereich: 0 bis 6 (Werte &gt; 6 -&gt; Fehler) |
| STAT_GKL_EINH | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-digital-gm3"></a>
### STEUERN_DIGITAL_GM3

Ansteuern eines digitalen Ein- oder Ausgangs v. GM3

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table BITS NAME PBADR ART TEXT |
| EIN | int | '1', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-analog-gm3"></a>
### STEUERN_ANALOG_GM3

Ansteuern eines analogen Ein- oder Ausgangs v. GM3

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente |
| WERT | long | Wert, mit welchen angesteuert werden soll |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-generic-gm3"></a>
### STEUERN_GENERIC_GM3

Ansteuern eines Statussignals

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PBADR | unsigned char | P-Bus-Adresse |
| ORT | unsigned char | gewuenschte Komponente |
| WERT | unsigned char | beliebiger Wert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-simultan-gm3"></a>
### STEUERN_SIMULTAN_GM3

Gleichzeitiges Ansteuern maximal 5 digitaler Signale des GM3 !!! ACHTUNG: ZKE III antwortet nicht !!!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT1 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |
| ORT2 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |
| ORT3 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |
| ORT4 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |
| ORT5 | string | gewuenschte Komponente Auswahl siehe JOB STEUERN_DIGITAL_.. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-status-bytes-gm3"></a>
### STATUS_BYTES_GM3

Status der Digitalsignale des GM III Signalart: BYTE-weise, d.h. ohne Interpretation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_DATEN0 | binary | Rohe digital Daten |
| STAT_DATEN1 | binary | Rohe digital Flags |
| _TEL_ANTWORT0 | binary |  |
| _TEL_ANTWORT1 | binary |  |

<a id="job-status-fh-hinten"></a>
### STATUS_FH_HINTEN

Status der FH-Signale hinten (GM3)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_PS_SBFHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_PS_SBFHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_PS_SBFHT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_PS_SBBHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_PS_SBBHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_PS_SBBHT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IFHBH_WERT | long | mom. Strom FH-Antrieb BT hinten Bereich: 0 bis 49,7 |
| STAT_IFHBH_EINH | string | Einheit: 'Ampere' |
| STAT_IFHFH_WERT | long | mom. Strom FH-Antrieb FT hinten Bereich: 0 bis 49,7 |
| STAT_IFHFH_EINH | string | Einheit: 'Ampere' |
| STAT_IBHMAX_WERT | long | max. Strom FH-Antrieb BT hinten Bereich: 0 bis 49,7 |
| STAT_IBHMAX_EINH | string | Einheit: 'Ampere' |
| STAT_IFHMAX_WERT | long | max. Strom FH-Antrieb FT hinten Bereich: 0 bis 49,7 |
| STAT_IFHMAX_EINH | string | Einheit: 'Ampere' |
| _TEL_ANTWORT | binary |  |

<a id="job-status-inrs"></a>
### STATUS_INRS

1.) Ansteuern: NGAG - 2.) Status lesen: INRS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EIN | int | '1', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_E_INRS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT1 | binary |  |
| _TEL_ANTWORT2 | binary |  |

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

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (81 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [FORTTEXTE](#table-forttexte) (85 × 2)
- [FARTTEXTE](#table-farttexte) (2 × 2)
- [IORTTEXTE](#table-iorttexte) (27 × 2)
- [BITS](#table-bits) (89 × 8)

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

Dimensions: 81 rows × 2 columns

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
| 0x76 | CEL |
| 0x77 | Audio Mobil |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia Automotive GmbH |
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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 85 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xB4 | Energiesparmode gesetzt |
| 0x01 | Sicherung Fensterheber hinten |
| 0x02 | Sicherung Innenraumbeleuchtung |
| 0x04 | Leitung Klemme R am GM III |
| 0x08 | Codierung Block 0 nicht erfolgt |
| 0x09 | Codierung Block 1 oder Block 2 nicht erfolgt |
| 0x0A | Codierung Block 0 nicht korrekt |
| 0x0B | Codierung Block 1 oder Block 2 nicht korrekt |
| 0x30 | Wischerschalter, Potentiometer |
| 0x32 | Wascherpumpe Unterbrechung |
| 0x31 | Wischermotor blockiert, Rueckstellkontakt, Wischerrelais |
| 0x33 | Kurzschluss Wascherpumpe |
| 0x38 | Leitung SRA Unterbrechung oder Relais SRA  |
| 0x39 | Relaiskleber nach U-Batt im DRM 2 |
| 0x48 | Leitung WI1 Kurzschluss gegen U-Batt oder Wischerrelais 1 |
| 0x49 | Leitung WI1 Unterbrechung oder Wischerrelais 1 |
| 0x4A | Leitung WI2 Kurzschluss gegen U-Batt oder Wischerrelais 2 |
| 0x4B | Leitung WI2 Unterbrechung oder Wischerrelais 2 |
| 0x40 | Leitungsunterbrechung Innenraumbeleuchtung |
| 0x41 | Kurzschluss Innenraumbeleuchtung |
| 0x42 | Kurzschluss VA |
| 0x46 | Unterbrechung OEH oder Zuleitung |
| 0x47 | Kurzschluss OEH oder Zuleitung |
| 0x50 | Relaiskleber Signal MER nach U-Batt im GM III |
| 0x51 | Relaiskleber Signal MER nach Masse im GM III |
| 0x52 | Relaiskleber Signal MVR nach U-Batt im GM III |
| 0x53 | Relaiskleber Signal MVR nach Masse im GM III |
| 0x54 | Relaiskleber Signal MZS nach U-Batt im GM III |
| 0x55 | Relaiskleber Signal MZS nach Masse im GM III |
| 0x56 | Relaiskleber Signal MERHK nach U-Batt im GM III |
| 0x57 | Relaiskleber Signal MERHK nach Masse im GM III |
| 0x58 | Crash-Sensor dauernd aktiv |
| 0x59 | ZV-Antrieb FT unterbrochen |
| 0x5A | ZV-Antrieb BT unterbrochen |
| 0x5B | ZV-Antrieb FT kurzgeschlossen |
| 0x5C | ZV-Antrieb BT kurzgeschlossen |
| 0x60 | Relaiskleber Signal MFFA nach U-Batt im PM FT |
| 0x61 | Relaiskleber Signal MFFA nach Masse im PM FT |
| 0x62 | Relaiskleber Signal MFFZ nach U-Batt im PM FT |
| 0x63 | Relaiskleber Signal MFFZ nach Masse im PM FT |
| 0x64 | Relaiskleber Signal MFBA nach U-Batt im PM BT |
| 0x65 | Relaiskleber Signal MFBA nach Masse im PM BT |
| 0x66 | Relaiskleber Signal MFBZ nach U-Batt im PM BT |
| 0x67 | Relaiskleber Signal MFBZ nach Masse im PM BT |
| 0x68 | Relaiskleber Signal MFFHA nach U-Batt im GM III |
| 0x69 | Relaiskleber Signal MFFHA nach Masse im GM III |
| 0x6A | Relaiskleber Signal MFFHZ nach U-Batt im GM III |
| 0x6B | Relaiskleber Signal MFFHZ nach Masse im GM III |
| 0x6C | Relaiskleber Signal MFBHA nach U-Batt im GM III |
| 0x6D | Relaiskleber Signal MFBHA nach Masse im GM III |
| 0x6E | Relaiskleber Signal MFBHZ nach U-Batt im GM III |
| 0x6F | Relaiskleber Signal MFBHZ nach Masse im GM III |
| 0x70 | PM Schalterblock |
| 0x7C | SHD-Motor blockiert oder PM SHD defekt |
| 0x7E | SHD-Schalter oder Zuleitungen NIO |
| 0x7F | PM SHD defekt (Relais) |
| 0x80 | Unterbrechung Servoventil oder Leitungen |
| 0x81 | Kurzschluss Servoventil oder Leitungen |
| 0x82 | Leitung ABS-Signal oder IKE fehlt |
| 0x83 | Leitung ABS-Signal oder IKE unplausibel |
| 0x92 | Neigungsgeber: Sicherung oder Leitung |
| 0x93 | DWA-LED: Kurzschluss gegen U-Batt oder Leitung DWAL |
| 0x94 | DWA-LED: Unterbrechung oder Leitung DWAL, KL30 |
| 0x95 | Innenraumschutz: Sicherung oder Leitung |
| 0xA0 | Unterbrechung Spiegelheizung FT oder Leitungen |
| 0xA1 | Kurzschluss Spiegelheizung FT oder Leitungen |
| 0xA2 | Unterbrechung Spiegelheizung BT oder Leitungen |
| 0xA3 | Kurzschluss Spiegelheizung BT oder Leitungen |
| 0xA4 | Spiegel FT, Potentiometer Vertikal oder Leitungen |
| 0xA5 | Spiegel FT, Potentiometer Horizontal oder Leitungen |
| 0xA6 | Spiegel BT, Potentiometer Vertikal oder Leitungen |
| 0xA7 | Spiegel BT, Potentiometer Horizontal oder Leitungen |
| 0xA8 | Unterbrechung Spiegelmotor FT Vertikal |
| 0xA9 | Kurzschluss Spiegelmotor FT Vertikal |
| 0xAA | Unterbrechung Spiegelmotor FT Horizontal |
| 0xAB | Kurzschluss Spiegelmotor FT Horizontal |
| 0xAC | Unterbrechung Spiegelmotor BT Vertikal |
| 0xAD | Kurzschluss Spiegelmotor BT Vertikal |
| 0xAE | Unterbrechung Spiegelmotor BT Horizontal |
| 0xAF | Kurzschluss Spiegelmotor BT Horizontal |
| 0xB0 | Unterbrechung Spiegelmotor FT Einklappen |
| 0xB1 | Kurzschluss Spiegelmotor FT Einklappen |
| 0xB2 | Unterbrechung Spiegelmotor BT Einklappen |
| 0xB3 | Kurzschluss Spiegelmotor BT Einklappen |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 2 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 27 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x70 | Unterbrechung Servoventil oder Leitungen (SERV1, SERV2) |
| 0x71 | Kurzschluss Servoventil oder Leitungen (SERV1, SERV2) |
| 0x72 | Servotronik: Leitung ABS-Signal oder IKE fehlt |
| 0x73 | Servotronik: Leitung ABS-Signal oder IKE unplausibel |
| 0x80 | DWA-Alarm : Klemme R |
| 0x81 | DWA-Alarm : Klemme 15 |
| 0x82 | DWA-Alarm : Panik-Mode |
| 0x83 | DWA-Alarm : Tuerkontakt FT |
| 0x84 | DWA-Alarm : Tuerkontakt BT |
| 0x85 | DWA-Alarm : Tuerkontakt FTH |
| 0x86 | DWA-Alarm : Tuerkontakt BTH |
| 0x87 | DWA-Alarm : Heckklappenkontakt |
| 0x89 | DWA-Alarm : Motorhaubenkontakt |
| 0x8A | DWA-Alarm : Neigungsgeber |
| 0x8B | DWA-Alarm : Innenraumschutz |
| 0x93 | Power Up vom GM III |
| 0x94 | Power Up vom PM FT |
| 0x95 | Power Up vom PM BT |
| 0xA0 | Wiederholsperre ZV angesprochen |
| 0xA1 | Crash-Sensor hat angesprochen |
| 0xA4 | Spiegel- u. ZV-Treiber in PM FT hat Uerbertemp.absch. angespr. |
| 0xA5 | Spiegel- u. ZV-Treiber in PM BT hat Uerbertemp.absch. angespr. |
| 0x60 | Fensterheber-Motor FT |
| 0x61 | Fensterheber-Motor BT |
| 0x62 | Fensterheber-Motor FTH |
| 0x63 | Fensterheber-Motor BTH |
| 0xXY | unbekannter Info-Ort |

<a id="table-bits"></a>
### BITS

Dimensions: 89 rows × 8 columns

| NAME | PBADR | BYTE | MASK | VALUE | INV | ART | TEXT |
| --- | --- | --- | --- | --- | --- | --- | --- |
| SIB | 0x00 | 1 | 0x80 | 0x80 | 0 | E | Schalter Innenraumbeleuchtung |
| INRS | 0x00 | 2 | 0x04 | 0x04 | 0 | E | Innenraumschutz (Heckscheibe oder Innenraum) |
| NGEG | 0x00 | 2 | 0x08 | 0x08 | 0 | E | Schnittstelle zum Neigungsgeber |
| THKU | 0x00 | 2 | 0x20 | 0x20 | 0 | E | Taste Heckklappe unten Entriegeln |
| KLR | 0x00 | 2 | 0x40 | 0x40 | 0 | E | Klemme R (Radio) |
| TOEHKI | 0x00 | 3 | 0x01 | 0x01 | 0 | E | Taster Oeffnen Heckklappe Innen |
| REE2 | 0x00 | 3 | 0x04 | 0x04 | 0 | E | Reserve Eingang 2 |
| REE1 | 0x00 | 3 | 0x08 | 0x08 | 0 | E | Reserve Eingang 1 |
| TZV | 0x00 | 3 | 0x10 | 0x10 | 0 | E | Taste zum Umschalten der ZV |
| TOEHK | 0x00 | 3 | 0x20 | 0x20 | 0 | E | Taster Oeffnen Heckklappe |
| SW1 | 0x00 | 3 | 0x40 | 0x40 | 0 | E | Schalter Wischer INT, ,ST2 kodiert |
| SW2 | 0x00 | 3 | 0x80 | 0x80 | 0 | E | Schalter Wischer ,ST1,ST2 kodiert |
| SWP | 0x00 | 4 | 0x01 | 0x01 | 0 | E | Schalter Wischer Wascherpumpe |
| SFFHA | 0x00 | 4 | 0x02 | 0x02 | 0 | E | FH-Schalter FH hinten auf |
| SFFHZ | 0x00 | 4 | 0x04 | 0x04 | 0 | E | FH-Schalter FH hinten zu |
| SPZ | 0x00 | 4 | 0x08 | 0x08 | 0 | E | Schalter Wischer Intensivpumpe |
| SFBHA | 0x00 | 4 | 0x10 | 0x10 | 0 | E | FH-Schalter BH hinten auf |
| SFBHZ | 0x00 | 4 | 0x20 | 0x20 | 0 | E | FH-Schalter BH hinten zu |
| RSK | 0x00 | 4 | 0x80 | 0x80 | 1 | E | Rueckstellkontakt Wischer |
| DMERHK | 0x00 | 5 | 0x01 | 0x01 | 0 | IE | interne Diagnoserueckfuehrung Motor ERHK |
| DMVR | 0x00 | 5 | 0x02 | 0x02 | 0 | IE | interne Diagnoserueckfuehrung Motor VR |
| DMER | 0x00 | 5 | 0x04 | 0x04 | 0 | IE | interne Diagnoserueckfuehrung Motor ER |
| DMZS | 0x00 | 5 | 0x08 | 0x08 | 0 | IE | interne Diagnoserueckfuehrung Motor ZS |
| DMFFHZ | 0x00 | 5 | 0x10 | 0x10 | 0 | IE | interne Diagnoserueckfuehrung Motor FFHZ |
| DMFFHA | 0x00 | 5 | 0x20 | 0x20 | 0 | IE | interne Diagnoserueckfuehrung Motor FFHA |
| DMFBHZ | 0x00 | 5 | 0x40 | 0x40 | 0 | IE | interne Diagnoserueckfuehrung Motor FBHZ |
| DMFBHA | 0x00 | 5 | 0x80 | 0x80 | 0 | IE | interne Diagnoserueckfuehrung Motor FBHA |
| DWI1 | 0x00 | 6 | 0x01 | 0x01 | 0 | IE | intern belegt |
| DWI2 | 0x00 | 6 | 0x02 | 0x02 | 0 | IE | intern belegt |
| S_SRA | 0x00 | 6 | 0x04 | 0x04 | 0 | IE | intern belegt |
| DDWAL | 0x00 | 6 | 0x10 | 0x10 | 0 | IE | intern belegt |
| S_NGAG | 0x00 | 6 | 0x20 | 0x20 | 0 | IE | intern belegt |
| S_XB21 | 0x00 | 6 | 0x40 | 0x40 | 0 | IE | intern belegt |
| S_XB22 | 0x00 | 6 | 0x80 | 0x80 | 0 | IE | intern belegt |
| S_MZS_MERHK_ST | 0x00 | 7 | 0x01 | 0x01 | 0 | IE | interne Diagnoserückführung Treiber Status |
| S_MER_MVR_ST | 0x00 | 7 | 0x02 | 0x02 | 0 | IE | interne Diagnoserückführung Treiber Status |
| S_MZS_ST | 0x00 | 7 | 0x08 | 0x08 | 0 | IE | interne Diagnoserückführung Treiber Status |
| MFBHA | 0x00 | 8 | 0x01 | 0x01 | 0 | A | internes Relais Fenster Beifahrer Hinten AUF |
| MFBHZ | 0x00 | 8 | 0x02 | 0x02 | 0 | A | internes Relais Fenster Beifahrer Hinten ZU |
| MFFHA | 0x00 | 8 | 0x04 | 0x04 | 0 | A | internes Relais Fenster Fahrer Hinten AUF |
| MFFHZ | 0x00 | 8 | 0x08 | 0x08 | 0 | A | internes Relais Fenster Fahrer Hinten ZU |
| SIRENE | 0x00 | 8 | 0x10 | 0x10 | 0 | A | DWA-Notstromsirene |
| OUT_PRELAY | 0x00 | 8 | 0x40 | 0x40 | 0 | A | Verpolschutz Power Relay |
| WP | 0x00 | 8 | 0x80 | 0x80 | 0 | A | Wascherpumpe |
| OUT_MVR_GH | 0x00 | 9 | 0x01 | 0x01 | 0 | A | ZV Motor Verriegeln High Side |
| OUT_MVR_GL | 0x00 | 9 | 0x02 | 0x02 | 0 | A | ZV Motor Verriegeln Low Side |
| OUT_MER_GH | 0x00 | 9 | 0x04 | 0x04 | 0 | A | ZV Motor Entriegeln High Side |
| OUT_MER_GL | 0x00 | 9 | 0x08 | 0x08 | 0 | A | ZV Motor Entriegeln Low Side |
| OUT_MZS_GH | 0x00 | 9 | 0x10 | 0x10 | 0 | A | ZV Motor Zentralsichern High Side |
| OUT_MZS_GL | 0x00 | 9 | 0x20 | 0x20 | 0 | A | ZV Motor Zentralsichern Low Side |
| OUT_MERHK_GH | 0x00 | 9 | 0x40 | 0x40 | 0 | A | HK Motor Entriegeln High Side; 2. VA mit SCA |
| VA_2 | 0x00 | 9 | 0x40 | 0x40 | 0 | A | 2. Verbraucherabschaltung (mit SCA) |
| OUT_MERHK_GL | 0x00 | 9 | 0x80 | 0x80 | 0 | A | HK Motor Entriegeln Low Side |
| OUT_OEH | 0x00 | 10 | 0x01 | 0x01 | 0 | A | Ausgang Optische Einstiegs Hilfe |
| OUT_IB | 0x00 | 10 | 0x02 | 0x02 | 0 | A | Ausgang Innenbeleuchtung |
| VA | 0x00 | 10 | 0x08 | 0x08 | 0 | A | Verbraucherabschaltung |
| OUT_XC7_H1 | 0x00 | 10 | 0x10 | 0x10 | 0 | A | ADV H1 Anpressdruckverstellung High Side |
| OUT_MERHKU | 0x00 | 10 | 0x10 | 0x10 | 0 | A | MERHKU mit SCA |
| OUT_XC7_L1 | 0x00 | 10 | 0x20 | 0x20 | 0 | A | ADV L1 Anpressdruckverstellung Low Side |
| OUT_XC16_H2 | 0x00 | 10 | 0x40 | 0x40 | 0 | A | ADV H2 Anpressdruckverstellung High Side |
| OUT_XC16_L2 | 0x00 | 10 | 0x80 | 0x80 | 0 | A | ADV L2 Anpressdruckverstellung Low Side |
| WI1 | 0x00 | 11 | 0x01 | 0x01 | 0 | A | Motor Wischer Stufe 1 (langsam) |
| WI2 | 0x00 | 11 | 0x02 | 0x02 | 0 | A | Motor Wischer Stufe 2  (schnell) |
| SRA | 0x00 | 11 | 0x04 | 0x04 | 0 | A | Motor Scheinwerferreinigung EIN |
| DWAL | 0x00 | 11 | 0x10 | 0x10 | 0 | A | DWA Leuchtdiode EIN |
| NGAG | 0x00 | 11 | 0x20 | 0x20 | 0 | A | Neigungsgeberausgang EIN |
| OUT_XB21 | 0x00 | 11 | 0x40 | 0x40 | 0 | A | Output B21: Z_RSCA_Z, Z_RERHS, Z_ANLE |
| OUT_XB22 | 0x00 | 11 | 0x80 | 0x80 | 0 | A | Output B22: Z_RSCA_A, Z_RERHK, Z_MERHKU |
| RSCA_A | 0x00 | 11 | 0x80 | 0x80 | 0 | A | Soft Close Automatik Auf |
| RSCA_Z | 0x00 | 11 | 0x40 | 0x40 | 0 | A | Soft Close Automatik ZU |
| MERHKU | 0x00 | 11 | 0x80 | 0x80 | 0 | A | Output B22: MERHKU ohne SCA |
| K_KLR | 0x00 | 12 | 0x01 | 0x01 | 0 | KS | Klemme R (ueber K-Bus) |
| K_KL15 | 0x00 | 12 | 0x02 | 0x02 | 0 | KS | Klemme 15 (ueber K-Bus) |
| K_KL50 | 0x00 | 12 | 0x04 | 0x04 | 0 | KS | Klemme 50 (ueber K-Bus) |
| K_KL58 | 0x00 | 13 | 0x02 | 0x02 | 0 | KS | Klemme 58 (ueber K-Bus) |
| P_VRFT | 0x00 | 19 | 0x01 | 0x01 | 0 | PS | ZV-Schalterpaket FT Verriegeln |
| P_VRBT | 0x00 | 21 | 0x01 | 0x01 | 0 | PS | ZV-Schalterpaket BT Verriegeln |
| K_VRFS | 0x00 | 23 | 0x01 | 0x01 | 0 | KS | Verriegeln von FBZV |
| TKFT | 0x11 | 8 | 0x10 | 0x10 | 0 | E | Tuerkontakt Fahrertuere vorne FT (an GM III) |
| TKBT | 0x11 | 8 | 0x20 | 0x20 | 0 | E | Tuerkontakt Beifahrertuere vorne BT (an GM III) |
| TKFH | 0x11 | 8 | 0x40 | 0x40 | 0 | E | Tuerkontakt Fahrertuere FH hinten |
| TKBH | 0x11 | 8 | 0x80 | 0x80 | 0 | E | Tuerkontakt Beifahrertuere BH hinten |
| HKK | 0x11 | 16 | 0x08 | 0x08 | 0 | E | Heckklappenkontakt |
| MHK | 0x11 | 16 | 0x80 | 0x80 | 0 | E | Motorhaubenkontakt |
| RERHK | 0x11 | 17 | 0x04 | 0x04 | 0 | A | Entriegelung HK unten |
| ZRS | 0x11 | 19 | 0x01 | 0x01 | 0 | E | Zahnradsensor |
| RDC | 0x11 | 19 | 0x02 | 0x02 | 0 | E | Reifen Druck Control |
| VORA | 0x11 | 19 | 0x04 | 0x04 | 0 | E | Vorraste (bei SCA) |
| XY | 0x00 | XY | 0xXY | 0xXY | 0 | XY | nicht definiertes Signal |
