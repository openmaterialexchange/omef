# Data Models

## Chemical Composition

### Model
[filename](_media/chemical_composition.json ':include')

### Description
| Property name      | Data type        | Required                                                                       | Description                                                                              | Allowed values                                                                                                                                                                                                                                                    |
|--------------------|------------------|--------------------------------------------------------------------------------|------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| client             | string           | yes                                                                            | company name of the company which requested the test                                     |                                                                                                                                                                                                                                                                   |
| lab                | string           | yes                                                                            | company name of the laboratory which performs the test                                   |                                                                                                                                                                                                                                                                   |
| testStandard       | string           | yes                                                                            |                                                                                          | ["ASTM E1086-14", "ASTM E415-17", "ASTM E415-21", "ASTM E3047-16", "Element SOP 20-02", "EN 10315 (2006)", "EN ISO 15350 (2000)", "CR 10320 (2004)"] or custom string                                                                                             |
| fdpt               | boolean          | no                                                                             |                                                                                          |                                                                                                                                                                                                                                                                   |
| norm               | string           | yes                                                                            |                                                                                          |                                                                                                                                                                                                                                                                   |
| grade              | string           | yes                                                                            |                                                                                          |                                                                                                                                                                                                                                                                   |
| elements           | array of objects | yes                                                                            | [see element](#gid=144910249)                                                            |                                                                                                                                                                                                                                                                   |
| measurement        | number           | is required in some grades                                                     | maximum section thickness at the time of heat treatment or final product thickness in mm |                                                                                                                                                                                                                                                                   |
| analysis           | string           | is required in some grades                                                     | type of chemical analysis                                                                | ["Heat", "Product", "Weld joint", "Weld overlay"]                                                                                                                                                                                                                 |
| zone               | string           | is required if analysis type is "Product"                                      |                                                                                          | ["Weld metal", "HAZ", "Base metal"]                                                                                                                                                                                                                               |
| steelMakingProcess | string           | no                                                                             | Steel making process. For some grades it changes the acceptance criteria                 | ["BOF", "EAF"]                                                                                                                                                                                                                                                    |
| position           | string           | no                                                                             |                                                                                          | if analysis type is Product: ["1/4 Thickness", "1/2 Thickness", "3/4 Thickness", "2 mm from OD", "2 mm from ID"]<br>if analysis type is Weld joint: ["Weld metal", "fusion line"]<br>if analysis type is Weld overlay: ["Weld metal", "fusion line", "last pass"] |
| distance           | number           | is required if position is either fusion line or last pass                     | distance from fusion line of from last pass in mm                                        |                                                                                                                                                                                                                                                                   |
| acceptance         | string           | no                                                                             | itp or qcp name                                                                          | ["FP-ITP Rev. 0"]                                                                                                                                                                                                                                                 |
| specimenId         | string           | is required if analysis type is one of "Product", "Weld joint", "Weld overlay" | id of the first specimen                                                                 |                                                                                                                                                                                                                                                                   |
| secondSpecimenId   | string           | no                                                                             | id of the second specimen                                                                |                                                                                                                                                                                                                                                                   |
| notes              | string           | no                                                                             | some additional notes/remarks about the test lab wants to mention                        |                                                                                                                                                                                                                                                                   |
| result             | string           | yes                                                                            | test result                                                                              | ["Acceptable", "Not Acceptable"]                                                                                                                                                                                                                                  |

| Property name | Data type | Required                                          | Description                                                                                                                  | Allowed values                                                                                                                                                  |
|---------------|-----------|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| min           | number    | is required in some grades                        |                                                                                                                              |                                                                                                                                                                 |
| max           | number    | is required in some grades                        |                                                                                                                              |                                                                                                                                                                 |
| value         | number    | yes                                               |                                                                                                                              |                                                                                                                                                                 |
| bm            | string    | yes                                               | chemical element                                                                                                             | ["Al", "As", "B", "Bi", "C", "Ca", "Co", "Cr", "Cu", "Fe", "H", "Mn", "Mo", "N", "Nb", "Ni", "O", "P", "Pb", "S", "Sb", "Si", "Sn", "Ta", "Ti", "V", "W", "Zr"] |
| id            | number    | yes                                               | element id in array. can be 1, 2, 3 etc.                                                                                     |                                                                                                                                                                 |
| formula       | string    | is required if bm is a formula. example: "CE_Pcm" | example: "C+Si/30+((Mn+Cu+Cr)/20)+Ni/60+Mo/15+V/10+B\*5"                                                                     |                                                                                                                                                                 |
| maxError      | number    | no                                                | There are some specifications that allow "value" to be higher than "max", in this case the acceptance criteria is "maxError" |

## Dimensional Test

### Model
[filename](_media/dimensional.json ':include')

### Description
| Property name      | Data type       | Required | Description                                                       | Allowed values                   |
|--------------------|-----------------|----------|-------------------------------------------------------------------|----------------------------------|
| client             | string          | yes      | company name of the company which requested the test              |                                  |
| lab                | string          | yes      | company name of the laboratory which performs the test            |                                  |
| elements           | array of object | yes      | [see element](#gid=2020845142)                                    |                                  |
| acceptanceCriteria | object          | no       | [see acceptance criteria](#gid=1487815395)                        |                                  |
| acceptance         | string          | no       | itp or qcp name                                                   | ["FP-ITP Rev. 0"]                |
| units              | object          | yes      | [see units](#gid=1941870506)                                      |                                  |
| file               | string          | no       | path to the file that is served on steeltrace server              |                                  |
| notes              | string          | no       | some additional notes/remarks about the test lab wants to mention |                                  |
| result             | string          | yes      | test result                                                       | ["Acceptable", "Not Acceptable"] |

| Property name    | Data type | Required | Description                                          | Allowed values |
|------------------|-----------|----------|------------------------------------------------------|----------------|
| productId        | string    | yes      | id of the specimen                                   |                |
| file             | string    | no       | path to the file that is served on steeltrace server |                |
| externalDiameter | object    | no       | [see object](#gid=997337937)                         |                |
| internalDiameter | object    | no       | [see object](#gid=997337937)                         |                |
| thickness        | object    | no       | [see object](#gid=997337937)                         |                |
| outOfRoundness   | object    | no       | [see object](#gid=997337937)                         |                |
| straightness     | object    | no       | [see object](#gid=997337937)                         |                |
| eccentricity     | object    | no       | [see object](#gid=997337937)                         |                |
| squareness       | object    | no       | [see object](#gid=997337937)                         |                |
| weldFLash        | object    | no       | [see object](#gid=997337937)                         |                |
| weldFlashOutside | object    | no       | [see object](#gid=997337937)                         |                |
| length           | number    | no       |                                                      |                |
| weight           | number    | no       |                                                      |                |
| bevelAngle       | number    | no       |                                                      |                |
| bevelRootFace    | number    | no       |                                                      |                |
| depthOfGroove    | number    | no       |                                                      |                |
| radialOffset     | number    | no       |                                                      |                |
| linearWeight     | number    | no       |                                                      |                |
| peaking          | object    | no       | [see object](#gid=997337937)                         |

| Property name    | Data type | Required | Description                  | Allowed values |
|------------------|-----------|----------|------------------------------|----------------|
| externalDiameter | object    | no       | [see object](#gid=253326535) |                |
| internalDiameter | object    | no       | [see object](#gid=253326535) |                |
| thickness        | object    | no       | [see object](#gid=253326535) |                |
| outOfRoundness   | object    | no       | [see object](#gid=253326535) |                |
| straightness     | object    | no       | [see object](#gid=253326535) |                |
| eccentricity     | object    | no       | [see object](#gid=253326535) |                |
| squareness       | object    | no       | [see object](#gid=253326535) |                |
| weldFLash        | object    | no       | [see object](#gid=253326535) |                |
| weldFlashOutside | object    | no       | [see object](#gid=253326535) |                |
| length           | object    | no       | [see object](#gid=253326535) |                |
| weight           | object    | no       | [see object](#gid=253326535) |                |
| bevelAngle       | object    | no       | [see object](#gid=253326535) |                |
| bevelRootFace    | object    | no       | [see object](#gid=253326535) |                |
| depthOfGroove    | object    | no       | [see object](#gid=253326535) |                |
| radialOffset     | object    | no       | [see object](#gid=253326535) |                |
| linearWeight     | object    | no       | [see object](#gid=253326535) |                |
| peaking          | object    | no       | [see object](#gid=253326535) |

| Property name    | Data type | Required | Description           | Allowed values |
|------------------|-----------|----------|-----------------------|----------------|
| externalDiameter | string    | no       | units of the property |                |
| internalDiameter | string    | no       | units of the property |                |
| thickness        | string    | no       | units of the property |                |
| outOfRoundness   | string    | no       | units of the property |                |
| straightness     | string    | no       | units of the property |                |
| eccentricity     | string    | no       | units of the property |                |
| squareness       | string    | no       | units of the property |                |
| weldFLash        | string    | no       | units of the property |                |
| weldFlashOutside | string    | no       | units of the property |                |
| length           | string    | no       | units of the property |                |
| weight           | string    | no       | units of the property |                |
| bevelAngle       | string    | no       | units of the property |                |
| bevelRootFace    | string    | no       | units of the property |                |
| depthOfGroove    | string    | no       | units of the property |                |
| radialOffset     | string    | no       | units of the property |                |
| linearWeight     | string    | no       | units of the property |                |
| peaking          | string    | no       | units of the property |

| Property name | Data type | Required | Description | Allowed values |
|---------------|-----------|----------|-------------|----------------|
| body          | number    | no       |             |                |
| leftEnd       | number    | no       |             |                |
| rightEnd      | number    | no       |             |

| Property name  | Data type | Required | Description              | Allowed values |
|----------------|-----------|----------|--------------------------|----------------|
| nominal        | number    | no       | nominal acceptance value |                |
| toleranceMinus | number    | no       | tolerance minus value    |                |
| tolerancePlus  | number    | no       | tolerance plus value     |

## Electromagnetic Induction Test (EMI)

### Model
[filename](_media/emi.json ':include')

### Description
| Property name            | Data type       | Required | Description                                                       | Allowed values                                                                                                                         |
|--------------------------|-----------------|----------|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| client                   | string          | yes      | company name of the company which requested the test              |                                                                                                                                        |
| lab                      | string          | yes      | company name of the laboratory which performs the test            |                                                                                                                                        |
| testStandard             | string          | yes      |                                                                   | ["API 5L Table E.7 (46 edition)", "ASTM E570 (2020)", "ASTM E309 (2016)", "ISO 10893-3 (2011)", "ISO 10893-2 (2011)"] or custom string |
| acceptance               | string          | yes      |                                                                   | ["API 5L Table E.8 (46 edition)"] or custom string                                                                                     |
| surfaceCondition         | string          | no       |                                                                   |                                                                                                                                        |
| examinedSurface          | array of string | yes      |                                                                   | ["100% of surface","Bevel ends","External surface","Internal surface","Welds"]                                                         |
| elements                 | array           | yes      | [see elements](#gid=376421336)                                    |                                                                                                                                        |
| result                   | string          | yes      | test result                                                       | ["No recordable indications","Acceptable indications","Not acceptable"]                                                                |
| notes                    | string          | no       | some additional notes/remarks about the test lab wants to mention |                                                                                                                                        |
| overallQuantityInspected | number          | yes      | how many products the certificate has                             |                                                                                                                                        |
| quantityInspected        | number          | yes      | how many products will be tested in this specific test            |                                                                                                                                        |
| pieceIdentification      | string          | yes      |                                                                   | ["Single piece", "Heat and lot"]                                                                                                       |
| examinationConditions    | object          | no       | [see examinationConditions](#gid=1219856979)                      |                                                                                                                                        |
| file                     | string          | no       | is a path to the file that is served on steeltrace server         |

| Property name   | Data type | Required | Description            | Allowed values |
|-----------------|-----------|----------|------------------------|----------------|
| notchesLocation | string    | yes      |                        |                |
| width           | number    | yes      | in mm                  |                |
| length          | number    | yes      | in mm                  |                |
| depth           | number    | yes      |                        |                |
| depthUnit       | string    | yes      | unit of depth property | ["mm", "%"]    |

| Property name | Data type | Required | Description                                 | Allowed values |
|---------------|-----------|----------|---------------------------------------------|----------------|
| 0             | object    | no       | [see examination condition](#gid=958530933) |                |
| 1             | object    | no       | [see examination condition](#gid=958530933) |                |
| 2             | object    | no       | [see examination condition](#gid=958530933) |                |
| ...           | object    | no       | [see examination condition](#gid=958530933) |

| Property name | Data type | Required | Description                                               | Allowed values |
|---------------|-----------|----------|-----------------------------------------------------------|----------------|
| file          | string    | no       | is a path to the file that is served on steeltrace server |                |
| value         | string    | no       |                                                           |

## Hardness Test

### Model
[filename](_media/hardness.json ':include')

| Property name | Data type | Required | Description                                                                            | Allowed values |
| ------------- | --------- | -------- | -------------------------------------------------------------------------------------- | -------------- |
| differentMax  | number    | no       | maximum in the test zone                                                               |                |
| differentMin  | number    | no       | minimum in the test zone                                                               |                |
| metal         | string    | yes      | test zone name                                                                         |                |
| position      | string    | yes      | positions that are included in the test zone divided with comma. example: "1, 2, 3, 4" |

## Heat Treatment

### Model
[filename](_media/heat_treatment.json ':include')

### Description
| Property name               | Data type | Required                                                  | Description                                                       | Allowed values                                                                                                                                                           |
|-----------------------------|-----------|-----------------------------------------------------------|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| method                      | string    | yes                                                       |                                                                   | ["Single batch furnace", "Localized", "In-line"]                                                                                                                         |
| type                        | string    | yes                                                       |                                                                   | ["Annealing", "Normalization","Post weld heat treatment","Quenching","Solution annealing","Tempering","Quench and Temper","Carbide solution treatment","Aging","Curing"] |
| temp                        | number    | yes                                                       | temperature                                                       |                                                                                                                                                                          |
| tempUnits                   | string    | yes                                                       | temperature units                                                 | ["celsius", "fahrenheit"]                                                                                                                                                |
| unitOfHoldingTime           | string    | no                                                        | unit to measure the holding time                                  | ["time", "thickness"]                                                                                                                                                    |
| holdingTimeUnits            | string    | required if holdingTime is not empty                      |                                                                   | ["sec", "min", "hr"]                                                                                                                                                     |
| holdingTime                 | number    | no                                                        |                                                                   |                                                                                                                                                                          |
| holdingThickness            | number    | no                                                        | ?                                                                 |                                                                                                                                                                          |
| holdingThicknessUnits       | string    | required if holdingThickness is not empty                 |                                                                   | ["in", "mm"]                                                                                                                                                             |
| coolingMedium               | string    | yes                                                       |                                                                   | ["Water", "Still air", "Forced air", "Oil", "Furnace"]                                                                                                                   |
| secondTemp                  | number    | required if type is "Quench and Temper"                   | temper temperature                                                |                                                                                                                                                                          |
| secondTempUnits             | string    | required if type is "Quench and Temper"                   |                                                                   | ["celsius", "fahrenheit"]                                                                                                                                                |
| secondCoolingMedium         | string    | required if type is "Quench and Temper"                   |                                                                   | ["Water", "Still air", "Forced air", "Oil", "Furnace"]                                                                                                                   |
| secondUnitOfHoldingTime     | string    | no                                                        | unit to measure the holding time                                  | ["time", "thickness"]                                                                                                                                                    |
| secondHoldingTime           | number    | no                                                        |                                                                   |                                                                                                                                                                          |
| secondHoldingTimeUnits      | string    | required if secondHoldingTime is not empty                |                                                                   | ["sec", "min", "hr"]                                                                                                                                                     |
| secondHoldingThickness      | number    | no                                                        | ?                                                                 |                                                                                                                                                                          |
| secondHoldingThicknessUnits | string    | required if secondHoldingThickness is not empty           |                                                                   | ["in", "mm"]                                                                                                                                                             |
| tolerancePlus               | number    | no                                                        | tolerance on temperature                                          |                                                                                                                                                                          |
| toleranceMinus              | number    | no                                                        | tolerance on temperature                                          |                                                                                                                                                                          |
| toleranceUnits              | string    | required if tolerancePlus or toleranceMinus is not empty  | tolerance on temperature units                                    | ["°C", "°F"]                                                                                                                                                             |
| heatingRateMin              | number    | no                                                        |                                                                   |                                                                                                                                                                          |
| heatingRateMax              | number    | no                                                        |                                                                   |                                                                                                                                                                          |
| heatingRateUnits            | string    | required if heatingRateMin or heatingRateMax is not empty |                                                                   | ["°C/h", "°F/h"]                                                                                                                                                         |
| coolingRateMin              | number    | no                                                        |                                                                   | ["°C/h", "°F/h"]                                                                                                                                                         |
| coolingRateMax              | number    | no                                                        |                                                                   |                                                                                                                                                                          |
| coolingRateUnits            | string    | required if coolingRateMin or coolingRateMax is not empty |                                                                   |                                                                                                                                                                          |
| notes                       | string    | no                                                        | some additional notes/remarks about the test lab wants to mention |                                                                                                                                                                          |
| strainHardening             | boolean   | no                                                        |                                                                   | [true, false]                                                                                                                                                            |
| images                      | array     | [see images](#gid=19352338)                               |                                                                   |

| Property name | Data type | Required | Description                                               | Allowed values |
|---------------|-----------|----------|-----------------------------------------------------------|----------------|
| preview       | boolean   | yes      |                                                           |                |
| preview_path  | string    | yes      | is a path to the file that is served on steeltrace server |

## Hydrogen Induced Cracking Test (HIC)

### Model
[filename](_media/hic.json ':include')

### Description
| Property name        | Data type | Required | Description                                                       | Allowed values                                                                     |
|----------------------|-----------|----------|-------------------------------------------------------------------|------------------------------------------------------------------------------------|
| client               | string    | yes      | company name of the company which requested the test              |                                                                                    |
| lab                  | string    | yes      | company name of the laboratory which performs the test            |                                                                                    |
| testStandard         | string    | yes      |                                                                   | ["NACE TM0284 (2016)","API 5L Annex H, clause H 7.2.2 / H.7.3.1"] or custom string |
| acceptance           | string    | yes      |                                                                   | ["ISO 15156-2 (2015) - NACE MR0175 Table B.3", "FP-ITP Rev. 0"] or custom string   |
| sampleID             | string    | yes      | ?                                                                 |                                                                                    |
| solution             | string    | yes      |                                                                   |                                                                                    |
| duration             | number    | yes      | test duration in hrs                                              |                                                                                    |
| temperature          | number    | yes      | test temperature in celsius                                       |                                                                                    |
| temperatureTolerance | number    | yes      | test temperature tolerance in celsius                             |                                                                                    |
| pressure             | number    | yes      | test pressure in bar                                              |                                                                                    |
| gasMixture           | string    | no       |                                                                   |                                                                                    |
| solutionPH           | object    | yes      | [see solutionPH](#gid=1794995702)                                 |                                                                                    |
| h2sConcentration     | object    | yes      | [see h2sConsentration](#gid=1492654674)                           |                                                                                    |
| requirements         | object    | no       | [see requirements](#gid=1634544984)                               | global requirements                                                                |
| elements             | array     | yes      | [see elements](#gid=106534246)                                    |                                                                                    |
| notes                | string    | no       | some additional notes/remarks about the test lab wants to mention |                                                                                    |
| result               | string    | yes      | test result                                                       | ["Acceptable", "Not Acceptable"]                                                   |

| Property name | Data type | Required | Description |
|---------------|-----------|----------|-------------|
| before        | string    | yes      |             |
| after         | string    | yes      |             |
| final         | string    | yes      |

| Property name | Data type | Required | Description |
|---------------|-----------|----------|-------------|
| initial       | string    | yes      |             |
| final         | string    | yes      |

| Property name            | Data type | Required | Description | Allowed values |
|--------------------------|-----------|----------|-------------|----------------|
| crackLengthRatioMax      | number    | no       |             |                |
| crackThicknessRatioMax   | number    | no       |             |                |
| crackSensitivityRatioMax | number    | no       |             |

| Property name         | Data type | Required                                                 | Description                                              | Allowed values |
|-----------------------|-----------|----------------------------------------------------------|----------------------------------------------------------|----------------|
| position              | string    | no                                                       |                                                          |                |
| orientation           | string    | yes                                                      |                                                          |                |
| specimenId            | string    | yes                                                      |                                                          |                |
| specimenLength        | number    | yes                                                      | in mm                                                    |                |
| specimenWidth         | number    | yes                                                      | in mm                                                    |                |
| specimenThickness     | number    | yes                                                      | in mm                                                    |                |
| controlSample         | boolean   | no                                                       |                                                          |                |
| requirements          | object    | no                                                       | [see requirements](#gid=1634544984) (local requirements) |                |
| crackLengthRatio      | number    | required if requirements.crackLengthRatioMax is set      | in %                                                     |                |
| crackThicknessRatio   | number    | required if requirements.crackThicknessRatioMax is set   | in %                                                     |                |
| crackSensitivityRatio | number    | required if requirements.crackSensitivityRatioMax is set | in %                                                     |

## Impact Test

### Model
[filename](_media/impact.json ':include')

### Description
| Property name   | Data type        | Required                                | Description                                                       | Allowed values                                           |
|-----------------|------------------|-----------------------------------------|-------------------------------------------------------------------|----------------------------------------------------------|
| client          | string           | yes                                     | company name of the company which requested the test              |                                                          |
| lab             | string           | yes                                     | company name of the laboratory which performs the test            |                                                          |
| fdpt            | boolean          | no                                      |                                                                   |                                                          |
| notch           | string           | yes                                     |                                                                   | ["KV", "KU"]                                             |
| radius          | string           | yes                                     | striker radius                                                    | ["2 mm", "8 mm"]                                         |
| width           | number           | yes                                     | width in mm                                                       |                                                          |
| height          | number           | yes                                     | height in mm                                                      | [10, 7.5, 6.67, 5, 3.33, 2.5]                            |
| outsideDiameter | number           | is required in some grades              | outside diameter in mm                                            |                                                          |
| thickness       | number           | is required in some grades              | final product thickness in mm                                     |                                                          |
| elements        | array of objects | yes                                     | [see element](#gid=354994940)                                     |                                                          |
| norm            | string           | yes                                     |                                                                   |                                                          |
| grade           | string           | yes                                     |                                                                   |                                                          |
| temperature     | number           | is required if impactTestCurve is false |                                                                   |                                                          |
| testStandard    | string           | yes                                     |                                                                   | ["ASTM E23 (2018)", "ISO 148-1 (2016)"] or custom string |
| acceptance      | string           | no                                      | itp or qcp name                                                   | ["FP-ITP Rev. 0"]                                        |
| result          | string           | yes                                     | test result                                                       | ["Acceptable", "Not Acceptable"]                         |
| unit            | string           | yes                                     | temperature unit, "celsius" is a default value                    | ["celsius", "fahrenheit"]                                |
| notes           | string           | no                                      | some additional notes/remarks about the test lab wants to mention |                                                          |
| impactTestCurve | boolean          | no                                      | true means that impact test curve will be drawn                   |                                                          |
| requirements    | object           | no                                      | [see requirements](#gid=87059542)                                 |                                                          |
| file            | string           |                                         | is a path to the file that is served on steeltrace server         |

| Property name | Data type | Required | Description                 | Allowed values |
|---------------|-----------|----------|-----------------------------|----------------|
| longitudinal  | object    | no       | [see object](#gid=91554620) |                |
| transverse    | object    | no       | [see object](#gid=91554620) |                |
| tangential    | object    | no       | [see object](#gid=91554620) |                |
| radial        | object    | no       | [see object](#gid=91554620) |

| Property name           | Data type | Required | Description                                    | Allowed values                                         |
|-------------------------|-----------|----------|------------------------------------------------|--------------------------------------------------------|
| average                 | number    | yes      | absorbed energy average min                    |                                                        |
| averageLateralExpansion | number    | no       | lateral expansion average min                  |                                                        |
| averageShearArea        | number    | no       | shear area average min                         |                                                        |
| location                | string    | no       |                                                | ["Base", "HAZ", "Weld"]                                |
| orientation             | string    | no       |                                                | ["transverse", "longitudinal", "tangential", "radial"] |
| single                  | number    | yes      | absorbed energy min                            |                                                        |
| singleLateralExpansion  | number    | no       | lateral expansion min                          |                                                        |
| singleShearArea         | number    | no       | shear area min                                 |                                                        |
| temperature             | number    | yes      |                                                |                                                        |
| unit                    | string    | yes      | temperature unit, "celsius" is a default value | ["celsius", "fahrenheit"]                              |

| Property name     | Data type | Required                                          | Description        | Allowed values                                                                                                                                                                          |
|-------------------|-----------|---------------------------------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| laboratory        | string    | yes                                               | id of the specimen |                                                                                                                                                                                         |
| location          | string    | yes                                               |                    | ["Base", "HAZ", "Weld"]                                                                                                                                                                 |
| notchPosition     | string    | is required if location is either "Weld" of "HAZ" |                    | ["fusion line","0.5 mm from fusion line","1 mm from fusion line","2 mm from fusion line","3 mm from fusion line","4 mm from fusion line","5 mm from fusion line","0.5 mm from weld CL"] |
| position          | string    | no                                                |                    | ["1/4 t","1/2 t","3/4 t","2 mm from ID","2 mm from OD"]                                                                                                                                 |
| orientation       | string    | yes                                               |                    | ["transverse", "longitudinal", "tangential", "radial"]                                                                                                                                  |
| temperature       | number    | is required if impactTestCurve is true            |                    |                                                                                                                                                                                         |
| energyJoule1      | number    | yes                                               |                    |                                                                                                                                                                                         |
| lateralExpansion1 | number    | is required in some grades                        |                    |                                                                                                                                                                                         |
| shearArea1        | number    | is required in some grades                        |                    |                                                                                                                                                                                         |
| energyJoule2      | number    | yes                                               |                    |                                                                                                                                                                                         |
| lateralExpansion2 | number    | is required in some grades                        |                    |                                                                                                                                                                                         |
| shearArea2        | number    | is required in some grades                        |                    |                                                                                                                                                                                         |
| energyJoule3      | number    | yes                                               |                    |                                                                                                                                                                                         |
| lateralExpansion3 | number    | is required in some grades                        |                    |                                                                                                                                                                                         |
| shearArea3        | number    | is required in some grades                        |                    |

## Sulphide Stress Corrosion Cracking Test (SSCC)

### Model
[filename](_media/sscc.json ':include')

### Description
| Property name           | Data type | Required | Description                                                       | Allowed values                                                                                                             |
|-------------------------|-----------|----------|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| client                  | string    | yes      | company name of the company which requested the test              |                                                                                                                            |
| lab                     | string    | yes      | company name of the laboratory which performs the test            |                                                                                                                            |
| testStandard            | string    | yes      |                                                                   | ["NACE TM0177 (2016)"] or custom string                                                                                    |
| acceptance              | string    | yes      |                                                                   | ["API 5L Annex H, clause H.4.5", "ISO 15156-2 (2015) - NACE MR0175 Table B.1"] or custom string           |
| solution                | string    | yes      |                                                                   |                                                                                                                            |
| duration                | number    | yes      | in hrs                                                            |                                                                                                                            |
| temperature             | number    | yes      | in celsius                                                        |                                                                                                                            |
| temperatureTolerance    | number    | yes      | in celsius                                                        |                                                                                                                            |
| pressure                | number    | yes      | in bar                                                            |                                                                                                                            |
| gasMixture              | string    | no       |                                                                   |                                                                                                                            |
| solutionPH              | object    | yes      | [see solutionPH](#gid=1036266614)                                 |                                                                                                                            |
| h2sConcentration        | object    | yes      | [see h2sConsentration](#gid=247307627)                            |                                                                                                                            |
| stressMethod            | string    | yes      |                                                                   | ["Uniaxial Tensile testing","Bent Beam testing","C-Ring testing","Double Cantilever Beam (DCB) test","Four Point Bend test"] |
| yeildStrengthType       | string    | yes      |                                                                   | ["Actual","Specified"]                                                                                                     |
| yeildStrengthValue      | number    | yes      | in MPa                                                            |                                                                                                                            |
| yeildStrengthPercentage | number    | yes      | in %                                                              |                                                                                                                            |
| appliedLoad             | number    | no       | applied stress in MPa                                             |                                                                                                                            |
| elements                | array     | yes      | [see element](#gid=731961699)                                     |                                                                                                                            |
| notes                   | string    | no       | some additional notes/remarks about the test lab wants to mention |                                                                                                                            |
| result                  | string    | yes      | test result                                                       | ["Acceptable", "Not Acceptable"]                                                                                           |

| Property name | Data type | Required | Description | Allowed values |
|---------------|-----------|----------|-------------|----------------|
| before        | number    | yes      |             |                |
| after         | number    | yes      |             |                |
| final         | number    | yes      |             |

| Property name | Data type | Required | Description | Allowed values |
|---------------|-----------|----------|-------------|----------------|
| initial       | number    | yes      | in ppm      |                |
| final         | number    | yes      | in ppm      |

| Property name     | Data type       | Required | Description                                               | Allowed values                     |
|-------------------|-----------------|----------|-----------------------------------------------------------|------------------------------------|
| position          | string          | yes      |                                                           |                                    |
| orientation       | string          | yes      |                                                           |                                    |
| specimenId        | string          | yes      |                                                           |                                    |
| specimenLength    | number          | yes      | in mm                                                     |                                    |
| specimenWidth     | number          | yes      | in mm                                                     |                                    |
| specimenThickness | number          | yes      | in mm                                                     |                                    |
| magnification     | number          | no       |                                                           |                                    |
| evaluationOfCraks | string          | yes      |                                                           | ["Absent (PASS)","Present (FAIL)"] |
| files             | array of string | no       | is a path to the file that is served on steeltrace server |

## Tensile Test

### Model
[filename](_media/tensile.json ':include')

### Description
| Property name | Data type        | Required | Description                                                           | Allowed values                                                                                                                  |
|---------------|------------------|----------|-----------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| client        | string           | yes      | company name of the company which requested the test                  |                                                                                                                                 |
| lab           | string           | yes      | company name of the laboratory which performs the test                |                                                                                                                                 |
| norm          | string           | yes      |                                                                       |                                                                                                                                 |
| grade         | string           | yes      |                                                                       |                                                                                                                                 |
| fdpt          | boolean          | no       |                                                                       |                                                                                                                                 |
| specimen      | string           | yes      | specimen type                                                         | ["Round", "Rectangular", "Strip"]                                                                                               |
| testStandard  | string           | yes      |                                                                       | ["ASTM A370 (2020)","ASTM A370 (2021)","ASTM E8 (2021)","ASTM E21 (2020)","ISO 6892-1:2019","ISO 6892-2:2018"] or custom string |
| result        | string           | yes      | test result                                                           | ["Acceptable", "Not Acceptable"]                                                                                                |
| acceptance    | string           | no       | itp or qcp name                                                       | ["FP-ITP Rev. 0"]                                                                                                               |
| elements      | array of objects | yes      | [see elements](#gid=116844094)                                        |                                                                                                                                 |
| notes         | string           | no       | some additional notes/remarks about the test lab wants to mention     |                                                                                                                                 |
| files         | array of string  | no       | each string is a path to the file that is served on steeltrace server |

| Property name        | Data type | Required                                                        | Description                                                                        | Allowed values                                                                                            |
|----------------------|-----------|-----------------------------------------------------------------|------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| position             | string    | yes                                                             |                                                                                    | ["1/4 thickness","1/2 thickness","3/4 thickness","2 mm from inside","2 mm from outside","full thickness"] |
| specimenId           | string    | yes                                                             | id of the specimen                                                                 |                                                                                                           |
| fracturAppearance    | string    | is required if test zone is "Weld Metal"                        |                                                                                    | ["Ductile", "Fragile"]                                                                                    |
| dimensionX           | number    | yes                                                             | diameter or width in mm                                                            |                                                                                                           |
| dimensionY           | number    | is required if specimen type is either "Rectangular" or "Strip" | thickness in mm                                                                    |                                                                                                           |
| gaugeLength          | number    | is required in some grades                                      | gauge length in mm                                                                 |                                                                                                           |
| temperature          | number    | no                                                              |                                                                                    |                                                                                                           |
| breakPosition        | string    | no                                                              |                                                                                    | ["Out Weld","In Weld"]                                                                                    |
| zone                 | string    | yes                                                             |                                                                                    | ["Base Metal","Weld Metal","Heat affected zone"]                                                          |
| orientation          | string    | no                                                              |                                                                                    | ["Longitudinal","Transversal","Tangential","Radial"]                                                      |
| heatTreatedThickness | number    | no                                                              | maximum section thickness at the time of heat treatment or final product thickness |                                                                                                           |
| boltDiameter         | string    | is required in some grades                                      |                                                                                    |                                                                                                           |
| rp                   | number    | is required in some grades                                      | yield strength                                                                     |                                                                                                           |
| rm                   | number    | is required in some grades                                      | tensile strength                                                                   |                                                                                                           |
| a                    | number    | is required in some grades                                      | elongation                                                                         |                                                                                                           |
| reductionOfArea      | number    | is required in some grades                                      | reduction of area                                                                  |                                                                                                           |
| uniformElongation    | number    | is required in some grades                                      | uniform elongation                                                                 |                                                                                                           |
| requirements         | object    | no                                                              | [see requirements](#gid=1621204917)                                                |

| Property name        | Data type | Required                   | Description             | Allowed values |
|----------------------|-----------|----------------------------|-------------------------|----------------|
| yeldMin              | number    | is required in some grades | yield strength min      |                |
| yeldMax              | number    | is required in some grades | yield strength max      |                |
| tensMin              | number    | is required in some grades | tensile strength min    |                |
| tensMax              | number    | is required in some grades | tensile strength max    |                |
| elongation           | number    | is required in some grades | elongation min          |                |
| reductionOfArea      | number    | is required in some grades | reduction of area min   |                |
| yeildTensileRatio    | number    | is required in some grades | yeild tensile ratio max |                |
| uniformElongationMin | number    | is required in some grades | uniform elongation min  |

## Ultrasonic Test

### Model
[filename](_media/ultrasonic.json ':include')

### Description
| Property name            | Data type | Required | Description                                               | Allowed values                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------------------|-----------|----------|-----------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| client                   | string    | yes      | company name of the company which requested the test      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| lab                      | string    | yes      | company name of the laboratory which performs the test    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| testStandard             | string    | yes      |                                                           | [<br>"ASME V Article 4 (2021)",<br>"ASME V Article 5 (2021)",<br>"API 5L Table E.7 (46 edition)",<br>"ASTM A388 (2019)",<br>"ASTM A745 (2020)",<br>"ASTM B594 (2019e1)",<br>"ASTM E213 (2020)",<br>"ASTM A435 (2017)",<br>"ASTM A578 (2017)",<br>"EN 10160 (1999)",<br>"EN 10306 (2001)",<br>"EN 10308 (2001)",<br>"ISO 10893-8 (2011/Amd1:2020)",<br>"ISO 10893-9 (2011/Amd1:2020)",<br>"ISO 10893-10 (2011/Amd1:2020)",<br>"EN 10228-3 (2016)"<br>]                                                                                                                                                                                                                                                                           |
| acceptance               | string    | yes      |                                                           | [<br>"ASME VIII Division 2 Paragraph 3.3.4 (2021)",<br>"API 5L Table E.8 (46 edition)",<br>"EN 10228-3 Class 1 (2016)",<br>"EN 10228-3 Class 2 (2016)",<br>"EN 10228-3 Class 3 (2016)",<br>"EN 10228-3 Class 4 (2016)",<br>"ISO 10893-8 Level U0 (2011/Amd1:2020)",<br>"ISO 10893-8 Level U1 (2011/Amd1:2020)",<br>"ISO 10893-8 Level U2 (2011/Amd1:2020)",<br>"ISO 10893-8 Level U3 (2011/Amd1:2020)",<br>"ASTM A745 QL-1 (2020)",<br>"ASTM A745 QL-2 (2020)",<br>"ASTM A745 QL-3 (2020)",<br>"ASTM A745 QL-4 (2020)",<br>"ASTM A745 QL-5 (2020)",<br>"ASTM B594 Class AAA (2019e1)",<br>"ASTM B594 Class AA (2019e1)",<br>"ASTM B594 Class A (2019e1)",<br>"ASTM B594 Class B (2019e1)",<br>"ASTM B594 Class C (2019e1)"<br>] |
| surfacePreparation       | string    | no       | surface condition                                         | ["As rolled", "As forged", "As welded", "Sandblasted", "Machined"]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| surfaceRoughness         | number    | no       | in μm                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| result                   | string    | yes      |                                                           | ["No indication", "Acceptable indications", "Not acceptable indications"]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| examination              | object    | no       | [see examination conditions](#gid=1839661012)             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| elements                 | array     | yes      | [see elements](#gid=634221726)                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| overallQuantityInspected | number    | yes      | how many products the certificate has                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| quantityInspected        | number    | yes      | how many products will be tested in this specific test    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| pieceIdentification      | string    | yes      |                                                           | ["Single piece", "Heat and lot"]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| examinationConditions    | object    | no       | [see examinationConditions](#gid=400286962)               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| file                     | string    | no       | is a path to the file that is served on steeltrace server |

| Property name | Data type | Required | Description                   | Allowed values |
|---------------|-----------|----------|-------------------------------|----------------|
| speed         | number    | no       | scanning speed in mm/s        |                |
| gel           | string    | no       | couplant gel                  |                |
| overlap       | number    | no       | scanning overlap minimum in % |

| Property name | Data type | Required | Description                     | Allowed values |
|---------------|-----------|----------|---------------------------------|----------------|
| technique     | object    | no       | [see technique](#gid=863857098) |                |
| probes        | object    | no       | [see probes](#gid=459282034)    |

| Property name | Data type       | Required | Description    | Allowed values                                                                             |
|---------------|-----------------|----------|----------------|--------------------------------------------------------------------------------------------|
| technique     | string          | no       |                | ["Impulse echo - Reflection method", "Through transmission method", "Phased Array"]        |
| sensitivity   | string          | no       |                | ["Back wall echo", "DAC curve", "AVG diagram"]                                             |
| volume        | array of string | no       | scenned volume | ["100% of volume", "Welds", "Weld seam", "Bevel ends", "Weld overlay", "150 mm from ends"] |

| Property name | Data type | Required | Description     | Allowed values                  |
|---------------|-----------|----------|-----------------|---------------------------------|
| waves         | string    | no       |                 | ["Straight beam", "Angle beam"] |
| angle         | number    | no       | degree          |                                 |
| model         | string    | no       | brand and model |                                 |
| size          | number    | no       | in mm           |                                 |
| frequency     | number    | no       | in MHz          |                                 |
| calibration   | string    | no       |                 |

| Property name | Data type | Required | Description                                  | Allowed values |
|---------------|-----------|----------|----------------------------------------------|----------------|
| 0             | object    | no       | [see examination condition](#gid=1024497525) |                |
| 1             | object    | no       | [see examination condition](#gid=1024497525) |                |
| 2             | object    | no       | [see examination condition](#gid=1024497525) |                |
| ...           | object    | no       | [see examination condition](#gid=1024497525) |

| Property name | Data type | Required | Description                                               | Allowed values |
|---------------|-----------|----------|-----------------------------------------------------------|----------------|
| file          | string    | no       | is a path to the file that is served on steeltrace server |                |
| value         | string    | no       |                                                           |