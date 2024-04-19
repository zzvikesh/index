# Core Data Services (CDS)
[Core Data Services (CDS)](https://app.capacities.io/8831d237-9973-4445-9f19-6c81fa7bd424/e3cd5ddc-1dbe-493c-9b1b-b85e177a013e)

# Virtual Data Models (VDMs)

**<<Definition Here>>**

Cloud: [Virtual Data Model and CDS Views in SAP S/4HANA Cloud | SAP Help Portal](https://help.sap.com/docs/SAP_S4HANA_CLOUD/c0c54048d35849128be8e872df5bea6d/8573b810511948c8a99c0672abc159aa.html?locale=en-US)

OP: [CDS Views | SAP Help Portal](https://help.sap.com/docs/SAP_S4HANA_ON-PREMISE/ee6ff9b281d8448f96b4fe6c89f2bdc8/5418de55938d1d22e10000000a44147b.html)

[Naming Conventions in the Virtual Data Model | SAP Help Portal](https://help.sap.com/docs/SAP_S4HANA_ON-PREMISE/6b356c79dea443c4bbeeaf0865e04207/8a8cee943ef944fe8936f4cc60ba9bc1.html?version=1809.000&locale=en-US)

[The Virtual Data Model in SAP S/4HANA | SAP Help Portal](https://help.sap.com/docs/SAP_S4HANA_ON-PREMISE/6b356c79dea443c4bbeeaf0865e04207/8573b810511948c8a99c0672abc159aa.html?version=1809.000&locale=en-US)

# VDM Layers

---


---

[VDM Layers Whiteboard](https://link.excalidraw.com/l/5eMbpiBu0l3/5sRgLPpDEZj)


---

## Basic View

### **Restrictive View** 

> ❗️ Not for exposure, should only consumed **within** the System.

> ❗️ Always, create one Basic View while creating a Database Table.



- Purpose of Basic View is **Reusability** and **Easy Consumption**. 

- Reusability:

    - `@EndUserText.label` to reuse the Field Description for UI.

    - Since, database cannot tables have **C1** stability contract. Basic View with released C1 contract can be consumed , Key User Extensions.

- For easy consumption:

    - Rename technical fieldnames to Business Semantic **descriptive** name with **Camel Casing**.

    - Associate to Foreign Key using Foreign Key Association, `@ObjectModel.foreignKey.association:'_Customer'`

    - `@Semantics` annotations to highlight the intended purpose of the field during consumption.

    - **Only**, if current View is on the top of Value/Check Table.

    - Example: 

        - `I_ProfitCenter`

        - `I_Customer`

        - `I_SalesOrganization`

        - `I_Plant`

    ---

    **View on Value Table** 

    `@ObjectModel.representativeKey: 'ProfitCenter'`

    `@ObjectModel.text.association: '_Text'`


    ---

    **View on Text Table**

    `@ObjectModel.dataCategory: #TEXT`

    `@ObjectModel.representativeKey: 'ProfitCenter'`

    Association [0..1] to I_Language

    `@Semantics.language: true`

    `@Semantics.text: true`


    ---

### **Interface View**

Special purpose Basic View, which we create to expose the data directly from the database to the UI. 

Example

- `I_AccountingDocumentCategory`

- `I_GoodsMovementRefDocType`

- `I_GoodsMovementStatus`

- `I_OverallBillingStatus`

## Composite View

Composite interface views combine multiple basic interface views or other composite interface views to form new semantic entities.






















































































📢 **Why Basic View is Important?**

- Single Basic View with proper annotations can easily be consumed by both **Analytical Cube** and **RAP BO**.

- Extension contracts can be maintained for easy consumption in Key User ABAP.

- Descriptive field names for easier readability. 



### **Basic Interface View - Semantic** **Annotations**

**Currency**

```text
@Semantics.amount.currencyCode:'currency_code' 
price : abap.curr;
@Semantics.currencyCode: true                    //Not allowed in View Entity
currency_code : abap.cuky;
```

**Quantity**

```text
@Semantics.quantity.unitOfMeasure:'' 
distance : abap.int4;
@Semantics.unitOfMeasure: true                   //Not allowed in View Entity
distance_unit : msehi;
```

**Date**

```text
@Semantics.businessDate:{
 at   : true
 from : true
 to   : true
}
```

**Calendar**

```text
@Semantics.calendar:{
 dayOfMonth      : true;
 dayOfYear       : true;
 week            : true;
 month           : true;
 quarter         : true;
 halfyear        : true;
 year            : true;
 yearWeek        : true;
 yearMonth       : true;
 yearQuarter     : true;
 yearHalfyear    : true;
}
```

**Business Card**

```text
@Semantics.name:{            
 fullName        : true;  
 givenName       : true;  
 additionalName  : true;  
 familyName      : true;  
 nickName        : true;  
 suffix          : true;  
 prefix          : true;  
 jobTitle        : true;  
}                            
@Semantics.telephone:type: [#HOME|#CELL|#WORK|#FAX|#REF|#TEXT|#VOICE|#VIDEO|#PAGER|#TEXT_PHONE]
@Semantics.address:{
 type: [ #HOME|#WORK|#PREF|#OTHER]
 city            : true
 street          : true
 streetNoNumber  : true
 number          : true
 country         : true
 region          : true
 subRegion       : true
 zipCode         : true
 postBox         : true
 label           : true
}
```

**Complete List**

| S/4HANA, On Premise (2022, FPS02) | [Semantics Annotations | SAP Help Portal](https://help.sap.com/docs/ABAP_PLATFORM_NEW/fc4c71aa50014fd1b43721701471913d/3ccd5cf7b98248618b1013a4a296e415.html?locale=en-US&version=202210.002) |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BTP, ABAP Environment
            | [Semantics Annotations | SAP Help Portal](https://help.sap.com/docs/abap-cloud/abap-rap/semantics-annotations?version=sap_btp)                                                                |

### **Basic Interface View - Header** **Annotations**

❗️ Missing 

- @ObjectModel.representativeKey:

- @ObjectModel.text.association: '_Text'

    - @Semantics.language: true

    - @Semantics.text: true

- Privileged Associations.

```text
-- DCL
@AccessControl:{
  authorizationCheck: #NOT_REQUIRED,
  privilegedAssociations: [ '_AssociationName', '_AddressDefaultRepresentation' ]
}
-- Metadata
@Metadata.ignorePropagatedAnnotations: true
-- Data Model
@VDM.viewType: #BASIC
-- Performance
@ObjectModel.usageType:{
    serviceQuality: #A,
    dataClass: #CUSTOMIZING | #ORGANIZATIONAL | #MASTER | #TRANSACTIONAL,
    sizeCategory: #S (#CUSTOMIZING) | #M (#ORGANIZATIONAL) | #L (#MASTER) | #XL  (#TRANSACTIONAL)
}
-- Analytical
@Analytics.dataCategory: #DIMENSION | #FACT (#TRANSACTIONAL with Measures)
OR 
@ObjectModel.dataCategory: #TEXT
-- Value / Check Table View
@ObjectModel.representativeKey: '<<ValueField>>'
@ObjectModel.dataCategory: #VALUE_HELP
@ObjectModel.resultSet.sizeCategory: #XS (#VALUE_HELP) -- For Drop Down
...
{
   @EndUserText.label: 'UN/NA Code'
   @ObjectModel.text.association: '_Text' /  @Semantics.language: true & @Semantics.text: true
   <<ValueField>>,  
   ...
}
```



## Composite Interface View

> 📢 **Public Interface View** - Can be consumed within the system and can also be exposed outside the system.

- These are **optional** helper views on the top of Base View to perform intermediate tasks like:

    - Aggregation View

    - Value Help View

    - Text View

    - Cube View and Facts View for Analytical Apps.

### **Composite View - Header** **Annotations**

```text
-- DCL
@AccessControl.authorizationCheck: #NOT_REQUIRED
-- Metadata
@Metadata.ignorePropagatedAnnotations: true
-- Data Model
@VDM.viewType: #COMPOSITE
-- Performance
@ObjectModel.usageType:{
serviceQuality: #B,
dataClass: #CUSTOMIZING | #ORGANIZATIONAL | #MASTER | #TRANSACTIONAL,
sizeCategory: #S (#CUSTOMIZING) | #M (#ORGANIZATIONAL) | #L (#MASTER) | #XL  (#TRANSACTIONAL)
}
--- Analytical !! Only for EA!!
@Analytics.dataCategory: #CUBE | #FACT (Transaction Item Table as a Source for Cube)
```

### Composite Interface View - Domain Value Help

---

**Domain Values**

```text
@EndUserText.label: '<Value Help Description>' //Input: <Value Help Description>
-- DCL
@AccessControl.authorizationCheck: #NOT_REQUIRED
-- Data Model
@VDM.viewType: #BASIC
@ObjectModel.dataCategory: #VALUE_HELP
-- Performance
@ObjectModel.usageType:{
    serviceQuality: #A,
    dataClass: #CUSTOMIZING,
    sizeCategory: #S
}
-- Drop Down
@ObjectModel.resultSet.sizeCategory: #XS
--- Analytical
@Analytics : {
    dataCategory: #DIMENSION, 
    dataExtraction.enabled : true | false ?Reference?
}
-- Foreign Key Associations
@ObjectModel.representativeKey: 'Code'
define view entity <Z1I_ViewNameVH> //Input: <Z1I_ViewNameVH>
  as select from dd07l
  association [0..*] to <Z1I_ViewNameVHText> as _Text on $projection.Code = _Text.Code //Input: <Z1I_ViewNameVHText>
{
      @ObjectModel.text.association: '_Text'
key cast( domvalue_l as <DataElementName> ) as Code, //Input: <DataElementName>
      _Text
}
where
      dd07l.domname  = '<DomaintName>' //Input: <DomainName> 
  and dd07l.as4local = 'A'
```


---

**Domain Value's Text** 

```text
@EndUserText.label: '<Value Help Description> Text' //Input: <Value Help Description>
-- DCL
@AccessControl.authorizationCheck: #NOT_REQUIRED
-- Data Model
@VDM.viewType: #BASIC
@ObjectModel.dataCategory: #TEXT
-- Performance
@ObjectModel.usageType:{
    serviceQuality: #A,
    dataClass: #CUSTOMIZING,
    sizeCategory: #S
}
-- Foreign Key Associations
@ObjectModel.representativeKey: 'Code'
define view entity <ZI1_ViewNameVHText> //Input: <ZI1_ViewNameVHText> 
  as select from dd07t 
  association [0..*] to <ZI1_ViewNameVH> as _Code     on $projection.Code = _Code.Code //Input: <ZI1_ViewNameVH>
  association [0..1] to I_Language       as _Language on $projection.Language = _Language.Language
{
  key cast( domvalue_l as <DataElementName> ) as Code, //Input: <DataElementName>
      @Semantics.language: true
      @ObjectModel.foreignKey.association: '_Language'
  key ddlanguage                              as Language,
      @Semantics.text: true
      ddtext                                  as Description,
      _Code,
      _Language
}
where
      domname  = '<DomaintName>' //Input: <DomainName>
  and as4local = 'A'
```


---

## Transactional BO View

> 📢 **Restrictive Interface View** - Can be consumed within the system. But, should never be exposed outside the system.

- Creates the Business Object for the Transactional Processing. BO is created  

- BO is created as below:  

    - Consuming the Basic View (**preferred**) or Database Table; 

    - Create **composition** to Parent and Child Entities.

    - Create **association** Composite Interface Views for any additional data. Ex: 

        - Getting the Description or value not belonging to the BO. 

        - Getting the values calculated by aggregation or union operations etc.

    - **SAP Only**: Create **association** to Extension View (E_*).

## Base BO View

> 📢 Should never be exposed and data should be protected using **Dummy DCL**.

# VDM Annotations

**Virtual Data Models (VDM)** based on CDS views are used for creating data models in ABAP while working on S4 HANA OP, S4 HANA Cloud and BTP, ABAP Env. This cheat sheet is a quick reference guide to help with creating ABAP based data models.

[abap-data-modelling-vdm/01. Data Modelling Overview.md at main · zvikesh/abap-data-modelling-vdm · GitHub](https://github.com/zvikesh/abap-data-modelling-vdm/blob/main/01.%20Data%20Modelling%20Overview.md)

[rap-annotations-cheat-sheet/01. Basic View.md at main · zvikesh/rap-annotations-cheat-sheet · GitHub](https://github.com/zvikesh/rap-annotations-cheat-sheet/blob/main/01.%20Basic%20View.md)

# VDM Annotations Cheat Sheet

## For Transactional Applications

[abap-data-modelling-vdm/02. Data Modelling Cheatsheet.md at main · zvikesh/abap-data-modelling-vdm · GitHub](https://github.com/zvikesh/abap-data-modelling-vdm/blob/main/02.%20Data%20Modelling%20Cheatsheet.md)

### Basic View (Generic)

```text
-- DCL
@AccessControl.authorizationCheck: #CHECK
-- Metadata
@Metadata:{
 allowExtensions: true,
 ignorePropagatedAnnotations: true
}
-- Data Model
@VDM.viewType: #BASIC
-- Performance
@ObjectModel.usageType:{
    serviceQuality: #A,
    dataClass: #CUSTOMIZING | #ORGANIZATIONAL | #MASTER | #TRANSACTIONAL,
    sizeCategory: #S (#CUSTOMIZING) | #M (#ORGANIZATIONAL) | #L (#MASTER) | #XL  (#TRANSACTIONAL)
}
--- Analytical
@Analytics : {
    dataCategory: #DIMENSION, 
    dataExtraction.enabled : true | false ?Reference?
}
```

**Annotations**

**Value Table Associations**

[https://github.com/zvikesh/rap-annotations-cheat-sheet/blob/main/01.%20Basic%20View.md#value-table-associations](https://github.com/zvikesh/rap-annotations-cheat-sheet/blob/main/01.%20Basic%20View.md#value-table-associations)

Foreign Key Association annotation helps to derivce Value Help for Consumption View. The cardinality of a foreign key association must be either [0..1] or [1..1] / [1]. Example: All the configurational and customizing data.

```text
I_ProfitCenter
I_Currency
I_Country
```

All semantic annotation.

I_User for Admin Data fields with [0..1] cardinality.

CDS views of configurational entities with [0..1] cardinality. Ex: I_Currency, I_UnitOfMeasure etc.

[abap-data-modelling-vdm/02. Data Modelling Cheatsheet.md at main · zvikesh/abap-data-modelling-vdm · GitHub](https://github.com/zvikesh/abap-data-modelling-vdm/blob/main/02.%20Data%20Modelling%20Cheatsheet.md)

### Helper Composite View / Transactional View

```text
-- DCL
@AccessControl.authorizationCheck: #CHECK
-- Metadata
@Metadata:{
allowExtensions: true,
ignorePropagatedAnnotations: true
}
-- Data Model
@VDM.viewType: #COMPOSITE
-- Performance
@ObjectModel.usageType:{
serviceQuality: #B,
dataClass: #CUSTOMIZING | #ORGANIZATIONAL | #MASTER | #TRANSACTIONAL,
sizeCategory: #S (#CUSTOMIZING) | #M (#ORGANIZATIONAL) | #L (#MASTER) | #XL  (#TRANSACTIONAL)
}
--- Analytical
@Analytics : {
dataCategory: #DIMENSION,
dataExtraction.enabled : true | false ?Reference?
} 
```




# Value Help

On the Top of Value Table

```java
      @Search:{ defaultSearchElement: true, fuzzinessThreshold: 0.7 }
      @UI.lineItem: [{ position: 10 }]
  key SalesOrganization,

      @Search:{ defaultSearchElement: true, fuzzinessThreshold: 0.7 }
      @UI.lineItem: [{ position: 20 }]
      _SalesOrganization._Text[ 1:Language = $session.system_language  ].SalesOrganizationName,  //In Interface Views

      @UI.lineItem: [{ position: 30 }]
      _SalesOrganization.CompanyCode
```

Value Help for Domain

---

```java
@AccessControl.authorizationCheck: #NOT_REQUIRED
@EndUserText.label: '<End User Label>'
@AbapCatalog.sqlViewName: '<SQL View Name>'
@Search.searchable
@ObjectModel.compositionRoot: true
@ObjectModel.usageType.serviceQuality: #A
@ObjectModel.usageType.sizeCategory: #S
@ObjectModel.usageType.dataClass: #CUSTOMIZING
@Analytics.dataCategory: #DIMENSION
@ObjectModel.representativeKey: 'Code'

define view <CDS Code View Name>
  as select from ZTMM_HAZCHEM
  association [0..*] to <CDS Text View Name> as _Text
    on $projection.Code = _Text.Code
{
  @ObjectModel.text.association: '_Text'
  @Search.DefaultSearchElement: true
  key cast( <Name of Code Field in Data Source> as ZSHPNAME1 ) as Code,
  @ObjectModel.association.type: [#TO_COMPOSITION_CHILD]
  _Text
}
```



---

```java
@AccessControl.authorizationCheck: #NOT_REQUIRED
@EndUserText.label: '<End User Label>'
@AbapCatalog.sqlViewName: '<SQL View Name>'
@Search.searchable
@ObjectModel.usageType.serviceQuality: #A
@ObjectModel.usageType.sizeCategory: #S
@ObjectModel.usageType.dataClass: #CUSTOMIZING
@ObjectModel.dataCategory: #TEXT
@ObjectModel.representativeKey: 'Code'

define view <CDS Text View Name>
  as select from <Data Source (View or Table)>
  association [0..*] to <CDS Code View Name> as _Code
    on $projection.Code = _Code.Code
  association [0..1] to I_Language as _Language
    on $projection.Language = _Language.Language
{
  @Search.DefaultSearchElement: true
  key cast( <Name of Code Field in Data Source> as ZSHPNAME1 ) as Code,
  @Semantics.language: true
  @ObjectModel.foreignKey.association: '_Language'
  //Use this for language-dependent descriptions:
  key <Name of Language Field in Data Source> as Language,
  //Use this for language-independent descriptions:
  //key $session.system_language as Language,
  @Search.DefaultSearchElement: true
  @Semantics.text: true
  <Name of Description Field in Data Source> as Description,
  @ObjectModel.association.type: [#TO_COMPOSITION_ROOT, #TO_COMPOSITION_PARENT]
  _Code,
  _Language
}
```


---

# Naming Conventions

[Naming Conventions](https://app.capacities.io/8831d237-9973-4445-9f19-6c81fa7bd424/7c6bff9b-71bd-4338-b7a2-6c4522ebafe5)


# Reference

[Virtual Data Model and CDS Views in SAP S/4HANA Cloud](https://help.sap.com/docs/SAP_S4HANA_CLOUD/c0c54048d35849128be8e872df5bea6d/8573b810511948c8a99c0672abc159aa.html)

[Virtual Data Model and CDS Views in SAP S/4HANA, On Premise](https://help.sap.com/docs/SAP_S4HANA_ON-PREMISE/ee6ff9b281d8448f96b4fe6c89f2bdc8/8573b810511948c8a99c0672abc159aa.html)


