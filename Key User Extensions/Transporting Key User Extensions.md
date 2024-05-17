# Pre-requisites

Key User has been enabled using:
- ATP Setup on On Premise and Private Cloud.
- Extensibility Settings App on Public Cloud.

# Official Document

[Assign Extensions to a Software Package and Transport Request.pdf](https://github.com/zzvikesh/index/files/15349172/Assign.Extensions.to.a.Software.Package.and.Transport.Request.pdf)

# Transporting Key User Extension in On Premise and Private Cloud

**Configure Software Packages**

![image](https://github.com/zzvikesh/index/assets/167571098/405515b3-4fa9-4b9e-8ef6-5fcd977952bb)

![image](https://github.com/zzvikesh/index/assets/167571098/78d36024-93c8-4e3e-8b84-4cd3698a9742)

Assign a specific transport request to the registered package and activate *Automatic Task Handling*.

> 💡 Activate *Automatic Request Handling*. This option also activates *Automatic Task Handling*.

**Register Extension for Transports**

Move object from local TEST* Package to Development Package.

![image](https://github.com/zzvikesh/index/assets/167571098/dd934bde-afcd-4f93-8595-2de770873d5d)

**Transport the TRs**

Transport the TRs using TR management tool of choice.

# Process Flow of Capturing Extension Item in a TR

The process works as follows:

- *Only for Change*: If a transport request is assigned to the item in **Register Extensions for Transport** app, that request will be used.

- If no transport is assigned the transport handling settings of the software package will be evaluated.

    - The registered transport request from **Configure Software Package** will be used. 

    - If no open request is registered and **Automatic Transport Handling** is switched on a newone will be created.

- **Automatic Task Handling** will create a task on the found request if needed.

> ❗️ If all this fails, the changes to the extensibility item will be rejected.

# FAQ

- How to change the Transport Request of the Extension Item?

    1. Reassign to the default local package.

    2. Change the TR in **Configure Software Packages**.

    3. Reassign to the development Package again.

- In **Register Extensions for Transport** app for newly created field on selecting **Assign to a Transport Request**, gives the error; '*Transport request <> cannot be assigned to item <> of type <>. Full retransport is only possible for transportable item.*'

    **Assign to a Transport Request**, is meant for when change recording is required during the next change to the item. 

# ATC Checks not to be used for Key User Extensibility Objects

**ABAP_CLOUD_READINESS**

The checks Allowed Object Types in Cloud Development and Usage of Released APIs must not be used on key user objects. Key user apps create objects and use APIs which are not allowed in ABAP language version ABAP for Cloud Development.

**Other ATC Checks**

- **Extended Naming** Conventions for Programs: This ATC must not be used on key user objects. The objects created by key user apps follow a different naming convention.

- Some checks may provide **warnings** that shall be ignored. As an example, the key user apps do not set all annotations in CDS views that are checked by the CDS ATC checks (check CDS views: Check of `@ObjectModel.usageType` Annotations).
