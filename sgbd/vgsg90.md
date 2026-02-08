# vgsg90.prg

- Jobs: [86](#jobs)
- Tables: [61](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Verteiler-Getriebe Steuergerät |
| ORIGIN | BMW EA-71 Frank Reuter |
| REVISION | 2.080 |
| AUTHOR | MAGNA STEYR Fahrzeugtechnik HES Mirko Podpecan |
| COMMENT | SGBD für E6x & E9x |
| PACKAGE | 1.49 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [DIAGNOSEPROTOKOLL_LESEN](#job-diagnoseprotokoll-lesen) - Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück
- [DIAGNOSEPROTOKOLL_SETZEN](#job-diagnoseprotokoll-setzen) - Wählt ein Diagnoseprotokoll aus
- [IDENT](#job-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [NORMALER_DATENVERKEHR](#job-normaler-datenverkehr) - Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [CBS_INFO](#job-cbs-info) - Ausgabe der CBS-Version
- [CBS_DATEN_LESEN](#job-cbs-daten-lesen) - CBS Daten auslesen (fuer CBS-Version 4) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (fuer CBS-Version 4) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
- [C_CI_LESEN](#job-c-ci-lesen) - Codierindex lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $9B Vehicle Manufacturer Coding Index oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [C_FG_LESEN](#job-c-fg-lesen) - Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [C_FG_SCHREIBEN](#job-c-fg-schreiben) - Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number Modus  : Default
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Fahrgestellnummer schreiben und ruecklesen Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [C_AEI_LESEN](#job-c-aei-lesen) - Aenderungsindex der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_AEI_SCHREIBEN](#job-c-aei-schreiben) - Aenderungsindex der Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_AEI_AUFTRAG](#job-c-aei-auftrag) - Aenderungsindex der Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_SCHREIBEN](#job-c-c-schreiben) - Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_LESEN](#job-zif-lesen) - Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_BACKUP_LESEN](#job-zif-backup-lesen) - Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [PHYSIKALISCHE_HW_NR_LESEN](#job-physikalische-hw-nr-lesen) - Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [HARDWARE_REFERENZ_LESEN](#job-hardware-referenz-lesen) - Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [DATEN_REFERENZ_LESEN](#job-daten-referenz-lesen) - Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DREF Modus  : Default
- [FLASH_ZEITEN_LESEN](#job-flash-zeiten-lesen) - Auslesen der Flash Loeschzeit, Signaturtestzeit, Authentisierberechnungszeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier $2501 Zeiten Modus  : Default
- [FLASH_BLOCKLAENGE_LESEN](#job-flash-blocklaenge-lesen) - Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default
- [AUTHENTISIERUNG_ZUFALLSZAHL_LESEN](#job-authentisierung-zufallszahl-lesen) - Authentisierung Zufallszahl des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $07 RequestForAuthentication Modus  : Default
- [AUTHENTISIERUNG_START](#job-authentisierung-start) - Authentisierung pruefen KWP2000: $31 StartRoutineByLocalIdentifier $08 ReleaseAuthentication Modus  : Default
- [FLASH_PROGRAMMIER_STATUS_LESEN](#job-flash-programmier-status-lesen) - Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default
- [FLASH_SIGNATUR_PRUEFEN](#job-flash-signatur-pruefen) - Flash Signatur pruefen KWP2000: $31 StartRoutineByLocalIdentifier $09 CheckSignature Modus  : Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [FLASH_LOESCHEN](#job-flash-loeschen) - Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default
- [FLASH_SCHREIBEN_ADRESSE](#job-flash-schreiben-adresse) - Vorbereitung fuer Flash schreiben Standard Flashjob KWP2000: $34 RequestDownload Modus  : Default
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Flash Daten schreiben Standard Flashjob KWP2000: $36 TransferData Modus  : Default
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Flashprogrammierung abschliessen Standard Flashjob KWP2000: $37 RequestTransferExit Modus  : Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [AIF_SCHREIBEN](#job-aif-schreiben) - Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default
- [STATUS_CODIERSTATUS](#job-status-codierstatus) - Codierung KWP2000: $21 ReadDataByLocalIdentifier LID0A Modus  : Default
- [STATUS_V_FZG](#job-status-v-fzg) - Vom VGSG ermittelte Fahrzeuggeschwindigkeit KWP2000: $21 ReadDataByLocalIdentifier LID0B Modus  : Default
- [STATUS_N_MOT](#job-status-n-mot) - Motordrehzahl die auf dem CAN ausgegeben wird KWP2000: $21 ReadDataByLocalIdentifier LID0C Modus  : Default
- [STATUS_KLEMMENSPANNUNG](#job-status-klemmenspannung) - Klemmenspannungen am Verteilergetriebe SG KWP2000: $21 ReadDataByLocalIdentifier LID0D Modus  : Default
- [STATUS_GETRIEBE_INTEGRATOREN](#job-status-getriebe-integratoren) - Getriebe Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID0E Modus  : Default
- [STATUS_LAMELLEN_INTEGRATOREN](#job-status-lamellen-integratoren) - Lamellen Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID0F Modus  : Default
- [STATUS_KUPPLUNG](#job-status-kupplung) - Status- und Fehlerinformation des Verteiler Getriebes KWP2000: $21 ReadDataByLocalIdentifier LID01 Modus  : Default
- [STATUS_CODIERDATEN](#job-status-codierdaten) - Daten der Variantencodierung auslesen KWP2000: $21 ReadDataByLocalIdentifier LID1A Modus  : Default
- [STATUS_LT_GETRIEBE_INTEGRATOREN](#job-status-lt-getriebe-integratoren) - Life Time Getriebe Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID1E Modus  : Default
- [STATUS_LT_LAMELLEN_INTEGRATOREN](#job-status-lt-lamellen-integratoren) - Life Time Lamellen Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID1F Modus  : Default
- [STATUS_AKTUATOR_STROM](#job-status-aktuator-strom) - Verteiler Getriebe Aktuator Strom KWP2000: $21 ReadDataByLocalIdentifier LID02 Modus  : Default
- [STATUS_VG_AKTUATOR_POSITION](#job-status-vg-aktuator-position) - Position bzw. Winkel des Verteiler Getriebe Aktuators KWP2000: $21 ReadDataByLocalIdentifier LID03 Modus  : Default
- [STATUS_VG_AKTUATOR_TEMPERATUR](#job-status-vg-aktuator-temperatur) - Temperatur des Aktuator am Verteiler Getriebe KWP2000: $21 ReadDataByLocalIdentifier LID04 Modus  : Default
- [STATUS_T_BELASTUNG_AKTUATOR](#job-status-t-belastung-aktuator) - Thermische Belastung des Verteiler Getriebe Aktuators KWP2000: $21 ReadDataByLocalIdentifier LID05 Modus  : Default
- [STATUS_VG_OEL_TEMP](#job-status-vg-oel-temp) - Oel Temperatur des Verteiler Getriebes KWP2000: $21 ReadDataByLocalIdentifier LID06 Modus  : Default
- [STATUS_T_BELASTUNG_KUPPLUNG](#job-status-t-belastung-kupplung) - Thermische Belastung der Kupplung KWP2000: $21 ReadDataByLocalIdentifier LID07 Modus  : Default
- [STATUS_MK_SOLL](#job-status-mk-soll) - Sollwert des Sollmoments an der Vorderachse KWP2000: $21 ReadDataByLocalIdentifier LID08 Modus  : Default
- [STATUS_MK_IST](#job-status-mk-ist) - Istwert des Sollmoments an der Vorderachse KWP2000: $21 ReadDataByLocalIdentifier LID09 Modus  : Default
- [STATUS_KLASSIERSPEICHER](#job-status-klassierspeicher) - Wiederstandsklassierung des Getriebe KWP2000: $21 ReadDataByLocalIdentifier LID11 Modus  : Default
- [STATUS_DAUERLAUFDATEN](#job-status-dauerlaufdaten) - Life Time Getriebe Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID1E Life Time Lamellen Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID1F Thermische Belastung des Verteiler Getriebe Aktuators KWP2000: $21 ReadDataByLocalIdentifier LID05 Position bzw. Winkel des Verteiler Getriebe Aktuators KWP2000: $21 ReadDataByLocalIdentifier LID03 Gefilterter Kalibrierwinkel KWP2000: $21 ReadDataByLocalIdentifier LID21 SG Temperatur und Ungefilterter Kalibrierwinkel KWP2000: $21 ReadDataByLocalIdentifier LID12 Temperatur des Aktuators am Verteiler Getriebe KWP2000: $21 ReadDataByLocalIdentifier LID04 Modus  : Default
- [STATUS_SW_STAENDE](#job-status-sw-staende) - Status der SW-Stände und MCU Daten KWP2000: $21 ReadDataByLocalIdentifier LID20 Modus  : Default
- [STATUS_KALIBRIERUNG](#job-status-kalibrierung) - Gefilterter Kalibrierwinkel KWP2000: $21 ReadDataByLocalIdentifier LID21 Modus  : Default
- [STATUS_MSA_START](#job-status-msa-start) - Gefilterter Kalibrierwinkel KWP2000: $21 ReadDataByLocalIdentifier LID22 Modus  : Default
- [STATUS_AKTUELLES_AIF_LESEN](#job-status-aktuelles-aif-lesen) - Auslesen des Anwender Informations Feldes KWP 2000: $1A ReadEcuIdentification LID86 Modus   : Default
- [HARDWARE_NUMMER_LESEN](#job-hardware-nummer-lesen) - ECU Hardware Nummer lesen KWP 2000: $1A ReadEcuIdentification LID91 Modus   : Default
- [STEUERN_KUPP_FUNKTIONSPRUEFUNG](#job-steuern-kupp-funktionspruefung) - KWP2000: $31 StartRoutineByLocalIdentifier $30 Funktionspruefung Kupplung Bedingungen: vFzg &lt; 0,2km/h, Kl15 ein Bedingungen: bei nmot&gt;800 UpM muss MKsoll &lt; 10Nm sein Modus  : Default
- [STEUERN_HO_INTEGRATOREN_LOESCHEN](#job-steuern-ho-integratoren-loeschen) - KWP2000: $31 StartRoutineByLocalIdentifier $31 Funktionspruefung Kupplung Bedingungen: vFzg &lt; 0,2km/h Modus  : Default
- [STEUERN_KALIBRIERUNG_LOESCHEN](#job-steuern-kalibrierung-loeschen) - KWP2000: $31 StartRoutineByLocalIdentifier $32 Funktionspruefung Kupplung Bedingungen: vFzg &lt; 0,2km/h, Kl15 ein, kein Ersatzprg. aktiv Bedingungen: MKsoll &lt; 10Nm Modus  : Default
- [STEUERN_LT_INTEGRATOREN_LOESCHEN](#job-steuern-lt-integratoren-loeschen) - KWP2000: $31 StartRoutineByLocalIdentifier $33 Funktionspruefung Kupplung Bedingungen: vFzg &lt; 0,2km/h Modus  : Default
- [STEUERN_FUNKTIONSPRUEFUNG](#job-steuern-funktionspruefung) - KWP2000: $31 StartRoutineByLocalIdentifier $32 Kalibrierung loeschen KWP2000: $11 ECUReset $01 PowerOn KWP2000: $31 StartRoutineByLocalIdentifier $30 Funktionspruefung Kupplung Bedingungen: vFzg &lt; 0,2km/h, Kl15 ein, kein Ersatzprg. aktiv Bedingungen: bei nmot&gt;800 UpM muss MKsoll &lt; 10Nm sein Modus  : Default
- [VGSG_DIAGNOSE_TESTJOB](#job-vgsg-diagnose-testjob) - Job fuer VGSG Diagnosetest (max. 8 Daten - SID,LID,usw.) KWP 2000: Modus   : Default
- [WRITE_GETRIEBE_INTEGRATOREN](#job-write-getriebe-integratoren) - Getriebe Integratoren ins EEPROM schreiben KWP 2000: $3B WriteDataByLocalIdentifier LID0E Bedingungen: vFzg &lt; 0,2km/h Modus   : Default
- [WRITE_LAMELLEN_INTEGRATOREN](#job-write-lamellen-integratoren) - Lamellen Integratoren ins EEPROM schreiben KWP 2000: $3B WriteDataByLocalIdentifier LID0F Bedingungen: vFzg &lt; 0,2km/h Modus   : Default
- [WRITE_LT_GETRIEBE_INTEGRATOREN](#job-write-lt-getriebe-integratoren) - Lifetime Getriebe Integratoren ins EEPROM schreiben KWP2000: $3B WriteDataByLocalIdentifier LID1E Bedingungen: vFzg &lt; 0,2km/h Modus: Default
- [WRITE_LT_LAMELLEN_INTEGRATOREN](#job-write-lt-lamellen-integratoren) - Lifetime Lamellen Integratoren ins EEPROM schreiben KWP2000: $3B WriteDataByLocalIdentifier LID1F Bedingungen: vFzg &lt; 0,2km/h Modus: Default
- [WRITE_MK_SOLL](#job-write-mk-soll) - Sollmomentvorgabe per Diagnose KWP 2000: $3B WriteDataByLocalIdentifier LID08 Bedingungen: vFzg &lt; 20km/h Modus   : Default
- [STEUERN_KLASSIERSPEICHER_RUECKSETZEN](#job-steuern-klassierspeicher-ruecksetzen) - Widerstandsklasse des Getriebe neu setzen KWP2000: $3B WriteDataByLocalIdentifier LID11 Bedingungen: vFzg &lt; 0,2km/h Modus: Default
- [STEUERN_VERSCHLEISSDATEN_AUSLIEFERZUSTAND](#job-steuern-verschleissdaten-auslieferzustand) - Auslieferzustand bei CBS (HO-Integratoren) und LT-Integratoren erstellen KWP2000: $3B WriteDataByLocalIdentifier LID12 Bedingungen: vFzg &lt; 0,2km/h und nmot&lt;100 UpM Modus: Default

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

<a id="job-diagnoseprotokoll-setzen"></a>
### DIAGNOSEPROTOKOLL_SETZEN

Wählt ein Diagnoseprotokoll aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_PROT | string | Diagnoseprotokoll table KONZEPT_TABELLE KONZEPT_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |

<a id="job-ident"></a>
### IDENT

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardware-Versionsindex |
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
| ID_SG_ADR | long | Steuergeraeteadresse bzw. LIN Master Steuergeraeteadresse |
| ID_LIN_SLAVE_ADR | long | LIN Slave Steuergeraeteadresse |
| ID_EWS_SS | int | Identifikation EWS-Schnittstelle Nur fuer DS2-Bordnetz benoetigt Fuer EWS-DME/DDE Abgleich |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | 0x????: Angabe eines einzelnen Fehlers 0xFFFB: alle Antriebsfehler 0xFFFC: alle Fahrwerkfehler 0xFFFD: alle Karosseriefehler 0xFFFE: alle Netzwerkfehler Default: 0xFFFF: alle Fehler |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-normaler-datenverkehr"></a>
### NORMALER_DATENVERKEHR

Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREIGEBEN | string | "ja"   -&gt; normalen Datenverkehr freigeben "nein" -&gt; normalen Datenverkehr sperren table DigitalArgument TEXT |
| SG_ANTWORT | string | "ja"   -&gt; SG soll antworten "nein" -&gt; SG soll nicht antworten table DigitalArgument TEXT Default:  SG soll antworten |
| FUNKTIONAL | string | "ja"   -&gt; Funktionale Adresse 0xEF wird benutzt nur in Verbindung mit SG_ANTWORT="nein" "nein" -&gt; SG Adresse wird benutzt table DigitalArgument TEXT Default:  SG Adresse wird benutzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ANTWORT | string | "ja"   -&gt; SG soll antworten "nein" -&gt; SG soll nicht antworten table DigitalArgument TEXT Default:  SG soll antworten |
| FUNKTIONAL | string | "ja"   -&gt; Funktionale Adresse 0xEF wird benutzt nur in Verbindung mit SG_ANTWORT="nein" "nein" -&gt; SG Adresse wird benutzt table DigitalArgument TEXT Default:  SG Adresse wird benutzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | real | a) Zeit nach der das Steuergerät einschläft Bereich   : 0.5 bis 20.0 [Sekunden] Auflösung : 0.5 [Sekunden] =&gt; zeitgesteuerter Power-Down (0x0E) wird aktiviert b) Default: (Es wird kein Argument übergeben!) =&gt; normaler Power-Down (0x05) wird aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cbs-info"></a>
### CBS_INFO

Ausgabe der CBS-Version

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ECU_NAME | string | Steuergeraetename |
| CBS_VERSION_TEXT | string | CBS Version im Klartext |
| CBS_VERSION_HEX | string | CBS Version als Wert |

<a id="job-cbs-daten-lesen"></a>
### CBS_DATEN_LESEN

CBS Daten auslesen (fuer CBS-Version 4) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Hex-String |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| ANZ_CBS | int | Anzahl der CBS - Umfaenge im Steuergeraet |
| ID_FN_CBS_MESS_WERT | int | CBS-Kennung als Zahl |
| ID_FN_CBS_MESS_HEX | string | CBS-Kennung als Hex-String |
| ID_FN_CBS_MESS_TEXT | string | table CbsKennung CBS_K CBS_K_TEXT CBS-Kennung im Klartext |
| RMMI_CBS_WERT | int | Restlaufleistung |
| RMMI_CBS_EINH | string | Information zur Restlaufleistung |
| ST_UN_CBS_WERT | int | Einheit Restlaufleistung als Zahl |
| ST_UN_CBS_HEX | string | Einheit Restlaufleistung als Hex-String |
| ST_UN_CBS_TEXT | string | Einheit Restlaufleistung im Klartext |
| COU_RSTG_CBS_MESS_WERT | int | Servicezaehler |
| COU_RSTG_CBS_MESS_EINH | string | Zaehler |
| AVAI_CBS_WERT | int | Verfuegbarkeit in % |
| AVAI_CBS_EINH | string | % |
| AVAI_CBS_WERT_OEL | int | Verfuegbarkeit OEL in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_CSF | int | Verfuegbarkeit CSF in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BATT | int | Verfügbarkeit BATT in %, für Prüfablauf Bandende |
| AVAI_CBS_WERT_VTG | int | Verfügbarkeit VTG in %, für Prüfablauf Bandende |
| AVAI_CBS_WERT_FILT | int | Verfuegbarkeit FILT in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BR_V | int | Verfuegbarkeit BR_V in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BR_H | int | Verfuegbarkeit BR_H in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BRFL | int | Verfuegbarkeit BRFL in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_ZKRZ | int | Verfuegbarkeit ZKRZ in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_SIC | int | Verfuegbarkeit SIC in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_KFL | int | Verfuegbarkeit KFL in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_UEB | int | Verfuegbarkeit UEB in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_DAD | int | Verfuegbarkeit DAD in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_ZKRZ_A | int | Verfuegbarkeit ZKRZ_A in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_H2 | int | Verfuegbarkeit H2 in %, fuer Pruefablauf Bandende |
| ZIEL_MM_WERT | int | Ziel-Monat |
| ZIEL_MM_EINH | string | Monat |
| ZIEL_YY_WERT | int | Ziel-Jahr |
| ZIEL_YY_EINH | string | Jahr |
| FRC_INTM_WAY_CBS_MESS | int | Prognose Wegintervall |
| FRC_INTM_WAY_CBS_EINH | string | Information zur Prognose Wegintervall |
| FRC_INTM_T_CBS_MESS | int | Prognose Zeitintervall |
| MANIP_CBS | int | Manipulationsbyte |
| MANIP_CBS_TEXT | string | Manipulationsbyte im Klartext |
| Res_Byte | int | Reserve Byte (noch unbenutzt) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cbs-reset"></a>
### CBS_RESET

CBS Daten Zuruecksetzen (fuer CBS-Version 4) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CBS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, ZKrz, Sic, Kfl, TUV, AU, Ueb, H2 Werte externe Umfaenge: Oel, Br_v, Br_h, Filt, CSF, Batt, VTG, ZKrz_a, DAD Defaultwert: 0x00 (ungueltig) |
| CBS_VERFUEGBARKEIT | int | gewuenschte Verfuegbarkeit in Prozent: 0-100 Schalter, keine Aenderung: 255 Defaultwert: 100 |
| CBS_ANZAHL_SERVICE | int | Anzahl der durchgefuehrten Services: 0-30 Schalter, Erhoehung der Anzahl um +1: 31 Defaultwert: 31 |
| CBS_ZIEL_MONAT | int | Ziel-Monat (HU/AU) Januar-Dezember: 1-12 Schalter, keine Aenderung: 255 Defaultwert: 255 |
| CBS_ZIEL_JAHR | int | Ziel-Jahr (HU/AU) 2000-2239: 0-239 Schalter, keine Aenderung: 255 Defaultwert: 255 |
| RMM_CBS_WERT | int | Restlaufleistung in km oder % (siehe Argument Einheit) Schalter, keine Aenderung: 8000h Defaultwert: 8000h |
| ST_UN_CBS_RSTG | int | Einheit Restlaufleistung 0hex -&gt; % 1hex -&gt; km*10 Fhex -&gt; d.c. Defaultwert: Fh |
| FRC_INTM_WAY_CBS_MESS | int | Prognose Wegintervall Umrechnung 1-254*1000km Schalter, setzt auf Defaultwert zurueck: 0h Schalter, keine Aenderung: FFh Defaultwert: FFh |
| FRC_INTM_T_CBS_MESS | int | Prognose Zeitintervall 0-254 Monate Schalter, keine Aenderung: FFh Defaultwert: FFh |
| Res_Byte | int | Reserve Byte (noch unbenutzt) Defaultwert: 00h |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Zahl |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

<a id="job-c-ci-lesen"></a>
### C_CI_LESEN

Codierindex lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $9B Vehicle Manufacturer Coding Index oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_COD_INDEX | int | Codier-Index |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-schreiben"></a>
### C_FG_SCHREIBEN

Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Fahrgestellnummer schreiben und ruecklesen Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-c-aei-lesen"></a>
### C_AEI_LESEN

Aenderungsindex der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-schreiben"></a>
### C_AEI_SCHREIBEN

Aenderungsindex der Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-auftrag"></a>
### C_AEI_AUFTRAG

Aenderungsindex der Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-c-schreiben"></a>
### C_C_SCHREIBEN

Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-seriennummer-lesen"></a>
### SERIENNUMMER_LESEN

Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SERIENNUMMER | string | Seriennummer des Steuergeraets |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-zif-lesen"></a>
### ZIF_LESEN

Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_PROGRAMM_REFERENZ | string | PRGREF ProgrammReferenz letzter lauffaehiger Programmstand Format: ZZZPPPxVBBxh 12 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller |
| ZIF_SG_KENNUNG | string | ZZZ |
| ZIF_PROJEKT | string | PPPxV |
| ZIF_PROGRAMM_STAND | string | BBxh |
| ZIF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| ZIF_BMW_HW | string | VMECUH*N vehicleManufacturerECUHardware*Number BMW Hardware Nummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG |

<a id="job-zif-backup-lesen"></a>
### ZIF_BACKUP_LESEN

Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_BACKUP_PROGRAMM_REFERENZ | string | PRGREFB ProgrammReferenzBackup letzter lauffaehiger Programmstand Format: ZZZPPPxVBBxh 12 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller |
| ZIF_BACKUP_SG_KENNUNG | string | ZZZ |
| ZIF_BACKUP_PROJEKT | string | PPPxV |
| ZIF_BACKUP_PROGRAMM_STAND | string | BBxh |
| ZIF_BACKUP_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| ZIF_BACKUP_BMW_HW | string | VMECUH*NB vehicleManufECUHW*NumberBackup BMW Hardware* Nummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-physikalische-hw-nr-lesen"></a>
### PHYSIKALISCHE_HW_NR_LESEN

Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PHYSIKALISCHE_HW_NR | string | Physikalische Hardware-Nummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-hardware-referenz-lesen"></a>
### HARDWARE_REFERENZ_LESEN

Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HARDWARE_REFERENZ | string | Hardware Referenz Format: ZZZPPPx 7 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware |
| HW_REF_SG_KENNUNG | string | ZZZ |
| HW_REF_PROJEKT | string | PPPx |
| HW_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-daten-referenz-lesen"></a>
### DATEN_REFERENZ_LESEN

Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DREF Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATEN_REFERENZ | string | Daten Referenz Format: ZZZPPPxVBBxhdxxxx 17 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller d     : Datenstandersteller xxxx  : frei aber eindeutig belegt |
| DATEN_REF_SG_KENNUNG | string | ZZZ |
| DATEN_REF_PROJEKT | string | PPPxV |
| DATEN_REF_PROGRAMM_STAND | string | BBxh |
| DATEN_REF_DATENSATZ | string | dxxxx |
| DATEN_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-zeiten-lesen"></a>
### FLASH_ZEITEN_LESEN

Auslesen der Flash Loeschzeit, Signaturtestzeit, Authentisierberechnungszeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier $2501 Zeiten Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_LOESCHZEIT | int | Flash Loeschzeit in Sekunden |
| FLASH_SIGNATURTESTZEIT | int | Flash Signaturtestzeit in Sekunden |
| FLASH_RESETZEIT | int | Flash Resetzeit in Sekunden |
| FLASH_AUTHENTISIERZEIT | int | Flash Authentisierberechnungszeit in Sekunden |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-blocklaenge-lesen"></a>
### FLASH_BLOCKLAENGE_LESEN

Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_BLOCKLAENGE_GESAMT | unsigned int | Flash Blocklaenge inclusive SID |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-authentisierung-zufallszahl-lesen"></a>
### AUTHENTISIERUNG_ZUFALLSZAHL_LESEN

Authentisierung Zufallszahl des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $07 RequestForAuthentication Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LEVEL | int |  |
| USER_ID | long | optional |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ZUFALLSZAHL | binary | Zufallszahl |
| AUTHENTISIERUNG | string | Authentisierungsart table Authentisierung AUTHG_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-authentisierung-start"></a>
### AUTHENTISIERUNG_START

Authentisierung pruefen KWP2000: $31 StartRoutineByLocalIdentifier $08 ReleaseAuthentication Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : (unbenutzt) Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : Authentisierungszeit in Sekunden Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : (unbenutzt) Wortadresse (low/highbyte, low/highword) Byte 21,....        : Schluesseldaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-programmier-status-lesen"></a>
### FLASH_PROGRAMMIER_STATUS_LESEN

Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_PROGRAMMIER_STATUS_TEXT | string | table ProgrammierStatus STATUS_TEXT |
| FLASH_PROGRAMMIER_STATUS | int | ProgrammierStatus 0 - 255 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-signatur-pruefen"></a>
### FLASH_SIGNATUR_PRUEFEN

Flash Signatur pruefen KWP2000: $31 StartRoutineByLocalIdentifier $09 CheckSignature Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BEREICH | string | 'Programm' 'Daten' |
| SIGNATURTESTZEIT | int | Zeit in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuergeraete-reset"></a>
### STEUERGERAETE_RESET

Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-loeschen"></a>
### FLASH_LOESCHEN

Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : Loeschzeit in Sekunden (Byteparameter 1) Byte 5,6            : Loeschzeit in Sekunden (WordParameter 1 (low/high)) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LOESCHEN_STATUS | int | Loeschstatus 1 = Speicher geloescht 2 = Speicher nicht geloescht 5 = Signaturpruefung PAF nicht durchgefuehrt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben-adresse"></a>
### FLASH_SCHREIBEN_ADRESSE

Vorbereitung fuer Flash schreiben Standard Flashjob KWP2000: $34 RequestDownload Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge ohne Telegramm-Overhead |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben"></a>
### FLASH_SCHREIBEN

Flash Daten schreiben Standard Flashjob KWP2000: $36 TransferData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : (unbenutzt) Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : (unbenutzt) Wortadresse (low/highbyte, low/highword) Byte 21,....        : Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_SCHREIBEN_ANZAHL | unsigned int | Anzahl FLASH_SCHREIBEN seit letztem FLASH_SCHREIBEN_ADRESSE |
| FLASH_SCHREIBEN_STATUS | int | Programmierstatus 1 = Programmierung in Ordnung 2 = Programmierung nicht in Ordnung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben-ende"></a>
### FLASH_SCHREIBEN_ENDE

Flashprogrammierung abschliessen Standard Flashjob KWP2000: $37 RequestTransferExit Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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

<a id="job-status-codierstatus"></a>
### STATUS_CODIERSTATUS

Codierung KWP2000: $21 ReadDataByLocalIdentifier LID0A Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CODIERUNG_TEXT | string | Status Codierung |
| STAT_CODIERUNG_WERT | int | Status Codierung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-v-fzg"></a>
### STATUS_V_FZG

Vom VGSG ermittelte Fahrzeuggeschwindigkeit KWP2000: $21 ReadDataByLocalIdentifier LID0B Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_V_FZG_WERT | real | Vom VGSG ermittelte Fahrzeuggeschwindigkeit |
| STAT_V_FZG_EINHEIT | string | Fahrzeuggeschwindigkeit Einheit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-n-mot"></a>
### STATUS_N_MOT

Motordrehzahl die auf dem CAN ausgegeben wird KWP2000: $21 ReadDataByLocalIdentifier LID0C Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_N_MOT_WERT | int | Motordrehzahl die auf dem CAN ausgegeben wird |
| STAT_N_MOT_EINHEIT | string | physikalische Einheit der Motordrehzahl |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klemmenspannung"></a>
### STATUS_KLEMMENSPANNUNG

Klemmenspannungen am Verteilergetriebe SG KWP2000: $21 ReadDataByLocalIdentifier LID0D Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KLEMMENSPG_VGSG_WERT | real | Klemmenspannung am Verteilergetriebe - KL30 |
| STAT_KLEMMENSPG_VGSG_EINHEIT | string | physikalische Einheit der Klemmenspannung |
| STAT_KLEMMENSPG_G_VGSG_WERT | real | Klemmenspannung am Verteilergetriebe - KL30g |
| STAT_KLEMMENSPG_G_VGSG_EINHEIT | string | physikalische Einheit der Klemmenspannung |
| STAT_KLEMME_15_WAKEUP_TEXT | string | Klemme 15 Ein oder Aus |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-getriebe-integratoren"></a>
### STATUS_GETRIEBE_INTEGRATOREN

Getriebe Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID0E Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GETRIEBE_1_WERT | real | Getriebe Integrator 1 |
| STAT_GETRIEBE_1_EINHEIT | string | Getriebe Integrator 1 Einheit |
| STAT_GETRIEBE_2_WERT | real | Getriebe Integrator 2 |
| STAT_GETRIEBE_2_EINHEIT | string | Getriebe Integrator 2 Einheit |
| STAT_INTEGRATOR_KM_WERT | real | Kilometerwert Integrator |
| STAT_INTEGRATOR_KM_EINHEIT | string | Kilometerwert Einheit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lamellen-integratoren"></a>
### STATUS_LAMELLEN_INTEGRATOREN

Lamellen Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID0F Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LAMELLE_1_WERT | real | Lamellen Integrator 1 |
| STAT_LAMELLE_1_EINHEIT | string | Lamellen Integrator 1 Einheit |
| STAT_LAMELLE_2_WERT | real | Lamellen Integrator 2 |
| STAT_LAMELLE_2_EINHEIT | string | Lamellen Integrator 2 Einheit |
| STAT_LAMELLE_3_WERT | real | Lamellen Integrator 3 |
| STAT_LAMELLE_3_EINHEIT | string | Lamellen Integrator 3 Einheit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kupplung"></a>
### STATUS_KUPPLUNG

Status- und Fehlerinformation des Verteiler Getriebes KWP2000: $21 ReadDataByLocalIdentifier LID01 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ERR_INFO_TEXT | string | Fehlerinformationen des Verteilergetriebes |
| STAT_ERR_INFO_DXC_WERT | int | Fehlerinformationen des Verteilergetriebes |
| STAT_STATUS_INFO_TEXT | string | Statusinformationen des Verteilergetriebes |
| STAT_STATUS_INFO_DXC_WERT | int | Statusinformationen des Verteilergetriebes |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierdaten"></a>
### STATUS_CODIERDATEN

Daten der Variantencodierung auslesen KWP2000: $21 ReadDataByLocalIdentifier LID1A Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BAUREIHE_TEXT | string | Baureihe |
| STAT_MOTORISIERUNG_TEXT | string | Verbauter Motor |
| STAT_GETRIEBEART_TEXT | string | Verbautes Getriebe |
| STAT_OELVERSCHLEISS_TEXT | string | Oel-Verschleiss FS-Eintrag |
| STAT_CBS_TEXT | string | CBS |
| STAT_TEMP_CALIB_TEXT | string | Temperaturabhaengige Kalibrier-Korrektur-Funktion |
| STAT_MILE_CALIB_TEXT | string | Laufstreckenabhaengige Kalibrier-Korrektur-Funktion |
| STAT_BAUREIHE_WERT | int | Baureihe |
| STAT_MOTORISIERUNG_WERT | int | Verbauter Motor |
| STAT_GETRIEBEART_WERT | int | Verbautes Getriebe |
| STAT_OELVERSCHLEISS_WERT | int | Oel-Verschleiss FS-Eintrag |
| STAT_CBS_WERT | int | CBS |
| STAT_TEMP_CALIB_WERT | int | Temperaturabhaengige Kalibrier-Korrektur-Funktion |
| STAT_MILE_CALIB_WERT | int | Laufstreckenabhaengige Kalibrier-Korrektur-Funktion |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lt-getriebe-integratoren"></a>
### STATUS_LT_GETRIEBE_INTEGRATOREN

Life Time Getriebe Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID1E Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LT_GETRIEBE_1_WERT | real | Lifetime Getriebe Integrator 1 |
| STAT_LT_GETRIEBE_1_EINHEIT | string | Lifetime Getriebe Integrator 1 Einheit |
| STAT_LT_GETRIEBE_2_WERT | real | Lifetime Getriebe Integrator 2 |
| STAT_LT_GETRIEBE_2_EINHEIT | string | Lifetime Getriebe Integrator 2 Einheit |
| STAT_LT_INTEGRATOR_KM_WERT | real | Kilometer Wert für Lifetime Integrator |
| STAT_LT_INTEGRATOR_KM_EINHEIT | string | Kilometer Wert für Lifetime Integrator Einheit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lt-lamellen-integratoren"></a>
### STATUS_LT_LAMELLEN_INTEGRATOREN

Life Time Lamellen Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID1F Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LT_LAMELLE_1_WERT | real | Lifetime Lamellen Integrator 1 |
| STAT_LT_LAMELLE_1_EINHEIT | string | Lifetime Lamellen Integrator 1 Einheit |
| STAT_LT_LAMELLE_2_WERT | real | Lifetime Lamellen Integrator 2 |
| STAT_LT_LAMELLE_2_EINHEIT | string | Lifetime Lamellen Integrator 2 Einheit |
| STAT_LT_LAMELLE_3_WERT | real | Lifetime Lamellen Integrator 3 |
| STAT_LT_LAMELLE_3_EINHEIT | string | Lifetime Lamellen Integrator 3 Einheit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktuator-strom"></a>
### STATUS_AKTUATOR_STROM

Verteiler Getriebe Aktuator Strom KWP2000: $21 ReadDataByLocalIdentifier LID02 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AKTUATOR_STROM_WERT | real | Bit0 - Bit15: Aktuator_Strom |
| STAT_AKTUATOR_STROM_EINHEIT | string | Aktuator Strom Einheit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vg-aktuator-position"></a>
### STATUS_VG_AKTUATOR_POSITION

Position bzw. Winkel des Verteiler Getriebe Aktuators KWP2000: $21 ReadDataByLocalIdentifier LID03 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AKTUATOR_POSITION_WERT | real | Istposition die auf den CAN ausgegeben wird |
| STAT_AKTUATOR_POSITION_EINHEIT | string | Istposition Einheit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vg-aktuator-temperatur"></a>
### STATUS_VG_AKTUATOR_TEMPERATUR

Temperatur des Aktuator am Verteiler Getriebe KWP2000: $21 ReadDataByLocalIdentifier LID04 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AKTUATOR_TEMPERATUR_WERT | int | Stellmotor Temperatur |
| STAT_AKTUATOR_TEMPERATUR_EINHEIT | string | Stellmotor Temperatur Einheit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-t-belastung-aktuator"></a>
### STATUS_T_BELASTUNG_AKTUATOR

Thermische Belastung des Verteiler Getriebe Aktuators KWP2000: $21 ReadDataByLocalIdentifier LID05 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_THERMISCHE_BELASTUNG_AKTUATOR_WERT | int | Thermische Belastung Aktuator |
| STAT_THERMISCHE_BELASTUNG_AKTUATOR_EINHEIT | string | Thermische Belastung Aktuator Einheit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vg-oel-temp"></a>
### STATUS_VG_OEL_TEMP

Oel Temperatur des Verteiler Getriebes KWP2000: $21 ReadDataByLocalIdentifier LID06 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_OEL_TEMP_WERT | int | VG Oel Temperatur |
| STAT_OEL_TEMP_EINHEIT | string | VG Oel Temperatur Einheit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-t-belastung-kupplung"></a>
### STATUS_T_BELASTUNG_KUPPLUNG

Thermische Belastung der Kupplung KWP2000: $21 ReadDataByLocalIdentifier LID07 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_THERMISCHE_BELASTUNG_KUPPLUNG_WERT | int | Belastungsgrad des VG |
| STAT_THERMISCHE_BELASTUNG_KUPPLUNG_EINHEIT | string | Belastungsgrad des VG Einheit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mk-soll"></a>
### STATUS_MK_SOLL

Sollwert des Sollmoments an der Vorderachse KWP2000: $21 ReadDataByLocalIdentifier LID08 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MK_SOLL_WERT | int | Sollmoment, das am CAN anliegt |
| STAT_MK_SOLL_EINHEIT | string | Soll Moment Einheit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mk-ist"></a>
### STATUS_MK_IST

Istwert des Sollmoments an der Vorderachse KWP2000: $21 ReadDataByLocalIdentifier LID09 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MK_IST_WERT | int | Istmoment das auf den CAN ausgegeben wird |
| STAT_MK_IST_EINHEIT | string | Ist Moment Einheit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klassierspeicher"></a>
### STATUS_KLASSIERSPEICHER

Wiederstandsklassierung des Getriebe KWP2000: $21 ReadDataByLocalIdentifier LID11 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RESISTOR_KLASS_AKTUAL_TEXT | string | Aktuell verwendeter Wert |
| STAT_RESISTOR_KLASS_AKTUAL_WERT | int | Aktuell verwendeter Wert |
| STAT_RESISTOR_KLASS_EEPROM_TEXT | string | Im EEPROM abgespeicherter Wert |
| STAT_RESISTOR_KLASS_EEPROM_WERT | int | Im EEPROM abgespeicherter Wert |
| STAT_RESISTOR_KLASS_ADC_TEXT | string | Am SG Eingan eingelesener Wert |
| STAT_RESISTOR_KLASS_ADC_WERT | int | Am SG Eingan eingelesener Wert |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dauerlaufdaten"></a>
### STATUS_DAUERLAUFDATEN

Life Time Getriebe Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID1E Life Time Lamellen Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID1F Thermische Belastung des Verteiler Getriebe Aktuators KWP2000: $21 ReadDataByLocalIdentifier LID05 Position bzw. Winkel des Verteiler Getriebe Aktuators KWP2000: $21 ReadDataByLocalIdentifier LID03 Gefilterter Kalibrierwinkel KWP2000: $21 ReadDataByLocalIdentifier LID21 SG Temperatur und Ungefilterter Kalibrierwinkel KWP2000: $21 ReadDataByLocalIdentifier LID12 Temperatur des Aktuators am Verteiler Getriebe KWP2000: $21 ReadDataByLocalIdentifier LID04 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LT_GETRIEBE_1_WERT | real | Lifetime Getriebe Integrator 1 |
| STAT_LT_GETRIEBE_1_EINHEIT | string | Lifetime Getriebe Integrator 1 Einheit |
| STAT_LT_GETRIEBE_2_WERT | real | Lifetime Getriebe Integrator 2 |
| STAT_LT_GETRIEBE_2_EINHEIT | string | Lifetime Getriebe Integrator 2 Einheit |
| STAT_LT_INTEGRATOR_KM_WERT | real | Kilometer Wert für Lifetime Integrator |
| STAT_LT_INTEGRATOR_KM_EINHEIT | string | Kilometer Wert für Lifetime Integrator Einheit |
| _TEL_AUFTRAG_1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |
| STAT_LT_LAMELLE_1_WERT | real | Lifetime Lamellen Integrator 1 |
| STAT_LT_LAMELLE_1_EINHEIT | string | Lifetime Lamellen Integrator 1 Einheit |
| STAT_LT_LAMELLE_2_WERT | real | Lifetime Lamellen Integrator 2 |
| STAT_LT_LAMELLE_2_EINHEIT | string | Lifetime Lamellen Integrator 2 Einheit |
| STAT_LT_LAMELLE_3_WERT | real | Lifetime Lamellen Integrator 3 |
| STAT_LT_LAMELLE_3_EINHEIT | string | Lifetime Lamellen Integrator 3 Einheit |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| STAT_THERMISCHE_BELASTUNG_AKTUATOR_WERT | int | Thermische Belastung Aktuator |
| STAT_THERMISCHE_BELASTUNG_AKTUATOR_EINHEIT | string | Thermische Belastung Aktuator Einheit |
| _TEL_AUFTRAG_3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG |
| STAT_AKTUATOR_POSITION_WERT | real | Istposition die auf den CAN ausgegeben wird |
| STAT_AKTUATOR_POSITION_EINHEIT | string | Istposition Einheit |
| _TEL_AUFTRAG_4 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_4 | binary | Hex-Antwort von SG |
| STAT_KALIB_INFO_TEXT | string | Status Kalibrierung |
| STAT_KALIB_INFO_WERT | int | Status Kalibrierung |
| STAT_PHISPERREKAL_WERT | real | Aktueller(gefilterter) Kalibrierwinkel |
| STAT_PHISPERREKAL_EINHEIT | string | Aktueller(gefilterter) Kalibrierwinkel Einheit |
| STAT_DELTAPHI_WERT | real | Differenz zum Erst-Kalibrierwinkel deltaPhi = Erst-Kalibrierwinkel - Aktueller-Kalibrierwinkel |
| STAT_DELTAPHI_EINHEIT | string | deltaPhi Einheit |
| _TEL_AUFTRAG_5 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_5 | binary | Hex-Antwort von SG |
| STAT_SGTEMP_WERT | real | Steuergeraete Temperatur |
| STAT_SGTEMP_EINHEIT | string | Steuergeraete Temperatur Einheit |
| STAT_PHISPERREKAL_UF_WERT | real | Ungefilterter Kalibrierwinkel |
| STAT_PHISPERREKAL_UF_EINHEIT | string | Ungefilterter Kalibrierwinkel Einheit |
| _TEL_AUFTRAG_6 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_6 | binary | Hex-Antwort von SG |
| STAT_AKTUATOR_TEMPERATUR_WERT | int | Stellmotor Temperatur |
| STAT_AKTUATOR_TEMPERATUR_EINHEIT | string | Stellmotor Temperatur Einheit |
| _TEL_AUFTRAG_7 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_7 | binary | Hex-Antwort von SG |

<a id="job-status-sw-staende"></a>
### STATUS_SW_STAENDE

Status der SW-Stände und MCU Daten KWP2000: $21 ReadDataByLocalIdentifier LID20 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BOOT_SW | string | Bootloader SW Version |
| STAT_APP_SW | string | Applikations SW Version |
| STAT_PIC_SW | string | PIC SW Version |
| STAT_MCU_PARTID | string | PartID register - Mask Set Number |
| STAT_MCU_SIZE | string | Memory Size register 1 und 0 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kalibrierung"></a>
### STATUS_KALIBRIERUNG

Gefilterter Kalibrierwinkel KWP2000: $21 ReadDataByLocalIdentifier LID21 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KALIB_INFO_TEXT | string | Status Kalibrierung |
| STAT_KALIB_INFO_WERT | int | Status Kalibrierung |
| STAT_PHISPERREKAL_WERT | real | Aktueller-Kalibrierwinkel |
| STAT_PHISPERREKAL_EINHEIT | string | Aktueller-Kalibrierwinkel Einheit |
| STAT_DELTAPHI_WERT | real | Differenz zum Erst-Kalibrierwinkel deltaPhi = Erst-Kalibrierwinkel - Aktueller-Kalibrierwinkel |
| STAT_DELTAPHI_EINHEIT | string | deltaPhi Einheit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-msa-start"></a>
### STATUS_MSA_START

Gefilterter Kalibrierwinkel KWP2000: $21 ReadDataByLocalIdentifier LID22 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ANZAHL_MIT_UNTERSPANNUNGSRESET | unsigned int | Status Anzahl der MSA Starts mit Unterspannungsreset |
| STAT_ANZAHL_MIT_POSITIONSVERLUST | unsigned int | Status Anzahl der MSA Starts mit Positionsverlust |
| STAT_ANZAHL_NACHLAUFKALIBRIERUNGEN | unsigned long | Status Anzahl der Nachlaufkalibrierungen |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktuelles-aif-lesen"></a>
### STATUS_AKTUELLES_AIF_LESEN

Auslesen des Anwender Informations Feldes KWP 2000: $1A ReadEcuIdentification LID86 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AIF_AKTUELL_FG_NR_TEXT | string | Fahrgestellnummer 7-stellig |
| STAT_AIF_AKTUELL_FG_NR_LANG_TEXT | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig |
| STAT_AIF_AKTUELL_DATUM_TEXT | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| STAT_AIF_AKTUELL_ZB_NR_TEXT | string | BMW/Rover Zusammenbaunummer |
| STAT_AIF_AKTUELL_SW_NR_TEXT | string | BMW/Rover Datensatznummer - Softwarenummer |
| STAT_AIF_AKTUELL_BEHOERDEN_NR_TEXT | string | BMW/Rover Behoerdennummer |
| STAT_AIF_AKTUELL_HAENDLER_NR_TEXT | string | Haendlernummer |
| STAT_AIF_AKTUELL_SERIEN_NR_TEXT | string | Tester Seriennummer |
| STAT_AIF_AKTUELL_KM_TEXT | long | km-Stand bei der Programmierung |
| STAT_AIF_AKTUELL_PROG_NR_TEXT | string | Programmstandsnummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hardware-nummer-lesen"></a>
### HARDWARE_NUMMER_LESEN

ECU Hardware Nummer lesen KWP 2000: $1A ReadEcuIdentification LID91 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HARDWARE_NUMMER | string | HW* Nummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kupp-funktionspruefung"></a>
### STEUERN_KUPP_FUNKTIONSPRUEFUNG

KWP2000: $31 StartRoutineByLocalIdentifier $30 Funktionspruefung Kupplung Bedingungen: vFzg &lt; 0,2km/h, Kl15 ein Bedingungen: bei nmot&gt;800 UpM muss MKsoll &lt; 10Nm sein Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ho-integratoren-loeschen"></a>
### STEUERN_HO_INTEGRATOREN_LOESCHEN

KWP2000: $31 StartRoutineByLocalIdentifier $31 Funktionspruefung Kupplung Bedingungen: vFzg &lt; 0,2km/h Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kalibrierung-loeschen"></a>
### STEUERN_KALIBRIERUNG_LOESCHEN

KWP2000: $31 StartRoutineByLocalIdentifier $32 Funktionspruefung Kupplung Bedingungen: vFzg &lt; 0,2km/h, Kl15 ein, kein Ersatzprg. aktiv Bedingungen: MKsoll &lt; 10Nm Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lt-integratoren-loeschen"></a>
### STEUERN_LT_INTEGRATOREN_LOESCHEN

KWP2000: $31 StartRoutineByLocalIdentifier $33 Funktionspruefung Kupplung Bedingungen: vFzg &lt; 0,2km/h Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-funktionspruefung"></a>
### STEUERN_FUNKTIONSPRUEFUNG

KWP2000: $31 StartRoutineByLocalIdentifier $32 Kalibrierung loeschen KWP2000: $11 ECUReset $01 PowerOn KWP2000: $31 StartRoutineByLocalIdentifier $30 Funktionspruefung Kupplung Bedingungen: vFzg &lt; 0,2km/h, Kl15 ein, kein Ersatzprg. aktiv Bedingungen: bei nmot&gt;800 UpM muss MKsoll &lt; 10Nm sein Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG_1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG |

<a id="job-vgsg-diagnose-testjob"></a>
### VGSG_DIAGNOSE_TESTJOB

Job fuer VGSG Diagnosetest (max. 8 Daten - SID,LID,usw.) KWP 2000: Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL_DATEN | int | Anzahl Datenbytes |
| DATEN_1 | int | Daten Byte 1 |
| DATEN_2 | int | Daten Byte 2 |
| DATEN_3 | int | Daten Byte 3 |
| DATEN_4 | int | Daten Byte 4 |
| DATEN_5 | int | Daten Byte 5 |
| DATEN_6 | int | Daten Byte 6 |
| DATEN_7 | int | Daten Byte 7 |
| DATEN_8 | int | Daten Byte 8 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VGSG_OUT | binary | Antwort von VGSG  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-getriebe-integratoren"></a>
### WRITE_GETRIEBE_INTEGRATOREN

Getriebe Integratoren ins EEPROM schreiben KWP 2000: $3B WriteDataByLocalIdentifier LID0E Bedingungen: vFzg &lt; 0,2km/h Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN_1 | string | Daten GetriebeArbeit1 |
| DATEN_2 | string | Daten GetriebeArbeit2 |
| DATEN_3 | string | Daten KM Stand Integrator |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-lamellen-integratoren"></a>
### WRITE_LAMELLEN_INTEGRATOREN

Lamellen Integratoren ins EEPROM schreiben KWP 2000: $3B WriteDataByLocalIdentifier LID0F Bedingungen: vFzg &lt; 0,2km/h Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN_1 | string | Daten Lamelle1 |
| DATEN_2 | string | Daten Lamelle2 |
| DATEN_3 | string | Daten Lamelle3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-lt-getriebe-integratoren"></a>
### WRITE_LT_GETRIEBE_INTEGRATOREN

Lifetime Getriebe Integratoren ins EEPROM schreiben KWP2000: $3B WriteDataByLocalIdentifier LID1E Bedingungen: vFzg &lt; 0,2km/h Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN_1 | string | Daten GetriebeArbeit1 |
| DATEN_2 | string | Daten GetriebeArbeit2 |
| DATEN_3 | string | Daten KM Stand Integrator |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-lt-lamellen-integratoren"></a>
### WRITE_LT_LAMELLEN_INTEGRATOREN

Lifetime Lamellen Integratoren ins EEPROM schreiben KWP2000: $3B WriteDataByLocalIdentifier LID1F Bedingungen: vFzg &lt; 0,2km/h Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN_1 | string | Daten Lamelle1 |
| DATEN_2 | string | Daten Lamelle2 |
| DATEN_3 | string | Daten Lamelle3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-mk-soll"></a>
### WRITE_MK_SOLL

Sollmomentvorgabe per Diagnose KWP 2000: $3B WriteDataByLocalIdentifier LID08 Bedingungen: vFzg &lt; 20km/h Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN_1 | string | Daten Sollmoment |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klassierspeicher-ruecksetzen"></a>
### STEUERN_KLASSIERSPEICHER_RUECKSETZEN

Widerstandsklasse des Getriebe neu setzen KWP2000: $3B WriteDataByLocalIdentifier LID11 Bedingungen: vFzg &lt; 0,2km/h Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-verschleissdaten-auslieferzustand"></a>
### STEUERN_VERSCHLEISSDATEN_AUSLIEFERZUSTAND

Auslieferzustand bei CBS (HO-Integratoren) und LT-Integratoren erstellen KWP2000: $3B WriteDataByLocalIdentifier LID12 Bedingungen: vFzg &lt; 0,2km/h und nmot&lt;100 UpM Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (118 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [CBSKENNUNG](#table-cbskennung) (20 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (59 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (42 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (46 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [FF_X_0](#table-ff-x-0) (1 × 4)
- [FF_X_A](#table-ff-x-a) (1 × 5)
- [FF_0_B](#table-ff-0-b) (1 × 7)
- [FF_1_B](#table-ff-1-b) (1 × 5)
- [FF_2_B](#table-ff-2-b) (1 × 6)
- [FF_2_C](#table-ff-2-c) (1 × 6)
- [FF_3_B](#table-ff-3-b) (1 × 7)
- [FF_4_B](#table-ff-4-b) (1 × 6)
- [FF_5_B](#table-ff-5-b) (1 × 7)
- [FF_6_B](#table-ff-6-b) (1 × 7)
- [FF_7_B](#table-ff-7-b) (1 × 6)
- [FF_8_B](#table-ff-8-b) (1 × 7)
- [KL15CAN](#table-kl15can) (3 × 2)
- [KL15](#table-kl15) (2 × 2)
- [NMOT](#table-nmot) (4 × 2)
- [RQ](#table-rq) (8 × 2)
- [SOLL_MOM_ANF](#table-soll-mom-anf) (6 × 2)
- [TORQUE_3](#table-torque-3) (4 × 2)
- [GESCHWINDIGKEIT_RAD](#table-geschwindigkeit-rad) (5 × 2)
- [TORQUE_2](#table-torque-2) (2 × 2)
- [TORQUE_1](#table-torque-1) (3 × 2)
- [STAT_DSC](#table-stat-dsc) (6 × 2)
- [LENKRADWINKEL](#table-lenkradwinkel) (3 × 2)
- [KLEMMENSTATUS](#table-klemmenstatus) (3 × 2)
- [KILOMETERSTAND](#table-kilometerstand) (2 × 2)
- [A_TEMP_RELATIVZEIT](#table-a-temp-relativzeit) (3 × 2)
- [GESCHWINDIGKEIT](#table-geschwindigkeit) (3 × 2)
- [GETRIEBEDATEN](#table-getriebedaten) (5 × 2)
- [GETRIEBEDATEN_2](#table-getriebedaten-2) (2 × 2)
- [FF_A_B](#table-ff-a-b) (1 × 7)
- [FF_B_B](#table-ff-b-b) (1 × 7)
- [FF_C_B](#table-ff-c-b) (1 × 7)
- [FF_D_B](#table-ff-d-b) (1 × 7)
- [FF_E_B](#table-ff-e-b) (1 × 7)
- [FF_F_B](#table-ff-f-b) (1 × 7)
- [FF_G_B](#table-ff-g-b) (1 × 7)
- [FF_H_B](#table-ff-h-b) (1 × 7)
- [FF_I_B](#table-ff-i-b) (1 × 7)
- [FF_J_B](#table-ff-j-b) (1 × 7)
- [FF_K_B](#table-ff-k-b) (1 × 7)
- [FF_L_B](#table-ff-l-b) (1 × 7)
- [FF_M_B](#table-ff-m-b) (1 × 7)
- [ENGINE_1](#table-engine-1) (2 × 2)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 5 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x10 | D-CAN |
| 0x0F | BMW-FAST |
| 0x0D | KWP2000* |
| 0x0C | KWP2000 |
| 0x06 | DS2 |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 95 rows × 2 columns

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
| ?04? | ERROR_ECU_INCORRECT_LIN_RESPONSE_ID |
| ?05? | ERROR_ECU_INCORRECT_LIN_LEN |
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
| ?81? | ERROR_VEHICLE_IDENTIFICATION_NR |
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
| ?9B? | ERROR_MOST_CAN_GATEWAY_DISABLE |
| ?9C? | ERROR_NO_P2MIN |
| ?9D? | ERROR_NO_P2MAX |
| ?9E? | ERROR_NO_P3MIN |
| ?9F? | ERROR_NO_P3MAX |
| ?A0? | ERROR_NO_P4MIN |
| ?B0? | ERROR_DIAG_PROT |
| ?B1? | ERROR_SG_ADRESSE |
| ?B2? | ERROR_SG_MAXANZAHL_AIF |
| ?B3? | ERROR_SG_GROESSE_AIF |
| ?B4? | ERROR_SG_ENDEKENNUNG_AIF |
| ?B5? | ERROR_SG_AUTHENTISIERUNG |
| ?C0? | ERROR_TELEGRAM_LEN_OUT_OFF_RANGE |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 118 rows × 2 columns

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
| 0x9A | Takata- Petri |
| 0x9B | Mitsubishi Electric B.V. (Melco) |
| 0x9C | Autokabel |
| 0x9D | GKN-Driveline |
| 0x9E | Zollner Elektronik AG |
| 0x9F | PEIKER acustics GmbH |
| 0xA0 | Bosal-Oris |
| 0xA1 | Cobasys |
| 0xA2 | Lighting Reutlingen GmbH |
| 0xA3 | CONTI VDO |
| 0xA4 | ADC Automotive Distance Control Systems GmbH |
| 0xA5 | Funkwerk Dabendorf GmbH |
| 0xA6 | Lame |
| 0xA7 | Magna/Closures |
| 0xA8 | Wanyu |
| 0xA9 | Thyssen Krupp Presta |
| 0xAA | ArvinMeritor |
| 0xAB | Kongsberg Automotive GmbH |
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
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

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

<a id="table-authentisierung"></a>
### AUTHENTISIERUNG

Dimensions: 4 rows × 2 columns

| AUTH_NR | AUTH_TEXT |
| --- | --- |
| 0x01 | Simple |
| 0x02 | Symetrisch |
| 0x03 | Asymetrisch |
| 0xFF | Keine |

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

<a id="table-programmierstatus"></a>
### PROGRAMMIERSTATUS

Dimensions: 19 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | Anlieferzustand |
| 0x01 | Normalbetrieb |
| 0x02 | nicht benutzt |
| 0x03 | Speicher gelöscht |
| 0x04 | nicht benutzt |
| 0x05 | Signaturprüfung PAF nicht durchgeführt |
| 0x06 | Signaturprüfung DAF nicht durchgeführt |
| 0x07 | Programmprogrammiersitzung aktiv |
| 0x08 | Datenprogrammiersitzung aktiv |
| 0x09 | Hardwarereferenzeintrag fehlerhaft |
| 0x0A | Programmreferenzeintrag fehlerhaft |
| 0x0B | Referenzierungsfehler Hardware -&gt; Programm |
| 0x0C | Programm nicht vorhanden oder nicht vollständig |
| 0x0D | Datenreferenzeintrag fehlerhaft |
| 0x0E | Referenzierungsfehler Programm -&gt; Daten |
| 0x0F | Daten nicht vorhanden oder nicht vollständig |
| 0x10 | Reserviert fuer BMW |
| 0x80 | Reserviert fuer Zulieferer |
| 0xXY | unbekannter Programmierstatus |

<a id="table-cbskennung"></a>
### CBSKENNUNG

Dimensions: 20 rows × 3 columns

| NR | CBS_K | CBS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Motoroel |
| 0x02 | Br_v | Bremsbelag vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x04 | Filt | Mikrofilter |
| 0x06 | Br_h | Bremsbelag hinten |
| 0x07 | CSF | Dieselpartikelfilter |
| 0x08 | Batt | Batterie |
| 0x09 | QMV | QMV-H-Oel |
| 0x10 | ZKrz | Zuendkerzen |
| 0x11 | Sic | Sichtpruefung/Fahrzeug-Check |
| 0x12 | Kfl | Kuehlfluessigkeit |
| 0x13 | H2 | H2-Check |
| 0x14 | Ueb | Uebergabedurchsicht |
| 0x15 | Efk | Einfahrkontrolle |
| 0x16 | DAD | Additiv fuer Partikelfilter |
| 0x20 | TUV | §Fahrzeuguntersuchung |
| 0x21 | AU | §Abgasuntersuchung |
| 0x23 | DKG | DK-Getriebeoel |
| 0x0A | ZKrz_a | Zuendkerzen adaptiv |
| 0x0D | NOx_a | NOx-Additiv |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 4 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| 1 | BMW-FAST |
| - | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 59 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5208 | 5208 Stellmotor Verkabelung |
| 0x52D0 | 52D0 Inkrementalgeber DIR - Leitung |
| 0x52D1 | 52D1 Inkrementalgeber Versorgung |
| 0x52D2 | 52D2 Inkrementalgeber IMP - Leitung |
| 0x52D4 | 52D4 Inkrementalgeber unplausibel |
| 0x5398 | 5398 Prüfsummenfehler Programmcode |
| 0x5399 | 5399 Prüfsummenfehler EEPROM |
| 0x539A | 539A Watchdog Fehlfunktion |
| 0x539B | 539B Prüffehler RAM |
| 0x539D | 539D Steuergerät interner Fehler |
| 0x53A0 | 53A0 Steuergerät nicht codiert bzw. Codierung ist fehlerhaft |
| 0x53FB | 53FB Fehlende Versorgung |
| 0x53FC | 53FC KL30 Versorgungsspannung |
| 0x53FD | 53FD KL30g Versorgungsspannung |
| 0x53FE | 53FE Unerwarteter Reset |
| 0x53FF | 53FF Kl15 Plausibilität |
| 0x5460 | 5460 Motorstrommessung Plausibilität |
| 0x5461 | 5461 Fehler Stellmotoransteuerung |
| 0x5462 | 5462 Fehler Stellmotor oder erhöhter Kraftbedarf Kupplung |
| 0x5463 | 5463 Bruch Mechanik |
| 0x54C4 | 54C4 Kalibrierung fehlerhaft |
| 0x54C5 | 54C5 Motorstrommessung Offset Strommessung |
| 0x54C6 | 54C6 Ölverschleiss |
| 0x55C0 | 55C0 Allrad Abschaltung. Abbruch VGSG-Allrad-Notlaufregelung wegen falscher CAN-Signale. |
| 0x55C2 | 55C2 Allrad Abschaltung. Keine DXC Sollmomentenvorgabe. |
| 0x55C3 | 55C3 VGSG-Allrad-Notlaufregelung aktiviert. Keine DXC Sollmomentenvorgabe. |
| 0x55C4 | 55C4 CAN_MESSAGE_SOLL_MOM_ANF, BB |
| 0x55C5 | 55C5 CAN_MESSAGE_TORQUE_3, AA |
| 0x55C6 | 55C6 CAN_MESSAGE_GESCHWINDIGKEIT_RAD, CE |
| 0x55C7 | 55C7 CAN_MESSAGE_GESCHWINDIGKEIT, 1A0 |
| 0x55C8 | 55C8 CAN_MESSAGE_KLEMMENSTATUS, 130 |
| 0x55C9 | 55C9 CAN_MESSAGE_TORQUE_1, A8 |
| 0x55CA | 55CA CAN_MESSAGE_KILOMETERSTAND, 330 |
| 0x55CB | 55CB CAN_MESSAGE_A_TEMP_RELATIVZEIT, 310 |
| 0x55CD | 55CD CAN_MESSAGE_STAT_DSC, 19E |
| 0x55CE | 55CE CAN_MESSAGE_GETRIEBEDATEN, BA |
| 0x55CF | 55CF CAN_MESSAGE_GETRIEBEDATEN_2, 1A2 |
| 0x55D0 | 55D0 CAN_MESSAGE_LENKRADWINKEL, C4 |
| 0x55D1 | 55D1 CAN_MESSAGE_ENGINE_1, 1D0 |
| 0xCF4B | CF4B CAN Bus Off |
| 0xCF54 | CF54 CAN_TIMEOUT_SOLL_MOM_ANF, BB |
| 0xCF55 | CF55 CAN_TIMEOUT_TORQUE_3, AA |
| 0xCF56 | CF56 CAN_TIMEOUT_GESCHWINDIGKEIT_RAD, CE |
| 0xCF57 | CF57 CAN_TIMEOUT_GESCHWINDIGKEIT, 1A0 |
| 0xCF58 | CF58 CAN_TIMEOUT_KLEMMENSTATUS, 130 |
| 0xCF59 | CF59 CAN_TIMEOUT_TORQUE_1, A8 |
| 0xCF5A | CF5A CAN_TIMEOUT_KILOMETERSTAND, 330 |
| 0xCF5B | CF5B CAN_TIMEOUT_A_TEMP_RELATIVZEIT, 310 |
| 0xCF5D | CF5D CAN_TIMEOUT_STAT_DSC, 19E |
| 0xCF5E | CF5E CAN_TIMEOUT_GETRIEBEDATEN, BA |
| 0xCF5F | CF5F CAN_TIMEOUT_GETRIEBEDATEN_2, 1A2 |
| 0xCF60 | CF60 CAN_TIMEOUT_LENKRADWINKEL, C4 |
| 0xCF61 | CF61 CAN_TIMEOUT_ENGINE_1, 1D0 |
| 0x55C1 | 55C1 ALLRADVERLUST |
| 0x54C7 | 54C7 Modell - Inkrementalgeber unplausibel |
| 0x54C8 | 54C8 Klassierwiderstand am Stellmotor |
| 0x54C9 | 54C9 Temperatursensor am Stellmotor |
| 0x539E | 539E Funktionsfehler VTG Gesamtsystem |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 42 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x5208 | 0x01 | FF_x_a | FF_3_b | - |
| 0x54C8 | 0x01 | FF_x_a | FF_3_b | - |
| 0x54C9 | 0x01 | FF_x_a | FF_3_b | - |
| 0x52D0 | 0x01 | FF_x_a | FF_2_b | FF_2_c |
| 0x52D1 | 0x01 | FF_x_a | FF_2_b | FF_2_c |
| 0x52D2 | 0x01 | FF_x_a | FF_2_b | FF_2_c |
| 0x52D4 | 0x01 | FF_x_a | FF_2_b | FF_2_c |
| 0x5398 | 0x01 | FF_x_a | FF_7_b | - |
| 0x5399 | 0x01 | FF_x_a | FF_7_b | - |
| 0x539A | 0x01 | FF_x_a | FF_4_b | - |
| 0x539B | 0x01 | FF_x_a | FF_4_b | - |
| 0x539D | 0x01 | FF_x_a | FF_4_b | - |
| 0x53A0 | 0x01 | FF_x_a | FF_4_b | - |
| 0x53FB | 0x01 | FF_x_a | FF_1_b | 0x0F |
| 0x53FC | 0x01 | FF_x_a | FF_2_b | FF_2_c |
| 0x53FD | 0x01 | FF_x_a | FF_2_b | FF_2_c |
| 0x53FE | 0x01 | FF_x_a | FF_1_b | 0x0F |
| 0x53FF | 0x01 | FF_x_a | FF_0_b | - |
| 0x5460 | 0x01 | FF_x_a | FF_6_b | - |
| 0x5461 | 0x01 | FF_x_a | FF_6_b | - |
| 0x5462 | 0x01 | FF_x_a | FF_6_b | - |
| 0x5463 | 0x01 | FF_x_a | FF_6_b | - |
| 0x54C4 | 0x01 | FF_x_a | FF_6_b | - |
| 0x54C5 | 0x01 | FF_x_a | FF_6_b | - |
| 0x54C6 | 0x01 | FF_x_a | FF_0_b | - |
| 0x54C7 | 0x01 | FF_x_a | FF_6_b | - |
| 0x539E | 0x01 | FF_x_a | FF_6_b | - |
| 0x55C4 | 0x01 | FF_x_a | FF_A_b | - |
| 0x55C5 | 0x01 | FF_x_a | FF_B_b | - |
| 0x55C6 | 0x01 | FF_x_a | FF_C_b | - |
| 0x55C7 | 0x01 | FF_x_a | FF_D_b | - |
| 0x55C8 | 0x01 | FF_x_a | FF_E_b | - |
| 0x55C9 | 0x01 | FF_x_a | FF_F_b | - |
| 0x55CA | 0x01 | FF_x_a | FF_G_b | - |
| 0x55CB | 0x01 | FF_x_a | FF_H_b | - |
| 0x55CD | 0x01 | FF_x_a | FF_I_b | - |
| 0x55CE | 0x01 | FF_x_a | FF_J_b | - |
| 0x55CF | 0x01 | FF_x_a | FF_K_b | - |
| 0x55D0 | 0x01 | FF_x_a | FF_L_b | - |
| 0x55D1 | 0x01 | FF_x_a | FF_M_b | - |
| 0x55C1 | 0x01 | FF_x_a | FF_8_b | - |
| default | 0x01 | FF_x_a | FF_5_b | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 46 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Eingangsspannung KL30 | Volt | - | unsigned char | - | 1 | 8 | 0 |
| 0x02 | KL15 Status CAN | 0-n | - | 0x03 | KL15CAN | 1 | 1 | 0 |
| 0x03 | KL15 Intern | 0-n | - | 0x04 | KL15 | 1 | 1 | 0 |
| 0x04 | Motordrehzahl | 0-n | - | 0x18 | NMOT | 1 | 1 | 0 |
| 0x05 | Reset-Quelle | 0-n | - | 0xE0 | RQ | 1 | 1 | 0 |
| 0x06 | MKSOLL | Nm | - | unsigned char | - | 10 | 1 | 0 |
| 0x07 | MSperrIstPosLim | Nm | - | unsigned char | - | 8 | 1 | 0 |
| 0x08 | deltaPhiSperreCal | Grad | - | unsigned char | - | -1 | 1 | 0 |
| 0x09 | SperreError | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x0A | SperreState | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x0B | SperreMainState | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x0E | iSM | Ampere | - | signed char | - | 1 | 2 | 0 |
| 0x0F | ResetWhileEngineOn | 0/1 | - | 0x01 | - | 1 | 1 | 0 |
| 0x10 | Fehlerzähler Kalibrierversuche | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x11 | Fehlerzähler Zeitüberschreitung | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x12 | SwErrNr | HEX | - | unsigned int | H | 1 | 1 | 0 |
| 0x13 | SGTemp | Grad C | - | signed char | - | 2 | 1 | 0 |
| 0x14 | CAN_Fehlersignale | 1 | - | unsigned char | _ | 1 | 1 | 0 |
| 0x15 | uSM_IE_VCC_ST | 0/1 | - | 0x01 | - | 1 | 1 | 0 |
| 0x16 | Plausib_Ink_Gradient | 0/1 | - | 0x02 | - | 1 | 1 | 0 |
| 0x17 | Plausib_Ink_Frequenz | 0/1 | - | 0x04 | - | 1 | 1 | 0 |
| 0x18 | Plausib_MotorModell | 0/1 | - | 0x08 | - | 1 | 1 | 0 |
| 0x19 | Plausib_Ink_Wackler | 0/1 | - | 0x10 | - | 1 | 1 | 0 |
| 0x1A | Page Number | HEX | - | unsigned char | - | 1 | 1 | 0 |
| 0x1B | Info | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x1C | Status | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x1D | SOLL_MOM_ANF_Fehlersignale | 0-n | - | 0x1F | SOLL_MOM_ANF | 1 | 1 | 0 |
| 0x1E | TORQUE_3_Fehlersignale | 0-n | - | 0x07 | TORQUE_3 | 1 | 1 | 0 |
| 0x1F | GESCHWINDIGKEIT_RAD_Fehlersignale | 0-n | - | 0x0F | GESCHWINDIGKEIT_RAD | 1 | 1 | 0 |
| 0x20 | SperreNotlauf | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x21 | EP_Sperre | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x22 | ExeptionHandlingKUPPSTAT | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x23 | ExeptionHandlingKUPPSTATERR | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x24 | ErrorKUPPSTAT | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x25 | TORQUE_2_FehlerSignale | 0-n | - | 0x01 | TORQUE_2 | 1 | 1 | 0 |
| 0x26 | TORQUE_1_FehlerSignale | 0-n | - | 0x03 | TORQUE_1 | 1 | 1 | 0 |
| 0x27 | STAT_DSC_FehlerSignale | 0-n | - | 0x1F | STAT_DSC | 1 | 1 | 0 |
| 0x28 | LENKRADWINKEL_FehlerSignale | 0-n | - | 0x03 | LENKRADWINKEL | 1 | 1 | 0 |
| 0x29 | KLEMMENSTATUS_FehlerSignale | 0-n | - | 0x03 | KLEMMENSTATUS | 1 | 1 | 0 |
| 0x2A | KILOMETERSTAND_FehlerSignale | 0-n | - | 0x01 | KILOMETERSTAND | 1 | 1 | 0 |
| 0x2B | A_TEMP_RELATIVZEIT_FehlerSignale | 0-n | - | 0x03 | A_TEMP_RELATIVZEIT | 1 | 1 | 0 |
| 0x2C | GESCHWINDIGKEIT_FehlerSignale | 0-n | - | 0x03 | GESCHWINDIGKEIT | 1 | 1 | 0 |
| 0x2D | GETRIEBEDATEN_FehlerSignale | 0-n | - | 0x0F | GETRIEBEDATEN | 1 | 1 | 0 |
| 0x2E | GETRIEBEDATEN_2_FehlerSignale | 0-n | - | 0x01 | GETRIEBEDATEN_2 | 1 | 1 | 0 |
| 0x2F | ENGINE_1_FehlerSignale | 0-n | - | 0x01 | ENGINE_1 | 1 | 1 | 0 |
| 0xFF | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

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

<a id="table-ff-x-0"></a>
### FF_X_0

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x02 | 0x03 | 0x04 |

<a id="table-ff-x-a"></a>
### FF_X_A

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x02 | 0x03 | 0x04 | 0x05 |

<a id="table-ff-0-b"></a>
### FF_0_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0A | 0x0B |

<a id="table-ff-1-b"></a>
### FF_1_B

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x06 | 0x0B | 0x12 | 0x13 |

<a id="table-ff-2-b"></a>
### FF_2_B

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x0E | 0x07 | 0x08 | 0x09 | 0x0B |

<a id="table-ff-2-c"></a>
### FF_2_C

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x15 | 0x16 | 0x17 | 0x18 | 0x19 |

<a id="table-ff-3-b"></a>
### FF_3_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x09 | 0x0B | 0x13 | 0x0E |

<a id="table-ff-4-b"></a>
### FF_4_B

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x0E | 0x0B | 0x1A | 0x12 | 0x13 |

<a id="table-ff-5-b"></a>
### FF_5_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x14 |

<a id="table-ff-6-b"></a>
### FF_6_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x0E | 0x07 | 0x10 | 0x09 | 0x0B | 0x11 |

<a id="table-ff-7-b"></a>
### FF_7_B

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x1B | 0x1C | 0x1A | 0x12 | 0x13 |

<a id="table-ff-8-b"></a>
### FF_8_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x20 | 0x21 | 0x0B | 0x09 | 0x22 | 0x23 |

<a id="table-kl15can"></a>
### KL15CAN

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | CAN Signal OK -- KL15 aus |
| 0x01 | CAN Signal OK -- KL15 ein |
| 0xXY | CAN Signal Timeout -- KL15 unbekannt |

<a id="table-kl15"></a>
### KL15

Dimensions: 2 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | KL15 aus |
| 0x04 | KL15 ein |

<a id="table-nmot"></a>
### NMOT

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | CAN Signal OK -- VKM aus |
| 0x08 | CAN Signal OK -- VKM ein |
| 0x10 | Ersatzwert -- VKM aus |
| 0x18 | Ersatzwert -- VKM ein |

<a id="table-rq"></a>
### RQ

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | UNKOWN_SOURCE |
| 0x20 | EE_RST_MARKER |
| 0x40 | OSEK_SHUTDOWN |
| 0x60 | BASIS_DRIVER_ERROR |
| 0x80 | UNDER_VOLTAGE |
| 0xA0 | INTERNAL_WATCHDOG |
| 0xC0 | EXTERN_WATCHDOG |
| 0xE0 | NO RESET |

<a id="table-soll-mom-anf"></a>
### SOLL_MOM_ANF

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | DSC_MOM_TAR_FTAX |
| 0x02 | DSC_ACV_OPN |
| 0x04 | DSC_DYNMC_DXC |
| 0x08 | DSC_RQ_FNT |
| 0x10 | DSC_EMMOD_OPN |
| 0xXY | multiple Signals |

<a id="table-torque-3"></a>
### TORQUE_3

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | TORQUE_3_N_MOT |
| 0x02 | TORQUE_3_ANG_ACPD |
| 0x04 | TORQUE_3_TORQ_DVCH |
| 0xXY | multiple Signals |

<a id="table-geschwindigkeit-rad"></a>
### GESCHWINDIGKEIT_RAD

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | GESCHWINDIGKEIT_RAD_V_WHL_FLH |
| 0x02 | GESCHWINDIGKEIT_RAD_V_WHL_FRH |
| 0x04 | GESCHWINDIGKEIT_RAD_V_WHL_RLH |
| 0x08 | GESCHWINDIGKEIT_RAD_V_WHL_RRH |
| 0xXY | multiple Signals |

<a id="table-torque-2"></a>
### TORQUE_2

Dimensions: 2 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | TORQUE_2_TORQ_AVL_MIN |
| 0xXY | multiple Signals |

<a id="table-torque-1"></a>
### TORQUE_1

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | TORQUE_1_ST_SW_CLT |
| 0x02 | TORQUE_1_ST_CT_BRPD_DME |
| 0xXY | multiple Signals |

<a id="table-stat-dsc"></a>
### STAT_DSC

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | STAT_DSC_ST_CT_BRPD |
| 0x02 | STAT_DSC_BRP |
| 0x04 | STAT_DSC_ST_ABS |
| 0x08 | STAT_DSC_ST_CLCTR |
| 0x10 | STAT_DSC_ST_HBA |
| 0xXY | multiple Signals |

<a id="table-lenkradwinkel"></a>
### LENKRADWINKEL

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | SIG_STWA |
| 0x02 | SIG_STWA_ERR |
| 0xXY | multiple Signals |

<a id="table-klemmenstatus"></a>
### KLEMMENSTATUS

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | KLEMMENSTATUS_ST_KL15 |
| 0x02 | KLEMMENSTATUS_ST_KL50 |
| 0xXY | multiple Signals |

<a id="table-kilometerstand"></a>
### KILOMETERSTAND

Dimensions: 2 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | KILOMETERSTAND_MILE_KM |
| 0xXY | multiple Signals |

<a id="table-a-temp-relativzeit"></a>
### A_TEMP_RELATIVZEIT

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | A_TEMP_RELATIVZEIT_T_TEMP_EX |
| 0x02 | A_TEMP_RELATIVZEIT_T_SEC_COU_REL |
| 0xXY | multiple Signals |

<a id="table-geschwindigkeit"></a>
### GESCHWINDIGKEIT

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | GESCHWINDIGKEIT_ACLN_VEH_ACRO_DSC |
| 0x02 | GESCHWINDIGKEIT_ANGV_YAW_DSC |
| 0xXY | multiple Signals |

<a id="table-getriebedaten"></a>
### GETRIEBEDATEN

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | GETRIEBEDATEN_ST_GR_GRB |
| 0x02 | GETRIEBEDATEN_ST_GRLV_ACV |
| 0x04 | GETRIEBEDATEN_ST_CCLT |
| 0x08 | GETRIEBEDATEN_RPM_GRB_NEGL |
| 0xXY | multiple Signals |

<a id="table-getriebedaten-2"></a>
### GETRIEBEDATEN_2

Dimensions: 2 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | GETRIEBEDATEN_2_RPM_GRB_TURB |
| 0xXY | multiple Signals |

<a id="table-ff-a-b"></a>
### FF_A_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x1D |

<a id="table-ff-b-b"></a>
### FF_B_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x1E |

<a id="table-ff-c-b"></a>
### FF_C_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x1F |

<a id="table-ff-d-b"></a>
### FF_D_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x2C |

<a id="table-ff-e-b"></a>
### FF_E_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x29 |

<a id="table-ff-f-b"></a>
### FF_F_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x26 |

<a id="table-ff-g-b"></a>
### FF_G_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x2A |

<a id="table-ff-h-b"></a>
### FF_H_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x2B |

<a id="table-ff-i-b"></a>
### FF_I_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x27 |

<a id="table-ff-j-b"></a>
### FF_J_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x2D |

<a id="table-ff-k-b"></a>
### FF_K_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x2E |

<a id="table-ff-l-b"></a>
### FF_L_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x28 |

<a id="table-ff-m-b"></a>
### FF_M_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x2F |

<a id="table-engine-1"></a>
### ENGINE_1

Dimensions: 2 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | ENGINE_1_ST_ENG_RUN |
| 0xXY | multiple Signals |
