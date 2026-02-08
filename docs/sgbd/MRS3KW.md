# MRS3KW.prg

- Jobs: [60](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MRS3KW |
| ORIGIN | Rover EE-R-45 John Longvill |
| REVISION | 1.01 |
| AUTHOR | Rover SSL A.Hoddinott, Crichton TI-435 |
| COMMENT | Comment Information |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information bzgl. SGBD
- [IDENT](#job-ident) - Identification data
- [IDENT_EXTENDED](#job-ident-extended) - Identification data
- [VIN_LESEN](#job-vin-lesen) - Identification data
- [VIN_SCHREIBEN](#job-vin-schreiben) - Write thge VIN to the ECU
- [PROGRAMMING_DATE_SCHREIBEN](#job-programming-date-schreiben) - Write the programming date to the ECU
- [ZCS_LESEN](#job-zcs-lesen) - Auslesen des Zentralen Codierschluessels aus Flash
- [ZCS_SCHREIBEN](#job-zcs-schreiben) - Write the ZCS record
- [START_DIAGNOSTICS](#job-start-diagnostics) - Begins a diagnostic session
- [SG_RESET](#job-sg-reset) - Reset the ECU
- [FS_LESEN](#job-fs-lesen) - Read faults
- [FS_LOESCHEN](#job-fs-loeschen) - Clears All Faults
- [STATUS_IO_DIGITAL_04](#job-status-io-digital-04) - Read digitals for LID 04 - Equipment configuration
- [STATUS_IO_DIGITAL_16](#job-status-io-digital-16) - Read digitals for LID 16 - ODS Status
- [STATUS_ANALOGUE_LOCK_BYTE](#job-status-analogue-lock-byte) - Read lock byte value LID 15
- [LOCK_BYTE_SCHREIBEN](#job-lock-byte-schreiben) - Write lock byte value LID 34
- [AIRBAG_DRV_1_SCHREIBEN](#job-airbag-drv-1-schreiben) - Write Airbag driver 1
- [BELT_PRE_DRV_SCHREIBEN](#job-belt-pre-drv-schreiben) - Write Belt pretensioner driver
- [BELT_PRE_PSNGR_SCHREIBEN](#job-belt-pre-psngr-schreiben) - Write Belt pretensioner passenger
- [AIRBAG_PSNGR_1_SCHREIBEN](#job-airbag-psngr-1-schreiben) - Write Airbag passneger
- [SIDEBAG_FRONT_LEFT_SCHREIBEN](#job-sidebag-front-left-schreiben) - Write Sidebag font left seat
- [SIDEBAG_FRONT_RIGHT_SCHREIBEN](#job-sidebag-front-right-schreiben) - Write Sidebag font right seat
- [BELT_PRE_REAR_LEFT_SCHREIBEN](#job-belt-pre-rear-left-schreiben) - Write Belt pretensioner rear left
- [BELT_PRE_REAR_RIGHT_SCHREIBEN](#job-belt-pre-rear-right-schreiben) - Write Belt pretensioner rear right
- [ITS_FRONT_LEFT_SCHREIBEN](#job-its-front-left-schreiben) - Write ITS front left
- [ITS_FRONT_RIGHT_SCHREIBEN](#job-its-front-right-schreiben) - Write ITS front right
- [AIRBAG_DRV_2_SCHREIBEN](#job-airbag-drv-2-schreiben) - Write Airbag driver 2
- [AIRBAG_PSNGR_2_SCHREIBEN](#job-airbag-psngr-2-schreiben) - Write Airbag passenger 2
- [BELT_BUCKLE_DRIVER_SCHREIBEN](#job-belt-buckle-driver-schreiben) - Write Belt Buckle driver
- [BELT_BUCKLE_PSNGR_SCHREIBEN](#job-belt-buckle-psngr-schreiben) - Write Belt Buckle passenger enabled
- [OC_SENSOR_ACTIVE_SCHREIBEN](#job-oc-sensor-active-schreiben) - Write OC Sensor active
- [RFIS_SCHREIBEN](#job-rfis-schreiben) - Write Rear facing infant sensor active
- [MRSA_FRONT_SCHREIBEN](#job-mrsa-front-schreiben) - Write MRSA front selected
- [MRSA_REAR_SCHREIBEN](#job-mrsa-rear-schreiben) - Write MRSA rear selected
- [RFIS_LAMP_SCHREIBEN](#job-rfis-lamp-schreiben) - Write  Rear facing infant sensor lamp enabled
- [US_VERSION_SCHREIBEN](#job-us-version-schreiben) - Write US version enabled
- [AIRBAG_DRV_1_DUP_SCHREIBEN](#job-airbag-drv-1-dup-schreiben) - Write Airbag driver 1
- [BELT_PRE_DRV_DUP_SCHREIBEN](#job-belt-pre-drv-dup-schreiben) - Write Belt pretensioner driver
- [BELT_PRE_PSNGR_DUP_SCHREIBEN](#job-belt-pre-psngr-dup-schreiben) - Write Belt pretensioner passenger
- [AIRBAG_PSNGR_1_DUP_SCHREIBEN](#job-airbag-psngr-1-dup-schreiben) - Write Airbag passneger
- [SIDEBAG_FRONT_LEFT_DUP_SCHREIBEN](#job-sidebag-front-left-dup-schreiben) - Write Sidebag font left seat
- [SIDEBAG_FRONT_RIGHT_DUP_SCHREIBEN](#job-sidebag-front-right-dup-schreiben) - Write Sidebag font right seat
- [BELT_PRE_REAR_LEFT_DUP_SCHREIBEN](#job-belt-pre-rear-left-dup-schreiben) - Write Belt pretensioner rear left
- [BELT_PRE_REAR_RIGHT_DUP_SCHREIBEN](#job-belt-pre-rear-right-dup-schreiben) - Write Belt pretensioner rear right
- [ITS_FRONT_LEFT_DUP_SCHREIBEN](#job-its-front-left-dup-schreiben) - Write ITS front left
- [ITS_FRONT_RIGHT_DUP_SCHREIBEN](#job-its-front-right-dup-schreiben) - Write ITS front right
- [AIRBAG_DRV_2_DUP_SCHREIBEN](#job-airbag-drv-2-dup-schreiben) - Write Airbag driver 2
- [AIRBAG_PSNGR_2_DUP_SCHREIBEN](#job-airbag-psngr-2-dup-schreiben) - Write Airbag passenger 2
- [BELT_BUCKLE_DRIVER_DUP_SCHREIBEN](#job-belt-buckle-driver-dup-schreiben) - Write Belt Buckle driver
- [BELT_BUCKLE_PSNGR_DUP_SCHREIBEN](#job-belt-buckle-psngr-dup-schreiben) - Write Belt Buckle passenger enabled
- [OC_SENSOR_DUP_SCHREIBEN](#job-oc-sensor-dup-schreiben) - Write OC Sensor active
- [RFIS_DUP_SCHREIBEN](#job-rfis-dup-schreiben) - Write Rear facing infant sensor active
- [MRSA_FRONT_DUP_SCHREIBEN](#job-mrsa-front-dup-schreiben) - Write MRSA front selected
- [MRSA_REAR_DUP_SCHREIBEN](#job-mrsa-rear-dup-schreiben) - Write MRSA rear selected
- [RFIS_LAMP_DUP_SCHREIBEN](#job-rfis-lamp-dup-schreiben) - Write  Rear facing infant sensor lamp enabled
- [US_VERSION_DUP_SCHREIBEN](#job-us-version-dup-schreiben) - Write US version enabled
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Ping message
- [SEED_KEY](#job-seed-key) - Obtain security access to the ECU
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden

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

Information bzgl. SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergeraet im Klartext Name of the ECU |
| ORIGIN | string | Steuergeraete-Verantwortlicher Person responsible For this file (Rover/BMW) |
| REVISION | string | Versions-Nummer Version Number (Form abc.xyz) |
| AUTHOR | string | Namen aller Autoren Author List |
| COMMENT | string | wichtige Hinweise General Comment about file |
| SPRACHE | string | deutsch / english |

<a id="job-ident"></a>
### IDENT

Identification data

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer BMW Part Number |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_DAY | int | Herstelldatum tag Day of manufacture |
| ID_DATUM_MONTH | int | Herstelldatum monat Month of manufacture |
| ID_DATUM_JAHR | int | Herstelldatum Jahr Year of manufacture |
| ID_SW_NR | int | Software version |
| ID_LIEF_NR | int | Lieferanten-Nummer Supplier code |
| ID_LIEF_TEXT | string | Lieferanten-Text Supplier Name |
| ID_AIF_VORHANDEN | int | 1, If AIF data is available |
| ID_SYSTEM_NAME | int | System Name |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-ident-extended"></a>
### IDENT_EXTENDED

Identification data

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_TEMIC_SERIAL_NR | string | Temic ecu serial number |
| ID_PROGRAMMING_DAY | int | ECU programming date Day |
| ID_PROGRAMMING_MONTH | int | ECU programming date month |
| ID_PROGRAMMING_YEAR | int | ECU programming date year |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-vin-lesen"></a>
### VIN_LESEN

Identification data

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_VIN | string | Vehicle Identification number |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-vin-schreiben"></a>
### VIN_SCHREIBEN

Write thge VIN to the ECU

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VIN | string | Vehicle Identification number |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-programming-date-schreiben"></a>
### PROGRAMMING_DATE_SCHREIBEN

Write the programming date to the ECU

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DAY | int | Program day |
| MONTH | int | Program month |
| YEAR | int | Program year |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-zcs-lesen"></a>
### ZCS_LESEN

Auslesen des Zentralen Codierschluessels aus Flash

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| GM | string | Zentralcode C1 - Grundmerkmal (8 ASCII nos + 1 ASCII c/sum) |
| SA | string | Zentralcode C2 - Sonderausstattung (16 ASCII nos + 1 ASCII c/sum) |
| VN | string | Zentralcode C3 - Versionsmerkmal (10 ASCII nos + 1 ASCII c/sum) |
| _TEL_ANTWORT1 | binary |  |
| _TEL_ANTWORT2 | binary |  |

<a id="job-zcs-schreiben"></a>
### ZCS_SCHREIBEN

Write the ZCS record

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GM | string | Zentralcode C1 - Grundmerkmal (8 ASCII nos + 1 ASCII c/sum) |
| SA | string | Zentralcode C2 - Sonderausstattung (16 ASCII nos + 1 ASCII c/sum) |
| VN | string | Zentralcode C3 - Versionsmerkmal (10 ASCII nos + 1 ASCII c/sum) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT1 | binary |  |
| _TEL_ANTWORT2 | binary |  |

<a id="job-start-diagnostics"></a>
### START_DIAGNOSTICS

Begins a diagnostic session

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int | Diagnostic mode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-sg-reset"></a>
### SG_RESET

Reset the ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-fs-lesen"></a>
### FS_LESEN

Read faults

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_HEX_CODE | binary | Raw fault data from the ECU |
| F_ORT_NR | int | Fault number as an integer |
| F_ORT_TEXT | string | Fault description |
| F_HFK | int | Frequency |
| F_UW_ANZ | int | Count of Environment Data Items per fault |
| F_ART_ANZ | int | Count of additional fault status information |
| F_ART1_NR | int | Fault status 1 |
| F_ART1_TEXT | string | Fault status text 1 |
| F_ART2_NR | int | Fault status 2 |
| F_ART2_TEXT | string | Fault status text 2 |
| F_ART3_NR | int | Fault status 3 |
| F_ART3_TEXT | string | Fault status text 3 |
| F_ART4_NR | int | Fault status 4 |
| F_ART4_TEXT | string | Fault status text 4 |
| F_ART5_NR | int | Fault status 5 |
| F_ART5_TEXT | string | Fault status text 5 |
| F_ART6_NR | int | Fault status 6 |
| F_ART6_TEXT | string | Fault status text 6 |
| F_ART7_NR | int | Fault status 7 |
| F_ART7_TEXT | string | Fault status text 7 |
| F_ART8_NR | int | Fault status 8 |
| F_ART8_TEXT | string | Fault status text 8 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Clears All Faults

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-status-io-digital-04"></a>
### STATUS_IO_DIGITAL_04

Read digitals for LID 04 - Equipment configuration

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AIRBAG_DRV_1_ENABLED | int | Airbag driver 1 |
| STAT_BELT_PRE_DRV_ENABLED | int | Belt pretensioner driver |
| STAT_BELT_PRE_PSNGR_ENABLED | int | Belt pretensioner passenger |
| STAT_AIRBAG_PSNGR_1_ENABLED | int | Airbag passneger |
| STAT_SIDEBAG_FRONT_LEFT_ENABLED | int | Sidebag font left seat |
| STAT_SIDEBAG_FRONT_RIGHT_ENABLED | int | Sidebag font right seat |
| STAT_BELT_PRE_REAR_LEFT_ENABLED | int | Belt pretensioner rear left |
| STAT_BELT_PRE_REAR_RIGHT_ENABLED | int | Belt pretensioner rear right |
| STAT_ITS_FRONT_LEFT_ENABLED | int | ITS front left |
| STAT_ITS_FRONT_RIGHT_ENABLED | int | ITS front right |
| STAT_AIRBAG_DRV_2_ENABLED | int | Airbag driver 2 |
| STAT_AIRBAG_PSNGR_2_ENABLED | int | Airbag passenger 2 |
| STAT_BELT_BUCKLE_DRIVER_ENABLED | int | Belt Buckle driver enabled |
| STAT_BELT_BUCKLE_PSNGR_ENABLED | int | Belt Buckle passenger enabled |
| STAT_OC_SENSOR_ACTIVE | int | OC Sensor active |
| STAT_RFIS_ACTIVE | int | Rear facing infant sensor active |
| STAT_MRSA_FRONT_SELECTED | int | MRSA front selected |
| STAT_MRSA_REAR_SELECTED | int | MRSA rear selected |
| STAT_RFIS_LAMP_ENABLED | int | Rear facing infant sensor lamp enabled |
| STAT_US_VERSION_ENABLED | int | US version enabled |
| STAT_AIRBAG_DRV_1_DUP_ENABLED | int | Airbag driver 1 |
| STAT_BELT_PRE_DRV_DUP_ENABLED | int | Belt pretensioner driver |
| STAT_BELT_PRE_PSNGR_DUP_ENABLED | int | Belt pretensioner passenger |
| STAT_AIRBAG_PSNGR_1_DUP_ENABLED | int | Airbag passneger |
| STAT_SIDEBAG_FRONT_LEFT_DUP_ENABLED | int | Sidebag font left seat |
| STAT_SIDEBAG_FRONT_RIGHT_DUP_ENABLED | int | Sidebag font right seat |
| STAT_BELT_PRE_REAR_LEFT_DUP_ENABLED | int | Belt pretensioner rear left |
| STAT_BELT_PRE_REAR_RIGHT_DUP_ENABLED | int | Belt pretensioner rear right |
| STAT_ITS_FRONT_LEFT_DUP_ENABLED | int | ITS front left |
| STAT_ITS_FRONT_RIGHT_DUP_ENABLED | int | ITS front right |
| STAT_AIRBAG_DRV_2_DUP_ENABLED | int | Airbag driver 2 |
| STAT_AIRBAG_PSNGR_2_DUP_ENABLED | int | Airbag passenger 2 |
| STAT_BELT_BUCKLE_DRIVER_DUP_ENABLED | int | Belt Buckle driver enabled |
| STAT_BELT_BUCKLE_PSNGR_DUP_ENABLED | int | Belt Buckle passenger enabled |
| STAT_OC_SENSOR_DUP_ACTIVE | int | OC Sensor active |
| STAT_RFIS_DUP_ACTIVE | int | Rear facing infant sensor active |
| STAT_MRSA_FRONT_DUP_SELECTED | int | MRSA front selected |
| STAT_MRSA_REAR_DUP_SELECTED | int | MRSA rear selected |
| STAT_RFIS_LAMP_DUP_ENABLED | int | Rear facing infant sensor lamp enabled |
| STAT_US_VERSION_DUP_ENABLED | int | US version enabled |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-status-io-digital-16"></a>
### STATUS_IO_DIGITAL_16

Read digitals for LID 16 - ODS Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PSNGR_SEAT_OCCUPIED_DETECTED | int | Passenger seat occupied |
| STAT_REAR_FACING_CHILD_SEAT_DETECTED | int | Reare facing child seat deetcted |
| STAT_OC_SENSOR_STATUS0_ACTIVE | int | OC Sensor status0 (SBE2) status 0 active |
| STAT_OC_SENSOR_STATUS1_ACTIVE | int | OC Sensor status1 (SBE2) status 1 active |
| STAT_OC_SENSOR_STATUS2_ACTIVE | int | OC Sensor status2 (SBE2) status 2 active |
| STAT_OC_SENSOR_STATUS3_ACTIVE | int | OC Sensor status3 (SBE2) status 3 active |
| STAT_OC_SENSOR_STATUS4_ACTIVE | int | OC Sensor status4 (SBE2) status 4 active |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-status-analogue-lock-byte"></a>
### STATUS_ANALOGUE_LOCK_BYTE

Read lock byte value LID 15

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |
| STAT_LOCK_BYTE_WERT | real | Lock byte value |
| STAT_LOCK_BYTE_EINH | string | Lock byte units |

<a id="job-lock-byte-schreiben"></a>
### LOCK_BYTE_SCHREIBEN

Write lock byte value LID 34

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Lock byte value |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-airbag-drv-1-schreiben"></a>
### AIRBAG_DRV_1_SCHREIBEN

Write Airbag driver 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Enable / Disable value |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-belt-pre-drv-schreiben"></a>
### BELT_PRE_DRV_SCHREIBEN

Write Belt pretensioner driver

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-belt-pre-psngr-schreiben"></a>
### BELT_PRE_PSNGR_SCHREIBEN

Write Belt pretensioner passenger

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-airbag-psngr-1-schreiben"></a>
### AIRBAG_PSNGR_1_SCHREIBEN

Write Airbag passneger

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-sidebag-front-left-schreiben"></a>
### SIDEBAG_FRONT_LEFT_SCHREIBEN

Write Sidebag font left seat

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-sidebag-front-right-schreiben"></a>
### SIDEBAG_FRONT_RIGHT_SCHREIBEN

Write Sidebag font right seat

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-belt-pre-rear-left-schreiben"></a>
### BELT_PRE_REAR_LEFT_SCHREIBEN

Write Belt pretensioner rear left

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-belt-pre-rear-right-schreiben"></a>
### BELT_PRE_REAR_RIGHT_SCHREIBEN

Write Belt pretensioner rear right

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-its-front-left-schreiben"></a>
### ITS_FRONT_LEFT_SCHREIBEN

Write ITS front left

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-its-front-right-schreiben"></a>
### ITS_FRONT_RIGHT_SCHREIBEN

Write ITS front right

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-airbag-drv-2-schreiben"></a>
### AIRBAG_DRV_2_SCHREIBEN

Write Airbag driver 2

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-airbag-psngr-2-schreiben"></a>
### AIRBAG_PSNGR_2_SCHREIBEN

Write Airbag passenger 2

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-belt-buckle-driver-schreiben"></a>
### BELT_BUCKLE_DRIVER_SCHREIBEN

Write Belt Buckle driver

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-belt-buckle-psngr-schreiben"></a>
### BELT_BUCKLE_PSNGR_SCHREIBEN

Write Belt Buckle passenger enabled

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-oc-sensor-active-schreiben"></a>
### OC_SENSOR_ACTIVE_SCHREIBEN

Write OC Sensor active

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-rfis-schreiben"></a>
### RFIS_SCHREIBEN

Write Rear facing infant sensor active

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-mrsa-front-schreiben"></a>
### MRSA_FRONT_SCHREIBEN

Write MRSA front selected

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-mrsa-rear-schreiben"></a>
### MRSA_REAR_SCHREIBEN

Write MRSA rear selected

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-rfis-lamp-schreiben"></a>
### RFIS_LAMP_SCHREIBEN

Write  Rear facing infant sensor lamp enabled

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-us-version-schreiben"></a>
### US_VERSION_SCHREIBEN

Write US version enabled

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-airbag-drv-1-dup-schreiben"></a>
### AIRBAG_DRV_1_DUP_SCHREIBEN

Write Airbag driver 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Enable / Disable value |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-belt-pre-drv-dup-schreiben"></a>
### BELT_PRE_DRV_DUP_SCHREIBEN

Write Belt pretensioner driver

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-belt-pre-psngr-dup-schreiben"></a>
### BELT_PRE_PSNGR_DUP_SCHREIBEN

Write Belt pretensioner passenger

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-airbag-psngr-1-dup-schreiben"></a>
### AIRBAG_PSNGR_1_DUP_SCHREIBEN

Write Airbag passneger

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-sidebag-front-left-dup-schreiben"></a>
### SIDEBAG_FRONT_LEFT_DUP_SCHREIBEN

Write Sidebag font left seat

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-sidebag-front-right-dup-schreiben"></a>
### SIDEBAG_FRONT_RIGHT_DUP_SCHREIBEN

Write Sidebag font right seat

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-belt-pre-rear-left-dup-schreiben"></a>
### BELT_PRE_REAR_LEFT_DUP_SCHREIBEN

Write Belt pretensioner rear left

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-belt-pre-rear-right-dup-schreiben"></a>
### BELT_PRE_REAR_RIGHT_DUP_SCHREIBEN

Write Belt pretensioner rear right

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-its-front-left-dup-schreiben"></a>
### ITS_FRONT_LEFT_DUP_SCHREIBEN

Write ITS front left

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-its-front-right-dup-schreiben"></a>
### ITS_FRONT_RIGHT_DUP_SCHREIBEN

Write ITS front right

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-airbag-drv-2-dup-schreiben"></a>
### AIRBAG_DRV_2_DUP_SCHREIBEN

Write Airbag driver 2

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-airbag-psngr-2-dup-schreiben"></a>
### AIRBAG_PSNGR_2_DUP_SCHREIBEN

Write Airbag passenger 2

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-belt-buckle-driver-dup-schreiben"></a>
### BELT_BUCKLE_DRIVER_DUP_SCHREIBEN

Write Belt Buckle driver

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-belt-buckle-psngr-dup-schreiben"></a>
### BELT_BUCKLE_PSNGR_DUP_SCHREIBEN

Write Belt Buckle passenger enabled

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-oc-sensor-dup-schreiben"></a>
### OC_SENSOR_DUP_SCHREIBEN

Write OC Sensor active

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-rfis-dup-schreiben"></a>
### RFIS_DUP_SCHREIBEN

Write Rear facing infant sensor active

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-mrsa-front-dup-schreiben"></a>
### MRSA_FRONT_DUP_SCHREIBEN

Write MRSA front selected

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-mrsa-rear-dup-schreiben"></a>
### MRSA_REAR_DUP_SCHREIBEN

Write MRSA rear selected

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-rfis-lamp-dup-schreiben"></a>
### RFIS_LAMP_DUP_SCHREIBEN

Write  Rear facing infant sensor lamp enabled

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-us-version-dup-schreiben"></a>
### US_VERSION_DUP_SCHREIBEN

Write US version enabled

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Airbag driver 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Ping message

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-seed-key"></a>
### SEED_KEY

Obtain security access to the ECU

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int | Security access mode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response as a hex string |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (30 × 2)
- [LIEFERANTEN](#table-lieferanten) (47 × 2)
- [FORTTEXTE](#table-forttexte) (91 × 2)
- [FARTTEXTE](#table-farttexte) (13 × 2)
- [ANALOGUE](#table-analogue) (2 × 4)
- [DIGITAL](#table-digital) (48 × 4)
- [DIGITALARGUMENT](#table-digitalargument) (12 × 2)
- [MONTHS](#table-months) (13 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 30 rows × 2 columns

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
| 0x92 | ERROR_ECU_RESERVED_BY_DOCUMENT |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 47 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen / Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe |
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
| 0x28 | DODUCO |
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
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 91 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9000 | ECU Internes Fehler |
| 0x9001 | Versogungspannung: Niedrig Spannung |
| 0x9003 | Airbag Warnlichte (AWL): Short to +Ve or Driver defect |
| 0x9004 | Airbag Warnlichte (AWL): Short to Ground or Open circuit |
| 0x9005 | Zukundskreis IC0 (Fahrer Airbag): Short to Ground |
| 0x9006 | Zukundskreis IC0 (Fahrer Airbag): Short to +Ve |
| 0x9007 | Zukundskreis IC0 (Fahrer Airbag): Resistance too low |
| 0x9008 | Zukundskreis IC0 (Fahrer Airbag): Resistance too high |
| 0x9009 | Zukundskreis IC3 (Airbag Passenger): Short to Ground |
| 0x9010 | Zukundskreis IC3 (Airbag Passenger): Short to +Ve |
| 0x9011 | Zukundskreis IC3 (Airbag Passenger): Resistance too low |
| 0x9012 | Zukundskreis IC3 (Airbag Passenger): Resistance too high |
| 0x9013 | Zukundskreis IC6 (Gurtstrammer links): Short to Ground |
| 0x9014 | Zukundskreis IC6 (Gurtstrammer links): Short to +Ve |
| 0x9015 | Zukundskreis IC6 (Gurtstrammer links): Resistance too low |
| 0x9016 | Zukundskreis IC6 (Gurtstrammer links): Resistance too high |
| 0x9017 | Zukundskreis IC7 (Gurtstrammer rechts): Short to Ground |
| 0x9018 | Zukundskreis IC7 (Gurtstrammer rechts): Short to +Ve |
| 0x9019 | Zukundskreis IC7 (Gurtstrammer rechts): Resistance too low |
| 0x9020 | Zukundskreis IC7 (Gurtstrammer rechts): Resistance too high |
| 0x9021 | Zukundskreis IC8 (Gurtstrammer hinten links): Short to Ground |
| 0x9022 | Zukundskreis IC8 (Gurtstrammer hinten links): Short to +Ve |
| 0x9023 | Zukundskreis IC8 (Gurtstrammer hinten links): Resistance too low |
| 0x9024 | Zukundskreis IC8 (Gurtstrammer hinten links): Resistance too high |
| 0x9025 | Zukundskreis IC9 (Gurtstrammer hinten rechts): Short to Ground |
| 0x9026 | Zukundskreis IC9 (Gurtstrammer hinten rechts): Short to +Ve |
| 0x9027 | Zukundskreis IC9 (Gurtstrammer hinten rechts): Resistance too low |
| 0x9028 | Zukundskreis IC9 (Gurtstrammer hinten rechts): Resistance too high |
| 0x9029 | Zukundskreis IC10 (Gurtstrammer hinten mitte): Short to Ground |
| 0x9030 | Zukundskreis IC10 (Gurtstrammer hinten mitte): Short to +Ve |
| 0x9031 | Zukundskreis IC10 (Gurtstrammer hinten mitte): Resistance too low |
| 0x9032 | Zukundskreis IC10 (Gurtstrammer hinten mitte): Resistance too high |
| 0x9033 | Zukundskreis IC4 (Seitenairbag vorne links): Short to Ground |
| 0x9034 | Zukundskreis IC4 (Seitenairbag vorne links): Short to +Ve |
| 0x9035 | Zukundskreis IC4 (Seitenairbag vorne links): Resistance too low |
| 0x9036 | Zukundskreis IC4 (Seitenairbag vorne links): Resistance too high |
| 0x9037 | Zukundskreis IC5 (Seitenairbag vorne rechts): Short to Ground |
| 0x9038 | Zukundskreis IC5 (Seitenairbag vorne rechts): Short to +Ve |
| 0x9039 | Zukundskreis IC5 (Seitenairbag vorne rechts): Resistance too low |
| 0x9040 | Zukundskreis IC5 (Seitenairbag vorne rechts): Resistance too high |
| 0x9041 | Zukundskreis IC1 (ITS vorne links): Short to Ground |
| 0x9042 | Zukundskreis IC1 (ITS vorne links): Short to +Ve |
| 0x9043 | Zukundskreis IC1 (ITS vorne links): Resistance too low |
| 0x9044 | Zukundskreis IC1 (ITS vorne links): Resistance too high |
| 0x9045 | Zukundskreis IC2 (ITS vorne rechts): Short to Ground |
| 0x9046 | Zukundskreis IC2 (ITS vorne rechts): Short to +Ve |
| 0x9047 | Zukundskreis IC2 (ITS vorne rechts): Resistance too low |
| 0x9048 | Zukundskreis IC2 (ITS vorne rechts): Resistance too high |
| 0x9049 | Zukundskreis IC11 (Ubat Disconnect): Short to Ground |
| 0x9050 | Zukundskreis IC11 (Ubat Disconnect): Short to +Ve |
| 0x9051 | Zukundskreis IC11 (Ubat Disconnect): Resistance too low |
| 0x9052 | Zukundskreis IC11 (Ubat Disconnect): Resistance too high |
| 0x9081 | Zukundskreis IC0 (Fahrer Airbag): Plausibility Fehler |
| 0x9082 | Zukundskreis IC3 (Airbag Passenger): Plausibility Fehler |
| 0x9083 | Zukundskreis IC6 (Gurtstrammer links): Plausibility Fehler |
| 0x9084 | Zukundskreis IC7 (Gurtstrammer rechts): Plausibility Fehler |
| 0x9085 | Zukundskreis IC8 (Gurtstrammer hinten links): Plausibility Fehler |
| 0x9086 | Zukundskreis IC9 (Gurtstrammer hinten rechts): Plausibility Fehler |
| 0x9087 | Zukundskreis IC10 (Gurtstrammer hinten mitte): Plausibility Fehler |
| 0x9088 | Zukundskreis IC4 (Seitenairbag vorne links): Plausibility Fehler |
| 0x9089 | Zukundskreis IC5 (Seitenairbag vorne rechts): Plausibility Fehler |
| 0x9090 | Zukundskreis IC1 (ITS vorne links): Plausibility Fehler |
| 0x9099 | Zukundskreis IC2 (ITS vorne rechts): Plausibility Fehler |
| 0x9100 | Zukundskreis IC11 (Ubat Disconnect): Plausibility Fehler |
| 0x9111 | Fahrersitz Schlossschalter: Resistance too low or Short to Ground |
| 0x9112 | Fahrersitz Schlossschalter: Resistance in grey area or not defined |
| 0x9113 | Fahrersitz Schlossschalter: Resistance too high / open / short to +Ve |
| 0x9114 | Fahrersitz Schlossschalter: Plausibility Fehler |
| 0x9121 | Beifahrersitz Schlossschalter: Resistance too low or Short to Ground |
| 0x9122 | Beifahrersitz Schlossschalter: Resistance in grey area or not defined |
| 0x9123 | Beifahrersitz Schlossschalter: Resistance too high / open / short to +Ve |
| 0x9124 | Beifahrersitz Schlossschalter: Plausibility Fehler |
| 0x9131 | Seitensensor links: Falsche Algorithm Parameter |
| 0x9132 | Seitensensor links: Plausibility Fehler |
| 0x9133 | Seitensensor links: Internes Fehler  |
| 0x9134 | Seitensensor links: Communication Fehler |
| 0x9141 | Seitensensor Rechts: Falsche Algorithm Parameter |
| 0x9142 | Seitensensor Rechts: Plausibility Fehler |
| 0x9143 | Seitensensor Rechts: Internes Fehler  |
| 0x9144 | Seitensensor Rechts: Communication Fehler |
| 0x9151 | RFIS Sensor: Internes RFIS Sensor Fehler |
| 0x9152 | RFIS Sensor: Schelcht Signal Stand |
| 0x9153 | RFIS Sensor: Freeze / Defreeze Fehler |
| 0x9154 | RFIS Sensor: Communication Fehler |
| 0x9155 | RFIS Sensor: Seriel Link Short to Ground |
| 0x9156 | RFIS Sensor: Seriel Link Short to +Ve |
| 0x9157 | RFIS Sensor: Plausibility Fehler |
| 0x9161 | RFIS Standlampe (HWL): Short to +Ve or Driver defect |
| 0x9162 | RFIS Standlampe (HWL): Short to Ground or Open circuit |
| 0x9200 | Unfall Telegram memory: Mindestens eine Unfall detected |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 13 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | No fault symptom available for this DTC |
| 0x02 | Above maximum threshold |
| 0x03 | Below minimum threshold |
| 0x04 | Open Circuit |
| 0x05 | Leakage / Short to Ground |
| 0x06 | Leakage / Short to Ubat |
| 0x07 | No DTC present |
| 0x08 | DTC is Sporadic |
| 0x09 | DTC is Present |
| 0x0A | No Error present |
| 0x0B | Error Present |
| 0xFF | Unknown Error |

<a id="table-analogue"></a>
### ANALOGUE

Dimensions: 2 rows × 4 columns

| NAME | FACT_A | FACT_B | EINH |
| --- | --- | --- | --- |
| LOCK_BYTE | 1.0 | 0.0 |  |
| ?? | 0.0 | 0.0 | ?? |

<a id="table-digital"></a>
### DIGITAL

Dimensions: 48 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| AIRBAG_DRV_1_ENABLED | 6 | 0x01 | 0x01 |
| BELT_PRE_DRV_ENABLED | 6 | 0x02 | 0x02 |
| BELT_PRE_PSNGR_ENABLED | 6 | 0x04 | 0x04 |
| AIRBAG_PSNGR_1_ENABLED | 6 | 0x08 | 0x08 |
| SIDEBAG_FRONT_LEFT_ENABLED | 6 | 0x10 | 0x10 |
| SIDEBAG_FRONT_RIGHT_ENABLED | 6 | 0x20 | 0x20 |
| BELT_PRE_REAR_LEFT_ENABLED | 6 | 0x40 | 0x40 |
| BELT_PRE_REAR_RIGHT_ENABLED | 6 | 0x80 | 0x80 |
| ITS_FRONT_LEFT_ENABLED | 7 | 0x01 | 0x01 |
| ITS_FRONT_RIGHT_ENABLED | 7 | 0x02 | 0x02 |
| AIRBAG_DRV_2_ENABLED | 7 | 0x04 | 0x04 |
| AIRBAG_PSNGR_2_ENABLED | 7 | 0x08 | 0x08 |
| BELT_BUCKLE_DRIVER_ENABLED | 8 | 0x01 | 0x01 |
| BELT_BUCKLE_PSNGR_ENABLED | 8 | 0x02 | 0x02 |
| OC_SENSOR_ACTIVE | 8 | 0x10 | 0x10 |
| RFIS_ACTIVE | 8 | 0x20 | 0x20 |
| MRSA_FRONT_SELECTED | 9 | 0x01 | 0x01 |
| MRSA_REAR_SELECTED | 9 | 0x02 | 0x02 |
| RFIS_LAMP_ENABLED | 9 | 0x08 | 0x08 |
| US_VERSION_ENABLED | 9 | 0x80 | 0x80 |
| AIRBAG_DRV_1_DUP_ENABLED | 10 | 0x01 | 0x01 |
| BELT_PRE_DRV_DUP_ENABLED | 10 | 0x02 | 0x02 |
| BELT_PRE_PSNGR_DUP_ENABLED | 10 | 0x04 | 0x04 |
| AIRBAG_PSNGR_1_DUP_ENABLED | 10 | 0x08 | 0x08 |
| SIDEBAG_FRONT_LEFT_DUP_ENABLED | 10 | 0x10 | 0x10 |
| SIDEBAG_FRONT_RIGHT_DUP_ENABLED | 10 | 0x20 | 0x20 |
| BELT_PRE_REAR_LEFT_DUP_ENABLED | 10 | 0x40 | 0x40 |
| BELT_PRE_REAR_RIGHT_DUP_ENABLED | 10 | 0x80 | 0x80 |
| ITS_FRONT_LEFT_DUP_ENABLED | 11 | 0x01 | 0x01 |
| ITS_FRONT_RIGHT_DUP_ENABLED | 11 | 0x02 | 0x02 |
| AIRBAG_DRV_2_DUP_ENABLED | 11 | 0x04 | 0x04 |
| AIRBAG_PSNGR_2_DUP_ENABLED | 11 | 0x08 | 0x08 |
| BELT_BUCKLE_DRIVER_DUP_ENABLED | 12 | 0x01 | 0x01 |
| BELT_BUCKLE_PSNGR_DUP_ENABLED | 12 | 0x02 | 0x02 |
| OC_SENSOR_DUP_ACTIVE | 12 | 0x10 | 0x10 |
| RFIS_DUP_ACTIVE | 12 | 0x20 | 0x20 |
| MRSA_FRONT_DUP_SELECTED | 13 | 0x01 | 0x01 |
| MRSA_REAR_DUP_SELECTED | 13 | 0x02 | 0x02 |
| RFIS_LAMP_DUP_ENABLED | 13 | 0x08 | 0x08 |
| US_VERSION_DUP_ENABLED | 13 | 0x80 | 0x80 |
| PSNGR_SEAT_OCCUPIED_DETECTED | 6 | 0x02 | 0x02 |
| REAR_FACING_CHILD_SEAT_DETECTED | 6 | 0x04 | 0x04 |
| OC_SENSOR_STATUS0_ACTIVE | 6 | 0x08 | 0x08 |
| OC_SENSOR_STATUS1_ACTIVE | 6 | 0x10 | 0x10 |
| OC_SENSOR_STATUS2_ACTIVE | 6 | 0x20 | 0x20 |
| OC_SENSOR_STATUS3_ACTIVE | 6 | 0x40 | 0x40 |
| OC_SENSOR_STATUS4_ACTIVE | 6 | 0x80 | 0x80 |
| ?? | 0 | 0x00 | 0x00 |

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 12 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| yes | 1 |
| no | 0 |
| on | 1 |
| off | 0 |
| true | 1 |
| false | 0 |
| 1 | 1 |
| 0 | 0 |

<a id="table-months"></a>
### MONTHS

Dimensions: 13 rows × 2 columns

| MONTH | DAYS |
| --- | --- |
| 0x01 | 31 |
| 0x02 | 28 |
| 0x03 | 31 |
| 0x04 | 30 |
| 0x05 | 31 |
| 0x06 | 30 |
| 0x07 | 31 |
| 0x08 | 31 |
| 0x09 | 30 |
| 0x0A | 31 |
| 0x0B | 30 |
| 0x0C | 31 |
| 0 | 0 |
