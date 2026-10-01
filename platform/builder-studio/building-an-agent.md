---
title: "Building an agent in Builder Studio"
---

Builder Studio is the canvas in Unframe AI OS where you build and publish your own AI agents. An agent is an automated workflow that carries out single or multiple tasks on its own, such as answering questions from a knowledge source, executing workflows and mini-applications for micro use-cases, running on a schedule, or connecting to another tool, without your engineering team building it for you. Builder Studio exists so any Builder-permissioned admin can assemble, test, and publish an agent directly from a visual canvas. This guide walks you through building and publishing an agent.

---

## Before you begin

You have Builder/admin access to your Unframe AI OS instance.

---

## Key concepts

A workflow consists of a single trigger followed by any configured steps, agentic tools, and MCP connections, all of which should be validated before publication.

These four primary concepts help you navigate the canvas and structure workflows effectively:

| Term | Definition |
| :---- | :---- |
| Trigger | The event that initiates a workflow run. Each agent requires exactly one trigger. |
| Step | An individual task within a workflow. Agents can incorporate multiple sequential steps. |
| Agentic tool | An existing published agent leveraged as a functional tool within a new workflow. |
| MCP connection | An integration enabling a workflow to interact with external services. |

## Ways to start building

Builder Studio presents three distinct building options. Choosing the correct path upfront ensures your canvas matches the intended agent structure.

**New Agent** opens an open-ended workflow canvas designed for sequential multi-step agents triggered by chat interactions or automated schedules.

**New Q\&A Agent** provides a specialized environment tailored specifically to conversational Q\&A patterns, featuring a streamlined Add Node panel suited for query handling.

**New Tool (MCP)** configures a reusable tool rather than a standalone agent, allowing it to be invoked by other agents as an MCP connection or agentic tool.

To select the right option, determine whether your goal is answering user queries, executing structured workflows, or providing functional utilities for other agents.

---

## Creating a new agent

1. In the side navigation menu, open **Builder Studio**.  
2. Click **Create**.  
3. Select [**New Workflow Agent**](#new-workflow-agent), [**New Q\&A Agent**](#new-q&a-agent), or [**New Tool (MCP)**](#new-tool-\(mcp\)).  
   Choosing the correct path upfront ensures your canvas matches the intended agent structure.

---

### New workflow agent {#new-workflow-agent}

Use this for a workflow with any combination of triggers, steps, tools, and MCP connections.

1. Enter a name for your agent.  
2. Click **Start building**.  
3. On the **Choose how to build your agent** screen, select one of:  
   1. The text field at the top, where you describe what your agent should do in your own words.  
   2. **Start from scratch**, which opens an empty canvas.  
   3. **Start with a Template**, which opens a library of prebuilt agent templates.

      ![Create a new agent](/platform/builder-studio/images/01-new-agent.png)

---

### New Q\&A Agent {#new-q&a-agent}

Use this for an agent whose only job is to answer questions in a chat conversation.

1. Enter a name for your agent on the **Set up your Q\&A agent** screen. You can rename it later.  
2. Click **Start building**.

New Q\&A Agent skips the **Choose how to build your agent** screen entirely. You land directly on a canvas that already has a **Chat** trigger and an **LLM Agent** step in place, and the canvas header shows a **Q\&A Agent** badge. Because the step type is fixed to a Q\&A pattern, the **Add node** panel on a Q\&A agent offers a narrower set of steps than a workflow agent built with New Agent.

You can integrate MCP connections and agentic tools to extend the LLM agent's capabilities and link to external data sources.

---

### New Tool (MCP) {#new-tool-(mcp)}

Register an MCP server as a tool other agents can call, rather than building an agent yourself. 

The MCP registry is set by an admin with Integration permissions. Once approved by an admin and added to the tenant registry, builders can use the MCP across workflows; without admin approval and inclusion in the registry, the tool or MCP cannot be utilized.

MCPs support both personal and global credentials. Personal access requires individual OAuth authentication when invoked, enabling team members to authenticate with their own credentials), whereas global access is configured at the workspace level by a builder, eliminating individual OAuth requirements.

1. In the side navigation menu, open **Builder Studio**.  
2. Click **Create**.  
3. Select **New tool (MCP)** to open the **Add MCP** dialog box.   
4. Enter the following details:  
1. **Name**.  
2. **URL**: Enter the server's endpoint.  
3. **Access:** Select an access level:  
   * **Private**: everyone who uses this MCP connects with their own credentials.  
   * **Shared**: individual runs use this one connection. Under **Authentication**, select the relevant option:  
     * **None**  
       * **API Key**: enter an API key  
         * **OAuth Authorization:** includes a collapsible **Advanced** section with an optional **Scopes** field  
         * **OAuth Credentials**:   
           * Enter **Client ID** and **Client Secret** fields  
           * Includes a collapsible **Advanced** section with an optional **Scopes** field  
4. Click **Save** (or **Connect**, for OAuth Authorization).  
     
   Once added, your new MCP will be listed in the **Tools & MCPs** tab in Builder Studio.  
   

    ![MCPs](/platform/builder-studio/images/02-mcps.png)

---

## Adding a trigger

A trigger is what starts your agent's workflow. 

1. In the side panel, select the relevant trigger: [Schedule](#schedule) or [Chat](#chat). 
![Select trigger](/platform/builder-studio/images/03-select-trigger.png)

#### Schedule  {#schedule}

Executes the agent using a custom cron expression or on a recurring basis. 

1. Configure the trigger's settings in the side panel.  
   
    ![Configure schedule](/platform/builder-studio/images/04-configure-schedule.png)

* Toggle **Active** on to activate the agent, or off to pause the trigger.   
* Select **Mode:**   
  * **Interval**: executes at specified intervals of days, hours, or minutes. Configure your preferred combination of **Days**, **Hours**, and **Minutes**; a preview display updates to show the chosen schedule (e.g., "Every 1 hour").  
  * **Weekly**: runs on specific days of the week. Select one or more **Days** (Sun through Sat) and set an **Hour** and **Minute**.  
  * **Custom cron**: enter a cron expression (for example, `0 */1 * * *`) in the **Cron expression** field; a preview shows the resulting schedule in plain language.  
  * **Schedule once**: fires a single time at a date and time you set in **Run at**.  
* Optional **Trigger input (JSON)**: Provide a JSON payload that is passed to the workflow each time the schedule executes. 

2. Click **Save** to save changes.

#### Chat {#chat}

Allow users to trigger the workflow directly from a chat session.

1. Configure the trigger's settings in the side panel.  
   
    ![Configure chat](/platform/builder-studio/images/05-configure-chat.png)

* **Validate chat input before run**: toggle on to ask users for any additional details needed prior to running.


* **Required items**: A list of specific details or parameters required prior to execution (e.g., user id, date range, or account number), entered either on separate lines or separated by commas.


* **Validation prompt**: guidelines for the LLM to assess if a chat request contains sufficient details to proceed.

To change a trigger type, select the **Action menu (···)** and select **Change trigger type**.  
![Change trigger](/platform/builder-studio/images/06-change-trigger.png)

#### Incoming email

Starts a workflow run when an email arrives in a connected mailbox via Outlook or Gmail integration.

#### Listen to a webhook

Triggers execution when an HTTP POST request is sent to the agent's dedicated URL, allowing external applications such as Salesforce, Typeform, Stripe, or custom tools to initiate a workflow directly.

#### Form

Replaces standard chat conversations with a defined intake form for initiating workflow executions. This setup is ideal for processes requiring a predefined, consistent set of inputs rather than unstructured user messages. 

In this initial release, forms support single submissions per run, are accessible exclusively within Work Hub (without external public link sharing), and do not include conditional logic across form fields.

#### Data contract trigger

When a row within a data contract table is created, updated, or deleted, this trigger initiates a workflow execution and routes the row's data to the subsequent step. Configuring this trigger involves selecting the target data contract table and specifying which event types (creation, update, or deletion) will initiate execution.

## Adding steps, agentic tools, and MCP connections

After setting up your trigger, build out your workflow:

1. Select the relevant node:

   - [**Steps**](#understanding-workflow-steps) serve as the baseline functional units within a workflow. Supported step types include **LLM Agent**, **AI summary**, **UI Block** (for rendering a natural-language output UI), **Human in the loop** (to pause execution for human review, input, or file uploads), **Send an email**, **HTTP Request**, and **Document extraction**. 

   - **Agentic tools** enable your workflow to invoke existing published agents, allowing the AI to determine how to utilize the resulting output.

   - **MCPs** facilitate integrations with external MCP servers. You can view all available servers linked to your workspace or click **Add MCP** to [integrate a new server connection](#heading=h.qbklid19h2j).

2. Configure it in the panel on the right.  
3. Repeat for each additional required node.

### Understanding workflow steps {#understanding-workflow-steps}

![Steps](/platform/builder-studio/images/07-steps.png)

#### LLM Agent

Setting up an LLM-driven agent step:

* **Instructions**: defines the task for the agent in this workflow step.   
    
  For example: Summarize all deals closed this week and highlight any risks.

* **Knowledge fabric access**: a searchable hierarchy of your workspace's data entities and fields.   
    
  Choose which entities this step can query:  
  * Picking a source automatically links the corresponding DB Access tool to execute queries.   
  * Use **Select All** or **Clear All** to update the entire tree simultaneously  
      
* **Inputs**: displays output data from preceding workflow steps available for reference. This remains empty until a prior step is added.  
    
* **Advanced**: an optional role or persona override for the agent.   
    
  For example: You are a loan onboarding specialist.

#### AI summary

Summarizes the output of prior steps using a prompt.

* **Prompt:** Specify the details and format for the AI summary.  
* **Inputs**: Toggle on which output data from preceding steps is accessible to the prompt by default. 

#### UI Block

Renders data from previous steps as a block, generated with AI or written by hand. 

1. Choose from two configuration modes:

* **AI mode** (default):  
  * **Template layout prompt**: define how the input data should be rendered visually (e.g., "a table listing all agents along with their name, status, and last modified date").  
  * Use the **Template preview** panel on the right to review the generated layout after providing your prompt.  
* **Coding mode**: write the layout manually instead of describing it, across four tabs: **HTML**, **CSS**, **JS**, and **Example** (a sample JSON payload used to preview your code against). A **Load files** button lets you upload .html, .css, .js, or .json files straight into the matching tab instead of typing them in.

2. **Inputs**: Toggle on which output data from preceding steps is accessible to the prompt by default.   
3. Click **Generate preview** to preview your template.

#### Human in the loop 

Temporarily halts workflow execution until a user provides approval, text feedback, or an uploaded document.

![Human in the loop](/platform/builder-studio/images/08-human-in-the-loop.png)

* Select what you need from the human under **Human action**:   
  * **Approval**: review and approve or reject  
    * **Yes label**: approve; continues the workflow  
    * **No label**: reject; stops the workflow  
  * **Text input**: replies to the human with a text response.  
  * **File input**: request a file upload; select the allowed file types and maximum file size.  
* Every mode includes a **Message to the reviewer** field.   
* **Context shown to human**: Specify which outputs from earlier steps are shared with the human reviewer.  
* **Who acts:** decides which person or group Builder Studio asks to complete the action.  
  * Select **Me as approver**, **Specific user**, or **Business role**.  
  * Choosing **Specific user** or **Business role** launches the **Actor settings** pane containing a **User** (or **Role**) menu, along with a **\+ Add escalation level** option. You can configure up to three escalation tiers, supporting a chain of four individuals overall. Each tier allows you to assign an alternate person or role to handle the request if the primary assignee is unresponsive. These configured tiers enable options within the **Timeout, rejection & failure** section (such as "escalate to backup approver"), which are unavailable when set to **Me as approver** due to the lack of alternate recipients.  
* **Timeout, rejection & failure**:  three dropdown menus covering:  
  * **If no response within**: 4h, 24h, 48h, 5 business days (escalates to backup approver), or no timeout.  
  * **If rejected**: re-route, stop with a rejection note, stop and notify applicant, or request submitter clarification.  
  * **If execution fails post-action**: retry then escalate to ops, fail and notify approver, leave for manual completion, or alert approver for guidance.  
* **Notify & wait through**: how Builder Studio reaches the human.   
  * **Unframe chat inbox** is on by default.   
  * **Email** and **Webhook** are currently unavailable.

#### Send an email 

Set up response templates and dynamic documentation.

* **Recipient (To)**: required. Add one or more email addresses.  
* **Sender (From)**: disabled. Defaults to Unframe.  
* **Reply to**: optional.  
* **Prompt**: required. Specifies the content the AI needs to generate for the email message. Select **Add Example** to provide the AI with a sample email template.  
* **Inputs**: toggle on which output data from preceding steps is accessible to the prompt by default. 

Toggle on **Active** to activate this step.

#### HTTP Request

Calls an HTTP endpoint and maps the response into this workflow step.

* **Request**  
  * **Method**: select from the dropdown menu  
  * **URL**: required. If you type or paste a URL that already has a query string (like ?status=open\&id=123), Builder Studio splits it automatically: the base URL stays in this field and each name=value pair appears as its own row under **Send query parameters**. The reverse also happens — editing the rows below updates this field to match once you click away from it.  
  * The **Preview Request** button is disabled until the request is configured.  
* **Authentication:** an **Authentication method** dropdown with five options, each revealing its own fields:  
  * **None** — no authentication fields.  
  * **API Key** — **Key**, **Value**, and **Add to** (**Header** or **Query params**).  
  * **Bearer Token** — a single **Token** field.  
  * **Basic Auth** — **Username** and **Password**.  
  * **OAuth Credentials** — **Client ID** and **Client Secret**, plus an **Advanced settings** section with **Token URL** and **Scopes**.  
  * **OAuth Authorization** — shows a **Create account** button, but it's disabled with a tooltip explaining this flow is coming soon. Don't offer it to end users yet.  
* **Send query parameters**  
  * Select the Specify query parameters from the dropdown menu  
  * Click **\+ Add query parameter** to add additional parameters.  
* **Send headers** :   
  * Toggle on to reveal the header fields, the same fields-or-JSON choice as query parameters.  
  * Select headers from the dropdown menu.  
* **Send body**.   
  * Toggle on display the body fields, the same fields-or-JSON choice, and is unavailable for methods that don't send a body (like GET).  
* **Request advanced options**: a collapsible section with:  
  * **Timeout** — **Fixed** (a number of milliseconds) or **Expression** (a value resolved at runtime), plus **Items per batch** and **Batch interval (ms)** for requests that run once per item.  
  * **Response** — two checkboxes, **Include response headers and status** and **Never error** (treat a failed request as a normal result instead of stopping the workflow).  
  * **Format** — how to parse the response: **Detected automatically**, **JSON**, or **Text**.  
  * **Array format in query** — how array values are written into the URL's query string: **No brackets**, **Brackets only**, or **Brackets with indices**.  
* **Inputs**: Toggle on which output data from preceding steps is accessible to the prompt by default. 


A newly added HTTP Request step starts with its **Active** toggle off. Once you fill in the required fields and Builder Studio can run it, it turns Active back on for you automatically.

#### Document extraction

Extracts uploaded documents and lets you define the extraction schema.

* **Required confidence score**: a slider and percentage field (0–100%, defaulting to 90%) setting the minimum extraction confidence needed for the step to succeed.  
* **Who acts?**: decide who reviews an extraction that falls below the confidence score. Select **Me as approver**, **Specific user**, or **Business role**.  
  * Choosing **Specific user** or **Business role** launches the **Actor settings** pane containing a **User** (or **Role**) menu, along with a **\+ Add escalation level** option. You can configure up to three escalation tiers, supporting a chain of four individuals overall. Each tier allows you to assign an alternate person or role to handle the request if the primary assignee is unresponsive. These configured tiers enable options within the **Timeout, rejection & failure** section (such as "escalate to backup approver"), which are unavailable when set to **Me as approver** due to the lack of alternate recipients.  
* **Choose data contracts**: your workspace's data contracts, split into **Connected** and **Available**:  
  * Under **Available**, each data contract shows how many entities it exposes and a **Select** button to connect it and choose which entities and fields to import.  
  * Once connected, a data contract moves to **Connected**, showing how many entities are selected out of the total. Its **Action menu (···)** offers **Manage** (change which entities and fields are imported), **Edit data contract** (edit the underlying data contract itself), and **Disconnect**.  
  * If a connected data contract is later deleted from Settings, it shows here as **Data contract no longer available** with a prompt to disconnect it and keep the step valid.  
* If the data contract you need isn't listed, click **Click here** to add an entity.

#### Branch

Branch is a node that splits a workflow into multiple paths based on conditions you define. 

1. Open the Branch node's config panel. It starts empty with "No branches set".  
2. Under **Condition inputs**, choose which prior step's output the conditions should be evaluated against (for example, the output of an AI summary step earlier in the workflow). Only one input source can be toggled on at a time.  
3. Click **\+ Add branch** to open the Add branch dialog:
![Branch](/platform/builder-studio/images/09-branch.png)
   * **Type**: build a condition. Select a field from the prior step's output, an operator (e.g. Equals), and a value to compare against.   
   * **\+ Add condition**: add another condition to the same branch; multiple conditions are combined with AND/OR logic.  
   * **Then go to**: from the dropdown menu, select which node this branch leads to if its conditions match. Only downstream nodes already on the canvas (or a new node you create from this picker) are valid destinations; you cannot route a branch back to an earlier node in the workflow.  
   * Click **Save branch** to add it.  
4. Repeat for each additional branch. Each one you add appears in the Branches list with its condition summary and destination.  
5. Toggle the node to **Active** once your branches are configured and you're ready for this step to run.

**Note:** A branch with no conditions blocks the workflow from being tested or published.

#### Loopback

A branch's target isn't limited to downstream nodes; you can also route a branch back to an earlier node in the same workflow. This repeats the flow from that node, which is how you build a retry or re-check loop. For example: validate a field, and if it fails, loop back to the extraction step before trying again.

**Note:** There's no separate "Loop" node: looping is a routing choice within Branch, not a distinct step type.

---

## Working with the canvas

You're not limited to adding nodes at the end of your workflow. Builder Studio's canvas supports rearranging, inserting, and removing nodes directly.

* **Insert a step between two existing steps.** Hover over the connecting line between two nodes. A **\+** button and a trash icon appear on the line. Click **\+** to open the **Add node** panel and insert a new step at that point in the workflow.  
* **Delete a step.** Open the step's panel and select **Delete** from its **...** menu, or click the trash icon on its connecting line. Deleting a step from its panel removes the step but doesn't reconnect the nodes on either side of it, so you'll see the steps that were connected to it left floating, with no line between them.  
* **Reconnect a floating step.** Drag from the connection point on one node to the connection point on another to draw a new line between them.  
* **Move a step.** Drag it to a new position on the canvas.  
* **Turn a step on or off.** Use the **Active** toggle on the step's card directly on the canvas; you don't need to open its panel.  
* **Resize your view of the canvas.** Use the zoom controls (or scroll) in the bottom-right corner.  
* **Move around the canvas.** Drag with the hand/pan tool.

Builder Studio permits only a single step panel to be open at any given moment. If you attempt to click **Add node** in the toolbar while a step panel remains open, the button will be disabled, displaying the tooltip "Adding a node is already in progress". Close the open panel to re-enable it, or hover over a connecting line to click the **\+** icon remains functional at all times.

---

## Testing an agent

Before you publish, confirm your workflow behaves the way you expect.

1. Navigate to the **Test** tab located at the top of the canvas.  
2. Provide a sample query in the message box and submit it.  
     
   **Example scenario**: If you are setting up an invoice extractor to verify details against your CRM, try entering: "I received an invoice from Acme Supplies for \$4,250.00 (Invoice \#INV-2026-0917). Extract the vendor, amount, and invoice number, then check whether Acme Supplies is an active vendor in the CRM."

3. Evaluate the generated output.  
4. Select **Show agent profile** to inspect the complete execution trace.

    ![Test agent](/platform/builder-studio/images/10-test-agent.png)

5. The agent will execute your instructions and present its reply directly within the chat window.  
6. Inside the agent profile, you can review the overall Status (e.g., Success) alongside a sequential list of executed Steps. Expanding a step reveals its specific details and output.   
   For example: a Human in the loop step includes the submitted message, attached files, reviewer details, and timestamps.  
7. Once you are satisfied, select **Next**.  
8. If adjustments are needed, select **Build** to return to the canvas editor.

---

## Publishing an agent

Publishing instantly deploys your agent. 

**Note:**   
Ensure to re-test your workflow before proceeding: 

- There is no review process or confirmation prompt before going live.   
- Unpublishing or undoing changes after publishing isn’t currently supported.


1. Verify that you are satisfied with the workflow configuration and test outcomes.  
2. Select **Publish**.

After publication, your active agent will appear under the **Available** tab in Builder Studio marked as **Published**. You can monitor its status, clone it, or [manage access permissions](#assigning-access-to-a-published-agent) at any time via its **Action menu (···)**.  

![Publish agent](/platform/builder-studio/images/11-publish-agent.png)

---

## Assigning access to a published agent {#assigning-access-to-a-published-agent}

Control who can see and use a published agent. Only the agent's owner can grant or revoke others' access or delete the agent; any editor can duplicate it.

1.  Locate the published agent in the Builder studio **Available** list.  
2. Click its **Action menu (···).**  
3. Select **Assign access**.  
4. The Assign access dialog box displays a list of users or groups already granted access, each with their permission level. Click the dropdown arrow to change permissions or remove access.

    ![Assign access](/platform/builder-studio/images/12-assign-access.png)

5. Search for a specific user or group by name in the search bar and click **Invite** to add them. They're added to the list below with **Viewer** access by default.  
6. Below the invite list, a toggle switches between:  
* **Restricted**: only the people/groups explicitly listed above can access the agent.  
* **Public** (everyone): anyone can access it, regardless of the list above.  
  ![Restricted](/platform/builder-studio/images/13-restricted.png)
7. Click **Save changes** to apply.

---

## Changing a published agent

If you need to make a change, duplicate it. Editing a published agent directly isn’t supported.

1. Locate the published agent in the Builder studio **Available** list.  
2. Click its **Action menu (···).**  
3. Select **Duplicate**.  
4. Enter a name for the copy.  
5. Click **Duplicate**.  
6. Make the required changes to the duplicate.  
7. Publish when ready.

Publishing the duplicate creates a new, separate agent. It doesn't create a new version of the original, and it doesn't affect the original's published status.

---

## FAQ

**Can I undo a publish?**   
No. Publishing is immediate and permanent. To change a published agent, duplicate it, edit the copy, and publish that instead.

**Why can't I add another node right now?**   
Builder Studio only shows one step's settings panel open at a time. Close the one that's open, and you'll be able to add the next node.

**What's the difference between New Agent and New Q\&A Agent?**   
New Q\&A Agent is built specifically for a chat-answering pattern. New Agent opens a more flexible canvas with a wider set of options, for building a workflow that isn't just answering questions.

**Can I edit a published agent?**   
Not directly. Duplicate it, make your changes on the copy, and publish the copy. That creates a new agent rather than a new version of the one you started with.

---

