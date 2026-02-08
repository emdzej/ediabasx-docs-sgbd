# ihkr89.prg

- Jobs: [107](#jobs)
- Tables: [35](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Control Panel IHKR E89 |
| ORIGIN | BMW EI-541 Linnemann Torsten |
| REVISION | 6.110 |
| AUTHOR | Valeo CPD Schmidt, Valeo CPD Trebes, Valeo CPD Brau |
| COMMENT | N/A |
| PACKAGE | 1.52 |
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
- [FS_SPERREN](#job-fs-sperren) - Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
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
- [STATUS_IHX_WERTE](#job-status-ihx-werte) - lesen von IHx relevanten Daten mit dem SGBD-Generator erzeugt
- [STATUS_TIMER_EINLAUFSCHUTZ](#job-status-timer-einlaufschutz) - lesen der verbleibenden Zeit für Kompressoreinlaufschutz mit dem SGBD-Generator erzeugt
- [STATUS_MOTOR_KLAPPENPOSITION](#job-status-motor-klappenposition) - lesen von Soll- und Ist-Klappenpositionen mit dem SGBD-Generator erzeugt
- [STATUS_KLIMASYSTEM](#job-status-klimasystem) - lesen Status Klimasystem und alller Adressen der LIN-Bus-Motoren mit dem SGBD-Generator erzeugt
- [STATUS_MOTOR_EICHLAUF](#job-status-motor-eichlauf) - lesen Status Motoren-Eichlauf mit dem SGBD-Generator erzeugt
- [STATUS_KLAPPEN_VERSTELLBEREICH](#job-status-klappen-verstellbereich) - Lesen des aktuellen Status der Verstellbereiche alle Motoren ermittelt über den Eichlauf mit dem SGBD-Generator erzeugt
- [STATUS_SENSOREN_ANALOG_PORT](#job-status-sensoren-analog-port) - Auslesen Rohwerte Sensoren mit dem SGBD-Generator erzeugt
- [STATUS_SPANNUNGEN_ANALOG_PORT](#job-status-spannungen-analog-port) - Auslesen Rohwert Batteriespannung mit dem SGBD-Generator erzeugt
- [STATUS_POTI_ANALOG_PORT](#job-status-poti-analog-port) - Auslesen Rohwerte Potentiometer mit dem SGBD-Generator erzeugt
- [STATUS_SZM_ANALOG_PORT](#job-status-szm-analog-port) - Auslesen der Rohwerte SZM-Analogeingänge mit dem SGBD-Generator erzeugt
- [STATUS_DIGITAL_PORT](#job-status-digital-port) - lesen der Digitaleingänge mit dem SGBD-Generator erzeugt
- [STATUS_SZM_VARIANTE](#job-status-szm-variante) - Auslesen der SZM-Variante mit dem SGBD-Generator erzeugt
- [STATUS_CAN_DRUCKSENSORSENSOR](#job-status-can-drucksensorsensor) - Auslesen des aktuellen Wertes des Drucksensors mit dem SGBD-Generator erzeugt
- [STATUS_TASTEN](#job-status-tasten) - aktueller Tasten-Status mit dem SGBD-Generator erzeugt
- [STATUS_FUNKTIONSBELEUCHTUNG](#job-status-funktionsbeleuchtung) - aktueller Status der Funktions-LEDs mit dem SGBD-Generator erzeugt
- [STATUS_SZM_TASTEN](#job-status-szm-tasten) - aktueller Tasten-Status SZM mit dem SGBD-Generator erzeugt
- [STATUS_SZM_FUNKTIONSBELEUCHTUNG](#job-status-szm-funktionsbeleuchtung) - aktueller Status der SZM Funktions-LEDs mit dem SGBD-Generator erzeugt
- [STATUS_PWM_FUNKTIONSBELEUCHTUNG](#job-status-pwm-funktionsbeleuchtung) - aktueller Status Helligkeit (PWM) der Funktionsbeleuchtung mit dem SGBD-Generator erzeugt
- [STATUS_BELEUCHTUNG](#job-status-beleuchtung) - aktueller Status Helligkeit (PWM) der Hintergrundbeleuchtung mit dem SGBD-Generator erzeugt
- [STATUS_DIAGNOSETESTBETRIEB_PERMANENT](#job-status-diagnosetestbetrieb-permanent) - Auslesen Status Diagnose Test Mode permanent mit dem SGBD-Generator erzeugt
- [STATUS_AUTOADRESIERUNG](#job-status-autoadresierung) - Auslesen autoadresierung status von motoren mit dem SGBD-Generator erzeugt
- [STATUS_EINZELADRESIERUNG](#job-status-einzeladresierung) - Auslesen adresierung status von letzte adressierte motor mit dem SGBD-Generator erzeugt
- [STATUS_MOTOR_KLAPPENPOSITION_INKREMENT](#job-status-motor-klappenposition-inkrement) - lesen Inkrement von Soll- und Ist-Klappenpositionen mit dem SGBD-Generator erzeugt
- [STATUS_MOTOR_IDENT](#job-status-motor-ident) - Liefert die Identdaten des jeweiligen LIN-Bus-Schrittmotors (reportCurrentState) KWP2000: $21 ReadDataByLocalIdentifier $xx InputOutputLocalIdetifier LIN-Bus-Teilnehmer Modus  : Default
- [STEUERN_KOMPRESSOR_EINLAUFSCHUTZ](#job-steuern-kompressor-einlaufschutz) - Setzen/Löschen des Kompressor Einlaufschutzes KWP2000: $3B WriteDataByLocalIdentifier $02 Kompressor Einlaufschutz (recordLocalIdentifier) $0x Ein/Aus (recordValue#1) Modus  : Default
- [STEUERN_TASTEN](#job-steuern-tasten) - Ansteuern Tasten KWP2000: $30 InputOutputControlByLocalIdentifier $01 InputOutputLocalIdetifier: Tasten $07 ShortTermAdjustment
- [STEUERN_FUNKTIONSBELEUCHTUNG](#job-steuern-funktionsbeleuchtung) - Ansteuern Funktionsbeleuchtungs-LEDs KWP2000: $30 InputOutputControlByLocalIdentifier $02 LED $07 ShortTermAdjustment
- [STEUERN_SZM_TASTEN](#job-steuern-szm-tasten) - Ansteuern Tasten SZM KWP2000: $30 InputOutputControlByLocalIdentifier $03 Tasten SZM $07 ShortTermAdjustment
- [STEUERN_SZM_FUNKTIONSBELEUCHTUNG](#job-steuern-szm-funktionsbeleuchtung) - Ansteuern SZM Funktionsbeleuchtungs-LEDs KWP2000: $30 InputOutputControlByLocalIdentifier $04 LED SZM $07 ShortTermAdjustment
- [STEUERN_PWM_FUNKTIONSBELEUCHTUNG](#job-steuern-pwm-funktionsbeleuchtung) - Setzen der Helligkeit (PWM) der Funtionsbeleuchtung KWP2000: $30 InputOutputControlByLocalIdentifier $05 PWM LEDs $01 ShortTermAdjustment
- [STEUERN_BELEUCHTUNG](#job-steuern-beleuchtung) - Ansteuern Hintergrundbeleuchtung KWP2000: $30 InputOutputControlByLocalIdentifier $06 LEDs $07 ShortTermAdjustment
- [STEUERN_12V_AUSGANG](#job-steuern-12v-ausgang) - Ansteuern 12V Ausgang (Schrittmotorversorgung) KWP2000: $30 InputOutputControlByLocalIdentifier $07 12V-Ausgang $07 ShortTermAdjustment
- [STEUERN_GEBLAESE](#job-steuern-geblaese) - Ansteuern Geblaese KWP2000: $30 InputOutputControlByLocalIdentifier $08 Geblaese $07 ShortTermAdjustment
- [STEUERN_KLAPPE_ZENTRALANTRIEB](#job-steuern-klappe-zentralantrieb) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $21 InputOutputLocalIdetifier (Zentralantrieb) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_UMLUFT](#job-steuern-klappe-umluft) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $22 InputOutputLocalIdetifier (Umluft) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_MISCHLUFT](#job-steuern-klappe-mischluft) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $23 InputOutputLocalIdetifier (Mischluft) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_CAN_HEIZBARE_HECKSCHEIBE](#job-steuern-can-heizbare-heckscheibe) - Ansteuern Zusatzwasserpumpe ueber CAN KWP2000: $30 InputOutputControlByLocalIdentifier $09 heizbare Heckscheibe $07 ShortTermAdjustment
- [STEUERN_CAN_KOMPRESSOR_VENTIL](#job-steuern-can-kompressor-ventil) - Ansteuern Kompressorventil ueber CAN KWP2000: $30 InputOutputControlByLocalIdentifier $0A Kompressorventil $07 ShortTermAdjustment
- [STEUERN_CAN_KOMPRESSOR_KUPPLUNG](#job-steuern-can-kompressor-kupplung) - Ansteuern Zusatzwasserpumpe ueber CAN KWP2000: $30 InputOutputControlByLocalIdentifier $0B Kompressorkupplung $07 ShortTermAdjustment
- [STEUERN_CAN_ZUSATZWASSERPUMPE](#job-steuern-can-zusatzwasserpumpe) - Ansteuern Zusatzwasserpumpe ueber CAN KWP2000: $30 InputOutputControlByLocalIdentifier $0C Zusatzwasserpumpe $07 ShortTermAdjustment
- [STEUERN_CAN_ELEKTRISCHE_WASSERPUMPE](#job-steuern-can-elektrische-wasserpumpe) - Ansteuern elektrische Wasserpumpe ueber CAN KWP2000: $30 InputOutputControlByLocalIdentifier $0D Kompressorventil $07 ShortTermAdjustment
- [STEUERN_DIAGNOSETESTBETRIEB_PERMANENT](#job-steuern-diagnosetestbetrieb-permanent) - Diagnose Test Mode mit/ohne Timeout-Ueberwachung KWP2000: $30 InputOutputControlByLocalIdentifier $0E DIAG_PERMANENT $07 ShortTermAdjustment
- [STEUERN_RETURN_ECU_CONTROL](#job-steuern-return-ecu-control) - Ruecksetzen Diagnose Test Mode KWP2000: $30 InputOutputControlByLocalIdentifier $00 ReturnControlToECU
- [STEUERN_MOTOREN_EICHLAUF](#job-steuern-motoren-eichlauf) - Löst Klappeneichlauf aus und kalibriert die Schrittzahlen neu KWP2000: $31 StartRoutineByLocalIdetifier $20 routineLocalIdentifier Klappenmotoreneichlauf Modus  : Default
- [STEUERN_AUTOADRESSIERUNG](#job-steuern-autoadressierung) - Startet die LIN-Bus Autoadressierung KWP2000: $31 StartRoutineByLocalIdetifier $22 routineLocalIdentifier LIN-Bus Autoadressierung Modus  : Default
- [STEUERN_EINZELADRESSIERUNG](#job-steuern-einzeladressierung) - Startet die LIN-Bus Einzeladressierung KWP2000: $31 StartRoutineByLocalIdetifier $23 routineLocalIdentifier LIN-Bus Einzeladressierung Modus  : Default
- [STEUERN_SETZEN_DEFAULT_WERTE_ALLE_SCHLUESSEL](#job-steuern-setzen-default-werte-alle-schluessel) - Setzt alle Schlüssel auf Default-Werte KWP2000: $31 StartRoutineByLocalIdetifier $26 routineLocalIdentifier LIN-Bus Autoadressierung Modus  : Default
- [STEUERN_DIAGNOSEBIT_LOESCHEN](#job-steuern-diagnosebit-loeschen) - Rücksetzen der I/O-Port-Diagnosebits (returnControlToECU) KWP2000: $30 InputOutputControlByLocalIdentifier $xx InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) $00 returnControlToECU Modus  : Default
- [STEUERN_SECURITY_ACCESS_AUFTRAG](#job-steuern-security-access-auftrag) - Zugang mit Security Access 
- [STEUERN_POTI_KALIBRIERUNG_LINKS_FUSS](#job-steuern-poti-kalibrierung-links-fuss) - Kalibierung Drehsteller links fuss. KWP2000: $31 StartRoutineByLocalIdetifier $11 routineLocalIdentifier Potentiometer links fuss. Modus  : Default
- [STEUERN_POTI_KALIBRIERUNG_LINKS_DEF](#job-steuern-poti-kalibrierung-links-def) - Kalibierung Drehsteller links defrost. KWP2000: $31 StartRoutineByLocalIdetifier $15 routineLocalIdentifier Potentiometer links defrost. Modus  : Default
- [STEUERN_POTI_KALIBRIERUNG_LINKS_BEL](#job-steuern-poti-kalibrierung-links-bel) - Kalibierung Drehsteller links beluftung. KWP2000: $31 StartRoutineByLocalIdetifier $12 routineLocalIdentifier Potentiometer links beluftung. Modus  : Default
- [STEUERN_POTI_KALIBRIERUNG_RECHTS_MIN](#job-steuern-poti-kalibrierung-rechts-min) - Kalibierung Drehsteller rechts min. KWP2000: $31 StartRoutineByLocalIdetifier $13 routineLocalIdentifier Potentiometer rechts min. Modus  : Default
- [STEUERN_POTI_KALIBRIERUNG_RECHTS_MAX](#job-steuern-poti-kalibrierung-rechts-max) - Kalibierung Drehsteller rechts max. KWP2000: $31 StartRoutineByLocalIdetifier $14 routineLocalIdentifier Potentiometer rechts max. Modus  : Default
- [STEUERN_EEPROM_RESET](#job-steuern-eeprom-reset) - Startet RESET des EEPROM-Inhalts KWP2000: $31 StartRoutineByLocalIdetifier $25 routineLocalIdentifier EEPROM reset Modus  : Default
- [STATUS_GEBLAESE](#job-status-geblaese) - aktuelle Ansteuerung Gebläse mit dem SGBD-Generator erzeugt
- [STATUS_FASTA_BLOCK](#job-status-fasta-block) - Aktueller Wert des FASTA-Blocks (je 16 Bit) KWP2000: $23 recordCommonIdentifier (High-Byte) $xx recordCommonIdentifier (Low-Byte) (FASTA-Block) Modus  : Default
- [STATUS_BEDIENGERAET](#job-status-bediengeraet) - Fertigungdaten KWP2000: $21 ReadDataByLocalIdentifier $30 LocalIdentifier Modus  : Default

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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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

<a id="job-status-ihx-werte"></a>
### STATUS_IHX_WERTE

lesen von IHx relevanten Daten mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_Y_WERT | real | aktueller Y-Wert Bereich von -128 [%] bis 127 [%] |
| STAT_Y_EINH | string | aktueller Y-Wert Einheit: % |
| STAT_DRUCK_KAELTEMITTEL_WERT | real | aktueller Kältemitteldruck Bereich von 0 [bar] bis 127 [bar] |
| STAT_DRUCK_KAELTEMITTEL_EINH | string | aktueller Kältemitteldruck Einheit: bar |
| STAT_KLEMME_30_WERT | real | aktuelle Versorgungsspannung Bereich von 0 [V] bis 25,5 [V] |
| STAT_KLEMME_30_EINH | string | aktuelle Versorgungsspannung Einheit: V |
| STAT_T_AUSSEN_WERT | real | aktuelle Aussentemperatur Bereich von -40 [°C] bis 85 [°C] |
| STAT_T_AUSSEN_EINH | string | aktuelle Aussentemperatur Einheit: °C |
| STAT_T_VERDAMPFER_WERT | real | aktuelle Verdampfertemperatur Bereich von -40 [°C] bis 105 [°C] |
| STAT_T_VERDAMPFER_EINH | string | aktuelle Verdampfertemperatur Einheit: °C |
| STAT_T_BELUEFTUNG_WERT | real | aktuelle Ausblastemperatur Belüftungsebene Bereich von -40 [°C] bis 105 [°C] |
| STAT_T_BELUEFTUNG_EINH | string | aktuelle Ausblastemperatur Belüftungsebene Einheit: °C |
| STAT_T_FUSSRAUM_WERT | real | aktuelle Ausblastemperatur Fussraumebene Bereich von -40 [°C] bis 105 [°C] |
| STAT_T_FUSSRAUM_EINH | string | aktuelle Ausblastemperatur Fussraumebene Einheit: °C |
| STAT_T_IHX_WERT | real | aktuelle Temperatur IHx (Leiterplatte) Bereich von -40 [°C] bis 105 [°C] |
| STAT_T_IHX_EINH | string | aktuelle Temperatur IHx (Leiterplatte) Einheit: °C |
| STAT_EC_LUEFTER_STUFE_WERT | real | aktuell gesetzte Stufe des EC-Luefters Bereich von 0 [Stufe] bis 14 [Stufe] |
| STAT_EC_LUEFTER_STUFE_EINH | string | aktuell gesetzte Stufe des EC-Luefters Einheit: Stufe |
| STAT_T_SOLLWERT_FA_WERT | real | aktueller Temperatursollwert Bereich von 0 [%] bis 100 [%] |
| STAT_T_SOLLWERT_FA_EINH | string | aktueller Temperatursollwert Einheit: % |
| STAT_LVT_WERT | real | aktuelle Einstellung Luftverteilung Bereich von 0 [°] bis 360 [°] |
| STAT_LVT_EINH | string | aktuelle Einstellung Luftverteilung Einheit: ° |
| STAT_SOLLWERT_GEBLAESE_WERT | real | aktuelle Einstellung Gebläse Bereich von 0 [Stufe] bis 7 [Stufe] |
| STAT_SOLLWERT_GEBLAESE_EINH | string | aktuelle Einstellung Gebläse Einheit: Stufe |
| STAT_TASTER_KULISSENSCHEIBE | int | Status Mikroschalter Kulissenscheibe |
| STAT_KLIMAKOMPRESSOR_EIN | int | aktueller Status Klimafunktion |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-timer-einlaufschutz"></a>
### STATUS_TIMER_EINLAUFSCHUTZ

lesen der verbleibenden Zeit für Kompressoreinlaufschutz mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TIMER_WERT | real | Restlaufzeit für den Kompressoreinlaufschutz in Sekunden Bereich von 0 [s] bis 255 [s] |
| STAT_TIMER_EINH | string | Restlaufzeit für den Kompressoreinlaufschutz in Sekunden Einheit: s |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-klappenposition"></a>
### STATUS_MOTOR_KLAPPENPOSITION

lesen von Soll- und Ist-Klappenpositionen mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ZENTRALANTRIEB_WERT | real | aktuelle Soll-Klappenposition des Zentralantriebmotors Bereich von 0 [%] bis 100 [%] |
| STAT_ZENTRALANTRIEB_EINH | string | aktuelle Soll-Klappenposition des Zentralantriebmotors Einheit: % |
| STAT_ZENTRALANTRIEB_IST_WERT | real | aktuelle Ist-Klappenposition des Zentralantriebmotors Bereich von 0 [%] bis 100 [%] |
| STAT_ZENTRALANTRIEB_IST_EINH | string | aktuelle Ist-Klappenposition des Zentralantriebmotors Einheit: % |
| STAT_FRISCHLUFT_UMLUFT_WERT | real | aktuelle Soll-Klappenposition des Frischluft-Umluft-Motors Bereich von 0 [%] bis 100 [%] |
| STAT_FRISCHLUFT_UMLUFT_EINH | string | aktuelle Soll-Klappenposition des Frischluft-Umluft-Motors Einheit: % |
| STAT_FRISCHLUFT_UMLUFT_IST_WERT | real | aktuelle Ist-Klappenposition des Frischluft-Umluft-Motors Bereich von 0 [%] bis 100 [%] |
| STAT_FRISCHLUFT_UMLUFT_IST_EINH | string | aktuelle Ist-Klappenposition des Frischluft-Umluft-Motors Einheit: % |
| STAT_MISCHLUFT_WERT | real | aktuelle Soll-Klappenposition des Mischluftmotors Bereich von 0 [%] bis 100 [%] |
| STAT_MISCHLUFT_EINH | string | aktuelle Soll-Klappenposition des Mischluftmotors Einheit: % |
| STAT_MISCHLUFT_IST_WERT | real | aktuelle Ist-Klappenposition des Mischluftmotors Bereich von 0 [%] bis 100 [%] |
| STAT_MISCHLUFT_IST_EINH | string | aktuelle Ist-Klappenposition des Mischluftmotors Einheit: % |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klimasystem"></a>
### STATUS_KLIMASYSTEM

lesen Status Klimasystem und alller Adressen der LIN-Bus-Motoren mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KLIMAGERAETTYP_WERT | int | Typ erkanntes Heizklimagerät table KlimageraetTypTab WERT |
| STAT_KLIMAGERAETTYP_TEXT | string | Typ erkanntes Heizklimagerät table KlimageraetTypTab TEXT |
| STAT_KLIMABEDIENTEILTYP_WERT | int | Typ erkanntes Heizklimabedienteil table KlimabedienteilTypTab WERT |
| STAT_KLIMABEDIENTEILTYP_TEXT | string | Typ erkanntes Heizklimabedienteil table KlimabedienteilTypTab TEXT |
| STAT_ZENTRALANTRIEB_ADRESSE_WERT | real | Adresse Zentralantriebmotor Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_ZENTRALANTRIEB_ADRESSE_EINH | string | Adresse Zentralantriebmotor Einheit: 0/1 |
| STAT_FRISCHLUFT_UMLUFT_ADRESSE_WERT | real | Adresse Frischluft-Umluft-Motor Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_FRISCHLUFT_UMLUFT_ADRESSE_EINH | string | Adresse Frischluft-Umluft-Motor Einheit: 0/1 |
| STAT_MISCHLUFT_ADRESSE_WERT | real | Adresse Mischluftklappenmotor Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_MISCHLUFT_ADRESSE_EINH | string | Adresse Mischluftklappenmotor Einheit: 0/1 |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-eichlauf"></a>
### STATUS_MOTOR_EICHLAUF

lesen Status Motoren-Eichlauf mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_EICHLAUF_WERT | int | globaler Status Eichlauf table StatusEichlaufAllgemeinTab WERT |
| STAT_EICHLAUF_TEXT | string | globaler Status Eichlauf table StatusEichlaufAllgemeinTab TEXT |
| STAT_EICHLAUF_HISTORY_WERT | int | zeigt Status der Historie table StatusEichlaufHistoryTab WERT |
| STAT_EICHLAUF_HISTORY_TEXT | string | zeigt Status der Historie table StatusEichlaufHistoryTab TEXT |
| STAT_ZENTRALANTRIEB_WERT | int | Status Eichlauf für Zentralantrieb table StatusEichlaufMotorTab WERT |
| STAT_ZENTRALANTRIEB_TEXT | string | Status Eichlauf für Zentralantrieb table StatusEichlaufMotorTab TEXT |
| STAT_KLAPPE_UMLUFT_WERT | int | Status Eichlauf für Frischluft-Umluft-Motor table StatusEichlaufMotorTab WERT |
| STAT_KLAPPE_UMLUFT_TEXT | string | Status Eichlauf für Frischluft-Umluft-Motor table StatusEichlaufMotorTab TEXT |
| STAT_KLAPPE_MISCHLUFT_WERT | int | Status Eichlauf für Mischluftmotor table StatusEichlaufMotorTab WERT |
| STAT_KLAPPE_MISCHLUFT_TEXT | string | Status Eichlauf für Mischluftmotor table StatusEichlaufMotorTab TEXT |
| STAT_EICHLAUF_IO_WERT | int | zeigt Status Eichlauf table StatusEichlaufIOTab WERT |
| STAT_EICHLAUF_IO_TEXT | string | zeigt Status Eichlauf table StatusEichlaufIOTab TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klappen-verstellbereich"></a>
### STATUS_KLAPPEN_VERSTELLBEREICH

Lesen des aktuellen Status der Verstellbereiche alle Motoren ermittelt über den Eichlauf mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VERSTELLBEREICH_WERT | int | Status Klappenverstellbereich 0 = keine gültigen Schrittweiten 1 = gültige Schrittweiten table StatusVerstellbereichTab WERT |
| STAT_VERSTELLBEREICH_TEXT | string | Status Klappenverstellbereich 0 = keine gültigen Schrittweiten 1 = gültige Schrittweiten table StatusVerstellbereichTab TEXT |
| STAT_VERSTELLBEREICH_FRISCHLUFT_UMLUFT_WERT | real | Verstellbereich des Frischluft-Umluft-Motors (65535 = Fehlerwert) Bereich von 0 [Inkremente] bis 65535 [Inkremente] |
| STAT_VERSTELLBEREICH_FRISCHLUFT_UMLUFT_EINH | string | Verstellbereich des Frischluft-Umluft-Motors (65535 = Fehlerwert) Einheit: Inkremente |
| STAT_VERSTELLBEREICH_MISCHLUFT_WERT | real | Verstellbereich des Mischluftmotors  (65535 = Fehlerwert) Bereich von 0 [Inkremente] bis 65535 [Inkremente] |
| STAT_VERSTELLBEREICH_MISCHLUFT_EINH | string | Verstellbereich des Mischluftmotors  (65535 = Fehlerwert) Einheit: Inkremente |
| STAT_VERSTELLBEREICH_DEFROSTNOCKE_WERT | real | Breite der Defrostnocke  (65535 = Fehlerwert) Bereich von 0 [Inkremente] bis 65535 [Inkremente] |
| STAT_VERSTELLBEREICH_DEFROSTNOCKE_EINH | string | Breite der Defrostnocke  (65535 = Fehlerwert) Einheit: Inkremente |
| STAT_VERSTELLBEREICH_FUSSRAUMNOCKE_WERT | real | Breite der Fussraumnocke  (65535 = Fehlerwert) Bereich von 0 [Inkremente] bis 65535 [Inkremente] |
| STAT_VERSTELLBEREICH_FUSSRAUMNOCKE_EINH | string | Breite der Fussraumnocke  (65535 = Fehlerwert) Einheit: Inkremente |
| STAT_VERSTELLBEREICH_NOCKENABSTAND_WERT | real | Abstand der Nocken  (65535 = Fehlerwert) Bereich von 0 [Inkremente] bis 65535 [Inkremente] |
| STAT_VERSTELLBEREICH_NOCKENABSTAND_EINH | string | Abstand der Nocken  (65535 = Fehlerwert) Einheit: Inkremente |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sensoren-analog-port"></a>
### STATUS_SENSOREN_ANALOG_PORT

Auslesen Rohwerte Sensoren mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_I_O_PORT_NAME_WERT | int | Ausgabe des IO-Port-Namens table AnalogPortTab WERT |
| STAT_I_O_PORT_NAME_TEXT | string | Ausgabe des IO-Port-Namens table AnalogPortTab TEXT |
| STAT_TEMP_VERDAMPFER_WERT | real | ADC Wert für Verdampfersensor Bereich von 0 [ROHWERT] bis 1023 [ROHWERT] |
| STAT_TEMP_VERDAMPFER_EINH | string | ADC Wert für Verdampfersensor Einheit: ROHWERT |
| STAT_TEMP_FUSSRAUM_WERT | real | ADC Wert für Fussraumsensor Bereich von 0 [ROHWERT] bis 1023 [ROHWERT] |
| STAT_TEMP_FUSSRAUM_EINH | string | ADC Wert für Fussraumsensor Einheit: ROHWERT |
| STAT_TEMP_BELUEFTUNG_WERT | real | ADC Wert für Belüftungssensor Bereich von 0 [ROHWERT] bis 1023 [ROHWERT] |
| STAT_TEMP_BELUEFTUNG_EINH | string | ADC Wert für Belüftungssensor Einheit: ROHWERT |
| STAT_TEMP_PCB_WERT | real | ADC Wert für Temperatur der Leiterplatte Bereich von 0 [ROHWERT] bis 1023 [ROHWERT] |
| STAT_TEMP_PCB_EINH | string | ADC Wert für Temperatur der Leiterplatte Einheit: ROHWERT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spannungen-analog-port"></a>
### STATUS_SPANNUNGEN_ANALOG_PORT

Auslesen Rohwert Batteriespannung mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ANALOG_PORT_NAME_WERT | int | Ausgabe des IO-Port-Namens table AnalogPortTab WERT |
| STAT_ANALOG_PORT_NAME_TEXT | string | Ausgabe des IO-Port-Namens table AnalogPortTab TEXT |
| STAT_U_BATT_WERT | real | ADC Wert für Batteriespannung Bereich von 0 [ROHWERT] bis 1023 [ROHWERT] |
| STAT_U_BATT_EINH | string | ADC Wert für Batteriespannung Einheit: ROHWERT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-poti-analog-port"></a>
### STATUS_POTI_ANALOG_PORT

Auslesen Rohwerte Potentiometer mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ANALOG_PORT_NAME_WERT | int | Ausgabe des IO-Port-Namens table AnalogPortTab WERT |
| STAT_ANALOG_PORT_NAME_TEXT | string | Ausgabe des IO-Port-Namens table AnalogPortTab TEXT |
| STAT_SOLLWERT_LINKS_1_WERT | real | ADC Wert 1 für Sollwert Luftverteilung Bereich von 0 [ROHWERT] bis 1023 [ROHWERT] |
| STAT_SOLLWERT_LINKS_1_EINH | string | ADC Wert 1 für Sollwert Luftverteilung Einheit: ROHWERT |
| STAT_SOLLWERT_LINKS_2_WERT | real | ADC Wert 2 für Sollwert Luftverteilung Bereich von 0 [ROHWERT] bis 1023 [ROHWERT] |
| STAT_SOLLWERT_LINKS_2_EINH | string | ADC Wert 2 für Sollwert Luftverteilung Einheit: ROHWERT |
| STAT_SOLLWERT_RECHTS_WERT | real | ADC Wert für Temperatursollwert rechts Bereich von 0 [ROHWERT] bis 1023 [ROHWERT] |
| STAT_SOLLWERT_RECHTS_EINH | string | ADC Wert für Temperatursollwert rechts Einheit: ROHWERT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-szm-analog-port"></a>
### STATUS_SZM_ANALOG_PORT

Auslesen der Rohwerte SZM-Analogeingänge mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_I_O_PORT_NAME_WERT | int | Ausgabe des IO-Port-Namens table AnalogPortTab WERT |
| STAT_I_O_PORT_NAME_TEXT | string | Ausgabe des IO-Port-Namens table AnalogPortTab TEXT |
| STAT_SZM_CODIER1_WERT | real | ADC Wert für Eingang Variante1 Bereich von 0 [ROHWERT] bis 1023 [ROHWERT] |
| STAT_SZM_CODIER1_EINH | string | ADC Wert für Eingang Variante1 Einheit: ROHWERT |
| STAT_SZM_CODIER2_WERT | real | ADC Wert für Eingang Variante2 Bereich von 0 [ROHWERT] bis 1023 [ROHWERT] |
| STAT_SZM_CODIER2_EINH | string | ADC Wert für Eingang Variante2 Einheit: ROHWERT |
| STAT_SZM_TAST1_WERT | real | ADC Wert für Eingang Taste1 Bereich von 0 [ROHWERT] bis 1023 [ROHWERT] |
| STAT_SZM_TAST1_EINH | string | ADC Wert für Eingang Taste1 Einheit: ROHWERT |
| STAT_SZM_TAST2_WERT | real | ADC Wert für Eingang Taste2 Bereich von 0 [ROHWERT] bis 1023 [ROHWERT] |
| STAT_SZM_TAST2_EINH | string | ADC Wert für Eingang Taste2 Einheit: ROHWERT |
| STAT_SZM_TAST3_WERT | real | ADC Wert für Eingang Taste3 Bereich von 0 [ROHWERT] bis 1023 [ROHWERT] |
| STAT_SZM_TAST3_EINH | string | ADC Wert für Eingang Taste3 Einheit: ROHWERT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-port"></a>
### STATUS_DIGITAL_PORT

lesen der Digitaleingänge mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CAN_ERR | int | Status CAN_ERR Ausgang CAN-Transciever |
| STAT_DIAG_EXT_5V_SUPPLY | int | Status externer 5V Versorgung |
| STAT_DIAG_12V_STEPPER_SUPPLY | int | Status 12V Ausgang Schrittmotorversorgung |
| STAT_TASTER_KULISSENSCHEIBE | int | Status Mikroschalter Kulissenscheibe |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-szm-variante"></a>
### STATUS_SZM_VARIANTE

Auslesen der SZM-Variante mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_I_O_PORT_NAME_WERT | int | Ausgabe des IO-Port-Namens table AnalogPortTab WERT |
| STAT_I_O_PORT_NAME_TEXT | string | Ausgabe des IO-Port-Namens table AnalogPortTab TEXT |
| STAT_SZM_VARIANTE_WERT | real | aktuelle SZM Variante Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_SZM_VARIANTE_EINH | string | aktuelle SZM Variante Einheit: 0/1 |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-drucksensorsensor"></a>
### STATUS_CAN_DRUCKSENSORSENSOR

Auslesen des aktuellen Wertes des Drucksensors mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DRUCKSENSOR_WERT | real | aktueller Wert Kältemitteldruck (CAN-Signal DT_PSEN_RFCI  ) Bereich von 0 [bar] bis 127 [bar] |
| STAT_DRUCKSENSOR_EINH | string | aktueller Wert Kältemitteldruck (CAN-Signal DT_PSEN_RFCI  ) Einheit: bar |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tasten"></a>
### STATUS_TASTEN

aktueller Tasten-Status mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_I_O_PORT_NAME_WERT | int | Ausgabe des IO-Port-Namens table IOPortTab WERT |
| STAT_I_O_PORT_NAME_TEXT | string | Ausgabe des IO-Port-Namens table IOPortTab TEXT |
| STAT_AC | int | Status Taste AC |
| STAT_UML | int | Status Taste Umluft |
| STAT_HHS | int | Status Taste Hechscheibenheizung |
| STAT_GBL_PLUS | int | Status Taste Gebläse plus |
| STAT_GBL_MINUS | int | Status Taste Gebläse minus |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-funktionsbeleuchtung"></a>
### STATUS_FUNKTIONSBELEUCHTUNG

aktueller Status der Funktions-LEDs mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_I_O_PORT_NAME_WERT | int | Ausgabe des IO-Port-Namens table IOPortTab WERT |
| STAT_I_O_PORT_NAME_TEXT | string | Ausgabe des IO-Port-Namens table IOPortTab TEXT |
| STAT_LED_AC | int | Status LED AC |
| STAT_LED_UML | int | Status LED Umluft |
| STAT_LED_HHS | int | Status LED Heckscheibenheitzung |
| STAT_LED_GEBL_1 | int | Status LED Gebläsestufe 1 |
| STAT_LED_GEBL_2 | int | Status LED Gebläsestufe 2 |
| STAT_LED_GEBL_3 | int | Status LED Gebläsestufe 3 |
| STAT_LED_GEBL_4 | int | Status LED Gebläsestufe 4 |
| STAT_LED_GEBL_5 | int | Status LED Gebläsestufe 5 |
| STAT_LED_GEBL_6 | int | Status LED Gebläsestufe 6 |
| STAT_LED_GEBL_7 | int | Status LED Gebläsestufe 7 |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-szm-tasten"></a>
### STATUS_SZM_TASTEN

aktueller Tasten-Status SZM mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_I_O_PORT_NAME_WERT | int | Ausgabe des IO-Port-Namens table IOPortTab WERT |
| STAT_I_O_PORT_NAME_TEXT | string | Ausgabe des IO-Port-Namens table IOPortTab TEXT |
| STAT_SHL | int | Status Taste Sitzheitzung links |
| STAT_SKL | int | Status Taste Sitzklima links |
| STAT_PDC | int | Status Taste Parc Distance Control |
| STAT_SKR | int | Status Taste Sitzklima rechts |
| STAT_SHR | int | Status Taste Sitzheitzung rechts |
| STAT_MSA | int | Status Taste Motor Start/Stop Automatik |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-szm-funktionsbeleuchtung"></a>
### STATUS_SZM_FUNKTIONSBELEUCHTUNG

aktueller Status der SZM Funktions-LEDs mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_I_O_PORT_NAME_WERT | int | Ausgabe des IO-Port-Namens table IOPortTab WERT |
| STAT_I_O_PORT_NAME_TEXT | string | Ausgabe des IO-Port-Namens table IOPortTab TEXT |
| STAT_LED_SHL_1 | int | Status LED Sitzheitzung links 1 |
| STAT_LED_SHL_2 | int | Status LED Sitzheitzung links 2 |
| STAT_LED_SHL_3 | int | Status LED Sitzheitzung links 3 |
| STAT_LED_SKL_1 | int | Status LED Sitzklima links 1 |
| STAT_LED_SKL_2 | int | Status LED Sitzklima links 2 |
| STAT_LED_SKL_3 | int | Status LED Sitzklima links 3 |
| STAT_LED_PDC | int | Status LED Parc Distance Control |
| STAT_LED_VDA | int | Status LED Verdeck auf |
| STAT_LED_VDZ | int | Status LED Verdeck zu |
| STAT_LED_SKR_1 | int | Status LED Sitzklima rechts 1 |
| STAT_LED_SKR_2 | int | Status LED Sitzklima rechts 2 |
| STAT_LED_SKR_3 | int | Status LED Sitzklima rechts 3 |
| STAT_LED_SHR_1 | int | Status LED Sitzheitzung rechts 1 |
| STAT_LED_SHR_2 | int | Status LED Sitzheitzung rechts 2 |
| STAT_LED_SHR_3 | int | Status LED Sitzheitzung rechts 3 |
| STAT_LED_MSA | int | Status LED Motor Start/Stop Automatik |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pwm-funktionsbeleuchtung"></a>
### STATUS_PWM_FUNKTIONSBELEUCHTUNG

aktueller Status Helligkeit (PWM) der Funktionsbeleuchtung mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_I_O_PORT_NAME_WERT | int | Ausgabe des IO-Port-Namens table IOPortTab WERT |
| STAT_I_O_PORT_NAME_TEXT | string | Ausgabe des IO-Port-Namens table IOPortTab TEXT |
| STAT_LED_GREEN_WERT | real | PWM-Ansteuerung Funktionsbeleuchtung grün Bereich von 0 [%] bis 100 [%] |
| STAT_LED_GREEN_EINH | string | PWM-Ansteuerung Funktionsbeleuchtung grün Einheit: % |
| STAT_LED_ORANGE_WERT | real | PWM-Ansteuerung Funktionsbeleuchtung orange Bereich von 0 [%] bis 100 [%] |
| STAT_LED_ORANGE_EINH | string | PWM-Ansteuerung Funktionsbeleuchtung orange Einheit: % |
| STAT_LED_BLUE_SZM_WERT | real | PWM-Ansteuerung Funktionsbeleuchtung blau (SZM) Bereich von 0 [%] bis 100 [%] |
| STAT_LED_BLUE_SZM_EINH | string | PWM-Ansteuerung Funktionsbeleuchtung blau (SZM) Einheit: % |
| STAT_LED_RED_SZM_WERT | real | PWM-Ansteuerung Funktionsbeleuchtung rot (SZM) Bereich von 0 [%] bis 100 [%] |
| STAT_LED_RED_SZM_EINH | string | PWM-Ansteuerung Funktionsbeleuchtung rot (SZM) Einheit: % |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-beleuchtung"></a>
### STATUS_BELEUCHTUNG

aktueller Status Helligkeit (PWM) der Hintergrundbeleuchtung mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_I_O_PORT_NAME_WERT | int | Ausgabe des IO-Port-Namens table IOPortTab WERT |
| STAT_I_O_PORT_NAME_TEXT | string | Ausgabe des IO-Port-Namens table IOPortTab TEXT |
| STAT_LED_ORANGE_WERT | real | PWM-Ansteuerung Suchbeleuchtung orange Bereich von 0 [%] bis 100 [%] |
| STAT_LED_ORANGE_EINH | string | PWM-Ansteuerung Suchbeleuchtung orange Einheit: % |
| STAT_LED_BLUE_WERT | real | PWM-Ansteuerung Suchbeleuchtung blau Bereich von 0 [%] bis 100 [%] |
| STAT_LED_BLUE_EINH | string | PWM-Ansteuerung Suchbeleuchtung blau Einheit: % |
| STAT_LED_RED_WERT | real | PWM-Ansteuerung Suchbeleuchtung rot Bereich von 0 [%] bis 100 [%] |
| STAT_LED_RED_EINH | string | PWM-Ansteuerung Suchbeleuchtung rot Einheit: % |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-diagnosetestbetrieb-permanent"></a>
### STATUS_DIAGNOSETESTBETRIEB_PERMANENT

Auslesen Status Diagnose Test Mode permanent mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_EIN_AUS | int | Diagnose Test Mode permanent aktiviert/nicht aktiviert |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-autoadresierung"></a>
### STATUS_AUTOADRESIERUNG

Auslesen autoadresierung status von motoren mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ROUTINE_STATUS_WERT | int | Ausgabe des Routine Status table StatusStepperRoutineStatus WERT |
| STAT_ROUTINE_STATUS_TEXT | string | Ausgabe des Routine Status table StatusStepperRoutineStatus TEXT |
| STAT_ROUTINE_RESULT_WERT | int | Ausgabe des Routine Resultate table StatusStepperRoutineResult WERT |
| STAT_ROUTINE_RESULT_TEXT | string | Ausgabe des Routine Resultate table StatusStepperRoutineResult TEXT |
| STAT_STEPPER_21H_ADDRESSING_WERT | int | Ausgabe des Adressierung Status motor 21h table StatusStepperAddrProg WERT |
| STAT_STEPPER_21H_ADDRESSING_TEXT | string | Ausgabe des Adressierung Status motor 21h table StatusStepperAddrProg TEXT |
| STAT_STEPPER_22H_ADDRESSING_WERT | int | Ausgabe des Adressierung Status motor 22h table StatusStepperAddrProg WERT |
| STAT_STEPPER_22H_ADDRESSING_TEXT | string | Ausgabe des Adressierung Status motor 22h table StatusStepperAddrProg TEXT |
| STAT_STEPPER_28H_ADDRESSING_WERT | int | Ausgabe des Adressierung Status motor 28h table StatusStepperAddrProg WERT |
| STAT_STEPPER_28H_ADDRESSING_TEXT | string | Ausgabe des Adressierung Status motor 28h table StatusStepperAddrProg TEXT |
| STAT_STEPPER_21H_PROGRAMMING_WERT | int | Ausgabe des Programierung Status motor 21h table StatusStepperAddrProg WERT |
| STAT_STEPPER_21H_PROGRAMMING_TEXT | string | Ausgabe des Programierung Status motor 21h table StatusStepperAddrProg TEXT |
| STAT_STEPPER_22H_PROGRAMMING_WERT | int | Ausgabe des Programierung Status motor 22h table StatusStepperAddrProg WERT |
| STAT_STEPPER_22H_PROGRAMMING_TEXT | string | Ausgabe des Programierung Status motor 22h table StatusStepperAddrProg TEXT |
| STAT_STEPPER_28H_PROGRAMMING_WERT | int | Ausgabe des Programierung Status motor 28h table StatusStepperAddrProg WERT |
| STAT_STEPPER_28H_PROGRAMMING_TEXT | string | Ausgabe des Programierung Status motor 28h table StatusStepperAddrProg TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-einzeladresierung"></a>
### STATUS_EINZELADRESIERUNG

Auslesen adresierung status von letzte adressierte motor mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ROUTINE_STATUS_WERT | int | Ausgabe des Routine Status table StatusStepperRoutineStatus WERT |
| STAT_ROUTINE_STATUS_TEXT | string | Ausgabe des Routine Status table StatusStepperRoutineStatus TEXT |
| STAT_ROUTINE_RESULT_WERT | int | Ausgabe des Routine Resultate table StatusStepperRoutineResult WERT |
| STAT_ROUTINE_RESULT_TEXT | string | Ausgabe des Routine Resultate table StatusStepperRoutineResult TEXT |
| STAT_STEPPER_ADDRESSING_WERT | int | Ausgabe des Adressierung Status table StatusStepperAddrProg WERT |
| STAT_STEPPER_ADDRESSING_TEXT | string | Ausgabe des Adressierung Status table StatusStepperAddrProg TEXT |
| STAT_STEPPER_PROGRAMMING_WERT | int | Ausgabe des Programierung Status table StatusStepperAddrProg WERT |
| STAT_STEPPER_PROGRAMMING_TEXT | string | Ausgabe des Programierung Status table StatusStepperAddrProg TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-klappenposition-inkrement"></a>
### STATUS_MOTOR_KLAPPENPOSITION_INKREMENT

lesen Inkrement von Soll- und Ist-Klappenpositionen mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ZENTRALANTRIEB_WERT | real | aktuelle Soll-position des Zentralantriebmotors Bereich von 0 [STEP] bis 32767 [STEP] |
| STAT_ZENTRALANTRIEB_EINH | string | aktuelle Soll-position des Zentralantriebmotors Einheit: STEP |
| STAT_ZENTRALANTRIEB_IST_WERT | real | aktuelle Ist-position des Zentralantriebmotors Bereich von 0 [STEP] bis 32767 [STEP] |
| STAT_ZENTRALANTRIEB_IST_EINH | string | aktuelle Ist-position des Zentralantriebmotors Einheit: STEP |
| STAT_FRISCHLUFT_UMLUFT_WERT | real | aktuelle Soll-Klappenposition des Frischluft-Umluft-Motors Bereich von 0 [STEP] bis 32767 [STEP] |
| STAT_FRISCHLUFT_UMLUFT_EINH | string | aktuelle Soll-Klappenposition des Frischluft-Umluft-Motors Einheit: STEP |
| STAT_FRISCHLUFT_UMLUFT_IST_WERT | real | aktuelle Ist-Klappenposition des Frischluft-Umluft-Motors Bereich von 0 [STEP] bis 32767 [STEP] |
| STAT_FRISCHLUFT_UMLUFT_IST_EINH | string | aktuelle Ist-Klappenposition des Frischluft-Umluft-Motors Einheit: STEP |
| STAT_MISCHLUFT_WERT | real | aktuelle Soll-Klappenposition des Mischluftmotors Bereich von 0 [STEP] bis 32767 [STEP] |
| STAT_MISCHLUFT_EINH | string | aktuelle Soll-Klappenposition des Mischluftmotors Einheit: STEP |
| STAT_MISCHLUFT_IST_WERT | real | aktuelle Ist-Klappenposition des Mischluftmotors Bereich von 0 [STEP] bis 32767 [STEP] |
| STAT_MISCHLUFT_IST_EINH | string | aktuelle Ist-Klappenposition des Mischluftmotors Einheit: STEP |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-ident"></a>
### STATUS_MOTOR_IDENT

Liefert die Identdaten des jeweiligen LIN-Bus-Schrittmotors (reportCurrentState) KWP2000: $21 ReadDataByLocalIdentifier $xx InputOutputLocalIdetifier LIN-Bus-Teilnehmer Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LIN_DEVICE_ARGUMENT | unsigned char | LIN-Bus-Teilnehmer table LinMotorTab  LinMotornumber,LinMotorname Wenn keine Eingabe: default = 0x21 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_REFERENCE | unsigned char | Aktuelle Referenznummer |
| STAT_SUPPLIER | unsigned char | Aktuelle Suppliernummer |
| STAT_ASIC_NR | unsigned char | Aktuelle ASIC-Nummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kompressor-einlaufschutz"></a>
### STEUERN_KOMPRESSOR_EINLAUFSCHUTZ

Setzen/Löschen des Kompressor Einlaufschutzes KWP2000: $3B WriteDataByLocalIdentifier $02 Kompressor Einlaufschutz (recordLocalIdentifier) $0x Ein/Aus (recordValue#1) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EIN_AUS | string | "ein" -&gt; Kompressoreinlaufschutz ein "aus" -&gt; Kompressoreinlaufschutz aus table DigitalArgument TEXT Wenn keine Eingabe: Default = "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tasten"></a>
### STEUERN_TASTEN

Ansteuern Tasten KWP2000: $30 InputOutputControlByLocalIdentifier $01 InputOutputLocalIdetifier: Tasten $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AC | string | "ein" -&gt; Taste AC ein "aus" -&gt; Taste AC aus table DigitalArgument TEXT default: "aus" |
| UML | string | "ein" -&gt; Taste UML ein "aus" -&gt; Taste UML aus table DigitalArgument TEXT default: "aus" |
| HHS | string | "ein" -&gt; Taste HHS ein "aus" -&gt; Taste HHS aus table DigitalArgument TEXT default: "aus" |
| GBL_PLUS | string | "ein" -&gt; Taste GEBLÄSE PLUS ein "aus" -&gt; Taste GEBLÄSE PLUS aus table DigitalArgument TEXT default: "aus" |
| GBL_MINUS | string | "ein" -&gt; Taste GEBLÄSE MINUS ein "aus" -&gt; Taste GEBLÄSE MINUS aus table DigitalArgument TEXT default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-funktionsbeleuchtung"></a>
### STEUERN_FUNKTIONSBELEUCHTUNG

Ansteuern Funktionsbeleuchtungs-LEDs KWP2000: $30 InputOutputControlByLocalIdentifier $02 LED $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LED_AC | string | "ein" -&gt; LED AC ein "aus" -&gt; LED AC aus table DigitalArgument TEXT default: "aus" |
| LED_UML | string | "ein" -&gt; LED Umluft ein "aus" -&gt; LED Umluft aus table DigitalArgument TEXT default: "aus" |
| LED_HHS | string | "ein" -&gt; LED HHS ein "aus" -&gt; LED HHS aus table DigitalArgument TEXT default: "aus" |
| LED_GEBL_1 | string | "ein" -&gt; LED Gebläse 1 ein "aus" -&gt; LED Gebläse 1 aus table DigitalArgument TEXT default: "aus" |
| LED_GEBL_2 | string | "ein" -&gt; LED Gebläse 2 ein "aus" -&gt; LED Gebläse 2 aus table DigitalArgument TEXT default: "aus" |
| LED_GEBL_3 | string | "ein" -&gt; LED Gebläse 3 ein "aus" -&gt; LED Gebläse 3 aus table DigitalArgument TEXT default: "aus" |
| LED_GEBL_4 | string | "ein" -&gt; LED Gebläse 4 ein "aus" -&gt; LED Gebläse 4 aus table DigitalArgument TEXT default: "aus" |
| LED_GEBL_5 | string | "ein" -&gt; LED Gebläse 5 ein "aus" -&gt; LED Gebläse 5 aus table DigitalArgument TEXT default: "aus" |
| LED_GEBL_6 | string | "ein" -&gt; LED Gebläse 6 ein "aus" -&gt; LED Gebläse 6 aus table DigitalArgument TEXT default: "aus" |
| LED_GEBL_7 | string | "ein" -&gt; LED Gebläse 7 ein "aus" -&gt; LED Gebläse 7 aus table DigitalArgument TEXT default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-szm-tasten"></a>
### STEUERN_SZM_TASTEN

Ansteuern Tasten SZM KWP2000: $30 InputOutputControlByLocalIdentifier $03 Tasten SZM $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SHL | string | "ein" -&gt; BUTTON SHL ein "aus" -&gt; BUTTON SHL aus table DigitalArgument TEXT default: "aus" |
| SKL | string | "ein" -&gt; BUTTON SVL ein "aus" -&gt; BUTTON SVL aus table DigitalArgument TEXT default: "aus" |
| PDC | string | "ein" -&gt; BUTTON PDC ein "aus" -&gt; BUTTON PDC aus table DigitalArgument TEXT default: "aus" |
| SKR | string | "ein" -&gt; BUTTON SVR ein "aus" -&gt; BUTTON SVR aus table DigitalArgument TEXT default: "aus" |
| SHR | string | "ein" -&gt; BUTTON SHR ein "aus" -&gt; BUTTON SHR aus table DigitalArgument TEXT default: "aus" |
| MSA | string | "ein" -&gt; BUTTON MSA ein "aus" -&gt; BUTTON MSA aus table DigitalArgument TEXT default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-szm-funktionsbeleuchtung"></a>
### STEUERN_SZM_FUNKTIONSBELEUCHTUNG

Ansteuern SZM Funktionsbeleuchtungs-LEDs KWP2000: $30 InputOutputControlByLocalIdentifier $04 LED SZM $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LED_SHL_1 | string | "ein" -&gt; LED SHL ein "aus" -&gt; LED SHL aus table DigitalArgument TEXT default: "aus" |
| LED_SHL_2 | string | "ein" -&gt; LED SHL 2 ein "aus" -&gt; LED SHL 2 aus table DigitalArgument TEXT default: "aus" |
| LED_SHL_3 | string | "ein" -&gt; LED SHL 3 ein "aus" -&gt; LED SHL 3 aus table DigitalArgument TEXT default: "aus" |
| LED_SKL_1 | string | "ein" -&gt; LED SKL ein "aus" -&gt; LED SKL aus table DigitalArgument TEXT default: "aus" |
| LED_SKL_2 | string | "ein" -&gt; LED SKL 2 ein "aus" -&gt; LED SKL 2 aus table DigitalArgument TEXT default: "aus" |
| LED_SKL_3 | string | "ein" -&gt; LED SKL 3 ein "aus" -&gt; LED SKL 3 aus table DigitalArgument TEXT default: "aus" |
| LED_PDC | string | "ein" -&gt; LED PDC ein "aus" -&gt; LED PDC aus table DigitalArgument TEXT default: "aus" |
| LED_VDA | string | "ein" -&gt; LED HT OPEN ein "aus" -&gt; LED HT OPEN aus table DigitalArgument TEXT default: "aus" |
| LED_VDZ | string | "ein" -&gt; LED HT CLOSE ein "aus" -&gt; LED HT CLOSE aus table DigitalArgument TEXT default: "aus" |
| LED_SKR_1 | string | "ein" -&gt; LED SKR 1 ein "aus" -&gt; LED SKR 1 aus table DigitalArgument TEXT default: "aus" |
| LED_SKR_2 | string | "ein" -&gt; LED SKR 2 ein "aus" -&gt; LED SKR 2 aus table DigitalArgument TEXT default: "aus" |
| LED_SKR_3 | string | "ein" -&gt; LED SKR 3 ein "aus" -&gt; LED SKR 3 aus table DigitalArgument TEXT default: "aus" |
| LED_SHR_1 | string | "ein" -&gt; LED SHL ein "aus" -&gt; LED SHL aus table DigitalArgument TEXT default: "aus" |
| LED_SHR_2 | string | "ein" -&gt; LED SHL 2 ein "aus" -&gt; LED SHL 2 aus table DigitalArgument TEXT default: "aus" |
| LED_SHR_3 | string | "ein" -&gt; LED SHL 3 ein "aus" -&gt; LED SHL 3 aus table DigitalArgument TEXT default: "aus" |
| LED_MSA | string | "ein" -&gt; LED MSA ein "aus" -&gt; LED MSA aus table DigitalArgument TEXT default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pwm-funktionsbeleuchtung"></a>
### STEUERN_PWM_FUNKTIONSBELEUCHTUNG

Setzen der Helligkeit (PWM) der Funtionsbeleuchtung KWP2000: $30 InputOutputControlByLocalIdentifier $05 PWM LEDs $01 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LED_GREEN | int | gewuenschte PWM-Ansteuerung Bereich: 0 bis 100 % default = 0 |
| LED_ORANGE | int | gewuenschte PWM-Ansteuerung Bereich: 0 bis 100 % default = 0 |
| LED_BLUE_SZM | int | gewuenschte PWM-Ansteuerung Bereich: 0 bis 100 % default = 0 |
| LED_RED_SZM | int | gewuenschte PWM-Ansteuerung Bereich: 0 bis 100 % default = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-beleuchtung"></a>
### STEUERN_BELEUCHTUNG

Ansteuern Hintergrundbeleuchtung KWP2000: $30 InputOutputControlByLocalIdentifier $06 LEDs $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LED_ORANGE | int | gewuenschte PWM-Ansteuerung Bereich: 0 bis 100 % default = 0 |
| LED_BLUE | int | gewuenschte PWM-Ansteuerung Bereich: 0 bis 100 % default = 0 |
| LED_RED | int | gewuenschte PWM-Ansteuerung Bereich: 0 bis 100 % default = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-12v-ausgang"></a>
### STEUERN_12V_AUSGANG

Ansteuern 12V Ausgang (Schrittmotorversorgung) KWP2000: $30 InputOutputControlByLocalIdentifier $07 12V-Ausgang $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PORT_STATUS | int | "ein" -&gt; 12V Ausgang ein "aus" -&gt; 12V Ausgang aus table DigitalArgument TEXT default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-geblaese"></a>
### STEUERN_GEBLAESE

Ansteuern Geblaese KWP2000: $30 InputOutputControlByLocalIdentifier $08 Geblaese $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PWM_VALUE | int | gewuenschte PWM-Ansteuerung Bereich: 0 aus, min. Gebläseleistung 10% - 20%, linear 20 - 80%, max. Gebläseleistung 80 - 95%, Notlauf &gt; 95% default = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-zentralantrieb"></a>
### STEUERN_KLAPPE_ZENTRALANTRIEB

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $21 InputOutputLocalIdetifier (Zentralantrieb) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Klappenstellung 0%-100% in 1% Schritten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-umluft"></a>
### STEUERN_KLAPPE_UMLUFT

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $22 InputOutputLocalIdetifier (Umluft) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Klappenstellung 0%-100% in 1% Schritten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-mischluft"></a>
### STEUERN_KLAPPE_MISCHLUFT

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $23 InputOutputLocalIdetifier (Mischluft) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Klappenstellung 0%-100% in 1% Schritten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-can-heizbare-heckscheibe"></a>
### STEUERN_CAN_HEIZBARE_HECKSCHEIBE

Ansteuern Zusatzwasserpumpe ueber CAN KWP2000: $30 InputOutputControlByLocalIdentifier $09 heizbare Heckscheibe $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HHS_EIN_AUS | string | "ein" -&gt; HHS ein "aus" -&gt; HHS aus table DigitalArgument TEXT default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-can-kompressor-ventil"></a>
### STEUERN_CAN_KOMPRESSOR_VENTIL

Ansteuern Kompressorventil ueber CAN KWP2000: $30 InputOutputControlByLocalIdentifier $0A Kompressorventil $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | unsigned char | Ansteuerung Kompressor 0%-100% in 1% Schritten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-can-kompressor-kupplung"></a>
### STEUERN_CAN_KOMPRESSOR_KUPPLUNG

Ansteuern Zusatzwasserpumpe ueber CAN KWP2000: $30 InputOutputControlByLocalIdentifier $0B Kompressorkupplung $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KUPPLUNG_EIN_AUS | string | "ein" -&gt; Kompressorkupplung ein "aus" -&gt; Kompressorkupplung aus table DigitalArgument TEXT default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-can-zusatzwasserpumpe"></a>
### STEUERN_CAN_ZUSATZWASSERPUMPE

Ansteuern Zusatzwasserpumpe ueber CAN KWP2000: $30 InputOutputControlByLocalIdentifier $0C Zusatzwasserpumpe $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZUSATZWASSERPUMPE_EIN_AUS | string | "ein" -&gt; ZUSATZWASSERPUMPE ein "aus" -&gt; ZUSATZWASSERPUMPE aus table DigitalArgument TEXT default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-can-elektrische-wasserpumpe"></a>
### STEUERN_CAN_ELEKTRISCHE_WASSERPUMPE

Ansteuern elektrische Wasserpumpe ueber CAN KWP2000: $30 InputOutputControlByLocalIdentifier $0D Kompressorventil $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | unsigned char | Ansteuerung elektrische Wasserpumpe 0%-100% in 1% Schritten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-diagnosetestbetrieb-permanent"></a>
### STEUERN_DIAGNOSETESTBETRIEB_PERMANENT

Diagnose Test Mode mit/ohne Timeout-Ueberwachung KWP2000: $30 InputOutputControlByLocalIdentifier $0E DIAG_PERMANENT $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EIN_AUS | string | "ein" -&gt; Diagnose Test Mode permanent aktiviert "aus" -&gt; Diagnose Test Mode permanent deaktiviert table DigitalArgument TEXT default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-return-ecu-control"></a>
### STEUERN_RETURN_ECU_CONTROL

Ruecksetzen Diagnose Test Mode KWP2000: $30 InputOutputControlByLocalIdentifier $00 ReturnControlToECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-motoren-eichlauf"></a>
### STEUERN_MOTOREN_EICHLAUF

Löst Klappeneichlauf aus und kalibriert die Schrittzahlen neu KWP2000: $31 StartRoutineByLocalIdetifier $20 routineLocalIdentifier Klappenmotoreneichlauf Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-autoadressierung"></a>
### STEUERN_AUTOADRESSIERUNG

Startet die LIN-Bus Autoadressierung KWP2000: $31 StartRoutineByLocalIdetifier $22 routineLocalIdentifier LIN-Bus Autoadressierung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-einzeladressierung"></a>
### STEUERN_EINZELADRESSIERUNG

Startet die LIN-Bus Einzeladressierung KWP2000: $31 StartRoutineByLocalIdetifier $23 routineLocalIdentifier LIN-Bus Einzeladressierung Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CURRENT_STEPPER_ADDESS | unsigned char | Aktuelle Adresse des zu programmierenden Motors |
| NEW_STEPPER_ADDRESS | unsigned char | Neue Adresse des zu programmierenden Motors |
| DIRECTION | unsigned char | Laufrichtung des zu programmierenden Motors 0x00=Laufrichtung im Uhrzeigersinn für steigende Schrittzahlen 0x01=Laufrichtung gegen den Uhrzeigersinn für steigende Schrittzahlen 0xFF=Laufrichtung wie aktuelle Motorprogrammierung |
| SAFETY_ENABLE | unsigned char | Notlaufaktivierung des zu programmierenden Motors 0x00=Notauf aktiviert 0x01=Notauf deaktiviert 0xFF=Notauf wie aktuelle Motorprogrammierung |
| SAFETY_DIRECTION | unsigned char | Notlaufendposition des zu programmierenden Motors 0x00=Zu niedrigen Schrittzahlen 0x01=Zu hohen Schrittzahlen 0xFF=Notlaufendposition wie aktuelle Motorprogrammierung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-setzen-default-werte-alle-schluessel"></a>
### STEUERN_SETZEN_DEFAULT_WERTE_ALLE_SCHLUESSEL

Setzt alle Schlüssel auf Default-Werte KWP2000: $31 StartRoutineByLocalIdetifier $26 routineLocalIdentifier LIN-Bus Autoadressierung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-diagnosebit-loeschen"></a>
### STEUERN_DIAGNOSEBIT_LOESCHEN

Rücksetzen der I/O-Port-Diagnosebits (returnControlToECU) KWP2000: $30 InputOutputControlByLocalIdentifier $xx InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) $00 returnControlToECU Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_ARGUMENT | unsigned char | Nummer des I/O-Ports table IOPortTab Portnumber,Portname Wenn keine Eingabe: default = 0x01 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-security-access-auftrag"></a>
### STEUERN_SECURITY_ACCESS_AUFTRAG

Zugang mit Security Access 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEY_NR | string | Schluessel (8-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-steuern-poti-kalibrierung-links-fuss"></a>
### STEUERN_POTI_KALIBRIERUNG_LINKS_FUSS

Kalibierung Drehsteller links fuss. KWP2000: $31 StartRoutineByLocalIdetifier $11 routineLocalIdentifier Potentiometer links fuss. Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-poti-kalibrierung-links-def"></a>
### STEUERN_POTI_KALIBRIERUNG_LINKS_DEF

Kalibierung Drehsteller links defrost. KWP2000: $31 StartRoutineByLocalIdetifier $15 routineLocalIdentifier Potentiometer links defrost. Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-poti-kalibrierung-links-bel"></a>
### STEUERN_POTI_KALIBRIERUNG_LINKS_BEL

Kalibierung Drehsteller links beluftung. KWP2000: $31 StartRoutineByLocalIdetifier $12 routineLocalIdentifier Potentiometer links beluftung. Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-poti-kalibrierung-rechts-min"></a>
### STEUERN_POTI_KALIBRIERUNG_RECHTS_MIN

Kalibierung Drehsteller rechts min. KWP2000: $31 StartRoutineByLocalIdetifier $13 routineLocalIdentifier Potentiometer rechts min. Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-poti-kalibrierung-rechts-max"></a>
### STEUERN_POTI_KALIBRIERUNG_RECHTS_MAX

Kalibierung Drehsteller rechts max. KWP2000: $31 StartRoutineByLocalIdetifier $14 routineLocalIdentifier Potentiometer rechts max. Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eeprom-reset"></a>
### STEUERN_EEPROM_RESET

Startet RESET des EEPROM-Inhalts KWP2000: $31 StartRoutineByLocalIdetifier $25 routineLocalIdentifier EEPROM reset Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-geblaese"></a>
### STATUS_GEBLAESE

aktuelle Ansteuerung Gebläse mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_I_O_PORT_NAME_WERT | int | Ausgabe des IO-Port-Namens table IOPortTab WERT |
| STAT_I_O_PORT_NAME_TEXT | string | Ausgabe des IO-Port-Namens table IOPortTab TEXT |
| STAT_PWM_VALUE_WERT | real | aktuelle Gebläseleistung in %, min. Gebläseleistung 20%, linear 20 - 80%, max. Gebläseleistung 100% Bereich von 0 [%] bis 100 [%] |
| STAT_PWM_VALUE_EINH | string | aktuelle Gebläseleistung in %, min. Gebläseleistung 20%, linear 20 - 80%, max. Gebläseleistung 100% Einheit: % |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | jjj Hex-Antwort von SG |

<a id="job-status-fasta-block"></a>
### STATUS_FASTA_BLOCK

Aktueller Wert des FASTA-Blocks (je 16 Bit) KWP2000: $23 recordCommonIdentifier (High-Byte) $xx recordCommonIdentifier (Low-Byte) (FASTA-Block) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FASTA_BLOCK_ARGUMENT | unsigned char | Nummer des FASTA-Blocks (0-FF) table FastaBlockTab Blocknumber,Blockname Wenn keine Eingabe: default = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FASTA_BLOCK_NAME_WERT | string | Ausgabe des FASTA-Blocksnamens |
| STAT_FASTA_BLOCK_EINH | string | Einheit des FASTA-Blocks Stunden oder Zählerstand |
| STAT_FASTA_BLOCK_WERT | real | Wert des FASTA-Blocks |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bediengeraet"></a>
### STATUS_BEDIENGERAET

Fertigungdaten KWP2000: $21 ReadDataByLocalIdentifier $30 LocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BMW_HARDWARE_STERN_NR | string | BMW-Teilenummer |
| STAT_SW_NR_FSV | string | Softwarenummer (functional software version) |
| STAT_AIF_ZB_NR | string | BMW Zusammenbaunummer |
| STAT_LIEF_FERTIGUNGSDATEN | string | Lieferanten Fertigungsdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (121 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (42 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (44 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (3 × 9)
- [FARTTYP](#table-farttyp) (42 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (31 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [KLIMAGERAETTYPTAB](#table-klimageraettyptab) (4 × 2)
- [KLIMABEDIENTEILTYPTAB](#table-klimabedienteiltyptab) (4 × 2)
- [KLIMASYSTEMFEHLERTAB](#table-klimasystemfehlertab) (4 × 2)
- [STATUSEICHLAUFALLGEMEINTAB](#table-statuseichlaufallgemeintab) (5 × 2)
- [STATUSEICHLAUFHISTORYTAB](#table-statuseichlaufhistorytab) (3 × 2)
- [STATUSEICHLAUFMOTORTAB](#table-statuseichlaufmotortab) (4 × 2)
- [STATUSVERSTELLBEREICHTAB](#table-statusverstellbereichtab) (3 × 2)
- [LINMOTORTAB](#table-linmotortab) (3 × 2)
- [IOPORTTAB](#table-ioporttab) (17 × 2)
- [ANALOGPORTTAB](#table-analogporttab) (5 × 2)
- [FASTABLOCKTAB](#table-fastablocktab) (17 × 2)
- [STATUSSTEPPERADDRPROG](#table-statusstepperaddrprog) (2 × 2)
- [STATUSSTEPPERROUTINESTATUS](#table-statusstepperroutinestatus) (2 × 2)
- [STATUSSTEPPERROUTINERESULT](#table-statusstepperroutineresult) (2 × 2)
- [STATUSEICHLAUFIOTAB](#table-statuseichlaufiotab) (3 × 2)

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

Dimensions: 121 rows × 2 columns

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
| 0xAC | SMR Automotive Mirrors |
| 0xAD | So.Ge.Mi. |
| 0xAE | MTA |
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

Dimensions: 42 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9C48 | Mischluftklappe (LIN) |
| 0x9C4A | Frischluft/Umluftklappe (LIN) |
| 0x9C4D | Zentralantrieb Kulissenscheibe (LIN) |
| 0x9C54 | Autoadressierung (LIN) |
| 0x9C56 | Temperaturfühler Fußraum |
| 0x9C58 | Temperaturfühler Innenraum |
| 0x9C5F | Temperaturfühler Belüftung |
| 0x9C61 | 5V-Versorgung Peripherie |
| 0x9C62 | Temperaturfühler Verdampfer |
| 0x9C63 | Referenzschalter Kulissenscheibe |
| 0x9C6C | 12V-Versorgung Peripherie |
| 0x9C75 | Unter/Überspannung |
| 0x9C90 | Steuergeraet defekt |
| 0x9CA7 | Energiesparmode aktiv |
| 0xE704 | CAN Bus physikalischer Busfehler |
| 0xE707 | CAN Bus OFF |
| 0xE714 | CAN Botschaft Klemmenstatus |
| 0xE715 | CAN Botschaft Aussentemperatur |
| 0xE716 | CAN Botschaft Dimmung |
| 0xE717 | CAN Botschaft Motordaten |
| 0xE718 | CAN Botschaft Status Druck Kältekreislauf |
| 0xE719 | CAN Botschaft Kilometer/Reichweite |
| 0xE71A | CAN Botschaft Drehmoment 3 |
| 0xE71B | CAN Botschaft Waermestrom Motor |
| 0xE71C | CAN Botschaft Geschwindigkeit |
| 0xE71D | CAN Botschaft Status PDC |
| 0xE71E | CAN Botschaft Status BFS |
| 0xE71F | CAN Botschaft Status FAS |
| 0xE720 | CAN Botschaft Powermanagement Verbrauchersteuerung |
| 0xE721 | CAN Botschaft Status Sensor AUC |
| 0xE722 | CAN Botschaft Status Funkschlüssel |
| 0xE725 | CAN Botschaft Fahrgestellnummer |
| 0xE728 | CAN Botschaft Relativzeit |
| 0xE72A | CAN Botschaft Status Wasserventil |
| 0xE72B | CAN Botschaft Status Zusatzwasserpumpe |
| 0xE72D | CAN Botschaft Status Ventil Klimakompressor |
| 0xE72E | CAN Botschaft Status MSA |
| 0xE72F | CAN Botschaft Status Fahrlicht |
| 0xE730 | CAN Botschaft Status HHS |
| 0xE733 | CAN Botschaft Fahrzeugtyp |
| 0xE737 | CAN Botschaft Nachlaufzeit Stromversorgung |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 44 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9C48 | 0x01 | 0x02 | 0x03 | - |
| 0x9C4A | 0x01 | 0x02 | 0x03 | - |
| 0x9C4D | 0x01 | 0x02 | 0x03 | - |
| 0x9C54 | 0x01 | 0x02 | 0x03 | - |
| 0x9C56 | 0x01 | 0x02 | 0x03 | - |
| 0x9C58 | 0x01 | 0x02 | 0x03 | - |
| 0x9C5F | 0x01 | 0x02 | 0x03 | - |
| 0x9C61 | 0x01 | 0x02 | 0x03 | - |
| 0x9C62 | 0x01 | 0x02 | 0x03 | - |
| 0x9C63 | 0x01 | 0x02 | 0x03 | - |
| 0x9C6C | 0x01 | 0x02 | 0x03 | - |
| 0x9C75 | 0x01 | 0x02 | 0x03 | - |
| 0x9C8F | 0x01 | 0x02 | 0x03 | - |
| 0x9C90 | 0x01 | 0x02 | 0x03 | - |
| 0x9CA7 | 0x01 | 0x02 | 0x03 | - |
| 0xE704 | 0x01 | 0x02 | 0x03 | - |
| 0xE707 | 0x01 | 0x02 | 0x03 | - |
| 0xE714 | 0x01 | 0x02 | 0x03 | - |
| 0xE715 | 0x01 | 0x02 | 0x03 | - |
| 0xE716 | 0x01 | 0x02 | 0x03 | - |
| 0xE717 | 0x01 | 0x02 | 0x03 | - |
| 0xE718 | 0x01 | 0x02 | 0x03 | - |
| 0xE719 | 0x01 | 0x02 | 0x03 | - |
| 0xE71A | 0x01 | 0x02 | 0x03 | - |
| 0xE71B | 0x01 | 0x02 | 0x03 | - |
| 0xE71C | 0x01 | 0x02 | 0x03 | - |
| 0xE71D | 0x01 | 0x02 | 0x03 | - |
| 0xE71E | 0x01 | 0x02 | 0x03 | - |
| 0xE71F | 0x01 | 0x02 | 0x03 | - |
| 0xE720 | 0x01 | 0x02 | 0x03 | - |
| 0xE721 | 0x01 | 0x02 | 0x03 | - |
| 0xE722 | 0x01 | 0x02 | 0x03 | - |
| 0xE725 | 0x01 | 0x02 | 0x03 | - |
| 0xE726 | 0x01 | 0x02 | 0x03 | - |
| 0xE728 | 0x01 | 0x02 | 0x03 | - |
| 0xE72A | 0x01 | 0x02 | 0x03 | - |
| 0xE72B | 0x01 | 0x02 | 0x03 | - |
| 0xE72D | 0x01 | 0x02 | 0x03 | - |
| 0xE72E | 0x01 | 0x02 | 0x03 | - |
| 0xE72F | 0x01 | 0x02 | 0x03 | - |
| 0xE730 | 0x01 | 0x02 | 0x03 | - |
| 0xE733 | 0x01 | 0x02 | 0x03 | - |
| 0xE737 | 0x01 | 0x02 | 0x03 | - |
| 0xFFFF | 0x01 | 0x02 | 0x03 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Aussentemperatur | °C | - | unsigned char | - | 1 | 2 | -40 |
| 0x02 | Kuehlmitteltemperatur | °C | - | unsigned char | - | 1 | 1 | -48 |
| 0x03 | Batteriespannung | V | - | unsigned char | - | 1 | 10 | 0 |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 42 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x9C48 | 0x000C | 0x000B | 0x000A | 0x0009 |
| 0x9C4A | 0x000C | 0x000B | 0x000A | 0x0009 |
| 0x9C4D | 0x000C | 0x000B | 0x000A | 0x0009 |
| 0x9C54 | 0x0012 | 0x0012 | 0x0012 | 0x000D |
| 0x9C56 | 0x0012 | 0x0012 | 0x000F | 0x000E |
| 0x9C58 | 0x0012 | 0x0012 | 0x000F | 0x000E |
| 0x9C5F | 0x0012 | 0x0012 | 0x000F | 0x000E |
| 0x9C61 | 0x0012 | 0x0012 | 0x0012 | 0x0013 |
| 0x9C62 | 0x0012 | 0x0012 | 0x000F | 0x000E |
| 0x9C63 | 0x0012 | 0x0012 | 0x0020 | 0x0021 |
| 0x9C6C | 0x0012 | 0x0012 | 0x0020 | 0x0021 |
| 0x9C75 | 0x0012 | 0x0012 | 0x001D | 0x001E |
| 0x9C90 | 0x0016 | 0x0012 | 0x0012 | 0x0012 |
| 0x9CA7 | 0x0012 | 0x0012 | 0x0012 | 0x0017 |
| 0xE704 | 0x0012 | 0x0012 | 0x0012 | 0x0018 |
| 0xE707 | 0x001A | 0x0019 | 0x0012 | 0x0012 |
| 0xE714 | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE715 | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE716 | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE717 | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE718 | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE719 | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE71A | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE71B | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE71C | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE71D | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE71E | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE71F | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE720 | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE721 | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE722 | 0x001C | 0x0012 | 0x0012 | 0x0012 |
| 0xE725 | 0x001C | 0x0012 | 0x0012 | 0x0012 |
| 0xE728 | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE72A | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE72B | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE72D | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE72E | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE72F | 0x001C | 0x0012 | 0x0012 | 0x0012 |
| 0xE730 | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xE733 | 0x001C | 0x0012 | 0x0012 | 0x0012 |
| 0xE737 | 0x001C | 0x001B | 0x0012 | 0x0012 |
| 0xFFFF | 0x0008 | 0x0004 | 0x0002 | 0x0001 |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 31 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x0001 | Signal oder Wert oberhalb Schwelle |
| 0x0002 | Signal oder Wert unterhalb Schwelle |
| 0x0004 | kein Signal oder Wert |
| 0x0008 | unplausibles Signal oder Wert |
| 0x0009 | interner Fehler Stellmotor |
| 0x000A | Blockierung |
| 0x000B | Motor antwortet nicht |
| 0x000C | falsche Schrittweite |
| 0x000D | keine Autoadressierung |
| 0x000E | Kurzschluß gegen Ubatt oder Leitungsunterbrechung |
| 0x000F | Kurzschluß gegen Masse |
| 0x0010 | Kurzschluss gegen Ubatt |
| 0x0011 | Kurzschluss gegen Masse oder Leitungsunterbrechung |
| 0x0012 | nicht verwendet |
| 0x0013 | Überstrom |
| 0x0014 | Blockierung |
| 0x0015 | Powermanagement Eingriff |
| 0x0016 | Steuergerät defekt |
| 0x0017 | Energiesparmode aktiv |
| 0x0018 | Eindrahtbetrieb |
| 0x0019 | Bus Off |
| 0x001A | Error Passiv |
| 0x001B | Timeout |
| 0x001C | ungültige Daten |
| 0x001D | Unterspannung |
| 0x001E | Überspannung |
| 0x001F | unbekannte Fehlerort |
| 0x0020 | Kurzschluß gegen Masse LIN-Versorgung |
| 0x0021 | Kurzschluß gegen Masse SZM-Versorgung |
| 0xFFFF | unbekannte Fehlerort |

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

<a id="table-klimageraettyptab"></a>
### KLIMAGERAETTYPTAB

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | unbekannt |
| 1 | Heizklimagerät IHKR |
| 2 | Heizklimagerät IHKA |
| 3 | ungültige Antwort |

<a id="table-klimabedienteiltyptab"></a>
### KLIMABEDIENTEILTYPTAB

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | unbekannt |
| 1 | Heizklimabedienteil IHKR |
| 2 | Heizklimabedienteil IHKA |
| 3 | ungültige Antwort |

<a id="table-klimasystemfehlertab"></a>
### KLIMASYSTEMFEHLERTAB

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Fehler |
| 2 | falsch codiert |
| 3 | falscher Klimakasten |
| 0xFF | ungültige Antwort |

<a id="table-statuseichlaufallgemeintab"></a>
### STATUSEICHLAUFALLGEMEINTAB

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | in diesem Klemmenzyklus (auch Klemme 30 Reset) noch nicht gestartet |
| 1 | Eichlauf läuft gerade |
| 2 | Eichlauf abgeschlossen IO |
| 3 | Eichlauf abgeschlossen NIO |
| 4 | ungültige Antwort |

<a id="table-statuseichlaufhistorytab"></a>
### STATUSEICHLAUFHISTORYTAB

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine gültigen Schrittweiten / keine History vorhanden |
| 16 | gültige Schrittweiten vorhanden |
| 32 | ungültige Antwort |

<a id="table-statuseichlaufmotortab"></a>
### STATUSEICHLAUFMOTORTAB

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | NIO |
| 1 | IO |
| 2 | Klappe nicht verbaut / nicht relevant |
| 3 | ungültige Antwort |

<a id="table-statusverstellbereichtab"></a>
### STATUSVERSTELLBEREICHTAB

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Verstellbereiche ungültig - Verwendung von Defaultwerten |
| 1 | Verstellbereiche gültig |
| 2 | ungültige Antwort |

<a id="table-linmotortab"></a>
### LINMOTORTAB

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x21 | Motor Zentralgetriebe |
| 0x22 | Frischluft-Umluft-Motor |
| 0x28 | Mischluftmotor |

<a id="table-ioporttab"></a>
### IOPORTTAB

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Tasten |
| 0x02 | Funktionsbeleuchtung |
| 0x03 | Tasten SZM |
| 0x04 | Funktionsbeleuchtung SZM |
| 0x05 | PWM Funktionsbeleuchtung |
| 0x06 | PWM Hintergrundbeleuchtung |
| 0x07 | 12V Ausgang |
| 0x08 | Gebläse |
| 0x09 | heizbare Heckscheibe (CAN) |
| 0x0A | Kompressorventil (CAN) |
| 0x0B | Kompressorkupplung |
| 0x0C | Zusatzwasserpumpe (CAN) |
| 0x0D | elektrische Wasserpumpe (CAN) |
| 0x0E | Diagnosetestbetrieb  permanent |
| 0x21 | Klappe Zentralantrieb |
| 0x22 | Klappe Frischluft/Umluft |
| 0x23 | Mischluftklappe |

<a id="table-analogporttab"></a>
### ANALOGPORTTAB

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0B | SZM-Variante |
| 0x11 | Sensoren |
| 0x12 | Analog Spannungen |
| 0x13 | Drehsteller Sollwerte |
| 0x14 | Ausgänge SZM |

<a id="table-fastablocktab"></a>
### FASTABLOCKTAB

Dimensions: 17 rows × 2 columns

| BLOCKNUMBER | BLOCKNAME |
| --- | --- |
| 0x00 | Gesamtbetriebsstunden |
| 0x01 | Anzahl der Resets |
| 0x02 | Richtungswechsel Mischluft |
| 0x03 | Richtungswechsel Frischluft/Umluft |
| 0x04 | Richtungswechsel Zentralgetriebe |
| 0x05 | Blockierungen Mischluft |
| 0x06 | Blockierungen Frischluft/Umluft |
| 0x07 | Aktivierungen Mikroschalter |
| 0x08 | Betriebsstunden Klimabetrieb |
| 0x09 | Betriebsstunden OFF-Funktion |
| 0x0A | Aktivierungen der OFF-Funktion |
| 0x19 | Zähler PCB temperature übersteigt 85°C |
| 0x1A | Zähler PCB temperature übersteigt 95°C |
| 0x1B | Zähler PCB temperature übersteigt 105°C |
| 0x1C | Anzahl der Power Management limitierung an die Heckscheibe Heizung |
| 0x1D | Anzahl der Power Management limitierung an die Gebläse |
| 0x1E | Anzahl der Motor Eichlauf |

<a id="table-statusstepperaddrprog"></a>
### STATUSSTEPPERADDRPROG

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | NOK |
| 1 | OK |

<a id="table-statusstepperroutinestatus"></a>
### STATUSSTEPPERROUTINESTATUS

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | inaktiv |
| 1 | aktiv |

<a id="table-statusstepperroutineresult"></a>
### STATUSSTEPPERROUTINERESULT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Nicht erfolgreich |
| 1 | Erfolgreich |

<a id="table-statuseichlaufiotab"></a>
### STATUSEICHLAUFIOTAB

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Eichlauf NIO |
| 32 | Eichlauf IO |
| 64 | ungültige Antwort |
