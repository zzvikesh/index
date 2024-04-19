# Goal

|||
|---|---|
| App Component | zm.cust.aims00 |
| BSP           | zm_cust_aims00 |

# Download Metadata File

Open Service Binding.

At the end of the service `.../zd_ui_customeraims_o4/srvd/sap/zd_sd_customeraims/0001/` add `$metadata`.


Save as `zd_sd_customeraims_0001.xml`

# Generate Fiori Application

Open workspace folder in VSCode.


## Open Template Wizard

`Ctrl + Shift + P` -> Open Applicaiton Generator.


## Select Data Source

| Data Source        | Upload a Metadata Document |
| ------------------ | -------------------------- |
| Metadata file path | <Pick the path>            |

## Select Root and Child entity.


## Application Attributes

> 📢 Application Name  = `<Namespace>.<ModuleName>00` should **not** be greater than **15** characters. Same name will be used while deploying the application in SAP by replacing '**.**' with '**_**'. 

Intended BSP name, zm_cust_aims00

- Next, version will be zm_cust_aims**01**, zm_cust_aims**02** and so on.

SAP UI5 Version can be found using Support Assistant on Preview Application.

---


---


---


# Work on Generated Application

File -> Open Folder -> `cust.aims` (New Created).



## manifest


`"enhanceI18n": "i18n/`Entity`OPi18n.properties"`


## EntityOPi18n.properties

[Localization of UI Texts | SAP Help Portal](https://help.sap.com/docs/ABAP_PLATFORM_NEW/468a97775123488ab3345a0c48cadd8f/b8cb649973534f08a6047692f8c6830d.html)


## Page Map


Enabling flexible column layout.


## Generate the BSP Application

Open the **Integrated Terminal**.


[UI5 CLI](https://sap.github.io/ui5-tooling/v2/pages/CLI/#ui5-build)

`npx ui5 build -a`

**dist** folder is created.


# Upload BSP Application to the System



---


---


---

# FLP Configuration


