---
title: "Creating a data contract for agents"
---

A Data Contract defines the operational data architecture for your AI agents within Unframe AI OS. It acts as a standardized, type-safe schema layer, structured similarly to a database table, that governs the exact format of information agents can retrieve, process, and update across your workflows.

By establishing explicit schema constraints, field definitions, and validation rules, Data Contracts ensure high reliability when agents interact with structured external data, eliminate ambiguity during automated document extraction, and allow data synchronization across multiple integrated systems.

This guide walks you through configuring a Data Contract to enable agents created in Builder Studio to work with your structured data.

---

## Before you begin

- Verify that your account has the Data Contract permission enabled. Ask your organization's administrator to grant access if the **Add Data Contract** button is missing from the designated pages.  
- Ensure that Salesforce or SharePoint is already integrated if you intend to link external data. Currently, these are the only supported integrations. Consult your administrator to complete the initial setup if neither platform is connected.

---

## Building the Data Contract

Data can be imported into a Data Contract using two primary methods:

1. Connect a system you already use, such as Salesforce or SharePoint, and Unframe AI OS syncs its fields automatically.   
2. Define the fields yourself manually or via document extraction.

---

## Creating a Data Contract

1. In the side navigation menu, click your profile avatar.  
2. Select **Manage account**.  
3. Select **Agentic data contracts** in your Settings menu.  
4. Click **Add Data Contract**.   
5. Select the relevant option: **Start from scratch** and **Import from integration**.

   ![Create a data contract](/platform/data-contract/images/01-create-new-contract.png)  
	

### Start from scratch

Select **Start from scratch** to define an entity manually.

1. Enter a name for your entity, for example Candidate or Invoice.

   ![Enter a name](/platform/data-contract/images/02-enter-name.png)

2. An entity is preloaded with an auto-generated UUID.   
   > **Note:**  
   You must add at least one field to it. before publishing.  
3. Click **Add entity** for each additional field needed.  
   > **Note:**  
   Unframe adds a unique ID field to every entity automatically. You don't need to add one yourself, and you can't edit it.  
4. Click **Add field** and select the relevant field type.  
5. Click the dropdown arrow on a field and click **Edit** to update the field name, field type, or add a description. 

   ![Edit the field](/platform/data-contract/images/03-edit-field.png)

6. When you are ready, click **Save and publish**.  
7. Confirm the action in the popup.

---

### Import from integration

Select **Import from integration** to sync an entity from a system you've already connected.

1. Select the integration you want to import from: **Salesforce** or **SharePoint**.  
2. Select the entity you want to sync, for example **Account** or **Contact**.  
3. Click **Save and publish**.

Fields within a synced entity inherit their names and data types directly from the source system. 

**Note:**  
Link fields carry no unique visual indicator and look identical to standard data fields (like text or numerical values), even when connecting to a separate record in the origin system.

---

## Apply column formatting

Once a field exists, you can control how it displays.

1. Open the field you want to format.  
2. Select a display option that matches its type.   
   - A true/false field can display as a checkbox or as text.   
   - A date field can display in several formats and can include a time and time zone.  
3. Click **Save** to apply the formatting.

---

## Relate two entities to each other

If your agents need to look up related records, for example matching an invoice to the account it belongs to, you create that link from the **Data contracts** page.

1. In the side navigation menu, click your profile avatar.  
2. Select **Manage account**.  
3. Select **Data contracts** in your Settings menu.  
4. Click **Add Data Contract**.  
5. In the **Contract Details** dialog box, enter a name for the new Data Contract, then click **Next**.  
6. In the **Data Fields** dialog box, define at least one field. Each field you add gets its own **Add Relation** link underneath it, so if you're adding several fields, add a relation under whichever specific field should hold the link.  
   * **Cell Renderer**: optional setting controlling non-plain text display in tables. Use supported names: `chip`, `status`, `dateTime`, `toggleSwitch`, `select`, `avatars`, `thumbnail`, `signedNumber`, `confidenceValue`, `labelWithIcon`, `lock`, `iconButton`, `inlineEdit`, `actionsMenu`, or `protectedName`. Unsupported names default to plain text.  
   * **Indexable**: toggle (off by default) that adds a database index to speed up filtering, sorting, or searching. Enable only for frequently queried fields to avoid unnecessary overhead.  
7. Click **Add Relation** under the field you want to link from.  
8. Select the **Related Data Contract**. This list includes every Data Contract in your organization, including ones synced from an integration.  
9. Select the **Related Field** on that Data Contract, the specific field you want this field to point to.  
10. Optional: Click **Add Another Relation** to link the same field to more than one Data Contract.  
11. Click **Next.**  
12. In the **Customize** dialog box, define how the Data Contract appears and what it allows:  
    * **Display Names**: enter a plural and a singular display name.  
    * **Permissions**: toggle on permissions for Readable, Editable, Creatable, Deletable, Multi Edit, and Multi Delete.   
    * **Columns Configuration**: three multi-select lists, each built from the fields you just defined: **Available Columns** (which fields can be shown at all), **Visible Columns** (which are shown by default), and **Relation Available Columns** (which fields can be used when another Data Contract relates to this one).  
    * **Field Pointers**: optional dropdowns for a **Title Field**, **Created Field**, and **Updated Field**, specifying which fields designate the record's primary title as well as its creation and update timestamps.  
    * **Item Details View**: enter a **Title Template** and **Subtitle Template** and **Drawer Width** in rem, controlling how a single record displays when opened.  
    * **Structure Sections**: Click **Add section** to organize fields into named groups.   
13. Once you're satisfied, click **Create Data Contract**.

Once your Data Contract is created and published, it's available to reference inside Builder Studio. The most direct connection is the **Document extraction** workflow step: when you configure it, you choose one or more of your published Data Contracts as the entity the extracted document data gets written into. Other workflow steps, such as LLM Agent, can also  read your Data Contract's data through a tool or connection you configure separately in Builder Studio.

