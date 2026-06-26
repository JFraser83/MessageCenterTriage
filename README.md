# Message Center Triage Agent

This guide outlines the requirements and setup steps for deploying the **Message Center Triage Agent** in Copilot Studio.

## Requirements

Before setting up the agent, ensure you have:

1. A Power Platform environment with Dataverse
2. Copilot Studio credits or pay-as-you-go configured  
   > This agent is autonomous.
3. Message Center sync to Planner configured

## Set Up Planner

> Take note of the Microsoft 365 Group and Planner plan name. You will need these values in later steps.

The Planner plan should include the following buckets:

- Informational
- Low
- Medium
- High
- Critical

## Set Up Message Center Sync to Planner

> **Warning:** If you are setting this up as a new sync, the 28-day option can take a long time. The 7-day option is recommended.

Reference: [Track message center tasks in Planner - Microsoft Planner](https://learn.microsoft.com/ener-syncing

When adding Planner sync, choose the **To-do** bucket as the default bucket.

## Add the Agent to Your Environment

1. Navigate to https://copilotstudio.microsoft.com.
2. Select your Power Platform environment on the right-hand side.
3. Select the three dots on the left navigation menu.
4. Choose **Solutions**.
5. Import the `MessageCenterTriage.zip` solution file.
6. Open the included **Workload Assignment** Excel file.
7. Update the product owners.
8. Save the file.
9. Navigate to https://make.powerapps.com.
10. Go to **Tables**.
11. Select the `MCTeamAssignments` table.
12. Select **Import**.
13. Choose **Import data from Excel**.
14. Select the Excel file updated in step 7.
15. Ensure the `Product` and `Owner` fields are mapped correctly.
16. Navigate back to Copilot Studio.
17. Select the **Message Center Triage Agent**.

## Configure Agent Tools

In Copilot Studio, navigate to **Tools** and update the `MessageCenterPlanner` tool with the Microsoft 365 Group and Planner plan name from the initial setup.

Update the following tools:

### GetPlannerBuckets

Update the `GetPlannerBuckets` tool with:

- Group name
- Plan name

### Get Plan Details

Update the `Get Plan Details` tool with the Planner plan ID.

The plan ID can be found by opening the plan in Planner. The plan ID is included in the Planner URL.

### ListWorkloadAssignments

Validate that the `ListWorkloadAssignments` tool is configured correctly.

It should show:

- Environment: `Current`
- Table name: `MCTeamAssignments`

After validating the tools, save and publish the changes.

## Optional: Roadmap MCP

The agent includes one optional MCP server connection. This connection can be deleted if you do not want to use it.

Reference: https://learn.microsoft.com/en-us/microsoft-365/admin/manage/mrc-mcp?view=o365-worldwide

## Test the Agent

At this point, the agent should be configured and ready to use.

If Planner sync is configured and Message Center posts are available in Planner, you can prompt the agent to triage a post.

Example prompts:

```text
Help me triage MC1309733
