# Prerequisite

**VS Code Setup**

[Visual Studio Code | SAP Help Portal](https://help.sap.com/docs/SAP_FIORI_tools/17d50220bcd848aa854c9c182d65b699/17efa217f7f34a9eba53d7b209ca4280.html)

# Download Metadata File

Open Service Binding.

![image](https://github.com/zzvikesh/index/assets/167571098/14cd10b1-2c5a-451c-898c-8c5b9d39e867)

At the end of the service `.../zd_ui_customeraims_o4/srvd/sap/zd_sd_customeraims/0001/` add `$metadata`.

![image](https://github.com/zzvikesh/index/assets/167571098/c257a3ed-8c1e-4560-85e8-96fabc6bf723)

Save as `zd_sd_customeraims_0001.xml`

# Generate Fiori Application

Open workspace folder in VSCode.

![image](https://github.com/zzvikesh/index/assets/167571098/057067af-09e4-45ec-b434-eafd9e95e126)

## Open Template Wizard

`Ctrl + Shift + P` -> Open Applicaiton Generator.

![image](https://github.com/zzvikesh/index/assets/167571098/1f7d1da9-b29d-4ed2-b4f8-d9db50c2c996)

## Select Data Source

| Data Source        | Upload a Metadata Document |
| ------------------ | -------------------------- |
| Metadata file path | <Pick the path>            |

![image](https://github.com/zzvikesh/index/assets/167571098/be72b181-fa27-457b-ae38-010fa3d7ea7a)

## Select Root and Child entity.

![image](https://github.com/zzvikesh/index/assets/167571098/0cb709eb-7ae6-492d-a3d5-055103de5c73)

## Application Attributes

> 📢 Application Name  = `<Namespace>.<ModuleName>00` should **not** be greater than **15** characters. Same name will be used while deploying the application in SAP by replacing '**.**' with '**_**'. 

Intended BSP name, zm_cust_aims00

- Next, version will be zm_cust_aims**01**, zm_cust_aims**02** and so on.

SAP UI5 Version can be found using Support Assistant on Preview Application.

<table>
<tr>
</tr>
<tr>
<td>

  ![image](https://github.com/zzvikesh/index/assets/167571098/77b4cda4-fc17-4c99-909f-60fc2898983b)

</td>
<td>

  ![image](https://github.com/zzvikesh/index/assets/167571098/4e559fe3-4119-46ac-baa9-44ff171f56f3)

</td>
</tr>
</table>

![image](https://github.com/zzvikesh/index/assets/167571098/8923516d-5d88-4d4e-9e16-907847f745c5)

# Work on Generated Application

File -> Open Folder -> `cust.aims` (New Created).

![image](https://github.com/zzvikesh/index/assets/167571098/eb325f20-5566-4111-9e7f-59706dde2c16)

## manifest

![image](https://github.com/zzvikesh/index/assets/167571098/1754d4cb-0f73-49c0-a905-a8944f839352)

`"enhanceI18n": "i18n/`Entity`OPi18n.properties"`

![image](https://github.com/zzvikesh/index/assets/167571098/e81301bb-4166-45a7-959f-b3e01fc3124a)

## EntityOPi18n.properties

[Localization of UI Texts | SAP Help Portal](https://help.sap.com/docs/ABAP_PLATFORM_NEW/468a97775123488ab3345a0c48cadd8f/b8cb649973534f08a6047692f8c6830d.html)


## Page Map

![image](https://github.com/zzvikesh/index/assets/167571098/fce32e65-49f6-4a24-9314-4cf372a0dcd1)

Enabling flexible column layout.

> Similarly, excel download functionality can be removed, multiple selection option can be added etc.

![image](https://github.com/zzvikesh/index/assets/167571098/5ef9e1b7-efa9-4527-8ac3-ff3cbf8fc5dd)

## Generate the BSP Application

![image](https://github.com/zzvikesh/index/assets/167571098/92031fa7-f8c6-4e00-b620-133e2676cc41)

Open the **Integrated Terminal**.

[UI5 CLI](https://sap.github.io/ui5-tooling/v2/pages/CLI/#ui5-build)

`npx ui5 build -a`

**dist** folder is created.

![image](https://github.com/zzvikesh/index/assets/167571098/903e64e3-08f2-4822-b481-f9d518b02873)

# Upload BSP Application to the System

![image](https://github.com/zzvikesh/index/assets/167571098/29ec6b33-639e-483e-89ae-0cca4e03e128)

![image](https://github.com/zzvikesh/index/assets/167571098/6674b4bf-38e6-47ad-a056-55abbe978e3e)

![image](https://github.com/zzvikesh/index/assets/167571098/cb1e3410-e323-4704-b63e-e97dbcbdf130)

![image](https://github.com/zzvikesh/index/assets/167571098/d6a7a8a6-4795-4fcc-99b2-a852b0ffce40)

# FLP Configuration

![image](https://github.com/zzvikesh/index/assets/167571098/d284a1a3-5daf-4423-86d6-6c04590ebd2d)

![image](https://github.com/zzvikesh/index/assets/167571098/75cf86bf-8033-456a-9066-2726db963c20)

> Parameters can also be maintained for auto populating fields during cross app navigation.

