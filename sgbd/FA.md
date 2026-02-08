# FA.PRG

- Jobs: [4](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Special SGBD used by coding system |
| ORIGIN | BMW TI-431 Nau |
| REVISION | 1.03 |
| AUTHOR | BMW TI-431 Dennert, BMW TI-431 Nau |
| COMMENT | N/A |
| PACKAGE | 1.24 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [INFO](#job-info) - Information SGBD
- [FA_STREAM2STRUCT](#job-fa-stream2struct) - Decoding of 'Fahrzeugauftrag' Further fuctionality: extraction of files according to memory type Further results VERSION, BR and C_TYP will be created during run time Further results C_DATE, LACK and POLSTER will be created during run time Further results ZUSBAU_XXX (1 ... ZUSBAU_ANZ) will be created during run time 'ZUSBAU-Nummer' as a 4-digit string. The number of results depends on ZUSBAU_ANZ. X corresponds to the variable number. Further results E_WORT_XXX (1 ... E_WORT_ANZ) will be created during run time 'Ergaenzungswort' as a 4-digit string. The number of results depends on E_WORT_ANZ. X corresponds to the variable number. Further results SA_XXX (1 ... SA_ANZ) will be created during run time 'SA' as a 4-digit string. The number of results depends on SA_ANZ. X corresponds to the variable number. Further results HO_XXX (1 ... HO_ANZ) will be created during run time 'HO' as a 4-digit string. The number of results depends on HO_ANZ. X corresponds to the variable number. Further result COMPRESSED_STREAM will be created during run time depending on parameter 'VERSION'
- [FA_STREAM_FOR_ECU](#job-fa-stream-for-ecu) - Conversion of 'Fahrzeugauftrag' from the application into Fahrzeugauftrag for the ECU. No identifiers will be provided by the application

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 if done |

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

<a id="job-fa-stream2struct"></a>
### FA_STREAM2STRUCT

Decoding of 'Fahrzeugauftrag' Further fuctionality: extraction of files according to memory type Further results VERSION, BR and C_TYP will be created during run time Further results C_DATE, LACK and POLSTER will be created during run time Further results ZUSBAU_XXX (1 ... ZUSBAU_ANZ) will be created during run time 'ZUSBAU-Nummer' as a 4-digit string. The number of results depends on ZUSBAU_ANZ. X corresponds to the variable number. Further results E_WORT_XXX (1 ... E_WORT_ANZ) will be created during run time 'Ergaenzungswort' as a 4-digit string. The number of results depends on E_WORT_ANZ. X corresponds to the variable number. Further results SA_XXX (1 ... SA_ANZ) will be created during run time 'SA' as a 4-digit string. The number of results depends on SA_ANZ. X corresponds to the variable number. Further results HO_XXX (1 ... HO_ANZ) will be created during run time 'HO' as a 4-digit string. The number of results depends on HO_ANZ. X corresponds to the variable number. Further result COMPRESSED_STREAM will be created during run time depending on parameter 'VERSION'

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | string | Possiblilties: '1' for the total stream-block, if the total stream lenght is &lt; 1kByte '2' for the first stream-block, if the total stream length is &gt; 1kByte '3' for the following stream-blocks, if the total stream length is &gt; 1kByte |
| FA_STREAM | string | 'Fahrzeugauftrag' as a data-array. Maximum array-length in total: 1 kByte Only the active constituents will be filtered out. If the array is longer than 1 kByte it will be separated from the calling application into two blocks. Particular results will be dynamicly generated during run time. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY -&gt; FA present and interpretable ERROR_NO_FA -&gt; 'Fahrzeugauftrag' (FA_STREAM) not present or filled with 0x00 or 0xFF ERROR_STRINGLENGTH, ERROR_BR, ... |
| STANDARD_FA | string | Standard 'Fahrzeugauftrag' (equals to 'Fahrzeugauftrag' without VERSION and incactive constituents) |
| SA_ANZ | int | Number of saved 'SA's' Particular results for the 'SA's' (3 digits each) will be dynamicly generated during run time |
| E_WORT_ANZ | int | Number of saved 'E-Worte' Particular results for the 'E-Worte' (4 digits each) will be dynamicly generated during run time. |
| HO_WORT_ANZ | int | Number of saved 'HO-Worte' Particular results for the 'HO-Worte' (4 digits each) will be dynamicly generated during run time. |
| ZUSBAU_ANZ | int | Number of saved 'ZusBau-Nummern' Particular results for the 'ZusBau-Nummern' (7 digits each) will be dynamicly generated during run time. |

<a id="job-fa-stream-for-ecu"></a>
### FA_STREAM_FOR_ECU

Conversion of 'Fahrzeugauftrag' from the application into Fahrzeugauftrag for the ECU. No identifiers will be provided by the application

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | string | Possiblilties: '1' for the total stream-block, if the total stream lenght is &lt; 1kByte '2' for the first stream-block, if the total stream length is &gt; 1kByte '3' for the following stream-blocks, if the total stream length is &gt; 1kByte |
| VERSION | string | VERSION comes from application (Oberflaeche) in any case |
| FA_STREAM_OF | string | 'Fahrzeugauftrag' from application (without VERSION, and only active constituents), corresponds to Standard FA-stream This argument is always present |
| FA_STREAM_ECU | string | 'Fahrzeugauftrag' from ECU as a data array (with VERSION, active and depending on memory type, inactive constituents). Maximum array-length in total: 1kByte Only the active constituents will be filtered out. Case empty Memory: FA_STREAM_ECU = ''. If the array is longer than 1 kByte it will be separated from the calling application into two blocks. Particular results will be dynamicly generated during run time. This argument not always present |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY -&gt; 'Fahrzeugauftrag'-conversion was successful |
| FA_STREAM_FOR_ECU | string | 'Fahrzeugauftrag' for ECU in certain representation depending on parameter VERSION |
| FA_STREAM_FOR_ECU_BIN | binary | 'Fahrzeugauftrag' for ECU in binary representation |
| DIFFERENCE | int | Number of differences (add, del, change) in streams Master is FA_STREAM_ECU |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (30 × 2)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 2 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0C | KWP2000 |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 30 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x01 | ERROR_NO_FA |
| 0x02 | ERROR_UNKNOWN_CONSTIT |
| 0x03 | ERROR_UNKNOWN_IDENTIFIER |
| 0x04 | ERROR_STRINGLENGTH |
| 0x05 | ERROR_TOTAL_STRING_LENGTH |
| 0x06 | ERROR_POSCOUNTER |
| 0x07 | ERROR_ACTIVE_TYPSCHLUESSELANZAHL_&gt;_1 |
| 0x08 | ERROR_ACTIVE_TYPSCHLUESSELANZAHL_!=_1 |
| 0x09 | ERROR_ACTIVE_C_DATE_NUMBER_&gt;_1 |
| 0x0A | ERROR_ACTIVE_C_DATE_NUMBER_!=_1 |
| 0x0B | ERROR_ACTIVE_LACK_NUMBER_&gt;_1 |
| 0x0C | ERROR_ACTIVE_LACK_NUMBER_!=_1 |
| 0x0D | ERROR_ACTIVE_POLSTER_NUMBER_&gt;_1 |
| 0x0E | ERROR_ACTIVE_POLSTER_NUMBER_!=_1 |
| 0x0F | ERROR_ACTIVE_ZUSBAU_NUMBER_&gt;_3 |
| 0x10 | ERROR_VERSION |
| 0x11 | ERROR_BR |
| 0x12 | ERROR_TYPSCHLUESSEL |
| 0x13 | ERROR_C_DATE |
| 0x14 | ERROR_LACK |
| 0x15 | ERROR_POLSTER |
| 0x16 | ERROR_ZUSBAUNUMMER |
| 0x17 | ERROR_SA |
| 0x18 | ERROR_E_WORT |
| 0x19 | ERROR_HO_WORT |
| 0x1A | ERROR_PAR_VERSION_NOT_PRESENT |
| 0x1B | ERROR_PAR_FA_STREAM_OF_NOT_PRESENT |
| 0x1C | ERROR_INVALID_BLOCK_0 |
| 0x1D | ERROR_BLOCK_0_NOT_PRESENT |
| 0xXY | ERROR_UNKNOWN |
