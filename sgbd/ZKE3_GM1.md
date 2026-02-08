# ZKE3_GM1.prg

- Jobs: [28](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ZKE III: Grundmodul E38, E39 |
| ORIGIN | BMW TI-430 Gerd Huber |
| REVISION | 1.1 |
| AUTHOR | BMW TI-430 Gerd Huber |
| COMMENT | Ansteuern nur bei entsichertem Fahrzeug! |
| PACKAGE | 0.04 |
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
- [STATUS_DIGITAL_GM3_EA](#job-status-digital-gm3-ea) - Status der Digitalsignale des GM III Signalart: Ein-/Ausgaenge
- [STATUS_DIGITAL_GM3_KP](#job-status-digital-gm3-kp) - Status der Digitalsignale des GM III Signalart: K-Bus bzw. P-Bus
- [STATUS_DIGITAL_GM3_INT](#job-status-digital-gm3-int) - Status der Digitalsignale des GM III Signalart: interne Signale
- [STATUS_ANALOG_GM3](#job-status-analog-gm3) - Status der Analogsignale des GM III
- [STEUERN_DIGITAL_GM3](#job-steuern-digital-gm3) - Ansteuern eines digitalen Ein- oder Ausgangs v. GM3
- [STEUERN_ANALOG_GM3](#job-steuern-analog-gm3) - Ansteuern eines analogen Ein- oder Ausgangs v. GM3
- [STEUERN_SIMULTAN_GM3](#job-steuern-simultan-gm3) - Gleichzeitiges Ansteuern maximal 5 digitaler Signale des GM3 !!! ACHTUNG: ZKE III antwortet nicht !!!
- [STATUS_BYTES_GM3](#job-status-bytes-gm3) - Status der Digitalsignale des GM III Signalart: BYTE-weise, d.h. ohne Interpretation
- [STATUS_FH_HINTEN](#job-status-fh-hinten) - Status der FH-Signale hinten (GM3)
- [STATUS_INRS](#job-status-inrs) - 1.) Ansteuern: NGAG - 2.) Status lesen: INRS
- [STATUS_KEY_MEMORY](#job-status-key-memory) - Auslesen der Nummer des Funkschluessels, mit dem zuletzt entriegelt wurde
- [PATCH_RUHESTROM_GM3](#job-patch-ruhestrom-gm3) - ZKE3 bzgl. Ruhestromverhalten einstellen
- [PATCH_TEST_RUHESTROM_GM3](#job-patch-test-ruhestrom-gm3) - Test der Patch-Daten bzgl. Ruhestromverhalten ZKE3

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
| COD_MIT_ADV | int | Anpressdruckverstellung |
| COD_MIT_SERVO | int | Servotronik |
| COD_MIT_TSH | int | Tuerschlossheizung |
| COD_MIT_SP_EINKLAPPEN | int | Spiegel einklappen |
| COD_MIT_SP_HEIZUNG | int | Spiegel-Heizung |
| COD_MIT_SP_MEMORY | int | Spiegel-Memory |
| COD_MIT_SCA_HK | int | Soft-Close-Automatik Heckklappe |
| COD_MIT_AUTO_ZV_8KMH | int | automatisch ZV verriegeln ab 8 km/h |
| COD_MIT_FHH | int | elektrische Fensterheber hinten |
| COD_MIT_LSM | int | Lenksaeulenmemory |
| COD_MIT_GLAS_SHD | int | Glasdach |
| COD_MIT_IRF_BT | int | Infrarot-Fernbedienung an Beifahrertuer |
| COD_MIT_HK_NICHT_ENTSICHERN | int | Heckklappe nicht entsichern |
| COD_FZG_TYP | string | Fahrzeugtyp: E38, E39 |
| COD_E39_2_HECK_FKT | int | E39/2: Heckklappen-, Heckscheibenfunktion |
| COD_BC_WS_IGNORIEREN | int | BC-Anforderung Wegfahrsicherung ignorieren |
| COD_MIT_SHD | int | mit Schiebehebedach |
| COD_MIT_SM | int | mit Sitzmemory |
| COD_MIT_SMBF | int | mit Sitzmemory Beifahrer |
| COD_MIT_SB_FOND | int | mit Schalterblock Fond |
| COD_FH_LA_AB | string | Laendervariante der Fensterheber-Abschaltung |
| COD_FH_KFO_INAKTIV | int | Komfortoeffnung bei Fensterheber |
| COD_FH_KFS_INAKTIV | int | Komfortschliessung bei Fensterheber |
| COD_WI_INT_STILL | string | Wischerintervallzeit bei Stillstand 0: 5 Sekunden 1: 3 Sekunden |
| COD_WI_OHNE_POTI | int | Wischerintervall ohne Potentiometer |
| COD_IL_OHNE_SOFT | int | ohne Soft On/Off bei Innenlicht |
| COD_MIT_SEL_ZV | int | selektive Zentralverriegelung |
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
| COD_QS_HORN | int | 1, wenn Quit.-sign. beim Schaerfen mit DWA-Horn oder Sirene |
| COD_QE_WARNBL | int | 1, wenn Quittierungssignal beim Entschaerfen mit Warnblinker |
| COD_QE_HORN | int | 1, wenn Quit.-sign. beim Entschaerfen mit DWA-Horn oder Sirene |
| COD_OHNE_NOTENTSCHAERFEN | int | 1, wenn Entfall Notentschaerfen |
| COD_AUTO_WS | int | 1, wenn automatische Wegfahrsperre |
| COD_REVERS_LANG | int | 1, wenn langes Reversieren bei Einklemmung |
| COD_SUEFV_DEAKTIV | int | Scheibenueberwachung Fahrertuere vorne deaktiv |
| COD_SUEFH_DEAKTIV | int | COD_Scheibenueberwachung Fahrertuere hinten deaktiv |
| COD_SUEBV_DEAKTIV | int | Scheibenueberwachung Beifahrertuere vorne deaktiv |
| COD_SUEBH_DEAKTIV | int | Scheibenueberwachung Beifahrertuere hinten deaktiv |
| COD_HSUE_DEAKTIV | int | Heckscheibenueberwachung deaktiv |
| COD_MIT_FUNK_IRS_H | int | Funkinnenraumschutz hinten |
| COD_TKV_AN_GM | string | Tuerkontakt vorne an Grundmodul angeschlossen |
| COD_LOGIK_TK | string | Logik Tuerkontakte |
| COD_FB_MIT_KFO | int | Fernbedienung mit Komfortoeffnung |
| COD_FB_MIT_KFS | int | Fernbedienung mit Komfortschliessung |
| COD_FB_MIT_AUTO_ZV | int | Fernbedienung mit automatischer Verriegelung nach 2 min |
| COD_FB_MIT_PANIK | int | Fernbedienung mit Panik-Mode |
| COD_FB_MIT_IL | int | Fernbedienung mit Innenlicht an bei mehrmaligem Verriegeln |
| COD_FB_MIT_ENTRIEGELN_KLR | int | Fernbedienung mit Entriegeln bei Klemme R |
| COD_FB_ZV_ENTRIEGELN_SCHLUESSEL | int | Fernbedienung mit ZV entriegeln ueber Schluessel |
| COD_FB_KBUS_SPERREN | int | Fernbedienung sperren ueber K-Bus |
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

<a id="job-status-digital-gm3-ea"></a>
### STATUS_DIGITAL_GM3_EA

Status der Digitalsignale des GM III Signalart: Ein-/Ausgaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_E_SFFHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SIR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SCAO_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_RSK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_NS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TOEHS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE (== E_NS) |
| STAT_E_TOEHKI_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TOEHK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_HKK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TZV_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_VRHK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_KLR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_ERHK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_DSIR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TKFT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TKBT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TKFH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TKBH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SW1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SW2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SWP_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SIB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_MHK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_REE2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_HFK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_INRS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SUEFH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_FIS2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE (== E_SUEFH) |
| STAT_E_SUEBH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_HSK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE (== E_SUEBH) |
| STAT_E_NGEG_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_REE1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_KL30GM_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_CS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_WS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_WI1_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_WI2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_SRA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_IP_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_DWAL_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_NGAG_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_ANLE_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_RERHS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE (== E_ANLE) |
| STAT_A_RERHK_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MHKER_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MVR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MER_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MZS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MFFHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MFFHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MFBHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MFBHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_EN_RXD_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_AN_TXD_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_DWAH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_WP_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MADVZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MADVA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_VA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_WFSI_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_SIRENE_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_PS_TKFT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_PS_TKBT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IFN_FTOFFEN_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IFN_BTOFFEN_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-digital-gm3-kp"></a>
### STATUS_DIGITAL_GM3_KP

Status der Digitalsignale des GM III Signalart: K-Bus bzw. P-Bus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_PS_TKFT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_PS_TKBT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_K_KLR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_K_KL15_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_K_KL50_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_K_KL58_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-digital-gm3-int"></a>
### STATUS_DIGITAL_GM3_INT

Status der Digitalsignale des GM III Signalart: interne Signale

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

Status der Analogsignale des GM III

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
| STAT_ADVP_WERT | real | aktuelle ADV-Position Bereich: 0 bis 4 (Werte &gt; 4 -&gt; Fehler) |
| STAT_ADVP_EINH | string | Einheit: '1' |
| STAT_GKL_WERT | real | aktuelle Geschwindigkeitsklasse Bereich: 0 bis 6 (Werte &gt; 6 -&gt; Fehler) |
| STAT_GKL_EINH | string | Einheit: '1' |
| STAT_IFHBH_WERT | real | mom. Strom FH-Antrieb BT hinten Bereich: 0 bis 49,7 |
| STAT_IFHBH_EINH | string | Einheit: 'Ampere' |
| STAT_IFHFH_WERT | real | mom. Strom FH-Antrieb FT hinten Bereich: 0 bis 49,7 |
| STAT_IFHFH_EINH | string | Einheit: 'Ampere' |
| STAT_IBHMAX_WERT | real | max. Strom FH-Antrieb BT hinten Bereich: 0 bis 49,7 |
| STAT_IBHMAX_EINH | string | Einheit: 'Ampere' |
| STAT_IFHMAX_WERT | real | max. Strom FH-Antrieb FT hinten Bereich: 0 bis 49,7 |
| STAT_IFHMAX_EINH | string | Einheit: 'Ampere' |
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
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-digital-gm3"></a>
### STEUERN_DIGITAL_GM3

Ansteuern eines digitalen Ein- oder Ausgangs v. GM3

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table BITS NAME ART TEXT |
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
| STAT_DATEN | binary | 32 Bytes |
| _TEL_ANTWORT | binary |  |

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

<a id="job-patch-ruhestrom-gm3"></a>
### PATCH_RUHESTROM_GM3

ZKE3 bzgl. Ruhestromverhalten einstellen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PATCH_OK | int | 1: Patch  IO (Patch durchgefuehrt) 2: Patch  IO (ohne Patch) -1: Patch NIO (Test1 = nio) -2: Patch NIO (Test2 = nio) -3: Patch NIO (Test3 = nio) |
| _TEL_ANTWORT | binary | letzte Hex-Antwort von SG |

<a id="job-patch-test-ruhestrom-gm3"></a>
### PATCH_TEST_RUHESTROM_GM3

Test der Patch-Daten bzgl. Ruhestromverhalten ZKE3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PATCH_OK | int | 1: Patch  IO (Patch durchgefuehrt) 2: Patch  IO (ohne Patch) -1: Patch NIO (Test1 = nio) -2: Patch NIO (Test2 = nio) -3: Patch NIO (Test3 = nio) |
| _TEL_ANTWORT | binary | letzte Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (10 × 2)
- [LIEFERANTEN](#table-lieferanten) (56 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [FORTTEXTE](#table-forttexte) (156 × 2)
- [FARTTEXTE](#table-farttexte) (2 × 2)
- [IORTTEXTE](#table-iorttexte) (34 × 2)
- [BITS](#table-bits) (87 × 6)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 10 rows × 2 columns

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
| 0x?? | ERROR_ECU_UNKNOWN_STATUSBYTE |

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 156 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xB4 | Energiesparmode gesetzt |
| 0x01 | Sicherung Fensterheber hinten |
| 0x02 | Sicherung Innenraumbeleuchtung |
| 0x03 | Sicherung DWA-Horn |
| 0x04 | Leitung Klemme R am GM III |
| 0x08 | Codierung Block 0 nicht erfolgt |
| 0x09 | Codierung Block 1 oder Block 2 nicht erfolgt |
| 0x0A | Codierung Block 0 nicht korrekt |
| 0x0B | Codierung Block 1 oder Block 2 nicht korrekt |
| 0x30 | Wischerschalter, Potentiometer |
| 0x31 | Wischermotor blockiert, Rueckstellkontakt, Wischerrelais |
| 0x33 | Kurzschluss Wascherpumpe |
| 0x34 | Unterbrechung ADV-Motor |
| 0x35 | Kurzschluss ADV-Motor |
| 0x36 | Nockenschalter |
| 0x37 | Unterbrechung Ansteuerung SIR, DRM 2 |
| 0x38 | Unterbrechung Ansteuerung SRA, DRM 2 |
| 0x39 | Relaiskleber nach U-Batt im DRM 2 |
| 0x48 | Leitung WI1 Kurzschluss gegen U-Batt oder Wischerrelais 1 |
| 0x49 | Leitung WI1 Unterbrechung oder Wischerrelais 1 |
| 0x4A | Leitung WI2 Kurzschluss gegen U-Batt oder Wischerrelais 2 |
| 0x4B | Leitung WI2 Unterbrechung oder Wischerrelais 2 |
| 0x40 | Leitungsunterbrechung Innenraumbeleuchtung |
| 0x41 | Kurzschluss Innenraumbeleuchtung |
| 0x44 | Leitungsunterbrechung Tuerschlossheizung |
| 0x45 | Kurzschluss Tuerschlossheizung |
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
| 0x5D | ZV-Antrieb FT oder Leitung STZVFT defekt |
| 0x5E | ZV-Antrieb BT oder Leitung STZVBT defekt |
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
| 0x82 | Leitung Tacho A oder IKE fehlt |
| 0x83 | Leitung Tacho A oder IKE unplausibel |
| 0x91 | Kurzschluss Signal DWAH oder Leitungen |
| 0x92 | Neigungsgeber: Sicherung oder Leitung |
| 0x93 | DWA-LED: Kurzschluss gegen U-Batt oder Leitung DWAL |
| 0x94 | DWA-LED: Unterbrechung oder Leitung DWAL, KL30 |
| 0x95 | Innenraumschutz: Sicherung oder Leitung |
| 0x96 | Innenraumschutz hinten: Sicherung oder Leitung |
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
| 0xC0 | FS Laengsverstellung: Uebertragungsfehler |
| 0xC1 | FS Laengsverstellung: Kurzschluss |
| 0xC2 | FS Laengsverstellung: Blockierung vorne |
| 0xC3 | FS Laengsverstellung: Blockierung hinten |
| 0xC4 | FS Sitzhoehe: Uebertragungsfehler |
| 0xC5 | FS Sitzhoehe: Kurzschluss |
| 0xC6 | FS Sitzhoehe: Blockierung oben |
| 0xC7 | FS Sitzhoehe: Blockierung unten |
| 0xC8 | FS Sitzneigung: Uebertragungsfehler |
| 0xC9 | FS Sitzneigung: Kurzschluss |
| 0xCA | FS Sitzneigung: Blockierung oben |
| 0xCB | FS Sitzneigung: Blockierung unten |
| 0xCC | FS Sitzlehne: Uebertragungsfehler |
| 0xCD | FS Sitzlehne: Kurzschluss |
| 0xCE | FS Sitzlehne: Blockierung vorne |
| 0xCF | FS Sitzlehne: Blockierung hinten |
| 0xD0 | FS Kopfstuetze: Uebertragungsfehler |
| 0xD1 | FS Kopfstuetze: Kurzschluss |
| 0xD2 | FS Kopfstuetze: Blockierung oben |
| 0xD3 | FS Kopfstuetze: Blockierung unten |
| 0xD4 | FS Sitztiefe: Uebertragungsfehler |
| 0xD5 | FS Sitztiefe: Kurzschluss |
| 0xD6 | FS Sitztiefe: Blockierung oben |
| 0xD7 | FS Sitztiefe: Blockierung unten |
| 0xD8 | FS Lehnenkopf: Uebertragungsfehler |
| 0xD9 | FS Lehnenkopf: Kurzschluss |
| 0xDA | FS Lehnenkopf: Blockierung vorne |
| 0xDB | FS Lehnenkopf: Blockierung hinten |
| 0xDC | LS Neigung: Uebertragungsfehler |
| 0xDD | LS Neigung: Kurzschluss |
| 0xDE | LS Neigung: Blockierung oben |
| 0xDF | LS Neigung: Blockierung unten |
| 0xE0 | LS Laengsverstellung: Uebertragungsfehler |
| 0xE1 | LS Laengsverstellung: Kurzschluss |
| 0xE2 | LS Laengsverstellung: Blockierung vorne |
| 0xE3 | LS Laengsverstellung: Blockierung hinten |
| 0xE4 | BFS Laengsverstellung: Uebertragungsfehler |
| 0xE5 | BFS Laengsverstellung: Kurzschluss |
| 0xE6 | BFS Laengsverstellung: Blockierung vorne |
| 0xE7 | BFS Laengsverstellung: Blockierung hinten |
| 0xE8 | BFS Sitzhoehe: Uebertragungsfehler |
| 0xE9 | BFS Sitzhoehe: Kurzschluss |
| 0xEA | BFS Sitzhoehe: Blockierung oben |
| 0xEB | BFS Sitzhoehe: Blockierung unten |
| 0xEC | BFS Sitzneigung: Uebertragungsfehler |
| 0xED | BFS Sitzneigung: Kurzschluss |
| 0xEE | BFS Sitzneigung: Blockierung oben |
| 0xEF | BFS Sitzneigung: Blockierung unten |
| 0xF0 | BFS Sitzlehne: Uebertragungsfehler |
| 0xF1 | BFS Sitzlehne: Kurzschluss |
| 0xF2 | BFS Sitzlehne: Blockierung vorne |
| 0xF3 | BFS Sitzlehne: Blockierung hinten |
| 0xF4 | BFS Kopfstuetze: Uebertragungsfehler |
| 0xF5 | BFS Kopfstuetze: Kurzschluss |
| 0xF6 | BFS Kopfstuetze: Blockierung oben |
| 0xF7 | BFS Kopfstuetze: Blockierung unten |
| 0xF8 | BFS Sitztiefe: Uebertragungsfehler |
| 0xF9 | BFS Sitztiefe: Kurzschluss |
| 0xFA | BFS Sitztiefe: Blockierung oben |
| 0xFB | BFS Sitztiefe: Blockierung unten |
| 0xFC | BFS Lehnenkopf: Uebertragungsfehler |
| 0xFD | BFS Lehnenkopf: Kurzschluss |
| 0xFE | BFS Lehnenkopf: Blockierung vorne |
| 0xFF | BFS Lehnenkopf: Blockierung hinten |
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

Dimensions: 34 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x70 | Unterbrechung Servoventil oder Leitungen (SERV1, SERV2) |
| 0x71 | Kurzschluss Servoventil oder Leitungen (SERV1, SERV2) |
| 0x72 | Leitung Tacho A oder IKE fehlt |
| 0x73 | Leitung Tacho A oder IKE unplausibel |
| 0x80 | DWA-Alarm : Klemme R |
| 0x81 | DWA-Alarm : Klemme 15 |
| 0x82 | DWA-Alarm : Panik-Mode |
| 0x83 | DWA-Alarm : Tuerkontakt FT |
| 0x84 | DWA-Alarm : Tuerkontakt BT |
| 0x85 | DWA-Alarm : Tuerkontakt FTH |
| 0x86 | DWA-Alarm : Tuerkontakt BTH |
| 0x87 | DWA-Alarm : Heckklappenkontakt |
| 0x88 | DWA-Alarm : Handschuhfachkontakt |
| 0x89 | DWA-Alarm : Motorhaubenkontakt |
| 0x8A | DWA-Alarm : Neigungsgeber |
| 0x8B | DWA-Alarm : Heckscheibe oder Innenraumschutz |
| 0x8C | DWA-Alarm : Scheibenueberwachung FT |
| 0x8D | DWA-Alarm : Scheibenueberwachung BT |
| 0x8E | DWA-Alarm : Scheibenueberwachung FTH |
| 0x8F | DWA-Alarm : Scheibenueberwachung BTH |
| 0x93 | Power Up vom GM III |
| 0x94 | Power Up vom PM FT |
| 0x95 | Power Up vom PM BT |
| 0xA0 | Wiederholsperre ZV angesprochen |
| 0xA1 | Crash-Sensor hat angesprochen |
| 0xA2 | BC hat WFSI angesteuert |
| 0xA3 | BC hat DWA-Horn angesteuert |
| 0xA4 | Spiegel- u. ZV-Treiber in PM FT hat Uerbertemp.absch. angespr. |
| 0xA5 | Spiegel- u. ZV-Treiber in PM BT hat Uerbertemp.absch. angespr. |
| 0x60 | Fensterheber-Motor FT |
| 0x61 | Fensterheber-Motor BT |
| 0x62 | Fensterheber-Motor FTH |
| 0x63 | Fensterheber-Motor BTH |
| 0xXY | unbekannter Info-Ort |

<a id="table-bits"></a>
### BITS

Dimensions: 87 rows × 6 columns

| NAME | BYTE | MASK | VALUE | ART | TEXT |
| --- | --- | --- | --- | --- | --- |
| SFFHA | 1 | 0x01 | 0x01 | E | FH-Schalter FH auf |
| SFFHZ | 1 | 0x02 | 0x02 | E | FH-Schalter FH zu |
| SIR | 1 | 0x04 | 0x04 | E | Schalter Wischer Intensivpumpe |
| SFBHA | 1 | 0x08 | 0x08 | E | FH-Schalter BH auf |
| SFBHZ | 1 | 0x10 | 0x10 | E | FH-Schalter BH zu |
| SCAO | 1 | 0x20 | 0x20 | E | Schalter Softcloseautomatik offen |
| RSK | 1 | 0x40 | 0x40 | E | Rueckstellkontakt Wischer |
| NS | 1 | 0x80 | 0x80 | E | Nockenschalter ADV |
| TOEHS | 1 | 0x80 | 0x80 | E | Taster zum Oeffnen der Heckscheibe |
| TOEHKI | 2 | 0x01 | 0x01 | E | Taster zum Oeffnen der Heckklappe von Innen |
| TOEHK | 2 | 0x02 | 0x02 | E | Taster zum Oeffnen der Heckklappe |
| HKK | 2 | 0x04 | 0x04 | E | Heckklappenkontakt |
| TZV | 2 | 0x08 | 0x08 | E | Taste zum Umschalten der ZV |
| VRHK | 2 | 0x10 | 0x10 | E | Schalter Schliesszylinder Heckklappe Verriegeln |
| KLR | 2 | 0x20 | 0x20 | E | Klemme R |
| ERHK | 2 | 0x40 | 0x40 | E | Schalter Schliesszylinder Heckklappe Entriegeln |
| DSIR | 2 | 0x80 | 0x80 | E | Diagnoserueckmeldung MIP und MSRA |
| TKFT | 3 | 0x01 | 0x01 | E | Tuerkontakt FT (vorgesehen am GM III) |
| TKBT | 3 | 0x02 | 0x02 | E | Tuerkontakt BT (vorgesehen am GM III) |
| TKFH | 3 | 0x04 | 0x04 | E | Tuerkontakt FTH |
| TKBH | 3 | 0x08 | 0x08 | E | Tuerkontakt BTH |
| SW1 | 3 | 0x10 | 0x10 | E | Schalter Wischer INT, ST2 kodiert |
| SW2 | 3 | 0x20 | 0x20 | E | Schalter Wischer ST1, ST2 kodiert |
| SWP | 3 | 0x40 | 0x40 | E | Schalter Wischer Wascherpumpe |
| SIB | 3 | 0x80 | 0x80 | E | Schalter Innenraumbeleuchtung |
| MHK | 4 | 0x01 | 0x01 | E | Motorhaubenkontakt |
| REE2 | 4 | 0x02 | 0x02 | E | Reserve Eingang 2 |
| HFK | 4 | 0x04 | 0x04 | E | Handschuhfachkontakt |
| INRS | 4 | 0x08 | 0x08 | E | Innenraumschutz (Heckscheibe oder Innenraum) |
| SUEFH | 4 | 0x10 | 0x10 | E | Scheibenueberwachung Fahrer Hinten |
| SUEBH | 4 | 0x20 | 0x20 | E | Scheibenueberwachung Beifahrer Hinten |
| NGEG | 4 | 0x40 | 0x40 | E | Schnittstellle zum Neigungsgeber |
| REE1 | 4 | 0x80 | 0x80 | E | Reserve Eingang 1 |
| FIS2 | 4 | 0x10 | 0x10 | E | Funkinnenraumschutz Hinten |
| HSK | 4 | 0x20 | 0x20 | E | Heckscheibenkontakt |
| DMERHK | 5 | 0x01 | 0x01 | IE | interne Diagnoserueckfuehrung Motor ERHK |
| DMVR | 5 | 0x02 | 0x02 | IE | interne Diagnoserueckfuehrung Motor VR |
| DMER | 5 | 0x04 | 0x04 | IE | interne Diagnoserueckfuehrung Motor ER |
| DMZS | 5 | 0x08 | 0x08 | IE | interne Diagnoserueckfuehrung Motor ZS |
| DMFFHZ | 5 | 0x10 | 0x10 | IE | interne Diagnoserueckfuehrung Motor FFHZ |
| DMFFHA | 5 | 0x20 | 0x20 | IE | interne Diagnoserueckfuehrung Motor FFHA |
| DMFBHZ | 5 | 0x40 | 0x40 | IE | interne Diagnoserueckfuehrung Motor FBHZ |
| DMFBHA | 5 | 0x80 | 0x80 | IE | interne Diagnoserueckfuehrung Motor FBHA |
| KL30GM | 6 | 0x01 | 0x01 | E | Klemme 30 &gt; 7V, keine Untersp. an GM III |
| CS | 6 | 0x04 | 0x04 | E | Crash-Sensor |
| DADV | 7 | 0x02 | 0x02 | IE | interne Diagnoserueckfuehrung ADV AUF und ZU |
| DVA | 7 | 0x04 | 0x04 | IE | interne Diagnoserueckfuehrung VA |
| DIB | 7 | 0x08 | 0x08 | IE | interne Diagnoserueckfuehrung IB |
| DSERVO | 7 | 0x10 | 0x10 | IE | interne Diagnoserueckfuehrung SERVO |
| DWP | 7 | 0x20 | 0x20 | IE | interne Diagnoserueckfuehrung WP |
| DDWAH | 7 | 0x40 | 0x40 | IE | interne Diagnoserueckfuehrung DWAH |
| WI1 | 8 | 0x01 | 0x01 | A | Relaisspule Wischer Stufe 1 |
| WI2 | 8 | 0x02 | 0x02 | A | Relaisspule Wischer Stufe 2 |
| SRA | 8 | 0x04 | 0x04 | A | Relais Scheinwerferreinigung |
| IP | 8 | 0x08 | 0x08 | A | Relais Scheibenintensivreinigung |
| DWAL | 8 | 0x10 | 0x10 | A | DWA Leuchtdiode |
| NGAG | 8 | 0x20 | 0x20 | A | Neigungsgeberausgang |
| ANLE | 8 | 0x40 | 0x40 | A | Anlasser Enable von Anlass-Sperr-Relais |
| RERHK | 8 | 0x80 | 0x80 | A | Relais Entriegelung Heckklappe E39/2 |
| RERHS | 8 | 0x40 | 0x40 | A | Relais Entriegelung Heckscheibe E39/2 |
| MHKER | 9 | 0x01 | 0x01 | A | Motor Heckklappe Entriegeln oder SCA |
| MVR | 9 | 0x02 | 0x02 | A | internes Relais ZV Verriegeln |
| MER | 9 | 0x04 | 0x04 | A | internes Relais ZV Entriegeln |
| MZS | 9 | 0x08 | 0x08 | A | internes Relais ZV Sichern |
| MFFHZ | 9 | 0x10 | 0x10 | A | internes Relais Fenster Fahrer Hinten Zu |
| MFFHA | 9 | 0x20 | 0x20 | A | internes Relais Fenster Fahrer Hinten Auf |
| MFBHZ | 9 | 0x40 | 0x40 | A | internes Relais Fenster Beifahrer Hinten Zu |
| MFBHA | 9 | 0x80 | 0x80 | A | internes Relais Fenster Beifahrer Hinten Auf |
| RXD | 10 | 0x01 | 0x01 | EN | K-Bus RxD |
| TXD | 10 | 0x02 | 0x02 | AN | K-Bus TxD |
| DWAH | 10 | 0x04 | 0x04 | A | DWA Horn |
| WP | 10 | 0x08 | 0x08 | A | Wascherpumpe |
| MADVZ | 10 | 0x10 | 0x10 | A | Anpressdruckverstellung Zu |
| MADVA | 10 | 0x20 | 0x20 | A | Anpressdruckverstellung Auf |
| VA | 11 | 0x01 | 0x01 | A | Verbraucherabschaltung |
| WFSI | 11 | 0x02 | 0x02 | A | Wegfahrsicherung |
| U2OFF | 11 | 0x04 | 0x04 | IA | VCC2 6,5V Off |
| IC6MM | 11 | 0x10 | 0x10 | IA | IC 6 Monitormode |
| SIRENE | 11 | 0x20 | 0x20 | A | DWA-Notstromsirene |
| P_VRFT | 18 | 0x01 | 0x01 | PS | ZV-Schalterpaket FT Verriegeln |
| P_VRBT | 20 | 0x01 | 0x01 | PS | ZV-Schalterpaket BT Verriegeln |
| K_KLR | 22 | 0x01 | 0x01 | KS | Klemme R (ueber K-Bus) |
| K_KL15 | 22 | 0x02 | 0x02 | KS | Klemme 15 (ueber K-Bus) |
| K_KL50 | 22 | 0x04 | 0x04 | KS | Klemme 50 (ueber K-Bus) |
| K_VRFS | 23 | 0x02 | 0x02 | KS | Verriegeln von FBZV |
| K_KL58 | 25 | 0x02 | 0x02 | KS | Klemme 58 (ueber K-Bus) |
| XY | XY | 0xXY | 0xXY | XY | nicht definiertes Signal |
