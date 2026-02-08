# HUD_60.prg

- Jobs: [99](#jobs)
- Tables: [40](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Head-Up-Display |
| ORIGIN | BMW EE-42 Mangold |
| REVISION | 1.01 |
| AUTHOR | BMW EE-42 Mangold, ESG TM-K Philipp, ESG AB-K Steiner |
| COMMENT | SGBD fuer HUD E60 |
| PACKAGE | 1.32 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
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
- [FS_SPERREN](#job-fs-sperren) - Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $00 all ECU Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
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
- [C_CHECKSUMME](#job-c-checksumme) - Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob
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
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
- [MOST_VERSION_LESEN](#job-most-version-lesen) - Auslesen von Most Version KWP2000: $21 ReadDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $A0 MOSTVersion MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STATUS_MOST_3DB](#job-status-most-3db) - Auslesen des Status der Lichtleistungsabsenkung KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AF OpticalTransmitPowSwitch MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STEUERN_MOST_3DB](#job-steuern-most-3db) - Lichtleistungsabsenkung einschalten KWP2000: $3B WriteDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AF OpticalTransmitPowSwitch $00 S1 geoeffnet = 3dB Absenkung MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STATUS_WAKE_UP_STATUS](#job-status-wake-up-status) - Auslesen des Status WakeupStatus KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD WakeUpStatus MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STATUS_ABILITY_TO_WAKE](#job-status-ability-to-wake) - Auslesen des Status AbilityToWake KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD WakeUpStatus MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STEUERN_ABILITY_TO_WAKE](#job-steuern-ability-to-wake) - AbilityToWake einstellen KWP2000: $3B WriteDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD AbilityToWake $00 of, $01 on, $02 critical MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [_STATUS_MPC_PWM](#job-status-mpc-pwm) - PWM-Ports des MPC 555 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $90 $01 xxh xx: Portnummer
- [_STATUS_MPC_ADC](#job-status-mpc-adc) - ADC-Kanäle des MPC 555 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $91 $01 $xx xx: Kanalnummer
- [_STATUS_MPC_MDASM](#job-status-mpc-mdasm) - MDASM-Kanäle des MPC 555 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $92 $01 $xx xx: Portnummer
- [_STATUS_MPC_IO](#job-status-mpc-io) - I/O-Ports des MPC 555 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $93 $01 $xx xx: Portnummer
- [_STATUS_ASSP_ADC](#job-status-assp-adc) - ADC-Kanäle des ASSP 3 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $25 $01 $xx 
- [_STATUS_ASSP_IO](#job-status-assp-io) - I/O-Ports des ASSP 3 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $27 $01 $xx xx: Portnummer
- [_STEUERN_MPC_PWM](#job-steuern-mpc-pwm) - PWM-Ports des MPC 555 setzen KWP2000: $30 InputOutputControlByLocalIdentifier $90 $07 Anforderung $90 $06 $pp $hh $ll Durchführung $pp: Portnummer $hh: High Byte $ll: Low Byte
- [STEUERN_HELLIGKEIT](#job-steuern-helligkeit) - PWM-Ports der Dimmungswerte des MPC 555 setzen KWP2000: $30 InputOutputControlByLocalIdentifier $90 $07 Anforderung $90 $06 $pp $hh $ll Durchführung $pp: 0x03, 0x11 und 0x13 $hh: High Byte $ll: Low Byte
- [STATUS_HELLIGKEIT](#job-status-helligkeit) - PWM-Ports der Dimmungswerte des MPC 555 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $90 $01 xxh xx: Portnummer
- [STEUERN_STROMWERTE](#job-steuern-stromwerte) - PWM-Ports der Referenzstromwerte des MPC 555 setzen KWP2000: $30 InputOutputControlByLocalIdentifier $90 $07 Anforderung $90 $06 $pp $hh $ll Durchführung $pp: 0x00, 0x01 und 0x12 $hh: High Byte $ll: Low Byte
- [STATUS_STROMWERTE](#job-status-stromwerte) - PWM-Ports der Referenzstromwerte des MPC 555 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $90 $01 xxh xx: Portnummer
- [_STEUERN_TASTER](#job-steuern-taster) - ADC-Kanal 00 des MPC 555 setzen Tasterbetätigung wird simuliert KWP2000: $30 InputOutputControlByLocalIdentifier $90 $07 Anforderung $90 $06 $kk $hh $ll Durchführung $pp: Kanalnummer $hh: High Byte $ll: Low Byte
- [_STEUERN_TASTER_STOP](#job-steuern-taster-stop) - ADC-Kanal 00 des MPC 555 setzen Tastersimulation wird beendet KWP2000: $30 InputOutputControlByLocalIdentifier $90 $07 Anforderung $90 $06 $kk $hh $ll Durchführung $pp: Kanalnummer $hh: High Byte $ll: Low Byte
- [STATUS_TASTER](#job-status-taster) - ADC-Kanal Nr.0 des MPC 555 auslesen 3,3V Taster betätigt 4,2V Taster nicht betätigt 5,0V Taster nicht angeschlossen KWP2000: $30 InputOutputControlByLocalIdentifier $91 $01 $xx xx: Kanalnummer
- [STATUS_BACKLIGHT_ENABLE](#job-status-backlight-enable) - ADC-Kanal Nr.3 des MPC 555 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $91 $01 $xx xx: Kanalnummer
- [_STEUERN_MPC_PWM_STOP](#job-steuern-mpc-pwm-stop) - Zugriff auf die PWM-Ports des MPC 555 beenden KWP2000: $30 InputOutputControlByLocalIdentifier $90 $00 Keine Argumente erforderlich
- [_STEUERN_MPC_ADC](#job-steuern-mpc-adc) - ADC-Kanäle des MPC 555 setzen KWP2000: $30 InputOutputControlByLocalIdentifier $90 $07 Anforderung $90 $06 $kk $hh $ll Durchführung $pp: Kanalnummer $hh: High Byte $ll: Low Byte
- [_STEUERN_MPC_ADC_STOP](#job-steuern-mpc-adc-stop) - Zugriff auf die ADC-Kanäle des MPC 555 beenden KWP2000: $30 InputOutputControlByLocalIdentifier $91 $00 Keine Argumente erforderlich
- [_STEUERN_MPC_MDASM](#job-steuern-mpc-mdasm) - MDASM-Kanäle des MPC 555 setzen KWP2000: $30 InputOutputControlByLocalIdentifier $92 $07 Anforderung $92 $06 $kk $ww Durchführung $kk: Kanalnummer $ww: Wert
- [_STEUERN_MPC_MDASM_STOP](#job-steuern-mpc-mdasm-stop) - Zugriff auf die MDASM des MPC 555 beenden KWP2000: $30 InputOutputControlByLocalIdentifier $92 $00 Keine Argumente erforderlich
- [_STEUERN_MPC_IO](#job-steuern-mpc-io) - I/O-Ports des MPC 555 setzen KWP2000: $30 InputOutputControlByLocalIdentifier $93 $07 Anforderung $93 $06 $kk $ww Durchführung $kk: Kanalnummer $ww: Wert
- [_STEUERN_MPC_IO_STOP](#job-steuern-mpc-io-stop) - Zugriff auf die I/O-Ports des MPC 555 beenden KWP2000: $30 InputOutputControlByLocalIdentifier $93 $00 Keine Argumente erforderlich
- [STEUERN_TESTBILD](#job-steuern-testbild) - Testbilder anzeigen Zustand ist erst durch Sleep Modus beendet KWP2000: $30 InputOutputControlByLocalIdentifier $FD $06
- [_STEUERN_DISPLAYBEREICH](#job-steuern-displaybereich) - Ausgewählte Displaybereiche ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $FEh 07 Anforderung $FEh 06 $aN $eN $gg $aN: Anfangsadresse $eN: Endadresse $gg: Grauwert
- [STEUERN_SELBSTTEST_EIN](#job-steuern-selbsttest-ein) - Selbsttestfunktion des Steuergeräts aktvieren KWP2000: $30 InputOutputControlByLocalIdentifier $26 $06 Keine Argumente erforderlich
- [STEUERN_SELBSTTEST_AUS](#job-steuern-selbsttest-aus) - Selbsttest des ASSP3 deaktivieren KWP2000: $30 InputOutputControlByLocalIdentifier $26 $00 Keine Argumente erforderlich
- [_STEUERN_ASSP_IO](#job-steuern-assp-io) - I/O-Ports des ASSP 3 setzen KWP2000: $30 InputOutputControlByLocalIdentifier $27 $07 Anforderung $27 $06 $kk $ww Durchführung $kk: Kanalnummer $ww: Wert
- [_STEUERN_ASSP_IO_STOP](#job-steuern-assp-io-stop) - Zugriff auf die I/O-Ports des ASSP 3 beenden KWP2000: $30 InputOutputControlByLocalIdentifier $27 $00 Keine Argumente erforderlich
- [_STEUERN_VOLLSCHRITT](#job-steuern-vollschritt) - Vollschritt-Test aktivieren KWP2000: $30 InputOutputControlByLocalIdentifier $FB $07 Anforderung $FB $06 $m1 $m2 $m3 $m4 Durchführung $m1: Schrittmotor 1 $m2: Schrittmotor 2 $m3: Schrittmotor 3 $m4: Schrittmotor 4
- [STEUERN_SHUTTER](#job-steuern-shutter) - Shutter auf oder zu fahren KWP2000: $30 InputOutputControlByLocalIdentifier $FB $07 Anforderung $FB $06 $m1 $m2 $m3 $m4 Durchführung $m1: Schrittmotor 1 $m2: Schrittmotor 2 $m3: Schrittmotor 3 $m4: Schrittmotor 4
- [_STEUERN_VOLLSCHRITT_STOP](#job-steuern-vollschritt-stop) - Vollschritt-Test beenden KWP2000: $30 InputOutputControlByLocalIdentifier $FB $00 Keine Argumente erforderlich
- [_STEUERN_MIKROSCHRITT_STOP](#job-steuern-mikroschritt-stop) - Schrittmotor in Ausgangsposition zurückstellen KWP2000: $30 InputOutputControlByLocalIdentifier $20 $00 Keine Argumente erforderlich
- [_STEUERN_MIKROSCHRITT](#job-steuern-mikroschritt) - Schrittmotor um vorgegebenen Winkel vorwärts bewegen. KWP2000: $30 InputOutputControlByLocalIdentifier $20 $07 Anforderung $20 $06 $hh $$ll Durchführung $hh: High Byte $ll: Low Byte
- [STATUS_ARRAY_TEMPERATUR](#job-status-array-temperatur) - Temperatur des LED Arrays auslesen
- [STATUS_KLEMMEN](#job-status-klemmen) - Klemmenstatus auslesen
- [STATUS_BORDNETZSPANNUNG](#job-status-bordnetzspannung) - Bordnetzspannung über AD-Kanal 4 des MPC auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $91 $01 $04
- [STATUS_ENERGIESPARMODUS](#job-status-energiesparmodus) - Aktivierten Energiesparmodus auslesen
- [_STATUS_SHACKHARTMANN_TESTER](#job-status-shackhartmann-tester) - Auslesen des Steuergeraete-Speichers KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [STEUERN_STEUERGERAETE_RESET](#job-steuern-steuergeraete-reset) - Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [_STATUS_HUD](#job-status-hud) - Status HUD auslesen Prüft, ob Display EIN oder AUS ist

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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

<a id="job-fs-sperren"></a>
### FS_SPERREN

Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPERREN | string | "ja"   -&gt; Fehlerspeicher sperren "nein" -&gt; Fehlerspeicher freigeben table DigitalArgument TEXT |
| SG_ANTWORT | string | "ja"   -&gt; SG soll antworten "nein" -&gt; SG soll nicht antworten table DigitalArgument TEXT Default:  SG soll antworten |
| FUNKTIONAL | string | "ja"   -&gt; Funktionale Adresse 0xEF wird benutzt nur in Verbindung mit SG_ANTWORT="nein" "nein" -&gt; SG Adresse wird benutzt table DigitalArgument TEXT Default:  SG Adresse wird benutzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table IOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen-detail"></a>
### IS_LESEN_DETAIL

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Infocode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt. Es darf dann nicht argument F_POS angegeben werden |
| F_POS | int | gewaehlter Eintrag Wenn dieser Parameter angegeben wird, wird die Position benutzt. Wertebereich 1 - 255 Es darf dann nicht argument F_CODE angegeben werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table IOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-loeschen"></a>
### IS_LOESCHEN

Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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

SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $00 all ECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | string | table SpeicherSegment SEG_NAME SEG_TEXT |
| ADRESSE | long | 0x000000 - 0xFFFFFF |
| ANZAHL | int | 1 - n ( 254 ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | string | table SpeicherSegment SEG_NAME SEG_TEXT |
| ADRESSE | long | 0x000000 - 0xFFFFFF |
| ANZAHL | int | 1 - n ( max. 249 ) |
| DATEN | string | zu schreibende Daten (Anzahl siehe oben) z.B. 1,2,03,0x04,0x05... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-energiesparmode"></a>
### ENERGIESPARMODE

Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default

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
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer 7-stellig |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-c-checksumme"></a>
### C_CHECKSUMME

Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| OUT_BUFFER | binary | Als Result wird der gefuellte Binaerbuffer zurueckgegeben Der Binaerbuffer hat den Aufbau von BINAER_BUFFER |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-blocklaenge-lesen"></a>
### FLASH_BLOCKLAENGE_LESEN

Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_BLOCKLAENGE_GESAMT | int | Flash Blocklaenge inclusive SID |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge |
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
| AUTHENTISIERUNG | string | Authentisierungsart 'Keine'        Keine Authentisierung 'Simple'       Einfache Authentisierung 'Symetrisch'   Symetrische Authentisierung 'Asymetrisch'  Asymetrische Authentisierung |
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
| FLASH_SCHREIBEN_ANZAHL | int | Anzahl FLASH_SCHREIBEN seit letztem FLASH_SCHREIBEN_ADRESSE |
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
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG AIF schreiben |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG AIF schreiben |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

<a id="job-most-version-lesen"></a>
### MOST_VERSION_LESEN

Auslesen von Most Version KWP2000: $21 ReadDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $A0 MOSTVersion MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| TRANSCEIVER_VERSION | string | Version des MOST Transceivers |
| NETSERVICES_VERSION | string | Version der Oasis NetServices |
| NETSERVICES_REVISION | string | Revision der Oasis NetServices |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-most-3db"></a>
### STATUS_MOST_3DB

Auslesen des Status der Lichtleistungsabsenkung KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AF OpticalTransmitPowSwitch MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MOST_3DB | int | Status der Lichtleistungsabsenkung 0 = Lichtleistung abgesenkt 1 = Volle Lichtleistung 5s nach Absenkung wird die volle Lichtleistung wieder aktiv |
| STAT_MOST_3DB_TEXT | string | Status der Lichtleistungsabsenkung als Text |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-3db"></a>
### STEUERN_MOST_3DB

Lichtleistungsabsenkung einschalten KWP2000: $3B WriteDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AF OpticalTransmitPowSwitch $00 S1 geoeffnet = 3dB Absenkung MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT Nach 5s wieder volle Lichtleistung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wake-up-status"></a>
### STATUS_WAKE_UP_STATUS

Auslesen des Status WakeupStatus KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD WakeUpStatus MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WAKE_UP_STATUS | int | Status ob Device geweckt hat oder geweckt wurde 0 = nicht initialisiert 1 = SG hat geweckt 2 = SG wurde geweckt |
| STAT_WAKE_UP_STATUS_TEXT | string | Status ob Device geweckt hat oder geweckt wurde als Text |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ability-to-wake"></a>
### STATUS_ABILITY_TO_WAKE

Auslesen des Status AbilityToWake KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD WakeUpStatus MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ABILITY_TO_WAKE | int | Status ob Device wecken darf 0 = off 1 = on 2 = critical |
| STAT_ABILITY_TO_WAKE_TEXT | string | Status ob Device wecken darf als Text |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ability-to-wake"></a>
### STEUERN_ABILITY_TO_WAKE

AbilityToWake einstellen KWP2000: $3B WriteDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD AbilityToWake $00 of, $01 on, $02 critical MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter AbilityToWake Modus table  AbilityToWake Status Defaultwert: DEFAULT 00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mpc-pwm"></a>
### _STATUS_MPC_PWM

PWM-Ports des MPC 555 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $90 $01 xxh xx: Portnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PWM_STROMBLAU_WERT | real | PWM-Signal blaue LED-Ketten |
| STAT_PWM_STROMBLAU_EINH | string | Prozent |
| STAT_PWM_STROMGRUEN_WERT | real | PWM-Signal blaue LED-Ketten |
| STAT_PWM_STROMGRUEN_EINH | string | Prozent |
| STAT_PWM_STROMROT_WERT | real | PWM-Signal rote LED-Ketten |
| STAT_PWM_STROMROT_EINH | string | Prozent |
| STAT_PWM_ROT_WERT | real | PWM-Signal rote LED-Ketten |
| STAT_PWM_ROT_EINH | string | Prozent |
| STAT_PWM_GRUEN_WERT | real | PWM-Signal gruene LED-Ketten |
| STAT_PWM_GRUEN_EINH | string | Prozent |
| STAT_PWM_BLAU_WERT | real | PWM-Signal blaue LED-Ketten |
| STAT_PWM_BLAU_EINH | string | Prozent |
| STAT_COMLVL_ADJUST_WERT | real | PWM-Signal ComLevel Adjust |
| STAT_COMLVL_ADJUST_EINH | string | Prozent |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mpc-adc"></a>
### _STATUS_MPC_ADC

ADC-Kanäle des MPC 555 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $91 $01 $xx xx: Kanalnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TASTER_WERT | real | Taster ein/aus |
| STAT_TASTER_EINH | string | Volt |
| STAT_LED_TEMP_WERT | real | Temperatur LED Array |
| STAT_LED_TEMP_EINH | string | Volt |
| STAT_KL30G_WERT | real | Versorgungsspannung Klemme 30 g |
| STAT_KL30G_EINH | string | Volt |
| STAT_ENABLE_BACKLIGHT_WERT | real | Enable Backlight Wert &lt;  1,0 V : disabled Wert &gt;= 4,5 V : enabled |
| STAT_ENABLE_BACKLIGHT_EINH | string | Volt |
| STAT_LED_KETTEN_ROT_WERT | real | LED-Ketten rot Wert &lt;  1,0 V : Fehler Wert &gt;= 1,0 V : i.O. |
| STAT_LED_KETTEN_ROT_EINH | string | Volt |
| STAT_LED_KETTEN_GRUEN_WERT | real | LED-Ketten gruen Wert &lt;  1,0 V : Fehler Wert &gt;= 1,0 V : i.O. |
| STAT_LED_KETTEN_GRUEN_EINH | string | Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mpc-mdasm"></a>
### _STATUS_MPC_MDASM

MDASM-Kanäle des MPC 555 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $92 $01 $xx xx: Portnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MOST_POWER | int | MOST Sendeleistung 0: reduziert 1: volle Leistung |
| STAT_MOST_RESET | int | MOST Reset 0: Reset 1: kein Reset |
| STAT_ENABLE_VCC_DISPLAY | int | Enable VCC Display 0: deaktiviert 1: aktiviert |
| STAT_ENABLE_BACKLIGHT | int | Enable Backlight 0: deaktiviert 1: aktiviert |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mpc-io"></a>
### _STATUS_MPC_IO

I/O-Ports des MPC 555 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $93 $01 $xx xx: Portnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DEBUGGER_1 | int | Debugger Port 1 0: abgeschaltet 1: eingeschaltet |
| STAT_DEBUGGER_2 | int | Debugger Port 2 0: abgeschaltet 1: eingeschaltet |
| STAT_OUT_CAN_TRANSCEIVER_1 | int | CAN Transceiver 1 0: abgeschaltet 1: eingeschaltet |
| STAT_OUT_CAN_TRANSCEIVER_2 | int | CAN Transceiver 2 0: abgeschaltet 1: eingeschaltet |
| STAT_OUT_PRG_SPANNUNG_FLASH_INTERN | int | Programmierspannung internes Flash 0: abgeschaltet 1: eingeschaltet |
| STAT_OUT_SELBSTHALTUNG_MPC | int | Selbsthaltung MPC 555 0: abgeschaltet 1: eingeschaltet |
| STAT_OUT_RESET_ASSP | int | Reset ASSP3 0: abgeschaltet 1: eingeschaltet |
| STAT_OUT_PRG_SPANNUNG_ASSP | int | Progammierspannung ASSP3 0: abgeschaltet 1: eingeschaltet |
| STAT_IN_TRANSFER_ACKN | int | Transfer Acknowledge 0: abgeschaltet 1: eingeschaltet |
| STAT_OUT_SDATA_DISP_TIMING | int | SDATA DISP TIMING 0: abgeschaltet 1: eingeschaltet |
| STAT_OUT_ENABLE_DAC | int | ENABLE DAC 0: abgeschaltet 1: eingeschaltet |
| STAT_IN_SCLK_DISP | int | SCLK DISP 0: abgeschaltet 1: eingeschaltet |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-assp-adc"></a>
### _STATUS_ASSP_ADC

ADC-Kanäle des ASSP 3 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $25 $01 $xx 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KL30G_WERT | real | Versorgungsspannung Klemme 30 g |
| STAT_KL30G_EINH | string | VOLT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-assp-io"></a>
### _STATUS_ASSP_IO

I/O-Ports des ASSP 3 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $27 $01 $xx xx: Portnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PORT_0_BI | int | I/O-Port 1 (In) |
| STAT_PORT_1_IN | int | I/O-Port 1 (In) |
| STAT_PORT_2_OUT | int | I/O-Port 2 (Out) |
| STAT_PORT_3_BI | int | I/O-Port 3 (Bidirektional) |
| STAT_PORT_4_BI | int | I/O-Port 4 (Bidirektional) |
| STAT_PORT_5_OUT | int | I/O-Port 5 (Out) |
| STAT_PORT_6_BI | int | I/O-Port 6 (Bidirektional) |
| STAT_PORT_8_BI | int | I/O-Port 8 (Bidrektional) |
| STAT_PORT_9_BI | int | I/O-Port 9 (Bidrektional) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mpc-pwm"></a>
### _STEUERN_MPC_PWM

PWM-Ports des MPC 555 setzen KWP2000: $30 InputOutputControlByLocalIdentifier $90 $07 Anforderung $90 $06 $pp $hh $ll Durchführung $pp: Portnummer $hh: High Byte $ll: Low Byte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PORT | int | Portnummer 0x00: Iref Blau 0x01: Iref Grün 0x02: Lüfter 0x03: Dimmung Grün 0x10: Comlevel Adjust (z.Zt. nicht aktiv) 0x11: Dimmung Blau 0x12: Iref Rot 0x13: Dimmung Rot |
| PWM_LEVEL | real | PWM-Signal (Dezimalwert) in Prozent 0.00 - 100.00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-helligkeit"></a>
### STEUERN_HELLIGKEIT

PWM-Ports der Dimmungswerte des MPC 555 setzen KWP2000: $30 InputOutputControlByLocalIdentifier $90 $07 Anforderung $90 $06 $pp $hh $ll Durchführung $pp: 0x03, 0x11 und 0x13 $hh: High Byte $ll: Low Byte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PWM_LEVEL1 | real | PWM-Signal Grün (Dezimalwert) in Prozent 0.00 - 100.00 |
| PWM_LEVEL2 | real | PWM-Signal Rot (Dezimalwert) in Prozent 0.00 - 100.00 |
| PWM_LEVEL3 | real | PWM-Signal Blau (Dezimalwert) in Prozent 0.00 - 100.00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-helligkeit"></a>
### STATUS_HELLIGKEIT

PWM-Ports der Dimmungswerte des MPC 555 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $90 $01 xxh xx: Portnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PWM_ROT_WERT | real | PWM-Signal rote LED-Ketten |
| STAT_PWM_ROT_EINH | string | Prozent |
| STAT_PWM_GRUEN_WERT | real | PWM-Signal gruene LED-Ketten |
| STAT_PWM_GRUEN_EINH | string | Prozent |
| STAT_PWM_BLAU_WERT | real | PWM-Signal blaue LED-Ketten |
| STAT_PWM_BLAU_EINH | string | Prozent |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-stromwerte"></a>
### STEUERN_STROMWERTE

PWM-Ports der Referenzstromwerte des MPC 555 setzen KWP2000: $30 InputOutputControlByLocalIdentifier $90 $07 Anforderung $90 $06 $pp $hh $ll Durchführung $pp: 0x00, 0x01 und 0x12 $hh: High Byte $ll: Low Byte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PWM_LEVEL1 | real | Strom Grün (Dezimalwert) in Prozent 0.00 - 100.00 |
| PWM_LEVEL2 | real | Strom Rot (Dezimalwert) in Prozent 0.00 - 100.00 |
| PWM_LEVEL3 | real | Strom Blau (Dezimalwert) in Prozent 0.00 - 100.00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-stromwerte"></a>
### STATUS_STROMWERTE

PWM-Ports der Referenzstromwerte des MPC 555 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $90 $01 xxh xx: Portnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PWM_STROMBLAU_WERT | real | PWM-Signal blaue LED-Ketten |
| STAT_PWM_STROMBLAU_EINH | string | Prozent |
| STAT_PWM_STROMGRUEN_WERT | real | PWM-Signal gruene LED-Ketten |
| STAT_PWM_STROMGRUEN_EINH | string | Prozent |
| STAT_PWM_STROMROT_WERT | real | PWM-Signal rote LED-Ketten |
| STAT_PWM_STROMROT_EINH | string | Prozent |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-taster"></a>
### _STEUERN_TASTER

ADC-Kanal 00 des MPC 555 setzen Tasterbetätigung wird simuliert KWP2000: $30 InputOutputControlByLocalIdentifier $90 $07 Anforderung $90 $06 $kk $hh $ll Durchführung $pp: Kanalnummer $hh: High Byte $ll: Low Byte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-taster-stop"></a>
### _STEUERN_TASTER_STOP

ADC-Kanal 00 des MPC 555 setzen Tastersimulation wird beendet KWP2000: $30 InputOutputControlByLocalIdentifier $90 $07 Anforderung $90 $06 $kk $hh $ll Durchführung $pp: Kanalnummer $hh: High Byte $ll: Low Byte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-taster"></a>
### STATUS_TASTER

ADC-Kanal Nr.0 des MPC 555 auslesen 3,3V Taster betätigt 4,2V Taster nicht betätigt 5,0V Taster nicht angeschlossen KWP2000: $30 InputOutputControlByLocalIdentifier $91 $01 $xx xx: Kanalnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TASTER_WERT | real | Taster ein/aus |
| STAT_TASTER_EINH | string | Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-backlight-enable"></a>
### STATUS_BACKLIGHT_ENABLE

ADC-Kanal Nr.3 des MPC 555 auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $91 $01 $xx xx: Kanalnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ENABLE_BACKLIGHT_WERT | real | Enable Backlight Wert &lt;  1,0 V : disabled Wert &gt;= 4,5 V : enabled anderer Wert  : undefined |
| STAT_ENABLE_BACKLIGHT_EINH | string | Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mpc-pwm-stop"></a>
### _STEUERN_MPC_PWM_STOP

Zugriff auf die PWM-Ports des MPC 555 beenden KWP2000: $30 InputOutputControlByLocalIdentifier $90 $00 Keine Argumente erforderlich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mpc-adc"></a>
### _STEUERN_MPC_ADC

ADC-Kanäle des MPC 555 setzen KWP2000: $30 InputOutputControlByLocalIdentifier $90 $07 Anforderung $90 $06 $kk $hh $ll Durchführung $pp: Kanalnummer $hh: High Byte $ll: Low Byte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KANAL | int | Kanalnummer 0x00: Taster Wert &lt; 0,5V : Fehler 0,5V &lt; Wert &lt; 3,0V : betätigt 3,0V &lt; Wert &lt; 4,5V : nicht betätigt 0x01: 0x02: Temperatur LED Array 0x03: Auslesen Enable Backlight Wert &lt;  1,0V : disable Wert &gt;= 4,5V : enable Setzen nur für Entwicklung 0x04: Versorgungsspannung Kl.30g 0x05: Auslesen LED-Ketten rot Wert &lt;  1,0V : Fehler Wert &gt;= 1,0V : i.O. Setzen nur für Entwicklung 0x06: Auslesen LED-Ketten gruen Wert &lt;  1,0V : Fehler Wert &gt;= 1,0V : i.O. Setzen nur für Entwicklung 0x07: 0x08: 0x09: 0x0A: 0x0B: 0x0C: 0x0D: 0x0E: Comlevel (z.Zt. nicht aktiv) |
| SPANNUNG | real | Spannungswert in Volt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mpc-adc-stop"></a>
### _STEUERN_MPC_ADC_STOP

Zugriff auf die ADC-Kanäle des MPC 555 beenden KWP2000: $30 InputOutputControlByLocalIdentifier $91 $00 Keine Argumente erforderlich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mpc-mdasm"></a>
### _STEUERN_MPC_MDASM

MDASM-Kanäle des MPC 555 setzen KWP2000: $30 InputOutputControlByLocalIdentifier $92 $07 Anforderung $92 $06 $kk $ww Durchführung $kk: Kanalnummer $ww: Wert

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KANAL | int | Kanalnummer 0x0C: MOST Sendeleistung 0x0D: Enable VCC Display 0x0E: CS LC12018 0x0F: MOST Reset 0x1B: Enable Backlight |
| WERT | int | Wert, 0 oder 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mpc-mdasm-stop"></a>
### _STEUERN_MPC_MDASM_STOP

Zugriff auf die MDASM des MPC 555 beenden KWP2000: $30 InputOutputControlByLocalIdentifier $92 $00 Keine Argumente erforderlich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mpc-io"></a>
### _STEUERN_MPC_IO

I/O-Ports des MPC 555 setzen KWP2000: $30 InputOutputControlByLocalIdentifier $93 $07 Anforderung $93 $06 $kk $ww Durchführung $kk: Kanalnummer $ww: Wert

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KANAL | int | Kanalnummer 0x00: --- vom Debugger genutzt 0x04: --- vom Debugger genutzt 0x05: OUT CAN Transceiver 0x06: OUT CAN Transceiver 0x07: IN 0x08: OUT Programmierspannung internes Flash 0x09: OUT Selbsthaltung MPC555 0x0A: OUT Reset ASSP3 0x0B: OUT Programmierspannung ASSP3 0x0C: IN  Transfer Acknowledge (Flash EEPROM) 0x0D: OUT SDATA DISP Timing (z.Zt. nicht genutzt) 0x0E: OUT Enable DAC (z.Zt. nicht genutzt) 0x0F: IN  SCLK DIPS  (z.Zt. nicht genutzt) |
| WERT | int | Wert, 0 oder 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mpc-io-stop"></a>
### _STEUERN_MPC_IO_STOP

Zugriff auf die I/O-Ports des MPC 555 beenden KWP2000: $30 InputOutputControlByLocalIdentifier $93 $00 Keine Argumente erforderlich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-testbild"></a>
### STEUERN_TESTBILD

Testbilder anzeigen Zustand ist erst durch Sleep Modus beendet KWP2000: $30 InputOutputControlByLocalIdentifier $FD $06

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BILD_ID | int | Testbildnummer (0x00 .. 0x0D) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-displaybereich"></a>
### _STEUERN_DISPLAYBEREICH

Ausgewählte Displaybereiche ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $FEh 07 Anforderung $FEh 06 $aN $eN $gg $aN: Anfangsadresse $eN: Endadresse $gg: Grauwert

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANFANGSADRESSE | string | Anfangsadresse s. Graphik Bildspeicher 8200000 - 82FF800 Anfangsadresse &lt; Endeadresse |
| ENDEADRESSE | string | Endadresse s. Graphik Bildspeicher 8200000 - 82FF800 Anfangsadresse &lt; Endeadresse |
| GRAUSTUFE | int | Graustufe zulässig 0x00 - 0x0F |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-selbsttest-ein"></a>
### STEUERN_SELBSTTEST_EIN

Selbsttestfunktion des Steuergeräts aktvieren KWP2000: $30 InputOutputControlByLocalIdentifier $26 $06 Keine Argumente erforderlich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-selbsttest-aus"></a>
### STEUERN_SELBSTTEST_AUS

Selbsttest des ASSP3 deaktivieren KWP2000: $30 InputOutputControlByLocalIdentifier $26 $00 Keine Argumente erforderlich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-assp-io"></a>
### _STEUERN_ASSP_IO

I/O-Ports des ASSP 3 setzen KWP2000: $30 InputOutputControlByLocalIdentifier $27 $07 Anforderung $27 $06 $kk $ww Durchführung $kk: Kanalnummer $ww: Wert

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KANAL | int | Kanalnummer 0x00: Bidirektonal 0x01: In 0x02: Out 0x03: Bidirektonal 0x04: Bidirektonal 0x05: Out 0x06: Bidirektonal 0x08: Bidirektonal 0x09: Bidirektonal |
| WERT | int | Wert, 0 oder 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-assp-io-stop"></a>
### _STEUERN_ASSP_IO_STOP

Zugriff auf die I/O-Ports des ASSP 3 beenden KWP2000: $30 InputOutputControlByLocalIdentifier $27 $00 Keine Argumente erforderlich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vollschritt"></a>
### _STEUERN_VOLLSCHRITT

Vollschritt-Test aktivieren KWP2000: $30 InputOutputControlByLocalIdentifier $FB $07 Anforderung $FB $06 $m1 $m2 $m3 $m4 Durchführung $m1: Schrittmotor 1 $m2: Schrittmotor 2 $m3: Schrittmotor 3 $m4: Schrittmotor 4

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RICHTUNG | int | Drehrichtung für Schrittmotor 0: vorwärts 1: rückwärts |
| PWM_LEVEL | real | PMW-Signal für Schrittmotor Angabe in % 0.0 - 100.0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-shutter"></a>
### STEUERN_SHUTTER

Shutter auf oder zu fahren KWP2000: $30 InputOutputControlByLocalIdentifier $FB $07 Anforderung $FB $06 $m1 $m2 $m3 $m4 Durchführung $m1: Schrittmotor 1 $m2: Schrittmotor 2 $m3: Schrittmotor 3 $m4: Schrittmotor 4

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RICHTUNG | int | Drehrichtung für Schrittmotor 0: Shutter zu 1: Shutter auf |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vollschritt-stop"></a>
### _STEUERN_VOLLSCHRITT_STOP

Vollschritt-Test beenden KWP2000: $30 InputOutputControlByLocalIdentifier $FB $00 Keine Argumente erforderlich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mikroschritt-stop"></a>
### _STEUERN_MIKROSCHRITT_STOP

Schrittmotor in Ausgangsposition zurückstellen KWP2000: $30 InputOutputControlByLocalIdentifier $20 $00 Keine Argumente erforderlich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mikroschritt"></a>
### _STEUERN_MIKROSCHRITT

Schrittmotor um vorgegebenen Winkel vorwärts bewegen. KWP2000: $30 InputOutputControlByLocalIdentifier $20 $07 Anforderung $20 $06 $hh $$ll Durchführung $hh: High Byte $ll: Low Byte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHRITTANZAHL | real | Anzahl der Mikroschritte für Schrittmotor 100 - 65535 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-array-temperatur"></a>
### STATUS_ARRAY_TEMPERATUR

Temperatur des LED Arrays auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LED_TEMP_WERT | real | Temperatur LED Array |
| STAT_LED_TEMP_EINH | string | Grad Celsius |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klemmen"></a>
### STATUS_KLEMMEN

Klemmenstatus auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KL_R | string | Status Klemme R EIN oder AUS |
| STAT_KL_15 | string | Status Klemme 15 EIN oder AUS |
| STAT_KL_50 | string | Status Klemme 50 EIN oder AUS |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bordnetzspannung"></a>
### STATUS_BORDNETZSPANNUNG

Bordnetzspannung über AD-Kanal 4 des MPC auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $91 $01 $04

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BORDNETZSPANNUNG_WERT | real | Bordnetzspannung |
| STAT_BORDNETZSPANNUNG_EINH | string | Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-energiesparmodus"></a>
### STATUS_ENERGIESPARMODUS

Aktivierten Energiesparmodus auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ENERGIESPARMODE | string | Status Energiesparmodus table EnergySaveMode |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-shackhartmann-tester"></a>
### _STATUS_SHACKHARTMANN_TESTER

Auslesen des Steuergeraete-Speichers KWP 2000: $23 ReadMemoryByAddress Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BYTE_01 | unsigned char | ausgelesenes Byte |
| BYTE_02 | unsigned char | ausgelesenes Byte |
| BYTE_03 | unsigned char | ausgelesenes Byte |
| BYTE_04 | unsigned char | ausgelesenes Byte |
| BYTE_05 | unsigned char | ausgelesenes Byte |
| BYTE_06 | unsigned char | ausgelesenes Byte |
| BYTE_07 | unsigned char | ausgelesenes Byte |
| BYTE_08 | unsigned char | ausgelesenes Byte |
| BYTE_09 | unsigned char | ausgelesenes Byte |
| BYTE_0A | unsigned char | ausgelesenes Byte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-steuergeraete-reset"></a>
### STEUERN_STEUERGERAETE_RESET

Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hud"></a>
### _STATUS_HUD

Status HUD auslesen Prüft, ob Display EIN oder AUS ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HUD | string | Status DISPLAY EIN oder AUS |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (76 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FORTTEXTE](#table-forttexte) (39 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (7 × 3)
- [LEERUW_7](#table-leeruw-7) (1 × 8)
- [LEERUW_6](#table-leeruw-6) (1 × 7)
- [LEERUW_5](#table-leeruw-5) (1 × 6)
- [LEERUW_4](#table-leeruw-4) (1 × 5)
- [LEERUW_3](#table-leeruw-3) (1 × 4)
- [LEERUW_2](#table-leeruw-2) (1 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (39 × 5)
- [LEDFARBE](#table-ledfarbe) (4 × 2)
- [CDBERROR](#table-cdberror) (3 × 2)
- [STATUSKOMBI](#table-statuskombi) (32 × 2)
- [ANZEIGEACC](#table-anzeigeacc) (16 × 2)
- [CCMELDUNG](#table-ccmeldung) (4 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (22 × 9)
- [IORTTEXTE](#table-iorttexte) (9 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (6 × 2)
- [MOST_UW](#table-most-uw) (1 × 4)
- [IUMWELTMATRIX](#table-iumweltmatrix) (9 × 5)
- [RAMSTATUS](#table-ramstatus) (3 × 2)
- [IUMWELTTEXTE](#table-iumwelttexte) (12 × 9)
- [ABILITY_TO_WAKE](#table-ability-to-wake) (4 × 2)
- [MOST_3DB](#table-most-3db) (3 × 2)
- [WAKE_UP_STATUS](#table-wake-up-status) (4 × 2)
- [TEMPLEDARRAY](#table-templedarray) (52 × 2)
- [KLEMMENSTATUS](#table-klemmenstatus) (3 × 2)
- [DISPLAYSTATUS](#table-displaystatus) (3 × 2)
- [ENERGYSAVEMODE](#table-energysavemode) (5 × 2)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 2 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0C | KWP2000 |

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

<a id="table-speichersegment"></a>
### SPEICHERSEGMENT

Dimensions: 12 rows × 3 columns

| SEG_BYTE | SEG_NAME | SEG_TEXT |
| --- | --- | --- |
| 0x00 | LAR | linearAdressRange |
| 0x01 | ROMI | ROM / EPROM, internal |
| 0x02 | ROMX | ROM / EPROM, external |
| 0x03 | NVRAM | NV-RAM (characteristic zones, DTC memory |
| 0x04 | RAMIS | RAM, internal (short MOV) |
| 0x05 | RAMXX | RAM, external (x data MOV) |
| 0x06 | FLASH | Flash EPROM, internal |
| 0x07 | UIFM | User Info Field Memory |
| 0x08 | VODM | Vehicle Order Data Memory |
| 0x09 | FLASHX | Flash EPROM, external |
| 0x0B | RAMIL | RAM, internal (long MOV / Register) |
| 0xFF | ??? | unbekanntes Speichersegment |

<a id="table-iarttexte"></a>
### IARTTEXTE

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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 39 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xA4E8 | Schalter (ein/aus), Überspannung oder Unterspannung |
| 0xA4E9 | Schaltregler NT LED Array |
| 0xA4EA | Backlight LED |
| 0xA4EB | Bordnetzspannung, Überspannung oder Unterspannung |
| 0xA4EC | Temperaturfühler LED |
| 0xA4ED | Interner Fotosensor |
| 0xA4EE | Kommunikation Master - Slave gestört |
| 0xA4EF | EEPROM - Kodierdatenfehler VDO |
| 0xA4F0 | EEPROM - Kodierdatenfehler BMW |
| 0xA4F1 | CAN: No ID |
| 0xA4F2 | CAN: Ausfall Telegramm Klemmenstatus |
| 0xA4F3 | CAN: Ausfall/Fehler Telegramm Anzeige ACC |
| 0xA4F4 | CAN: Ausfall Telegramm Geschwindigkeit |
| 0xA4F5 | CAN: Ausfall/Fehler Telegramm Status Kombi |
| 0xA4F6 | CAN: Ausfall Telegramm Regelgeschwindigkeit Stufentempomat |
| 0xA4F7 | CAN: Ausfall Telegramm LCD Leuchtdichte |
| 0xA4F8 | CAN: Ausfall Telegramm Einheiten |
| 0xA4F9 | CAN: Ausfall Telegramm Status Fahrlicht |
| 0xA4FA | CAN: Ausfall Telegramm Kilometer/Reichweite |
| 0xA4FB | CAN: Ausfall/Fehler Telegramm Anzeigesteuerung CC-Meldung |
| 0xA4FC | CAN: Ausfall Telegramm Status Bordcomputer |
| 0xA4FD | CAN: Ausfall Telegramm Anzeige Kombi/Externe Anzeige |
| 0xA4FE | CAN: physikalischer Fehler EIN |
| 0xA4FF | CAN: Senden misslungen |
| 0xA500 | CAN: kein Acknowledge |
| 0xA501 | CAN: Bus off |
| 0xA502 | CAN: Signal ungültig |
| 0xA503 | CAN: Ausfall Telegramm Personalisierung Erweitert |
| 0xA504 | CAN: Ausfall Telegramm Personalisierung Standard |
| 0xA505 | CAN: No Answer to Request (580h+3Dh) |
| 0xA506 | Energiesparmode aktiv |
| 0xD844 | CAN: Low |
| 0xD847 | CAN: Bus off oder dual ported RAM |
| 0xD84D | Weckendes Device hat 3 mal erfolglos versucht das Netzwerk zu wecken. (Error_WakeUp_Failed). |
| 0xD84E | Obwohl Shutdown(Execute) geschickt wurde, ging das Licht nicht aus. (Error_Light_Not_Off). |
| 0xD850 | Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose). |
| 0xD851 | Lange und/oder haeufige Unlocks (Error_Unlock_Long). |
| 0xD852 | Ein Device hat sich wegen Uebertemperatur abgeschaltet (Error_Temp_Shutdown). |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 7 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxx00xx | 20 | Text a |
| xxxx01xx | 21 | Text b |
| xxxx10xx | 22 | Text c |
| xxxx11xx | 23 | Text d |
| xxxxxx01 | 11 | Text x |
| xxxxxx10 | 12 | Text y |
| xxxxxxxx | 0 | -- |

<a id="table-leeruw-7"></a>
### LEERUW_7

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0xAA | 0xAA | 0xAA | 0xAA | 0xAA | 0xAA | 0xAA |

<a id="table-leeruw-6"></a>
### LEERUW_6

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0xAA | 0xAA | 0xAA | 0xAA | 0xAA | 0xAA |

<a id="table-leeruw-5"></a>
### LEERUW_5

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0xAA | 0xAA | 0xAA | 0xAA | 0xAA |

<a id="table-leeruw-4"></a>
### LEERUW_4

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0xAA | 0xAA | 0xAA | 0xAA |

<a id="table-leeruw-3"></a>
### LEERUW_3

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0xAA | 0xAA | 0xAA |

<a id="table-leeruw-2"></a>
### LEERUW_2

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0xAA | 0xAA |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 39 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xA4E8 | 0x02 | 0x0B | 0x01 | 0xAA |
| 0xA4E9 | 0x02 | 0x0B | 0x01 | 0xAA |
| 0xA4EA | 0x02 | 0x0B | 0x01 | 0x03 |
| 0xA4EB | 0x02 | 0x0B | 0x01 | 0xAA |
| 0xA4EC | 0x02 | 0x0B | 0x01 | 0xAA |
| 0xA4ED | 0x02 | 0x0B | 0x01 | 0xAA |
| 0xA4EE | 0x02 | 0x0B | 0x01 | 0xAA |
| 0xA4EF | 0x02 | 0x01 | 0x04 | LeerUW_2 |
| 0xA4F0 | 0x02 | 0x01 | 0x04 | LeerUW_2 |
| 0xA4F1 | 0x01 | LeerUW_5 | - | - |
| 0xA4F2 | 0x01 | LeerUW_5 | - | - |
| 0xA4F3 | 0x01 | 0x13 | LeerUW_4 | - |
| 0xA4F4 | 0x01 | LeerUW_5 | - | - |
| 0xA4F5 | 0x01 | 0x12 | LeerUW_4 | - |
| 0xA4F6 | 0x01 | LeerUW_5 | - | - |
| 0xA4F7 | 0x01 | LeerUW_5 | - | - |
| 0xA4F8 | 0x01 | LeerUW_5 | - | - |
| 0xA4F9 | 0x01 | LeerUW_5 | - | - |
| 0xA4FA | 0x01 | LeerUW_5 | - | - |
| 0xA4FB | 0x01 | 0x14 | LeerUW_4 | - |
| 0xA4FC | 0x01 | LeerUW_5 | - | - |
| 0xA4FD | 0x01 | LeerUW_5 | - | - |
| 0xA4FE | 0x01 | 0x0D | LeerUW_4 | - |
| 0xA4FF | 0x01 | 0x0E | LeerUW_4 | - |
| 0xA500 | 0x01 | 0x0F | LeerUW_4 | - |
| 0xA501 | 0x01 | 0x10 | LeerUW_4 | - |
| 0xA502 | 0x01 | 0x11 | LeerUW_4 | - |
| 0xA503 | 0x01 | LeerUW_5 | - | - |
| 0xA504 | 0x01 | LeerUW_5 | - | - |
| 0xA505 | 0x0C | LeerUW_5 | - | - |
| 0xA506 | LeerUW_3 | LeerUW_3 | - | - |
| 0xD844 | 0x01 | LeerUW_7 | - | - |
| 0xD847 | 0x01 | LeerUW_7 | - | - |
| 0xD84D | 0x01 | LeerUW_7 | - | - |
| 0xD84E | 0x01 | LeerUW_7 | - | - |
| 0xD850 | 0x01 | 0xAA | 0x09 | LeerUW_4 |
| 0xD851 | 0x01 | LeerUW_7 | - | - |
| 0xD852 | 0x01 | LeerUW_7 | - | - |
| default | 0x01 | - | - | - |

<a id="table-ledfarbe"></a>
### LEDFARBE

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | rot |
| 0x02 | gruen |
| 0x03 | blau |
| XY | Farbe unplausibel |

<a id="table-cdberror"></a>
### CDBERROR

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Unkritisch |
| 0x01 | Kritisch |
| XY | Kritikalität unplausibel |

<a id="table-statuskombi"></a>
### STATUSKOMBI

Dimensions: 32 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Timeout |
| 0x02 | Checksum |
| 0x03 | Timeout und Checksum |
| 0x04 | Fehler Alive-Zähler |
| 0x05 | Timeout und Alive-Zähler |
| 0x06 | Checksum und Alive-Zähler |
| 0x07 | Timeout, Checksum und Alive-Zähler |
| 0x08 | Fehler Schnittstelle ACC/Kombi |
| 0x09 | Timeout und Schnittstelle ACC/Kombi |
| 0x0A | Checksum und Schnittstelle ACC/Kombi |
| 0x0B | Timeout, Checksum, Schnittstelle ACC/Kombi |
| 0x0C | Alive-Zähler und Schnittstelle ACC/Kombi |
| 0x0D | Timeout, Alive-Zähler, Schnittstelle ACC/Kombi |
| 0x0E | Checksum, Alive-Zähler, Schnittstelle ACC/Kombi |
| 0x0F | Timeout, Checksum, Alive-Zähler, Schnittstelle ACC/Kombi |
| 0x10 | ungültige Geschwindigkeit |
| 0x11 | Timeout, ungültige Geschwindigkeit |
| 0x12 | Checksum, ungültige Geschwindigkeit |
| 0x13 | Timeout, Checksum und ungültige Geschwindigkeit |
| 0x14 | Fehler Alive-Zähler und Ungült.Geschwindigkeit |
| 0x15 | Timeout, Alive-Zähler, Ungült.Geschwindigkeit |
| 0x16 | Checksum, Alive-Zähler, Ungült.Geschwindigkeit |
| 0x17 | Timeout, Checksum, Alive, Ungült.Geschwindigkeit |
| 0x18 | Fehler Schnittstelle ACC/Kombi, Ungült.Geschwindigkeit |
| 0x19 | Timeout, Schnittstelle ACC/Kombi, Ungült.Geschwindigkeit |
| 0x1A | Checksum, Schnittstelle ACC/Kombi, Ungült.Geschwindigkeit |
| 0x1B | Timeout, Checksum, Schnittst. ACC/KI, ungült.Geschwindigkeit |
| 0x1C | Alive, Schnittst. ACC/Kombi, ungült.Geschwindigkeit |
| 0x1D | Timeout, Alive, Schnittst. ACC/KI, ungült.Geschwindigkeit |
| 0x1E | Checksum, Alive, Schnittst. ACC/KI,ungült.Geschwindigkeit |
| 0x1F | Timeout,Checksum,Alive,Schnittst. ACC/KI,ungül.Geschwindigkeit |
| XY | Status Kombi unplaubsibel |

<a id="table-anzeigeacc"></a>
### ANZEIGEACC

Dimensions: 16 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Timeout |
| 0x02 | Checksum |
| 0x03 | Timeout und Checksum |
| 0x04 | Fehler im Alive-Zähler |
| 0x05 | Timeout und Alive-Zähler |
| 0x06 | Checksum und Alive-Zähler |
| 0x07 | Timeout, Checksum und Alive-Zähler |
| 0x08 | Ungueltiger oder Reserve-Wert |
| 0x09 | Timeout und ungueltiger/Reserve-Wert |
| 0x0A | Checksum und ungueltiger/Reserve-Wert |
| 0x0B | Timeout, Checksum und unguelt./Reserve-Wert |
| 0x0C | Alive-Zähler und ungueltiger/Reserve-Wert |
| 0x0D | Timeout,Alive-Zähler und ungül./Reserve-Wert |
| 0x0E | Checksum, Alive-Zähler, unguelt./Reserve-Wert |
| 0x0F | Timeout,Checksum, Alive, ungül./Reserve-Wert |
| XY | Anzeige ACC unplaubsibel |

<a id="table-ccmeldung"></a>
### CCMELDUNG

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Timeout |
| 0x02 | Textupdate ungueltig |
| 0x03 | Timeout und Textupdate ungueltig |
| XY | CC Meldung unplaubsibel |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 22 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Bordnetzspannung | Volt | -- | unsigned char | -- | 1 | 10 | 0 |
| 0x02 | Betriebsdauer | Stunden | H | unsigned int | -- | 1 | 1 | 0 |
| 0x03 | LED Kette | 0-n | -- | 0xFF | LEDFarbe | 1 | 1 | 0 |
| 0x04 | Codierdatenfehler | 0-n | -- | 0xFF | CDBError | 1 | 1 | 0 |
| 0x05 | Geräteadresse NAK | Hex | H | unsigned int | -- | 1 | 1 | 0 |
| 0x06 | Funktionsblock | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x07 | Instanz ID | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x08 | Funktions ID | Hex | H | unsigned int | -- | 1 | 1 | 0 |
| 0x09 | Position Node Register | Hex | H | unsigned int | -- | 1 | 1 | 0 |
| 0x0A | Geräteadresse | Hex | H | unsigned int | -- | 1 | 1 | 0 |
| 0x0B | Temperatur LED Array | Grad C | H | signed int | -- | 1 | 1 | 0 |
| 0x0C | Anfrage ID | Hex | H | unsigned int | -- | 1 | 1 | 0 |
| 0x0D | Physikalischer Fehler | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x0E | Senden misslungen | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x0F | Kein Acknowledge | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x10 | Bus off | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x11 | Signal ungültig | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x12 | Status Kombi | 0-n | -- | 0xFF | StatusKombi | 1 | 1 | 0 |
| 0x13 | Anzeige ACC | 0-n | -- | 0xFF | AnzeigeACC | 1 | 1 | 0 |
| 0x14 | CC Meldung | 0-n | -- | 0xFF | CCMeldung | 1 | 1 | 0 |
| 0xAA | ohne Bedeutung | Hex | -- | unsigned char | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 9 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9308 | Device bekam Reset (Error_Reset). |
| 0x930A | Device ist im Zustand Normal Operation und das Licht am Eingang geht ohne Vorankuendigung aus (Error_Sudden_light_off). |
| 0x930B | Anfragendes Device bekommt keine Antwort obwohl Partner vorhanden ist (Error_Device_No_Answer). |
| 0x930C | Kurze Unlocks (Error_Unlock_Short). |
| 0x930D | Kein Broadcast Configuration(Status) vom Networkmaster erhalten (Error_t_CfgStatus). |
| 0x9310 | Empfaenger hat eine Nachricht nicht abgenommen (Error_NAK). |
| 0x9400 | Helligkeitsreduzierung aufgrund zu niedriger Bordnetzspannung |
| 0x9401 | Helligkeitsreduzierung aufgrund zu hoher LED Array Temperatur |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-most-uw"></a>
### MOST_UW

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x04 | 0x05 | 0x06 |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 9 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9308 | 0x01 | 0x02 | LeerUW_6 | - |
| 0x930A | 0x01 | LeerUW_7 | - | - |
| 0x930B | 0x01 | 0xAA | 0x08 | MOST_UW |
| 0x930C | 0x01 | LeerUW_7 | - | - |
| 0x930D | 0x01 | LeerUW_7 | - | - |
| 0x9310 | 0x01 | 0xAA | 0x03 | MOST_UW |
| 0x9400 | 0x09 | 0x0A | 0x01 | LeerUW_3 |
| 0x9401 | 0x09 | 0x0A | 0x01 | LeerUW_3 |
| default | 0x01 | - | - | - |

<a id="table-ramstatus"></a>
### RAMSTATUS

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | RAM Verlust |
| 0x01 | RAM Erhalt |
| YX | unplausibler RAM Status |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 12 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Bordnetzspannung | Volt | -- | unsigned char | -- | 1 | 10 | 0 |
| 0x02 | Reset mit | 0-n | -- | 0xFF | RAMStatus | 1 | 1 | 0 |
| 0x03 | Geräteadresse NAK | Hex | H | unsigned int | -- | 1 | 1 | 0 |
| 0x04 | Funktionsblock | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x05 | Instanz ID | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x06 | Funktions ID | Hex | H | unsigned int | -- | 1 | 1 | 0 |
| 0x07 | Position Node Register | Hex | H | unsigned int | -- | 1 | 1 | 0 |
| 0x08 | Geräteadresse | Hex | H | unsigned int | -- | 1 | 1 | 0 |
| 0x09 | Betriebsdauer | Stunden | H | unsigned int | -- | 1 | 1 | 0 |
| 0x0A | Temperatur LED Array | Grad C | H | signed int | -- | 1 | 1 | 0 |
| 0xAA | ohne Bedeutung | Hex | - | unsigned char | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-ability-to-wake"></a>
### ABILITY_TO_WAKE

Dimensions: 4 rows × 2 columns

| ABILITY_TO_WAKE_NR | ABILITY_TO_WAKE_MODE |
| --- | --- |
| 0x00 | off |
| 0x01 | on |
| 0x02 | critical |
| 0xXY | unbekannter Mode |

<a id="table-most-3db"></a>
### MOST_3DB

Dimensions: 3 rows × 2 columns

| MOST_3DB_NR | MOST_3DB_MODE |
| --- | --- |
| 0x00 | Lichtleistung abgesenkt |
| 0x01 | Volle Lichtleistung |
| 0xXY | unbekannter Mode |

<a id="table-wake-up-status"></a>
### WAKE_UP_STATUS

Dimensions: 4 rows × 2 columns

| WAKE_UP_STATUS_NR | WAKE_UP_STATUS_MODE |
| --- | --- |
| 0x00 | nicht initialisiert |
| 0x01 | SG hat geweckt |
| 0x02 | SG wurde geweckt |
| 0xXY | unbekannter Mode |

<a id="table-templedarray"></a>
### TEMPLEDARRAY

Dimensions: 52 rows × 2 columns

| SPANNUNG | TEMPERATUR |
| --- | --- |
| 50 | -39 |
| 49 | -39 |
| 48 | -32 |
| 47 | -25 |
| 46 | -22 |
| 45 | -18 |
| 44 | -15 |
| 43 | -11 |
| 42 | -9 |
| 41 | -4 |
| 40 | -1 |
| 39 | 1 |
| 38 | 2 |
| 37 | 4 |
| 36 | 6 |
| 35 | 8 |
| 34 | 10 |
| 33 | 12 |
| 32 | 14 |
| 31 | 16 |
| 30 | 18 |
| 29 | 20 |
| 28 | 22 |
| 27 | 23 |
| 26 | 24 |
| 25 | 25 |
| 24 | 27 |
| 23 | 30 |
| 22 | 32 |
| 21 | 35 |
| 20 | 37 |
| 19 | 40 |
| 18 | 42 |
| 17 | 45 |
| 16 | 47 |
| 15 | 50 |
| 14 | 52 |
| 13 | 55 |
| 12 | 57 |
| 11 | 60 |
| 10 | 62 |
| 9 | 65 |
| 8 | 67 |
| 7 | 69 |
| 6 | 71 |
| 5 | 78 |
| 4 | 85 |
| 3 | 95 |
| 2 | 101 |
| 1 | 115 |
| 0 | 115 |
| 0xXY | unbekannte Temperatur |

<a id="table-klemmenstatus"></a>
### KLEMMENSTATUS

Dimensions: 3 rows × 2 columns

| WERT | STATUS |
| --- | --- |
| 0x00 | AUS |
| 0x01 | EIN |
| 0xXY | unbekannter Klemmenstatus |

<a id="table-displaystatus"></a>
### DISPLAYSTATUS

Dimensions: 3 rows × 2 columns

| WERT | STATUS |
| --- | --- |
| 0x00 | AUS |
| 0x01 | EIN |
| 0xXY | unbekannter Displaystatus |

<a id="table-energysavemode"></a>
### ENERGYSAVEMODE

Dimensions: 5 rows × 2 columns

| WERT | MODE |
| --- | --- |
| 0x00 | Kein Energiesparmodus aktiv |
| 0x01 | Fertigungsmodus aktiv |
| 0x02 | Transportmodus aktiv |
| 0x04 | Werkstattmodus aktiv |
| 0xXY | unbekannter Energiesparmodus |
