# sap-rap-sales-order-mgmt
Full-stack SAP RAP implementation of a Sales Order BO using an Unmanaged Save scenario with Draft enablement, custom transactional buffering, and OData V4 service exposure on S/4HANA.


# SAP RAP: Sales Order Management (Unmanaged Scenario)

## 📋 Project Overview
This repository contains the source code for a modern Sales Order application built using the **ABAP RESTful Programming Model (RAP)**. The project focuses on the **Unmanaged Save** pattern, demonstrating how to bridge legacy ABAP logic with the modern, cloud-ready RAP orchestration.

### 🏗️ Architecture & Layers
The application is built following the "Clean Core" principles and is structured into four distinct layers:

1.  **Data Modeling:** CDS View Entities for Header and Item data with specialized UI annotations.
2.  **Behavior Definition (BDEF):** A strict contract defining Create, Update, and Delete operations with **Draft** support.
3.  **Behavior Pool (ABP):** The core logic engine featuring:
    * **Transactional Buffer:** A local singleton class (`lcl_buffer`) managing the state between the UI and Database.
    * **ID Mapping:** Precise handling of `%cid` and `%pid` for consistent record creation.
    * **Saver Class:** Manual persistence logic within the `SAVE_MODIFIED` method.
4.  **Service Exposure:** OData V4 Service Bindings optimized for **Fiori Elements**.

## 🛠️ Key Technical Features
* **Unmanaged Save:** Complete manual control over the SAP LUW (Logical Unit of Work).
* **Draft Capabilities:** Stateless web interaction support using `with draft`.
* **Determinations:** Automated header-total recalculations triggered by item modifications.
* **EML (Entity Manipulation Language):** Used for internal data access and cross-entity communication.
* **ABAP Cloud Syntax:** Coded in `Strict(2)` mode for upgrade stability.

## 📂 Repository Structure
* `/src/ddls/` - Core Data Services (Data Definitions)
* `/src/bdef/` - Behavior Definitions
* `/src/classes/` - Behavior Pool Implementation (Handler & Saver)
* `/src/srvd/` - Service Definitions & Bindings

## 💡 Why this approach?
I chose the **Unmanaged Scenario** specifically to showcase the ability to handle complex persistence requirements. By manually implementing the buffer and saver, this project simulates a real-world integration where a developer must wrap legacy Function Modules or BAPIs into a modern RAP Business Object.

