# DDE22DS0.prg

- Jobs: [73](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | DDE 2.2 fuer M51 E38 / E39 |
| ORIGIN | BMW TI-433 Schiefer |
| REVISION | 1.26 |
| AUTHOR | BMW TP-421 Weber, BMW TP-421 Teepe, BMW TP-421 Mellersh, BMW TI-433 Schiefer |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [EDIC_RESET](#job-edic-reset) - EDIC-Reset
- [initialisierung](#job-initialisierung) - Default Init-Job
- [INFO](#job-info) - Information SGBD
- [ISN_LESEN](#job-isn-lesen)
- [ISN_LESEN_ROH](#job-isn-lesen-roh)
- [RAM_LESEN](#job-ram-lesen) - Beliebige RAM - Zellen auslesen
- [ROM_LESEN](#job-rom-lesen) - Beliebige EPROM - Zellen auslesen
- [EEPROM_LESEN](#job-eeprom-lesen) - Beliebige EPROM - Zellen auslesen
- [ADC_LESEN](#job-adc-lesen) - Beliebigen ADC Kanal auslesen
- [EEPROM_SCHREIBEN](#job-eeprom-schreiben) - Beliebige EEPROM Zellen mit 02 beschreiben
- [IDENT](#job-ident) - Ident-Daten fuer DME
- [ECU_CONFIG](#job-ecu-config) - Ident-Daten fuer DME
- [CODIER_VARIANTE_LESEN](#job-codier-variante-lesen) - Auslesen des Varianten - Steuerwort
- [ABGAS_VARIANTE_LESEN](#job-abgas-variante-lesen) - Auslesen der Abgasvariante
- [STATUS_CODIER_CHECKSUMME](#job-status-codier-checksumme) - Codier - Checksumme abfragen
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Auslesen des QUICK Fehlerspeichers
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [FS_SHADOW_LESEN](#job-fs-shadow-lesen) - Auslesen des SCHADOW Fehlerspeichers
- [STATUS_SPRITZBEGINN_SOLL](#job-status-spritzbeginn-soll) - Job Spritzbeginn Soll
- [STATUS_SPRITZBEGINN_IST](#job-status-spritzbeginn-ist) - Job Spritzbeginn IST
- [STATUS_MENGE_AKTUELL](#job-status-menge-aktuell) - Menge Aktuell
- [STATUS_PWG](#job-status-pwg) - PWG
- [STATUS_PWG_POTI_SPANNUNG](#job-status-pwg-poti-spannung) - PWG
- [STATUS_FGR](#job-status-fgr) - PWG
- [STATUS_LADEDRUCK](#job-status-ladedruck) - Ladedruck
- [STATUS_SCHIEBERWEG_IST](#job-status-schieberweg-ist) - Schieberweg IST
- [STATUS_SCHIEBERWEG_SOLL](#job-status-schieberweg-soll) - Schieberweg SOLL
- [STATUS_LUFTMASSE](#job-status-luftmasse) - LUFTMASSE
- [STATUS_LL_ABGLEICH](#job-status-ll-abgleich) - LL_Abgleich
- [STATUS_GM_ABGLEICH](#job-status-gm-abgleich) - Grundmengenabgleich
- [STATUS_SM_ABGLEICH](#job-status-sm-abgleich) - Startmengenabgleich
- [STATUS_KUEHLMITTELTEMPERATUR](#job-status-kuehlmitteltemperatur) - Job Kuehlmitteltemperatur
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - Job Kuehlmitteltemperatur
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Motordrehzahl auslesen
- [STATUS_OELTEMPERATUR](#job-status-oeltemperatur) - LADELUFTtemperatur
- [STATUS_KRAFTSTOFFTEMPERATUR](#job-status-kraftstofftemperatur) - Ansauglufttemperatur
- [STATUS_UBATT](#job-status-ubatt) - Batteriespannung
- [STATUS_GESCHWINDIGKEIT](#job-status-geschwindigkeit) - Fahrzeuggeschwindigkeit
- [STATUS_AGR_ABGLEICH](#job-status-agr-abgleich) - AGR - Abgleich
- [STATUS_FAHRVER_MENGE](#job-status-fahrver-menge) - Fahrverhalten Menge
- [STATUS_BEGRENZ_MENGE](#job-status-begrenz-menge) - Begrenzungsmenge
- [STATUS_SOLL_LL_DREHZ](#job-status-soll-ll-drehz) - Soll LL-Drehzahl
- [STATUS_ATMOS_DRUCK](#job-status-atmos-druck) - Atmosphaerendruck
- [STATUS_MW1](#job-status-mw1) - Messwert BLock 1 auslesen
- [STATUS_MW2](#job-status-mw2) - Messwerte (einzelne RAM - Zellen) auslesen
- [STATUS_MW3](#job-status-mw3) - Messwerte (einzelne RAM - Zellen) auslesen
- [STATUS_MW4](#job-status-mw4) - Messwerte (einzelne RAM - Zellen) auslesen
- [STATUS_MW5](#job-status-mw5) - Messwerte (einzelne RAM - Zellen) auslesen
- [STATUS_DIGITAL](#job-status-digital) - Status Schalteingaenge
- [STATUS_DIGITAL1](#job-status-digital1) - Status Schalteingaenge
- [STEUERN_ELAB](#job-steuern-elab) - ELAB  ansteuern
- [STEUERN_SB_VENTIL](#job-steuern-sb-ventil) - Magnetventil fuer Spritzbeginn ansteuern
- [STEUERN_AGR_STELLER](#job-steuern-agr-steller) - AGR Steller ansteuern
- [STEUERN_GLUEH_RELAIS](#job-steuern-glueh-relais) - Glueg Relais ansteuern
- [STEUERN_DIAGNOSE_ANZEIGE](#job-steuern-diagnose-anzeige) - Diagnoseanzeige ansteuern
- [STEUERN_KLIMA_KOMP](#job-steuern-klima-komp) - Klimakompressor ansteuern
- [STEUERN_VORGLUEHLAMPE](#job-steuern-vorgluehlampe) - Vorgluehlampe ansteuern
- [STEUERN_FGR_LAMPE](#job-steuern-fgr-lampe) - FGR - Lampe ansteuern
- [STEUERN_LADER](#job-steuern-lader) - Lader ansteuern
- [STEUERN_MOTORLAGER](#job-steuern-motorlager) - FGR - Lampe ansteuern
- [STEUERN_VORFOERDERPUMPE](#job-steuern-vorfoerderpumpe) - Vorfoerderpumpe ansteuern
- [STEUERN_EKP](#job-steuern-ekp) - Vorfoerderpumpe ansteuern
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Loeschen des Fehlerspeichers
- [LOGIN_REQUEST](#job-login-request) - Freigabe fuer EEP-Funktionen
- [ABGLEICHWERTE_SCHREIBEN](#job-abgleichwerte-schreiben) - Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten
- [ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - Lesen des EEPROM-Speichers ab Adresse 0x8022
- [ABGLEICHFLAG_SCHREIBEN](#job-abgleichflag-schreiben) - Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten
- [ABGLEICHFLAG_LESEN](#job-abgleichflag-lesen) - Lesen des EEPROM-Speichers ab Adresse 0x0032
- [ABGLEICH_LL_DREHZAHL_770](#job-abgleich-ll-drehzahl-770)
- [STATUS_LL_DREHZAHL_770](#job-status-ll-drehzahl-770)
- [EEPROM_BYTE_AENDERN](#job-eeprom-byte-aendern) - Beliebige EPROM - Zellen aendern
- [EEPROM_BYTE_ABFRAGE](#job-eeprom-byte-abfrage) - Beliebige EPROM - Zellen abfragen

<a id="job-edic-reset"></a>
### EDIC_RESET

EDIC-Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-initialisierung"></a>
### initialisierung

Default Init-Job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn job erfolgreich 0 wenn job nicht erfolgreich |

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

<a id="job-isn-lesen"></a>
### ISN_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ISN_LESEN_WERT | string | ISN als  WERT |
| JOB_STATUS | string |  |

<a id="job-isn-lesen-roh"></a>
### ISN_LESEN_ROH

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ISN_LESEN_WERT | string | ISN als  WERT |
| JOB_STATUS | string |  |

<a id="job-ram-lesen"></a>
### RAM_LESEN

Beliebige RAM - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RAM_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |
| RAM_LESEN_ANZAHL_BYTE | int | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| RAM_LESEN_WERT | binary | nichts |
| RAM_LESEN_EINH | string | Einheit HEX |

<a id="job-rom-lesen"></a>
### ROM_LESEN

Beliebige EPROM - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ROM_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |
| ROM_LESEN_ANZAHL_BYTE | int | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ROM_LESEN_WERT | binary | nichts |
| ROM_LESEN_EINH | string | Einheit HEX |

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

Beliebige EPROM - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EEPROM_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |
| EEPROM_LESEN_ANZAHL_BYTE | int | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| EEPROM_LESEN_WERT | binary | nichts |
| EEPROM_LESEN_EINH | string | Einheit HEX |

<a id="job-adc-lesen"></a>
### ADC_LESEN

Beliebigen ADC Kanal auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADC_KANAL | int | Uebergabeparameter, Kanal fuer ADC Lesen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ADC_LESEN_WERT | int | nichts |
| ADC_LESEN_EINH | string | Einheit HEX |

<a id="job-eeprom-schreiben"></a>
### EEPROM_SCHREIBEN

Beliebige EEPROM Zellen mit 02 beschreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EEPROM_SCHREIBEN_ADRESSE_DATEN | binary | Uebergabeparameter, Startadresse High-Middle-Low und Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| EEPROM_SCHREIBEN_ADRESSE | binary | nichts |
| EEPROM_SCHREIBEN_STATUS | int | nichts |
| EEPROM_SCHREIBEN_ANZAHL | int | nichts |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer DME

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_VARIANTEN_NR | string | Variante |
| ID_BUS_INDEX | string | Bus-Index |
| ID_DATUM | string | Herstelldatum |
| ID_SW_NR | string | Softwarenummer |
| ID_DATENSTAND | string | Datenstand |
| ID_DATENSATZ | string | Datensatz |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) |
| ID_MOTOR | string | SG - Identifikation fuer MoTest |
| ID_LAMBDA_STEREO | int | Parameter fuer MoTest 0=Mono, 1=STEREO |
| ID_EML | int | Parameter fuer MoTest 0=Kein EML verb, 1=EML M70, 2=EML M73 |
| ID_LU_MESSUNG | int | Parameter fuer MoTest 1=Laufunruhemessung sonst 0 |
| ID_OBD2 | int | Parameter fuer MoTest 0=ECE, 1=OBD2-Fahrzeug |
| ID_SG_HERSTELLER | int | Parameter fuer MoTest 0=Bosch, 1=Siemens-Fahrzeug |
| ID_EWS_SS | int | Identifikation EWS-Schnittstelle |

<a id="job-ecu-config"></a>
### ECU_CONFIG

Ident-Daten fuer DME

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| EGS_VORHANDEN | int | EGS vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |

<a id="job-codier-variante-lesen"></a>
### CODIER_VARIANTE_LESEN

Auslesen des Varianten - Steuerwort

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| CODIER_VARIANTE | string | Varianten - Steuerwort |

<a id="job-abgas-variante-lesen"></a>
### ABGAS_VARIANTE_LESEN

Auslesen der Abgasvariante

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ABGAS_VARIANTE_WERT | int | Abgasvariante 0=KAT-V , 1= KAT |

<a id="job-status-codier-checksumme"></a>
### STATUS_CODIER_CHECKSUMME

Codier - Checksumme abfragen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_CHECKSUMME_WERT | int | Ergebnis |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Auslesen des QUICK Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_BSZ_AKT | real | Betriebsstundenzahler aktuell |
| F_BSZ_ALT | real | Betriebsstundenzaehler beim letzten Loeschen |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_ORT_NR | int | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
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
| F_ART5_NR | int | Fehlerart 5 Index |
| F_ART5_TEXT | string | Fehlerart 5 Text |
| F_ART6_NR | int | Fehlerart 6 Index |
| F_ART6_TEXT | string | Fehlerart 6 Text |
| F_ART7_NR | int | Fehlerart 7 Index |
| F_ART7_TEXT | string | Fehlerart 7 Text |
| F_ART8_NR | int | Fehlerart 8 Index |
| F_ART8_TEXT | string | Fehlerart 8  Text |
| F_UW1_NR | int | Umweltbedingung 1 Index |
| F_UW1_TEXT | string | Umweltbedingung 1 Einheit |
| F_UW1_EINH | string | Umweltbedingung 1 Text |
| F_UW1_WERT | real | Umweltbedingung 1 Wert |
| F_UW2_NR | int | Umweltbedingung 2Index |
| F_UW2_TEXT | string | Umweltbedingung 2 Text |
| F_UW2_EINH | string | Umweltbedingung 2 Einheit |
| F_UW2_WERT | real | Umweltbedingung 2 Wert |
| F_UW3_NR | int | Umweltbedingung 3 Index |
| F_UW3_TEXT | string | Umweltbedingung 3 Text |
| F_UW3_EINH | string | Umweltbedingung 3 Einheit |
| F_UW3_WERT | real | Umweltbedingung 3 Wert |
| F_CODEHEX | binary | 5 Fehlerbyte |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-fs-shadow-lesen"></a>
### FS_SHADOW_LESEN

Auslesen des SCHADOW Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_ORT_NR | int | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
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
| F_ART5_NR | int | Fehlerart 5 Index |
| F_ART5_TEXT | string | Fehlerart 5 Text |
| F_ART6_NR | int | Fehlerart 6 Index |
| F_ART6_TEXT | string | Fehlerart 6 Text |
| F_ART7_NR | int | Fehlerart 7 Index |
| F_ART7_TEXT | string | Fehlerart 7 Text |
| F_ART8_NR | int | Fehlerart 8 Index |
| F_ART8_TEXT | string | Fehlerart 8  Text |
| F_UW1_NR | int | Umweltbedingung 1 Index |
| F_UW1_TEXT | string | Umweltbedingung 1 Einheit |
| F_UW1_EINH | string | Umweltbedingung 1 Text |
| F_UW1_WERT | real | Umweltbedingung 1 Wert |
| F_UW2_NR | int | Umweltbedingung 2Index |
| F_UW2_TEXT | string | Umweltbedingung 2 Text |
| F_UW2_EINH | string | Umweltbedingung 2 Einheit |
| F_UW2_WERT | real | Umweltbedingung 2 Wert |
| F_UW3_NR | int | Umweltbedingung 3 Index |
| F_UW3_TEXT | string | Umweltbedingung 3 Text |
| F_UW3_EINH | string | Umweltbedingung 3 Einheit |
| F_UW3_WERT | real | Umweltbedingung 3 Wert |
| F_CODEHEX | binary | 5 Fehlerbyte |

<a id="job-status-spritzbeginn-soll"></a>
### STATUS_SPRITZBEGINN_SOLL

Job Spritzbeginn Soll

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_SPRITZBEGINN_SOLL_WERT | real | Wert |
| STATUS_SPRITZBEGINN_SOLL_EINH | string | Einheit |

<a id="job-status-spritzbeginn-ist"></a>
### STATUS_SPRITZBEGINN_IST

Job Spritzbeginn IST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_SPRITZBEGINN_IST_WERT | real | Wert |
| STATUS_SPRITZBEGINN_IST_EINH | string | Einheit |

<a id="job-status-menge-aktuell"></a>
### STATUS_MENGE_AKTUELL

Menge Aktuell

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MENGE_AKTUELL_WERT | real | Batteriespannung Wert |
| STATUS_MENGE_AKTUELL_EINH | string | Einheit |

<a id="job-status-pwg"></a>
### STATUS_PWG

PWG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_PWG_WERT | real | PWG Wert |
| STATUS_PWG_EINH | string | Einheit |

<a id="job-status-pwg-poti-spannung"></a>
### STATUS_PWG_POTI_SPANNUNG

PWG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_PWG_POTI_SPANNUNG_1_WERT | real | PWG Wert |
| STAT_PWG_POTI_SPANNUNG_EINH | string | Einheit |

<a id="job-status-fgr"></a>
### STATUS_FGR

PWG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_FGR_WERT | real | FGR Bedienteil  Wert in mV |
| STATUS_FGR_EINH | string | Einheit |

<a id="job-status-ladedruck"></a>
### STATUS_LADEDRUCK

Ladedruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LADEDRUCK_WERT | real | Ladedruck Wert |
| STATUS_LADEDRUCK_EINH | string | Einheit |

<a id="job-status-schieberweg-ist"></a>
### STATUS_SCHIEBERWEG_IST

Schieberweg IST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_SCHIEBERWEG_IST_WERT | real | Schieberweg IST Wert |
| STATUS_SCHIEBERWEG_IST_EINH | string | Einheit |

<a id="job-status-schieberweg-soll"></a>
### STATUS_SCHIEBERWEG_SOLL

Schieberweg SOLL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_SCHIEBERWEG_SOLL_WERT | real | Schieb.weg Soll Wert |
| STATUS_SCHIEBERWEG_SOLL_EINH | string | Einheit |

<a id="job-status-luftmasse"></a>
### STATUS_LUFTMASSE

LUFTMASSE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LUFTMASSE_WERT | real | LUFTMASSE Wert |
| STATUS_LUFTMASSE_EINH | string | Einheit |

<a id="job-status-ll-abgleich"></a>
### STATUS_LL_ABGLEICH

LL_Abgleich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LL_ABGLEICH_WERT | real | LL-Abgleich Wert |
| STATUS_LL_ABGLEICH_EINH | string | Einheit |

<a id="job-status-gm-abgleich"></a>
### STATUS_GM_ABGLEICH

Grundmengenabgleich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_GM_ABGLEICH_WERT | real | GM - Abgleich Wert |
| STATUS_GM_ABGLEICH_EINH | string | Einheit |

<a id="job-status-sm-abgleich"></a>
### STATUS_SM_ABGLEICH

Startmengenabgleich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_SM_ABGLEICH_WERT | real | Startmengenabgleich Wert |
| STATUS_SM_ABGLEICH_EINH | string | Einheit |

<a id="job-status-kuehlmitteltemperatur"></a>
### STATUS_KUEHLMITTELTEMPERATUR

Job Kuehlmitteltemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_KUEHLMITTELTEMPERATUR_WERT | real | Wert |
| STATUS_KUEHLMITTELTEMPERATUR_EINH | string | Einheit |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

Job Kuehlmitteltemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MOTORTEMPERATUR_WERT | real | Wert |
| STAT_MOTORTEMPERATUR_WERT | real | Wert |
| STATUS_MOTORTEMPERATUR_EINH | string | Einheit |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Motordrehzahl auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MOTORDREHZAHL_WERT | real | Motordrehzahl |
| STAT_MOTORDREHZAHL_WERT | real | Motordrehzahl |
| STATUS_MOTORDREHZAHL_EINH | string | Einheit 1/min |

<a id="job-status-oeltemperatur"></a>
### STATUS_OELTEMPERATUR

LADELUFTtemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_OELTEMPERATUR_WERT | real | Ladelufttemperatur Wert |
| STATUS_OELTEMPERATUR_EINH | string | Einheit Grad C |

<a id="job-status-kraftstofftemperatur"></a>
### STATUS_KRAFTSTOFFTEMPERATUR

Ansauglufttemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_KRAFTSTOFFTEMPERATUR_WERT | real | Kraftstofftemperatur Wert |
| STATUS_KRAFTSTOFFTEMPERATUR_EINH | string | Einheit Grad C |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

Batteriespannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_UBATT_WERT | real | Batteriespannung Wert |
| STATUS_UBATT_EINH | string | Einheit V |

<a id="job-status-geschwindigkeit"></a>
### STATUS_GESCHWINDIGKEIT

Fahrzeuggeschwindigkeit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_GESCHWINDIGKEIT_WERT | real | Geschwindigkeit Wert |
| STATUS_GESCHWINDIGKEIT_EINH | string | Einheit kmh |

<a id="job-status-agr-abgleich"></a>
### STATUS_AGR_ABGLEICH

AGR - Abgleich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_AGR_ABGLEICH_WERT | real | AGR - Abgleich Wert |
| STATUS_AGR_ABGLEICH_EINH | string | Einheit |

<a id="job-status-fahrver-menge"></a>
### STATUS_FAHRVER_MENGE

Fahrverhalten Menge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_FAHRVER_MENGE_WERT | real | Fahrverhalten Menge Wert |
| STATUS_FAHRVER_MENGE_EINH | string | Einheit |

<a id="job-status-begrenz-menge"></a>
### STATUS_BEGRENZ_MENGE

Begrenzungsmenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_BEGRENZ_MENGE_WERT | real | Begrenzungsmenge Wert |
| STATUS_BEGRENZ_MENGE_EINH | string | Einheit |

<a id="job-status-soll-ll-drehz"></a>
### STATUS_SOLL_LL_DREHZ

Soll LL-Drehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_SOLL_LL_DREHZ_WERT | real | Soll LL-Drehzahl Wert |
| STATUS_SOLL_LL_DREHZ_EINH | string | Einheit |

<a id="job-status-atmos-druck"></a>
### STATUS_ATMOS_DRUCK

Atmosphaerendruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ATMOS_DRUCK_WERT | real | Atmosphaerendruck Wert |
| STATUS_ATMOS_DRUCK_EINH | string | Einheit |

<a id="job-status-mw1"></a>
### STATUS_MW1

Messwert BLock 1 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MW1_WERT | real | MW  Wert |
| STATUS_MW1_EINH | string | Einheit |
| STATUS_MW1_TEXT | string | Text |

<a id="job-status-mw2"></a>
### STATUS_MW2

Messwerte (einzelne RAM - Zellen) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MW2_WERT | real | MW  Wert |
| STATUS_MW2_EINH | string | Einheit |
| STATUS_MW2_TEXT | string | Text |

<a id="job-status-mw3"></a>
### STATUS_MW3

Messwerte (einzelne RAM - Zellen) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MW3_WERT | real | MW  Wert |
| STATUS_MW3_EINH | string | Einheit |
| STATUS_MW3_TEXT | string | Text |

<a id="job-status-mw4"></a>
### STATUS_MW4

Messwerte (einzelne RAM - Zellen) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MW4_WERT | real | MW  Wert |
| STATUS_MW4_EINH | string | Einheit |
| STATUS_MW4_TEXT | string | Text |

<a id="job-status-mw5"></a>
### STATUS_MW5

Messwerte (einzelne RAM - Zellen) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MW5_WERT | real | MW  Wert |
| STATUS_MW5_EINH | string | Einheit |
| STATUS_MW5_TEXT | string | Text |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_BREMS_TEST_SCHALTER_EIN | int | Status Bremstestschalter 0=Aus / 1=Ein |
| STATUS_BREMS_LICHT_SCHALTER_EIN | int | Status Bremslichtschalter 0=Aus / 1=Ein |
| STAT_BLS_EIN | int | Status Bremslichtschalter 0=Aus / 1=Ein |
| STATUS_FS_EIN | int | Status FS 0=Aus / 1=Ein |
| STATUS_DWA_EIN | int | Status DWA Eingang 0=Aus / 1=Ein |
| STATUS_PWG_EIN | int | Status PWG Schalter  0=Aus / 1=Ein |
| STATUS_DIA_EIN | int | Status Diagnose Schalter  0=Aus / 1=Ein |
| STATUS_AC_EIN | int | Status AC Schalter  0=Aus / 1=Ein |
| STAT_AC_EIN | int | Status AC Schalter  0=Aus / 1=Ein |
| STATUS_KO_EIN | int | Status Komp. Schalter  0=Aus / 1=Ein |
| STAT_KO_EIN | int | Status Komp. Schalter  0=Aus / 1=Ein |
| STAT_KUP_EIN | int | Status Kup. Schalter  0=Aus / 1=Ein |
| STATUS_TEMPOMAT_HAUPTSCHALTER_EIN | int | Status Tempomat Hauptschalter  0=Aus / 1=Ein |
| STATUS_TEMPOMAT_EIN_EIN | int | Status Tempomat Ein  0=Aus / 1=Ein |
| STATUS_TEMPOMAT_AUS_EIN | int | Status Tempomat Aus  0=Aus / 1=Ein |
| STATUS_TEMPOMAT_WIEDERAUF_EIN | int | Status Tempomat Wiederaufnahme  0=Aus / 1=Ein |

<a id="job-status-digital1"></a>
### STATUS_DIGITAL1

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_DIGITAL1_TEXT | string | Beschreibung Eingang |
| STATUS_DIGITAL1_STATUS | string | Status Eingang |

<a id="job-steuern-elab"></a>
### STEUERN_ELAB

ELAB  ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-sb-ventil"></a>
### STEUERN_SB_VENTIL

Magnetventil fuer Spritzbeginn ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-agr-steller"></a>
### STEUERN_AGR_STELLER

AGR Steller ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-glueh-relais"></a>
### STEUERN_GLUEH_RELAIS

Glueg Relais ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-diagnose-anzeige"></a>
### STEUERN_DIAGNOSE_ANZEIGE

Diagnoseanzeige ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-klima-komp"></a>
### STEUERN_KLIMA_KOMP

Klimakompressor ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-vorgluehlampe"></a>
### STEUERN_VORGLUEHLAMPE

Vorgluehlampe ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-fgr-lampe"></a>
### STEUERN_FGR_LAMPE

FGR - Lampe ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-lader"></a>
### STEUERN_LADER

Lader ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-motorlager"></a>
### STEUERN_MOTORLAGER

FGR - Lampe ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-vorfoerderpumpe"></a>
### STEUERN_VORFOERDERPUMPE

Vorfoerderpumpe ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ekp"></a>
### STEUERN_EKP

Vorfoerderpumpe ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-login-request"></a>
### LOGIN_REQUEST

Freigabe fuer EEP-Funktionen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-abgleichwerte-schreiben"></a>
### ABGLEICHWERTE_SCHREIBEN

Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_SCHREIBEN_ANZAHL | int | Anzahl der zu schreibenden Abgleichdatenbytes ohne die Pruefziffer |
| ABGLEICHWERTE_SCHREIBEN_DATEN | string | Abgleichdaten in folgendem Format z.B. 01 02 AB FF ... &lt;PZ&gt; Datenbytes - 2-stellige Hex-Werte, jeweils gefolgt von einem (1) Leerzeichen - Wertebereich: 00 - FF - nur Grossbuchstaben A - F sind erlaubt Pruefziffer &lt;PZ&gt;: - 1-stelliges Zeichen - Wertebereich: 0 - 9, A - Z - nur Grossbuchstaben A - Z sind erlaubt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_... , wenn argument nicht uebergeben oder ausser Bereich |
| ABGLEICHWERTE_SCHREIBEN_ABGLEICHDATEN | string | Abgleichdaten zum Steuergeraet |
| ABGLEICHWERTE_SCHREIBEN_PRUEFZEICHEN | string | das im Job berechnete Pruefzeichen |

<a id="job-abgleichwerte-lesen"></a>
### ABGLEICHWERTE_LESEN

Lesen des EEPROM-Speichers ab Adresse 0x8022

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_LESEN_ANZAHL | int | Anzahl der zu lesenden Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_LESEN_DATEN | string | aus dem Steuergeraet ausgelesene Daten im Format z.B.: "01 A5 FE" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_..., wenn argument nicht uebergeben oder ausser Bereich |

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

<a id="job-abgleichflag-lesen"></a>
### ABGLEICHFLAG_LESEN

Lesen des EEPROM-Speichers ab Adresse 0x0032

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHFLAG_LESEN_WERT | string | 0x01 --&gt; ABGLEICH_IO 0xFF --&gt; ABGLEICH_NIO |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_..., wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-abgleich-ll-drehzahl-770"></a>
### ABGLEICH_LL_DREHZAHL_770

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-ll-drehzahl-770"></a>
### STATUS_LL_DREHZAHL_770

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_LL_DREHZAHL_770 | string | Abgleich durchgefuehrt = TRUE, Abgleich fehlerhaft = FALSE |
| JOB_STATUS | string |  |

<a id="job-eeprom-byte-aendern"></a>
### EEPROM_BYTE_AENDERN

Beliebige EPROM - Zellen aendern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EEPROM_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |
| EEPROM_AENDERN_BYTE | int | Uebergabeparameter, BYTE zum verundern/verodern |
| EEPROM_AENDERN_OPER | string | Uebergabeparameter, Operator- "AND", "OR", "XOR" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| SCHREIB_STATUS | string | "KORREKT", wenn fehlerfrei |
| EEPROM_LESEN_WERT | int | nichts |
| EEPROM_SCHREIBEN_WERT | int | nichts |

<a id="job-eeprom-byte-abfrage"></a>
### EEPROM_BYTE_ABFRAGE

Beliebige EPROM - Zellen abfragen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EEPROM_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BIT_0_STATUS | string | "BIT_0_SET" oder "BIT_0_RESET" |
| BIT_1_STATUS | string | "BIT_1_SET" oder "BIT_1_RESET" |
| BIT_2_STATUS | string | "BIT_2_SET" oder "BIT_2_RESET" |
| BIT_3_STATUS | string | "BIT_3_SET" oder "BIT_3_RESET" |
| BIT_4_STATUS | string | "BIT_4_SET" oder "BIT_4_RESET" |
| BIT_5_STATUS | string | "BIT_5_SET" oder "BIT_5_RESET" |
| BIT_6_STATUS | string | "BIT_6_SET" oder "BIT_6_RESET" |
| BIT_7_STATUS | string | "BIT_7_SET" oder "BIT_7_RESET" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| EEPROM_LESEN_WERT | int | nichts |

## Tables

### Index

- [BETRIEBSWMATRIX](#table-betriebswmatrix) (24 × 8)
- [BITS](#table-bits) (16 × 4)
- [FORTTEXTE](#table-forttexte) (37 × 4)
- [FARTMATRIX](#table-fartmatrix) (35 × 17)
- [FARTTEXTE](#table-farttexte) (48 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (11 × 5)
- [NULLEINSTEXTE](#table-nulleinstexte) (4 × 3)
- [JOBRESULT](#table-jobresult) (8 × 2)

<a id="table-betriebswmatrix"></a>
### BETRIEBSWMATRIX

Dimensions: 24 rows × 8 columns

| NAME | QUELLE | ZELLE | ORD | TYP | FAKT_A | FAKT_B | EINH |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Nmot | RAM1E | 0x2FB61 | -- | 1 | 22.745 | 0 | 1/min |
| Sp_soll | RAM1E | 0x2FB62 | -- | 1 | 0.0784 | 0 | Grad KW |
| Sp_ist | RAM1E | 0x2FB63 | -- | 1 | 0.0784 | 0 | Grad KW |
| Geschwindigkeit | RAM1E | 0x2FB64 | -- | 1 | 0.9412 | 0 | km/h |
| Menge_ak | RAM1E | 0x2FB65 | -- | 1 | 0.1686 | 0 | mg/Hub |
| PWG_wunsch | RAM1E | 0x2FB5E | -- | 1 | 19.6078 | 0 | mV |
| PWG_wunsch_2 | RAM1E | 0x2FB5E | -- | 1 | 0.0196078 | 0 | V |
| FGR_wunsch | RAM1E | 0x2FB68 | -- | 1 | 0.39216 | 0 | % |
| Lade_druck | RAM1E | 0x2FB69 | -- | 1 | 9.80392 | 125 | hPa |
| Schieberweg_soll | RAM1E | 0x2FB6A | -- | 1 | 19.6078 | 0 | -- |
| Schieberweg_ist | RAM1E | 0x2FB6B | -- | 1 | 19.6078 | 0 | mV |
| Ubatt | RAM1E | 0x2FB76 | -- | 1 | 0.0647 | 0 | Volt |
| Kuehlm_temp | RAM1E | 0x2FB6F | -- | 1 | -0.6863 | 135 | -- |
| Oel_temp | RAM1E | 0x2FB71 | -- | 1 | 0.7647 | -40 | Grad C |
| Kraftst_temp | RAM1E | 0x2FB70 | -- | 1 | 0.4314 | 0 | Grad C |
| LUFTMASSE | RAM1E | 0x2FB67 | -- | 1 | 3.0 | 0 | kg/h |
| Leerlaufabgleich | RAM1E | 0x2FB7C | -- | 1 | 22.745 | -2911 | 1/min |
| Startme_abgleich | RAM1E | 0x2FB7E | -- | 1 | 0.0843 | -10.75 | mg/Hub |
| Volme_abgleich | RAM1E | 0x2FB7D | -- | 1 | 0.7818 | -100 | mg/Hub |
| AGR_abgleich | RAM1E | 0x2FB7F | -- | 1 | 5 | -640 | mg/Hub |
| Fahrver_menge | RAM1E | 0x2FB72 | -- | 1 | 0.2 | 0 | mg/Hub |
| Begrenz_menge | RAM1E | 0x2FB74 | -- | 1 | 0.2 | 0 | mg/Hub |
| Soll_ll_drehz | RAM1E | 0x2FB80 | -- | 1 | 22.745 | 0 | 1/min |
| Atm_druck | RAM1E | 0x2FB77 | -- | 1 | 9.8039 | 125 | hPa |

<a id="table-bits"></a>
### BITS

Dimensions: 16 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| S_PWGL | 0 | 0x40 | 0x40 |
| S_BRL | 0 | 0x80 | 0x80 |
| S_DWA | 1 | 0x02 | 0x02 |
| S_BRT | 1 | 0x20 | 0x20 |
| S_PN | 1 | 0x40 | 0x40 |
| A_KO | 3 | 0x20 | 0x20 |
| S_DIA | 3 | 0x08 | 0x08 |
| S_AC | 3 | 0x40 | 0x40 |
| S_KO | 3 | 0x80 | 0x80 |
| S_T_SCHA | 2 | 0x01 | 0x01 |
| S_T_AUS | 2 | 0x01 | 0x00 |
| S_T_EINP | 2 | 0x02 | 0x02 |
| S_T_EINM | 2 | 0x05 | 0x05 |
| S_T_WA | 2 | 0x08 | 0x08 |
| S_T_BRE | 2 | 0x20 | 0x20 |
| A_T_KUP | 2 | 0x40 | 0x40 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 37 rows × 4 columns

| ORT | ORTTEXT | UW_1 | UW_2 |
| --- | --- | --- | --- |
| 0x00 | -- | 0x00 | 0x00 |
| 0x01 | Mengensteller | 0x01 | 0x02 |
| 0x03 | Elektrisches Abschaltventil (ELAB) | 0x01 | 0x03 |
| 0x05 | Nadelbewegungsfuehler | 0x01 | 0x03 |
| 0x06 | AGR-Regelung | 0x01 | 0x03 |
| 0x08 | Gluehzeitsteuerung | 0x01 | 0x03 |
| 0x0A | Spritzbeginnregelung | 0x01 | 0x05 |
| 0x10 | Batteriespannung | 0x01 | 0x03 |
| 0x15 | SWG | 0x01 | 0x02 |
| 0x1A | Bremsschalter | 0x01 | 0x03 |
| 0x1C | Kupplungsschalter | 0x01 | 0x03 |
| 0x1D | Fahrgeschwindigkeits-Signal | 0x01 | 0x03 |
| 0x20 | Bedienteil Fahrgeschwindigkeitsregelung FGR | 0x01 | 0x03 |
| 0x23 | Kraftstofftemperaturfuehler | 0x06 | 0x03 |
| 0x24 | Oeltemperaturfuehler | 0x01 | 0x04 |
| 0x25 | Pedalwertgeber | 0x01 | 0x03 |
| 0x26 | Heissfilmluftmassenmesser | 0x01 | 0x03 |
| 0x2D | Elektronische Wegfahrsicherung | 0x01 | 0x03 |
| 0x2F | Drehzahlgeber | 0x06 | 0x03 |
| 0x34 | Lufttemperaturfuehler | 0x01 | 0x04 |
| 0x35 | Wassertemperaturfuehler | 0x01 | 0x02 |
| 0x36 | Ladedruckfuehler | 0x01 | 0x05 |
| 0x65 | Laderregelung | 0x01 | 0x04 |
| 0x66 | Rechnerkopplung R1 / R2 | 0x01 | 0x03 |
| 0x67 | Rechnerkopplung R1 / R3 | 0x01 | 0x03 |
| 0x68 | U_ist Abgleichweite R1 defekt | 0x01 | 0x03 |
| 0x69 | U_ist Abgleichweite R2 defekt | 0x01 | 0x03 |
| 0x6A | Endstufenfehler | 0x01 | 0x03 |
| 0x6B | ADF | 0x01 | 0x08 |
| 0x6C | Variantenkodierung R1 | 0x01 | 0x03 |
| 0x6D | Variantenkodierung R2 | 0x01 | 0x03 |
| 0x6E | Luftmasse | 0x01 | 0x05 |
| 0x6F | EG2 Abgleich | 0x01 | 0x05 |
| 0x70 | CAN EGS | 0x01 | 0x07 |
| 0x71 | CAN ASR/MSR | 0x01 | 0x07 |
| 0x72 | CAN-Botschaft INSTR3 | 0x01 | 0x09 |
| 0xXY | unbekannter Fehlerort | 0x00 | 0x00 |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 35 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x03 | 0x00 | 0x00 | 0x00 | 0x16 | 0x00 | 0x00 | 0x00 | 0x17 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x05 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x18 | 0x00 | 0x19 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x06 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x20 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x08 | 0x00 | 0x21 | 0x00 | 0x22 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x0A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x10 | 0x00 | 0x00 | 0x00 | 0x23 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x15 | 0x00 | 0x25 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x26 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x1A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x27 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x1C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x28 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x1D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x29 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x20 | 0x00 | 0x30 | 0x00 | 0x31 | 0x00 | 0x00 | 0x00 | 0x32 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x23 | 0x00 | 0x24 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x24 | 0x00 | 0x24 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x25 | 0x00 | 0x24 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x33 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x26 | 0x00 | 0x24 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x34 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x2D | 0x00 | 0x36 | 0x00 | 0x37 | 0x00 | 0x38 | 0x00 | 0x39 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x2F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x40 | 0x00 | 0x41 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x34 | 0x00 | 0x24 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x35 | 0x00 | 0x24 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x36 | 0x00 | 0x24 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x42 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x65 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x66 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x43 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x67 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x43 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x68 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x44 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x69 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x44 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x6A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x45 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x6B | 0x00 | 0x24 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x6C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x46 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x6D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x46 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x6E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x47 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x6F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x48 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x70 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x71 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x05 | 0x00 | 0x06 | 0x08 | 0x07 | 0x00 | 0x09 |
| 0x72 | 0x00 | 0x00 | 0x00 | 0x49 | 0x00 | 0x50 | 0x00 | 0x51 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 48 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | obere Grenze ueberschritten |
| 0x02 | untere Grenze unterschritten |
| 0x03 | Leitungsunterbrechung |
| 0x04 | Zustand nicht plausibel |
| 0x05 | abgasrelevant |
| 0x06 | fertig entprellt |
| 0x07 | Fehler momentan vorhanden |
| 0x08 | Fehler momentan nicht vorhanden |
| 0x09 | sporadischer Fehler |
| 0x15 | Regelkreis nicht plausibel |
| 0x16 | Endstufe defekt (Kurzschluss) |
| 0x17 | Fehler bei ELAB - Test im Start |
| 0x18 | Leitungsabfall |
| 0x19 | Drehzahl aus NBF nicht plausibel |
| 0x20 | Regelkreis nicht plausibel |
| 0x21 | Fehler bei Ansteuerung mit High |
| 0x22 | Fehler bei Ansteuerung mit Low |
| 0x23 | Unterspannung |
| 0x24 | obere Grenze ueberschritten |
| 0x25 | untere Grenze unterschritten |
| 0x26 | nicht plausibel mit Nadelbewegungsfuehler |
| 0x27 | Bremse und red. Bremse nicht plausibel |
| 0x28 | Signal nicht plausibel |
| 0x29 | zu viele Impulse oder nicht plausibel |
| 0x30 | analoges Bedienteil: obere Grenze ueberschritten |
| 0x31 | analoges Bedienteil: untere Grenze unterschritten |
| 0x32 | MFL: Togglebit aendert sich nicht (Leitungsabfall) |
| 0x33 | nicht plausibel zu Leergasschalter |
| 0x34 | Luftmasse zu klein |
| 0x35 | Steuergeraet im Auslieferungszustand |
| 0x36 | EWS-Mode 2 falscher Code angekommen |
| 0x37 | EWS-Mode 2 kein Code angekommen |
| 0x38 | EWS-Mode 2 EWS-Codes sporadisch gestoert |
| 0x39 | EWS Mode 1 falscher Pegel eingelesen |
| 0x40 | keine Drehzahl Impulse (Leitungsabfall) |
| 0x41 | Drehzahlimpulse nicht plausibel |
| 0x42 | nicht plausibel mit ADF |
| 0x43 | serielle Schnittstelle defekt |
| 0x44 | Abgleichwerte nicht plausibel (Checksumme) |
| 0x45 | Kurzschluss einer oder mehrer Endstufen |
| 0x46 | Fehler in der Variantencodierung |
| 0x47 | Mengenreduktion aufgrund zu hoher Luftmasse |
| 0x48 | EG2 Abgleich Checksummenfehler |
| 0x49 | CAN Dual Ported RAM defekt (SG-intern) |
| 0x50 | keine Botschaft empfangen, CAN Fehler |
| 0x51 | CAN Baustein ausgefallen |
| 0xFF | unbekannte Fehlerart |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 11 rows × 5 columns

| UWNR | UWTEXT | UW_EINH | UWF_A | UWF_B |
| --- | --- | --- | --- | --- |
| 0x00 | -- | -- | 1 | 0 |
| 0x01 | Motordrehzahl | 1/min | 22.745 | 0 |
| 0x02 | Kraftstofftemperatur | Grad C | 0.4314 | 0 |
| 0x03 | Kuehlmitteltemperatur | Grad C | -0.6863 | 135 |
| 0x04 | Ladedruck | hPa | 9.8039 | 125 |
| 0x05 | Einspritzmenge | mg/Hub | 0.2 | 0 |
| 0x06 | Motordrehzahl NBF | 1/min | 22.745 | 0 |
| 0x07 | Geschwindigkeit | km/h | 0.9412 | 0 |
| 0x08 | Ansauglufttemperatur | Grad C | -0.6863 | 135 |
| 0x09 | Batteriespannung | V |  |  |
| 0xXY | unbekannte Umweltbedingung | -- | 1 | 0 |

<a id="table-nulleinstexte"></a>
### NULLEINSTEXTE

Dimensions: 4 rows × 3 columns

| SELECTOR | 0 | 1 |
| --- | --- | --- |
| AE | AUS | EIN |
| OZ | OFFEN | ZU |
| AA | AUS | AKTIV |
| XY | kein Text gefunden | kein Text gefunden |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |
