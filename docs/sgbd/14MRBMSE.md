# 14MRBMSE.prg

- Jobs: [160](#jobs)
- Tables: [24](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MRBMSE |
| ORIGIN | BMW_Motorrad UX-EE-1 Stefan Krimmer |
| REVISION | 14.000 |
| AUTHOR | MM Motorbike Fabio_Felici, MM Motorbike Walter_Geri, BMW_Motorr |
| COMMENT | N/A |
| PACKAGE | 1.53 |
| SPRACHE | English |

## Jobs

### Index

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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [C_CI_LESEN](#job-c-ci-lesen) - Codierindex lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $9B Vehicle Manufacturer Coding Index oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_LESEN](#job-zif-lesen) - Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_BACKUP_LESEN](#job-zif-backup-lesen) - Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [PHYSIKALISCHE_HW_NR_LESEN](#job-physikalische-hw-nr-lesen) - Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [HARDWARE_REFERENZ_LESEN](#job-hardware-referenz-lesen) - Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [DATEN_REFERENZ_LESEN](#job-daten-referenz-lesen) - Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DREF Modus  : Default
- [FLASH_ZEITEN_LESEN](#job-flash-zeiten-lesen) - Auslesen der Flash Loeschzeit, Signaturtestzeit, Authentisierberechnungszeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier $2501 Zeiten Modus  : Default
- [FLASH_BLOCKLAENGE_LESEN](#job-flash-blocklaenge-lesen) - Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default
- [FLASH_PROGRAMMIER_STATUS_LESEN](#job-flash-programmier-status-lesen) - Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [FLASH_LOESCHEN](#job-flash-loeschen) - Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default
- [FLASH_SCHREIBEN_ADRESSE](#job-flash-schreiben-adresse) - Vorbereitung fuer Flash schreiben Standard Flashjob KWP2000: $34 RequestDownload Modus  : Default
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Flash Daten schreiben Standard Flashjob KWP2000: $36 TransferData Modus  : Default
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Flashprogrammierung abschliessen Standard Flashjob KWP2000: $37 RequestTransferExit Modus  : Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [AIF_SCHREIBEN](#job-aif-schreiben) - Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default
- [BAUDRATE_115200](#job-baudrate-115200) - Umschaltung auf 115200 Baud (und BMW-FAST wg. Fast-Initialisation)
- [NG_FLASH_LOESCHEN](#job-ng-flash-loeschen) - Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default
- [FLASH_CHECKSUMME](#job-flash-checksumme) - Flash Checksumme pruefen KWP2000: $31 StartRoutineByLocalIdentifier $01 CheckCodingChecksum $02 Program (Application Code), $04 Data (Calibration Code) Modus  : Default
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [FLASH_SCHREIBEN_XXL](#job-flash-schreiben-xxl) - Flash Daten schreiben XXL-Format Standard Flashjob KWP2000: $36 TransferData Modus  : Default
- [SEED_KEY](#job-seed-key) - Security Access KWP2000: $27 Security Access Request $03 to $04 Access Mode
- [C_FA_LESEN](#job-c-fa-lesen) - Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 vehicle order Modus  : Default
- [C_FA_SCHREIBEN](#job-c-fa-schreiben) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 Fahrzeugauftrag Modus  : Default
- [C_FA_AUFTRAG](#job-c-fa-auftrag) - Fahrzeugauftrag schreiben und zuruecklesen KWP2000: $2E   WriteDataByCommonIdentifier $3F00 vehicle order KWP2000: $22   ReadDataByCommonIdentifier $3F00 vehicle order Modus  : Default
- [C_FG_LESEN](#job-c-fg-lesen) - 7-stellige Fahrgestellnummer lesen KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0x1010 Modus   : Default
- [STATUS_BOOT_VERSION](#job-status-boot-version) - Identdaten KWP2000: $1A ReadBootVersion Modus  : Default
- [STATUS_LIEFERUNG_VERSION](#job-status-lieferung-version) - Software Delivery Type KWP2000: $22 ReadDataByCommonIdentifier $1020 Read Software Delivery Type Modus  : Default
- [STATUS_SW_CALIB_VERSION](#job-status-sw-calib-version) - Software Ident KWP2000: $22 ReadDataByCommonIdentifier $2510 Read Software and Calibration Version Modus  : Default
- [STATUS_DIGITAL_KL15](#job-status-digital-kl15) - Status Klemme 15 KWP2000: $22 ReadDataByCommonIdentifier $0031 Status Digital Klemme 15 Modus  : Default
- [STATUS_ROHWERT_BATTERIESPANNUNG](#job-status-rohwert-batteriespannung) - Bordnetzspannung Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0006 Battery Voltage (raw) Modus  : Default
- [STATUS_BATTERIESPANNUNG](#job-status-batteriespannung) - Bordnetzspannung KWP2000: $22 ReadDataByCommonIdentifier $0007 Battery Voltage (processed) Modus  : Default
- [STATUS_ROHWERT_BREMSE](#job-status-rohwert-bremse) - Spannung Bremsschalter Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0020 Brake Switch input voltage Modus  : Default
- [STATUS_DIGITAL_BREMSE](#job-status-digital-bremse) - Status Bremsschalter KWP2000: $22 ReadDataByCommonIdentifier $0021 Status Digital Bremse Modus  : Default
- [STATUS_DIGITAL_KILL_SCHALTER](#job-status-digital-kill-schalter) - Status Kill-Schalter KWP2000: $22 ReadDataByCommonIdentifier $0032 Status Digital Kill-Schalter Modus  : Default
- [STATUS_DIGITAL_START_SCHALTER](#job-status-digital-start-schalter) - Status Start-Schalter KWP2000: $22 ReadDataByCommonIdentifier $0033 Status Digital Start-Schalter Modus  : Default
- [STATUS_ROHWERT_DROSSELKLAPPE](#job-status-rohwert-drosselklappe) - Spannung Drosselklappe Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0000 TPS Voltage Modus  : Default
- [STATUS_ROHWERT_DROSSELKLAPPE_ADAPTIERT](#job-status-rohwert-drosselklappe-adaptiert) - Spannung Drosselklappe Rohwert Adaptiert KWP2000: $22 ReadDataByCommonIdentifier $0005 TPS Voltage Adapted Modus  : Default
- [STATUS_DROSSELKLAPPENWINKEL](#job-status-drosselklappenwinkel) - Drosselklappenwinkel KWP2000: $22 ReadDataByCommonIdentifier $0004 TPS Angle Modus  : Default
- [STATUS_DROSSELKLAPPENPOSITION](#job-status-drosselklappenposition) - Drosselklappenposition KWP2000: $22 ReadDataByCommonIdentifier $0001 TPS percentage Modus  : Default
- [STATUS_ROHWERT_GETRIEBEEINGANG](#job-status-rohwert-getriebeeingang) - Spannung Getriebeeingang Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0014 Gear input Voltage Modus  : Default
- [STATUS_DIGITAL_NEUTRALSCHALTER](#job-status-digital-neutralschalter) - Status Neutralschalter KWP2000: $22 ReadDataByCommonIdentifier $0015 Status Digital Neutralschalter Modus  : Default
- [STATUS_DIGITAL_GANG](#job-status-digital-gang) - Status Gang KWP2000: $22 ReadDataByCommonIdentifier $0025 Status Digital Gang Modus  : Default
- [STATUS_ROHWERT_SSA](#job-status-rohwert-ssa) - Spannung Seitenstuetze E Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0022 Side-stand Switch 1 Voltage Modus  : Default
- [STATUS_ROHWERT_SSA2](#job-status-rohwert-ssa2) - Spannung Seitenstuetze A Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0023 Side-stand Switch 2 Voltage Modus  : Default
- [STATUS_ROHWERT_KUPPLUNGSSCHALTER](#job-status-rohwert-kupplungsschalter) - Spannung Kupplungseingang Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0026 Clutch switch input Voltage Modus  : Default
- [STATUS_KUPPLUNGSSCHALTER](#job-status-kupplungsschalter) - Status Kupplungsschalter KWP2000: $22 ReadDataByCommonIdentifier $0027 Status Kupplungsschalter Modus  : Default
- [STATUS_DIGITAL_SEITENSTUETZE](#job-status-digital-seitenstuetze) - Status Seitenstuetze KWP2000: $22 ReadDataByCommonIdentifier $0024 Status Digital Seitenstuetze Modus  : Default
- [STATUS_DIGITAL_OELNIVEAUSCHALTER](#job-status-digital-oelniveauschalter) - Status Oelniveauschalter KWP2000: $22 ReadDataByCommonIdentifier $0041 Status Digital Oelniveauschalter Modus  : Default
- [STATUS_OELNIVEAU](#job-status-oelniveau) - Status Oelniveau KWP2000: $22 ReadDataByCommonIdentifier $0042 Oil Level Status Modus  : Default
- [STATUS_DIGITAL_ABS_TASTER](#job-status-digital-abs-taster) - Status ABS Taster KWP2000: $22 ReadDataByCommonIdentifier $0028 Status Digital ABS Taster Modus  : Default
- [STATUS_ROHWERT_OELTEMPERATUR](#job-status-rohwert-oeltemperatur) - Spannung Oeltemperatur Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0016 Oil Temperature Voltage Modus  : Default
- [STATUS_OELTEMPERATUR](#job-status-oeltemperatur) - Oeltemperatur KWP2000: $22 ReadDataByCommonIdentifier $0017 Oil Temperature Modus  : Default
- [STATUS_ROHWERT_KUEHLWASSERTEMPERATUR](#job-status-rohwert-kuehlwassertemperatur) - Spannung Kuehlwassertemperatur Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0008 Coolant Temperature Sensor Voltage Modus  : Default
- [STATUS_KUEHLWASSERTEMPERATUR](#job-status-kuehlwassertemperatur) - Kuehlwassertemperatur KWP2000: $22 ReadDataByCommonIdentifier $0009 Coolant Temperature Modus  : Default
- [STATUS_ROHWERT_ANSAUGLUFTTEMPERATUR](#job-status-rohwert-ansauglufttemperatur) - Spannung Ansauglufttemperatur Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0010 Air Temperature Sensor Voltage Modus  : Default
- [STATUS_ANSAUGLUFTTEMPERATUR](#job-status-ansauglufttemperatur) - Ansauglufttemperatur KWP2000: $22 ReadDataByCommonIdentifier $0011 Air Temperature Modus  : Default
- [STATUS_ROHWERT_LAMBDA](#job-status-rohwert-lambda) - Spannung Lambda Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0012 Lambda Sensor Voltage Modus  : Default
- [STATUS_LAMBDA](#job-status-lambda) - Status Lambda KWP2000: $22 ReadDataByCommonIdentifier $0013 Status Lambda Modus  : Default
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Motordrehzahl KWP2000: $22 ReadDataByCommonIdentifier $0100 Engine Speed Modus  : Default
- [STATUS_FAHRZEUGGESCHWINDIGKEIT](#job-status-fahrzeuggeschwindigkeit) - Status Fahrzeuggeschwindigkeit KWP2000: $22 ReadDataByCommonIdentifier $0101 Fahrzeuggeschwindigkeit Modus  : Default
- [STATUS_DIGITAL_LASTRELAIS](#job-status-digital-lastrelais) - Status Lastrelais KWP2000: $22 ReadDataByCommonIdentifier $0061 Status Digital Lastrelais Modus  : Default
- [STATUS_DIGITAL_START_RELAIS](#job-status-digital-start-relais) - Status Start-Relais KWP2000: $22 ReadDataByCommonIdentifier $0062 Status Digital Start-Relais Modus  : Default
- [STATUS_DIGITAL_EKP_RELAIS](#job-status-digital-ekp-relais) - Status EKP-Relais KWP2000: $22 ReadDataByCommonIdentifier $0060 Status Digital EKP-Relais Modus  : Default
- [STATUS_DIGITAL_LUEFTERRELAIS](#job-status-digital-luefterrelais) - Status Luefterrelais KWP2000: $22 ReadDataByCommonIdentifier $0063 Status Digital Luefterrelais Modus  : Default
- [STATUS_TEV](#job-status-tev) - Status TEV KWP2000: $22 ReadDataByCommonIdentifier $0185 PWM TEV Modus  : Default
- [STATUS_EINSPRITZDAUER_ZYL1](#job-status-einspritzdauer-zyl1) - Status Einspritzventil 1 KWP2000: $22 ReadDataByCommonIdentifier $0110 Einspritzdauer Zylinder 1 Modus  : Default
- [STATUS_EINSPRITZDAUER_ZYL2](#job-status-einspritzdauer-zyl2) - Status Einspritzventil 2 KWP2000: $22 ReadDataByCommonIdentifier $0111 Einspritzdauer Zylinder 2 Modus  : Default
- [STATUS_DIGITAL_UEBERTEMPERATURWARNLEUCHTE](#job-status-digital-uebertemperaturwarnleuchte) - Status Uebertemperaturwarnleuchte KWP2000: $22 ReadDataByCommonIdentifier $0108 Status Digital Uebertemperaturwarnleuchte Modus  : Default
- [STATUS_ZUENDZEITPUNKT_ZYL1](#job-status-zuendzeitpunkt-zyl1) - Status Zuendzeitpunkt Zyl. 1 KWP2000: $22 ReadDataByCommonIdentifier $0120 Zuendzeitpunkt Zylinder 1 Modus  : Default
- [STATUS_SCHLIESSZEIT_ZYL1](#job-status-schliesszeit-zyl1) - Status Schliesszeit Zyl. 1 KWP2000: $22 ReadDataByCommonIdentifier $0130 Schliesszeit Zylinder 1 Modus  : Default
- [STATUS_ZUENDZEITPUNKT_ZYL2](#job-status-zuendzeitpunkt-zyl2) - Status Zuendzeitpunkt Zyl. 2 KWP2000: $22 ReadDataByCommonIdentifier $0121 Zuendzeitpunkt Zylinder 2 Modus  : Default
- [STATUS_SCHLIESSZEIT_ZYL2](#job-status-schliesszeit-zyl2) - Status Schliesszeit Zyl. 2 KWP2000: $22 ReadDataByCommonIdentifier $0131 Schliesszeit Zylinder 2 Modus  : Default
- [STATUS_ABGASKLAPPE](#job-status-abgasklappe) - Status Abgasklappenposition KWP2000: $22 ReadDataByCommonIdentifier $0186 Abgasklappenposition Modus  : Default
- [STATUS_LAM1_HZ](#job-status-lam1-hz) - Status Lambdasondenheizung KWP2000: $22 ReadDataByCommonIdentifier $0190 PWM Lambdasondenheizung Modus  : Default
- [STATUS_STEPPERMOTOR](#job-status-steppermotor) - Status Steppermotorposition KWP2000: $22 ReadDataByCommonIdentifier $0090 Stepper Motor Position Modus  : Default
- [STATUS_ROHWERT_UMGEBUNGSDRUCK](#job-status-rohwert-umgebungsdruck) - Spannung Umgebungsdruck Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0002 Atmospheric Pressure Sensor Voltage Modus  : Default
- [STATUS_UMGEBUNGSDRUCK](#job-status-umgebungsdruck) - Status Umgebungsdruck KWP2000: $22 ReadDataByCommonIdentifier $0003 Umgebungsdruck Modus  : Default
- [STATUS_VORDERRADGESCHWINDIGKEIT](#job-status-vorderradgeschwindigkeit) - Status Vorderradgeschwindigkeit KWP2000: $22 ReadDataByCommonIdentifier $0103 Geschwindigkeit Vorderrad Modus  : Default
- [STATUS_HINTERRADGESCHWINDIGKEIT](#job-status-hinterradgeschwindigkeit) - Status Hinterradgeschwindigkeit KWP2000: $22 ReadDataByCommonIdentifier $0104 Geschwindigkeit Hinterrad Modus  : Default
- [STATUS_LEERLAUFDREHZAHL_SOLL](#job-status-leerlaufdrehzahl-soll) - Status Sollleerlaufdrehzahl KWP2000: $22 ReadDataByCommonIdentifier $0105 Leerlaufdrehzahl Soll Modus  : Default
- [STATUS_LEERLAUFADAPTIONSWERT](#job-status-leerlaufadaptionswert) - Status Leerlaufadaptionswert KWP2000: $22 ReadDataByCommonIdentifier $0106 Leerlaufadaptionswert (Stepper) Modus  : Default
- [STATUS_DIGITAL_LAMBDASONDENHEIZUNG](#job-status-digital-lambdasondenheizung) - Status Lambdasondenheizung KWP2000: $22 ReadDataByCommonIdentifier $0064 Status Digital Lambdasondenheizung Modus  : Default
- [STATUS_LAMBDAREGELFAKTOR](#job-status-lambdaregelfaktor) - Status Lambdaregelfaktor KWP2000: $22 ReadDataByCommonIdentifier $0065 Lambdaregelfaktor Modus  : Default
- [STATUS_LAMBDAREGELADAPTION](#job-status-lambdaregeladaption) - Status Lambdaregeladaption KWP2000: $22 ReadDataByCommonIdentifier $0066 Lambdaregeladaption Modus  : Default
- [STATUS_DIGITAL_LAMBDAREGELUNG](#job-status-digital-lambdaregelung) - Status Lambdaregelung KWP2000: $22 ReadDataByCommonIdentifier $0067 Status Digital Lambdaregelung Modus  : Default
- [STATUS_DIGITAL_MOTORLAST](#job-status-digital-motorlast) - Status Motorlast KWP2000: $22 ReadDataByCommonIdentifier $0068 Status Digital Motorlast Modus  : Default
- [STATUS_DROSSELKLAPPENADAPTION_ZU](#job-status-drosselklappenadaption-zu) - Status Drosselklappenadaption Zu KWP2000: $22 ReadDataByCommonIdentifier $0018 Drosselklappenadaption Position Zu Modus  : Default
- [STATUS_DROSSELKLAPPENADAPTION_AUF](#job-status-drosselklappenadaption-auf) - Status Drosselklappenadaption Auf KWP2000: $22 ReadDataByCommonIdentifier $0019 Drosselklappenadaption Position Auf Modus  : Default
- [STATUS_GANGADAPTION_GANG_1](#job-status-gangadaption-gang-1) - Status Gangadaption 1 KWP2000: $22 ReadDataByCommonIdentifier $0141 Adaptionswert Gang 1 Modus  : Default
- [STATUS_GANGADAPTION_GANG_2](#job-status-gangadaption-gang-2) - Status Gangadaption 2 KWP2000: $22 ReadDataByCommonIdentifier $0142 Adaptionswert Gang 2 Modus  : Default
- [STATUS_GANGADAPTION_GANG_3](#job-status-gangadaption-gang-3) - Status Gangadaption 3 KWP2000: $22 ReadDataByCommonIdentifier $0143 Adaptionswert Gang 3 Modus  : Default
- [STATUS_GANGADAPTION_GANG_4](#job-status-gangadaption-gang-4) - Status Gangadaption 4 KWP2000: $22 ReadDataByCommonIdentifier $0144 Adaptionswert Gang 4 Modus  : Default
- [STATUS_GANGADAPTION_GANG_5](#job-status-gangadaption-gang-5) - Status Gangadaption 5 KWP2000: $22 ReadDataByCommonIdentifier $0145 Adaptionswert Gang 5 Modus  : Default
- [STATUS_GANGADAPTION_GANG_6](#job-status-gangadaption-gang-6) - Status Gangadaption 6 KWP2000: $22 ReadDataByCommonIdentifier $0146 Adaptionswert Gang 6 Modus  : Default
- [STATUS_FAHRZEUGMODUS_SOLL](#job-status-fahrzeugmodus-soll) - Status Fahrzeugmodus Soll KWP2000: $22 ReadDataByCommonIdentifier $0151 Status Fahrzeugmodus Soll Modus  : Default
- [STATUS_FAHRZEUGMODUS_IST](#job-status-fahrzeugmodus-ist) - Status Fahrzeugmodus IST KWP2000: $22 ReadDataByCommonIdentifier $0152 Status Fahrzeugmodus IST Modus  : Default
- [STATUS_DIGITAL_STARTFREIGABE](#job-status-digital-startfreigabe) - Status Startfreigabe KWP2000: $22 ReadDataByCommonIdentifier $0070 Status Digital Startfreigabe Modus  : Default
- [STATUS_DIGITAL_EWS_FREIGABE](#job-status-digital-ews-freigabe) - Status EWS-Freigabe KWP2000: $22 ReadDataByCommonIdentifier $0071 Status Digital EWS-Freigabe Modus  : Default
- [STATUS_DIGITAL_MOTORWARNLEUCHTE](#job-status-digital-motorwarnleuchte) - Status Motorwarnleuchte KWP2000: $22 ReadDataByCommonIdentifier $0072 Status Digital Motorwarnleuchte Modus  : Default
- [STATUS_DIGITAL_SHOWROOMMODUS](#job-status-digital-showroommodus) - Status Showroommodus KWP2000: $22 ReadDataByCommonIdentifier $1021 Status Digital Showroommodus Modus  : Default
- [STATUS_GEMISCHADAPTION](#job-status-gemischadaption) - Fuel Adaption Table Reading KWP2000: $22 ReadDataByCommonIdentifier $0300 ReadWarmAdaptionTable $0301 ReadColdAdaptionTable Modus  : Default
- [STATUS_DIGITAL_GEPAECKFACH](#job-status-digital-gepaeckfach) - Status Gepaeckfach KWP2000: $22 ReadDataByCommonIdentifier $0073 Status Digital Gepaeckfach Modus  : Default
- [STATUS_DIGITAL_SYNCRO](#job-status-digital-syncro) - Status Motorsyncronization KWP2000: $22 ReadDataByCommonIdentifier $0076 Status Digital Syncro Modus  : Default
- [STATUS_EWS](#job-status-ews) - KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC000 Zurücklesen verschiedener interner Stati für EWS
- [STATUS_EWS4_SK](#job-status-ews4-sk) - KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC002 Lesen des SecretKey des Server sowie Client für EWS4
- [STEUERN_EWS4_SK](#job-steuern-ews4-sk) - 17 "EWS4-data" schreiben KWP 2000: $2E WriteDataByCommonIdentifier CommonIdentifier=0xC001
- [STATUS_HIREVCNT](#job-status-hirevcnt) - KWP2000: $22 ReadDataByCommonIdentifier $0501 Modus  : Default
- [STATUS_GWSZ_ANZEIGE](#job-status-gwsz-anzeige) - Lesen des Kilometerstandes KWP2000:    $22   ReadDataByCommonIdentifier $C010 "redundanter Kilometerstand" Modus:      Default
- [STEUERN_GWSZ_ANZEIGE_SCHREIBEN](#job-steuern-gwsz-anzeige-schreiben) - Schreiben des Kilometerstandes KWP2000:    $2E   WriteDataByCommonIdentifier $C011 "redundanter Kilometerstand schreiben" Modus:      Default
- [STATUS_SERVICE_RESTWEG](#job-status-service-restweg) - redundanten BMSKP KM-Zaehlerstand bis zum naechsten Service auslesen KWP2000: $22   ReadDataByCommonIdentifier $C030 Local-ID für Lesen SERVKM zusaetzlich wird noch der BMSKP interne KM-Stand ausgelesen daraus wird die Differenz (Intervall/Zaehlerstand) berechnet  KWP2000: $22   ReadDataByCommonIdentifier KWP2000: $C010 Local-ID für internen KM-Stand lesen
- [STEUERN_SERVICE_RESTWEG](#job-steuern-service-restweg) - redundanten BMSKP KM-Zaehlerstand bis zum naechsten Service setzen KWP2000: $2E   WriteDataByCommonIdentifier $C031 Local-ID für Service Datum (SERVKM) schreiben [km] zusaetzlich wird noch der BMSKP interne KM-Stand ausgelesen dazu wird das Intervall/Zaehlerstand addiert  KWP2000: $22   ReadDataByCommonIdentifier KWP2000: $C010 Local-ID für internen KM-Stand lesen
- [STATUS_SERVICE_DATE](#job-status-service-date) - redundantes Service-Datum aus BMSKP auslesen KWP2000: $22   ReadDataByCommonIdentifier $C032 Local-ID für Lesen SERVDAT
- [STEUERN_SERVICE_DATE](#job-steuern-service-date) - redundantes Service-Datum in BMSKP Setzen KWP2000: $2E   WriteDataByCommonIdentifier $C033 Local-ID für Service Datum (SERVDAT) schreiben
- [STATUS_FAHRGESTELLNUMMER](#job-status-fahrgestellnummer) - 17 ASCII Byte Fahrgestell-Nummer KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0x1010 Modus   : Default
- [STEUERN_FAHRGESTELLNUMMER](#job-steuern-fahrgestellnummer) - 17 ASCII "Fahrgestellnummer" schreiben KWP2000: $2E WriteDataByCommonIdentifier CommonIdentifier=$1010 Full Vehicle Identification Number Modus  : Default
- [STEUERN_LASTRELAIS](#job-steuern-lastrelais) - Steuern Lastrelais KWP2000: $31 StartRoutineByLocalIdentifier $A1 Start Routine Activation Load Relay Modus  : Default
- [STEUERN_ENDE_LASTRELAIS](#job-steuern-ende-lastrelais) - Steuern Ende Lastrelais KWP2000: $32 StopRoutineByLocalIdentifier $A1 Stop Routine Activation Load Relay Modus  : Default
- [STEUERN_EKP_RELAIS](#job-steuern-ekp-relais) - Steuern EKP-Relais KWP2000: $31 StartRoutineByLocalIdentifier $A7 Start Routine Activation Fuel Pump Relay Modus  : Default
- [STEUERN_ENDE_EKP_RELAIS](#job-steuern-ende-ekp-relais) - Steuern Ende EKP-Relais KWP2000: $32 StopRoutineByLocalIdentifier $A7 Stop Routine Activation Fuel Pump Relay Modus  : Default
- [STEUERN_LUEFTERRELAIS](#job-steuern-luefterrelais) - Steuern Luefterrelais KWP2000: $31 StartRoutineByLocalIdentifier $A8 Start Routine Activation Fan Relay Modus  : Default
- [STEUERN_ENDE_LUEFTERRELAIS](#job-steuern-ende-luefterrelais) - Steuern Ende Luefterrelais KWP2000: $32 StopRoutineByLocalIdentifier $A8 Stop Routine Activation Fan Relay Modus  : Default
- [STEUERN_TEV](#job-steuern-tev) - Steuern TEV KWP2000: $31 StartRoutineByLocalIdentifier $A6 Start Routine Activation Canister Valve Modus  : Duty Cycle 15%, frequency 12Hz, up to timeout of 10s
- [STEUERN_ENDE_TEV](#job-steuern-ende-tev) - Steuern Ende TEV KWP2000: $32 StopRoutineByLocalIdentifier $A6 Stop Routine Activation Canister Valve Modus  : Stop immediately the active diagnosis test of the Canister Valve
- [STEUERN_EV1](#job-steuern-ev1) - Steuern EV1 KWP2000: $31 StartRoutineByLocalIdentifier $A5 Start Routine Activation Injection cyl 1 Modus  : ton = 1.2 ms, toff = 98.8 ms, frequency 10Hz, up to timeout of 10s
- [STEUERN_ENDE_EV1](#job-steuern-ende-ev1) - Steuern Ende EV1 KWP2000: $32 StopRoutineByLocalIdentifier $A5 Stop Routine Activation Injection cyl 1 Modus  : Stop immediately the activation of the injection cyl 1
- [STEUERN_EV2](#job-steuern-ev2) - Steuern EV2 KWP2000: $31 StartRoutineByLocalIdentifier $AB Start Routine Activation Injection cyl 2 Modus  : ton = 1.2 ms, toff = 98.8 ms, frequency 10Hz, up to timeout of 10s
- [STEUERN_ENDE_EV2](#job-steuern-ende-ev2) - Steuern Ende EV2 KWP2000: $32 StopRoutineByLocalIdentifier $AB Stop Routine Activation Injection cyl 2 Modus  : Stop immediately the activation of the injection cyl 2
- [STEUERN_UEBERTEMPERATURLEUCHTE](#job-steuern-uebertemperaturleuchte) - Steuern Uebertemperaturleuchte KWP2000: $31 StartRoutineByLocalIdentifier $AD Start Routine Activation Temperature Warning Lamp Modus  : The Warning Lamp Flashes with Duty Cycle 50%, frequency 1Hz, up to timeout of 10s
- [STEUERN_ENDE_UEBERTEMPERATURLEUCHTE](#job-steuern-ende-uebertemperaturleuchte) - Steuern Ende Uebertemperaturleuchte KWP2000: $32 StopRoutineByLocalIdentifier $AD Stop Routine Activation Temperature Warning Lamp Modus  : Stop immediately the activation of the Temperature Warning Lamp
- [STEUERN_ABGASKLAPPE](#job-steuern-abgasklappe) - Steuern Abgasklappe KWP2000: $31 StartRoutineByLocalIdentifier $AA Start Routine Activation Exhaust Valve Modus  : The target duty cycle is 5% for the first 5s and 95% for the next 5s, the timeout is 10s
- [STEUERN_ENDE_ABGASKLAPPE](#job-steuern-ende-abgasklappe) - Steuern Ende Abgasklappe KWP2000: $32 StopRoutineByLocalIdentifier $AA Stop Routine Activation Exhaust Valve Modus  : Stop immediately the active diagnosis test of the Exhaust Valve
- [STEUERN_LAMBDASONDENHEIZUNG](#job-steuern-lambdasondenheizung) - Steuern Lambdasondenheizung KWP2000: $31 StartRoutineByLocalIdentifier $AF Start Routine Activation O2 Heater Modus  : Duty Cycle 50%, frequency 12Hz, up to timeout of 10s
- [STEUERN_ENDE_LAMBDASONDENHEIZUNG](#job-steuern-ende-lambdasondenheizung) - Steuern Ende Lambdasondenheizung KWP2000: $32 StopRoutineByLocalIdentifier $AF Stop Routine Activation O2 Heater Modus  : Stop immediately the active diagnosis test of the O2 Heater
- [STEUERN_STEPPERMOTOR](#job-steuern-steppermotor) - Steuern Steppermotor KWP2000: $31 StartRoutineByLocalIdentifier $A9 Start Routine Activation of the Stepper Motor Modus  : The target position is 87.5% for the first 4s and 4% for the next 6s, the timeout is 10s
- [STEUERN_ENDE_STEPPERMOTOR](#job-steuern-ende-steppermotor) - Steuern Ende Steppermotor KWP2000: $32 StopRoutineByLocalIdentifier $A9 Stop Routine Activation of the Stepper Motor Modus  : Stop immediately the active diagnosis test of the Stepper Motor
- [STEUERN_MOTORWARNLEUCHTE](#job-steuern-motorwarnleuchte) - Steuern Motorwarnleuchte KWP2000: $31 StartRoutineByLocalIdentifier $AC Start Routine Activation Engine Warning Lamp Modus  : The Warning Lamp Flashes with Duty Cycle 50%, frequency 1Hz, up to timeout of 10s
- [STEUERN_ENDE_MOTORWARNLEUCHTE](#job-steuern-ende-motorwarnleuchte) - Steuern Ende Motorwarnleuchte KWP2000: $32 StopRoutineByLocalIdentifier $AC Stop Routine Activation Engine Warning Lamp Modus  : Stop immediately the activation of the Engine Warning Lamp
- [STEUERN_SHOWROOMMODUS](#job-steuern-showroommodus) - Steuern Showroom Modus KWP2000: $31 StartRoutineByLocalIdentifier $29 Start Routine Activation of the Showroom Modus
- [STEUERN_ENDE_SHOWROOMMODUS](#job-steuern-ende-showroommodus) - Steuern Ende Showroom Modus KWP2000: $32 StopRoutineByLocalIdentifier $29 Stop Routine Activation of the Showroom Modus
- [STEUERN_ADAPTIONSWERTE_LOESCHEN](#job-steuern-adaptionswerte-loeschen) - Steuern Adaptionswerte Loeschen KWP2000: $31 StartRoutineByLocalIdentifier $A0 Delete All Adaption Values Modus  : Default
- [STEUERN_ZERO_TPS](#job-steuern-zero-tps) - Steuern Zero TPS KWP2000: $31 StartRoutineByLocalIdentifier $21 Learning of the Idle TPS position KWP2000: $33 ReadRoutineResultByLocalIdentifier Modus  : Default
- [STEUERN_RESET_STEPPER](#job-steuern-reset-stepper) - Steuern Reset Stepper KWP2000: $31 StartRoutineByLocalIdentifier $22 Reset Stepper KWP2000: $33 ReadRoutineResultByLocalIdentifier Modus  : Default
- [STEUERN_NEUTRALGANG_ADAPTION](#job-steuern-neutralgang-adaption) - Steuern Neutralgang Adaption KWP2000: $31 StartRoutineByLocalIdentifier $23 Gear Self-learning procedure KWP2000: $33 ReadRoutineResultByLocalIdentifier Modus  : Default

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

<a id="job-baudrate-115200"></a>
### BAUDRATE_115200

Umschaltung auf 115200 Baud (und BMW-FAST wg. Fast-Initialisation)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-ng-flash-loeschen"></a>
### NG_FLASH_LOESCHEN

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

<a id="job-flash-checksumme"></a>
### FLASH_CHECKSUMME

Flash Checksumme pruefen KWP2000: $31 StartRoutineByLocalIdentifier $01 CheckCodingChecksum $02 Program (Application Code), $04 Data (Calibration Code) Modus  : Default

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

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-flash-schreiben-xxl"></a>
### FLASH_SCHREIBEN_XXL

Flash Daten schreiben XXL-Format Standard Flashjob KWP2000: $36 TransferData Modus  : Default

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

<a id="job-seed-key"></a>
### SEED_KEY

Security Access KWP2000: $27 Security Access Request $03 to $04 Access Mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-c-fa-lesen"></a>
### C_FA_LESEN

Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 vehicle order Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string | Daten des Fahrzeugauftrages |
| SPEICHER_STATUS | string | BELEGT bzw. UNBELEGT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-schreiben"></a>
### C_FA_SCHREIBEN

Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 Fahrzeugauftrag Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-auftrag"></a>
### C_FA_AUFTRAG

Fahrzeugauftrag schreiben und zuruecklesen KWP2000: $2E   WriteDataByCommonIdentifier $3F00 vehicle order KWP2000: $22   ReadDataByCommonIdentifier $3F00 vehicle order Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string | max Laenge 200 Byte |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

7-stellige Fahrgestellnummer lesen KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0x1010 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-boot-version"></a>
### STATUS_BOOT_VERSION

Identdaten KWP2000: $1A ReadBootVersion Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ID_BOOT | string | Softwarenummer (BOOT version) |
| STAT_BOOT_CONF_WORD | int | Boot Configuration Word |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lieferung-version"></a>
### STATUS_LIEFERUNG_VERSION

Software Delivery Type KWP2000: $22 ReadDataByCommonIdentifier $1020 Read Software Delivery Type Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOFTWARE_EOL | string | Software Delivery Type Value: 0-1 Value "0" --&gt; "Standard delivery software" Value "1" --&gt; "EndOfLine delivery software" |
| JOB_STATUS | string | OKAY, no-error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-sw-calib-version"></a>
### STATUS_SW_CALIB_VERSION

Software Ident KWP2000: $22 ReadDataByCommonIdentifier $2510 Read Software and Calibration Version Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOFTWARE_CALIB_VERSION | string | Software Ident Daten |
| JOB_STATUS | string | OKAY, no-error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-kl15"></a>
### STATUS_DIGITAL_KL15

Status Klemme 15 KWP2000: $22 ReadDataByCommonIdentifier $0031 Status Digital Klemme 15 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_KLEMME15_WERT | unsigned int | Status Klemme 15 Value: 0-1 |
| STAT_STATUS_KLEMME15_EINH | string | Einheit = - |
| STAT_STATUS_KLEMME15_TEXT | string | Value "0" --&gt; "Klemme 15 = AUS" Value "1" --&gt; "Klemme 15 = EIN" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-rohwert-batteriespannung"></a>
### STATUS_ROHWERT_BATTERIESPANNUNG

Bordnetzspannung Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0006 Battery Voltage (raw) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BORDNETZSPANNUNG_ROHWERT_WERT | string | Bordnetzspannung Rohwert Range: 0-25000 |
| STAT_BORDNETZSPANNUNG_ROHWERT_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-batteriespannung"></a>
### STATUS_BATTERIESPANNUNG

Bordnetzspannung KWP2000: $22 ReadDataByCommonIdentifier $0007 Battery Voltage (processed) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BORDNETZSPANNUNG_WERT | string | Bordnetzspannung Range: 0-25,5 |
| STAT_BORDNETZSPANNUNG_EINH | string | Einheit = V |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-rohwert-bremse"></a>
### STATUS_ROHWERT_BREMSE

Spannung Bremsschalter Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0020 Brake Switch input voltage Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_BREMSSCHALTER_ROHWERT_WERT | string | Spannung Bremsschalter Rohwert Range: 0-4995 |
| STAT_SPANNUNG_BREMSSCHALTER_ROHWERT_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-bremse"></a>
### STATUS_DIGITAL_BREMSE

Status Bremsschalter KWP2000: $22 ReadDataByCommonIdentifier $0021 Status Digital Bremse Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_BREMSSCHALTER_WERT | unsigned int | Status Bremsschalter Value: 0-1 |
| STAT_STATUS_BREMSSCHALTER_EINH | string | Einheit = - |
| STAT_STATUS_BREMSSCHALTER_TEXT | string | Value "0" --&gt; "Bremse nicht betaetigt" Value "1" --&gt; "Bremse betaetigt" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-kill-schalter"></a>
### STATUS_DIGITAL_KILL_SCHALTER

Status Kill-Schalter KWP2000: $22 ReadDataByCommonIdentifier $0032 Status Digital Kill-Schalter Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_KILL_SCHALTER_WERT | unsigned int | Status Kill-Schalter Value: 0-1 |
| STAT_STATUS_KILL_SCHALTER_EINH | string | Einheit = - |
| STAT_STATUS_KILL_SCHALTER_TEXT | string | Value "0" --&gt; "Kill-Schalter nicht betaetigt" Value "1" --&gt; "Kill-Schalter betaetigt" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-start-schalter"></a>
### STATUS_DIGITAL_START_SCHALTER

Status Start-Schalter KWP2000: $22 ReadDataByCommonIdentifier $0033 Status Digital Start-Schalter Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_START_SCHALTER_WERT | unsigned int | Status Start-Schalter Value: 0-1 |
| STAT_STATUS_START_SCHALTER_EINH | string | Einheit = - |
| STAT_STATUS_START_SCHALTER_TEXT | string | Value "0" --&gt; "Start-Schalter nicht betaetigt" Value "1" --&gt; "Start-Schalter betaetigt" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-rohwert-drosselklappe"></a>
### STATUS_ROHWERT_DROSSELKLAPPE

Spannung Drosselklappe Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0000 TPS Voltage Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_DROSSELKLAPPE_ROHWERT_WERT | string | Spannung Drosselklappe Rohwert Range: 0-4995 |
| STAT_SPANNUNG_DROSSELKLAPPE_ROHWERT_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-rohwert-drosselklappe-adaptiert"></a>
### STATUS_ROHWERT_DROSSELKLAPPE_ADAPTIERT

Spannung Drosselklappe Rohwert Adaptiert KWP2000: $22 ReadDataByCommonIdentifier $0005 TPS Voltage Adapted Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_DROSSELKLAPPE_ROHWERT_ADAPTIERT_WERT | string | Spannung Drosselklappe Rohwert Adaptiert Range: 0-4995 |
| STAT_SPANNUNG_DROSSELKLAPPE_ROHWERT_ADAPTIERT_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-drosselklappenwinkel"></a>
### STATUS_DROSSELKLAPPENWINKEL

Drosselklappenwinkel KWP2000: $22 ReadDataByCommonIdentifier $0004 TPS Angle Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DROSSELKLAPPENWINKEL_WERT | string | Drosselklappenwinkel Range: 0-95 |
| STAT_DROSSELKLAPPENWINKEL_EINH | string | Einheit = deg |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-drosselklappenposition"></a>
### STATUS_DROSSELKLAPPENPOSITION

Drosselklappenposition KWP2000: $22 ReadDataByCommonIdentifier $0001 TPS percentage Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DROSSELKLAPPENPOSITION_WERT | string | Drosselklappenposition Range: 0-99,9 |
| STAT_DROSSELKLAPPENPOSITION_EINH | string | Einheit = % |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-rohwert-getriebeeingang"></a>
### STATUS_ROHWERT_GETRIEBEEINGANG

Spannung Getriebeeingang Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0014 Gear input Voltage Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_GETRIEBEEINGANG_ROHWERT_WERT | string | Spannung Getriebeeingang Rohwert Range: 0-4995 |
| STAT_SPANNUNG_GETRIEBEEINGANG_ROHWERT_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-neutralschalter"></a>
### STATUS_DIGITAL_NEUTRALSCHALTER

Status Neutralschalter KWP2000: $22 ReadDataByCommonIdentifier $0015 Status Digital Neutralschalter Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_NEUTRALSCHALTER_WERT | unsigned int | Status Neutralschalter Value: 0-1 |
| STAT_STATUS_NEUTRALSCHALTER_EINH | string | Einheit = - |
| STAT_STATUS_NEUTRALSCHALTER_TEXT | string | Value "0" --&gt; "Gang = nicht N" Value "1" --&gt; "Gang = N" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-gang"></a>
### STATUS_DIGITAL_GANG

Status Gang KWP2000: $22 ReadDataByCommonIdentifier $0025 Status Digital Gang Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_GANG_WERT | unsigned int | Status Gang Value: 0-64 |
| STAT_STATUS_GANG_EINH | string | Einheit = - |
| STAT_STATUS_GANG_TEXT | string | Value "0"  --&gt; "Gang = N" Value "1"  --&gt; "Gang = 1" Value "2"  --&gt; "Gang = 2" Value "4"  --&gt; "Gang = 3" Value "8"  --&gt; "Gang = 4" Value "16" --&gt; "Gang = 5" Value "32" --&gt; "Gang = 6" Value "64" --&gt; "Gang = undefined" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-rohwert-ssa"></a>
### STATUS_ROHWERT_SSA

Spannung Seitenstuetze E Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0022 Side-stand Switch 1 Voltage Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_SEITENSTUETZE_E_ROHWERT_WERT | string | Spannung Seitenstuetze E Rohwert Range: 0-4995 |
| STAT_SPANNUNG_SEITENSTUETZE_E_ROHWERT_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-rohwert-ssa2"></a>
### STATUS_ROHWERT_SSA2

Spannung Seitenstuetze A Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0023 Side-stand Switch 2 Voltage Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_SEITENSTUETZE_A_ROHWERT_WERT | string | Spannung Seitenstuetze A Rohwert Range: 0-4995 |
| STAT_SPANNUNG_SEITENSTUETZE_A_ROHWERT_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-rohwert-kupplungsschalter"></a>
### STATUS_ROHWERT_KUPPLUNGSSCHALTER

Spannung Kupplungseingang Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0026 Clutch switch input Voltage Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_KUPPLUNGSEINGANG_ROHWERT_WERT | string | Spannung Kupplungseingang Rohwert Range: 0-4995 |
| STAT_SPANNUNG_KUPPLUNGSEINGANG_ROHWERT_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-kupplungsschalter"></a>
### STATUS_KUPPLUNGSSCHALTER

Status Kupplungsschalter KWP2000: $22 ReadDataByCommonIdentifier $0027 Status Kupplungsschalter Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_KUPPLUNGSSCHALTER_WERT | unsigned int | Status Kupplungsschalter Value: 0-1 |
| STAT_STATUS_KUPPLUNGSSCHALTER_EINH | string | Einheit = - |
| STAT_STATUS_KUPPLUNGSSCHALTER_TEXT | string | Value "0" --&gt; "Kupplung betaetigt" Value "1" --&gt; "Kupplung nicht betaetigt" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-seitenstuetze"></a>
### STATUS_DIGITAL_SEITENSTUETZE

Status Seitenstuetze KWP2000: $22 ReadDataByCommonIdentifier $0024 Status Digital Seitenstuetze Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_SEITENSTUETZE_WERT | unsigned int | Status Seitenstuetze Value: 0-1 |
| STAT_STATUS_SEITENSTUETZE_EINH | string | Einheit = - |
| STAT_STATUS_SEITENSTUETZE_TEXT | string | Value "0" --&gt; "Seitenstuetze eingeklappt" Value "1" --&gt; "Seitenstuetze ausgeklappt" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-oelniveauschalter"></a>
### STATUS_DIGITAL_OELNIVEAUSCHALTER

Status Oelniveauschalter KWP2000: $22 ReadDataByCommonIdentifier $0041 Status Digital Oelniveauschalter Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_OELNIVEAUSCHALTER_WERT | unsigned int | Status Oelniveauschalter Value: 0-1 |
| STAT_STATUS_OELNIVEAUSCHALTER_EINH | string | Einheit = - |
| STAT_STATUS_OELNIVEAUSCHALTER_TEXT | string | Value "0" --&gt; "Oelniveauschalter nicht betaetigt" Value "1" --&gt; "Oelniveauschalter betaetigt" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-oelniveau"></a>
### STATUS_OELNIVEAU

Status Oelniveau KWP2000: $22 ReadDataByCommonIdentifier $0042 Oil Level Status Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_OELNIVEAU_WERT | unsigned int | Status Oelniveau Value: 1-3 |
| STAT_STATUS_OELNIVEAU_EINH | string | Einheit = - |
| STAT_STATUS_OELNIVEAU_TEXT | string | Value "1" --&gt; "Oelniveau = OK" Value "2" --&gt; "Oelniveau = nicht OK" Value "3" --&gt; "Oelniveau = noch kein Messwert vorhanden" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-abs-taster"></a>
### STATUS_DIGITAL_ABS_TASTER

Status ABS Taster KWP2000: $22 ReadDataByCommonIdentifier $0028 Status Digital ABS Taster Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_ABS_TASTER_WERT | unsigned int | Status ABS Taster Value: 0-1 |
| STAT_STATUS_ABS_TASTER_EINH | string | Einheit = - |
| STAT_STATUS_ABS_TASTER_TEXT | string | Value "0" --&gt; "ABS-Taster nicht betaetigt" Value "1" --&gt; "ABS-Taster betaetigt" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-rohwert-oeltemperatur"></a>
### STATUS_ROHWERT_OELTEMPERATUR

Spannung Oeltemperatur Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0016 Oil Temperature Voltage Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_OELTEMPERATUR_ROHWERT_WERT | string | Spannung Oeltemperatur Rohwert Range: 0-4995 |
| STAT_SPANNUNG_OELTEMPERATUR_ROHWERT_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-oeltemperatur"></a>
### STATUS_OELTEMPERATUR

Oeltemperatur KWP2000: $22 ReadDataByCommonIdentifier $0017 Oil Temperature Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OELTEMPERATUR_WERT | string | Oeltemperatur Range: (-40)-160 |
| STAT_OELTEMPERATUR_EINH | string | Einheit = °C |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-rohwert-kuehlwassertemperatur"></a>
### STATUS_ROHWERT_KUEHLWASSERTEMPERATUR

Spannung Kuehlwassertemperatur Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0008 Coolant Temperature Sensor Voltage Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_KUEHLWASSERTEMPERATUR_ROHWERT_WERT | string | Spannung Kuehlwassertemperatur Rohwert Range: 0-4995 |
| STAT_SPANNUNG_KUEHLWASSERTEMPERATUR_ROHWERT_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-kuehlwassertemperatur"></a>
### STATUS_KUEHLWASSERTEMPERATUR

Kuehlwassertemperatur KWP2000: $22 ReadDataByCommonIdentifier $0009 Coolant Temperature Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KUEHLWASSERTEMPERATUR_WERT | string | Kuehlwassertemperatur Range: (-40)-140 |
| STAT_KUEHLWASSERTEMPERATUR_EINH | string | Einheit = °C |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-rohwert-ansauglufttemperatur"></a>
### STATUS_ROHWERT_ANSAUGLUFTTEMPERATUR

Spannung Ansauglufttemperatur Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0010 Air Temperature Sensor Voltage Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_ANSAUGLUFTTEMPERATUR_ROHWERT_WERT | string | Spannung Ansauglufttemperatur Rohwert Range: 0-4995 |
| STAT_SPANNUNG_ANSAUGLUFTTEMPERATUR_ROHWERT_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-ansauglufttemperatur"></a>
### STATUS_ANSAUGLUFTTEMPERATUR

Ansauglufttemperatur KWP2000: $22 ReadDataByCommonIdentifier $0011 Air Temperature Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANSAUGLUFTTEMPERATUR_WERT | string | Ansauglufttemperatur Range: (-40)-140 |
| STAT_ANSAUGLUFTTEMPERATUR_EINH | string | Einheit = °C |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-rohwert-lambda"></a>
### STATUS_ROHWERT_LAMBDA

Spannung Lambda Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0012 Lambda Sensor Voltage Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_LAMBDA_ROHWERT_WERT | string | Spannung Lambda Sonde Rohwert Range: 0-4995 |
| STAT_SPANNUNG_LAMBDA_ROHWERT_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-lambda"></a>
### STATUS_LAMBDA

Status Lambda KWP2000: $22 ReadDataByCommonIdentifier $0013 Status Lambda Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_LAMBDA_WERT | unsigned int | Status Lambda Value: 1-3 |
| STAT_STATUS_LAMBDA_EINH | string | Einheit = - |
| STAT_STATUS_LAMBDA_TEXT | string | Value "1" --&gt; "Status Lambda = Mager" Value "2" --&gt; "Status Lambda = Verboten" Value "3" --&gt; "Status Lambda = Fett" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Motordrehzahl KWP2000: $22 ReadDataByCommonIdentifier $0100 Engine Speed Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTORDREHZAHL_WERT | string | Motordrehzahl Range: 0-20000 |
| STAT_MOTORDREHZAHL_EINH | string | Einheit = rpm |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-fahrzeuggeschwindigkeit"></a>
### STATUS_FAHRZEUGGESCHWINDIGKEIT

Status Fahrzeuggeschwindigkeit KWP2000: $22 ReadDataByCommonIdentifier $0101 Fahrzeuggeschwindigkeit Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_FAHRZEUGGESCHWINDIGKEIT_WERT | string | Status Fahrzeuggeschwindigkeit Range: 0-4095 |
| STAT_STATUS_FAHRZEUGGESCHWINDIGKEIT_EINH | string | Einheit = km/h |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-lastrelais"></a>
### STATUS_DIGITAL_LASTRELAIS

Status Lastrelais KWP2000: $22 ReadDataByCommonIdentifier $0061 Status Digital Lastrelais Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_LASTRELAIS_WERT | unsigned int | Status Lastrelais Value: 0-1 |
| STAT_STATUS_LASTRELAIS_EINH | string | Einheit = - |
| STAT_STATUS_LASTRELAIS_TEXT | string | Value "0" --&gt; "Lastrelais nicht aktiv" Value "1" --&gt; "Lastrelais aktiv" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-start-relais"></a>
### STATUS_DIGITAL_START_RELAIS

Status Start-Relais KWP2000: $22 ReadDataByCommonIdentifier $0062 Status Digital Start-Relais Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_START_RELAIS_WERT | unsigned int | Status Start-Relais Value: 0-1 |
| STAT_STATUS_START_RELAIS_EINH | string | Einheit = - |
| STAT_STATUS_START_RELAIS_TEXT | string | Value "0" --&gt; "Start-Relais nicht aktiv" Value "1" --&gt; "Start-Relais aktiv" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-ekp-relais"></a>
### STATUS_DIGITAL_EKP_RELAIS

Status EKP-Relais KWP2000: $22 ReadDataByCommonIdentifier $0060 Status Digital EKP-Relais Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_EKP_RELAIS_WERT | unsigned int | Status EKP-Relais Value: 0-1 |
| STAT_STATUS_EKP_RELAIS_EINH | string | Einheit = - |
| STAT_STATUS_EKP_RELAIS_TEXT | string | Value "0" --&gt; "EKP-Relais nicht aktiv" Value "1" --&gt; "EKP-Relais aktiv" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-luefterrelais"></a>
### STATUS_DIGITAL_LUEFTERRELAIS

Status Luefterrelais KWP2000: $22 ReadDataByCommonIdentifier $0063 Status Digital Luefterrelais Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_LUEFTERRELAIS_WERT | unsigned int | Status Luefterrelais Value: 0-1 |
| STAT_STATUS_LUEFTERRELAIS_EINH | string | Einheit = - |
| STAT_STATUS_LUEFTERRELAIS_TEXT | string | Value "0" --&gt; "Luefterrelais nicht aktiv" Value "1" --&gt; "Luefterrelais aktiv" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-tev"></a>
### STATUS_TEV

Status TEV KWP2000: $22 ReadDataByCommonIdentifier $0185 PWM TEV Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_TEV_WERT | string | Status TEV Range: 0-100 |
| STAT_STATUS_TEV_EINH | string | Einheit = % |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-einspritzdauer-zyl1"></a>
### STATUS_EINSPRITZDAUER_ZYL1

Status Einspritzventil 1 KWP2000: $22 ReadDataByCommonIdentifier $0110 Einspritzdauer Zylinder 1 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_EINSPRITZVENTIL1_WERT | string | Status Einspritzventil 1 Range: 0-655,35 |
| STAT_STATUS_EINSPRITZVENTIL1_EINH | string | Einheit = ms |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-einspritzdauer-zyl2"></a>
### STATUS_EINSPRITZDAUER_ZYL2

Status Einspritzventil 2 KWP2000: $22 ReadDataByCommonIdentifier $0111 Einspritzdauer Zylinder 2 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_EINSPRITZVENTIL2_WERT | string | Status Einspritzventil 2 Range: 0-655,35 |
| STAT_STATUS_EINSPRITZVENTIL2_EINH | string | Einheit = ms |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-uebertemperaturwarnleuchte"></a>
### STATUS_DIGITAL_UEBERTEMPERATURWARNLEUCHTE

Status Uebertemperaturwarnleuchte KWP2000: $22 ReadDataByCommonIdentifier $0108 Status Digital Uebertemperaturwarnleuchte Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_UEBERTEMPERATURWARNLEUCHTE_WERT | unsigned int | Status Uebertemperaturwarnleuchte Value: 0-1 |
| STAT_STATUS_UEBERTEMPERATURWARNLEUCHTE_EINH | string | Einheit = - |
| STAT_STATUS_UEBERTEMPERATURWARNLEUCHTE_TEXT | string | Value "0" --&gt; "Uebertemperaturwarnleuchte nicht angesteuert" Value "1" --&gt; "Uebertemperaturwarnleuchte angesteuert" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-zuendzeitpunkt-zyl1"></a>
### STATUS_ZUENDZEITPUNKT_ZYL1

Status Zuendzeitpunkt Zyl. 1 KWP2000: $22 ReadDataByCommonIdentifier $0120 Zuendzeitpunkt Zylinder 1 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_ZUENDZEITPUNKT_ZYL1_WERT | string | Status Zuendzeitpunkt Zyl. 1 Range: (-30)-(+75) |
| STAT_STATUS_ZUENDZEITPUNKT_ZYL1_EINH | string | Einheit = deg |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-schliesszeit-zyl1"></a>
### STATUS_SCHLIESSZEIT_ZYL1

Status Schliesszeit Zyl. 1 KWP2000: $22 ReadDataByCommonIdentifier $0130 Schliesszeit Zylinder 1 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_SCHLIESSZEIT_ZYL1_WERT | string | Status Schliesszeit Zyl. 1 Range: 0-25,5 |
| STAT_STATUS_SCHLIESSZEIT_ZYL1_EINH | string | Einheit = ms |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-zuendzeitpunkt-zyl2"></a>
### STATUS_ZUENDZEITPUNKT_ZYL2

Status Zuendzeitpunkt Zyl. 2 KWP2000: $22 ReadDataByCommonIdentifier $0121 Zuendzeitpunkt Zylinder 2 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_ZUENDZEITPUNKT_ZYL2_WERT | string | Status Zuendzeitpunkt Zyl. 2 Range: (-30)-(+75) |
| STAT_STATUS_ZUENDZEITPUNKT_ZYL2_EINH | string | Einheit = deg |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-schliesszeit-zyl2"></a>
### STATUS_SCHLIESSZEIT_ZYL2

Status Schliesszeit Zyl. 2 KWP2000: $22 ReadDataByCommonIdentifier $0131 Schliesszeit Zylinder 2 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_SCHLIESSZEIT_ZYL2_WERT | string | Status Schliesszeit Zyl. 2 Range: 0-25,5 |
| STAT_STATUS_SCHLIESSZEIT_ZYL2_EINH | string | Einheit = ms |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-abgasklappe"></a>
### STATUS_ABGASKLAPPE

Status Abgasklappenposition KWP2000: $22 ReadDataByCommonIdentifier $0186 Abgasklappenposition Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_ABGASKLAPPE_WERT | string | Status Abgasklappenposition Range: 0-100 |
| STAT_STATUS_ABGASKLAPPE_EINH | string | Einheit = % |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-lam1-hz"></a>
### STATUS_LAM1_HZ

Status Lambdasondenheizung KWP2000: $22 ReadDataByCommonIdentifier $0190 PWM Lambdasondenheizung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_LAMBDASONDENHEIZUNG_WERT | string | Status Lambdasondenheizung Range: 0-100 |
| STAT_STATUS_LAMBDASONDENHEIZUNG_EINH | string | Einheit = % |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-steppermotor"></a>
### STATUS_STEPPERMOTOR

Status Steppermotorposition KWP2000: $22 ReadDataByCommonIdentifier $0090 Stepper Motor Position Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_STEPPERMOTORPOSITION_WERT | string | Status Steppermotorposition Range: 0-255 |
| STAT_STATUS_STEPPERMOTORPOSITION_EINH | string | Einheit = step |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-rohwert-umgebungsdruck"></a>
### STATUS_ROHWERT_UMGEBUNGSDRUCK

Spannung Umgebungsdruck Rohwert KWP2000: $22 ReadDataByCommonIdentifier $0002 Atmospheric Pressure Sensor Voltage Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_UMGEBUNGSDRUCK_ROHWERT_WERT | string | Spannung Umgebungsdruck Rohwert Range: 0-4995 |
| STAT_SPANNUNG_UMGEBUNGSDRUCK_ROHWERT_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-umgebungsdruck"></a>
### STATUS_UMGEBUNGSDRUCK

Status Umgebungsdruck KWP2000: $22 ReadDataByCommonIdentifier $0003 Umgebungsdruck Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_UMGEBUNGSDRUCK_WERT | string | Status Umgebungsdruck Range: 0-1200 |
| STAT_STATUS_UMGEBUNGSDRUCK_EINH | string | Einheit = mbar |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-vorderradgeschwindigkeit"></a>
### STATUS_VORDERRADGESCHWINDIGKEIT

Status Vorderradgeschwindigkeit KWP2000: $22 ReadDataByCommonIdentifier $0103 Geschwindigkeit Vorderrad Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_VORDERRADGESCHWINDIGKEIT_WERT | string | Status Vorderradgeschwindigkeit Range: 0-4095 |
| STAT_STATUS_VORDERRADGESCHWINDIGKEIT_EINH | string | Einheit = km/h |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-hinterradgeschwindigkeit"></a>
### STATUS_HINTERRADGESCHWINDIGKEIT

Status Hinterradgeschwindigkeit KWP2000: $22 ReadDataByCommonIdentifier $0104 Geschwindigkeit Hinterrad Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_HINTERRADGESCHWINDIGKEIT_WERT | string | Status Hinterradgeschwindigkeit Range: 0-4095 |
| STAT_STATUS_HINTERRADGESCHWINDIGKEIT_EINH | string | Einheit = km/h |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-leerlaufdrehzahl-soll"></a>
### STATUS_LEERLAUFDREHZAHL_SOLL

Status Sollleerlaufdrehzahl KWP2000: $22 ReadDataByCommonIdentifier $0105 Leerlaufdrehzahl Soll Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_SOLLLEERLAUFDREHZAHL_WERT | string | Status Sollleerlaufdrehzahl Range: 0-20000 |
| STAT_STATUS_SOLLLEERLAUFDREHZAHL_EINH | string | Einheit = rpm |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-leerlaufadaptionswert"></a>
### STATUS_LEERLAUFADAPTIONSWERT

Status Leerlaufadaptionswert KWP2000: $22 ReadDataByCommonIdentifier $0106 Leerlaufadaptionswert (Stepper) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_LEERLAUFADAPTIONSWERT_WERT | string | Status Leerlaufadaptionswert Range: (-300)-(+700) |
| STAT_STATUS_LEERLAUFADAPTIONSWERT_EINH | string | Einheit = Nm |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-lambdasondenheizung"></a>
### STATUS_DIGITAL_LAMBDASONDENHEIZUNG

Status Lambdasondenheizung KWP2000: $22 ReadDataByCommonIdentifier $0064 Status Digital Lambdasondenheizung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_LAMBDASONDENHEIZUNG_WERT | unsigned int | Status Lambdasondenheizung Value: 0-1 |
| STAT_STATUS_LAMBDASONDENHEIZUNG_EINH | string | Einheit = - |
| STAT_STATUS_LAMBDASONDENHEIZUNG_TEXT | string | Value "0" --&gt; "Lambdasondenheizung = AUS" Value "1" --&gt; "Lambdasondenheizung = EIN" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-lambdaregelfaktor"></a>
### STATUS_LAMBDAREGELFAKTOR

Status Lambdaregelfaktor KWP2000: $22 ReadDataByCommonIdentifier $0065 Lambdaregelfaktor Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_LAMBDAREGELFAKTOR_WERT | string | Status Lambdaregelfaktor Range: (-50)-(+50) |
| STAT_STATUS_LAMBDAREGELFAKTOR_EINH | string | Einheit = % |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-lambdaregeladaption"></a>
### STATUS_LAMBDAREGELADAPTION

Status Lambdaregeladaption KWP2000: $22 ReadDataByCommonIdentifier $0066 Lambdaregeladaption Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_LAMBDAREGELADAPTION_WERT | string | Status Lambdaregeladaption Range: 0-2 |
| STAT_STATUS_LAMBDAREGELADAPTION_EINH | string | Einheit = - |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-lambdaregelung"></a>
### STATUS_DIGITAL_LAMBDAREGELUNG

Status Lambdaregelung KWP2000: $22 ReadDataByCommonIdentifier $0067 Status Digital Lambdaregelung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_LAMBDAREGELUNG_WERT | unsigned int | Status Lambdaregelung Value: 0-1 |
| STAT_STATUS_LAMBDAREGELUNG_EINH | string | Einheit = - |
| STAT_STATUS_LAMBDAREGELUNG_TEXT | string | Value "0" --&gt; "Lambdaregelung = nicht Aktiv" Value "1" --&gt; "Lambdaregelung = Aktiv" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-motorlast"></a>
### STATUS_DIGITAL_MOTORLAST

Status Motorlast KWP2000: $22 ReadDataByCommonIdentifier $0068 Status Digital Motorlast Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_MOTORLAST_WERT | unsigned int | Status Motorlast Value: 0-4 |
| STAT_STATUS_MOTORLAST_EINH | string | Einheit = - |
| STAT_STATUS_MOTORLAST_TEXT | string | Value "0" --&gt; "Motorlast = Aus" Value "1" --&gt; "Motorlast = Leerlauf" Value "2" --&gt; "Motorlast = Volllast" Value "4" --&gt; "Motorlast = Teillast" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-drosselklappenadaption-zu"></a>
### STATUS_DROSSELKLAPPENADAPTION_ZU

Status Drosselklappenadaption Zu KWP2000: $22 ReadDataByCommonIdentifier $0018 Drosselklappenadaption Position Zu Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_DROSSELKLAPPENADAPTION_ZU_WERT | string | Status Drosselklappenadaption Zu Range: 0-95 |
| STAT_STATUS_DROSSELKLAPPENADAPTION_ZU_EINH | string | Einheit = deg |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-drosselklappenadaption-auf"></a>
### STATUS_DROSSELKLAPPENADAPTION_AUF

Status Drosselklappenadaption Auf KWP2000: $22 ReadDataByCommonIdentifier $0019 Drosselklappenadaption Position Auf Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_DROSSELKLAPPENADAPTION_AUF_WERT | string | Status Drosselklappenadaption Auf Range: 0-95 |
| STAT_STATUS_DROSSELKLAPPENADAPTION_AUF_EINH | string | Einheit = deg |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-gangadaption-gang-1"></a>
### STATUS_GANGADAPTION_GANG_1

Status Gangadaption 1 KWP2000: $22 ReadDataByCommonIdentifier $0141 Adaptionswert Gang 1 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_GANGADAPTION_1_WERT | string | Status Gangadaption 1 Range: 0-4995 |
| STAT_STATUS_GANGADAPTION_1_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-gangadaption-gang-2"></a>
### STATUS_GANGADAPTION_GANG_2

Status Gangadaption 2 KWP2000: $22 ReadDataByCommonIdentifier $0142 Adaptionswert Gang 2 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_GANGADAPTION_2_WERT | string | Status Gangadaption 2 Range: 0-4995 |
| STAT_STATUS_GANGADAPTION_2_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-gangadaption-gang-3"></a>
### STATUS_GANGADAPTION_GANG_3

Status Gangadaption 3 KWP2000: $22 ReadDataByCommonIdentifier $0143 Adaptionswert Gang 3 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_GANGADAPTION_3_WERT | string | Status Gangadaption 3 Range: 0-4995 |
| STAT_STATUS_GANGADAPTION_3_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-gangadaption-gang-4"></a>
### STATUS_GANGADAPTION_GANG_4

Status Gangadaption 4 KWP2000: $22 ReadDataByCommonIdentifier $0144 Adaptionswert Gang 4 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_GANGADAPTION_4_WERT | string | Status Gangadaption 4 Range: 0-4995 |
| STAT_STATUS_GANGADAPTION_4_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-gangadaption-gang-5"></a>
### STATUS_GANGADAPTION_GANG_5

Status Gangadaption 5 KWP2000: $22 ReadDataByCommonIdentifier $0145 Adaptionswert Gang 5 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_GANGADAPTION_5_WERT | string | Status Gangadaption 5 Range: 0-4995 |
| STAT_STATUS_GANGADAPTION_5_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-gangadaption-gang-6"></a>
### STATUS_GANGADAPTION_GANG_6

Status Gangadaption 6 KWP2000: $22 ReadDataByCommonIdentifier $0146 Adaptionswert Gang 6 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_GANGADAPTION_6_WERT | string | Status Gangadaption 6 Range: 0-4995 |
| STAT_STATUS_GANGADAPTION_6_EINH | string | Einheit = mV |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-fahrzeugmodus-soll"></a>
### STATUS_FAHRZEUGMODUS_SOLL

Status Fahrzeugmodus Soll KWP2000: $22 ReadDataByCommonIdentifier $0151 Status Fahrzeugmodus Soll Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_FAHRZEUGMODUS_SOLL_WERT | unsigned int | Status Fahrzeugmodus Soll Value: 1-2 |
| STAT_STATUS_FAHRZEUGMODUS_SOLL_EINH | string | Einheit = - |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-fahrzeugmodus-ist"></a>
### STATUS_FAHRZEUGMODUS_IST

Status Fahrzeugmodus IST KWP2000: $22 ReadDataByCommonIdentifier $0152 Status Fahrzeugmodus IST Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_FAHRZEUGMODUS_IST_WERT | unsigned int | Status Fahrzeugmodus IST Value: 1-2 |
| STAT_STATUS_FAHRZEUGMODUS_IST_EINH | string | Einheit = - |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-startfreigabe"></a>
### STATUS_DIGITAL_STARTFREIGABE

Status Startfreigabe KWP2000: $22 ReadDataByCommonIdentifier $0070 Status Digital Startfreigabe Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_STARTFREIGABE_WERT | unsigned int | Status Startfreigabe Value: 0-1 |
| STAT_STATUS_STARTFREIGABE_EINH | string | Einheit = - |
| STAT_STATUS_STARTFREIGABE_TEXT | string | Value "0" --&gt; "Start nicht moeglich" Value "1" --&gt; "Start moeglich" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-ews-freigabe"></a>
### STATUS_DIGITAL_EWS_FREIGABE

Status EWS-Freigabe KWP2000: $22 ReadDataByCommonIdentifier $0071 Status Digital EWS-Freigabe Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_EWS_FREIGABE_WERT | unsigned int | Status EWS-Freigabe Value: 0-1 |
| STAT_STATUS_EWS_FREIGABE_EINH | string | Einheit = - |
| STAT_STATUS_EWS_FREIGABE_TEXT | string | Value "0" --&gt; "EWS-Freigabe nicht erteilt" Value "1" --&gt; "EWS-Freigabe erteilt" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-motorwarnleuchte"></a>
### STATUS_DIGITAL_MOTORWARNLEUCHTE

Status Motorwarnleuchte KWP2000: $22 ReadDataByCommonIdentifier $0072 Status Digital Motorwarnleuchte Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_MOTORWARNLEUCHTE_WERT | unsigned int | Status Motorwarnleuchte Value: 1-5 |
| STAT_STATUS_MOTORWARNLEUCHTE_EINH | string | Einheit = - |
| STAT_STATUS_MOTORWARNLEUCHTE_TEXT | string | Value "1" --&gt; "Motorwarnleuchte = Aus" Value "2" --&gt; "Motorwarnleuchte = Blinken 1Hz" Value "4" --&gt; "Motorwarnleuchte = Blinken 4Hz" Value "5" --&gt; "Motorwarnleuchte = An" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-showroommodus"></a>
### STATUS_DIGITAL_SHOWROOMMODUS

Status Showroommodus KWP2000: $22 ReadDataByCommonIdentifier $1021 Status Digital Showroommodus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_SHOWROOMMODUS_WERT | unsigned int | Status Showroommodus Value: 0-1 |
| STAT_STATUS_SHOWROOMMODUS_EINH | string | Einheit = - |
| STAT_STATUS_SHOWROOMMODUS_TEXT | string | Value "0" --&gt; "Showroommodus = nicht aktiv" Value "1" --&gt; "Showroommodus = aktiv" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-gemischadaption"></a>
### STATUS_GEMISCHADAPTION

Fuel Adaption Table Reading KWP2000: $22 ReadDataByCommonIdentifier $0300 ReadWarmAdaptionTable $0301 ReadColdAdaptionTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _ROWS_BREAK | string | Row breakpoint vector |
| _COLS_BREAK | string | Column breakpoint vector |
| _ADAT_TAB_HEAD | string | Adaptive warm table header |
| STAT_ADAT_TAB | string | Adaptive warm table values |
| _ROWS_BREAK2 | string | 2nd Row breakpoint vector |
| _COLS_BREAK2 | string | 2nd Column breakpoint vector |
| _ADAT_COLD_TAB_HEAD | string | Adaptive cold table header |
| STAT_ADAT_COLD_TAB | string | Adaptive cold table values |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |
| _TEL_AUFTRAG2 | binary | Hex-answer an SG |
| _TEL_ANTWORT2 | binary | Hex-answer von SG |

<a id="job-status-digital-gepaeckfach"></a>
### STATUS_DIGITAL_GEPAECKFACH

Status Gepaeckfach KWP2000: $22 ReadDataByCommonIdentifier $0073 Status Digital Gepaeckfach Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_GEPAECKFACH_WERT | unsigned int | Status Gepaeckfach Value: 1-3 |
| STAT_STATUS_GEPAECKFACH_EINH | string | Einheit = - |
| STAT_STATUS_GEPAECKFACH_TEXT | string | Value "1" --&gt; "Gepaeckfach = geschlossen" Value "2" --&gt; "Gepaeckfach = offen" Value "3" --&gt; "Signal vom Kombi fehlerhaft" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-digital-syncro"></a>
### STATUS_DIGITAL_SYNCRO

Status Motorsyncronization KWP2000: $22 ReadDataByCommonIdentifier $0076 Status Digital Syncro Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_MOTORSYNCRONIZATION_WERT | string | Status Motorsyncronization Value: 0-255 |
| STAT_STATUS_MOTORSYNCRONIZATION_EINH | string | Einheit = - |
| STAT_STATUS_MOTORSYNCRONIZATION_BIT0_TEXT | string | Value "0" --&gt; "Keine Syncronisation erforderlich" Value "1" --&gt; "Warten auf Syncronisation" |
| STAT_STATUS_MOTORSYNCRONIZATION_BIT1_TEXT | string | Value "0" --&gt; "Kurbelwellengeber vorhanden" Value "1" --&gt; "Kurbelwellengeber nicht vorhanden" |
| STAT_STATUS_MOTORSYNCRONIZATION_BIT2_TEXT | string | Value "0" --&gt; "Kurbelwellensignal nicht erkannt" Value "1" --&gt; "Kurbelwellensignal erkannt" |
| STAT_STATUS_MOTORSYNCRONIZATION_BIT3_TEXT | string | Value "0" --&gt; "System nicht synchronisiert auf Kurbelwelle" Value "1" --&gt; "System synchronisiert auf Kurbelwelle" |
| STAT_STATUS_MOTORSYNCRONIZATION_BIT4_TEXT | string | Value "0" --&gt; "Nockenwellengeber nicht vorhanden" Value "1" --&gt; "Nockenwellengeber vorhanden" |
| STAT_STATUS_MOTORSYNCRONIZATION_BIT5_TEXT | string | Value "0" --&gt; "Nockenwellensignal, OK" Value "1" --&gt; "Nockenwellensignal, Fehler" |
| STAT_STATUS_MOTORSYNCRONIZATION_BIT6_TEXT | string | Value "0" --&gt; "System nicht synchronisiert auf Nockenwellensensor" Value "1" --&gt; "System synchronisiert auf Nockenwellensensor" |
| STAT_STATUS_MOTORSYNCRONIZATION_BIT7_TEXT | string | Value "0" --&gt; "System nicht synchronisiert auf Drehungleichfoermigkeit" Value "1" --&gt; "System synchronisiert auf Drehungleichfoermigkeit" |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-ews"></a>
### STATUS_EWS

KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC000 Zurücklesen verschiedener interner Stati für EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS3_CAPABLE | int | 0 Das SG beherrscht kein EWS3 1 Das SG beherrscht EWS3 |
| STAT_EWS4_CAPABLE | int | 0 Das SG beherrscht kein EWS4 1 Das SG beherrscht EWS4 |
| STAT_EWS3_ACTIVE | int | 0 EWS3 ist nicht (mehr) aktiv 1 EWS3 ist aktiv (oder lässt sich aktivieren) |
| STAT_EWS4_ACTIVE | int | 0 EWS4 ist nicht aktiv 1 EWS4 ist aktiv |
| STAT_EWS4_SERVER_SK_LOCKED | int | 0 SecretKey server lässt sich noch schreiben 1 SecretKey server lässt sich nicht mehr schreiben/lesen |
| STAT_EWS4_CLIENT_SK_LOCKED | int | 0 SecretKey client lässt sich noch schreiben 1 SecretKey client lässt sich nicht mehr schreiben/lesen |
| STAT_CLIENT_AUTHENTICATED | int | 0 Freigabe (noch) nicht erteilt (noch nicht versucht oder Kommunikation gestört) 1 Freigabe erteilt (Challenge-Response erfolgreich) 2 Freigabe abgelehnt (Challenge-Response fehlgeschlagen, falsche Response, Kommunikation i.O.) 3 nicht definiert |
| STAT_CLIENT_AUTHENTICATED_TXT | string | Text zu Status Wert |
| STAT_DH_ACTIVE | int | 0 Diffie-Hellman-Abgleich nicht aktiv 1 Diffie-Hellman-Abgleich aktiv |
| STAT_E_LABEL_ACTIVE | int | 0 E-Label ist nicht aktiv 1 E-Label ist aktiv |
| STAT_FREE_SK0 | int | 0..0xFD Freie Flashablagen 0xFE    Freie Flashablage nicht begrenzt 0xFF    Fehlerkennzeichnung |
| _STAT_FREE_SK0_TXT | string | Freie Plaetze |
| STAT_FREE_SK1 | int | 0..0xFD Freie Flashablagen 0xFE    Freie Flashablage nicht begrenzt 0xFF    Fehlerkennzeichnung |
| _STAT_FREE_SK1_TXT | string | Freie Plaetze |
| STAT_VERSION | int | 0x01 Direktschreiben des SecretKey 0x02 Direktschreiben des SecretKey und DH-Abgleich |
| _STAT_VERSION_TXT | string | Version |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ews4-sk"></a>
### STATUS_EWS4_SK

KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC002 Lesen des SecretKey des Server sowie Client für EWS4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS4_SERVER_SK | binary | SecretKey Server |
| STAT_EWS4_CLIENT_SK | binary | SecretKey Client |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ews4-sk"></a>
### STEUERN_EWS4_SK

17 "EWS4-data" schreiben KWP 2000: $2E WriteDataByCommonIdentifier CommonIdentifier=0xC001

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | Byte0 LOCK_SERVER_SK LOCK_CLIENT_SK WRITE_SERVER_SK WRITE_CLIENT_SK UNLOCK_CLIENT_SK RESET_CLIENT_SK |
| DATA | string | Byte1...16 16 Byte Daten (SecretKey), falls MODE = WRITE_SERVER_SK/WRITE_CLIENT_SK, "0x01,0x02,.." 16 Byte Daten (Hash code), falls MODE = RESET_CLIENT_SK, "0x01,0x02,.." KEINE Daten nötig, falls MODE = LOCK_SERVER_SK/LOCK_CLIENT_SK |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hirevcnt"></a>
### STATUS_HIREVCNT

KWP2000: $22 ReadDataByCommonIdentifier $0501 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HIREV_COUNT | unsigned int | Range: 0-65535 |
| JOB_STATUS | string | OKAY, no-error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-status-gwsz-anzeige"></a>
### STATUS_GWSZ_ANZEIGE

Lesen des Kilometerstandes KWP2000:    $22   ReadDataByCommonIdentifier $C010 "redundanter Kilometerstand" Modus:      Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GWSZ_ANZEIGE_WERT | string | Kilometerstand gültiger Bereich: 0 bis 16777216 km |
| STAT_GWSZ_ANZEIGE_EINH | string | bei BMSKP immer km |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-gwsz-anzeige-schreiben"></a>
### STEUERN_GWSZ_ANZEIGE_SCHREIBEN

Schreiben des Kilometerstandes KWP2000:    $2E   WriteDataByCommonIdentifier $C011 "redundanter Kilometerstand schreiben" Modus:      Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GWSZ_ANZEIGE_WERT | real | Tachometerstand (KM oder Meilen) gueltiger Bereich: 0 bis 999999 km |
| GWSZ_ANZEIGE_EINH | string | km od. miles |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-service-restweg"></a>
### STATUS_SERVICE_RESTWEG

redundanten BMSKP KM-Zaehlerstand bis zum naechsten Service auslesen KWP2000: $22   ReadDataByCommonIdentifier $C030 Local-ID für Lesen SERVKM zusaetzlich wird noch der BMSKP interne KM-Stand ausgelesen daraus wird die Differenz (Intervall/Zaehlerstand) berechnet  KWP2000: $22   ReadDataByCommonIdentifier KWP2000: $C010 Local-ID für internen KM-Stand lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SERV_WEG_WERT | string | Service Wegstrecken - Zaehlerstand [km] |
| STAT_SERV_WEG_EINH | string | km od. miles Die Einheit wird beim Schreiben des redundaten Service-Zaehlerstandes vom Tester vorbelegt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag1 an SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort1 von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag2 an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort2 von SG |

<a id="job-steuern-service-restweg"></a>
### STEUERN_SERVICE_RESTWEG

redundanten BMSKP KM-Zaehlerstand bis zum naechsten Service setzen KWP2000: $2E   WriteDataByCommonIdentifier $C031 Local-ID für Service Datum (SERVKM) schreiben [km] zusaetzlich wird noch der BMSKP interne KM-Stand ausgelesen dazu wird das Intervall/Zaehlerstand addiert  KWP2000: $22   ReadDataByCommonIdentifier KWP2000: $C010 Local-ID für internen KM-Stand lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERV_WEG_WERT | real | Neuer Startwert fuer Serviceintervallzaehler in km oder meilen (nur ganze Werte &lt;= 65535 eingeben) |
| SERV_WEG_EINH | string | km od. miles |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag1 an SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort1 von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag2 an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort2 von SG |

<a id="job-status-service-date"></a>
### STATUS_SERVICE_DATE

redundantes Service-Datum aus BMSKP auslesen KWP2000: $22   ReadDataByCommonIdentifier $C032 Local-ID für Lesen SERVDAT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SERV_DATE_DD | string | Service-Datum: Tag |
| STAT_SERV_DATE_MM | string | Service-Datum: Monat |
| STAT_SERV_DATE_YYYY | string | Service-Datum: Jahr |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-service-date"></a>
### STEUERN_SERVICE_DATE

redundantes Service-Datum in BMSKP Setzen KWP2000: $2E   WriteDataByCommonIdentifier $C033 Local-ID für Service Datum (SERVDAT) schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERV_DATE_DD | int | Service-Datum: Tag  TT = 1..28,29,30,31 |
| SERV_DATE_MM | int | Service-Datum: Monat  MM = 1..12 |
| SERV_DATE_YYYY | int | Service-Datum: Jahr  YYYY = 2006..2099 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrgestellnummer"></a>
### STATUS_FAHRGESTELLNUMMER

17 ASCII Byte Fahrgestell-Nummer KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0x1010 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FGNUMMER | string | ausgelesene Fahrgestellnummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fahrgestellnummer"></a>
### STEUERN_FAHRGESTELLNUMMER

17 ASCII "Fahrgestellnummer" schreiben KWP2000: $2E WriteDataByCommonIdentifier CommonIdentifier=$1010 Full Vehicle Identification Number Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NUMMER | string | "Fahrgestellnummer" 17 x {1...0A...Z} ======&gt; Byte0-16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lastrelais"></a>
### STEUERN_LASTRELAIS

Steuern Lastrelais KWP2000: $31 StartRoutineByLocalIdentifier $A1 Start Routine Activation Load Relay Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ENTRY_OPTION | unsigned char | 0x00: TEST with a Timeout of 10s 0x01: Relay ON TEST Default: 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ende-lastrelais"></a>
### STEUERN_ENDE_LASTRELAIS

Steuern Ende Lastrelais KWP2000: $32 StopRoutineByLocalIdentifier $A1 Stop Routine Activation Load Relay Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ekp-relais"></a>
### STEUERN_EKP_RELAIS

Steuern EKP-Relais KWP2000: $31 StartRoutineByLocalIdentifier $A7 Start Routine Activation Fuel Pump Relay Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ENTRY_OPTION | unsigned char | 0x00: TEST with a Timeout of 10s 0x01: Relay ON TEST Default: 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ende-ekp-relais"></a>
### STEUERN_ENDE_EKP_RELAIS

Steuern Ende EKP-Relais KWP2000: $32 StopRoutineByLocalIdentifier $A7 Stop Routine Activation Fuel Pump Relay Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-luefterrelais"></a>
### STEUERN_LUEFTERRELAIS

Steuern Luefterrelais KWP2000: $31 StartRoutineByLocalIdentifier $A8 Start Routine Activation Fan Relay Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ENTRY_OPTION | unsigned char | 0x00: TEST with Relay OFF for the first 3s and ON for the next 7s, the Timeout is 10s 0x01: TEST with Relay OFF for the first 3s, then Relay ON without Timeout Default: 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ende-luefterrelais"></a>
### STEUERN_ENDE_LUEFTERRELAIS

Steuern Ende Luefterrelais KWP2000: $32 StopRoutineByLocalIdentifier $A8 Stop Routine Activation Fan Relay Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-tev"></a>
### STEUERN_TEV

Steuern TEV KWP2000: $31 StartRoutineByLocalIdentifier $A6 Start Routine Activation Canister Valve Modus  : Duty Cycle 15%, frequency 12Hz, up to timeout of 10s

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ende-tev"></a>
### STEUERN_ENDE_TEV

Steuern Ende TEV KWP2000: $32 StopRoutineByLocalIdentifier $A6 Stop Routine Activation Canister Valve Modus  : Stop immediately the active diagnosis test of the Canister Valve

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ev1"></a>
### STEUERN_EV1

Steuern EV1 KWP2000: $31 StartRoutineByLocalIdentifier $A5 Start Routine Activation Injection cyl 1 Modus  : ton = 1.2 ms, toff = 98.8 ms, frequency 10Hz, up to timeout of 10s

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ende-ev1"></a>
### STEUERN_ENDE_EV1

Steuern Ende EV1 KWP2000: $32 StopRoutineByLocalIdentifier $A5 Stop Routine Activation Injection cyl 1 Modus  : Stop immediately the activation of the injection cyl 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ev2"></a>
### STEUERN_EV2

Steuern EV2 KWP2000: $31 StartRoutineByLocalIdentifier $AB Start Routine Activation Injection cyl 2 Modus  : ton = 1.2 ms, toff = 98.8 ms, frequency 10Hz, up to timeout of 10s

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ende-ev2"></a>
### STEUERN_ENDE_EV2

Steuern Ende EV2 KWP2000: $32 StopRoutineByLocalIdentifier $AB Stop Routine Activation Injection cyl 2 Modus  : Stop immediately the activation of the injection cyl 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-uebertemperaturleuchte"></a>
### STEUERN_UEBERTEMPERATURLEUCHTE

Steuern Uebertemperaturleuchte KWP2000: $31 StartRoutineByLocalIdentifier $AD Start Routine Activation Temperature Warning Lamp Modus  : The Warning Lamp Flashes with Duty Cycle 50%, frequency 1Hz, up to timeout of 10s

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ende-uebertemperaturleuchte"></a>
### STEUERN_ENDE_UEBERTEMPERATURLEUCHTE

Steuern Ende Uebertemperaturleuchte KWP2000: $32 StopRoutineByLocalIdentifier $AD Stop Routine Activation Temperature Warning Lamp Modus  : Stop immediately the activation of the Temperature Warning Lamp

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-abgasklappe"></a>
### STEUERN_ABGASKLAPPE

Steuern Abgasklappe KWP2000: $31 StartRoutineByLocalIdentifier $AA Start Routine Activation Exhaust Valve Modus  : The target duty cycle is 5% for the first 5s and 95% for the next 5s, the timeout is 10s

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ende-abgasklappe"></a>
### STEUERN_ENDE_ABGASKLAPPE

Steuern Ende Abgasklappe KWP2000: $32 StopRoutineByLocalIdentifier $AA Stop Routine Activation Exhaust Valve Modus  : Stop immediately the active diagnosis test of the Exhaust Valve

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-lambdasondenheizung"></a>
### STEUERN_LAMBDASONDENHEIZUNG

Steuern Lambdasondenheizung KWP2000: $31 StartRoutineByLocalIdentifier $AF Start Routine Activation O2 Heater Modus  : Duty Cycle 50%, frequency 12Hz, up to timeout of 10s

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ende-lambdasondenheizung"></a>
### STEUERN_ENDE_LAMBDASONDENHEIZUNG

Steuern Ende Lambdasondenheizung KWP2000: $32 StopRoutineByLocalIdentifier $AF Stop Routine Activation O2 Heater Modus  : Stop immediately the active diagnosis test of the O2 Heater

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-steppermotor"></a>
### STEUERN_STEPPERMOTOR

Steuern Steppermotor KWP2000: $31 StartRoutineByLocalIdentifier $A9 Start Routine Activation of the Stepper Motor Modus  : The target position is 87.5% for the first 4s and 4% for the next 6s, the timeout is 10s

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ende-steppermotor"></a>
### STEUERN_ENDE_STEPPERMOTOR

Steuern Ende Steppermotor KWP2000: $32 StopRoutineByLocalIdentifier $A9 Stop Routine Activation of the Stepper Motor Modus  : Stop immediately the active diagnosis test of the Stepper Motor

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-motorwarnleuchte"></a>
### STEUERN_MOTORWARNLEUCHTE

Steuern Motorwarnleuchte KWP2000: $31 StartRoutineByLocalIdentifier $AC Start Routine Activation Engine Warning Lamp Modus  : The Warning Lamp Flashes with Duty Cycle 50%, frequency 1Hz, up to timeout of 10s

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ende-motorwarnleuchte"></a>
### STEUERN_ENDE_MOTORWARNLEUCHTE

Steuern Ende Motorwarnleuchte KWP2000: $32 StopRoutineByLocalIdentifier $AC Stop Routine Activation Engine Warning Lamp Modus  : Stop immediately the activation of the Engine Warning Lamp

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-showroommodus"></a>
### STEUERN_SHOWROOMMODUS

Steuern Showroom Modus KWP2000: $31 StartRoutineByLocalIdentifier $29 Start Routine Activation of the Showroom Modus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-ende-showroommodus"></a>
### STEUERN_ENDE_SHOWROOMMODUS

Steuern Ende Showroom Modus KWP2000: $32 StopRoutineByLocalIdentifier $29 Stop Routine Activation of the Showroom Modus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, no error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-answer an SG |
| _TEL_ANTWORT | binary | Hex-answer von SG |

<a id="job-steuern-adaptionswerte-loeschen"></a>
### STEUERN_ADAPTIONSWERTE_LOESCHEN

Steuern Adaptionswerte Loeschen KWP2000: $31 StartRoutineByLocalIdentifier $A0 Delete All Adaption Values Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUIREMENTS | string | This field highlights particular requirements when needed |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zero-tps"></a>
### STEUERN_ZERO_TPS

Steuern Zero TPS KWP2000: $31 StartRoutineByLocalIdentifier $21 Learning of the Idle TPS position KWP2000: $33 ReadRoutineResultByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,       when the Zero TPS procedure succeded ERROR_MODE, when the Zero TPS procedure failed table JobResult STATUS_TEXT |
| _REQUIREMENTS | string | This field highlights particular requirements when needed |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-answer von SG |

<a id="job-steuern-reset-stepper"></a>
### STEUERN_RESET_STEPPER

Steuern Reset Stepper KWP2000: $31 StartRoutineByLocalIdentifier $22 Reset Stepper KWP2000: $33 ReadRoutineResultByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-answer von SG |

<a id="job-steuern-neutralgang-adaption"></a>
### STEUERN_NEUTRALGANG_ADAPTION

Steuern Neutralgang Adaption KWP2000: $31 StartRoutineByLocalIdentifier $23 Gear Self-learning procedure KWP2000: $33 ReadRoutineResultByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,       when the Gear Self-learning procedure succeded ERROR_MODE, when the Gear Self-learning procedure failed table JobResult STATUS_TEXT |
| _REQUIREMENTS | string | This field highlights particular requirements when needed |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-answer von SG |

## Tables

### Index

- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (62 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (61 × 5)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (4 × 9)
- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [LIEFERANTEN](#table-lieferanten) (126 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [JOBRESULT](#table-jobresult) (100 × 2)
- [STATCLIENTAUTHTXT](#table-statclientauthtxt) (4 × 2)
- [STATFREESKTXT](#table-statfreesktxt) (3 × 2)
- [STATEWSVERTXT](#table-statewsvertxt) (3 × 2)
- [SWTFEHLER_TAB](#table-swtfehler-tab) (51 × 2)

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
| 0xXY | -- | Unknown diagnostic mode |

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
| 0xXY | -- | Unknown Baudrate |

<a id="table-programmierstatus"></a>
### PROGRAMMIERSTATUS

Dimensions: 19 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | Delivery status |
| 0x01 | Normal operation |
| 0x02 | unused |
| 0x03 | Memory erased |
| 0x04 | unused |
| 0x05 | Signature check PAF not done |
| 0x06 | Signature check DAF not done |
| 0x07 | Program-programming session active |
| 0x08 | Data-programming session active |
| 0x09 | Hardware reference faulty |
| 0x0A | Program reference faulty |
| 0x0B | Referencing error Hardware -&gt; Program |
| 0x0C | Program not available or not complete |
| 0x0D | Data reference faulty |
| 0x0E | Referencing error Program -&gt; Data |
| 0x0F | Data not available or not complete |
| 0x10 | reserved for BMW |
| 0x80 | reserved for Manufacturer |
| 0xXY | Unknown programming status |

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
| 0xFF | ??? | Unknown memory segment |

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
| - | BMW-FAST |
| - | KWP2000* |
| 1 | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 62 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x2710 | EWS4: unauthenticated response received |
| 0x2720 | EWS4: CAN bus timeout error |
| 0x2730 | EWS4: no secret key programmed |
| 0x2740 | EWS4: data storage write error |
| 0x2741 | EWS4: data storage plausibility error |
| 0x2760 | Injector 1 circuit malfunction |
| 0x2761 | Injector 2 circuit malfunction |
| 0x2762 | Ignition coil 1 circuit malfunction |
| 0x2763 | Ignition coil 2 circuit malfunction |
| 0x2764 | Crankshaft sensor circuit malfunction |
| 0x2765 | HEGO1 sensor heater - circuit short to Vbatt |
| 0x2766 | HEGO1 sensor heater - circuit short to GND or open circuit |
| 0x2767 | HEGO1 sensor circuit malfunction |
| 0x2768 | Throttle position sensor - circuit low voltage |
| 0x2769 | Throttle position sensor - circuit high voltage |
| 0x2770 | Atmospheric pressure 1 sensor - circuit low voltage |
| 0x2771 | Atmospheric pressure 1 sensor - circuit high voltage |
| 0x2772 | Intake air temperature sensor - circuit low voltage |
| 0x2773 | Intake air temperature sensor - circuit high voltage |
| 0x2774 | Engine coolant temperature sensor - circuit low voltage |
| 0x2775 | Engine coolant temperature sensor - circuit high voltage |
| 0x2776 | Fuel pump relay - circuit short to Vbatt |
| 0x2777 | Fuel pump relay - circuit short to GND or open circuit |
| 0x2778 | Load relay - circuit short to Vbatt or open circuit |
| 0x2779 | Load relay - circuit short to GND |
| 0x2780 | Starter relay - circuit short to Vbatt |
| 0x2781 | Starter relay - circuit short to GND or open circuit |
| 0x2782 | Fan coil relay - circuit short to Vbatt |
| 0x2783 | Fan coil relay - circuit short to GND |
| 0x2784 | Fan coil relay - open circuit |
| 0x2785 | Malfunction of the STH motor |
| 0x2786 | System voltage circuit malfunction |
| 0x2787 | EEPROM error |
| 0x2788 | Purge canister valve solenoid - circuit short to Vbatt |
| 0x2789 | Purge canister valve solenoid - circuit short to GND or open circuit |
| 0x2790 | Oil temperature sensor - circuit low voltage |
| 0x2791 | Oil temperature sensor - circuit high voltage |
| 0x2792 | Side Stand switch - circuit high voltage |
| 0x2793 | Camshaft sensor - signal not plausible |
| 0x2794 | Idle control - signal not plausible |
| 0x2795 | RAM test - signal not plausible |
| 0x2796 | ROM test - signal not plausible |
| 0x2797 | Lambda self adaption - signal not plausible |
| 0x2798 | HEGO2 sensor circuit malfunction |
| 0x2799 | Warning lamp circuit malfunction |
| 0x2800 | HEGO2 sensor heater - circuit short to Vbatt |
| 0x2801 | HEGO2 sensor heater - circuit short to GND or open circuit |
| 0x2802 | ECU system malfunction |
| 0x2803 | Vehicle speed too high |
| 0x2804 | Vehicle speed not plausible |
| 0x2805 | Tachometer circuit malfunction |
| 0x2806 | Gear sensor - circuit high voltage |
| 0x2807 | Gear sensor - circuit low voltage |
| 0x2808 | Gear sensor - signal not plausible |
| 0x2809 | Showroommode active |
| 0xCD84 | EWS4: CAN frame error |
| 0xCD85 | Bus-Off or BMS mute node |
| 0xCD86 | No Rx ABS frame |
| 0xCD87 | No Rx KOMBI 0x3FF frame |
| 0xCD88 | No Rx KOMBI 0x2B4 frame |
| 0xCD89 | No Rx SPEED MBK 0x2A8 frame |
| 0xFFFF | Unknown error location |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 61 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x2710 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2720 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2730 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2740 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2741 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2760 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2761 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2762 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2763 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2764 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2765 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2766 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2767 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2768 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2769 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2770 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2771 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2772 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2773 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2774 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2775 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2776 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2777 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2778 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2779 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2780 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2781 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2782 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2783 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2784 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2785 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2786 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2787 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2788 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2789 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2790 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2791 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2792 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2793 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2794 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2795 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2796 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2797 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2798 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2799 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2800 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2801 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2802 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2803 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2804 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2805 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2806 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2807 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2808 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x2809 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCD84 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCD85 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCD86 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCD87 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCD88 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCD89 | 0x01 | 0x02 | 0x03 | 0x04 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | Unknown error location |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | Unknown error location |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Engine speed | rpm | - | unsigned char | - | 50 | 1 | 0 |
| 0x02 | Coolant temperature | °C | - | unsigned char | - | 1 | 1 | -40 |
| 0x03 | Throttle position | % | - | unsigned char | - | 0,5 | 1 | 0 |
| 0x04 | Battery voltage | V | - | unsigned char | - | 0,1 | 1 | 0 |

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

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 126 rows × 2 columns

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
| 0x19 | Electromatic South Africa |
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
| 0x51 | ZF Steering systems |
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
| 0xAF | Alfmeier |
| 0xB0 | ELTEK VALERE DEUTSCHLAND GMBH |
| 0xB1 | Omron Automotive Electronics Europe Group |
| 0xB2 | ASK |
| 0xB3 | CML Innovative Technologies GmbH & Co. KG |
| 0xFF | Unknown manufacturer |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 14 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | No matching error symptom |
| 0x01 | Signal or value above threshold |
| 0x02 | Signal or value below threshold |
| 0x04 | No signal or value |
| 0x08 | Implausible signal or value |
| 0x10 | Test conditions fulfilled |
| 0x11 | Test conditions not yet fulfilled |
| 0x20 | Error not occurred yet |
| 0x21 | Error not present now, but already stored |
| 0x22 | Error present now, but not yet stored (debouncing phase) |
| 0x23 | Error present now and already stored |
| 0x30 | Error would not cause a warning lamp to light up |
| 0x31 | Error would cause a warning lamp to light up |
| 0xFF | Unknown type of error |

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

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 100 rows × 2 columns

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
| 0x35 | ERROR_ECU_INVALID_KEY |
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
| 0x81 | ERROR_ECU_RESERVED_BY_DOCUMENT |
| 0x90 | ERROR_ECU_RESERVED_BY_DOCUMENT |
| 0xFA | ERROR_ECU_SUSTEM_SUPPLIER_SPEZIFIC |
| 0xFF | ERROR_ECU_RESERVED_BY_DOCUMENT |
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

<a id="table-statclientauthtxt"></a>
### STATCLIENTAUTHTXT

Dimensions: 4 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0x00 | clearance from ignition and injection not yet gained (not yet challenged or communication disturbed, engine run locked) |
| 0x01 | clearance from ignition and injection gained (challenge-response successful) |
| 0x02 | clearance from ignition and injection declined (challenge-response failed, wrong response, communication ok) |
| 0x03 | not definded |

<a id="table-statfreesktxt"></a>
### STATFREESKTXT

Dimensions: 3 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0xFE | delivery unlimited |
| 0xFF | invalid |
| 0xXY | free delivery |

<a id="table-statewsvertxt"></a>
### STATEWSVERTXT

Dimensions: 3 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0x01 | direct writing off SecretKey |
| 0x02 | direct writing of SecretKey and DH sync |
| 0xXY | unknown |

<a id="table-swtfehler-tab"></a>
### SWTFEHLER_TAB

Dimensions: 51 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x31 | OUT_OF_RANGE |
| 0xCD | KEYFAKTOR_NICHT_VORHANDEN |
| 0xD0 | EXTENSION_CHECK_FEHLERHAFT |
| 0xD1 | FSC_UNGUELTIG |
| 0xD2 | FGN_ZUGRIFF_FEHLERHAFT |
| 0xD3 | KEIN_SPEICHERPLATZ_MEHR_VORHANDEN |
| 0xD4 | FALSCHER_ZERTIFIKATSINHALT_UNBEKANNTES_CRIT-ELEMENT |
| 0xD5 | FALSCHER_FSC_INHALT |
| 0xD6 | FALSCHE_PARAMETERS |
| 0xD7 | FSCS_ZERTIFIKAT_ABGELEHNT |
| 0xD8 | KEINE_DATEN_ZU_ANGEGEBENEM_SG_VORHANDEN |
| 0xD9 | KEINE_AUTHENTISIERUNG |
| 0xDA | FINGER_PRINT_MECHANISMUS_NOT_OK |
| 0xDB | SIGS_ID_UND_ZERTIFIKAT_PASSEN_NICHT_ZUSAMMEN |
| 0xDC | GUELTIGKEITS_PRUEFUNG_SCHLUG_FEHL |
| 0xDD | FAHRGESTELLNUMMER_FEHLERHAFT |
| 0xDE | FGN_PRUEFUNG_SCHLUG_FEHL |
| 0xDF | FLASH_LESEFEHLER |
| 0xE0 | FLASH_SCHREIBFEHLER |
| 0xE1 | FALSCHER_ZERTIFIKATSINHALT_KEY_USAGE |
| 0xE2 | FALSCHER_ZERTIFIKATSINHALT_ISSUER |
| 0xE3 | FALSCHER_ZERTIFIKATSINHALT_VALIDITY |
| 0xE4 | FSCS_ZERTIFIKAT_PRUEFUNG_SCHLUG_FEHL |
| 0xE5 | FSCS_ZERTIFIKAT_UNGUELTIG |
| 0xE6 | FSCS_ZERTIFIKAT_NOCH_NICHT_GEPRUEFT |
| 0xE7 | FSCS_ZERTIFIKAT_NICHT_VORHANDEN |
| 0xE8 | SIGS_ZERTIFIKAT__PRUEFUNG_SCHLUG_FEHL |
| 0xE9 | SIGS_ZERTIFIKAT_UNGUELTIG |
| 0xEA | SIGS_ZERTIFIKAT_NOCH_NICHT_GEPRUEFT |
| 0xEB | SIGS_ZERTIFIKAT_NICHT_VORHANDEN |
| 0xEC | ROOT_ZERTIFIKAT_UNGUELTIG |
| 0xED | ROOT_ZERTIFIKAT_STATUS_ABGELEHNT |
| 0xEE | ROOT_ZERTIFIKAT_FEHLERHAFT |
| 0xEF | ROOT_ZERTIFIKAT_NICHT_LESBAR |
| 0xF0 | ROOT_ZERTIFIKAT_NICHT_VORHANDEN |
| 0xF1 | ZERTIFIKAT_STATUS_ABGELEHNT |
| 0xF2 | ZERTIFIKAT_NICHT_VORHANDEN |
| 0xF3 | FSC_PRUEFUNG_SCHLUG_FEHL |
| 0xF4 | FSC_STORNIERT |
| 0xF5 | FSC_STATUS_ABGELEHNT |
| 0xF6 | FSC_NICHT_VORHANDEN |
| 0xF7 | FALSCHE_FSCS_ID_IM_FSC |
| 0xF8 | UNGUELTIGES_FSC_ERSTELLUNGSDDATUM |
| 0xF9 | SIGNATUR_PRUEFUNG_SCHLUG_FEHL |
| 0xFA | SW_SIGNATURPRUEFUNG_SCHLUG_FEHL |
| 0xFB | SW_SIG_STATUS_ABGELEHNT |
| 0xFC | SW_ID_PRUEFUNG_SCHLUG_FEHL |
| 0xFD | SW_NICHT_AKTIVIERT |
| 0xFE | SW_NICHT_EINGESPIELT |
| 0xFF | UNBEKANNTER_FEHLER |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |
