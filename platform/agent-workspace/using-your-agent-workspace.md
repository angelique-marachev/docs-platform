---
title: "Using your Agent Workspace"
---

The Agent Workspace serves as your central hub in Unframe AI OS to discover, manage, and execute agents. 

![The agent workspace](/platform/agent-workspace/images/01-agent-workspace.png)

It features a comprehensive list of all agents accessible to you. Within the workspace, you can browse available options, inspect individual agent details, and pin your favorites for quick access. Pinning an agent saves it to your personal set, making it accessible directly from your chat sidebar so you can bypass catalog searches.

This guide covers how to explore the workspace catalog, pin essential agents, engage with them directly through Chat, and manage pending requests using your Inbox.

---

## Before you begin

- You need an Unframe AI OS account with access to at least one agent.   
- Admin permissions govern which agents are visible in your Workspace. By managing roles and groups, your organization's admin controls access and shares agents when they are ready. The agents displayed in your Workspace directly correspond to the permissions configured for you or your team.

---

## Key concepts

| Term | Definition |
| :---- | :---- |
| Agent Workspace | The page where you browse and pin the agents available to you. |
| Pin | Adding an agent to your personal set from the Workspace. A pinned agent appears in your chat sidebar and counts toward the badge there. |
| Inbox | The section inside your Chat panel where agents that need your approval or input leave items for you to act on. |

---

## Role of the Agent Workspace in your workflow

Explore the Agent Workspace to discover and pin the required agents. After pinning them, execute your routine tasks using those agents straight from Chat. The Workspace is for discovery and setup; Chat is where you run agents day-to-day.

---

## Pinning an agent

1. In the side navigation menu, open **Agent Workspace**.  
2. Use the search bar to find an agent by name or description, or scroll through the list.  
3. Select an agent  to open its details.

    ![Agent details side panel](/platform/agent-workspace/images/02-open-agent-details.png)

4. Click **Connect agent**. The agent is added to your pinned set in Char, and a green dot appears on its card to indicate it is pinned.

    ![A pinned agent](/platform/agent-workspace/images/03-pinned.png)

If you no longer need an agent pinned, open its details and click **Disconnect** to remove it from your set. This doesn't affect the agent itself, only your personal list.

---

## Running a pinned agent

1. You can run a pinned agent two ways:  
   * **From the Agent Workspace:** In the Agent Workspace, click a pinned agent to open its details panel and click Run agent. You're redirected to **Chat**.  
   * **From Chat**: In the side navigation menu, open **Chat**.  
2. Click the agent dropdown at the bottom of the chat window and select the pinned agent from the list.

    ![Select agent in chat](/platform/agent-workspace/images/04-select-agent.png)

3. Enter your message in plain language and send it. The agent responds in the conversation the same way the default assistant does. Learn more about [Chat](#using-chat).

If the agent you selected requires a connection you haven't set up yet, such as access to a data source, a dialog box appears requesting you to complete the setup before the conversation continues. When the setup is complete, the agent picks up where it left off; you don't need to re-select the agent or start over.

---

## Using Chat {#using-chat}

Chat is where you work with agents once they're pinned. It has three parts: 

* The left sidebar listing **New chat**, your **Inbox**, and your past conversations  
* The input composer at the bottom where you type and send messages.   
  This section includes the following:  
- The text input field  
- The agent dropdown selector  
- The AI model selector  
- An attachment button for adding a file to the conversation for contex  
  Additionally, each response an agent gives you can be rated, copied, or have its underlying query shown, so you can see what the agent actually did to produce the answer.  
* The conversation pane where the conversation with an agent takes place

A conversation saves automatically as you go; there's no separate save step. You can return to it later from the sidebar, or start a new one at any time with **New chat**.

### Receiving notifications to your Inbox

If an agent requires your confirmation or additional input, such as filling out a form or validating a value before proceeding, it will temporarily pause its execution. A notification will appear as an actionable item in your Chat **Inbox**. 

![Chat Inbox](/platform/agent-workspace/images/05-inbox.png)

To allow the agent to resume its task, open the notification and submit the requested details or approval.

