# IHKAR50R.prg

- Jobs: [31](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | IHKA R50 RD |
| ORIGIN | BMW EI-63 Schusser |
| REVISION | 1.03 |
| AUTHOR | BHTC T-E23 Dietmar Nolte |
| COMMENT | N/A |
| PACKAGE | 1.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [IDENT](#job-ident) - Identdaten
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen Clears all faults
- [SPEICHER_LESEN](#job-speicher-lesen) - Speicher lesen mit Adresse Read ECU memory by address
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des SG Speichers mit Adresse Write memory to a specified address
- [STATUS_SG](#job-status-sg) - Steuergeraet Mode, LED und LCD auslesen
- [STATUS_SG_MODE](#job-status-sg-mode) - Steuergeraet, Einstellung auslesen
- [STATUS_SG_LED_LCD](#job-status-sg-led-lcd) - Steuergeraet, Status LED und LCD auslesen
- [STATUS_SG_TASTER](#job-status-sg-taster) - Steuergeraet, Status Taster auslesen
- [STATUS_SYSTEMPARAMETER](#job-status-systemparameter) - Systemparameter auslesen
- [STEUERN_MOTOREN](#job-steuern-motoren) - Steuern der Motoren Blocknummer 0 Force the blend actuators IO block 0
- [STEUERN_LED_LCD](#job-steuern-led-lcd) - Steuern des Bedienteil LCD
- [STEUERN_LED](#job-steuern-led) - Steuer der Bedienteil LED
- [STEUERN_LCD](#job-steuern-lcd) - Steuern des Bedienteil LCD
- [STEUERN_KOMP_UMLUFT](#job-steuern-komp-umluft) - Steuern von Kompressor und Umluft
- [STEUERN_EICHLAUF](#job-steuern-eichlauf) - Motoren kalibrieren
- [STEUERN_SG_RESET](#job-steuern-sg-reset) - SG Reset Reset ECU
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. Only the last 3 bytes can be written
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten
- [CODIERUNG_SCHREIBEN](#job-codierung-schreiben) - Codierdaten Schreiben fuer R50 IHKA/ATC RD Es muessen immer alle vier Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten Ping message
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [CALIBRATE_MOTORS](#job-calibrate-motors) - Send manual calibration of blend and distribution motors message Job ist wegen Kompatibilitaet zur SGBD IHKAR50 integriert! Job soll nur im Werk Oxford verwendet werden! Fuer neue Anwendungen bitte den Job STEUERN_EICHLAUF verwenden!
- [STATUS_SYSTEM_PARAMETER](#job-status-system-parameter) - Read the system parameters Job ist wegen Kompatibilitaet zur SGBD IHKAR50 integriert! Job soll nur im Werk Oxford verwendet werden! Fuer neue Anwendungen bitte den Job STATUS_SYSTEMPARAMETER verwenden!
- [STATUS_IO_DIGITAL](#job-status-io-digital) - Read IO States for block 0 - Push Buttons, LEDs and Set Points Job ist wegen Kompatibilitaet zur SGBD IHKAR50 integriert! Job soll nur im Werk Oxford verwendet werden! Fuer neue Anwendungen bitte die Jobs STATUS_SG_xx verwenden!
- [STEUERN_ACTUATORS](#job-steuern-actuators) - Force the blend actuators IO block 0 Job ist wegen Kompatibilitaet zur SGBD IHKAR50 integriert! Job soll nur im Werk Oxford verwendet werden! Fuer neue Anwendungen bitte den Job STEUERN_MOTOREN verwenden!
- [STEUERN_AIRCON_RECIRC](#job-steuern-aircon-recirc) - Force Air conditioning and recirculation IO block 2 Job ist wegen Kompatibilitaet zur SGBD IHKAR50 integriert! Job soll nur im Werk Oxford verwendet werden! Fuer neue Anwendungen bitte den Job STEUERN_KOMP_UMLUFT verwenden!

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

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode Raw fault data from the ECU |
| F_ORT_NR | int | Index fuer Fehlerort Fault number |
| F_ORT_TEXT | string | Fehlerort als Text Fault description |
| F_HFK | int | Fehlerhaeufigkeit Error frequency counter |
| F_ART_ANZ | int | Anzahl der Fehlerarten = 6 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen = 0 |
| F_ART1_NR | int | 1 oder 0 |
| F_ART1_TEXT | string | 'Kurzschluss gegen U-Batt' oder '--' |
| F_ART2_NR | int | 2 oder 0 |
| F_ART2_TEXT | string | 'Kurzschluss gegen Masse' oder '--' |
| F_ART3_NR | int | 4 oder 0 |
| F_ART3_TEXT | string | 'Leitungsunterbrechung' oder '--' |
| F_ART4_NR | int | 8 oder 0 |
| F_ART4_TEXT | string | 'unplausibler Wert, ungueltiger Arbeitsbereich' oder '--' |
| F_ART5_NR | int | 64 oder 0 |
| F_ART5_TEXT | string | 'Fehler momentan vorhanden' oder '--' |
| F_ART6_NR | int | 128 oder 0 |
| F_ART6_TEXT | string | 'sporadischer Fehler' oder '--' |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen Clears all faults

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | HEX-Antwort vom SG ECU responce packet |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Speicher lesen mit Adresse Read ECU memory by address

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | unsigned long | Adresse im RAM 0x0000 - 0xFFFF |
| ANZAHL | int | Anzahl speicher lesen Length of memory to read 1 - 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten ECU data wich is read |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | HEX-Antwort vom SG ECU responce packet |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Beschreiben des SG Speichers mit Adresse Write memory to a specified address

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | int | Speichersegment EEPROM = 3 RAM = 4 |
| ADRESSE | unsigned long | Adresse im RAM 0x0000 - 0xFFFF |
| ANZAHL | int | Anzahl speicher schreiben Length of memory to write 1 - 27 |
| DATEN | string | zu schreibende Daten Data bytes to write z.B. 1,2,03,0x04,0x05... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | HEX-Antwort vom SG ECU responce packet |

<a id="job-status-sg"></a>
### STATUS_SG

Steuergeraet Mode, LED und LCD auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TEMP_SOLL_WERT | real | Temperatursollwert |
| STAT_TEMP_SOLL_EINH | string | Einheit fuer Temperatursollwert |
| STAT_MAN_GEBL_STUFE | int | Manuelle Geblaesestufe 1 bis 8 |
| STAT_MODE | int | Bedienteilmode auslesen Bit 15: Temperatureinheit Bit 14 .. 10: nicht verwendet Bit 9: Geblaeseautomatik Bit 8: Heizbare Heckscheibe |
| STAT_LED | int | Funktionsbeleuchtung auslesen Bit 7: Luftverteilung Oben Bit 6: Luftverteilung Mitte Bit 5: Luftverteilung Unten Bit 4: HHS Bit 3: Umluft Bit 2: Kompressor Bit 1: AUTO Bit 0: Defrost |
| STAT_TASTER | int | Drucktaster gedrueckt Bit 15: Kompressor Bit 14: HHS Bit 13: TEMP+ Bit 12: TEMP- Bit 11 .. 8: nicht verwendet Bit 7: Luftverteilung Unten Bit 6: Defrost Bit 5: Geblaese Minus Bit 4: Luftverteilung Mitte Bit 3: Geblaese Plus Bit 2: Auto Bit 1: Umluft Bit 0: Luftverteilung Oben |
| STAT_LCD_PWM_WERT | int | Einschaltdauer fuer LCD PWM |
| STAT_LCD_PWM_EINH | string | Einheit fuer LCD PWM |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-status-sg-mode"></a>
### STATUS_SG_MODE

Steuergeraet, Einstellung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TEMP_SOLL_WERT | real | Temperatursollwert |
| STAT_TEMP_SOLL_EINH | string | Einheit fuer Temperatursollwert |
| STAT_FAHRENH_AKTIV | int | Einheit fuer Anzeige Temperatursollwert im Display 1=aktiv, 0=nicht aktiv |
| STAT_OFF_AKTIV | int | OFF-Mode 1=aktiv, 0=nicht aktiv |
| STAT_DEFROST_AKTIV | int | Defrost-Mode 1=aktiv, 0=nicht aktiv |
| STAT_GEBL_AUTO_AKTIV | int | Geblaeseautomatik 1=aktiv, 0=nicht aktiv |
| STAT_MAN_GEBL_STUFE | int | Manuelle Geblaesestufe 1 bis 8 |
| STAT_LV_AUTO_AKTIV | int | Luftverteilungsautomatik 1=aktiv, 0=nicht aktiv |
| STAT_LV_OBEN_AKTIV | int | manuelle Luftverteilung Oben 1=aktiv, 0=nicht aktiv |
| STAT_LV_MITTE_AKTIV | int | manuelle Luftverteilung Mitte 1=aktiv, 0=nicht aktiv |
| STAT_LV_UNTEN_AKTIV | int | manuelle Luftverteilung Unten 1=aktiv, 0=nicht aktiv |
| STAT_KOMPR_AUS_AKTIV | int | Kompressor 1=aktiv, 0=nicht aktiv |
| STAT_UMLUFT_AKTIV | int | 1=aktiv, 0=nicht aktiv |
| STAT_HHS_AKTIV | int | 1=aktiv, 0=nicht aktiv |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-status-sg-led-lcd"></a>
### STATUS_SG_LED_LCD

Steuergeraet, Status LED und LCD auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LED_AUT_AKTIV | int | LED AUTO-Mode 1=aktiv, 0=nicht aktiv |
| STAT_LED_DEF_AKTIV | int | LED Defrost-Mode 1=aktiv, 0=nicht aktiv |
| STAT_LED_KOM_AKTIV | int | LED Kompressor 1=aktiv, 0=nicht aktiv |
| STAT_LED_UML_AKTIV | int | LED Umluft 1=aktiv, 0=nicht aktiv |
| STAT_LED_HHS_AKTIV | int | LED heizbare Heckscheibe 1=aktiv, 0=nicht aktiv |
| STAT_LED_LVO_AKTIV | int | LED manuelle Luftverteilung Oben 1=aktiv, 0=nicht aktiv |
| STAT_LED_LVM_AKTIV | int | LED manuelle Luftverteilung Mitte 1=aktiv, 0=nicht aktiv |
| STAT_LED_LVU_AKTIV | int | LED manuelle Luftverteilung Unten 1=aktiv, 0=nicht aktiv |
| STAT_LCD_PWM_WERT | int | Einschaltdauer fuer LCD PWM |
| STAT_LCD_PWM_EINH | string | Einheit fuer LCD PWM |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-status-sg-taster"></a>
### STATUS_SG_TASTER

Steuergeraet, Status Taster auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WTAST_AUT_AKTIV | int | Wipp-Taster Auto-Mode 1=gedrueckt, 0=nicht gedrueckt |
| STAT_WTAST_DEF_AKTIV | int | Wipp-Taster Defrost 1=gedrueckt, 0=nicht gedrueckt |
| STAT_DTAST_KOM_AKTIV | int | Drucktaster Kompressor 1=gedrueckt, 0=nicht gedrueckt |
| STAT_DTAST_UML_AKTIV | int | Drucktaster Umluft 1=gedrueckt, 0=nicht gedrueckt |
| STAT_DTAST_HHS_AKTIV | int | Drucktaster heizbare Heckscheibe 1=gedrueckt, 0=nicht gedrueckt |
| STAT_DRING_T_M_AKTIV | int | Drehring Temperatur minus 1=gedreht, 0=nicht gedreht |
| STAT_DRING_T_P_AKTIV | int | Drehring Temperatur plus 1=gedreht, 0=nicht gedreht |
| STAT_WTAST_G_M_AKTIV | int | Wipp-Taster Geblaese minus 1=gedrueckt, 0=nicht gedrueckt |
| STAT_WTAST_G_P_AKTIV | int | Wipp-Taster Geblaese plus 1=gedrueckt, 0=nicht gedrueckt |
| STAT_DTAST_LVO_AKTIV | int | Drucktaster Luftverteilung oben 1=gedrueckt, 0=nicht gedrueckt |
| STAT_DTAST_LVM_AKTIV | int | Drucktaster Luftverteilung mitte 1=gedrueckt, 0=nicht gedrueckt |
| STAT_DTAST_LVU_AKTIV | int | Drucktaster Luftverteilung unten 1=gedrueckt, 0=nicht gedrueckt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-status-systemparameter"></a>
### STATUS_SYSTEMPARAMETER

Systemparameter auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SOLARSEN_WERT | real | Sonnenbelastung, Solarsensor, AD_05 |
| STAT_SOLARSEN_EINH | string | Einheit fuer Sonnenbelastung |
| STAT_TEMP_INNEN_WERT | real | Innenraumtemperatur, AD_08 |
| STAT_TEMP_WT_WERT | real | Waermetauschertemperatur, AD_01 |
| STAT_TEMP_EINH | string | Einheit fuer Temperatur |
| STAT_RM_TKLAPPE_WERT | int | Rueckmeldung der Motors fuer die Temperatur-Mischklappe, AD_02 |
| STAT_RM_LV_WERT | int | Rueckmeldung des Motors fuer die Luftverteilungs, AD_07 |
| STAT_RM_EINH | string | Einheit fuer die Rueckmeldung |
| STAT_SPG_GEBL_WERT | real | Geblaesespannung, AD_06 |
| STAT_SPG_KLR_WERT | real | Spannung Klemme R, AD_04 |
| STAT_SPG_EINH | string | Einheit fuer Spannung |
| STAT_FREQ_BEMO_WERT | int | Frequenz des Belueftungsmotors fuer den Innentemperatursensor |
| STAT_FREQ_BEMO_EINH | string | Einheit fuer Frequenz |
| STAT_KF_MOTOREN_WERT | string | Kalibrierungsflag fuer die Motoren Luftverteilung und Temperatur-Mischklappe |
| STAT_KF_EINH | string |  |
| STAT_SW_VERSION | string | Software version |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-steuern-motoren"></a>
### STEUERN_MOTOREN

Steuern der Motoren Blocknummer 0 Force the blend actuators IO block 0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_TM_MOTOR_AKTIV | int | Steuern des Temperatur-Mischklappen-Motors vorgeben 0 = nicht vorgeben, 1 = vorgeben Force Blend (1 = force, 0 = not force) |
| STEUERN_TM_MOTOR | int | Vorgabe fuer Temperatur-Mischklappen-Motor Blend percentage 0% - 100% |
| STEUERN_LV_MOTOR_AKTIV | int | Steuer des Luftverteilungs-Klappen-Motors vorgeben 0 = nicht vorgeben, 1 = vorgeben Force Distrib (1 = force, 0 = not force) |
| STEUERN_LV_MOTOR | int | Vorgabe fuer Luftverteilungs-Klappen-Motor Distribution percentage 0% - 100% |
| STEUERN_GEBLAESE_AKTIV | int | Steuern des Geblaeses vorgeben 0 = nicht vorgeben, 1 = vorgeben Force Blower (1 = force, 0 = not force) |
| STEUERN_GEBLAESE | int | Vorgabe fuer Geblase Blower level 0% -  100% |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-led-lcd"></a>
### STEUERN_LED_LCD

Steuern des Bedienteil LCD

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_LED_AKTIV | int | Steuern der LEDs vorgeben 0 = nicht vorgeben, 1 = vorgeben |
| STEUERN_LED | int | Funktions-LEDs 0 = aus, 1 = an Bit 0 = Defrost LED Bit 1 = AUTO LED Bit 2 = Kompressor LED Bit 3 = Umluft LED Bit 4 = HHS LED Bit 5 = Luftverteilung Unten Bit 6 = Luftverteilung Mitte Bit 7 = Luftverteilung Oben |
| STEUERN_LCD_AKTIV | int | Steuern des LCDs vorgeben 0 = nicht vorgeben, 1 = vorgeben |
| STEUERN_LCD_ZEHNER | int | 7-Segment Sollwert Zehnerstelle 0 = aus, 1 = an Bit 0 = oben Bit 1 = links oben Bit 2 = links unten Bit 3 = unten Bit 4 = rechts unten Bit 5 = rechts oben Bit 6 = mitte |
| STEUERN_LCD_EINER | int | 7-Segment Sollwert Einerstelle Bit 0 = oben Bit 1 = links oben Bit 2 = links unten Bit 3 = unten Bit 4 = rechts unten Bit 5 = rechts oben Bit 6 = mitte |
| STEUERN_LCD_EINHEIT | int | Segmente der Einheit 0 = aus, 1 = an Bit 0=C1 , 1=C2 , 2=C3 Fahrenheit = C1 und C2 = 3 Celsius = C1 und C3 = 5 |
| STEUERN_LCD_GEBL_BALKEN | int | Geblaesebalken 0 = aus, 1 = an Bit 0..7 = Balken 1 .. 8 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-led"></a>
### STEUERN_LED

Steuer der Bedienteil LED

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_LED_AKTIV | int | Steuern der LEDs vorgeben 0 = nicht vorgeben, 1 = vorgeben |
| STEUERN_LED_AUT | int | AUTO LED 0 = aus, 1 = an |
| STEUERN_LED_DEF | int | Defrost LED 0 = aus, 1 = an |
| STEUERN_LED_KOM | int | Kompressor LED 0 = aus, 1 = an |
| STEUERN_LED_UML | int | Umluft LED 0 = aus, 1 = an |
| STEUERN_LED_HHS | int | Heizbare Heckscheibe 0 = aus, 1 = an |
| STEUERN_LED_LVO | int | Luftverteilung Oben 0 = aus, 1 = an |
| STEUERN_LED_LVM | int | Luftverteilung Mitte 0 = aus, 1 = an |
| STEUERN_LED_LVU | int | Luftverteilung Unten 0 = aus, 1 = an |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-lcd"></a>
### STEUERN_LCD

Steuern des Bedienteil LCD

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_LCD_AKTIV | int | Steuern des LCDs vorgeben 0 = nicht vorgeben, 1 = vorgeben |
| STEUERN_LCD_ZEHNER | int | 7-Segment Sollwert Zehnerstelle 0 = aus, 1 = an Bit 0 = oben Bit 1 = links oben Bit 2 = links unten Bit 3 = unten Bit 4 = rechts unten Bit 5 = rechts oben Bit 6 = mitte |
| STEUERN_LCD_EINER | int | 7-Segment Sollwert Einerstelle Bit 0 = oben Bit 1 = links oben Bit 2 = links unten Bit 3 = unten Bit 4 = rechts unten Bit 5 = rechts oben Bit 6 = mitte |
| STEUERN_LCD_EINHEIT | int | Segmente der Einheit 0 = aus, 1 = an Bit 0=C1 , 1=C2 , 2=C3 Fahrenheit = C1 und C2 = 3 Celsius = C1 und C3 = 5 |
| STEUERN_LCD_GEBL_BALKEN | int | Geblaesebalken 0 = aus, 1 = an Bit 0..7 = Balken 1 .. 8 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-komp-umluft"></a>
### STEUERN_KOMP_UMLUFT

Steuern von Kompressor und Umluft

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_KOMP_AKTIV | int | Steuern des Kompressors vorgeben 0 = nicht vorgeben, 1 = vorgeben |
| STEUERN_KOMP | int | Vorgeben des Kompressors 0 = aus, 1 = an |
| STEUERN_UMLUFT_AKTIV | int | Steuern des Umluft/Frischluft Motors vorgeben 0 = nicht vorgeben, 1 = vorgeben |
| STEUERN_UMLUFT | int | Vorgeben des Umluft/Frischluft Motors 0 = aus, 1 = an |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-eichlauf"></a>
### STEUERN_EICHLAUF

Motoren kalibrieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-sg-reset"></a>
### STEUERN_SG_RESET

SG Reset Reset ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. Only the last 3 bytes can be written

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write teststamp telegram to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG Read new teststamp response |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODE | string | 4 Codierbytes in Hex |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-codierung-schreiben"></a>
### CODIERUNG_SCHREIBEN

Codierdaten Schreiben fuer R50 IHKA/ATC RD Es muessen immer alle vier Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODE1 | int | 0-255 bzw. 0x00-0xFF Bit 0  1 = EEP-Kennlinine Bit 1  1 = Standardanzeiger Grad F Bit 2  1 = Klima Ein bei Auto Ein Bit 3  1 = Zuschaltung HHS/HFS bei Defrost Bit 4  1 = Verbau HFS Bit 5  1 = reduzierbare Geblaesestufe bei Defrost Bit 6  1 = Freigeben der internen BHTC-Diagnose Bit 7  1 = manuelle LV Oben und Mitte verriegeln |
| CODE2 | int | 0-255 bzw. 0x00-0xFF Bit 0  1 = neuer Sonnensensor Bit 1  1 = Sperren der Kompressortaste Bit 2  1 = max Heizen bei Defrost mit T(aussen) ueber 0 Grad C Bit 3  1 = Auto-Umluft Bit 4  1 = Frischluft-Anteil Bit 5  1 = noch nicht verwendet Bit 6  1 = WT Fuehler intern 7K5 Pull-Up Widerstand Bit 7  1 = WT Fuehler extern 1K2 Serienwiderstand |
| CODE3 | int | 0-255 bzw. 0x00-0xFF Bit 0  1 = Diagnosetestmode für 240s (anstatt 10s) Bit 1  1 = zyklische Klemmenanforderung bei Kl.R abschalten Bit 2  1 = kein Telegramm 8Bh bei Kl. 15 aus Bit 3  1 = noch nicht verwendet Bit 4  1 = noch nicht verwendet Bit 5  1 = noch nicht verwendet Bit 6  1 = noch nicht verwendet Bit 7  1 = noch nicht verwendet |
| CODE4 | int | 0-255 bzw. 0x00-0xFF Bit 0  1 = noch nicht verwendet Bit 1  1 = noch nicht verwendet Bit 2  1 = noch nicht verwendet Bit 3  1 = noch nicht verwendet Bit 4  1 = noch nicht verwendet Bit 5  1 = noch nicht verwendet Bit 6  1 = noch nicht verwendet Bit 7  1 = noch nicht verwendet |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode des SG aufrecht erhalten Ping message

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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

<a id="job-calibrate-motors"></a>
### CALIBRATE_MOTORS

Send manual calibration of blend and distribution motors message Job ist wegen Kompatibilitaet zur SGBD IHKAR50 integriert! Job soll nur im Werk Oxford verwendet werden! Fuer neue Anwendungen bitte den Job STEUERN_EICHLAUF verwenden!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-system-parameter"></a>
### STATUS_SYSTEM_PARAMETER

Read the system parameters Job ist wegen Kompatibilitaet zur SGBD IHKAR50 integriert! Job soll nur im Werk Oxford verwendet werden! Fuer neue Anwendungen bitte den Job STATUS_SYSTEMPARAMETER verwenden!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_SUN_LOAD_WERT | real | Sun load |
| STAT_SUN_LOAD_EINH | string |  |
| STAT_CABIN_TEMP_WERT | real | Cabin temperature |
| STAT_CABIN_TEMP_EINH | string |  |
| STAT_HEATER_AIR_OFF_TEMP_WERT | real | Heater air off temperature |
| STAT_HEATER_AIR_OFF_TEMP_EINH | string |  |
| STAT_BLENDDOOR_CURRENT_FDBK_WERT | real | Blend door feedback |
| STAT_BLENDDOOR_CURRENT_FDBK_EINH | string |  |
| STAT_DISTRIB_CURRENT_FDBK_WERT | real | Distribution feedback |
| STAT_DISTRIB_CURRENT_FDBK_EINH | string |  |
| STAT_BLOWER_VOLTAGE_WERT | real | Blower voltage |
| STAT_BLOWER_VOLTAGE_EINH | string |  |
| STAT_BATTERY_VOLTAGE_WERT | real | Battery Voltage |
| STAT_BATTERY_VOLTAGE_EINH | string |  |
| STAT_ASPIRATOR_DIAG_FREQ_WERT | real | Aspirator Distribution feedback |
| STAT_ASPIRATOR_DIAG_FREQ_EINH | string |  |
| STAT_CALIBRATION_DISTRI_MOTOR_WERT | string | Calibration Done = AA |
| STAT_CALIBRATION_BLEND_MOTOR_WERT | string | Calibration Done = AA |
| STAT_SOFTWARE_VERSION_WERT | string | Software version |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-digital"></a>
### STATUS_IO_DIGITAL

Read IO States for block 0 - Push Buttons, LEDs and Set Points Job ist wegen Kompatibilitaet zur SGBD IHKAR50 integriert! Job soll nur im Werk Oxford verwendet werden! Fuer neue Anwendungen bitte die Jobs STATUS_SG_xx verwenden!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DISTRIB_SCREEN_ACTIVE | int | Distribution to screen 1=activ, 0=nicht |
| STAT_DISTRIB_FEET_ACTIVE | int | Distribution to feet 1=activ, 0=nicht |
| STAT_DISTRIB_FACE_ACTIVE | int | Distribution to face 1=activ, 0=nicht |
| STAT_BLOWER_AUTO_ACTIVE | int | Automatic Blower 1=activ, 0=nicht |
| STAT_RECIRC_ACTIVE | int | Recirculation mode 1=activ, 0=nicht |
| STAT_AC_ACTIVE | int | AirCon mode 1=activ, 0=nicht |
| STAT_DISTRIB_AUTO_ACTIVE | int | Automatic Distribution 1=activ, 0=nicht |
| STAT_DISTRIB_FACE_LED_ON | int | Touch LED for face distributiuon on 1 wenn ein / 0 wenn aus |
| STAT_DISTRIB_SCREEN_LED_ON | int | Touch LED for screen distributiuon on 1 wenn ein / 0 wenn aus |
| STAT_DISTRIB_FEET_LED_ON | int | Touch LED for feet distributiuon on 1 wenn ein / 0 wenn aus |
| STAT_AUTO_LED_ON | int | Touch LED Auto on 1 wenn ein / 0 wenn aus |
| STAT_AC_LED_ON | int | Touch LED for AirCon on 1 wenn ein / 0 wenn aus |
| STAT_RECIRC_LED_ON | int | Touch LED for recirculation on 1 wenn ein / 0 wenn aus |
| STAT_HRW_HFS_LED_ON | int | LED for heated rear window and heated fromt screen on 1 wenn ein / 0 wenn aus |
| STAT_TEMP_UNIT_FARENHEIT | int | Temperature unit 1 wenn Farenheit / 0 wenn Celsius |
| STAT_TEMP_PLUS_BUTTON_PRESSED | int | Temperature+ button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_TEMP_MINUS_BUTTON_PRESSED | int | Temperature- button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_BLOWER_PLUS_BUTTON_PRESSED | int | Blower+ button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_BLOWER_MINUS_BUTTON_PRESSED | int | Blower- button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_FACE_BUTTON_PRESSED | int | Distribution Face button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_SCREEN_BUTTON_PRESSED | int | Distribution Screen button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_FEET_BUTTON_PRESSED | int | Distribution Feet button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_AUTO_BUTTON_PRESSED | int | Automatic button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_AC_BUTTON_PRESSED | int | AirCon button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_RECIRC_BUTTON_PRESSED | int | Recirculation button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_HRW_HFS_BUTTON_PRESSED | int | Heated rear window and heated front screen button pressed 1 wenn einschalten / 0 wenn ausschalten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-actuators"></a>
### STEUERN_ACTUATORS

Force the blend actuators IO block 0 Job ist wegen Kompatibilitaet zur SGBD IHKAR50 integriert! Job soll nur im Werk Oxford verwendet werden! Fuer neue Anwendungen bitte den Job STEUERN_MOTOREN verwenden!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FORCE_BLEND | int | Force Blend (1 = force, 0 = not force) |
| BLEND_PCT | int | Blend percentage 0 - 100% |
| FORCE_DISTRIB | int | Force Distrib (1 = force, 0 = not force) |
| DISTRIB_PCT | int | Distribution percentage 0 - 100% |
| FORCE_BLOWER | int | Force Blower (1 = force, 0 = not force) |
| BLOWER_LEVEL | int | Blower level 0 - 31 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-aircon-recirc"></a>
### STEUERN_AIRCON_RECIRC

Force Air conditioning and recirculation IO block 2 Job ist wegen Kompatibilitaet zur SGBD IHKAR50 integriert! Job soll nur im Werk Oxford verwendet werden! Fuer neue Anwendungen bitte den Job STEUERN_KOMP_UMLUFT verwenden!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FORCE_AIRCON | int | Force Aircon (1 = force, 0 = not force) |
| AIRCON_ON | int | Air conditioning  value (1 = ON, 0 = OFF) |
| FORCE_RECIRC | int | Force Recirc (1 = force, 0 = not force) |
| RECIRC_ON | int | Recirculation value (1 - ON, 0 - OFF) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (72 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [FORTTEXTE](#table-forttexte) (12 × 2)
- [FARTTEXTE](#table-farttexte) (8 × 2)
- [BEDIENTEILBITS](#table-bedienteilbits) (31 × 4)

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

Dimensions: 72 rows × 2 columns

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

Dimensions: 12 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Waermetauscherfuehler |
| 0x01 | RMP Motor Temperaturmischklappe |
| 0x04 | Solarsensor |
| 0x06 | RMP Motor Luftverteilungsklappe |
| 0x07 | Innenraumtemperaturfuehler |
| 0x08 | Versorgungsspannung RMP |
| 0x09 | Geblaesesteuerspannung |
| 0x0A | Innenfuehlergeblaese |
| 0x0B | Motor Luftverteilungsklappe |
| 0x0C | Motor Temperaturmischklappe |
| 0x63 | Energiesparmode aktiv |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 8 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen U-Batt |
| 0x02 | Kurzschluss gegen Masse |
| 0x04 | Leitungsunterbrechung |
| 0x08 | unplausibler Wert, ungueltiger Arbeitsbereich |
| 0x40 | Fehler momentan vorhanden |
| 0x80 | sporadischer Fehler |
| 0xFF | unbekannte Fehlerart |

<a id="table-bedienteilbits"></a>
### BEDIENTEILBITS

Dimensions: 31 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| FAHRENHEIT | 6 | 0x80 | 0x80 |
| GEBL_AUTOMATIK | 6 | 0x02 | 0x02 |
| HHS | 6 | 0x01 | 0x01 |
| OFF | 7 | 0x80 | 0x80 |
| LV_OBEN | 7 | 0x40 | 0x40 |
| LV_AUTOMATIK | 7 | 0x20 | 0x20 |
| KOMPRESSOR_AUS | 7 | 0x10 | 0x10 |
| DEFROST_MODE | 7 | 0x08 | 0x08 |
| UMLUFT | 7 | 0x04 | 0x04 |
| LV_MITTE | 7 | 0x02 | 0x02 |
| LV_UNTEN | 7 | 0x01 | 0x01 |
| LED_LVO | 8 | 0x80 | 0x80 |
| LED_LVM | 8 | 0x40 | 0x40 |
| LED_LVU | 8 | 0x20 | 0x20 |
| LED_HHS | 8 | 0x10 | 0x10 |
| LED_UML | 8 | 0x08 | 0x08 |
| LED_KOM | 8 | 0x04 | 0x04 |
| LED_AUT | 8 | 0x02 | 0x02 |
| LED_DEF | 8 | 0x01 | 0x01 |
| DTASTER_KOM | 9 | 0x80 | 0x80 |
| DTASTER_HHS | 9 | 0x40 | 0x40 |
| DRING_TEMP_P | 9 | 0x20 | 0x20 |
| DRING_TEMP_M | 9 | 0x10 | 0x10 |
| DTASTER_LVU | 10 | 0x80 | 0x80 |
| WTASTER_DEF | 10 | 0x40 | 0x40 |
| WTASTER_GBL_M | 10 | 0x20 | 0x20 |
| DTASTER_LVM | 10 | 0x10 | 0x10 |
| WTASTER_GBL_P | 10 | 0x08 | 0x08 |
| WTASTER_AUT | 10 | 0x04 | 0x04 |
| DTASTER_UML | 10 | 0x02 | 0x02 |
| DTASTER_LVO | 10 | 0x01 | 0x01 |
